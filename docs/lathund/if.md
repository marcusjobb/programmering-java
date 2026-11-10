---
title: "Lathund: if"
author: Marcus Ackre Medina
description: "if, else if och else i Java: syntax, jämförelseoperatorer, skillnaden mot flera if i rad och vanliga misstag."
parent: Lathund
nav_order: 31
---
# Lathund: if

`if` kör ett kodblock bara när ett villkor är sant. Med `else if` och `else` väljer programmet mellan flera vägar. Använd det när programmet ska göra olika saker beroende på ett värde.

Läs mer: [If](../conditionals/index.md).

## Snabbfakta

| Egenskap | Värde |
|---|---|
| Villkor | Ett `boolean`-uttryck inom parenteser |
| Kodblock | `{ }`, används alltid även när blocket bara har en rad |
| Ordning | `if` först, sedan valfritt flera `else if`, sist valfritt en `else` |
| Antal block som körs | Högst ett |

```java
if (villkor) {
    // körs om villkoret är sant
} else if (annatVillkor) {
    // körs om det första villkoret är falskt och detta är sant
} else {
    // körs om inget av villkoren är sant
}
```

## Operationer

| Operator | Betydelse | Exempel | Resultat (ålder = 18) |
|---|---|---|---|
| `==` | lika med | `ålder == 18` | `true` |
| `!=` | inte lika med | `ålder != 18` | `false` |
| `<`, `<=`, `>`, `>=` | jämförelse | `ålder >= 18` | `true` |
| `&&` | och, båda måste vara sanna | `ålder >= 18 && ålder < 65` | `true` |
| `\|\|` | eller, minst en måste vara sann | `ålder < 18 \|\| ålder >= 65` | `false` |
| `!` | inte, vänder på värdet | `!(ålder < 18)` | `true` |

### Enkel if

```java
int ålder = 18;
if (ålder >= 18) {
    System.out.println("Du är myndig.");
}
```

Utskrift: `Du är myndig.`

### if-else

```java
int poäng = 85;
if (poäng >= 90) {
    System.out.println("Utmärkt resultat!");
} else {
    System.out.println("Du har inte nått 90 poäng.");
}
```

Utskrift: `Du har inte nått 90 poäng.`

### else if

```java
int poäng = 75;
if (poäng >= 90) {
    System.out.println("Utmärkt!");
} else if (poäng >= 80) {
    System.out.println("Mycket bra!");
} else if (poäng >= 70) {
    System.out.println("Godkänt.");
} else {
    System.out.println("Inte godkänt än.");
}
```

Utskrift: `Godkänt.` Java testar villkoren uppifrån och ned och stannar vid första sanna.

## Jämförelser

| | Flera `if` i rad | `if` med `else if` |
|---|---|---|
| Villkor som kontrolleras | Alla | Till och med det första sanna |
| Antal block som kan köras | Flera | Högst ett |
| Passar när | Flera oberoende kontroller | Ett val mellan alternativ |

## Vanliga misstag

- Skriva `=` i stället för `==` i ett villkor. `=` tilldelar ett värde, `==` jämför.
- Skriva `if (villkor);` med semikolon. Då blir kodblocket under `if` aldrig villkorat.
- Ordna `else if` så att ett generellt villkor kommer först. Då nås de efterföljande villkoren aldrig.
- Jämföra två `String`-värden med `==`. Använd `.equals()`, till exempel `namn.equals("Anna")`.
- Använda flera `if` i rad när bara ett block ska köras. Då kan fler än ett block köras.

## Terminologi

| Term | Betydelse |
|---|---|
| `if` | Kontrollstruktur som kör kod när villkoret är sant |
| villkor | Uttryck som ger `true` eller `false` |
| `else if` | Ytterligare villkor som testas när föregående villkor är falskt |
| `else` | Block som körs när inget tidigare villkor är sant |
| `boolean` | Datatyp med värdena `true` och `false` |
