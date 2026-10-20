---
title: Protected
grand_parent: Objektorienterad programmering (OOP)
author: Marcus Ackre Medina
parent: Åtkomstmoderator
nav_order: 20
---
# Protected

En Nyckel till Polymorfismens Hemligheter!

## Introduktion

Välkommen till denna spännande övning där vi kommer att utforska den kraftfulla åtkomstmodifieraren "protected" inom programmeringsspråket Java. Genom att använda "protected" kan vi låta en metod eller egenskap vara tillgänglig för den klass den är deklarerad i samt alla dess avledda klasser. Detta ger oss en möjlighet att skapa flexibla och effektiva kodstrukturer genom polymorfism. Låt oss ta reda på hur "protected" kan användas för att skapa en väl sammanhållen kodbas och göra våra klasser och metoder tillgängliga för rätt komponenter i arvshierarkin.

## TL;DR

I denna övning har vi bekantat oss med "protected", en åtkomstmodifierare som låter oss dela metoder och egenskaper mellan en klass och dess avledda klasser. Genom att använda "protected" kan vi skapa välstrukturerad kod som främjar återanvändning och underhållbarhet. Genom att skydda våra privata detaljer och samtidigt göra dem tillgängliga för relevanta delar av kodbasen kan vi skapa harmoniska och välbalanserade program.

## När du läst detta ska du kunna

- Förstå vad "protected" är och dess syfte inom Java-programmering.
- Tillämpa "protected" för att dela metoder och egenskaper mellan en klass och dess avledda klasser.
- Förklara fördelarna med att använda "protected" för att uppnå polymorfism.
- Skapa kodexempel som demonstrerar användningen av "protected" för att skapa flexibla kodstrukturer.

## Vad är "protected"?

"Protected" är en åtkomstmodifierare inom Java som gör att en metod eller egenskap kan vara tillgänglig för den klass där den är deklarerad och alla klasser som ärver från den. Detta möjliggör en hierarkisk kodstruktur där vi kan dela gemensam funktionalitet mellan en överordnad klass och dess avledda klasser. Med "protected" får vi en balanserad kombination av åtkomstnivåer, vilket underlättar arv och skapar mer flexibla kodstrukturer.

## Fördelar

Att använda "protected" ger oss flera fördelar:

1. **Polymorfism och Återanvändning:** Genom att dela metoder och egenskaper med "protected" kan vi skapa en grundläggande kodbas som används och anpassas av flera avledda klasser. Detta främjar återanvändning av kod och minskar duplicering.

2. **Säkerhet och Modulär Design:** "Protected" ger oss en säker och kontrollerad åtkomstnivå, vilket låter oss skydda våra privata detaljer samtidigt som vi gör dem tillgängliga för relevanta delar av kodbasen. Detta bidrar till en modulär och välsammanhängande design.

3. **Kodunderhåll:** Genom att använda "protected" skapar vi en tydlig koppling mellan överordnade klasser och deras avledda klasser. Detta gör det enklare att förstå kodens hierarki och underhålla den på lång sikt.

## Begränsningar

Det är viktigt att vara medveten om att "protected" inte är en universallösning för alla situationer. Det finns vissa begränsningar att överväga:

1. **Måttfullhet:** Använd "protected" med omsorg och överväg noga vilka metoder och egenskaper som bör delas mellan klasser. Överanvändning av "protected" kan leda till en mindre strukturerad kodbas.

2. **Överkomplicerad Hierarki:** Om klasshierarkin blir för komplex med många nivåer av avledning, kan det bli svårare att hantera kodens komplexitet och förståelse.

## Exempel

Låt oss nu ta ett praktiskt exempel på hur "protected" kan användas för att dela en egenskap mellan en överordnad klass och dess avledda klass:

```java
// Klassen Animal ärver inte från någon annan klass
public class Animal {
    protected String sound;

    public void makeSound() {
        System.out.println("Animal sound: " + sound);
    }
}

// Klassen Cat ärver från Animal och kan därför använda "sound"
public class Cat extends Animal {
    public Cat() {
        this.sound = "Meow";
    }
}

// Klassen Dog ärver också från Animal och kan använda "sound"
public class Dog extends Animal {
    public Dog() {
        this.sound = "Woof";
    }
}
```

I det här exemplet kan både klassen "Cat" och "Dog" använda egenskapen "sound" från den överordnade klassen "Animal" tack vare "protected".

## Slutsats

Grattis! Du har nu utforskat hemligheterna med "protected" och dess roll inom polymorfism och arv i Java. Genom att använda "protected" kan du skapa välbalanserade och strukturerade kodstrukturer, vilket främjar återanvändning och underhållbarhet. Så var modig och fortsätt att utveckla kreativa och spännande program med Java! Världen av möjligheter väntar på dig!

## Obligatorisk Dad-Joke

Varför var nyckelordet "protected" så noga med sina privata detaljer?

För att det ville vara "protected" från nyfikna ögon och bara dela sina hemligheter med sina mest nära och kära - dess avledda klasser!
