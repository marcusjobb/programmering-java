---
title: "Lathund: LinkedList"
author: Marcus Ackre Medina
description: "LinkedList i Java i lathundsform: lägga till och ta bort i början och slutet, hämta element och när den är bättre än ArrayList."
parent: Lathund
nav_order: 73
---
# Lathund: LinkedList

`LinkedList` är en lista där varje element pekar på nästa element. Det är snabbt att lägga till och ta bort i början och slutet, men långsamt att hoppa till ett element på en viss position. Den implementerar både `List` och `Deque`, så den kan användas som lista, kö eller stack.

Läs mer: [Datastrukturer](../data-structures/index.md).

## Snabbfakta

| Egenskap | Värde |
|---|---|
| Typ | `LinkedList<E>`, implementerar `List<E>` och `Deque<E>` |
| Struktur | Noder som pekar på nästa element (och föregående) |
| Ordning | Bevaras |
| Dubbletter | Tillåtna |
| Null | Tillåtet |
| Import | `java.util.LinkedList`, `java.util.List` |

## Operationer

Exemplen utgår från `LinkedList<String> stationer = new LinkedList<>(List.of("Stockholm", "Uppsala"));`.

| Operation | Betydelse | Exempel | Resultat |
|---|---|---|---|
| Lägg till sist | `add(element)` | `stationer.add("Västerås");` | `[Stockholm, Uppsala, Västerås]` |
| Lägg till först | `addFirst(element)` | `stationer.addFirst("Solna");` | `[Solna, Stockholm, Uppsala]` |
| Ta bort först | `removeFirst()` | `stationer.removeFirst();` | Returnerar `"Stockholm"` |
| Ta bort sist | `removeLast()` | `stationer.removeLast();` | Returnerar `"Uppsala"` |
| Ta bort värde | `remove(Object)` | `stationer.remove("Uppsala");` | `true`, listan blir `[Stockholm]` |
| Hämta första | `getFirst()` | `stationer.getFirst()` | `"Stockholm"` |
| Hämta på index | `get(index)`, långsam | `stationer.get(1)` | `"Uppsala"` |
| Antal | `size()` | `stationer.size()` | `2` |
| Tom | `isEmpty()` | `stationer.isEmpty()` | `false` |

Samma sak i ett körbart program:

```java
import java.util.LinkedList;
import java.util.List;

public class LinkedListExempel {
    public static void main(String[] args) {
        // Skapar en lista med två stationer
        LinkedList<String> stationer = new LinkedList<>(List.of("Stockholm", "Uppsala"));

        stationer.add("Västerås");                      // Läggs sist
        stationer.addFirst("Solna");                    // Läggs först
        System.out.println(stationer);                  // [Solna, Stockholm, Uppsala, Västerås]

        String forsta = stationer.removeFirst();        // Tar bort och returnerar "Solna"
        System.out.println(forsta);

        // Loopar genom alla stationer
        for (String station : stationer) {
            System.out.println(station);
        }
    }
}
```

## Jämförelser

`ArrayList` är oftast det bästa valet. `LinkedList` vinner bara när du ofta lägger till eller tar bort i början eller slutet.

| Operation | ArrayList | LinkedList |
|---|---|---|
| Hämta på index (`get`) | Snabb | Långsam, går igenom listan |
| Lägg till och ta bort först | Långsam, flyttar alla element | Snabb |
| Lägg till och ta bort sist | Snabb | Snabb |
| Minnesåtgång per element | Lägre | Högre, pekare till nästa element |

## Vanliga misstag

- Att loopa med `get(i)` på en `LinkedList` blir långsamt, eftersom varje `get` går igenom listan från början. Använd `for-each`-loopen.
- `add(index, element)` måste också gå till positionen först, så den är inte snabb bara för att det är en `LinkedList`.
- `removeFirst()` och `getFirst()` på en tom lista kastar `NoSuchElementException`. Kontrollera med `isEmpty()` först.
- Om du bara behöver en kö eller en stack är `ArrayDeque` oftast snabbare och tydligare. Se [Queue](queue.md) och [Stack](stack.md).

## Terminologi

| Term | Betydelse |
|---|---|
| Nod | Ett element i listan tillsammans med pekaren till nästa |
| Pekare (referens) | Något som visar var nästa nod finns i minnet |
| Dubbellänkad lista | Lista där varje nod pekar både framåt och bakåt, som `LinkedList` i Java |
| Sekventiell åtkomst | Att gå igenom elementen ett i taget från början |
