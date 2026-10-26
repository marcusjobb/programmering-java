---
title: "MySQL i Java"
description: "Från tom Java-applikation till en MySQL-databas med JDBC: anslutning, CREATE TABLE, INSERT och SELECT steg för steg."
parent: "SQL"
nav_order: 50
---

# MySQL i Java

**Verktyg:** Java 21, Maven, JDBC med MySQL Connector/J, MySQL (t.ex. via Docker)

Nu ansluter vi till MySQL från Java med **JDBC** (Java Database Connectivity) — Javas standardgränssnitt för databaser. Principen är densamma oavsett databas: vi skickar SQL och läser svaret. Skillnaden mot SQLite är att vi ansluter via nätverket med en URL, användare och lösenord.

> **Behöver du MySQL?** Enklaste sättet är via Docker. Se [MySQL med Docker](mysql-docker.md) för hur du startar en container med ett kommando.

---

## 1. Skapa projektet

Vi döper projektet till `MySQL_Live`.

**I terminalen (Maven):**

```bash
mvn archetype:generate \
  -DgroupId=se.nionit \
  -DartifactId=MySQL_Live \
  -DarchetypeArtifactId=maven-archetype-quickstart \
  -DinteractiveMode=false
cd MySQL_Live
```

**I IntelliJ IDEA:**
*New Project* → **Maven** → döp projektet till `MySQL_Live` → `se.nionit` som Group ID → *Create*.

**I VS Code:**
Installera *Extension Pack for Java* → öppna *Command Palette* → `Java: Create Java Project` → **Maven** → välj `maven-archetype-quickstart`.

---

## 2. Lägg till beroende

Lägg till MySQL Connector/J i `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>com.mysql</groupId>
        <artifactId>mysql-connector-j</artifactId>
        <version>8.3.0</version>
    </dependency>
</dependencies>
```

Kör sedan:

```bash
mvn install
```

---

## 3. JDBC-URL

En JDBC-URL berättar var databasen finns:

```java
String url      = "jdbc:mysql://localhost:3306/produkter";
String user     = "root";
String password = "root";
```

| Del | Vad det betyder |
|-----|-----------------|
| `jdbc:mysql://` | JDBC-protokoll + MySQL-driver |
| `localhost:3306` | Server och port (3306 är MySQL:s standard) |
| `produkter` | Vilken databas vi vill ansluta till |

---

## 4. Anslut till databasen

```java
import java.sql.*;

String url      = "jdbc:mysql://localhost:3306/produkter";
String user     = "root";
String password = "root";

try (Connection conn = DriverManager.getConnection(url, user, password)) {
    System.out.println("Ansluten till MySQL!");
}
```

`try-with-resources` stänger anslutningen automatiskt — vi behöver inte anropa `conn.close()` manuellt. Om lösenordet är fel kastas ett `SQLException`.

---

## 5. Skapa tabellen — CREATE TABLE

```java
String createSql = """
    CREATE TABLE IF NOT EXISTS produkter (
        Id         INT AUTO_INCREMENT PRIMARY KEY,
        Namn       VARCHAR(200) NOT NULL,
        Pris       DECIMAL(10,2) NOT NULL,
        Lagersaldo INT DEFAULT 0
    )
    """;

try (Statement stmt = conn.createStatement()) {
    stmt.executeUpdate(createSql);
    System.out.println("Tabell skapad (eller fanns redan).");
}
```

`IF NOT EXISTS` gör att vi kan köra programmet flera gånger utan felmeddelande om tabellen redan finns.

`executeUpdate` kör SQL-kommandon som inte returnerar rader — CREATE TABLE, INSERT och UPDATE passar här.

---

## 6. Lägg till produkter — INSERT

```java
String insertSql = "INSERT INTO produkter (Namn, Pris, Lagersaldo) VALUES (?, ?, ?)";

try (PreparedStatement ps = conn.prepareStatement(insertSql)) {
    ps.setString(1, "Tangentbord");
    ps.setBigDecimal(2, new BigDecimal("649.00"));
    ps.setInt(3, 12);
    ps.executeUpdate();

    ps.setString(1, "Mus");
    ps.setBigDecimal(2, new BigDecimal("299.00"));
    ps.setInt(3, 24);
    ps.executeUpdate();

    ps.setString(1, "Skärm");
    ps.setBigDecimal(2, new BigDecimal("3499.00"));
    ps.setInt(3, 5);
    ps.executeUpdate();

    System.out.println("Tre produkter tillagda.");
}
```

