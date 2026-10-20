---
title: Textfiler
author: Marcus Ackre Medina
parent: Filhantering
nav_order: 40
---
# Textfiler

## När du läst detta ska du kunna

- Förstå och förklara hur man skapar och manipulerar textfiler i Java.
- Diskutera fördelar och begränsningar med att använda filhantering i Java.
- Identifiera olika användningsområden där filhantering kan vara användbart.
- Förstå hur man läser och skriver textfiler i olika situationer.

## Introduktion

Textfiler är en vanlig filtyp som används för att lagra textbaserad data. I Java kan vi använda olika klasser och metoder för att skapa, läsa, skriva över och radera textfiler. I Detta avsnitt kommer vi att utforska hur vi kan hantera textfiler i Java och vilka möjligheter det ger oss.

## Skapa en textfil

För att skapa en textfil i Java använder vi klasserna `FileWriter` och `BufferedWriter`. Följande kod visar hur man skapar en textfil och skriver innehållet till filen:

```java
String contents = "God morgon Mr Bond! Jag har ett meddelande till dig.";
String fileName = "Message.txt";

try {
    FileWriter fileWriter = new FileWriter(fileName);
    BufferedWriter bufferedWriter = new BufferedWriter(fileWriter);
    bufferedWriter.write(contents);
    bufferedWriter.close();
    System.out.println("Textfilen har skapats.");
} catch (IOException e) {
    System.out.println("Ett fel inträffade vid skapandet av textfilen.");
}
```

## Läs in en textfil

För att läsa innehållet från en textfil använder vi klassen `Scanner`. Här är hur vi kan läsa innehållet från en textfil:

```java
try {
    File file = new File("Message.txt");
    Scanner scanner = new Scanner(file);
    while (scanner.hasNextLine()) {
        String contents = scanner.nextLine();
        System.out.println(contents);
    }
    scanner.close();
} catch (FileNotFoundException e) {
    System.out.println("Textfilen kunde inte hittas.");
}
```

## Spara en lista i en textfil

Ibland vill vi spara en lista av data i en textfil. Vi kan använda `FileWriter` och `BufferedWriter` för att uppnå detta. Här är ett exempel på hur vi kan spara en lista av strängar i en textfil:

```java
List<String> names = new ArrayList<>();
names.add("Picard");
names.add("Janeway");
names.add("Kirk");
names.add("Sisko");
names.add("Archer");

try {
    FileWriter fileWriter = new FileWriter("names.txt");
    BufferedWriter bufferedWriter = new BufferedWriter(fileWriter);
    for (String name : names) {
        bufferedWriter.write(name);
        bufferedWriter.newLine();
    }
    bufferedWriter.close();
    System.out.println("Listan har sparats i textfilen.");
} catch (IOException e) {
    System.out.println("Ett fel inträffade vid sparandet av listan i textfilen.");
}
```

## Läs in en lista från en textfil

När vi vill läsa innehållet från en textfil och spara det i en lista, kan vi använda klassen `Scanner` igen. Här är ett exempel på hur vi kan göra det:

```java
List<String> names = new ArrayList<>();

try {
    File file = new File("names.txt");
    Scanner scanner = new Scanner(file);
    while (scanner.hasNextLine()) {
        String name = scanner.nextLine();
        names.add(name);
    }
    scanner.close();
} catch (FileNotFoundException e) {
    System.out.println("Textfilen kunde inte hittas.");
}
```

## Lägg till text i en textfil

För att lägga till text i en befintlig textfil använder vi `FileWriter` igen. Här är ett exempel på hur man gör det:

```java
String contents = "James Bond, din uppgift är enkel men avgörande: Sök upp den fiktiva elakingen och eliminera honom utan nåd. Låt inget stå i vägen för rättvisa och säkerhet. Var din vanliga självsäkra och eleganta själv. Tiden är knapp, agera snabbt och precist. Världen litar på dig, 007. Gör det som behöver göras.";
String fileName = "Message.txt";

try {
    FileWriter fileWriter = new FileWriter(fileName, true);
    BufferedWriter bufferedWriter = new BufferedWriter(fileWriter);
    bufferedWriter.newLine();
    bufferedWriter.write(contents);
    bufferedWriter.close();
    System.out.println("Texten har lagts till i textfilen.");
} catch (IOException e) {
    System.out.println("Ett fel inträffade vid tillägg av texten i textfilen.");
}
```

