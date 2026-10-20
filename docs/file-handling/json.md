---
title: Json
author: Marcus Ackre Medina
parent: Filhantering
nav_order: 60
---
# Json

## Introduktion till JSON

JSON (JavaScript Object Notation) är ett lättläst och lättförståeligt datautbytesformat som används för att strukturera och utbyta data mellan olika delar av en applikation eller för att kommunicera med externa API:er. Det är inspirerat av JavaScripts objektnotation, men det kan användas i många programmeringsspråk, inklusive Java. JSON är vanligtvis användbart för att representera komplexa datastrukturer på ett organiserat sätt.

För att använda JSON i Maven behöver du inkludera följande beroende i din pom.xml-fil:

```xml
<dependency>
    <groupId>org.json</groupId>
    <artifactId>json</artifactId>
    <version>20210307</version>
</dependency>
```

Välj en nyare version om det finns, undvik beta tester ;)

Det finns andra bibliotek, men vi kör på detta för att det är enkelt att använda.

### Vad är JSON?

JSON består av två huvudelement: objekt och arrayer. Ett JSON-objekt är en samling av nyckel-värde-par, där nyckeln är en sträng som identifierar ett attribut och värdet är datat som är associerat med nyckeln. JSON-objekt börjar och avslutas med måsvingar `{}`. Ett JSON-objekt kan innehålla flera nyckel-värde-par, och varje par separeras med ett kolon `:`. Exempel på ett JSON-objekt:

```json
{
  "name": "Luke Skywalker",
  "age": 25,
  "occupation": "Jedi Knight"
}
```

I det här exemplet har vi ett JSON-objekt som representerar en karaktär vid namn Luke Skywalker. Objektet innehåller nycklar som "name", "age" och "occupation" med motsvarande värden.

Ser det bekant ut?

```java
public class Character {
    private String name;
    private int age;
    private String occupation;

    public String getName() { return name;}
    public int getAge() { return age; }
    public String getOccupation() { return occupation; }
    public void setName(String name) { this.name = name; }
    public void setAge(int age) { this.age = age; }
    public void setOccupation(String occupation) { this.occupation = occupation; }
    @Override
    public String toString() {
        return String.format(
            "Name: %s, Age: %d, Occupation: %s",
            name, age, occupation);
    }
}

public class Main() {
    public static void main(String[] args) {
        Character luke = new Character();
        luke.setName("Luke Skywalker");
        luke.setAge(25);
        luke.setOccupation("Jedi Knight");
    }
}

```

### Vad är en JSON-array?

En JSON-array är en ordnad samling av värden, som kan vara strängar, tal, booleska värden, null eller andra JSON-objekt och arrayer. JSON-arrayer börjar och avslutas med hakparenteser `[]` (känns det igen? ;) ), och varje värde i arrayen separeras med ett komma `,`. Exempel på en JSON-array:

```json
[
  "Darth Vader",
  "Obi-Wan Kenobi",
  "Princess Leia"
]
```

Känns det igen?
```java
String[] names = {
    "Darth Vader",
    "Obi-Wan Kenobi",
    "Princess Leia"
};
```

I detta exempel har vi en JSON-array som representerar namnen på några karaktärer från Star Wars. Arrayen innehåller tre strängvärden.

### Hur bygger vi JSON-strukturer?

JSON-strukturer skapas genom att kombinera JSON-objekt och arrayer. Du kan ha ett JSON-objekt som innehåller arrayer, eller du kan ha arrayer som innehåller JSON-objekt. Detta gör det möjligt att representera komplexa datastrukturer på ett lättläst sätt.

Exempel på en JSON-struktur med arrayer och objekt:

```json
{
  "heroes": [
    {
      "name": "Luke Skywalker",
      "age": 25,
      "occupation": "Jedi Knight"
    },
    {
      "name": "Princess Leia",
      "age": 23,
      "occupation": "Rebel Leader"
    }
  ],
  "villains": [
    {
      "name": "Darth Vader",
      "age": 45,
      "occupation": "Sith Lord"
    }
  ]
}
```

