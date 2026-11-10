---
title: "Lathund: Variabler"
author: Marcus Ackre Medina
description: "Snabbreferens för hur du deklarerar, initierar och använder variabler i Java."
parent: Lathund
nav_order: 21
---
# Lathund: Variabler

En variabel är ett namngivet utrymme för ett värde. Du använder den när du vill spara ett värde och kunna läsa eller ändra det senare i koden.

Läs mer: [Variabler](../variables/index.md).

## Deklaration och initialisering

| Syntax | Beskrivning |
|--------|-------------|
| `int x;` | Deklarerar en `int` utan värde. Variabeln måste få ett värde innan den används. |
| `int x = 10;` | Deklarerar och initierar en `int` i samma rad. |
| `var y = 20;` | Deklarerar en lokal variabel. Java räknar ut typen (`int`) från värdet. |

```java
int antalGäster;        // deklaration, inget värde ännu
antalGäster = 12;       // tilldelning
int ålder = 30;         // deklaration och initiering i samma rad
var poäng = 87;         // Java ser att värdet är en int
```

## Modifierare

| Modifierare | Beskrivning | Exempel |
|-------------|-------------|---------|
| `final` | Gör variabeln konstant. Värdet kan bara tilldelas en gång. | `final int maxVärde = 100;` |
| `static` | Gör variabeln till en klassvariabel som delas av alla objekt i klassen. Används på fält, inte på lokala variabler. | `static int antal;` |

## Operationer

| Syntax | Beskrivning | Exempel |
|--------|-------------|---------|
| `x = y + z;` | Tilldelar summan av `y` och `z` till `x` | `total = pris + moms;` |
| `x *= y;` | Multiplicerar `x` med `y` och sparar resultatet i `x` | `x *= 2;` |
| `x++;` | Ökar värdet med 1 | `ålder++;` |
| `x -= 5;` | Minskar värdet med 5 | `poäng -= 5;` |

## Jämförelser

| Syntax | Beskrivning | Exempel |
|--------|-------------|---------|
| `if (x > y)` | Sant om `x` är större än `y` | `if (ålder > 18)` |
| `if (x == y)` | Sant om `x` är lika med `y`. Används för tal och andra primitiva typer. | `if (svar == rättSvar)` |
| `if (x != y)` | Sant om `x` inte är lika med `y` | `if (antal != 0)` |
| `if (!x.equals(y))` | Sant om strängen `x` inte har samma innehåll som `y` | `if (!lösenord.equals("hemligt"))` |

## Vanliga misstag

- Att använda en lokal variabel innan den fått ett värde. Kompilatorn säger *variable might not have been initialized*.
- `var` kräver ett startvärde. `var x;` ger ett kompileringsfel.
- `static` på en lokal variabel ger ett kompileringsfel. `static` hör till klassen, inte till en metod.
- `==` på `String` jämför om det är samma objekt, inte om texten är lika. Använd `equals()`.
- Java skiljer på stora och små bokstäver. `ålder` och `Ålder` är två olika variabler.

## Terminologi

| Term | Betydelse |
|------|-----------|
| Variabel | Ett namngivet utrymme i minnet som håller ett värde |
| Deklaration | Att tala om vilken typ och vilket namn variabeln har |
| Initiering | Att ge variabeln ett första värde |
| Tilldelning | Att sätta ett värde på en variabel med `=` |
| Datatyp | Typen som avgör vilka värden variabeln kan hålla |
| Konstant | En variabel med `final` som inte kan ändras efter tilldelningen |
| Klassvariabel | En variabel med `static` som tillhör klassen, inte ett enskilt objekt |
