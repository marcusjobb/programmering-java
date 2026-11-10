---
title: "Lathund: Arrayer"
author: Marcus Ackre Medina
description: "Arrayer i Java i lathundsform: skapa, läsa, ändra, sortera och kopiera med hjälp av klassen Arrays."
parent: Lathund
nav_order: 71
---
# Lathund: Arrayer

En array är en lista med fast storlek där alla element har samma typ. Storleken bestäms när arrayen skapas och ändras inte efteråt. Behöver du en lista som växer, använd [List](list.md).

Läs mer: [Datastrukturer](../data-structures/index.md).

## Snabbfakta

| Egenskap | Värde |
|---|---|
| Typ | `int[]`, `String[]` osv. Alla element är av samma typ |
| Storlek | Fast. Sätts vid skapandet |
| Index | Börjar på 0. Sista index är `längd - 1` |
| Längd | `array.length` (utan parenteser, till skillnad från `size()` i listor) |
| Standardvärden | `0` för tal, `false` för `boolean`, `null` för objekt |
| Import | `java.util.Arrays` för hjälpmetoderna |

## Operationer

Exemplen utgår från arrayen `int[] tal = {3, 7, 4};`

| Operation | Betydelse | Exempel | Resultat |
|---|---|---|---|
| Läsa | Hämta element på index | `tal[0]` | `3` |
| Ändra | Skriva över element på index | `tal[1] = 9;` | `tal` blir `[3, 9, 4]` |
| Längd | Antal platser | `tal.length` | `3` |
| Skriva ut | Gör om arrayen till text | `Arrays.toString(tal)` | `"[3, 7, 4]"` |
| Sortera | Sorterar arrayen på plats | `Arrays.sort(tal);` | `tal` blir `[3, 4, 7]` |
| Fylla | Sätter alla platser till samma värde | `Arrays.fill(tal, 0);` | `tal` blir `[0, 0, 0]` |
| Kopiera | Ny array med angiven längd. Nya platser får standardvärde | `Arrays.copyOf(tal, 5)` | `[3, 7, 4, 0, 0]` |

Samma sak i ett körbart program:

```java
import java.util.Arrays;

public class ArrayExempel {
    public static void main(String[] args) {
        // Skapar en array med tre heltal
        int[] tal = {3, 7, 4};

        System.out.println(tal[0]);                     // 3, index börjar på 0
        tal[1] = 9;                                     // Ändrar andra platsen
        System.out.println(Arrays.toString(tal));       // [3, 9, 4]

        // Loopar genom alla element
        for (int siffra : tal) {
            System.out.println(siffra);
        }

        Arrays.sort(tal);                               // Sorterar på plats
        System.out.println(Arrays.toString(tal));       // [3, 4, 9]

        // Kopierar till en ny array som är längre. Originalet ändras inte.
        int[] kopia = Arrays.copyOf(tal, 5);
        System.out.println(Arrays.toString(kopia));     // [3, 4, 9, 0, 0]
    }
}
```

## Jämförelser

Array och lista används för samma sak men skiljer sig på några punkter.

| Egenskap | Array | List (ArrayList) |
|---|---|---|
| Storlek | Fast | Växer och krymper |
| Typ för heltal | `int[]`, primitiv | `List<Integer>`, objekt |
| Längd | `array.length` | `list.size()` |
| Läsa element | `array[i]` | `list.get(i)` |
| Hjälpmetoder | `java.util.Arrays` | Metoder direkt på listan |

## Vanliga misstag

- Index utanför intervallet kastar `ArrayIndexOutOfBoundsException`. Med tre platser är giltiga index 0, 1 och 2.
- `System.out.println(tal)` skriver ut arrayens minnesadress (till exempel `[I@1b6d3586`), inte innehållet. Använd `Arrays.toString(tal)`.
- `tal1 == tal2` jämför om det är samma array, inte om innehållet är lika. Använd `Arrays.equals(tal1, tal2)`.
- `Arrays.copyOf` skapar en ny array. Ändrar du kopian ändras inte originalet, och tvärtom.

## Terminologi

| Term | Betydelse |
|---|---|
| Array | Samling med fast storlek där alla element har samma typ |
| Index | Platsens nummer, börjar på 0 |
| Element | Ett värde i arrayen |
| Längd | Antalet platser, `length` |
| Standardvärde | Värdet en plats får när arrayen skapas utan värden |