I detta exempel har vi ett JSON-objekt som innehåller två arrayer, "heroes" och "villains". Varje array innehåller JSON-objekt som representerar olika karaktärer från Star Wars-universumet.

Hur skulle detta se ut i Java?

```java
// Återanvänder Character klassen från ovan

public class Main() {
    public static void main(String[] args) {
        List<Character> heroes = new ArrayList<>();
        heroes.add(new Character("Luke Skywalker", 25, "Jedi Knight"));
        heroes.add(new Character("Princess Leia", 23, "Rebel Leader"));

        List<Character> villains = new ArrayList<>();
        villains.add(new Character("Darth Vader", 45, "Sith Lord"));
    }
}
```

### JSON och Java

För att arbeta med JSON i Java finns det olika bibliotek som kan hjälpa oss att konvertera JSON-data till Java-objekt och vice versa. Ett av de populära biblioteken är `org.json`, som ger enkla metoder för att hantera JSON-data i Java.

För att använda `org.json`-biblioteket behöver du inkludera dess beroende i ditt projekt. Här är ett exempel på hur du kan använda detta bibliotek för att läsa in JSON-data från en fil och bearbeta den:

```java
import org.json.JSONArray;
import org.json.JSONObject;
import java.io.IOException;
import java.nine.file.Files;
import java.nine.file.Paths;

public class JSONProcessing {

    public static void main(String[] args) {
        try {
            // Läs JSON-data från en fil
            String jsonData = new String(Files.readAllBytes(Paths.get("data.json")));

            // Skapa ett JSON-objekt från inläst data
            JSONObject jsonObject = new JSONObject(jsonData);

            // Hämta JSON-arrayen "heroes" från JSON-objektet
            JSONArray heroesArray = jsonObject.getJSONArray("heroes");

            // Loopa igenom hjältarna och skriv ut deras namn och yrke
            for (int i = 0; i < heroesArray.length(); i++) {
                JSONObject hero = heroesArray.getJSONObject(i);
                String name = hero.getString("name");
                String occupation = hero.getString("occupation");
                System.out.println("Hero: " + name + ", Occupation: " + occupation);
            }

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

I detta exempel läser vi JSON-data från filen "data.json" och konverterar den till ett `JSONObject`. Vi hämtar sedan arrayen "heroes" från JSON-objektet och loopar igenom den för att få tillgång till varje hjältes namn och yrke.

### CRUD-Operationer med JSON

Nu när vi har en djupare förståelse av JSON-strukturer och hur vi kan hantera dem i Java, kan vi utföra CRUD-operationer (Create, Read, Update, Delete) med JSON-data.

Exempelkod för CRUD-Operationer:

```java
import org.json.JSONArray;
import org.json.JSONObject;

public class JSONCRUDOperations {

