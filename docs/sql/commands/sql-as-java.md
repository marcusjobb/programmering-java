---
title: "SQL som Java-kod"
description: "Varje SQL-kommando bredvid samma sak skriven i Java: INSERT blir add, SELECT blir en for-loop, WHERE blir if."
parent: "SQL-kommandon"
nav_order: 111
---

# SQL som Java-kod

Kan du Java? Då har du redan gjort det mesta vi gör i SQL, fast med listor, loopar och `if`. Här ställer vi dem bredvid varandra: *det här SQL-kommandot gör det här, och det är som om vi hade skrivit så här i Java.*

Exemplen bygger vidare på hjältarna i [Din första databas](../first-database.md).

## 1. Tabellen = en klass + en lista

I SQL beskriver vi hur en rad ser ut och skapar en tom tabell:

```sql
CREATE TABLE "People" (
    "Id"    INTEGER NOT NULL,
    "Name"  TEXT NOT NULL,
    "City"  TEXT,
    PRIMARY KEY("Id" AUTOINCREMENT)
);
```

I Java beskriver klassen hur *en* rad ser ut, och listan är själva tabellen. Liknelsen mellan tabell och klass går vi igenom mer i [Från tabell till klass](tables-and-classes.md).

```java
class People {
    private final int id;
    private final String name;
    private String city;

    People(int id, String name, String city) {
        this.id = id;
        this.name = Objects.requireNonNull(name, "name får inte vara null");
        this.city = city;
    }

    int getId() { return id; }
    String getName() { return name; }
    String getCity() { return city; }
    void setCity(String city) { this.city = city; }
}
```

```java
List<People> people = new ArrayList<>();
```

| SQL | Java |
|---|---|
| Kolumn | Fält med getter |
| Rad | Objekt |
| Tabell | `List<People>` |
| `TEXT NOT NULL` | `String` + `requireNonNull` |
| `TEXT` (får vara `NULL`) | `String` som får vara `null` |

## 2. INSERT = add

```sql
INSERT INTO People (Name, City) VALUES
    ('Clark Kent', 'Metropolis'),
    ('Bruce Wayne', 'Gotham City');
```

är som:

```java
people.add(new People(1, "Clark Kent", "Metropolis"));
people.add(new People(2, "Bruce Wayne", "Gotham City"));
```

Lägg märke till `id`. I SQL sköter `AUTOINCREMENT` numreringen åt oss. Listan i Java har ingen aning om att `id` ska vara unikt, så där får vi hålla koll själva.

## 3. SELECT * = for-loop

```sql
SELECT * FROM People;
```

är som att gå igenom hela listan och skriva ut varje rad:

```java
for (People p : people)
    System.out.println(p.getId() + " " + p.getName() + " " + p.getCity());
```

## 4. WHERE = if

```sql
SELECT Name FROM People WHERE Name LIKE 'Clark%';
```

är som en loop med ett `if` i:

```java
for (People p : people)
    if (p.getName().startsWith("Clark"))
        System.out.println(p.getName());
```

`%` betyder "vad som helst". Var `%` står avgör vilken Java-metod det motsvarar:

| SQL | Java | Hittar |
|---|---|---|
| `LIKE 'Clark%'` | `startsWith("Clark")` | Namn som *börjar* på Clark |
| `LIKE '%Kent'` | `endsWith("Kent")` | Namn som *slutar* på Kent |
| `LIKE '%Clark%'` | `contains("Clark")` | Namn som *innehåller* Clark var som helst |
| `= 'Clark Kent'` | `.equals("Clark Kent")` | Exakt det namnet |

> **Skillnad:** `LIKE` i SQLite bryr sig inte om stora och små bokstäver, så `'clark%'` hittar också Clark. `startsWith` i Java gör skillnad på dem.

> **Fälla:** Jämför aldrig texter med `==` i Java. `==` kollar om det är *samma objekt*, inte om texten är densamma. Använd `.equals()`.

## 5. LIMIT 1 = findFirst

Vill vi bara ha den *första* som matchar:

```sql
SELECT Name FROM People WHERE Name LIKE 'Clark%' LIMIT 1;
```

är som:

