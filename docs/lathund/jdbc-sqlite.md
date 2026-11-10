---
title: "Lathund: JDBC med SQLite"
author: Marcus Ackre Medina
description: "JDBC med SQLite i lathundsform: Connection, PreparedStatement, CRUD, transaktioner och seeding utan ORM."
parent: Lathund
nav_order: 20
---
# Lathund: JDBC med SQLite

JDBC är Javas lägsta lager mot databaser. Du skriver SQL själv och hanterar anslutningen själv. Hibernate bygger på samma sak bakom kulisserna. Se även [SQL](../sql/index.md).

## Dependency

```xml
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

SQLite behöver ingen server. Driverjaren innehåller allt.

## Connection string

I `config.json`:

```json
{
  "ConnectionStrings": {
    "Sqlite": "jdbc:sqlite:webshop.db"
  }
}
```

Läs den:

```java
ObjectMapper mapper = new ObjectMapper();
JsonNode config = mapper.readTree(new File("config.json"));
String url = config.get("ConnectionStrings").get("Sqlite").asText();
```

SQLite har inget lösenord. Filen skapas första gången anslutningen öppnas.

## Skapa tabellen

```java
// Tänk på att lägga till try/catch där något kan gå fel
try (Connection connection = DriverManager.getConnection(url);
     Statement statement = connection.createStatement()) {

    statement.execute("""
        CREATE TABLE IF NOT EXISTS Products (
            Id    INTEGER PRIMARY KEY AUTOINCREMENT,
            Name  TEXT    NOT NULL,
            Price REAL    NOT NULL
        )
        """);
}
```

Textblock med `"""` gör SQL:en lättare att läsa.

## CRUD

Mönstret är alltid detsamma: öppna anslutningen, skapa en `PreparedStatement`, kör den och läs resultatet. Frågetecken (`?`) markerar parametrar.

```java
try (Connection connection = DriverManager.getConnection(url)) {

    // Create
    try (PreparedStatement insert = connection.prepareStatement(
            "INSERT INTO Products (Name, Price) VALUES (?, ?)")) {
        insert.setString(1, "Kaffe");
        insert.setDouble(2, 49.0);
        int antal = insert.executeUpdate();
    }

    // Read
    try (PreparedStatement select = connection.prepareStatement(
            "SELECT Id, Name, Price FROM Products WHERE Price < ?")) {
        select.setDouble(1, 100.0);
        try (ResultSet rs = select.executeQuery()) {
            while (rs.next()) {
                System.out.println(rs.getInt("Id") + " " + rs.getString("Name") + " " + rs.getDouble("Price"));
            }
        }
    }

    // Update
    try (PreparedStatement update = connection.prepareStatement(
            "UPDATE Products SET Price = ? WHERE Name = ?")) {
        update.setDouble(1, 39.0);
        update.setString(2, "Kaffe");
        update.executeUpdate();
    }

    // Delete
    try (PreparedStatement delete = connection.prepareStatement(
            "DELETE FROM Products WHERE Name = ?")) {
        delete.setString(1, "Kaffe");
        delete.executeUpdate();
    }
}
```

`rs.next()` går till nästa rad och returnerar `false` när det inte finns fler. Det betyder inte att något gått fel.

## Parametrar

Bygg aldrig SQL genom att klistra ihop strängar med värden från användaren. Det öppnar för SQL-injektion. Med `PreparedStatement` skickas värdena separat, och de tolkas aldrig som SQL. Mer om det finns i SQL-injektion.

```java
try (PreparedStatement ps = connection.prepareStatement(
        "SELECT Id, Name, Price FROM Products WHERE Name = ?")) {
    ps.setString(1, inmatatNamn);
    try (ResultSet rs = ps.executeQuery()) {
        // ...
    }
}
```

## Transaktioner

JDBC kör som standard varje sats i en egen transaktion. Stäng av det, gör ändringarna och commit eller rollback:

```java
try (Connection connection = DriverManager.getConnection(url)) {
    connection.setAutoCommit(false);
    try (Statement statement = connection.createStatement()) {
        statement.executeUpdate("UPDATE Products SET Price = Price - 5 WHERE Name = 'Kaffe'");
        statement.executeUpdate("INSERT INTO Orders (ProductName) VALUES ('Kaffe')");
        connection.commit();
    } catch (SQLException e) {
        connection.rollback();
        System.out.println("Ändringen ångrades: " + e.getMessage());
    }
}
```

Glöm inte `setAutoCommit(false)`. Utan det är varje sats redan sparad innan `rollback` anropas.

## Seeding

Kontrollera först om tabellen är tom. Skriv startdatan i en transaktion:

```java
try (Connection connection = DriverManager.getConnection(url)) {
    int antal;
    try (Statement check = connection.createStatement();
         ResultSet rs = check.executeQuery("SELECT COUNT(*) FROM Products")) {
        rs.next();
        antal = rs.getInt(1);
    }

    if (antal == 0) {
        connection.setAutoCommit(false);
        try (PreparedStatement insert = connection.prepareStatement(
                "INSERT INTO Products (Name, Price) VALUES (?, ?)")) {
            insert.setString(1, "Kaffe");
            insert.setDouble(2, 49.0);
            insert.executeUpdate();

            insert.setString(1, "Te");
            insert.setDouble(2, 35.0);
            insert.executeUpdate();
        }
        connection.commit();
    }
}
```

## Hjälpmedel och IDE

| Verktyg | Hur du använder det |
|---------|---------------------|
| **DB Browser for SQLite** | Öppna `webshop.db`. Fliken *Browse Data* visar tabellerna. Ladda ner från sqlitebrowser.org. |
| **IntelliJ IDEA** | *Database*-panelen → *+* → *Data Source* → *SQLite*. Ange filen `webshop.db`. |
| **VS Code** | Installera tillägget *SQLite* av alexcvzz. |

## Terminologi

| Term | Betydelse |
|------|-----------|
| **Connection** | Anslutningen till databasen. Stäng den när du är klar |
| **Statement** | En SQL-sats utan parametrar |
| **PreparedStatement** | En SQL-sats med parametrar, säker mot SQL-injektion |
| **ResultSet** | Raderna som en fråga gav, som läses framåt |
| **executeUpdate** | Kör en sats som inte returnerar rader |
| **Transaction** | Flera ändringar som lyckas eller ångras tillsammans |

## Tips och tricks

- Använd alltid `PreparedStatement` när värdet kommer från användaren.
- Använd try-with-resources. Då stängs anslutningen, satsen och resultatet automatiskt.
- `SELECT COUNT(*)` ger ett enda värde. Läs det med `rs.next()` och `rs.getInt(1)`.
- Radera `webshop.db` om du vill börja om från början.
