---
title: "Lathund: HashSet"
author: Marcus Ackre Medina
description: "HashSet i Java i lathundsform: unika element, snabb sökning med contains, och varför ordningen inte är garanterad."
parent: Lathund
nav_order: 75
---
# Lathund: HashSet

`HashSet` är en samling där varje element bara finns en gång. Den är snabb på att svara på frågan "finns det här?", men den garanterar ingen ordning. Du skriver variabeln som `Set` och skapar den som `HashSet`.

Läs mer: [Datastrukturer](../data-structures/index.md).

## Snabbfakta

| Egenskap | Värde |
|---|---|
| Typ | `Set<E>` (gränssnitt). Skapas som `HashSet<E>` |
| Dubbletter | Otillåtna. `add` returnerar `false` för en dubblett |
| Ordning | Ingen garanterad ordning |
| Sök med `contains` | Snabb |
| Null | Ett `null`-element är tillåtet |
| Import | `java.util.HashSet`, `java.util.Set` |

## Operationer

Exemplen utgår från `Set<String> skatter = new HashSet<>();`

| Operation | Betydelse | Exempel | Resultat |
|---|---|---|---|
| Lägg till | `add(element)` | `skatter.add("Guld");` | `true` |
| Lägg till dubblett | `add` med samma värde | `skatter.add("Guld");` | `false`, ingen ändring |
| Ta bort | `remove(element)` | `skatter.remove("Guld");` | `true` |
| Finns | `contains(element)` | `skatter.contains("Guld")` | `true` eller `false` |
| Antal | `size()` | `skatter.size()` | Antalet unika element |
| Tom | `isEmpty()` | `skatter.isEmpty()` | `true` eller `false` |
| Lägg till flera | `addAll(samling)` | `skatter.addAll(List.of("Silver", "Brons"));` | Lägger till alla som inte finns |
| Behåll gemensamma | `retainAll(samling)` | `skatter.retainAll(List.of("Silver"));` | Behåller bara de som finns i båda |
| Töm | `clear()` | `skatter.clear();` | Tom mängd |

Samma sak i ett körbart program:

```java
import java.util.HashSet;
import java.util.Set;

public class HashSetExempel {
    public static void main(String[] args) {
        // Skapar en mängd med unika skatter
        Set<String> skatter = new HashSet<>();

        skatter.add("Guld");
        skatter.add("Silver");
        boolean nyTillagd = skatter.add("Guld");       // Redan där, så false
        System.out.println(nyTillagd);                  // false
        System.out.println(skatter.size());             // 2

        if (skatter.contains("Silver")) {
            System.out.println("Silver finns i kistan");
        }

        // Loopar genom alla skatter. Ordningen är inte garanterad.
        for (String skatt : skatter) {
            System.out.println(skatt);
        }
    }
}
```

## Jämförelser

### Tre implementationer av Set

Alla tre förhindrar dubbletter. De skiljer sig i ordningen.

<details>
<summary>HashSet: ingen ordning</summary>

```java
Set<String> skatter = new HashSet<>();
```

Snabbast. Det vanligaste valet när du bara vill veta om något finns med.

</details>

<details>
<summary>LinkedHashSet: i den ordning du lade in dem</summary>

```java
Set<String> skatter = new LinkedHashSet<>();
```

Använd när du vill att utskriften ska följa insättningsordningen.

</details>

<details>
<summary>TreeSet: sorterad</summary>

```java
Set<String> skatter = new TreeSet<>();
```

Använd när du vill ha elementen sorterade. Elementen måste gå att jämföra.

</details>

### Lista eller mängd

| Egenskap | List (ArrayList) | Set (HashSet) |
|---|---|---|
| Dubbletter | Tillåtna | Otillåtna |
| Ordning | Bevaras | Ingen garanterad |
| Sök med `contains` | Går igenom listan | Snabb |
| Hämta med index | Ja, `get(i)` | Nej |

## Vanliga misstag

- Att förvänta sig en viss ordning i en `HashSet`. Ordningen kan ändras mellan körningar och mellan Java-versioner.
- `add` returnerar `false` vid dubbletter, men kastar inget fel. Kontrollera returvärdet om du behöver veta det.
- Egna klasser i en `HashSet` behöver `equals` och `hashCode`. En `record` får dem automatiskt.
- Om du ändrar ett objekt som ligger i mängden, så att dess `hashCode` ändras, hittar `contains` det inte längre.

## Terminologi

| Term | Betydelse |
|---|---|
| Set | Gränssnitt för en samling utan dubbletter |
| HashSet | Implementation av `Set` som använder hashning för snabb sökning |
| Dubblett | Ett element som redan finns i mängden |
| Hashkod (`hashCode`) | Ett tal som räknas ut ur ett objekt och används för att hitta det snabbt |
| Mängd | Svensk term för en samling utan dubbletter och utan ordning |