```java
String sup = people.stream()
        .filter(p -> p.getName().startsWith("Clark"))
        .map(People::getName)
        .findFirst()
        .orElse(null);
System.out.println(sup);
```

`findFirst` slutar leta så fort den hittar en träff, precis som `LIMIT 1`. Hittar den ingen får vi `null` från `orElse(null)`.

Lägg märke till hur strömmen läses nästan som SQL: `filter` är `WHERE`, `map` väljer kolumn som `SELECT Name`, och `findFirst` är `LIMIT 1`.

## 6. UPDATE = loop + if + setter

```sql
UPDATE People SET City = 'Metropolis' WHERE Name = 'Bruce Wayne';
```

är som:

```java
for (People p : people)
    if (p.getName().equals("Bruce Wayne"))
        p.setCity("Metropolis");
```

`WHERE` är `if`-satsen och `SET` är settern. Glömmer du `if` i Java får *alla* Metropolis som stad. Glömmer du `WHERE` i SQL händer exakt samma sak.

## 7. Så varför inte bara använda en lista?

| | `List<People>` i Java | Tabell i en databas |
|---|---|---|
| **Var bor datan?** | I minnet. Borta när programmet stängs. | I en fil. Finns kvar tills du raderar den. |
| **Unika `id`** | Du får hålla koll själv | `AUTOINCREMENT` sköter det |
| **Regler** | Bara det du själv kodar | `NOT NULL`, `UNIQUE`, `CHECK`, främmande nycklar |
| **Hur du frågar** | Du skriver *hur* den ska leta: loop, `if`, utskrift | Du skriver *vad* du vill ha, och databasen räknar ut hur |
| **Flera användare** | Ett program åt gången | Många program och användare samtidigt |

Den viktigaste raden är *hur* kontra *vad*. I Java skriver vi loopen själva. I SQL beskriver vi bara resultatet vi vill ha.

## Hela programmet

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Objects;

public class Main {
    public static void main(String[] args) {
        System.out.println("Hello, SQL!");

        // CREATE TABLE
        List<People> people = new ArrayList<>();

        // INSERT INTO People (Name, City) VALUES (...), (...);
        people.add(new People(1, "Clark Kent", "Metropolis"));
        people.add(new People(2, "Bruce Wayne", "Gotham City"));

        // SELECT * FROM People;
        for (People p : people)
            System.out.println(p.getId() + " " + p.getName() + " " + p.getCity());

        // SELECT Name FROM People WHERE Name LIKE 'Clark%';
        for (People p : people)
            if (p.getName().startsWith("Clark"))
                System.out.println(p.getName());

        // SELECT Name FROM People WHERE Name LIKE 'Clark%' LIMIT 1;
        String sup = people.stream()
                .filter(p -> p.getName().startsWith("Clark"))
                .map(People::getName)
                .findFirst()
                .orElse(null);
        System.out.println(sup);

        // UPDATE People SET City = 'Metropolis' WHERE Name = 'Bruce Wayne';
        for (People p : people)
            if (p.getName().equals("Bruce Wayne"))
                p.setCity("Metropolis");
    }
}

class People {
    private final int id;
    private final String name;
    private String city;

    People(int id, String name, String city) {
        this.id = id;
        this.name = Objects.requireNonNull(name, "name får inte vara null");
        this.city = city;
    }

    int getId() { return id; }
    String getName() { return name; }
    String getCity() { return city; }
    void setCity(String city) { this.city = city; }
}
```

## TL;DR

| SQL | Java |
|---|---|
| `CREATE TABLE` | `class` + `new ArrayList<>()` |
| `INSERT INTO` | `.add()` |
| `SELECT *` | `for (People p : people)` |
| `WHERE` | `if` |
| `LIKE 'Clark%'` / `'%Kent'` / `'%Clark%'` | `startsWith` / `endsWith` / `contains` |
| `LIMIT 1` | `.stream().filter(...).findFirst()` |
| `UPDATE ... SET ... WHERE` | loop + `if` + setter |

En lista lever i minnet och försvinner när programmet stängs. En databas sparar datan, håller koll på reglerna och låter dig fråga efter *vad* du vill ha i stället för att skriva *hur* den ska leta.
