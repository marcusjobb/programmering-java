---
title: Byte och Short
author: Marcus Ackre Medina
parent: Variabler
nav_order: 110
---
# Byte och Short

Byte och Short i Java - Små Men Kraftfulla Numeriska Datatyper

Inom programmeringens värld stöter vi ofta på situationer där vi behöver hantera små heltal. För att optimera minnesanvändningen och förbättra prestanda introducerades "byte" och "short" som numeriska datatyper i Java. Dessa datatyper tar minimalt med minne och kan användas när vi vet att värdena är inom ett begränsat intervall. I Detta avsnitt ska vi dyka in i "byte" och "short", utforska deras egenskaper och upptäcka varför deras små storlek inte hindrar dem från att vara kraftfulla verktyg i Java-världen.

## TL;DR

"Byte" och "short" är små numeriska datatyper i Java som tar 8-bitars och 16-bitars minne, respektive. "Byte" används för att representera heltal inom intervallet -128 till 127, medan "short" används för heltal inom intervallet -32,768 till 32,767. Dessa datatyper är användbara när minnesutrymme är kritiskt och när värdena är inom ett begränsat område.

## När du läst detta ska du kunna

- Förstå vad "byte" och "short" representerar i Java.
- Identifiera när det är lämpligt att använda "byte" och "short" för att optimera minnesanvändningen.
- Använda "byte" och "short" korrekt i Java-programmering.

## "Byte" - Minsta Heltalet

"Byte" är den minsta numeriska datatypen i Java och tar endast 8-bitars minne. Detta innebär att "byte" kan representera heltal inom intervallet från -128 till 127. "Byte" används främst när minnesutrymme är avgörande och när vi vet att våra värden kommer att vara små. Exempel på användning inkluderar lagring av ASCII-värden för tecken och manipulering av binärdata.

## "Short" - Halvvägs Mellan "Byte" och "Int"

"Short" är en större datatyp än "byte" men tar fortfarande relativt litet minnesutrymme, nämligen 16-bitar. Detta gör att "short" kan representera heltal inom intervallet från -32,768 till 32,767. "Short" är användbart när vi behöver större värden än "byte" kan hantera, men inte så stora att vi behöver använda den mer utrymmeskrävande "int"-datatypen. Användningen av "short" kan hjälpa oss att balansera minnesutrymme och prestanda i våra program.

## Skillnader i Minnesanvändning

Skillnaden mellan "byte", "short" och andra numeriska datatyper som "int" och "long" ligger i deras minnesanvändning. Eftersom "byte" och "short" tar mindre minne än de andra datatyperna, kan de vara fördelaktiga för små datamängder och situationer där minnesutrymme är viktigt. Å andra sidan kan "int" och "long" hantera större värden, men de tar också mer minne. Det är viktigt att välja rätt datatyp beroende på de värden vi förväntar oss att hantera och optimeringsbehoven i vår kod.

## Exempelkod - Användning av "byte" och "short"

Låt oss använda "byte" och "short" i en enkel kodexempel:

```java
public class NumericDataTypesExample {
    public static void main(String[] args) {
        byte smallNumber = 100;
        short mediumNumber = 1000;

        int result = smallNumber + mediumNumber;
        System.out.println("Result: " + result);
    }
}
```

Resultatet blir:

```
Result: 1100
```

I detta exempel adderar vi "byte" och "short" för att få ett resultat i "int"-datatypen.

## Myten om Nuclear Ghandi

I artikeln "[Nuclear Gandhi](https://en.wikipedia.org/wiki/Nuclear_Gandhi)" diskuteras en rolig dataspelsmyt som kretsar kring den karaktär som representerar Mahatma Gandhi i strategispelet Civilization från 1991. Enligt legenden skulle en bugg göra att Gandhi, som vanligtvis var en fridsam ledare, plötsligt blev extremt aggressiv och använde kärnvapen i stor omfattning. Ursprungligen uppstod påståendet på TV Tropes wiki år 2012 och spreds sig sedan över internet som en humoristisk historia.

Enligt myten hade alla ledare i spelet en aggressionsnivå på en skala från **1 till 10**. Gandhi hade den lägsta möjliga nivån av 1, men när han bytte regering till demokrati, vilket var fördelaktigt för fredliga nationer, minskade hans aggression med 2 och blev därmed negativ.

<img src="nuclearghandi.png" alt="Nuclear Ghandi" style="float: right;">Buggen påstods bero på att aggressionen lagrades som en 8-bitars osignerad heltalsvariabel som kunde lagra värden från 0 till 255, vilket ledde till en överflödesfel (integer overflow) och en **aggressionsnivå på 255** för Gandhi. När ett osignerat värde blir negativ ökas det automagiskt med det högsta värdet som datatypen kan lagra, vilket i detta fall var 256 (0 räknas också ;) ). Detta gjorde att Gandhi fick en aggressionsnivå på 255, vilket gjorde honom till den mest aggressiva ledaren i spelet. Spelets teknologiträd avslöjar vanligtvis kärnvapen endast efter demokrati, vilket gjorde att Gandhi redan hade en mycket hög aggressionsnivå när Indien blev kapabelt att använda kärnvapen, och därmed attackerade andra civilisationer med kärnvapenmissiler.

```text
1 - 2 = -1 + 256 = 255
```

Fastän denna bugg inte existerade i verkligheten blev "Nuclear Gandhi" en av de mest igenkännliga dataspelsmissarna och en populär internetmeme. Den användes också som exempel på heltalsöverflöde i datavetenskap och inkluderades som en påskägg i andra spel i Civilization-serien.

Även om myten om "Nuclear Gandhi" inte var sann, har den bidragit till att göra spelet ännu mer underhållande och har varit en rolig och minnesvärd del av spelhistorien.

## Slutsats

I Detta avsnitt har vi dykt in i den spännande världen av "byte" och "short" som små men kraftfulla numeriska datatyper i Java. Dessa datatyper ger oss möjlighet att hantera små heltal och samtidigt optimera minnesanvändningen i våra program. Genom att välja rätt datatyp för våra applikationer kan vi förbättra prestanda och effektivt utnyttja den begränsade resursen av minne. Så låt inte storleken lura dig, "byte" och "short" har bevisat att de kan vara viktiga komponenter i din Java-kod och bidra till en smidig och effektiv programmeringserfarenhet!

## Obligatorisk dad joke

Varför kan inte "byte" se på skräckfilmer på bio?

För att de är för små... naaaaaw :'(
