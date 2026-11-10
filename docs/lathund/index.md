---
title: Lathund
author: Marcus Ackre Medina
description: "Snabbreferens för databaser i Java: JDBC med SQLite, JPA och Hibernate samt MongoDB. Installation, konfiguration, CRUD, transaktioner och seeding på ett ställe."
parent: Java
nav_order: 990
has_children: true
---
# Lathund

Här samlar vi snabbreferenser för det du använder mest i Java: datatyper, kontrollflöde, samlingar, git och databaser. Sidorna är i ordning efter bokens kapitel, så de nya längst upp hör ihop med kapitlen före dem.

| Sida | Vad den täcker |
|------|----------------|
| [Variabler](variables.md) | Deklaration, typer och namngivning |
| [Heltal](integers.md) | `int`, `long`, parsning och överflöde |
| [Decimaltal](decimals.md) | `double`, `float`, `BigDecimal` |
| [Booleans](booleans.md) | `boolean` och logiska operatorer |
| [Strängar](strings.md) | `String`-metoder och jämförelser |
| [Datatyper](datatypes.md) | Översikt över primitiva typer och deras storlek |
| [If](if.md) | Villkor och if-satser |
| [Switch](switch.md) | Switch-satsen och switch-uttryck |
| [While](while.md) | While-loopar |
| [Do-while](do-while.md) | Loopar som körs minst en gång |
| [For](for.md) | For-loopar och for-each |
| [Arrayer](arrays.md) | Arrayer med fast storlek |
| [List](list.md) | `List` och `ArrayList` |
| [Länkad lista](linked-list.md) | `LinkedList` |
| [Map](dictionary.md) | `Map`, `HashMap` och nyckel-värde-par |
| [HashSet](hashset.md) | Mängder utan dubbletter |
| [Stack](stack.md) | Stack med `Deque` |
| [Queue](queue.md) | Kö med `Queue` och `ArrayDeque` |
| [Git-snabbguide](git-quickguide.md) | Vanliga git-kommandon |
| [Git Flow](git-flow.md) | Branchstruktur och PR-flöde |
| [Kommandotolken](command-line.md) | Windows-kommandotolken |
| [Markdown](markdown.md) | Formatering för README och dokumentation |
| [Scrum](scrum.md) | Roller, artefakter och events |
| [JPA och Hibernate](jpa-hibernate.md) | ORM: entiteter, sessioner, HQL, relationer och seeding |
| [JDBC med SQLite](jdbc-sqlite.md) | Lägsta lagret: du skriver SQL och hanterar anslutningen själv |
| [MongoDB](mongodb.md) | Dokumentdatabas: Docker, Atlas, Compass, CRUD och transaktioner |

Databas-sidorna ligger längst ner i listan. Grunderna finns i [Databaser](../orm/index.md) och [SQL](../sql/index.md).

## Konfiguration i JSON

Alla lathundar läser connection strings från `config.json`. Lösenord hör inte hemma i filen. De kommer från miljövariabler.

```json
{
  "ConnectionStrings": {
    "Sqlite": "jdbc:sqlite:webshop.db",
    "MongoLocal": "mongodb://localhost:27017",
    "MongoAtlas": "mongodb+srv://<användarnamn>:<lösenord>@<kluster>.mongodb.net/?retryWrites=true&w=majority"
  }
}
```

Läs filen med Jackson:

```java
ObjectMapper mapper = new ObjectMapper();
JsonNode config = mapper.readTree(new File("config.json"));
String url = config.get("ConnectionStrings").get("Sqlite").asText();
```

Lösenordet läser du från en miljövariabel, så det aldrig hamnar i git:

```java
String atlasUrl = System.getenv("MONGO_ATLAS");
```

Sätt variabeln i terminalen innan du startar programmet.
