---
title: "Lathund: Decimaltal"
author: Marcus Ackre Medina
description: "Snabbreferens för decimaltal i Java: double, float och BigDecimal, omvandling, avrundning och vanliga fallgropar."
parent: Lathund
nav_order: 23
---
# Lathund: Decimaltal

Java har två inbyggda flyttalstyper, `double` och `float`. För exakta belopp, till exempel pengar, används `BigDecimal`. Java har ingen egen `decimal`-typ.

Läs mer: [Variabler](../variables/index.md).

## Datatyper

| Datatyp | Beskrivning | Exempel |
|---------|-------------|---------|
| `double` | 64-bitars flyttal. Standardvalet för decimaltal. | `double pi = 3.14159265359;` |
| `float` | 32-bitars flyttal med mindre precision. Värdet måste ha suffixet `F`. | `float pris = 19.99F;` |
| `BigDecimal` | Decimaltal med exakt precision. Används för pengar. | `BigDecimal saldo = new BigDecimal("1000.50");` |

## Omvandling

| Metod | Beskrivning | Exempel | Resultat |
|-------|-------------|---------|----------|
| `Double.valueOf` | Omvandlar till ett `Double`-objekt. Ett heltal blir automatiskt ett decimaltal. | `Double.valueOf(42)` | `42.0` |
| `Float.valueOf` | Omvandlar till ett `Float`-objekt. Argumentet måste vara ett `float`, alltså med `F`. | `Float.valueOf(19.99F)` | `19.99` |
| `new BigDecimal(String)` | Skapar ett `BigDecimal` från en sträng. Använd strängen, inte `double`. | `new BigDecimal("1000.50")` | `1000.50` |
| `Integer.valueOf` | Omvandlar till ett `Integer`-objekt | `Integer.valueOf(42)` | `42` |
| `Long.valueOf` | Omvandlar till ett `Long`-objekt. Värdet måste ha suffixet `L`. | `Long.valueOf(1234567890123L)` | `1234567890123` |

## Avrundning

| Metod | Beskrivning | Exempel | Resultat |
|-------|-------------|---------|----------|
| `Math.round` | Avrundar till närmaste heltal. Returnerar `long` för ett `double`. | `Math.round(3.5)` | `4` |
| `Math.floor` | Avrundar nedåt. Returnerar ett `double`. | `Math.floor(3.99)` | `3.0` |
| `Math.ceil` | Avrundar uppåt. Returnerar ett `double`. | `Math.ceil(3.01)` | `4.0` |

`Math.round` tar bara ett argument. För två decimaler multiplicerar du först med 100 och delar sedan:

```java
double värde = 3.14159;
double avrundat = Math.round(värde * 100) / 100.0;   // 3.14
```

För pengar är `BigDecimal` ett bättre val. Ange antal decimaler och avrundningsregel med `setScale`:

```java
BigDecimal saldo = new BigDecimal("10.005");
BigDecimal visat = saldo.setScale(2, RoundingMode.HALF_UP);   // 10.01
```

## Vanliga misstag

- **Glömt suffix:** `float pris = 19.99;` ger ett kompileringsfel, eftersom decimaltal i Java är `double` som standard. Skriv `19.99F`.
- **Binär approximation:** `0.1 + 0.2` ger `0.30000000000000004`. `double` lagrar talen i binärt format, så många decimaltal blir ungefärliga. Använd `BigDecimal` för exakta belopp.
- **`BigDecimal` från `double`:** `new BigDecimal(0.1)` ger den binära approximationen. Skriv `new BigDecimal("0.1")` i stället.
- **Decimalkomma:** i Java skrivs decimaltal med punkt: `3.14`, inte `3,14`.
- **Trunkering:** `(int) 3.7` ger `3`, inte `4`. Java kapar decimaldelen. För avrundning, använd `Math.round`.
- **Typen från `Math.round`:** `int x = Math.round(2.5);` ger ett fel, eftersom resultatet är `long`. Skriv `(int) Math.round(2.5)` om du vet att det får plats.

## Terminologi

| Term | Betydelse |
|------|-----------|
| Flyttal | Ett tal med decimalpunkt, lagrat i en approximerad form |
| Precision | Hur många siffror som går att lagra exakt |
| Binär approximation | Ett decimaltal som inte kan lagras exakt i binärt format |
| Avrundning | Att justera ett tal till närmaste värde med ett givet antal decimaler |
| Trunkering | Att kapa decimaldelen utan att avrunda |
| Suffix | Bokstav efter ett tal som anger typen, till exempel `F` för `float` och `L` för `long` |
