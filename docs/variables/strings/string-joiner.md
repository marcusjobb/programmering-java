---
title: String joiner
grand_parent: Variabler
author: Marcus Ackre Medina
parent: Stränghantering
nav_order: 60
---
# String joiner

## Introduktion

Välkomna, kära nyfikna kodare, till den spännande världen av StringJoiner! Här kommer vi att utforska detta fantastiska verktyg som låter oss förena flera strängar till ett enda coolt paket. Med StringJoiner i vår verktygslåda kan vi skapa sammanhängande och välstrukturerade textsträngar utan krångel. Så slå dig ner och förbered dig för en rolig resa in i den fängslande världen av StringJoiner! 💻

## Vad är StringJoiner?

StringJoiner är en smidig klass i Java som hjälper oss att sammanfoga flera strängar med en avgränsare mellan dem. Tänk på det som att binda ihop flera pärlor på en tråd för att skapa ett vackert smycke av ord! StringJoiner låter oss skapa dessa vackra textsträngar på ett enkelt och elegant sätt, och det är perfekt för när vi behöver slå ihop flera delar av information till en enda mening eller ett meddelande.

## Hur Använder Vi StringJoiner?

Användningen av StringJoiner är lika enkel som ett kattens nys! 😺 Vi skapar bara en ny instans av StringJoiner och anger den avgränsare vi vill använda mellan strängarna. Sedan lägger vi till våra strängar en efter en som pärlor på en tråd. När vi är klara kan vi få ut den sammanfogade strängen som ett enda, sammanhängande paket av text! Låt oss ta en titt på ett exempel för att göra det ännu tydligare:

```java
StringJoiner joiner = new StringJoiner(", "); // Skapar en StringJoiner med komma och mellanslag som avgränsare
joiner.add("Revan"); // I am Revan reborn, and before me you are nothing!
joiner.add("Basila Shan"); // The force is my ally, and a powerful ally it is!
joiner.add("Carth Onasi"); //  I guess stupidity and ignorance will never go out of style.
joiner.add("HK-47"); // Query: What is it you wish, meatbag?
joiner.add("Mission Vao"); // I'm not scared of you! Well, maybe a little.
joiner.add("Zaalbar"); // Rrrraaargh!
joiner.add("Darth Traya"); // It is such a quiet thing, to fall. But far more terrible is to admit it.

String result = joiner.toString();
System.out.println(result);
```

Resultatet kommer att vara:

```
Revan, Basila Shan, Carth Onasi, HK-47, Mission Vao, Zaalbar, Darth Traya
```

## Coola Användningsområden

Det bästa med StringJoiner är att det fungerar för många olika ändamål! Vi kan använda det för att skapa en lista av element, bygga SQL-frågor, eller förbereda användarvänliga meddelanden. Det är som en allt-i-ett-verktyg för att skapa snygga och välorganiserade textsträngar!

```java
String name = "Anakin Skywalker";
String replace = "Darth Vader";

// Skapa en SQL-fråga med Update
StringJoiner joiner = new StringJoiner(" ");
joiner.add("UPDATE");
joiner.add("Jedi");
joiner.add("SET");
joiner.add("name ='");
joiner.add(replace);
joiner.add("' WHERE");
joiner.add("name ='");
joiner.add(name);
joiner.add("';");
```
ger oss
```
UPDATE Jedi SET name ='Darth Vader' WHERE name ='Anakin Skywalker';
```

## Anpassning med Prefix och Suffix

Inte nog med det, vi kan även anpassa vår StringJoiner genom att ange ett
prefix och ett suffix. Detta gör att vi kan lägga till en speciell text i
början och slutet av den sammanfogade strängen. Perfekt för när vi vill skapa
kompletta meningar eller stycken!

```java
    StringJoiner logPath = new StringJoiner("", "/user/", "/documents/diary/");
    StringJoiner logEntry = new StringJoiner("", "Log/" , ".txt");
    logpath.add("Kyp Durron");
    logEntry.add("7 BoE"); // 7 år efter slaget om Endor
    String log = "Kära dagbok, idag såg jag Exar Kuns spöke :-O";

    String filePath = logPath.toString() + logEntry.toString();
    System.out.println(filePath);
    System.out.println(log);

```

Resultatet blir:

```
/user/Kyp Durron/documents/diary/Log/7 BoE.txt
Dear diary, today saw jag Exar Kuns ghost :-O
```

## Funktioner

| Funktion   | Beskrivning                                               | Exempel                                | Resultat                |
| -----------| -------------------------------------------------------- | -------------------------------------- | ----------------------- |
| StringJoiner(CharSequence delimiter) | Skapar en ny StringJoiner med angiven delimiter | `StringJoiner sj = new StringJoiner(", ");` | `""` (tom sträng) |
| add(CharSequence newElement) | Lägger till ett nytt element till StringJoiner | `sj.add("Äpple");`<br>`sj.add("Banan");`<br>`sj.add("Apelsin");` | `"Äpple, Banan, Apelsin"` |
| length() | Returnerar längden av den resulterande strängen i StringJoiner | `int length = sj.length(); System.out.println(length);` | `17` |
| setEmptyValue(CharSequence emptyValue) | Ställer in ett värde att returnera om StringJoiner är tom | `sj.setEmptyValue("Inget frukt tillgängligt");`<br>`System.out.println(sj.toString());` | `"Inget frukt tillgängligt"` |
| toString() | Returnerar den resulterande strängen i StringJoiner | `String result = sj.toString(); System.out.println(result);` | `"Äpple, Banan, Apelsin"` |

Med `StringJoiner` kan du enkelt sammanfoga flera strängar med ett delimiter och skapa en kommaseparerad lista, vilket är användbart när du hanterar listor av värden! ;)

## Slutsats

Så där har ni det, mäster kodare!

StringJoiner är ett coolt verktyg som gör textbehandling till ett nöje! Genom
att förena flera strängar till ett enda paket kan vi skapa snygga och
sammanhängande textsträngar på ett enkelt sätt. Använd StringJoiner för att
skapa listor, SQL-frågor, eller bara för att bygga meddelanden som får ditt
hjärta att slå lite snabbare! Nu är det dags att släppa loss din kreativitet
och skapa magi med dina kodsträngar! Lycka till och ha det superkul med din nya
vän, StringJoiner!
