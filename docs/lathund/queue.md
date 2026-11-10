---
title: "Lathund: Queue"
author: Marcus Ackre Medina
description: "Queue i Java: FIFO med offer, poll och peek, och skillnaden mellan metoder som returnerar null och metoder som kastar undantag."
parent: Lathund
nav_order: 77
---
# Lathund: Queue

En kö följer principen FIFO (First In, First Out): den som kom först är den första som tas om hand, som i en kö vid en biljettlucka. `Queue` är gränssnittet. Skapa den med en implementation, oftast `ArrayDeque`.

Läs mer: [Datastrukturer](../data-structures/index.md).

## Snabbfakta

| Egenskap | Värde |
|---|---|
| Typ | `Queue<E>` (gränssnitt). Skapas som `ArrayDeque<E>` |
| Princip | FIFO, först in först ut |
| Lägg till | I slutet av kön |
| Ta bort och titta | Från början av kön |
| Null | Tillåtet inte i `ArrayDeque` |
| Import | `java.util.ArrayDeque`, `java.util.Queue` |

## Operationer

Exemplen utgår från `Queue<String> biljetter = new ArrayDeque<>();`

| Operation | Betydelse | Exempel | Resultat |
|---|---|---|---|
| Ställ dig sist | `offer(element)` | `biljetter.offer("Marcus");` | `true` |
| Ta första | `poll()`, `null` om tom | `biljetter.poll()` | Returnerar `"Marcus"` och tar bort |
| Titta på första | `peek()`, `null` om tom | `biljetter.peek()` | Returnerar första, tar inte bort |
| Antal | `size()` | `biljetter.size()` | Antalet i kön |
| Tom | `isEmpty()` | `biljetter.isEmpty()` | `true` eller `false` |
| Ta bort specifik | `remove(element)` | `biljetter.remove("Anna");` | `true` om den fanns |
| Finns | `contains(element)` | `biljetter.contains("Anna")` | `true` eller `false` |
| Töm | `clear()` | `biljetter.clear();` | Tom kö |

Samma sak i ett körbart program:

```java
import java.util.ArrayDeque;
import java.util.Queue;

public class QueueExempel {
    public static void main(String[] args) {
        // Skapar en kö av personer som väntar på biljett
        Queue<String> biljetter = new ArrayDeque<>();

        biljetter.offer("Marcus");                      // Ställer sig sist
        biljetter.offer("Anna");
        System.out.println(biljetter.peek());           // Marcus, först i kön

        // Betjänar kön tills den är tom
        while (!biljetter.isEmpty()) {
            String person = biljetter.poll();           // Tar den första i kön
            System.out.println(person + " får en biljett");
        }
    }
}
```

## Jämförelser

### Två uppsättningar metoder

`Queue` har två uppsättningar metoder för samma sak. Skillnaden syns när kön är tom eller full.

| Uppgift | Returnerar `null` eller `false` | Kastar undantag |
|---|---|---|
| Lägg till sist | `offer(element)` | `add(element)` |
| Ta första | `poll()` | `remove()` |
| Titta på första | `peek()` | `element()` |

Använd `offer`, `poll` och `peek` när en tom kö är en normal situation. Använd `add`, `remove` och `element` när en tom kö är ett fel.

### Implementation

<details>
<summary>ArrayDeque (rekommenderas)</summary>

```java
Queue<String> biljetter = new ArrayDeque<>();
```

Snabb och tillåter inte `null`.

</details>

<details>
<summary>LinkedList</summary>

```java
Queue<String> biljetter = new LinkedList<>();
```

Fungerar också som kö och tillåter `null`. Använd den om du behöver `null` i kön, annars är `ArrayDeque` ofta bättre.

</details>

## Vanliga misstag

- `Queue` är ett gränssnitt, så `new Queue<>()` fungerar inte. Skapa med en implementation, till exempel `new ArrayDeque<>()`.
- `poll()` på en tom kö returnerar `null`. Om du packar upp det direkt i ett `int` eller använder det som om det vore ett objekt får du `NullPointerException`. Kontrollera med `isEmpty()` först.
- `ArrayDeque` tillåter inte `null`. `offer(null)` kastar `NullPointerException`.
- Kön är inte sorterad efter någonting annat än när elementen kom in. Vill du ha prioritet, använd `PriorityQueue`.

## Terminologi

| Term | Betydelse |
|---|---|
| Queue | Gränssnitt för en kö där det först inlagda tas ut först |
| FIFO | First In, First Out. Först in, först ut |
| Offer | Att lägga till sist i kön |
| Poll | Att ta bort och returnera den första i kön |
| Peek | Att titta på den första i kön utan att ta bort den |
| Kö | Svensk term för en samling där elementen behandlas i ankomstordning |