`?` är parametrar — vi skriver aldrig in värden direkt i SQL-strängen. Det skyddar mot SQL injection och är alltid rätt sätt att göra det.

`setString(1, ...)` — parametrar är 1-indexerade i Java (inte 0 som i arrayer).

---

## 7. Läs produkterna — SELECT

```java
String selectSql = "SELECT Id, Namn, Pris, Lagersaldo FROM produkter ORDER BY Pris DESC";

try (Statement stmt    = conn.createStatement();
     ResultSet  rs     = stmt.executeQuery(selectSql)) {

    System.out.println();
    System.out.printf("%-5s %-20s %12s  %6s%n", "Id", "Namn", "Pris", "Lager");
    System.out.println("─".repeat(48));

    while (rs.next()) {
        int        id    = rs.getInt("Id");
        String     namn  = rs.getString("Namn");
        BigDecimal pris  = rs.getBigDecimal("Pris");
        int        lager = rs.getInt("Lagersaldo");

        System.out.printf("%-5d %-20s %12.2f  %6d%n", id, namn, pris, lager);
    }
}
```

`executeQuery` returnerar ett `ResultSet`. `rs.next()` returnerar `true` för varje rad och `false` när det inte finns fler — perfekt för en `while`-loop.

Vi hämtar värden per kolumnnamn med `getString`, `getInt` och `getBigDecimal`. Det är tydligare och säkrare än att hämta på index.

**Output:**

```
Id    Namn                       Pris   Lager
────────────────────────────────────────────────
3     Skärm                  3499,00       5
1     Tangentbord             649,00      12
2     Mus                     299,00      24
```

---

## 8. Hela Main.java

```java
import java.math.BigDecimal;
import java.sql.*;

public class Main {
    public static void main(String[] args) throws SQLException {
        String url      = "jdbc:mysql://localhost:3306/produkter";
        String user     = "root";
        String password = "root";

        try (Connection conn = DriverManager.getConnection(url, user, password)) {
            System.out.println("Ansluten till MySQL!");

            // CREATE TABLE
            try (Statement stmt = conn.createStatement()) {
                stmt.executeUpdate("""
                    CREATE TABLE IF NOT EXISTS produkter (
                        Id         INT AUTO_INCREMENT PRIMARY KEY,
                        Namn       VARCHAR(200) NOT NULL,
                        Pris       DECIMAL(10,2) NOT NULL,
                        Lagersaldo INT DEFAULT 0
                    )
                    """);
            }
            System.out.println("Tabell klar.");

            // INSERT
            String insertSql = "INSERT INTO produkter (Namn, Pris, Lagersaldo) VALUES (?, ?, ?)";
            Object[][] produkter = {
                {"Tangentbord", new BigDecimal("649.00"),  12},
                {"Mus",         new BigDecimal("299.00"),  24},
                {"Skärm",      new BigDecimal("3499.00"),   5},
            };

            try (PreparedStatement ps = conn.prepareStatement(insertSql)) {
                for (Object[] p : produkter) {
                    ps.setString(1, (String) p[0]);
                    ps.setBigDecimal(2, (BigDecimal) p[1]);
                    ps.setInt(3, (int) p[2]);
                    ps.executeUpdate();
                }
            }
            System.out.println("Produkter tillagda.");

            // SELECT
            try (Statement stmt = conn.createStatement();
                 ResultSet  rs  = stmt.executeQuery(
                     "SELECT Id, Namn, Pris, Lagersaldo FROM produkter ORDER BY Pris DESC")) {

                System.out.println();
                System.out.printf("%-5s %-20s %12s  %6s%n", "Id", "Namn", "Pris", "Lager");
                System.out.println("─".repeat(48));

                while (rs.next()) {
                    System.out.printf("%-5d %-20s %12.2f  %6d%n",
                        rs.getInt("Id"),
                        rs.getString("Namn"),
                        rs.getBigDecimal("Pris"),
                        rs.getInt("Lagersaldo"));
                }
            }
        }
    }
}
```

> **Nästa steg:** i [MySQL med DbHandler](mysql-handler-java.md) flyttar vi databaskoden till en egen klass och håller `Main.java` ren.
