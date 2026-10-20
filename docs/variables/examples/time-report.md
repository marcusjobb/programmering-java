---
title: Arbetad tid
author: Marcus Ackre Medina
parent: Variabler
nav_order: 10
---
# Arbetad tid

Vi ska göra en beräkning av arbetad tid på en månad, vi gör detta genom att
skapa variabler för varje dag och varje vecka, sedan skapar vi en variabel för
hela månaden.

## Kod

Då det är fyra veckor kommer vi att markera varje dag med siffra för vilken
vecka den tillhör. Vi ska också skapa en variabel för varje dag och vecka.
Vi kommer att använda oss av `float` för att kunna använda decimaler, för att float är i jämförelse mot `double` mindre minneskrävande och vi behöver inte så många decimaler.

```java
class Main {
  public static void main(String[] args) {

    // Vecka 1
    float monday = 7.5; // 7 timmar och 30 minuter
    float tuesday = 8;
    float wednesday = 8;
    float thursday = 9; // Personal möte
    float friday = 6;
    float week = monday + tuesday + wednesday + thursday + friday;
    float throughAverageWeek = week / 5;

    // Vecka 2
    float monday = 8;
    float tuesday = 8.5;
    float wednesday = 8.5;
    float thursday = 9; // Personal möte
    float friday = 5.5;
    float week = monday + tuesday + wednesday + thursday + friday;
    float throughAverageWeek = week / 5;

    // Vecka 3
    float monday = 8.5;
    float tuesday = 8.5;
    float wednesday = 8.5;
    float thursday = 9; // Personal möte
    float friday = 6;
    float week = monday + tuesday + wednesday + thursday + friday;
    float genomsnittVecka3 = week / 5;

    // Vecka 4
    float monday = 8;
    float tuesday = 8.5;
    float wednesday = 8.5;
    float thursday = 9; // Personal möte
    float friday = 6;
    float week = monday + tuesday + wednesday + thursday + friday;
    float genomsnittVecka4 = week / 5;

    // Månad
    float month = week + week + week + week;
    float genomsnittMåmnad = throughAverageWeek + throughAverageWeek + genomsnittVecka3 + genomsnittVecka4;

    // Rapport
    System.out.println("Arbetad tid denna månad: " + month + " timmar");
    System.out.println("Genomsnittlig arbetad tid per vecka: " + genomsnittMåmnad + " timmar");
    System.out.println("Genomsnittlig arbetad tid per dag: " + genomsnittMåmnad / 5 + " timmar");

  }
}
```

Detta ger oss resultatet

```text
Arbetad tid denna månad: 160.0 timmar
Genomsnittlig arbetad tid per vecka: 40.0 timmar
Genomsnittlig arbetad tid per dag: 8.0 timmar
```

## Andra tillvägagångssätt

Vårt projekt, även med sin enkla form har en helt klart tydlig kod som är lätt att förstå och lätt att läsa, och som du faktiskt kan använda. Enda nackdelen är kanske att du får skriva minuter i decimalform, det går att lösa.

```java
    float wednesday = 8 + 15/60; // 8 timmar och 15 minuter, eller 8.25 timmar
```

Java har inbyggda funktioner för att räkna ut tid också, den heter LocalTime, men tyvärr arbetar den med heltal, så vi får omvandla och göra koden rörigare.

```java
    LocalTime wednesday = LocalTime.of(8, 15); // 8 timmar och 15 minuter
    float wednesday = wednesday.getHour() + wednesday.getMinute() / 60; // 8.25 timmar
```

## Lärdomar av detta

- Bra namngivning av variabler gör koden lättare att läsa
- Beräkning av minuter kan vara bråkigt
- Vår kod är som ett Excel-blad
  - Lättöverskådlig
  - Lätt att förstå
  - Lätt att använda
  - Lätt att ändra
  - Lätt att felsöka
- Vi använder variabler för allt som innebär saker vi ska hålla koll på
- Variablerna är våra "minneslappar" för att hålla koll på saker

## Summan av kardemumman

Vi har skapat variabler för varje dag och vecka, sedan har vi skapat en variabel för hela månaden. Vi har också skapat en variabel för genomsnittlig arbetad tid per vecka och dag. Vi har använt oss av `float` för att kunna använda decimaler, för att float är i jämförelse mot `double` mindre minneskrävande och vi behöver inte så många decimaler.

Men då vi är programmerare vill vi förenkla detta, vilket vi självklart kan göra med hjälp av loopar, metoder, listor... men det är sådant vi ska titta på längre fram i denna bok.
