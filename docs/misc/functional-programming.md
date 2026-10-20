---
title: Funktionell Programmering i Java
author: Marcus Ackre Medina
parent: Övrigt
nav_order: 10
---
# Funktionell Programmering i Java

Vad är snyggare än ett bra planerat OOP projekt? Funktionell kod! Det är en Snyggare och Bättre Värld av Kod!

## Introduktion

Välkommen till en resa in i den fascinerande världen av funktionell programmering i Java! I Detta avsnitt kommer vi att utforska vad funktionell programmering är och varför det har blivit allt mer populärt inom programmeringsvärlden. Vi kommer att upptäcka hur funktionell kod kan göra våra program mer eleganta, lättlästa och underhållbara. För att illustrera detta kommer vi att jämföra icke-funktionell kod med motsvarande funktionell kod i flera exempel. Låt oss börja resan och låta den funktionella världen av Java ta över!

## TL;DR

I Detta avsnitt har vi utforskat fördelarna med funktionell programmering i Java genom att jämföra icke-funktionell kod med motsvarande funktionell kod. Genom funktionell programmering kan vi skriva snyggare, kortare och mer lättlästa kodavsnitt, vilket gör våra program mer robusta och underhållbara. Genom att använda funktionella koncept som lambda-uttryck och strömmar kan vi skapa eleganta lösningar och förenkla vår kod.

## När du läst detta ska du kunna

- Förstå vad funktionell programmering är och dess fördelar.
- Identifiera situationer där funktionell programmering kan användas.
- Jämföra icke-funktionell kod med funktionell kod och se fördelarna med den senare.
- Skriva funktionell kod med hjälp av lambda-uttryck och strömmar i Java.
- Uppskatta elegansen och snyggheten hos funktionell kod.

## Vad är Funktionell Programmering?

Funktionell programmering är en programmeringsparadigm som behandlar programmering som matematiska funktioner. Det betyder att funktioner i funktionell kod inte har några biverkningar och alltid returnerar samma värde för samma indata. Detta ger oss ren och förutsägbar kod som är lättare att testa och underhålla.

## Fördelar med Funktionell Programmering

Funktionell programmering erbjuder flera fördelar som förbättrar våra program:

1. **Tydligare och mer uttrycksfull kod**: Funktionell kod tenderar att vara mer uttrycksfullt och kortfattat. Detta gör koden lättare att läsa och förstå, vilket ökar dess underhållbarhet.

2. **Minskad mutabilitet**: Funktionell programmering främjar användningen av oföränderliga datastrukturer och undviker mutabilitet. Det minskar risken för buggar relaterade till dataförändringar och gör koden mer robust.

3. **Enklare parallellisering**: Funktionell kod tenderar att vara mer lämpad för parallellisering, vilket gör det enklare att utnyttja flera kärnor och förbättra prestandan.

4. **Färre buggar**: Tack vare oföränderliga datastrukturer och avsaknaden av biverkningar är funktionell kod mindre benägen att innehålla buggar och oväntade sidoeffekter.

## Icke-funktionell kod: Enkel iteration över en lista

Låt oss börja med ett enkelt exempel där vi itererar över en lista av tal och dubblar varje tal i listan.

```java
public class NonFunctionalExample {
    public static void main(String[] args) {

        // Skapa en lista
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // Skapa en lista för resultatet
        List<Integer> doubledNumbers = new ArrayList<>();

        // Helt vanlig foreach-loop
        for (int number : numbers) {
            int doubled = number * 2;
            doubledNumbers.add(doubled);
        }

        // Skriv ut resultatet
        System.out.println(doubledNumbers);
    }
}
```

I detta icke-funktionella exempel använder vi en vanlig for-loop för att iterera över listan `numbers`. Vi multiplicerar varje tal med 2 och lägger sedan till de dubblerade talen i en annan lista `doubledNumbers`.

## Funktionell kod: Dubbla tal med hjälp av strömmar och lambda-uttryck

Nu ska vi omvandla det icke-funktionella exemplet till funktionell kod med hjälp av strömmar och lambda-uttryck.

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

public class FunctionalExample {
    public static void main(String[] args) {

        // Skapa en lista
        List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

        // Skapa en lista för resultatet och fyll den med dubblerade tal
        List<Integer> doubledNumbers = numbers.stream()
                                              .map(number -> number * 2)
                                              .collect(Collectors.toList());

        // Skriv ut resultatet
        System.out.println(doubledNumbers);
    }
}
```

I detta funktionella exempel använder vi strömmar och lambda-uttryck för att uppnå samma resultat. Med `numbers.stream()` omvandlar vi listan `numbers` till en ström och använder sedan `map()` för att dubbla varje tal. Slutligen samlar vi de dubblerade talen i en lista med `collect(Collectors.toList())`.

## Jämförelse och Slutsats
Som vi kan se ger funktionell programmering oss möjligheten att skriva snyggare och kortare kod, vilket gör våra program mer läsbara och underhållbara. Genom att använda strömmar och lambda-uttryck kan vi uttrycka våra intentioner tydligare och undvika onödig kodupprepning.

Funktionell programmering öppnar upp en värld av möjligheter för oss att skapa eleganta och effektiva program i Java. Genom att lära oss de funktionella koncepten kan vi ta vår kod till nya höjder och göra våra programmeringsäventyr ännu roligare och mer givande. Så fortsätt utforska funktionell programmering och låt den ta din kod till nya nivåer av snygghet och effektivitet!

## Obligatorisk dad joke:

Varför älskar programmerare funktionell programmering?

För att det alltid är lambda-gott!
