---
title: "Lathund: boolean"
author: Marcus Ackre Medina
description: "Snabbreferens för typen boolean i Java: sant och falskt, jämförelser, logiska operatorer och vanliga fallgropar."
parent: Lathund
nav_order: 24
---
# Lathund: boolean

`boolean` har bara två värden, `true` och `false`. Den används i villkor som `if` och `while` och för allt som är ja eller nej i koden.

Läs mer: [Variabler](../variables/index.md).

## Deklaration och jämförelser

```java
boolean ärSant = true;
boolean ärFalskt = false;

int x = 10;
int y = 11;

boolean ärLika = x == y;      // false
boolean ärMindre = x < y;     // true
boolean ärStörre = (5 > 2);   // true
```

## Jämförelse med boolean

| Operation | Beskrivning | Exempel | Resultat |
|-----------|-------------|---------|----------|
| `==` | Sant om båda värdena är lika | `true == true` | `true` |
| `!=` | Sant om värdena är olika | `true != false` | `true` |

## Logiska operatorer

| Operator | Beskrivning | Exempel | Resultat |
|----------|-------------|---------|----------|
| `&&` | Logiskt OCH. Båda måste vara `true`. | `true && false` | `false` |
| `\|\|` | Logiskt ELLER. Minst en måste vara `true`. | `true \|\| false` | `true` |
| `!` | Logiskt INTE. Vänder värdet. | `!true` | `false` |

`&&` och `||` är *kortslutna*. Om resultatet redan är klart hoppar Java över resten av uttrycket.

## Bitvisa operatorer

Bitvisa operatorer arbetar på heltal. `&`, `|` och `^` fungerar också på `boolean`, men utan kortslutning. `~` fungerar inte på `boolean`.

| Operator | Beskrivning | Exempel | Resultat |
|----------|-------------|---------|----------|
| `&` | Bitvis OCH | `5 & 3` | `1` |
| `\|` | Bitvis ELLER | `5 \| 3` | `7` |
| `^` | Bitvis XOR (exklusivt ELLER) | `5 ^ 3` | `6` |
| `~` | Bitvis komplement (INTE) | `~5` | `-6` |

## Vanliga misstag

- **Tilldelning i stället för jämförelse:** `if (ärSant = false)` kompilerar, men sätter `ärSant` till `false` och går aldrig in i `if`-blocket. Jämför med `==`.
- **Onödig jämförelse:** `if (ärSant == true)` fungerar, men `if (ärSant)` är enklare.
- **`&` i stället för `&&`:** `&` utvärderar båda sidor, även när den första är `false`. Använd `&&` i villkor, om du inte har ett särskilt skäl.
- **Sidoeffekter i det andra ledet:** med `&&` och `||` körs det andra ledet bara om det behövs. Om en metod där ändrar något, sker ändringen inte alltid.

## Terminologi

| Term | Betydelse |
|------|-----------|
| Boolean | Datatyp med värdena `true` och `false` |
| Logisk operator | Operator som kombinerar eller vänder `boolean`-värden, till exempel `&&`, `||` och `!` |
| Kortslutning | Att Java hoppar över resten av ett logiskt uttryck när resultatet redan är klart |
| Villkor | Ett uttryck som ger `true` eller `false`, till exempel i en `if`-sats |
| Bitvis operator | Operator som arbetar på enskilda bitar i ett heltal |
| Inversion | Att vända ett värde, till exempel från `true` till `false` med `!` |
