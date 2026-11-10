---
title: "Lathund: String"
author: Marcus Ackre Medina
description: "Snabbreferens för String i Java: längd, sökning, delsträngar, ersättning, delning och jämförelse av innehåll."
parent: Lathund
nav_order: 25
---
# Lathund: String

`String` är Javas typ för text. Strängar är oföränderliga: metoderna ändrar inte originalet utan returnerar en ny sträng. Index börjar på 0.

Läs mer: [Variabler](../variables/index.md).

## Grundläggande operationer

| Metod | Beskrivning | Exempel | Resultat |
|-------|-------------|---------|----------|
| `length()` | Antal tecken i strängen | `"Java är roligt".length()` | `14` |
| `trim()` | Tar bort mellanslag i början och slutet | `"   Text   ".trim()` | `"Text"` |
| `toUpperCase()` | Konverterar till versaler | `"hej".toUpperCase()` | `"HEJ"` |
| `toLowerCase()` | Konverterar till gemener | `"HELLO".toLowerCase()` | `"hello"` |
| `isEmpty()` | Sant om längden är 0. Kastar `NullPointerException` om strängen är `null`. | `"".isEmpty()` | `true` |
| `isBlank()` | Sant om strängen är tom eller bara innehåller blanksteg (Java 11+) | `"   ".isBlank()` | `true` |

<details>
<summary>Sammanfoga strängar: två sätt</summary>

```java
String hälsning = "Hej" + " " + "världen!";     // "Hej världen!"
String hälsning2 = "Hej".concat(" världen!");     // "Hej världen!"
```

`+` är det vanligaste sättet. `concat` tar bara ett argument, så för fler delar behöver du flera anrop.

</details>

## Sökning och utskärning

| Metod | Beskrivning | Exempel | Resultat |
|-------|-------------|---------|----------|
| `contains()` | Sant om strängen innehåller delsträngen. Skiftlägeskänsligt. | `"Java är roligt".contains("roligt")` | `true` |
| `contains()` | Samma metod, men med stor bokstav i sökordet | `"Java är roligt".contains("Roligt")` | `false` |
| `indexOf()` | Index för första förekomsten, eller `-1` om den saknas | `"Java är roligt".indexOf("är")` | `5` |
| `substring(start, slut)` | Del av strängen. Slutindex är exklusivt. | `"Java är roligt".substring(5, 7)` | `"är"` |
| `substring(start)` | Från start till slutet av strängen | `"Java är roligt".substring(8)` | `"roligt"` |

Alla dessa metoder är skiftlägeskänsliga. Vill du söka oavsett skiftläge, gör först båda till gemener:

```java
String text = "Java är roligt";
boolean finns = text.toLowerCase().contains("roligt");   // true
```

## Ersättning och delning

| Metod | Beskrivning | Exempel | Resultat |
|-------|-------------|---------|----------|
| `replace()` | Ersätter alla förekomster av en delsträng. Returnerar en ny sträng. | `"Hej Emma".replace("Emma", "vän")` | `"Hej vän"` |
| `split()` | Delar strängen vid ett mönster. Returnerar en `String[]`. | `"äpple,banan,päron".split(",")` | `["äpple", "banan", "päron"]` |

Om texten har mellanslag efter kommatecknen följer de med till delarna:

```java
String[] frukter = "äpple, banan, päron".split(",");
// ["äpple", " banan", " päron"]

String[] rena = "äpple, banan, päron".split(",\\s*");
// ["äpple", "banan", "päron"]
```

`split` tar ett reguljärt uttryck. `\\s*` betyder "noll eller fler blanksteg" (`\\` blir `\` i mönstret).

## Jämförelser

`==` jämför om två variabler pekar på samma objekt. `equals()` jämför innehållet.

```java
String a = "hej";
String b = "hej";
String c = new String("hej");

System.out.println(a == b);        // true, samma objekt i strängpoolen
System.out.println(a == c);        // false, olika objekt
System.out.println(a.equals(c));   // true, samma innehåll
```

## Vanliga misstag

- **`==` på text:** använd `equals()`. `==` fungerar bara av en slump för literaler.
- **`null`:** `text.length()` på en variabel som är `null` ger `NullPointerException`. Kontrollera först: `if (text != null && !text.isEmpty())`.
- **Oföränderlighet:** `namn.toUpperCase();` ändrar inte `namn`. Skriv `namn = namn.toUpperCase();`.
- **Utanför index:** `substring(9, 15)` på en sträng med 14 tecken kastar `StringIndexOutOfBoundsException`.
- **Mellanslag i `split`:** `split(",")` tar inte bort mellanslag. Använd `split(",\\s*")` eller `trim()` på varje del.

## Terminologi

| Term | Betydelse |
|------|-----------|
| Sträng | Text, lagrad som ett `String`-objekt |
| Oföränderlig (immutable) | Ett objekt vars innehåll inte kan ändras efter att det skapats |
| Delsträng | En del av en sträng |
| Index | Positionen för ett tecken, där den första positionen är 0 |
| Skiftlägeskänslig | Att `A` och `a` räknas som olika tecken |
| Null | Ett värde som betyder att en referens inte pekar på något objekt |
| Reguljärt uttryck | Ett mönster för att matcha text, till exempel `\\s*` i `split` |
