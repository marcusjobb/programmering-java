---
title: "Lathund: Datatyper"
author: Marcus Ackre Medina
description: "Översikt över Javas datatyper: primitiva typer, referenstyper, omfång och exempel på deklaration."
parent: Lathund
nav_order: 26
---
# Lathund: Datatyper

Java är statiskt typat. Varje variabel har en typ som bestäms när den deklareras, och typen avgör vilka värden variabeln kan hålla. Javas typer delas in i primitiva typer, som lagrar värdet direkt, och referenstyper, som pekar på ett objekt.

Läs mer: [Variabler](../variables/index.md).

## Primitiva typer

| Datatyp | Omfång | Exempel |
|---------|--------|---------|
| `byte` | `-128` till `127` | `byte liten = 100;` |
| `short` | `-32 768` till `32 767` | `short år = 2026;` |
| `int` | `-2 147 483 648` till `2 147 483 647` | `int ålder = 30;` |
| `long` | `-9 223 372 036 854 775 808` till `9 223 372 036 854 775 807` | `long stort = 8_000_000_000L;` |
| `float` | Ungefär `±1,4 × 10^-45` till `±3,4 × 10^38` | `float pris = 19.99F;` |
| `double` | Ungefär `±4,9 × 10^-324` till `±1,7 × 10^308` | `double pi = 3.14159;` |
| `char` | Ett UTF-16-tecken, `'\u0000'` till `'￿'` | `char bokstav = 'A';` |
| `boolean` | `true` eller `false` | `boolean ärSant = true;` |

## Referenstyper

| Datatyp | Beskrivning | Exempel |
|---------|-------------|---------|
| `String` | Text. Längden begränsas bara av minnet. | `String namn = "Emma";` |
| `Integer` | Ett `int` som objekt. Kan vara `null`. | `Integer valfrittTal = null;` |
| `int[]` | En array med heltal | `int[] nummer = {1, 2, 3};` |
| `List<Integer>` | En lista med heltal | `List<Integer> nummerLista = new ArrayList<>(List.of(1, 2, 3));` |
| `Map<String, Integer>` | Nyckel-värde-par | `Map<String, Integer> städer = new HashMap<>();` |

Så fyller du en `Map`. Koden kräver `import java.util.*;`.

```java
Map<String, Integer> städer = new HashMap<>();
städer.put("Stockholm", 975_904);    // understreck gör stora tal lättare att läsa
städer.put("Göteborg", 583_056);
```

<details>
<summary>Oföränderlig lista med List.of</summary>

`List.of` skapar en lista som inte går att ändra. Det är ofta det säkraste valet när du bara vill läsa värdena.

```java
List<Integer> siffror = List.of(1, 2, 3);
siffror.add(4);   // kastar UnsupportedOperationException
```

Använd `new ArrayList<>(List.of(...))` när du behöver lägga till eller ta bort värden.

</details>

## Vanliga misstag

- **Decimalkomma:** i kod skrivs decimaltal med punkt: `3.14`, inte `3,14`.
- **Suffix:** `float` kräver `F` (`19.99F`). `long` kräver `L` när värdet inte får plats i `int`: `long x = 8000000000L;`.
- **`int` och `null`:** en `int` kan inte vara `null`. Använd `Integer` om värdet ibland saknas.
- **`char` och `String`:** `'A'` är en `char` med ett tecken. `"A"` är en `String`. De är inte utbytbara.
- **Typen på en lista:** `List<int>` fungerar inte. Använd den inslagna typen `List<Integer>`.

## Terminologi

| Term | Betydelse |
|------|-----------|
| Statiskt typat | Typen bestäms vid kompileringen, och Java kontrollerar att värdena passar |
| Primitiv typ | En inbyggd typ som lagrar värdet direkt i variabeln |
| Referenstyp | En typ där variabeln pekar på ett objekt i minnet |
| Omfång | Det största och minsta värde som typen kan hålla |
| Inslagen typ (wrapper) | Ett objekt som omsluter en primitiv typ, till exempel `Integer` för `int` |
| Array | En fast lång samling värden av samma typ |
| Suffix | Bokstav efter ett tal som anger typen, till exempel `F` för `float` och `L` för `long` |
