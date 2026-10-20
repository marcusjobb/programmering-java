---
title: ArrayCopy
grand_parent: Datastrukturer
author: Marcus Ackre Medina
parent: Array övningar
nav_order: 20
---
# ArrayCopy

## När du läst detta ska du kunna

- Förstå hur man plockar ut en del av en array och skapar en ny array i Java.
- Använda `System.arraycopy` för att kopiera delar av en array till en ny array.
- Utforska andra metoder för att kopiera delar av en array, såsom `Arrays.copyOfRange` eller manuell kopiering med `for`-loop.

## Introduktion

I detta exempel visar vi hur du kan plocka ut en del av en array och skapa en ny array av det i Java. Detta kan vara användbart när du vill använda en delmängd av en befintlig array för att skapa en ny array.

## Kodexempel

```java
public class MainClass {
    public static void main(String[] args) {
        // Skapa en array med 10 heltal
        int[] integer = { 5, 2, 7, 1, 9, 3, 8, 4, 6, 10 };

        // Skriv ut den ursprungliga arrayen
        System.out.print("Siffror: ");
        printArray(integer);

        // Skapa en ny array som innehåller de fem första talen i den ursprungliga arrayen
        int[] femForsta = new int[5];
        System.arraycopy(integer, 0, femForsta, 0, 5);

        // Skriv ut den nya arrayen
        System.out.print("De fem första talen: ");
        printArray(femForsta);

        System.out.println();
    }

    private static void printArray(int[] array) {
        for (int num : array) {
            System.out.print(num + " ");
        }
    }
}
```

## Resultat

```text
Siffror: 5 2 7 1 9 3 8 4 6 10
De fem första talen: 5 2 7 1 9
```

I det här exemplet skapar vi en array `integer` med 10 heltal. Sedan använder vi `System.arraycopy` för att kopiera de fem första talen från `integer` till en ny array `femForsta`. Vi skriver ut både den ursprungliga arrayen och den nya arrayen genom att använda metoden `printArray`.

## Metoden `printArray`

Metoden `printArray` används för att skriva ut innehållet i en array. Den använder en förbättrad `for`-loop för att iterera över varje element i arrayen och skriva ut det. Detta ger oss en enkel och läsbar sätt att visa innehållet i en array.

## Alternativa sätt att kopiera delar av en array

Det finns flera sätt att kopiera delar av en array i Java. Istället för att använda `System.arraycopy` kan du även använda metoden `Arrays.copyOfRange` för att skapa en ny array med en del av den ursprungliga arrayen. Detta gör att du kan kopiera delen med en enda metodanrop.

```java
int[] femForsta = Arrays.copyOfRange(integer, 0, 5);
```

En annan möjlighet är att använda en `for`-loop för att manuellt kopiera elementen från den ursprungliga arrayen till den nya arrayen.

Det är alltid bra att experimentera och utforska olika sätt att lösa problemet på egen hand. Genom att göra det kan du utöka din förståelse för arrayer och Java-programmering som helhet.

## Avslutande ord

Jag hoppas att detta exempel har varit användbart för dig att förstå hur man plockar ut en del av en array och skapar en ny array i Java. Att kunna hantera arrayer och kopiera deras innehåll är viktiga färdigheter inom programmering. Om du har fler frågor eller behöver ytterligare hjälp, tveka inte att fråga!
