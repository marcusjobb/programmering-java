---
title: Loop kontroller
author: Marcus Ackre Medina
parent: Loopar
nav_order: 90
---
# Loop kontroller

I den här övningen kommer vi att utforska olika loopkontroller som ger oss mer kontroll över hur loopar beter sig i programmering. Dessa loopkontroller inkluderar `break`, `continue`, `return`, och `yield`.

## TL;DR

Loopkontroller ger oss möjlighet att anpassa loopars beteende. `break` avbryter en loop, `continue` hoppar över en iteration, `return` avslutar en metod, och `yield` avslutar en iterator. Genom att använda dessa loopkontroller kan vi skräddarsy våra loopar efter våra behov och förbättra våra programmeringsfärdigheter.

## Vad är Loopkontroller?

Loopkontroller är verktyg som används för att modifiera och anpassa beteendet hos loopar i programmering. Genom att använda loopkontroller kan vi avbryta en loop innan den är klar, hoppa över vissa iterationer eller till och med avsluta en hel metod eller iterator.

## Break - Avbryt en Loop

`break` används för att avbryta en loop innan den har gått igenom alla sina iterationer. Detta kan vara användbart när vi vill avsluta en loop baserat på ett visst villkor.

```java
int max = 5;
for(int i = 0; i < 10; i++) {
    if(i >= max) {
        break;
    }
    System.out.println(i);
}
```

Resultatet av koden ovan kommer att vara:

```text
0
1
2
3
4
```

I detta exempel använder vi `break` för att avsluta loopen när variabeln `i` når värdet som är lika med eller större än `max`.

## Continue - Hoppa över en Iteration

`continue` används för att hoppa över en iteration i en loop. Detta innebär att alla kodrader efter `continue` för den aktuella iterationen kommer att ignoreras, och loopen går vidare till nästa iteration.

```java
int mod=3;
for(int i = 0; i < 10; i++) {
    if(i % mod == 0) {
        continue;
    }
    System.out.println(i);
}
```

Resultatet av koden ovan kommer att vara:

```text
1
2
4
5
7
8
```

Här använder vi `continue` för att hoppa över alla tal i loopen som är jämnt delbara med värdet av variabeln `mod`.

## Return - Avsluta en Metod

`return` används för att avsluta en metod innan den är klar. När `return` nås avslutas metoden omedelbart, och alla kvarvarande kodblokkar efter `return` kommer inte att utföras.

```java
public static void main(String[] args) {
    int max = 5;
    for(int i = 0; i < 10; i++) {
        if(i >= max) {
            return;
        }
        System.out.println(i);
    }
}
```

Resultatet av koden ovan kommer att vara:

```text
0
1
2
3
4
```

I detta exempel avslutas hela `main`-metoden när `return`-uttrycket körs.

## Yield - Avsluta en Iterator

`yield` används för att avsluta en iterator innan den är klar. Detta kan vara användbart om vi vill avsluta en iterator när ett visst villkor är uppfyllt.

```java
public static void main(String[] args) {
    int max = 5;
    for(int i = 0; i < 10; i++) {
        if(i >= max) {
            yield;
        }
        System.out.println(i);
    }
}
```

Resultatet av koden ovan kommer att vara:

```text
0
1
2
3
4
```

I detta exempel använder vi `yield` för att avsluta hela iteratorn när variabeln `i` blir lika med eller större än `max`. Skillnaden mellan `break` och `yield` är att `yield` avslutar hela iteratorn, medan `break` bara avslutar loopen.

## Summan av kardemumman

Loopkontroller ger oss möjlighet att ha mer kontroll över loopar i programmering. Genom att använda `break`, `continue`, `return`, och `yield`, kan vi anpassa loopar och metoder efter våra behov.

## Termer

Här är en lista över termer som används i artikeln:

| Term     | Förklaring                                                         |
| -------- | ------------------------------------------------------------------ |
| break    | Avbryter en loop eller en switch-sats när ett villkor är uppfyllt. |
| continue | Hoppa över en iteration i en loop när ett villkor är uppfyllt.     |
| return   | Avsluta en metod och returnera tillbaka till den anropande koden.  |
| yield    | Avsluta en iterator när ett villkor är uppfyllt.                   |

## Slutsats

Loopkontroller ger oss verktyg för att forma loopar och metoder på ett mer flexibelt sätt. Genom att använda `break`, `continue`, `return`, och `yield` kan vi förbättra kontrollen och prestandan i våra program.
