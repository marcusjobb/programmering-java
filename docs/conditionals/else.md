---
title: Else
author: Marcus Ackre Medina
parent: If
nav_order: 10
---
# Else

I programmeringsspråket Java används nyckelordet "Else" för att skapa en alternativ väg i en kodblockstruktur. Det ger möjlighet att utföra en annan sekvens av kod om en "if"-sats utvärderas som falsk. Med andra ord kan "Else" användas för att hantera fall där "if"-villkoret inte är uppfyllt, och programmet kan utföra en annan uppsättning instruktioner istället.

## När du läst detta ska du kunna

- Förstå och förklara vad "Else" är och dess användning i Java.
- Identifiera olika användningsområden där "Else" kan vara användbart.
- Förstå och tolka ett kodexempel som använder "Else" i Java.
- Göra villkorsbaserade beslut i dina egna program med hjälp av "Else".

## TL;DR

I Java används nyckelordet "Else" för att skapa en alternativ kodväg när ett "if"-villkor är falskt. Genom att använda "else" kan programmerare göra olika beslut beroende på olika villkor. Det är viktigt att balansera användningen av "else" för att hålla koden läsbar och förståelig. Användningsområdena för "else" inkluderar bland annat ålderskontroll och betygssystem.

## Vad är Else?

"Else" är ett nyckelord som används i Java för att definiera ett alternativt kodblock som utförs när det motsatta villkoret av en "if"-sats är sant. Om "if"-villkoret utvärderas som falskt, kommer programmet att hoppa över kodblocket inom "if" och istället utföra kodblocket inom "else".

För att använda "Else" måste det alltid följas av en "if". Det är också viktigt att notera att "Else" alltid kommer i slutet av en "if"-sats och kan inte användas utanför den.

## Fördelar med Else

Här är några fördelar med att använda "Else" i Java:

1. **Beslutsfattande:** "Else" ger programmerare möjlighet att göra beslut i sina program baserat på olika villkor. Detta är särskilt användbart när olika handlingar behövs beroende på ett villkors sanning eller falskhet.

2. **Alternativa vägar:** Genom att använda "Else" kan olika vägar definieras i koden, vilket ökar programmens flexibilitet och funktionalitet.

## Begränsningar med Else

Några saker att vara medveten om när du använder "Else":

1. **Enkelriktat flöde:** "Else" möjliggör bara en alternativ kodväg i relation till "if"-villkoret. Om flera olika vägar behövs, kan det vara nödvändigt att använda flera "if-else" uttalanden.

2. **Komplicerad kod:** Om "if-else" kedjor blir alltför komplicerade kan det vara svårt att förstå flödet i koden. Det är viktigt att balansera användningen av "else" för att hålla koden läsbar.

## Användningsområden för Else

"Else" kan användas i olika situationer där beslut behöver fattas baserat på olika villkor. Här är några exempel på användningsområden för "Else" i Java:

1. **Ålderskontroll:** Som illustrerat i exemplet tidigare kan "Else" användas för att kontrollera om en person är myndig eller inte baserat på deras ålder.

2. **Betygsättningssystem:** I ett betygssystem kan "Else" användas för att bestämma vilket betyg en student får beroende på deras poäng.

## Exempelkod - Else i en berättelse

För att förtydliga användningen av "Else", låt oss gå igenom ett exempel där vi använder "Else" för att bestämma om ett nummer är positivt eller negativt:

```java
int number = -5;
if (number >= 0) {
    System.out.println("Numret är positivt");
} else {
    System.out.println("Numret är negativt");
}
```

I detta exempel är "nummer" satt till -5. Eftersom -5 är mindre än 0, utvärderas "if"-villkoret som falskt, och programmet skriver ut "Numret är negativt".

## Termer och förklaringar

| Term         | Förklaring                                                                                                                                                                  |
| ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Else         | Ett nyckelord i Java som används för att skapa en alternativ väg i kodblocket när "if"-villkoret är falskt.                                                               |
| If           | Ett nyckelord i Java som används för att skapa en villkorsbaserad kodblockstruktur. Om villkoret är sant, utförs kodinstruktionerna inom "if"-blocket                     |
| Kodblock     | En grupp av kodinstruktioner som är grupperade tillsammans.                                                                                                                |
| Villkor      | En logisk fråga som kan utvärderas som antingen sann eller falsk.                                                                                                          |
| Positivt/negativt | Inom detta sammanhang betyder positivt att ett nummer är större än eller lika med noll och negativt att det är mindre än noll.                                           |

## Slutsats

"Else" är ett viktigt nyckelord inom Java som ger möjlighet att skapa alternativa kodvägar beroende på om ett "if"-villkor är sant eller falskt. Detta ger programmerare möjlighet att hantera olika fall och fatta beslut i sina program. Genom att använda "else" kan programmen bli mer flexibla och kapabla att hantera olika scenarier.
