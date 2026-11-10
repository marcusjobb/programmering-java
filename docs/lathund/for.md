---
title: "Lathund: for"
author: Marcus Ackre Medina
description: "for-loopen i Java: syntax med initiering, villkor och steg, nästlade loopar, break och continue, samt for-each."
parent: Lathund
nav_order: 53
---
# Lathund: for

En `for`-loop samlar start, villkor och steg på en rad. Den passar när du vet hur många varv som ska köras, till exempel när du räknar från 1 till 5.

Läs mer: [Loopar](../loops/index.md).

## Snabbfakta

| Egenskap | Värde |
|---|---|
| Syntax | `for (initiering; villkor; steg) { ... }` |
| Initiering | Körs en gång, före första varvet |
| Villkor | Kontrolleras före varje varv |
| Steg | Körs efter varje varv |
| Minsta antal varv | 0 |

```java
for (int i = 1; i <= 5; i++) {
    // körs så länge villkoret i <= 5 är sant
}
```

## Operationer

| Operation | Betydelse | Exempel |
|---|---|---|
| `break` | Avslutar loopen direkt | `if (i == 3) { break; }` |
| `continue` | Hoppar till steget (`i++`) och sedan villkoret | `if (i == 3) { continue; }` |
| `for (;;)` | Oändlig loop, saknar villkor | `for (;;) { ... }` |

### Vanlig loop

```java
for (int i = 1; i <= 5; i++) {
    System.out.println("Iteration " + i);
}
```

Utskrift: `Iteration 1` till `Iteration 5`.

### Nästlad loop

```java
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        System.out.println("i: " + i + ", j: " + j);
    }
}
```

Utskrift: nio rader, `i: 1, j: 1` till `i: 3, j: 3`. Den inre loopen körs klart för varje varv i den yttre.

### Break

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        break;
    }
    System.out.println("Iteration " + i);
}
```

Utskrift: `Iteration 1` och `Iteration 2`.

### Continue

```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue;
    }
    System.out.println("Iteration " + i);
}
```

Utskrift: `Iteration 1`, `Iteration 2`, `Iteration 4`, `Iteration 5`. Värdet 3 hoppas över, men `i++` körs ändå.

### Loop som aldrig körs

```java
for (int i = 1; i < 1; i++) {
    System.out.println("Denna rad skrivs aldrig ut.");
}
```

Villkoret `i < 1` är falskt redan från början, så kodblocket hoppas över helt.

### for-each

```java
String[] namn = {"Anna", "Bo", "Cecilia"};
for (String n : namn) {
    System.out.println(n);
}
```

Utskrift: de tre namnen, ett per rad. Med for-each behövs inget index, men du kan inte räkna eller hoppa mellan elementen på samma sätt.

## Jämförelser

| | `for` | `while` |
|---|---|---|
| Antal varv | Känt eller lätt att räkna ut | Okänt på förhand |
| Startvärde, villkor och steg | På samma rad | På olika ställen |
| Passar när | Räkna genom ett intervall eller en samling med index | Körs tills något händer |

## Vanliga misstag

- Skriva `;` direkt efter `for (...)`, till exempel `for (int i = 0; i < 5; i++);`. Då är kodblocket tomt.
- Använda `<=` när du menar `<`, eller tvärtom. `for (int i = 0; i < 5; i++)` ger värdena 0 till 4, inte 5.
- Ändra loopvariabeln i kodblocket utan att tänka på hur det påverkar antalet varv.

## Terminologi

| Term | Betydelse |
|---|---|
| initiering | Startvärdet för loopvariabeln, körs en gång |
| villkor | Uttryck som avgör om nästa varv ska köras |
| steg | Ändring av loopvariabeln efter varje varv |
| loopvariabel | Räknare, ofta `i`, som styr loopen |
| varv (iteration) | Ett enskilt svep genom kodblocket |
| for-each | Loop som går igenom varje element i en samling |