## Skriv över en textfil

Om vi vill skriva över innehållet i en textfil helt och hållet, använder vi `FileWriter` utan att ange `true` som andra argument. Här är hur man skriver över en textfil:

```java
String message = "Message deducted.";
String fileName = "Message.txt";

try {
    FileWriter fileWriter = new FileWriter(fileName);
    BufferedWriter bufferedWriter = new BufferedWriter(fileWriter);
    bufferedWriter.write(message);
    bufferedWriter.close();
    System.out.println("Textfilen har skrivits över.");
} catch (IOException e) {
    System.out.println("Ett fel inträffade vid skrivning över textfilen.");
}
```

## Radera en textfil

För att radera en textfil använder vi klassen `File`. Här är hur vi kan radera en textfil:

```java
String fileName = "Message.txt";

try {
    File file = new File(fileName);
    if (file.delete()) {
        System.out.println("Textfilen har raderats.");
    } else {
        System.out.println("Kunde inte radera textfilen.");
    }
} catch (Exception e) {
    System.out.println("Ett fel inträffade vid radering av textfilen.");
}
```

## Läs in en textfil från en URL

För att läsa innehållet i en textfil från en URL, använder vi `URL` och `Scanner`. Här är ett exempel på hur man gör det:

```java
try {
    URL url = new URL("https://minwebbsida/text.txt");
    Scanner scanner = new Scanner(url.openStream());
    while (scanner.hasNextLine()) {
        String contents = scanner.nextLine();
        System.out.println(contents);
    }
    scanner.close();
} catch (IOException e) {
    System.out.println("Ett fel inträffade vid läsning av textfilen.");
}
```

## Spara en textfil från en URL

Om vi vill spara en textfil från en URL, använder vi `URL

`, `InputStream` och `Files`. Här är hur vi kan göra det:

```java
try {
    URL url = new URL("https://minwebbsida/text.txt");
    InputStream inputStream = url.openStream();
    Files.copy(inputStream, Paths.get("text.txt"), StandardCopyOption.REPLACE_EXISTING);
    System.out.println("Textfilen har sparats.");
} catch (IOException e) {
    System.out.println("Ett fel inträffade vid sparande av textfilen.");
}
```

## Lista på termer i artikeln

| Ord                | Förklaring                                                               |
| ------------------ | ------------------------------------------------------------------------ |
| Buffer             | En buffert är en tillfällig lagringsplats för data.                      |
| Buffering          | Att använda en buffert för att lagra data.                               |
| Byte               | En byte är en enhet för digital information som består av åtta bitar.    |
| Byte array         | En byte array är en samling av bytes.                                    |
| Byte stream        | En byte stream är en sekvens av bytes.                                   |
| Character stream   | En character stream är en sekvens av tecken.                             |
| Close              | Att stänga en filanslutning.                                             |
| Copy               | Att kopiera en fil.                                                      |
| File               | En fil är en samling av data som lagras på en enhet.                     |
| File path          | En filväg är en sträng som identifierar en fil.                          |
| File writer        | En filskrivare är en klass som används för att skriva till filer.        |
| File reader        | En filskrivare är en klass som används för att läsa från filer.          |
| File input stream  | En filinmatningsström är en ström som används för att läsa från filer.   |
| File output stream | En filutmatningsström är en ström som används för att skriva till filer. |
| File writer        | En filskrivare är en klass som används för att skriva till filer.        |
| File reader        | En filskrivare är en klass som används för att läsa från filer.          |

## Obligatorisk Dad-joke

Varför gillar textfiler att gå på fester?

För att de älskar att dra skämt om "line"-dans! :)
