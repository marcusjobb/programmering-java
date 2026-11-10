---
title: "Lathund: Stack"
author: Marcus Ackre Medina
description: "Stack i Java i lathundsform: LIFO med push, pop och peek, med Deque och ArrayDeque som rekommenderat val."
parent: Lathund
nav_order: 76
---
# Lathund: Stack

En stack följer principen LIFO (Last In, First Out): det du lade sist på stapeln är det första du tar av. Java har en klass som heter `Stack`, men den är gammal. Använd i stället `Deque` med implementationen `ArrayDeque`, som har samma metoder och är snabbare.

Läs mer: [Datastrukturer](../data-structures/index.md).

## Snabbfakta

| Egenskap | Värde |
|---|---|
| Typ | `Deque<E>` (gränssnitt). Skapas som `ArrayDeque<E>` |
| Princip | LIFO, sist in först ut |
| Topp | Det element som lades till senast |
| Null | Tillåtet inte i `ArrayDeque` |
| Import | `java.util.ArrayDeque`, `java.util.Deque` |

## Operationer

Exemplen utgår från `Deque<String> böcker = new ArrayDeque<>();`

| Operation | Betydelse | Exempel | Resultat |
|---|---|---|---|
| Lägg på toppen | `push(element)` | `böcker.push("Harry Potter");` | `"Harry Potter"` är överst |
| Ta bort från toppen | `pop()`, kastar om tom | `böcker.pop()` | Returnerar `"Harry Potter"` |
| Titta på toppen | `peek()`, `null` om tom | `böcker.peek()` | Returnerar toppen, tar inte bort den |
| Antal | `size()` | `böcker.size()` | Antalet element |
| Tom | `isEmpty()` | `böcker.isEmpty()` | `true` eller `false` |
| Töm | `clear()` | `böcker.clear();` | Tom stack |

Samma sak i ett körbart program:

```java
import java.util.ArrayDeque;
import java.util.Deque;

public class StackExempel {
    public static void main(String[] args) {
        // Skapar en stack av böcker
        Deque<String> böcker = new ArrayDeque<>();

        böcker.push("Harry Potter");
        böcker.push("Sagan om ringen");

        System.out.println(böcker.peek());              // Sagan om ringen, överst

        // Tar bort så länge det finns något på stapeln
        while (!böcker.isEmpty()) {
            String bok = böcker.pop();
            System.out.println("Tar bort: " + bok);
        }
        // Utskrift: Sagan om ringen, sedan Harry Potter
    }
}
```

## Jämförelser

### Deque eller den gamla Stack-klassen

Båda fungerar för en stack, men de skiljer sig i detaljer.

<details>
<summary>ArrayDeque med Deque (rekommenderas)</summary>

```java
Deque<String> böcker = new ArrayDeque<>();
```

- `pop` och `peek` returnerar `null` eller kastar `NoSuchElementException` vid tom stack, beroende på metod.
- En `for-each`-loop går från toppen och ner till botten.
- Det är den moderna varianten och den du bör använda i ny kod.

</details>

<details>
<summary>Stack (äldre klass)</summary>

```java
Stack<String> böcker = new Stack<>();
```

- `pop` och `peek` kastar `EmptyStackException` vid tom stack.
- `search(objekt)` ger avståndet från toppen, där toppen är 1.
- En `for-each`-loop går från botten och upp till toppen, vilket är motsatsen mot `Deque`.
- Klassen ärver från `Vector` och används främst i gammal kod.

</details>

## Vanliga misstag

- `pop()` på en tom `ArrayDeque` kastar `NoSuchElementException`. Kontrollera med `isEmpty()` först, eller använd `pollFirst()` som returnerar `null` i stället.
- `ArrayDeque` tillåter inte `null`. `push(null)` kastar `NullPointerException`.
- Använd inte `Stack` i ny kod. Skriv `Deque` och skapa med `ArrayDeque`.
- Stacken har bara åtkomst till toppen. Vill du komma åt ett element i mitten behöver du en annan datastruktur, till exempel en lista.

## Terminologi

| Term | Betydelse |
|---|---|
| Stack | Datastruktur där det senast tillagda elementet tas ut först |
| LIFO | Last In, First Out. Sist in, först ut |
| Topp | Elementet som ligger överst och som `pop` och `peek` arbetar med |
| Push | Att lägga ett element på toppen |
| Pop | Att ta bort och returnera toppen |
| Deque | Gränssnitt för en kö som går att använda från båda ändarna, double-ended queue |
