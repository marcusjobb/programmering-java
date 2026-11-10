---
title: "Lathund: switch"
author: Marcus Ackre Medina
description: "switch i Java: switch-sats med break, switch-sats med pilar och switch-uttryck (Java 14+), samt skillnaden mot if."
parent: Lathund
nav_order: 32
---
# Lathund: switch

`switch` väljer ett block utifrån värdet på ett uttryck. Det passar när du jämför samma värde mot flera fasta alternativ. Från Java 14 finns även `switch`-uttryck, som ger tillbaka ett värde.

Läs mer: [If](../conditionals/index.md).

## Snabbfakta

| Egenskap | Värde |
|---|---|
| Uttryck | `int`, `char`, `byte`, `short`, `String` eller `enum` |
| Etikett | `case värde:` (klassisk form) eller `case värde ->` (pilform) |
| Standard | `default` körs när inget `case` matchar |
| Avslut | `break` i klassisk form, annars slutar blocket av sig självt |

## Operationer

Det finns tre former som gör ungefär samma sak. Välj den som passar.

<details>
<summary>Klassisk switch-sats med break</summary>

```java
int nummer = 2;
switch (nummer) {
    case 1:
        System.out.println("Ett");
        break;
    case 2:
        System.out.println("Två");
        break;
    case 3:
        System.out.println("Tre");
        break;
    default:
        System.out.println("Inget matchade");
}
```

Utskrift: `Två`. `break` avslutar hela `switch`-satsen. Utan `break` fortsätter koden in i nästa `case`, vilket kallas fall-through.

</details>

<details>
<summary>Switch-sats med pilar (Java 14+)</summary>

```java
int nummer = 2;
switch (nummer) {
    case 1 -> System.out.println("Ett");
    case 2 -> System.out.println("Två");
    case 3 -> System.out.println("Tre");
    default -> System.out.println("Inget matchade");
}
```

Utskrift: `Två`. Med pilar körs bara det valda blocket och `break` behövs inte.

</details>

<details>
<summary>Switch-uttryck (Java 14+)</summary>

```java
String dag = "Måndag";
String typ = switch (dag) {
    case "Måndag", "Tisdag", "Onsdag", "Torsdag", "Fredag" -> "Arbetsdag";
    case "Lördag", "Söndag" -> "Helgdag";
    default -> "Ogiltig dag";
};
System.out.println(typ);
```

Utskrift: `Arbetsdag`. Ett switch-uttryck ger ett värde som kan sparas i en variabel. Har blocket flera rader används `yield` för att ange värdet:

```java
String typ = switch (dag) {
    case "Lördag", "Söndag" -> {
        System.out.println("Helg!");
        yield "Helgdag";
    }
    default -> "Arbetsdag";
};
```

</details>

## Jämförelser

| | `switch` | `if` och `else if` |
|---|---|---|
| Passar när | Ett värde mot fasta alternativ | Villkor av olika slag, till exempel intervall |
| Villkor | Likhet med ett värde | Vilket booleskt uttryck som helst |
| Läsbarhet med många fall | Hög | Lägre |

```java
// Intervall går inte i switch, använd if
int poäng = 85;
if (poäng >= 90) {
    System.out.println("Utmärkt!");
} else if (poäng >= 80) {
    System.out.println("Mycket bra!");
}
```

## Vanliga misstag

- Glömma `break` i klassisk form. Då körs även nästa `case`.
- Tro att `break` bara avslutar ett `case`. Den avslutar hela `switch`-satsen.
- Använda `case poäng >= 90:`. Etiketter måste vara konstanter, så intervall skrivs med `if`.
- Glömma `default` i ett switch-uttryck. Kompilatorn kräver att alla möjliga värden täcks.

## Terminologi

| Term | Betydelse |
|---|---|
| `switch` | Kontrollstruktur som väljer ett block utifrån ett värde |
| `case` | Etikett som matchas mot uttryckets värde |
| `break` | Avslutar `switch`-satsen |
| `default` | Block som körs när inget `case` matchar |
| `yield` | Ger tillbaka värdet från ett block i ett switch-uttryck |
| fall-through | Att koden fortsätter in i nästa `case` när `break` saknas |
