---
title: "Lathund: JPA och Hibernate"
author: Marcus Ackre Medina
description: "JPA och Hibernate i lathundsform: entiteter, SessionFactory, CRUD, transaktioner, relationer och seeding med SQLite."
parent: Lathund
nav_order: 10
---
# Lathund: JPA och Hibernate

JPA är standarden för objekt-relationsmappning i Java. Hibernate är den vanligaste implementationen. Du markerar klasserna med annoteringar, och Hibernate skriver SQL:en åt dig. Motsvarigheten i C#-boken är Entity Framework Core.

## Dependencies

Lägg till i `pom.xml`:

```xml
<dependency>
    <groupId>org.hibernate.orm</groupId>
    <artifactId>hibernate-core</artifactId>
    <version>7.4.15.Final</version>
</dependency>
<dependency>
    <groupId>org.hibernate.orm</groupId>
    <artifactId>hibernate-community-dialects</artifactId>
    <version>7.4.15.Final</version>
</dependency>
<dependency>
    <groupId>org.xerial</groupId>
    <artifactId>sqlite-jdbc</artifactId>
    <version>3.54.1.0</version>
</dependency>
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.23.0</version>
</dependency>
```

`hibernate-community-dialects` behövs för SQLite. SQLite-dialekten ligger inte i `hibernate-core`. Versionerna är de senaste stabila när sidan skrevs. Kontrollera senaste version på Maven Central innan du startar.

## Entitet

```java
import jakarta.persistence.*;

@Entity
@Table(name = "products")
public class Product {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(length = 100, nullable = false)
    private String name;

    private double price;

    protected Product() {
        // JPA kräver en tom konstruktor
    }

    public Product(String name, double price) {
        this.name = name;
        this.price = price;
    }

    public Long getId() { return id; }
    public String getName() { return name; }
    public double getPrice() { return price; }
    public void setPrice(double price) { this.price = price; }
}
```

`@Entity` markerar klassen som en tabell. `@Id` och `@GeneratedValue` ger den primärnyckel. `@Column` styr längd och om fältet får vara tomt.

## Konfiguration och SessionFactory

```java
Configuration configuration = new Configuration()
        .addAnnotatedClass(Product.class)
        .setProperty("hibernate.connection.driver_class", "org.sqlite.JDBC")
        .setProperty("hibernate.connection.url", url)
        .setProperty("hibernate.dialect", "org.hibernate.community.dialect.SQLiteDialect")
        .setProperty("hibernate.hbm2ddl.auto", "update");

SessionFactory factory = configuration.buildSessionFactory();
```

`url` är värdet från `config.json`. `hbm2ddl.auto=update` skapar eller uppdaterar tabellerna när programmet startar. I riktiga projekt använder man migrationer i stället.

Stäng factory när programmet avslutas:

```java
// Tänk på att lägga till try/catch där något kan gå fel
factory.close();
```

## CRUD

En `Session` är en arbetsyta. Ändringar görs inom en transaktion som du startar och avslutar:

```java
try (Session session = factory.openSession()) {
    Transaction tx = session.beginTransaction();

    // Create
    session.persist(new Product("Kaffe", 49.0));

    tx.commit();
}
```

```java
try (Session session = factory.openSession()) {
    // Read med primärnyckel
    Product produkt = session.get(Product.class, 1L);

    // Read med HQL, Hibernates frågespråk
    List<Product> billiga = session
            .createQuery("from Product p where p.price < :max", Product.class)
            .setParameter("max", 100.0)
            .getResultList();
}
```

```java
try (Session session = factory.openSession()) {
    Transaction tx = session.beginTransaction();

    // Update: hämta, ändra och commit. Hibernate ser ändringen själv
    Product kaffe = session.createQuery("from Product p where p.name = :namn", Product.class)
            .setParameter("namn", "Kaffe")
            .getSingleResult();
    kaffe.setPrice(39.0);

    tx.commit();
}
```

```java
try (Session session = factory.openSession()) {
    Transaction tx = session.beginTransaction();

    // Delete
    Product kaffe = session.get(Product.class, 1L);
    session.remove(kaffe);

    tx.commit();
}
```

Hibernate ser att fältet ändrats när sessionen commitas. Du behöver inget `save()` eller `update()`.

## Transaktioner

En transaktion omsluter alla operationer i en `Session`. Rollback ångrar allt:

```java
try (Session session = factory.openSession()) {
    Transaction tx = session.beginTransaction();
    try {
        Product kaffe = session.get(Product.class, 1L);
        kaffe.setPrice(kaffe.getPrice() - 5.0);
        session.persist(new Order("Kaffe"));
        tx.commit();
    } catch (RuntimeException e) {
        tx.rollback();
        throw e;
    }
}
```

Samma idé som i [JDBC med SQLite](jdbc-sqlite.md). Hibernate skriver SQL:en, men transaktionen är din.

## Relationer

Relationer uttrycks med annoteringar i klasserna:

```java
@Entity
public class Order {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @ManyToOne
    @JoinColumn(name = "product_id", nullable = false)
    private Product product;

    protected Order() { }

    public Order(Product product) {
        this.product = product;
    }
}
```

Den motsatta sidan i `Product`:

```java
@OneToMany(mappedBy = "product")
private List<Order> orders = new ArrayList<>();
```

För specialfall, till exempel vad som händer med barnraderna när föräldern tas bort, använder du en annotering som styr databasen direkt:

```java
@ManyToOne(fetch = FetchType.LAZY)
@OnDelete(action = OnDeleteAction.CASCADE)
@JoinColumn(name = "product_id", nullable = false)
private Product product;
```

`CASCADE` gör att databasen tar bort ordrarna när produkten tas bort. Utan annoteringen måste du ta bort dem själv i koden, eller hindra borttagningen.

## Seeding

Fyll tabellen bara om den är tom:

```java
try (Session session = factory.openSession()) {
    Transaction tx = session.beginTransaction();

    Long antal = session.createQuery("select count(p) from Product p", Long.class)
            .getSingleResult();

    if (antal == 0) {
        session.persist(new Product("Kaffe", 49.0));
        session.persist(new Product("Te", 35.0));
    }

    tx.commit();
}
```

Anropa seedern en gång när programmet startar, efter att factoryn skapats.

## Terminologi

| Term | Betydelse |
|------|-----------|
| **Entitet** | En klass som Hibernate kan spara och läsa |
| **SessionFactory** | Skapas en gång per databas. Dyr att skapa |
| **Session** | Arbetsytan för en uppsättning operationer |
| **Dirty checking** | Hibernate jämför objekten med det som lästes och skriver bara ändringar |
| **HQL** | Hibernates frågespråk, som SQL men med klassnamn och egenskaper |
| **Dialect** | Det som anpassar SQL:en till en viss databas |

## Tips och tricks

- Entiteter ska ha en tom `protected`-konstruktor. JPA kräver den.
- Håll sessionen kort. Öppna den, gör jobbet och stäng den.
- `getSingleResult()` kastar ett undantag om raden saknas eller det finns flera. Använd `getResultList()` när det kan vara fler.
- Lagra pengar som `BigDecimal` i riktiga program. `double` kan ge avrundningsfel.
- Lösenord ligger i miljövariabler, aldrig i `config.json` som ligger i git.
