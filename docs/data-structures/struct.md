---
title: Struct
author: Marcus Ackre Medina
parent: Datastrukturer
nav_order: 60
---
# Struct

## Introduktion

Structs är en vanlig datastruktur i vissa programmeringsspråk, men i Java, använder vi oftast klasser för att uppnå liknande funktionalitet. Så vad är egentligen en struct och hur relaterar det till Java? Kan man likställa en Java-klass med en struct från andra språk, och om ja, varför inte bara använda termen "struct"? Dessa frågor kommer att utforskas och besvaras i detta avsnitt.

## TL;DR

I Java används klasser för att representera en struktur liknande structs i andra programmeringsspråk. Medan det tekniskt sett inte finns en "struct" i Java, kan vi uppnå samma mål genom att använda klasser.

## När du läst detta ska du kunna

- Förstå vad en struct är i programmeringskontext.
- Se sambandet mellan structs och klasser i Java.
- Diskutera varför Java valde att inte ha en dedikerad struct.
- Identifiera när och hur man kan använda en klass som en struct i Java.
- Skriva en enkel Java-klass som representerar en struct från andra språk.

## Vad är Struct?

I programmeringsspråk som C och C++, representerar en struct en samling av variabler (kan vara av olika datatyper) under ett enda namn. Structs kan användas för att gruppera data som hör ihop. I Java uppnår vi liknande funktionalitet med klasser.

## Fördelar

Att använda klasser i Java som structs:

1. Ökar läsbarheten: Gruppering av relaterad data under ett enda namn gör koden mer lättläst.
2. Modularitet: Tillåter återanvändning av kod.
3. Utökbarhet: Till skillnad från traditionella structs, kan Java-klasser utökas med metoder, konstruktorer och mycket mer.

## Begränsningar

Även om Java-klasser erbjuder en bredare funktionalitet jämfört med structs, finns det några begränsningar:

1. Större overhead: Klasser i Java kan ha en större overhead jämfört med lättviktiga structs i språk som C.
2. Saknad av stack-allocated objekt: I Java allokeras alla objekt på heapen, vilket kan vara mindre effektivt än stack-allocated structs i vissa scenarier.

## Användningsområden

Java-klasser används i stort sett överallt inom Java-programmering. De kan representera allt från komplexa datastrukturer till enkla objekt som representerar en punkt i 2D-rymden.

## Exempelkod - "Struct" i Java berättad genom en punkt

I detta exempel kommer vi att skapa en Java-klass som representerar en 2D-punkt, liknande hur en struct skulle användas i C.

```java
public class Point {
    public int x; // x-koordinat
    public int y; // y-koordinat

    // Konstruktor
    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }
}
```

## Termer

| Term | Förklaring |
| --- | --- |
| Struct | En samling av variabler under ett enda namn, oftast används i språk som C och C++. |
| Klass | En mall för att skapa objekt i Java, kan fungera som en struct med utökad funktionalitet. |

## Slutsats

Även om Java tekniskt sett inte har en "struct", kan dess klasser fungera som en. Medan det finns några skillnader och begränsningar, erbjuder Java-klasser en flexibel och kraftfull mekanism för att gruppera relaterad data under ett enda namn, precis som en struct skulle göra i andra språk.

## Obligatorisk dad joke:

Varför kunde Javabönan inte programmera? Den var inte bryggd än!
