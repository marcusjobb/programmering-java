---
title: "Lathund: do-while"
author: Marcus Ackre Medina
description: "do-while-loopen i Java: syntax, skillnaden mot while, break och continue samt vanliga misstag."
parent: Lathund
nav_order: 52
---
# Lathund: do-while

En `do-while`-loop kör kodblocket först och kontrollerar villkoret efter varje varv. Blocket körs därför alltid minst en gång. Använd den när något ska göras minst en gång, till exempel att fråga efter en inmatning tills den är giltig.

Läs mer: [Loopar](../loops/index.md).

## Snabbfakta

| Egenskap | Värde |
|---|---|
| Syntax | `do { ... } while (villkor);` |
| Villkor kontrolleras | Efter varje varv |
| Minsta antal varv | 1 |
| Semikolon | Obligatoriskt efter `while (villkor)` |

```java
do {
    // körs minst en gång, sedan så länge villkoret är sant
} while (villkor);
```

## Operationer

| Operation | Betydelse | Exempel |
|---|---|---|
| `break` | Avslutar loopen direkt | `if (i == 3) { break; }` |
| `continue` | Hoppar till villkoret. Resten av kodblocket hoppas över | `if (i == 3) { i++; continue; }` |

### Vanlig loop

```java
int i = 1;
do {
    System.out.println("Iteration " + i);
    i++;
} while (i <= 5);
```

Utskrift: `Iteration 1` till `Iteration 5`.

### Körs en gång även när villkoret är falskt

```java
int i = 10;
do {
    System.out.println("Blocket körs ändå en gång.");
} while (i < 5);
```

Utskrift: en rad. Villkoret `i < 5` är falskt redan från början, men kodblocket har hunnit köras en gång före kontrollen.

### Break

```java
int i = 1;
do {
    if (i == 3) {
        break;
    }
    System.out.println("Iteration " + i);
    i++;
} while (i <= 5);
```

Utskrift: `Iteration 1` och `Iteration 2`.

### Continue

```java
int i = 1;
do {
    if (i == 3) {
        i++;
        continue;
    }
    System.out.println("Iteration " + i);
    i++;
} while (i <= 5);
```

Utskrift: `Iteration 1`, `Iteration 2`, `Iteration 4`, `Iteration 5`. Notera att `i++` måste stå före `continue`. Annars hoppar `continue` till villkoret med oförändrat `i`, och loopen fastnar.

## Jämförelser

| | `while` | `do-while` |
|---|---|---|
| Villkor kontrolleras | Före varje varv | Efter varje varv |
| Minsta antal varv | 0 | 1 |
| Passar när | Blocket ska kanske inte köras alls | Blocket ska köras minst en gång |

## Vanliga misstag

- Glömma semikolonet efter `while (villkor)`. Det ger ett kompileringsfel.
- Tro att `do-while` bara körs när villkoret är sant från början. Blocket körs alltid minst en gång.
- Placera `i++` efter `continue`. Då fastnar loopen.

## Terminologi

| Term | Betydelse |
|---|---|
| `do` | Nyckelord som inleder blocket |
| `while` | Nyckelord som följer blocket och anger villkoret |
| villkor | Uttryck som ger `true` eller `false`, kontrolleras efter varje varv |
| varv (iteration) | Ett enskilt svep genom kodblocket |
