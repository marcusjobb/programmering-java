---
title: "Lathund: List och ArrayList"
author: Marcus Ackre Medina
description: "List och ArrayList i Java i lathundsform: skapa, lägga till, ta bort, söka, sortera och loopa."
parent: Lathund
nav_order: 72
---
# Lathund: List och ArrayList

`List` är Javas gränssnitt för en ordnad samling där dubbletter är tillåtna och där du kommer åt elementen med index. `ArrayList` är den vanligaste implementationen och den du oftast skapar. Du skriver variabeln som `List` och skapar den som `ArrayList`.

Läs mer: [Datastrukturer](../data-structures/index.md).

## Snabbfakta

| Egenskap | Värde |
|---|---|
| Typ | `List<E>` (gränssnitt). Skapas som `ArrayList<E>` |
| Ordning | Bevaras. Elementen ligger i den ordning du lade in dem |
| Dubbletter | Tillåtna |
| Index | Börjar på 0 |
| Storlek | Växer automatiskt. Läses med `size()` |
| Import | `java.util.ArrayList`, `java.util.List`, `java.util.Comparator` |

## Operationer

Exemplen utgår från `List<Integer> tal = new ArrayList<>(List.of(3, 7, 4));`, så listan innehåller `[3, 7, 4]`.

| Operation | Betydelse | Exempel | Resultat |
|---|---|---|---|
| Lägg till sist | `add(element)` | `tal.add(5);` | `[3, 7, 4, 5]` |
| Lägg till på plats | `add(index, element)` | `tal.add(1, 9);` | `[3, 9, 7, 4]` |
| Hämta | `get(index)` | `tal.get(0)` | `3` |
| Ändra | `set(index, element)` | `tal.set(1, 9);` | `[3, 9, 4]` |
| Ta bort på index | `remove(index)` | `tal.remove(0);` | `[7, 4]` |
| Ta bort värde | `remove(Object)` | `tal.remove(Integer.valueOf(7));` | `[3, 4]` |
| Antal | `size()` | `tal.size()` | `3` |
| Finns värdet | `contains(element)` | `tal.contains(7)` | `true` |
| Position | `indexOf(element)`, `-1` om det saknas | `tal.indexOf(4)` | `2` |
| Sortera | `sort(Comparator)` | `tal.sort(Comparator.naturalOrder());` | `[3, 4, 7]` |
| Första och sista | `getFirst()`, `getLast()` (Java 21) | `tal.getFirst()` | `3` |
| Tom | `isEmpty()` | `tal.isEmpty()` | `false` |
| Töm | `clear()` | `tal.clear();` | `[]` |
| Del av listan | `subList(från, till)` | `tal.subList(0, 2)` | `[3, 7]` |

Samma sak i ett körbart program:

```java
import java.util.ArrayList;
import java.util.Comparator;
import java.util.List;

public class ListExempel {
    public static void main(String[] args) {
        // Skapar en föränderlig lista med tre heltal
        List<Integer> tal = new ArrayList<>(List.of(3, 7, 4));

        tal.add(5);                                     // [3, 7, 4, 5]
        tal.set(1, 9);                                  // [3, 9, 4, 5]
        tal.remove(Integer.valueOf(9));                 // Tar bort värdet 9: [3, 4, 5]
        System.out.println(tal.get(0));                 // 3

        // Loopar genom alla element
        for (int siffra : tal) {
            System.out.println(siffra);
        }

        tal.sort(Comparator.naturalOrder());            // Sorterar stigande
        System.out.println(tal);                        // [3, 4, 5]
    }
}
```

## Jämförelser

### Två sätt att skapa en lista

Båda skapar en `List`, men de skiljer sig i om listan går att ändra.

<details>
<summary>Föränderlig lista med ArrayList</summary>

```java
List<String> namn = new ArrayList<>();
namn.add("Kalle");   // Fungerar
```

Använd den här när du ska lägga till, ta bort eller ändra element.

</details>

<details>
<summary>Oföränderlig lista med List.of</summary>

```java
List<String> namn = List.of("Kalle", "Pelle");
namn.add("Tjalle");  // Kastar UnsupportedOperationException
```

Använd den här när listan ska vara fast, till exempel en lista med konstanta värden.

</details>

### Lista eller array

Se [Arrayer](arrays.md) för en jämförelse mellan array och lista.

## Vanliga misstag

- `remove(7)` på en `List<Integer>` tar bort elementet på index 7, inte värdet 7. För att ta bort värdet använd `remove(Integer.valueOf(7))`.
- `tal.sort()` utan argument finns inte på `List`. Skicka med en `Comparator`, till exempel `Comparator.naturalOrder()`.
- `get(index)` och `set(index, ...)` med ogiltigt index kastar `IndexOutOfBoundsException`.
- Att ändra listan i en `for-each`-loop kastar `ConcurrentModificationException`. Samla de element du vill ta bort i en ny lista och ta bort dem efter loopen, eller använd `removeIf`.
- `subList` ger en vy av originallistan. Vill du ha en fristående kopia, skriv `new ArrayList<>(tal.subList(0, 2))`.

## Terminologi

| Term | Betydelse |
|---|---|
| List | Gränssnitt för en ordnad samling med index |
| ArrayList | Implementation av `List` som bygger på en array som växer |
| Index | Platsens nummer, börjar på 0 |
| Generics (`<E>`) | Anger vilken typ listan innehåller, till exempel `<Integer>` |
| Autoboxing | Java omvandlar automatiskt `int` till `Integer` när du lägger till i listan |
| Oföränderlig | Går inte att ändra efter att den skapats, till exempel `List.of` |
