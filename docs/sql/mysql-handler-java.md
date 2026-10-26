---
title: "MySQL med DbHandler"
description: "Flytta MySQL-koden till en separat klass och håll Main.java ren — samma projekt som förut, bättre struktur."
parent: "SQL"
nav_order: 55
---

# MySQL med DbHandler

**Verktyg:** Java 21, Maven, JDBC med MySQL Connector/J, MySQL (t.ex. via Docker)

I [MySQL i Java](mysql-java.md) lade vi all kod direkt i `Main.java`. Det fungerar för enkla program, men när antalet frågor växer blir filen rörig. Lösningen är att flytta all databaskod till en **separat klass** — en `DbHandler`.

`Main.java` vet ingenting om hur SQL fungerar. Den ber `DbHandler` om data och litar på att det funkar.

---

## 1. Projektstruktur

Vi utgår från samma projekt (`MySQL_Live`) och lägger till tre filer:

```
MySQL_Live/
└── src/main/java/se/nionit/
    ├── Main.java       ← bara logik
    ├── DbHandler.java  ← all databaskod
    └── Produkt.java    ← datamodell
```

---

## 2. Datamodell — Produkt.java

```java
package se.nionit;

import java.math.BigDecimal;

public record Produkt(int id, String namn, BigDecimal pris, int lagersaldo) {}
```

En Java `record` är en oföränderlig dataklass — perfekt för rader vi läser från databasen. Kompilatorn genererar konstruktor, getters, `equals`, `hashCode` och `toString` automatiskt.

---

## 3. DbHandler.java — skelettet

```java
package se.nionit;

import java.sql.*;
import java.math.BigDecimal;
import java.util.*;

public class DbHandler {

    private final String url;
    private final String user;
    private final String password;

    public DbHandler(String url, String user, String password) {
        this.url      = url;
        this.user     = user;
        this.password = password;
    }

    private Connection getConnection() throws SQLException {
        return DriverManager.getConnection(url, user, password);
    }
}
```

Connection-uppgifterna sparas i konstruktorn. `getConnection()` öppnar en ny anslutning — varje publik metod använder den och stänger den via `try-with-resources`.

---

## 4. Skapa tabellen — createTable

```java
public void createTable() throws SQLException {
    try (Connection conn = getConnection();
         Statement  stmt = conn.createStatement()) {
        stmt.executeUpdate("""
            CREATE TABLE IF NOT EXISTS produkter (
                Id         INT AUTO_INCREMENT PRIMARY KEY,
                Namn       VARCHAR(200) NOT NULL,
                Pris       DECIMAL(10,2) NOT NULL,
                Lagersaldo INT DEFAULT 0
            )
            """);
    }
}
```

`createTable` skapar tabellen om den inte finns. `IF NOT EXISTS` gör att vi kan anropa den varje gång programmet startar utan att det kraschar.

---

## 5. Lägg till en produkt — addProduct

```java
public void addProduct(String namn, BigDecimal pris, int lagersaldo) throws SQLException {
    String sql = "INSERT INTO produkter (Namn, Pris, Lagersaldo) VALUES (?, ?, ?)";
    try (Connection      conn = getConnection();
         PreparedStatement ps = conn.prepareStatement(sql)) {
        ps.setString(1, namn);
        ps.setBigDecimal(2, pris);
        ps.setInt(3, lagersaldo);
        ps.executeUpdate();
    }
}
```

Parametrar (`?`) skyddar mot SQL injection. Värden skrivs aldrig direkt in i SQL-strängen.

---

## 6. Hämta alla produkter — getProducts

```java
public List<Produkt> getProducts() throws SQLException {
    var result = new ArrayList<Produkt>();
    String sql = "SELECT Id, Namn, Pris, Lagersaldo FROM produkter ORDER BY Pris DESC";

    try (Connection conn = getConnection();
         Statement  stmt = conn.createStatement();
         ResultSet  rs   = stmt.executeQuery(sql)) {

        while (rs.next()) {
            result.add(new Produkt(
                rs.getInt("Id"),
                rs.getString("Namn"),
                rs.getBigDecimal("Pris"),
                rs.getInt("Lagersaldo")
            ));
        }
    }
    return result;
}
```

