---
title: Lathund
author: Marcus Ackre Medina
description: "Snabbreferens för databaser i Java: JDBC med SQLite, JPA och Hibernate samt MongoDB. Installation, konfiguration, CRUD, transaktioner och seeding på ett ställe."
parent: Java
nav_order: 990
has_children: true
---
# Lathund

Här samlar vi det du behöver när du jobbar med databaser i Java. Varje sida har samma upplägg: installation, konfiguration, CRUD, transaktioner, seeding och terminologi.

| Sida | Vad den täcker |
|------|----------------|
| [JPA och Hibernate](jpa-hibernate.md) | ORM: entiteter, sessioner, HQL, relationer och seeding |
| [JDBC med SQLite](jdbc-sqlite.md) | Lägsta lagret: du skriver SQL och hanterar anslutningen själv |
| [MongoDB](mongodb.md) | Dokumentdatabas: Docker, Atlas, Compass, CRUD och transaktioner |

Grunderna finns i [Databaser](../orm/index.md) och [SQL](../sql/index.md).

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

---

Samma innehåll finns för C#, med Entity Framework Core, ADO.NET och MongoDB C#-drivern.
