---
title: Invertera en array
grand_parent: Datastrukturer
author: Marcus Ackre Medina
parent: Array övningar
nav_order: 50
---
# Invertera en array

## Beskrivning av övningen

Denna övning handlar om att skriva en metod som inverterar ordningen på elementen i en array av strängar. Metoden ska returnera den resulterande inverterade arrayen.

## Kodmall

```java
public class Main {
    public static String[] reverseArray(String[] words) {
        // Implementera kod här
    }

    public static void main(String[] args) {
        String[] words = { "Katt", "Hund", "Kanin", "Capybara" };
        String[] reversed = reverseArray(words);
        System.out.println(String.join(", ", reversed));
    }
}
```

## Förväntad output

Förväntad output efter att metoden `reverseArray` har implementerats korrekt:

```text
Capybara, Kanin, Hund, Katt
```

## Implementering

För att lösa denna uppgift kan vi använda en enkel algoritm som skapar en ny array och fyller den med elementen från den ursprungliga arrayen, fast i omvänd ordning.

```java
public static String[] reverseArray(String[] words) {
    String[] reversed = new String[words.length];
    int index = 0;
    for (int i = words.length - 1; i >= 0; i--) {
        reversed[index] = words[i];
        index++;
    }
    return reversed;
}
```

I denna implementation skapar vi en ny array `reversed` med samma längd som den ursprungliga arrayen `words`. Sedan använder vi en loop för att gå igenom `words` baklänges och fylla `reversed` med elementen i omvänd ordning.

## Facit

<details><summary>Klicka här för att se facit</summary>

```java
public static String[] reverseArray(String[] words) {
    String[] reversed = new String[words.length];
    int index = 0;
    for (int i = words.length - 1; i >= 0; i--) {
        reversed[index] = words[i];
        index++;
    }
    return reversed;
}
```

Detta är en grundläggande implementation av `reverseArray`. Men det finns också andra sätt att lösa uppgiften. Till exempel kan du använda metoden `reverse()` i klassen `Collections` för att vända på ordningen av elementen i arrayen.

```java
import java.util.Arrays;
import java.util.Collections;
import java.util.List;

public static String[] reverseArray(String[] words) {
    List<String> list = Arrays.asList(words);
    Collections.reverse(list);
    return list.toArray(new String[list.size()]);
}
```

Det finns också en smidigare lösning med hjälp av Java's Stream API, som ger kortare och mer läsbar kod:

```java
import java.util.Arrays;

public static String[] reverseArray(String[] words) {
    return Arrays.stream(words)
        .reversed()
        .toArray(String[]::new);
}
```

Oavsett vilken lösning du väljer, är det viktigt att förstå algoritmens logik och syfte. Att invertera en array är en grundläggande uppgift som kan vara användbar i olika programmeringskontexter.
