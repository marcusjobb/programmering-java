---
title: Record i Java
author: Marcus Ackre Medina
parent: Datastrukturer
nav_order: 50
---
# Record i Java

## Introduktion

Har du någonsin önskat att Java kunde ha en funktion där man snabbt kunde skapa en klass bara för att hålla lite data, utan allt det extra? Vad om jag sa att Java nu har en sådan funktion? Låt oss dyka ner i den spännande världen av `Record` i Java!

## TL;DR

`Record` är en funktion introducerad i Java som ger en mer komprimerad syntax för att definiera datahållarklasser. De är oföränderliga, vilket innebär att de ger många fördelar som tydlighet, säkerhet och integritet.

## När du läst detta ska du kunna

- Förstå och förklara vad `Record` är och dess relevans inom Java programmering.
- Diskutera fördelar och begränsningar med `Record`.
- Identifiera olika användningsområden där `Record` kan tillämpas.
- Förstå och tolka ett kodexempel som använder `Record`.
- Sammanfatta viktiga insikter och rekommendationer för vidare läsning.

## Vad är Record?

`Record` i Java är en ny typ av klass som tillåter dig att skapa en datahållarklass med minimal syntax. De är oföränderliga, vilket innebär att när en `Record` är skapad, kan dess innehåll inte ändras. De introducerades för att minska bloat-koden som behövs för att definiera en klass, bara för att hålla lite data.

## Fördelar

- **Enkelhet:** Inget behov av att skriva getters, setters, equals, hashCode eller toString metoder. Java gör allt detta för dig bakom kulisserna!
- **Oföränderlighet:** En garanti om att ditt dataobjekt förblir oförändrat, vilket bidrar till bättre kodintegritet.
- **Läsbarhet:** Med mindre kod blir ditt program mer lättläst och underhållbart.

## Begränsningar

- **Begränsad funktionalitet:** Eftersom det är en datahållarklass, kan du inte lägga till ytterligare funktionalitet. Detta kan vara begränsande i vissa scenarier.
- **Oföränderlighet:** Kan ses som en nackdel om du behöver förändra ditt objekt efter att det har skapats.

## Användningsområden

`Record` är perfekt när:

- Du vill representera enkla dataobjekt, som koordinater `(x, y)`.
- Du behöver oföränderliga objekt, till exempel för att undvika bieffekter i ditt program.
- Du vill ha tydlighet och förutsägbarhet i din kod.

## Exempelkod - Record i en berättelse

Föreställ dig att du skapar en klass för att representera en punkt i ett koordinatsystem. Istället för att skriva allt detta:

```java
public class Point {
    private final int x;
    private final int y;

    public Point(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public int x() {return x;}
    public int y() {return y;}

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Point)) return false;
        Point point = (Point) o;
        return x == point.x && y == point.y;
    }

    @Override
    public int hashCode() {
        return Objects.hash(x, y);
    }

    @Override
    public String toString() { return "Point{ x=" + x + ", y=" + y +"}"; }
}
```

Med `Record` blir det bara:

```java
public record Point(int x, int y) {}
```

Fascinerande, eller hur? Så nu undrar du, varför lärde jag mig allt det där om klasser? Det är för att du ska förstå hur `Record` fungerar under huven.

## Exempel

Här är ett enkelt exempel på hur du kan använda `Record` i Java:

```java
public record Person(String name, String alias, String workplace) {}

public class TestRecord {
    public static void main(String[] args) {
        Person bruceWayne = new Person("Bruce Wayne", "Batman", "Wayne Enterprises, Inc.");

        System.out.println(bruceWayne.name());       // Skriver ut: Bruce Wayne
        System.out.println(bruceWayne.alias());      // Skriver ut: Batman
        System.out.println(bruceWayne.workplace());  // Skriver ut: Wayne Enterprises, Inc.

        System.out.println(bruceWayne);  // Skriver ut: Person[name=Bruce Wayne, alias=Batman, workplace=Wayne Enterprises, Inc.]
    }
}
```

med outputen

```text
Bruce Wayne
Batman
Wayne Enterprises, Inc.
Person[name=Bruce Wayne, alias=Batman, workplace=Wayne Enterprises, Inc.]
```

## Termer

| Term         | Förklaring                                                                     |
| ------------ | ------------------------------------------------------------------------------ |
| Record       | En ny typ av klass i Java för att representera datahållare med minimal syntax. |
| Bloat-kod    | Onödig kod som inte bidrar till funktionaliteten i ett program.                |
| Oföränderlig | Ett objekt vars tillstånd inte kan ändras efter att det har skapats.           |
| Mutable      | Ett objekt vars tillstånd kan ändras efter att det har skapats.                |
| Unmutable    | Ett objekt vars tillstånd inte kan ändras efter att det har skapats.           |

## Slutsats

`Record` i Java är en revolutionerande funktion som förenklar skapandet av datahållarklasser. Med sin enkelhet, läsbarhet och oföränderlighet är det ett kraftfullt verktyg i Java-programmerarens verktygslåda. Glöm inte att dyka djupare in i detta ämne för att utforska alla dess nyanser!

## Obligatorisk dad joke:

Varför älskar Java-klasser objekt? För att de skapades för varandra!
