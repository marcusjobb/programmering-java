---
title: Tabeller
author: Marcus Ackre Medina
parent: SQL
nav_order: 10
---
# Tabeller

I Detta avsnitt utforskar vi de spännande skillnaderna i hanteringen av tabeller mellan tre populära databassystem - SQL Server, SQLite och MySQL. Vi kommer att fokusera på hur varje system skiljer sig åt när det gäller att skapa och hantera tabeller, samt användningen av primärnycklar och främmande nycklar. Låt oss dyka in i dessa skillnader och upptäcka hur varje databassystem erbjuder unika egenskaper inom tabellhantering!

## TL;DR

- SQL Server, SQLite och MySQL är olika databassystem som används för att hantera tabeller och data.
- Skillnaderna ligger i syntax och stöd för olika funktioner.
- SQL Server erbjuder en mäktig och omfattande hantering av tabeller, perfekt för företagsanvändning.
- SQLite är en lättviktig databasmotor som är perfekt för inbyggda system eller små applikationer.
- MySQL är ett populärt databassystem som är plattformsoberoende och används ofta för webbapplikationer.

## Vad är Databastabeller?

Databastabeller är som rutnät av data som lagras i en databas. Varje tabell består av kolumner och rader, där varje kolumn representerar en specifik datatyp och varje rad innehåller en post med värden för varje kolumn. Tabeller används för att organisera och strukturera data på ett sätt som gör det lätt att läsa och manipulera.

## Skillnader i Tabellskapande

### SQL Server

För att skapa en tabell i SQL Server använder vi följande syntax:

```sql
CREATE TABLE tableName (
    column1 dataType1 constraints,
    column2 dataType2 constraints,
);
```

### SQLite

För att skapa en tabell i SQLite använder vi en liknande syntax, men SQLite är mer flexibelt med datatyper:

```sql
CREATE TABLE tableName (
    column1 dataType1 constraints,
    column2 dataType2 constraints,
);
```

### MySQL

I MySQL används också liknande syntax för att skapa en tabell:

```sql
CREATE TABLE tableName (
    column1 dataType1 constraints,
    column2 dataType2 constraints,
);
```

Skillnader i syntax är små, men det är viktigt att notera att vissa datatyper och funktioner kan variera beroende på vilket system du använder.

## Hantering av Primärnycklar

### SQL Server

I SQL Server definieras en primärnyckel på följande sätt:

```sql
CREATE TABLE tableName (
    primaryKeyColumn dataType constraints PRIMARY KEY,
);
```

### SQLite

I SQLite definieras en primärnyckel på följande sätt:

```sql
CREATE TABLE tableName (
    primaryKeyColumn dataType constraints,
    PRIMARY KEY (primaryKeyColumn)
);
```

### MySQL

I MySQL definieras en primärnyckel på liknande sätt som i SQL Server:

```sql
CREATE TABLE tableName (
    primaryKeyColumn dataType constraints,
    PRIMARY KEY (primaryKeyColumn)
);
```

## Hantering av Främmande Nycklar

### SQL Server

I SQL Server definieras en främmande nyckel genom att ange CONSTRAINT och FOREIGN KEY på följande sätt:

```sql
CREATE TABLE tableName (
    foreignKeyColumn dataType constraints,
    CONSTRAINT FK_name FOREIGN KEY (foreignKeyColumn) REFERENCES referenceTable (referenceColumn)
);
```

### SQLite

SQLite stödjer också främmande nycklar, men de är inte lika strikta som i SQL Server. Här är hur en främmande nyckel kan definieras:

```sql
CREATE TABLE tableName (
    foreignKeyColumn dataType constraints REFERENCES referenceTable (referenceColumn)
);
```

### MySQL

I MySQL används liknande syntax för att definiera en främmande nyckel som i SQL Server:

```sql
CREATE TABLE tableName (
    foreignKeyColumn dataType constraints,
    FOREIGN KEY (foreignKeyColumn) REFERENCES referenceTable (referenceColumn)
);
```

## Exempelkod - Tabellen "cars"

Här är ett exempel som visar hur tabellen "cars" kan skapas för varje databassystem:

### SQL Server

```sql
CREATE TABLE cars (
    CarId INT PRIMARY KEY,
    Model VARCHAR(30) NOT NULL,
    Brand VARCHAR(50)
);
```

### SQLite

```sql
CREATE TABLE cars (
    CarId INTEGER PRIMARY KEY,
    Model TEXT NOT NULL,
    Brand TEXT
);
```

### MySQL

```sql
CREATE TABLE cars (
    CarId INT AUTO_INCREMENT PRIMARY KEY,
    Model VARCHAR(30) NOT NULL,
    Brand VARCHAR(50)
);
```

## Summan av kardemumman

Skillnaderna i hantering av tabeller mellan SQL Server, SQLite och MySQL är huvudsakligen relaterade till syntax och stöd för olika funktioner. SQL Server erbjuder en mäktig och omfattande hantering av tabeller, vilket gör det till ett utmärkt val för företagsanvändning. SQLite är en lättviktig databasmotor som är perfekt för inbyggda system eller små applikationer på grund av dess minimala krav på systemresurser. MySQL, å andra sidan, är ett populärt databassystem som är plattformsoberoende och används ofta för webbapplikationer på grund av dess höga prestanda och skalbarhet.

Fortsätt utforska dessa databassystem och använd deras unika egenskaper för att passa dina specifika behov och projekt. Ha kul med databashantering och fortsätt skapa fantastiska applikationer med hjälp av tabeller och databasdrivna funktioner!

## Obligatorisk Dad Joke:

Varför förlorade SQL-databasen sitt jobb?
För att den inte kunde sluta med att kommunicera med "tables" hela tiden! 😄
