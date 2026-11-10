---
title: "Lathund: while"
author: Marcus Ackre Medina
description: "while-loopen i Java: syntax, break och continue, nästlade loopar, oändliga loopar och vanliga misstag."
parent: Lathund
nav_order: 51
---
# Lathund: while

En `while`-loop upprepar ett kodblock så länge villkoret är sant. Villkoret kontrolleras före varje varv, så blocket kan köras noll gånger. Använd den när du inte vet på förhand hur många varv som behövs.

Läs mer: [Loopar](../loops/index.md).

## Snabbfakta

| Egenskap | Värde |
|---|---|
| Syntax | `while (villkor) { ... }` |
| Villkor kontrolleras | Före varje varv |
| Minsta antal varv | 0 |
| Passar när | Antal varv är okänt, till exempel tills användaren skriver rätt svar |

```java
while (villkor) {
    // körs så länge villkoret är sant
}
```

## Operationer

| Operation | Betydelse | Exempel |
|---|---|---|
| `break` | Avslutar loopen direkt | `if (i == 5) { break; }` |
| `continue` | Hoppar till nästa varv. Villkoret kontrolleras igen | `if (i == 3) { continue; }` |
| `while (true)` | Loopen körs tills något `break` stoppar den | `while (true) { ... }` |

### Vanlig loop

```java
int i = 0;
while (i < 5) {
    System.out.println("Iteration " + i);
    i++;
}
```

Utskrift: `Iteration 0` till `Iteration 4`.

### Nästlad loop

```java
int i = 1;
while (i <= 3) {
    int j = 1;
    while (j <= 3) {
        System.out.print(i * j + " ");
        j++;
    }
    System.out.println();
    i++;
}
```

Utskrift: en multiplikationstabell med tre rader. Den inre loopen körs klart för varje varv i den yttre.

### Break

```java
int i = 0;
while (i < 10) {
    System.out.println(i);
    if (i == 5) {
        break;
    }
    i++;
}
```

Utskrift: `0` till `5`. Loopen bryts när `i` är 5, efter att värdet skrivits ut.

### Continue

```java
int i = 0;
while (i < 5) {
    i++;
    if (i == 3) {
        continue;
    }
    System.out.println(i);
}
```

Utskrift: `1`, `2`, `4`, `5`. Värdet 3 hoppas över eftersom `continue` går direkt till villkoret.

### Oändlig loop med break

```java
int i = 0;
while (true) {
    if (i == 3) {
        break;
    }
    System.out.println(i);
    i++;
}
```

Utskrift: `0`, `1`, `2`. Med `while (true)` finns ingen villkorsregel som stoppar loopen. Det är `break` som gör det.

## Jämförelser

| | `while` | `for` |
|---|---|---|
| Antal varv | Okänt på förhand | Känt på förhand |
| Startvärde, villkor och steg | Skrivs på olika ställen | Skrivs på samma rad |

## Vanliga misstag

- Glömma att ändra variabeln i loopen. Då blir loopen oändlig.
- Skriva `;` direkt efter villkoret, till exempel `while (i < 5);`. Då är kodblocket tomt, och loopen fastnar om villkoret aldrig blir falskt.
- Placera `i++` efter `continue`. Då hoppas ökningen över och loopen fastnar.

## Terminologi

| Term | Betydelse |
|---|---|
| `while` | Nyckelord som inleder en loop med villkor före varje varv |
| villkor | Uttryck som ger `true` eller `false` |
| varv (iteration) | Ett enskilt svep genom loopens kodblock |
| `break` | Avslutar loopen |
| `continue` | Hoppar till nästa varv |
| oändlig loop | Loop vars villkor aldrig blir falskt |
