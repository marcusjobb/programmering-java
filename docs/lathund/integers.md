---
title: "Lathund: Heltal (int)"
author: Marcus Ackre Medina
description: "Snabbreferens för heltalstypen int i Java: omvandling, aritmetik, jämförelser och vanliga fallgropar."
parent: Lathund
nav_order: 22
---
# Lathund: Heltal (int)

`int` är Javas vanligaste heltalstyp. Den används för räknare, ålder, poäng och allt annat som saknar decimaler. Värdena ligger mellan −2 147 483 648 och 2 147 483 647.

Läs mer: [Variabler](../variables/index.md).

## Omvandling

| Metod | Beskrivning | Exempel | Resultat |
|-------|-------------|---------|----------|
| `Integer.parseInt` | Omvandlar en sträng till `int`. Kastar `NumberFormatException` om texten inte är ett heltal. | `Integer.parseInt("42")` | `42` |
| `Integer.valueOf` | Omvandlar en sträng till ett `Integer`-objekt | `Integer.valueOf("42")` | `42` |
| `Integer.toString` | Omvandlar en `int` till en sträng | `Integer.toString(42)` | `"42"` |

<details>
<summary>Skillnaden mellan parseInt och valueOf</summary>

`parseInt` ger en primitiv `int`. `valueOf` ger ett `Integer`-objekt, som kan vara `null`. I de flesta fall spelar det ingen roll, eftersom Java packar upp (unboxar) värdet automatiskt.

```java
int siffra = Integer.parseInt("42");    // primitiv int
Integer tal = Integer.valueOf("42");    // Integer-objekt
int igen = tal;                         // automatisk unboxing
```

</details>

Ogiltig text ger ett undantag. Om texten kommer från användaren, fånga det:

```java
try {
    int antal = Integer.parseInt("abc");   // kastar NumberFormatException
    System.out.println(antal);
} catch (NumberFormatException ex) {
    System.out.println("Det där är inte ett heltal");
}
```

## Aritmetiska operationer

| Operation | Beskrivning | Exempel | Resultat |
|-----------|-------------|---------|----------|
| `+` | Addition | `5 + 2` | `7` |
| `-` | Subtraktion | `5 - 2` | `3` |
| `*` | Multiplikation | `5 * 2` | `10` |
| `/` | Heltalsdivision. Decimaldelen kastas bort. | `5 / 2` | `2` |
| `%` | Modulus, resten vid division | `5 % 2` | `1` |

## Jämförelser

| Operation | Beskrivning | Exempel | Resultat |
|-----------|-------------|---------|----------|
| `==` | Lika med | `5 == 2` | `false` |
| `!=` | Inte lika med | `5 != 2` | `true` |
| `>` | Större än | `5 > 2` | `true` |
| `<` | Mindre än | `5 < 2` | `false` |
| `>=` | Större än eller lika med | `5 >= 2` | `true` |
| `<=` | Mindre än eller lika med | `5 <= 2` | `false` |

Jämförelser ger alltid ett `boolean`-värde, som du kan använda i `if`.

## Vanliga misstag

- **Heltalsdivision:** `5 / 2` ger `2`, inte `2.5`. Låt minst ett av talen vara decimaltal, till exempel `5.0 / 2`.
- **Division med noll:** `int` kastar `ArithmeticException`. Ett `double` ger `Infinity` i stället.
- **Överflöd:** `Integer.MAX_VALUE + 1` blir tyst `-2147483648`. Java varnar inte.
- **Integer-objekt med `==`:** två `Integer`-objekt jämförs som referenser. Använd `equals()`, eller låt Java packa upp värdet till `int`.
- **Ogiltig text:** `Integer.parseInt` kastar undantag. Kontrollera indata eller fånga `NumberFormatException`.

## Terminologi

| Term | Betydelse |
|------|-----------|
| Heltal | Tal utan decimaldel |
| Heltalsdivision | Division där resultatet trunkeras mot noll |
| Modulus | Resten efter en heltalsdivision, skrivs med `%` |
| Överflöd (overflow) | Ett värde som blir större än typens maxvärde och börjar om från minvärdet |
| Omvandling (parsing) | Att läsa ett tal från text |
| Unboxing | Att Java packar upp ett `Integer`-objekt till en `int` |
