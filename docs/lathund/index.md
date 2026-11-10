---
title: Lathund
description: "Snabbreferenser för Java: datatyper, kontrollflöde, samlingar, databaser och verktyg. Kort och strukturerat, med länkar till kapitlen för den grundliga genomgången."
author: Marcus Ackre Medina
parent: Java
nav_order: 990
has_children: true
---
# Lathund

Snabbreferenser för det du behöver när du skriver kod. Sidorna är ordnade efter bokens kapitel, så den som följer boken hittar rätt direkt. Vill du förstå något grundligt, gå till kapitlet som sidan länkar till.

## Datatyper

Grunderna för variabler och värden.

| Sida | Vad den täcker |
|------|----------------|
| [Variabler](variables.md) | Snabbreferens för hur du deklarerar, initierar och använder variabler i Java. |
| [Heltal (int)](integers.md) | Snabbreferens för heltalstypen int i Java: omvandling, aritmetik, jämförelser och vanliga fallgropar. |
| [Decimaltal](decimals.md) | Snabbreferens för decimaltal i Java: double, float och BigDecimal, omvandling, avrundning och vanliga fallgropar. |
| [Boolean](booleans.md) | Snabbreferens för typen boolean i Java: sant och falskt, jämförelser, logiska operatorer och vanliga fallgropar. |
| [String](strings.md) | Snabbreferens för String i Java: längd, sökning, delsträngar, ersättning, delning och jämförelse av innehåll. |
| [Datatyper](datatypes.md) | Översikt över Javas datatyper: primitiva typer, referenstyper, omfång och exempel på deklaration. |

## Kontrollflöde

Villkor och loopar, från enklast till mest omfattande.

| Sida | Vad den täcker |
|------|----------------|
| [If](if.md) | if, else if och else i Java: syntax, jämförelseoperatorer, skillnaden mot flera if i rad och vanliga misstag. |
| [Switch](switch.md) | switch i Java: switch-sats med break, switch-sats med pilar och switch-uttryck (Java 14+), samt skillnaden mot if. |
| [While](while.md) | while-loopen i Java: syntax, break och continue, nästlade loopar, oändliga loopar och vanliga misstag. |
| [Do-while](do-while.md) | do-while-loopen i Java: syntax, skillnaden mot while, break och continue samt vanliga misstag. |
| [For](for.md) | for-loopen i Java: syntax med initiering, villkor och steg, nästlade loopar, break och continue, samt for-each. |

## Samlingar

Arrayer, listor och andra samlingar.

| Sida | Vad den täcker |
|------|----------------|
| [Arrayer](arrays.md) | Arrayer i Java: skapa, läsa, ändra, sortera och kopiera med hjälp av klassen Arrays. |
| [List och ArrayList](list.md) | List och ArrayList i Java: skapa, lägga till, ta bort, söka, sortera och loopa. |
| [LinkedList](linked-list.md) | LinkedList i Java: lägga till och ta bort i början och slutet, hämta element och när den är bättre än ArrayList. |
| [Dictionary (Map och HashMap)](dictionary.md) | Map och HashMap i Java: nyckel-värde-par, sök med nyckel, loopa och varför Java inte kallar det Dictionary. |
| [HashSet](hashset.md) | HashSet i Java: unika element, snabb sökning med contains, och varför ordningen inte är garanterad. |
| [Stack](stack.md) | Stack i Java: LIFO med push, pop och peek, med Deque och ArrayDeque som rekommenderat val. |
| [Queue](queue.md) | Queue i Java: FIFO med offer, poll och peek, och skillnaden mellan metoder som returnerar null och metoder som kastar undantag. |

## Databaser

JDBC, JPA med Hibernate och dokumentdatabaser.

| Sida | Vad den täcker |
|------|----------------|
| [JDBC med SQLite](jdbc-sqlite.md) | JDBC med SQLite: Connection, PreparedStatement, CRUD, transaktioner och seeding utan ORM. |
| [JPA och Hibernate](jpa-hibernate.md) | JPA och Hibernate: entiteter, SessionFactory, CRUD, transaktioner, relationer och seeding med SQLite. |
| [MongoDB](mongodb.md) | MongoDB i Java: Docker, Atlas, Compass, konfiguration, CRUD, transaktioner med replica set och seeding. |

## Verktyg och arbetssätt

Git, kommandotolken, markdown och Scrum.

| Sida | Vad den täcker |
|------|----------------|
| [Git](git-quickguide.md) | Git: att skapa och klona ett repository, arbeta med grenar, skicka upp ändringar, ångra och hantera fjärrrepositoryn. |
| [Git Flow](git-flow.md) | Git Flow: branchstrukturen main, develop och feature-grenar, pull requests, hotfix och de vanligaste kommandona. |
| [Kommandotolken](command-line.md) | Kommandotolken (cmd) i Windows: navigering, filhantering, filsökning, systeminformation, nätverk och användarkonton. |
| [Markdown](markdown.md) | Markdown för README-filer och dokumentation i Java-projekt: rubriker, listor, länkar, tabeller och kodblock. |
| [Scrum](scrum.md) | Scrum: roller, artefakter, events, estimering och user stories med tabeller. |

## Konfiguration i JSON

Databaslathundarna läser connection strings från `config.json`. Lösenord hör inte hemma i filen. De kommer från miljövariabler:

```json
{
  "ConnectionStrings": {
    "Sqlite": "jdbc:sqlite:webshop.db",
    "MongoLocal": "mongodb://localhost:27017"
  }
}
```

Sätt variabeln i terminalen innan du startar programmet, till exempel `MONGO_ATLAS`.
