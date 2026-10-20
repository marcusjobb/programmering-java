---
title: Do While
author: Marcus Ackre Medina
parent: Loopar
nav_order: 60
---
# Do While

En artikel som utforskar Do While-loopen i Java och dess användningsområden för att köra kodblock minst en gång och sedan fortsätta så länge som ett villkor är sant.

## När du läst detta ska du kunna

- Förstå hur Do While-loopen fungerar och dess skillnad jämfört med andra loopstrukturer.
- Använda Do While-loopen för att upprepa kod minst en gång innan villkoret kontrolleras.
- Tillämpa Do While-loopen i praktiska kodexempel.

## Beskrivning

Do While är en loopstruktur i Java som liknar While-loopen. Skillnaden är att i en Do While-loop kontrolleras villkoret efter varje iteration, vilket innebär att loopen alltid körs minst en gång. Detta är användbart när du vill att en viss kod ska utföras minst en gång innan villkoret kontrolleras.

## Exempel

För att förstå hur en Do While-loop fungerar, låt oss titta på följande kodexempel:

```java
int i = 0;
do {
    System.out.println(i);
    i++;
} while (i < 10);
```

I detta exempel deklarerar vi en variabel `i` och tilldelar den värdet 0. Sedan har vi en Do While-loop som kontrollerar om `i` är mindre än 10. Inuti loopen skriver den ut värdet av `i` och ökar sedan värdet med 1. Loopen fortsätter att köras så länge som `i` är mindre än 10.

Output:

```text
0
1
2
3
4
5
6
7
8
9
```

Medan villkoret i Do While-loopen är sant, körs koden inuti loopen. När villkoret blir falskt, avslutas loopen och programmet fortsätter med resten av koden efter loopen.

I detta specifika exempel kommer loopen att köra 10 gånger och skriva ut värdena från 0 till 9.

## Summan av kardemumman

Do While är en loopstruktur i Java som körs minst en gång och sedan fortsätter att köra så länge som villkoret är sant. Det är användbart när du behöver utföra en viss kod minst en gång innan villkoret kontrolleras.

## Termer

| Term          | Förklaring                                                                                                          |
| ------------- | ------------------------------------------------------------------------------------------------------------------- |
| Do While-loop | En loopstruktur i Java som körs minst en gång och sedan fortsätter att köra så länge som villkoret är sant.         |
| Loop          | En struktur i programmering som gör att en viss kod kan köras upprepade gånger tills ett visst villkor är uppfyllt. |
| Iteration     | En enskild körning av kod inuti en loop.                                                                            |
| Villkor       | Ett uttryck som avgör om en loop ska fortsätta köras eller inte.                                                    |

## Obligatorisk Dad-joke

Varför älskar programmerare Do While-loopen?

För att de alltid får ett *bra* resultat - minst en gång! 😄

## Obligatoriskt sista ordet

Do While-loopen är en användbar loopstruktur i Java som låter oss köra kod minst en gång och sedan fortsätta så länge som ett villkor är sant. Genom att förstå hur denna loop fungerar kan du skapa mer dynamiska och effektiva program. Fortsätt experimentera med olika loopstrukturer och fortsätt ha kul med programmering! Ha en fantastisk dag!