Metoden returnerar en `List<Produkt>`. `Main.java` slipper veta vad `ResultSet` är — det är ett implementationsdetalj som stannar i `DbHandler`.

---

## 7. Hela DbHandler.java

```java
package se.nionit;

import java.math.BigDecimal;
import java.sql.*;
import java.util.*;

public class DbHandler {

    private final String url;
    private final String user;
    private final String password;

    public DbHandler(String url, String user, String password) {
        this.url      = url;
        this.user     = user;
        this.password = password;
    }

    private Connection getConnection() throws SQLException {
        return DriverManager.getConnection(url, user, password);
    }

    public void createTable() throws SQLException {
        try (Connection conn = getConnection();
             Statement  stmt = conn.createStatement()) {
            stmt.executeUpdate("""
                CREATE TABLE IF NOT EXISTS produkter (
                    Id         INT AUTO_INCREMENT PRIMARY KEY,
                    Namn       VARCHAR(200) NOT NULL,
                    Pris       DECIMAL(10,2) NOT NULL,
                    Lagersaldo INT DEFAULT 0
                )
                """);
        }
    }

    public void addProduct(String namn, BigDecimal pris, int lagersaldo) throws SQLException {
        String sql = "INSERT INTO produkter (Namn, Pris, Lagersaldo) VALUES (?, ?, ?)";
        try (Connection      conn = getConnection();
             PreparedStatement ps = conn.prepareStatement(sql)) {
            ps.setString(1, namn);
            ps.setBigDecimal(2, pris);
            ps.setInt(3, lagersaldo);
            ps.executeUpdate();
        }
    }

    public List<Produkt> getProducts() throws SQLException {
        var result = new ArrayList<Produkt>();
        String sql = "SELECT Id, Namn, Pris, Lagersaldo FROM produkter ORDER BY Pris DESC";

        try (Connection conn = getConnection();
             Statement  stmt = conn.createStatement();
             ResultSet  rs   = stmt.executeQuery(sql)) {

            while (rs.next()) {
                result.add(new Produkt(
                    rs.getInt("Id"),
                    rs.getString("Namn"),
                    rs.getBigDecimal("Pris"),
                    rs.getInt("Lagersaldo")
                ));
            }
        }
        return result;
    }
}
```

---

## 8. Main.java — ren och tydlig

```java
package se.nionit;

import java.math.BigDecimal;
import java.sql.SQLException;

public class Main {
    public static void main(String[] args) throws SQLException {
        var db = new DbHandler(
            "jdbc:mysql://localhost:3306/produkter",
            "root",
            "root"
        );

        db.createTable();

        db.addProduct("Tangentbord", new BigDecimal("649.00"),  12);
        db.addProduct("Mus",         new BigDecimal("299.00"),  24);
        db.addProduct("Skärm",      new BigDecimal("3499.00"),   5);

        System.out.printf("%-5s %-20s %12s  %6s%n", "Id", "Namn", "Pris", "Lager");
        System.out.println("─".repeat(48));

        for (Produkt p : db.getProducts()) {
            System.out.printf("%-5d %-20s %12.2f  %6d%n",
                p.id(), p.namn(), p.pris(), p.lagersaldo());
        }
    }
}
```

`Main.java` vet nu inte ens att det finns en MySQL-databas bakom — det är exakt den separation vi vill ha.

---

## C# vs Java — samma mönster, annan syntax

| Koncept | C# | Java |
|---------|-----|------|
| Anslutning | `MySqlConnection` | `DriverManager.getConnection` |
| Parametrar | `@namn` | `?` |
| Sätta parameter | `AddWithValue("@namn", ...)` | `setString(1, ...)` |
| Läsa rad | `reader.GetString("Namn")` | `rs.getString("Namn")` |
| Stänga resurser | `using var` | `try-with-resources` |
| Datamodell | tuple / record | `record` (Java 16+) |

Principen är identisk. Syntaxen skiljer sig — men om du förstår en, förstår du den andra.
