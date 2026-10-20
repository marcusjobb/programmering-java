---
title: Stringbuilder
grand_parent: Variabler
author: Marcus Ackre Medina
parent: Stränghantering
nav_order: 50
---
# Stringbuilder

## Introduktion

Nu ska vi titta på StringBuilder! Här kommer vi att utforska en kraftfull verktygslåda som låter dig bygga och manipulera textsträngar på ett enkelt och effektivt sätt. Glöm tråkiga och ineffektiva metoder, för med StringBuilder kommer du att känna dig som en äkta trollkarl i textbehandlingsvärlden! Så låt oss dyka in och upptäcka de charmiga förmågorna hos StringBuilder!

## Vad är StringBuilder?

StringBuilder är en av de coolaste klasserna i Java som låter dig bygga, ändra och sammanslå textsträngar med lätthet. Istället för att skapa nya strängar varje gång du ändrar texten, som andra metoder gör, låter StringBuilder dig manipulera texten direkt i samma objekt. Detta sparar inte bara minne utan förbättrar också prestandan i din kod!

## Fördelar med StringBuilder

1. **Effektivt Minneanvändning:** När du ändrar textsträngar med andra metoder skapas nya objekt för varje ändring. Detta kan slösa bort minne och orsaka onödigt skräp i ditt program. Med StringBuilder undviker du dessa problem genom att ändra texten direkt i samma objekt, vilket minimerar minnesförbrukningen.

2. **Snabbare Prestanda:** Eftersom StringBuilder tillåter direkt manipulation av text, är det mycket snabbare än andra metoder som skapar nya strängobjekt vid varje ändring. Om du behöver bygga eller ändra stora textsträngar, kommer StringBuilder att imponera dig med sin blixtsnabba prestanda!

3. **Enkel Att Använda:** StringBuilder kommer med enkla metoder för att lägga till, ta bort, byta ut och manipulera texten. Detta gör det till en användarvänlig klass för alla dina textbehandlingsbehov.

4. **Trådsäkerhet (till viss del):** Om du har flera trådar som hanterar samma StringBuilder-objekt, behöver du inte oroa dig för konflikter. StringBuilder är inte helt trådsäker, men om du använder det i enkeltrådade applikationer, kommer det inte att ge några problem.

kortfattat: Använd alltid StringBuilder när du ska bygga eller manipulera textsträngar. Det är snabbt, effektivt och enkelt att använda!

```java

// Gör en timer som räknar antal sekunder en loop tar att köra

String testString ="";
StringhBuilder stringBuilderTest = new StringBuilder();
int loopCount = 100000;

long startTime = System.currentTimeMillis();
for (int i = 0; i < loopCount; i++) {
    testString += "test";
}
long endTime = System.currentTimeMillis();

System.out.println("Time taken for String: " + (endTime - startTime) + " milli seconds");

startTime = System.currentTimeMillis();
for (int i = 0; i < loopCount; i++) {
    stringBuilderTest.append("test");
}
endTime = System.currentTimeMillis();

System.out.println("Time taken for StringBuilder: " + (endTime - startTime) + " milli seconds");

```

Det ger oss

```text
Time taken for String: 10 milli seconds
Time taken for StringBuilder: 0 milli seconds
```

Nu kanske du förstår varför vi använder StringBuilder istället för String när vi ska bygga textsträngar.

## Exempel - Bygg en Magisk Trollformel

Låt oss använda StringBuilder för att bygga en magisk trollformel:

```java
StringBuilder formula = new StringBuilder("Hocus Pocus! ");
formula.append("Abracadabra! ")
    .append("Simsalabim!");

System.out.println(formula.toString());
```

Resultat:

```
Hocus Pocus! Abracadabra! Simsalabim!
```

```Java
StringBuilder bond=
    new StringBuilder("My name is ")
    .append("Bond, ")
    .append("James Bond")
    .appendLine("Give me a Martini, ")
    .append("shaken, not stirred.");
```

Resultat:

```text
My name is Bond, James Bond
Give me a Martini, shaken, not stirred.
```

## Funktioner

| Funktion   | Beskrivning                                               | Exempel                            | Resultat                 |
| -----------| -------------------------------------------------------- | ---------------------------------- | ------------------------ |
| append()   | Lägger till en sträng i slutet av StringBuilder-objektet | `StringBuilder sb = new StringBuilder();`<br>`sb.append("Hello");` | `Hello`                  |
| insert()   | Infogar en sträng vid en given position i StringBuilder-objektet | `StringBuilder sb = new StringBuilder("Hello");`<br>`sb.insert(5, " world");` | `Hello world`            |
| delete()   | Tar bort tecken från StringBuilder-objektet mellan angivna index | `StringBuilder sb = new StringBuilder("Hello world");`<br>`sb.delete(5, 10);` | `Hello`                  |
| reverse()  | Omvänder ordningen på tecken i StringBuilder-objektet    | `StringBuilder sb = new StringBuilder("Hello");`<br>`sb.reverse();` | `olleH`                  |
| replace()  | Ersätter en sekvens av tecken med en annan i StringBuilder-objektet | `StringBuilder sb = new StringBuilder("Hello");`<br>`sb.replace(1, 3, "ey");` | `Heylo`                |
| capacity() | Returnerar den nuvarande kapaciteten (storleken) av StringBuilder-objektet | `StringBuilder sb = new StringBuilder("Hello");`<br>`int capacity = sb.capacity();` | `21`                     |
| length()   | Returnerar den nuvarande längden (antal tecken) av StringBuilder-objektet | `StringBuilder sb = new StringBuilder("Hello");`<br>`int length = sb.length();` | `5`                       |
| setLength()| Ställer in längden (antal tecken) på StringBuilder-objektet | `StringBuilder sb = new StringBuilder("Hello");`<br>`sb.setLength(10);` | `Hello     ` (med 5 extra utrymme fyllda med nolltecken) |
| indexOf()  | Returnerar den första förekomsten av en sträng eller ett tecken i StringBuilder-objektet | `StringBuilder sb = new StringBuilder("Hello");`<br>`int index = sb.indexOf("l");` | `2`                       |
| substring()| Returnerar en delsträng av StringBuilder-objektet baserat på angivna index | `StringBuilder sb = new StringBuilder("Hello");`<br>`String subStr = sb.substring(1, 4);` | `ell`                    |
| toString() | Konverterar StringBuilder-objektet till en vanlig sträng | `StringBuilder sb = new StringBuilder("Hello");`<br>`String str = sb.toString();` | `Hello`                  |

## Sammanfattning

Med StringBuilder i din verktygslåda har du makten att skapa magiska textsträngar på ett effektivt och enkelt sätt. Dess förmåga att spara minne och förbättra prestanda gör det till ett oumbärligt val för alla dina textbehandlingsbehov. Så om du vill trolla med text och skapa imponerande textsträngar, är det dags att omfamna StringBuilder och låta dina textbehandlingsskills lysa som aldrig förr!

## Obligatorisk text-smiley:

Låt oss bygga en värld av häftiga textsträngar tillsammans! ;)
