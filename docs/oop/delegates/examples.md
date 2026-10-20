---
title: Exempel
grand_parent: Objektorienterad programmering (OOP)
author: Marcus Ackre Medina
parent: Delegater
nav_order: 10
---
# Exempel

Nu ska vi kliva ner i en djup och mörk grotta av kodning och utforska Delegater i Java! Gör dig redo för en helt ny nyvå inom programmering... Utforska Kreativ Programmering... utforska Delegater i Java!

## Introduktion

Välkommen till denna spännande övning om användningen av delegater i Java! I den här övningen kommer vi att dyka in i världen av delegater, som är ett kraftfullt koncept inom programmering som hjälper oss att hantera och använda metoder på ett flexibelt sätt. Vad är egentligen en delegat? Hur kan vi dra nytta av dess funktioner? Låt oss ta reda på det och mycket mer!

## TL;DR

I denna övning har vi utforskat användningen av delegater i Java och upptäckt hur de kan hjälpa oss att representera och anropa metoder med olika signaturer. Delegater ger oss möjligheten att implementera händelsehantering och callback-funktioner på ett smidigt sätt. Genom att förstå delegater kan vi skapa kod som blir mer flexibel och återanvändbar!

## När du läst detta ska du kunna

- Förstå vad en delegat är och hur den fungerar i Java.
- Använda delegater för att skapa flexibla metoder och callback-funktioner.
- Implementera en enkel klass med delegater i Java.
- Utforska fördelarna med att använda delegater för händelsehantering.

## Vad är en Delegat i Java?

En delegat i Java är ett kraftfullt verktyg som låter oss representera och anropa metoder med en specifik signatur. Med hjälp av delegater kan vi skapa referenser till metoder och sedan använda dessa referenser för att anropa metoden. Detta ger oss möjlighet att skapa mer dynamiska och flexibla lösningar inom programmering.

Kortfattat: Vi kan skicka iväg metoder på samma sätt som vi skickar iväg variabler.

## Fördelar med Delegater

Delegater erbjuder flera fördelar som förbättrar koden och underlättar utvecklingen:

1. **Flexibilitet:** Genom att använda delegater kan vi byta ut vilken metod som helst som har samma signatur vid behov. Detta gör koden mer modulär och lätt att underhålla.

2. **Händelsehantering:** Delegater är utmärkta för att implementera händelsehantering, vilket gör det möjligt att hantera händelser och anropa metoder när något specifikt inträffar.

3. **Callback-funktioner:** Delegater kan användas för att skicka funktioner som argument till andra funktioner. Detta gör det möjligt att skapa mer dynamiska och anpassningsbara funktioner.

## Exempel: Skapa en Delegat i Java

Låt oss utforska hur vi kan skapa och använda en delegat i Java genom ett enkelt exempel:

```java

// Vi skapar ett interface med namnet Calculation som har en metod calculate
// som tar två heltal som parametrar och returnerar inget. Den får fungera
// som mall för vår delegat.
// Det viktiga här är att metoden i interfacet har samma signatur som de
// metoder vi vill använda med delegaten.
// Alltså void (namn) (int a, int b)   <--- delegatmallen
interface Calculation {
    void calculate(int a, int b);
}

// Vi skapar en klass med namnet Calculator som har metoder för att addera,
// subtrahera och eventuellt ytterligare beräkningar.
public class Calculator {
    public void add(int a, int b) {
        int sum = a + b;
        System.out.println("Summan av " + a + " och " + b + " är " + sum);
    }

    public void subtract(int a, int b) {
        int difference = a - b;
        System.out.println("Skillnaden mellan " + a + " och " + b + " är " + difference);
    }

    // ... andra beräkningsmetoder ...

    // Vi skapar en metod som tar emot två heltal och en delegat som parameter.
    // Metoden anropar sedan delegaten med de två heltalen som argument.
    // Metoden vet alltså inte från början vad den ska räkna ut, den vet
    // att den ska använda en metod som skickas in till den, och att den
    // ska förse metoden med de värden som skickats in.
    public void performCalculation(int a, int b, Calculation calculation) {
        calculation.calculate(a, b);
    }

    public static void main(String[] args) {
        // Vi instansierar vår Calculator-klass
        Calculator calculator = new Calculator();

        // Nu använder vi interface-mallen för att delegater
        Calculation addDelegate = calculator::add; // <--- delegat till add
        Calculation subtractDelegate = calculator::subtract; <--- delegat till subtract

        // Anropa metoderna med delegaterna som argument
        calculator.performCalculation(5, 3, addDelegate);
        calculator.performCalculation(5, 3, subtractDelegate);
    }
}
```

I det här exemplet skapar vi en gränssnitt med namnet Calculation som har en metod calculate som tar två heltal som parametrar och returnerar inget. Sedan skapar vi en Calculator-klass med metoder för att addera, subtrahera och eventuellt ytterligare beräkningar.

Vi skapar två instanser av gränssnittet Calculation genom att använda metodreferenser (lambda-uttryck kan också användas för detta ändamål). Dessa instanser refererar till de respektive beräkningsmetoderna add och subtract i Calculator-klassen.

Slutligen använder vi performCalculation-metoden för att utföra de beräkningar som vi har definierat genom delegaterna. Detta visar hur enkelt det är att byta mellan olika beräkningsmetoder genom att använda delegater!

## Andra Användningsområden för Delegater

- **Händelsehantering:** Delegater kan användas för att implementera händelsehantering, vilket gör det möjligt att hantera händelser och anropa metoder när något specifikt inträffar.
- **Callback-funktioner:** Delegater kan användas för att skicka funktioner som argument till andra funktioner. Detta gör det möjligt att skapa mer dynamiska och anpassningsbara funktioner.

## Slutsats

Grattis! Nu har du utforskat den spännande världen av delegater i Java. Delegater är ett kraftfullt verktyg som ger oss möjlighet att skapa flexibla och återanvändbara metoder. Genom att använda delegater kan vi hantera händelser och implementera callback-funktioner på ett smidigt sätt. Fortsätt att utforska Java och dess många möjligheter för att skapa fantastiska program och applikationer!

## Obligatorisk dad joke:

Vad är en programmerares favoritverktyg? En byte-sax!
