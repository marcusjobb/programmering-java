---
title: Abstrakta Klasser
grand_parent: Objektorienterad programmering (OOP)
author: Marcus Ackre Medina
parent: Polymorfism
nav_order: 20
has_children: true
---
# Abstrakta Klasser

Ett Kreativt Vägval i Programmering!

## Introduktion

Välkommen till världen av abstrakta klasser - en spännande kombination av kod och abstrakta metoder som ger oss möjligheten att skapa flexibla och återanvändbara klasser inom programmering. I den här övningen kommer vi att dyka in i vad abstrakta klasser är och hur de kan användas för att skapa hierarkier av klasser med gemensamma egenskaper och metoder. Låt oss ställa några nyfikna frågor: Vad är en abstrakt klass och vad skiljer den från en vanlig klass? Hur kan vi använda abstrakta klasser för att förbättra kodens struktur och organisering? Följ med oss på detta kreativa vägval inom programmering!

## TL;DR

I den här övningen har vi upptäckt den spännande världen av abstrakta klasser. Vi har lärt oss att en abstrakt klass kombinerar kod med abstrakta metoder och används för att möjliggöra arv för andra klasser. Genom att använda abstrakta klasser kan vi skapa hierarkier av klasser som delar gemensamma egenskaper och metoder. Det ger oss möjligheten att utnyttja polymorfism och skapa mer flexibel och underhållbar kod!

## När du läst detta ska du kunna

- Förstå och förklara vad abstrakta klasser är och deras roll inom programmering.
- Diskutera fördelar med att använda abstrakta klasser för kodens struktur och organisation.
- Skapa och använda abstrakta klasser för att möjliggöra arv för andra klasser.
- Förklara hur polymorfism kan utnyttjas med abstrakta klasser för mer flexibel kod.

## Vad är Abstrakta Klasser?

En abstrakt klass är som ett kreativt vägval i programmering - det är en klass som innehåller både konkret kod och abstrakta metoder. Men vad innebär det egentligen? Låt oss ta en närmare titt!

En abstrakt klass används som en grundläggande mall för andra klasser att ärva från. Det går dock inte att skapa objekt av en abstrakt klass direkt - den används endast som en blåkopia för att skapa specialiserade klasser som delar vissa gemensamma egenskaper och beteenden.

### Vad är abstrakta metoder?

Abstrakta metoder är metoder som inte har någon kod i sig. De är endast deklarerade med en signatur och inget mer. Detta innebär att de inte kan användas direkt, utan måste implementeras i en underklass för att kunna användas.

## Exempel

För att förstå abstrakta klasser bättre, låt oss skapa en abstrakt klass kallad "Shape" (Geometrisk Form). I den definierar vi en abstrakt metod "area()" som ska användas för att beräkna arean för olika geometriska former.

```java
// Abstrakt klass för geometriska former
public abstract class Shape {
    // Abstrakt metod för att beräkna arean
    public abstract double area();
}
```

Nu kan vi skapa underklasser som ärver från den abstrakta klassen "Shape" och implementerar den abstrakta metoden "area()". Låt oss skapa två underklasser - "Circle" (Cirkel) och "Rectangle" (Rektangel).

```java
// Underklass för cirkel som ärver från Shape
public class Circle extends Shape {
    private double radius; // Radien på cirkeln

    // Konstruktor för att skapa en cirkel med given radie
    public Circle(double radius) {
        this.radius = radius;
    }

    // Överskuggning av area-metoden för att beräkna arean av cirkeln
    @Override
    public double area() {
        return Math.PI * radius * radius;
    }
}

// Underklass för rektangel som ärver från Shape
public class Rectangle extends Shape {
    private double width; // Bredden på rektangeln
    private double height; // Höjden på rektangeln

    // Konstruktor för att skapa en rektangel med given bredd och höjd
    public Rectangle(double width, double height) {
        this.width = width;
        this.height = height;
    }

    // Överskuggning av area-metoden för att beräkna arean av rektangeln
    @Override
    public double area() {
        return width * height;
    }
}
```

Nu kan vi skapa en array av typen "Shape" och fylla den med objekt av typen "Circle" och "Rectangle". Vi kan sedan loopa igenom arrayen och anropa "area()" metoden för att beräkna arean för varje geometrisk form.

```java
// Skapar en array av typen Shape
Shape[] shapes = new Shape[2];

// Lägger in ett objekt av typen Circle i arrayen
shapes[0] = new Circle(5);

// Lägger in ett objekt av typen Rectangle i arrayen
shapes[1] = new Rectangle(5, 10);

// Loopar igenom arrayen och anropar area-metoden på varje objekt
for (Shape shape : shapes) {
    System.out.println(shape.area());
}
```

Genom att använda abstrakta klasser och polymorfism kan vi på ett smidigt sätt beräkna arean av olika geometriska former med samma kod. Det är verkligen kraftfullt och kreativt!

## Referenser

- [Abstrakta klasser - Microsoft](https://docs.microsoft.com/en-us/dotnet/Java/programming-guide/classes-and-structs/abstract-classes)
- [Abstract class - W3Schools](https://www.w3schools.com/cs/cs_abstract.php)