    public static void main(String[] args) {
        try {
            // Skapa ett JSON-objekt för en ny karaktär
            JSONObject newCharacter = new JSONObject();
            newCharacter.put("name", "Han Solo");
            newCharacter.put("age", 35);
            newCharacter.put("occupation", "Smuggler");

            // Läs befintlig JSON-data från filen "characters.json"
            String jsonData = //kod för att läsa filens innehåll;
            JSONObject jsonObject = new JSONObject(jsonData);
            JSONArray charactersArray = jsonObject.getJSONArray("characters");

            // Skapa en ny karaktär i JSON-arrayen
            charactersArray.put(newCharacter);

            // Uppdatera karaktärens ålder
            JSONObject characterToUpdate = charactersArray.getJSONObject(0);
            characterToUpdate.put("age", 36);

            // Ta bort en karaktär från JSON-arrayen
            charactersArray.remove(1);

            // Skriv tillbaka den uppdaterade JSON-datan till filen
            String json= jsonObject.toString(2);

            //kod för att spara data till filen;

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

I detta exempel visar vi hur man kan skapa, uppdatera och ta bort data i en JSON-array. Vi skapar en ny karaktär med hjälp av `JSONObject`, uppdaterar en karaktärs ålder och tar bort en annan karaktär från JSON-arrayen.

### Skapa JSON-data från Java-objekt

OK vi kan skapa klasser som `Character` och vi kan skapa `JSONObject`, men hur skapar vi JSON-data från våra Java-objekt? Nu ställer du rätt fråga! Utan den länken mellan klass och JSONobject har vi ingen praktiskt nytta av allt detta!

För att skapa JSON-data från Java-objekt kan vi använda `JSONObject`-konstruktorn som tar emot ett Java-objekt som argument. Detta konverterar automatiskt Java-objektet till JSON-data. Exempel:

Först, se till att ditt Maven projekt har googles JSON bibliotek:

```xml
<dependency>
    <groupId>com.google.code.gson</groupId>
    <artifactId>gson</artifactId>
</dependency>
```

```java
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;

public class JSONFromJavaObject {

    public static void main(String[] args) {
        // Skapa ett Java-objekt
        Character luke = new Character("Luke Skywalker", 25, "Jedi Knight");

        // Skapa ett JSON-objekt från Java-objektet
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        String json = gson.toJson(luke);
        System.out.println(json);
    }
}
```

Outputten blir

```json
{
  "name": "Luke Skywalker",
  "age": 25,
  "occupation": "Jedi Knight"
}
```

OK, det funkade, men hur gör vi med en lista av objekt?

```java
import com.google.gson.Gson;
import com.google.gson.GsonBuilder;
import java.util.ArrayList;
import java.util.List;

public class JSONFromJavaObject {

    public static void main(String[] args) {
        // Skapa ett Java-objekt
        List<Character> characters = new ArrayList<>();
        characters.add(new Character("Luke Skywalker", 25, "Jedi Knight"));
        characters.add(new Character("Princess Leia", 23, "Rebel Leader"));

        // Skapa ett JSON-objekt från Java-objektet
        Gson gson = new GsonBuilder().setPrettyPrinting().create();
        String json = gson.toJson(characters);
        System.out.println(json);
    }
}
```

Output blir

```json
[
  {
    "name": "Luke Skywalker",
    "age": 25,
    "occupation": "Jedi Knight"
  },
  {
    "name": "Princess Leia",
    "age": 23,
    "occupation": "Rebel Leader"
  }
]
```

Najs! _Som Taylor Swift skulle sagt! (Om du inte är en Swiftie så ropar hon **Nice!** i låten Bejeweled)_

## Slutsats

JSON är en kraftfull och lättläst struktur för datautbyte som används över hela programmeringsvärlden. Med `org.json`-biblioteket kan vi enkelt hantera JSON-data i Java och utföra CRUD-operationer för att manipulera vår data. Genom att förstå hur man bygger JSON-strukturer med objekt och arrayer kan vi skapa komplexa datastrukturer som hjälper oss att representera och utbyta data på ett organiserat sätt. Så ge dig ut i den datavävda galaxen och utforska möjligheterna med JSON i din Java-programmering!

## Obligatorisk dad joke:

Vad sa Json till XML?

Oj! vad du gått upp i vikt!

**Förklaring:**

```json
[
  {
    "name": "Luke Skywalker",
    "age": 25,
    "occupation": "Jedi Knight"
  },
  {
    "name": "Princess Leia",
    "age": 23,
    "occupation": "Rebel Leader"
  }
]
```
i XML blir
```xml
<character>
    <name>Luke Skywalker</name>
    <age>25</age>
    <occupation>Jedi Knight</occupation>
</character>
<character>
    <name>Princess Leia</name>
    <age>23</age>
    <occupation>Rebel Leader</occupation>
</character>
```
