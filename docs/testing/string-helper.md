---
title: Stringhelper
author: Marcus Ackre Medina
parent: Testa din kod
nav_order: 40
---
# Stringhelper

Stränghantering är alltid krånglig, så vi ska skapa några metoder som förenklar arbetet med
strängar. Vi ska använda TDD för att skapa dessa metoder.

# Test-Driven Development (TDD) med StringHelper i Java

Test-Driven Development (TDD) är en utvecklingsmetodik där tester skrivs innan den faktiska koden
skapas. Vi kommer att tillämpa TDD för att utveckla en klass kallad StringHelper. Denna klass
kommer att innehålla olika metoder för strängmanipulation.

Var noga med att ditt Mavenprojekt innehåller
följande beroenden:

```xml
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.9.3</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

## Steg 1: Skapa projekt och StringHelper-klass

Först börjar vi med att skapa ett nytt Java-projekt i din favorit-IDE (Integrated Development
Environment). Skapa sedan en ny Java-klass med namnet "StringHelper".

```java
public class StringHelper {
    package com.marcusjobb;

    import java.util.Arrays;
    import java.util.List;

}
```

## Steg 2: Skapa metoden GetWord

Nu ska vi skapa metoder till vår klass att implementera metoden "GetWord", som returnerar ett specifikt ord från en sträng vid ett givet index. Om ett separator tecken anges delar metoden strängen baserat på det.

```java
/**
 * Returnerar ett specifikt ord från en sträng vid ett givet index.
 * Om ett separator-tecken anges, delas strängen baserat på det.
 *
 * @param text      strängen som ska delas och behandlas
 * @param x         indexet för det önskade ordet i strängen
 * @param separator (valfritt) tecknet som används för att dela strängen, standardvärde är mellanslag
 * @return det önskade ordet vid det givna indexet eller en tom sträng om indexet är ogiltigt
 */
public String GetWord(String text, int x, char separator) {
    // Implementera koden för att få ordet vid det givna indexet från strängen
    // och dela strängen med separator om det är angivet.
    return "";
}
```

## Steg 3: Skapa metoden StringToList

Nästa metod vi ska implementera är "StringToList", som tar en sträng och returnerar en lista med dess ord, delade genom ett separator-tecken om det är angivet.

```java
/**
 * Delar en sträng baserat på ett separator-tecken (om angivet) och returnerar en lista med dess ord.
 *
 * @param text      strängen som ska delas och behandlas
 * @param separator (valfritt) tecknet som används för att dela strängen, standardvärde är mellanslag
 * @return en List<String> som innehåller ord från den ursprungliga strängen
 */
public List<String> StringToList(String text, char separator) {
    // Implementera koden för att dela strängen och returnera en List<String>.
    return new ArrayList<>();
}
```

## Steg 4: Skapa metoden RemoveWord

Nu ska vi skapa metoden "RemoveWord", som tar bort ett specifikt ord från en given text och returnerar den uppdaterade texten.

```java
/**
 * Tar bort ett specifikt ord från en given text och returnerar den uppdaterade texten.
 *
 * @param text   den ursprungliga texten som ska bearbetas
 * @param remove ordet som ska tas bort från texten
 * @return den uppdaterade texten utan det specifika ordet
 */
public String RemoveWord(String text, String remove) {
    // Implementera koden för att ta bort ett specifikt ord från texten.
    return "";
}
```

## Steg 5: Skapa metoden RemoveWordAt

Nu ska vi implementera metoden "RemoveWordAt", som tar bort ett ord från en given text baserat på dess index i texten.

```java
/**
 * Tar bort ett ord från en given text baserat på dess index i texten.
 *
 * @param text den ursprungliga texten som ska bearbetas
 * @param pos  indexet för ordet som ska tas bort
 * @return den uppdaterade texten utan det ordet vid det givna indexet
 */
public String RemoveWordAt(String text, int pos) {
    // Implementera koden för att ta bort ordet vid det givna indexet från texten.
    return "";
}
```

## Steg 6: Skapa metoden InsertWordAfter

Vi kommer nu att skapa metoden "InsertWordAfter", som lägger till ett ord efter ett annat ord i en given text.

```java
/**
 * Lägger till ett ord efter ett annat ord i en given text.
 *
 * @param text  den ursprungliga texten som ska bearbetas
 * @param after ordet efter vilket det nya ordet ska läggas till
 * @param add   det nya ordet som ska läggas till
 * @return den uppdaterade texten med det nya ordet infogat efter det angivna ordet
 */
public String InsertWordAfter(String text, String after, String add) {
// Implementera koden för att lägga till ett ord efter ett annat ord i texten.
return "";
}
```

## Steg 7: Skapa metoden SwapWords

Slutligen, låt oss implementera metoden "SwapWords", som byter plats på två ord i en given text.

/**
* Byter plats på två ord i en given text.
*
* @param text  den ursprungliga texten som ska bearbetas
* @param word1 det första ordet som ska byta plats
* @param word2 det andra ordet som ska byta plats
* @return den uppdaterade texten med de två orden bytta
*/
```java
public String SwapWords(String text, String word1, String word2) {
    // Implementera koden för att byta plats på två ord i texten.
    return "";
}
```
## Hela klassen

Här är hela StringHelper-klassen med alla metoder implementerade:

```java
package com.marcusjobb;

import java.util.Arrays;
import java.util.List;
import java.util.Objects;

public class StringHelper {
    /**
     * Returnerar ett specifikt ord från en sträng vid ett givet index.
     * Om ett separator-tecken anges, delas strängen baserat på det.
     *
     * @param text      strängen som ska delas och behandlas
     * @param x         indexet för det önskade ordet i strängen
     * @param separator (valfritt) tecknet som används för att dela strängen, standardvärde är mellanslag
     * @return det önskade ordet vid det givna indexet eller en tom sträng om indexet är ogiltigt
     */
    public String GetWord(String text, int x, char separator) {
        // Implementera koden för att få ordet vid det givna indexet från strängen
        // och dela strängen med separator om det är angivet.
        String[] words = text.split(Character.toString(separator));
        if (x >= 0 && x < words.length) {
            return words[x];
        }
        return "";

    }

    /**
     * Delar en sträng baserat på ett separator-tecken (om angivet) och returnerar en lista med dess ord.
     *
     * @param text      strängen som ska delas och behandlas
     * @param separator (valfritt) tecknet som används för att dela strängen, standardvärde är mellanslag
     * @return en List<String> som innehåller ord från den ursprungliga strängen
     */
    public List<String> StringToList(String text, char separator) {
        // Implementera koden för att dela strängen och returnera en List<String>.
        return Arrays.asList(text.split(Character.toString(separator)));
    }

    /**
     * Tar bort ett specifikt ord från en given text och returnerar den uppdaterade texten.
     *
     * @param text   den ursprungliga texten som ska bearbetas
     * @param remove ordet som ska tas bort från texten
     * @return den uppdaterade texten utan det specifika ordet
     */
    public String RemoveWord(String text, String remove) {
        // Implementera koden för att ta bort ett specifikt ord från texten.
        return text.replace(remove, "");
    }

    /**
     * Tar bort ett ord från en given text baserat på dess index i texten.
     *
     * @param text den ursprungliga texten som ska bearbetas
     * @param pos  indexet för ordet som ska tas bort
     * @return den uppdaterade texten utan det ordet vid det givna indexet
     */
    public String RemoveWordAt(String text, int pos) {
        // Implementera koden för att ta bort ordet vid det givna indexet från texten.
        String[] words = text.split("\\s+");
        if (pos >= 0 && pos < words.length) {
            StringBuilder result = new StringBuilder();
            for (int i = 0; i < words.length; i++) {
                if (i != pos) {
                    result.append(words[i]).append(" ");
                }
            }
            return result.toString().trim();
        }
        return text;
    }

    /**
     * Lägger till ett ord efter ett annat ord i en given text.
     *
     * @param text  den ursprungliga texten som ska bearbetas
     * @param after ordet efter vilket det nya ordet ska läggas till
     * @param add   det nya ordet som ska läggas till
     * @return den uppdaterade texten med det nya ordet infogat efter det angivna ordet
     */
    public String InsertWordAfter(String text, String after, String add) {
        // Implementera koden för att lägga till ett ord efter ett annat ord i texten.
        return text.replace(after, after + " " + add);
    }

    /**
     * Byter plats på två ord i en given text.
     *
     * @param text  den ursprungliga texten som ska bearbetas
     * @param word1 det första ordet som ska byta plats
     * @param word2 det andra ordet som ska byta plats
     * @return den uppdaterade texten med de två orden bytta
     */
    public String SwapWords(String text, String word1, String word2) {
        // Implementera koden för att byta plats på två ord i texten.
        return text.replace(word1, "TEMP").replace(word2, word1).replace("TEMP", word2);
    }
}

```

## Steg 8: Skapa testklassen

Nu ska vi skapa en testklass för att testa vår StringHelper-klass. Vi kommer att använda JUnit för att skapa våra testfall.

```java
package com.marcusjobb;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

import java.util.Arrays;

import static org.junit.jupiter.api.Assertions.*;

public class StringHelperTest {

    StringHelper stringHelper;

    @BeforeEach
    public void beforeEach() {
        stringHelper = new StringHelper();
    }

    @Test
    public void testGetWord() {

    }

    @Test
    public void testStringToList() {

    }

    @Test
    public void testRemoveWord() {
    }

    @Test
    public void testRemoveWordAt() {
    }

    @Test
    public void testInsertWordAfter() {
    }

    @Test
    public void testSwapWords() {
    }
}
```

## Facit

Här är de implementerade metoderna för StringHelper-klassen:

<details><summary>Klicka här för att se facit</summary>

```java
package com.marcusjobb;

import java.util.Arrays;
import java.util.List;
import java.util.Objects;

public class StringHelper {
    /**
     * Returnerar ett specifikt ord från en sträng vid ett givet index.
     * Om ett separator-tecken anges, delas strängen baserat på det.
     *
     * @param text      strängen som ska delas och behandlas
     * @param x         indexet för det önskade ordet i strängen
     * @param separator (valfritt) tecknet som används för att dela strängen, standardvärde är mellanslag
     * @return det önskade ordet vid det givna indexet eller en tom sträng om indexet är ogiltigt
     */
    public String GetWord(String text, int x, char separator) {
        // Implementera koden för att få ordet vid det givna indexet från strängen
        // och dela strängen med separator om det är angivet.
        String[] words = text.split(Character.toString(separator));
        if (x >= 0 && x < words.length) {
            return words[x];
        }
        return "";
    }

    /**
     * Delar en sträng baserat på ett separator-tecken (om angivet) och returnerar en lista med dess ord.
     *
     * @param text      strängen som ska delas och behandlas
     * @param separator (valfritt) tecknet som används för att dela strängen, standardvärde är mellanslag
     * @return en List<String> som innehåller ord från den ursprungliga strängen
     */
    public List<String> StringToList(String text, char separator) {
        // Implementera koden för att dela strängen och returnera en List<String>.
        // Trimma alla rader innan return
        String[] words = text.split(Character.toString(separator));
        for (int i = 0; i < words.length; i++) {
            words[i] = words[i].trim();
        }
        return Arrays.asList(words);
    }

    /**
     * Tar bort ett specifikt ord från en given text och returnerar den uppdaterade texten.
     *
     * @param text   den ursprungliga texten som ska bearbetas
     * @param remove ordet som ska tas bort från texten
     * @return den uppdaterade texten utan det specifika ordet
     */
    public String RemoveWord(String text, String remove) {
        // Implementera koden för att ta bort ett specifikt ord från texten.
        return text.replace(remove, "");
    }

    /**
     * Tar bort ett ord från en given text baserat på dess index i texten.
     *
     * @param text den ursprungliga texten som ska bearbetas
     * @param pos  indexet för ordet som ska tas bort
     * @return den uppdaterade texten utan det ordet vid det givna indexet
     */
    public String RemoveWordAt(String text, int pos) {
        // Implementera koden för att ta bort ordet vid det givna indexet från texten.
        String[] words = text.split("\\s+");
        if (pos >= 0 && pos < words.length) {
            StringBuilder result = new StringBuilder();
            for (int i = 0; i < words.length; i++) {
                if (i != pos) {
                    result.append(words[i]).append(" ");
                }
            }
            return result.toString().trim();
        }
        return text;
    }

    /**
     * Lägger till ett ord efter ett annat ord i en given text.
     *
     * @param text  den ursprungliga texten som ska bearbetas
     * @param after ordet efter vilket det nya ordet ska läggas till
     * @param add   det nya ordet som ska läggas till
     * @return den uppdaterade texten med det nya ordet infogat efter det angivna ordet
     */
    public String InsertWordAfter(String text, String after, String add) {
        // Kontrollera edge cases
        if (!text.contains(after)) return text;
        if (text.equals("") || after.equals("") || add.equals("")) return text;

        // gör jobbet
        return text.replace(after, after + " " + add);
    }

    /**
     * Byter plats på två ord i en given text.
     *
     * @param text  den ursprungliga texten som ska bearbetas
     * @param word1 det första ordet som ska byta plats
     * @param word2 det andra ordet som ska byta plats
     * @return den uppdaterade texten med de två orden bytta
     */
    public String SwapWords(String text, String word1, String word2) {
        // Implementera koden för att byta plats på två ord i texten.
        return text.replace(word1, "TEMP").replace(word2, word1).replace("TEMP", word2);
    }
}
```

Här är lösningen på testklassen:

```java
package com.marcusjobb;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

import java.util.Arrays;

import static org.junit.jupiter.api.Assertions.*;

public class StringHelperTest {

    StringHelper stringHelper;

    @BeforeEach
    public void beforeEach() {
        stringHelper = new StringHelper();
    }
    @Test
    public void testGetWord() {
        String text = "It's not wise to upset a Wookiee";
        char separator = ' ';

        // Vanlig test
        assertEquals("wise", stringHelper.GetWord(text, 2, separator));
        assertEquals("Wookiee", stringHelper.GetWord(text, 6, separator));

        // Edge case
        assertEquals("", stringHelper.GetWord(text, 10, separator));
        assertEquals("", stringHelper.GetWord(text, -1, separator));
    }

    @Test
    public void testStringToList() {
        String text = "Luke, Leia, Han, Chewie";

        // Vanlig test
        assertEquals(Arrays.asList("Luke", "Leia", "Han", "Chewie"), stringHelper.StringToList(text, ','));

        // Edge case
        assertEquals(Arrays.asList("Luke,", "Leia,", "Han,", "Chewie"), stringHelper.StringToList(text, ' '));
    }

    @Test
    public void testRemoveWord() {
        String text = "May the force be with you always";

        // Vanlig test
        assertEquals("May the force be with you ", stringHelper.RemoveWord(text, "always"));
        assertEquals("May  force be with you always", stringHelper.RemoveWord(text, "the"));
        // Observera att orden som valdes tas bort, men inte mellanslag före eller efter
        // därav "May  force be with you always" och inte "May force be with you "

        // Edge case
        assertEquals(text, stringHelper.RemoveWord(text, "Java"));
    }

    @Test
    public void testRemoveWordAt() {
        String text = "The force is my ally";

        // Vanlig test
        assertEquals("The force my ally", stringHelper.RemoveWordAt(text, 2));
        assertEquals("The force is ally", stringHelper.RemoveWordAt(text, 3));
        // Edge case
        assertEquals(text, stringHelper.RemoveWordAt(text, 10));
        assertEquals(text, stringHelper.RemoveWordAt(text, -1));
    }

    @Test
    public void testInsertWordAfter() {
        String text = "The force is strong with this one";

        // Vanlig test
        assertEquals("The force is really strong with this one", stringHelper.InsertWordAfter(text, "force is", "really"));
        assertEquals("The force is strong with the cat of this one", stringHelper.InsertWordAfter(text, "with", "the cat of"));

        // Edge case
        assertEquals(text, stringHelper.InsertWordAfter(text, "Java", "rocks"));
        assertEquals(text, stringHelper.InsertWordAfter(text, "", "rocks"));
        assertEquals(text, stringHelper.InsertWordAfter(text, "Java", ""));
        assertEquals(text, stringHelper.InsertWordAfter(text, "is", ""));
    }

    @Test
    public void testSwapWords() {
        String text = "Trust the Force";

        // Vanlig test
        assertEquals("Trust the Jedi", stringHelper.SwapWords(text, "Force", "Jedi"));
        assertEquals("Force the Trust", stringHelper.SwapWords(text, "Trust", "Force"));

        // Edge case
        assertEquals(text, stringHelper.SwapWords(text, "Java", "rocks"));
        assertEquals(text, stringHelper.SwapWords(text, "", "rocks"));
    }
}
```

## Avslutning

Grattis! Du har nu framgångsrikt implementerat olika strängmanipulationsmetoder med hjälp av Test-Driven Development. TDD är en kraftfull metod för att säkerställa att din kod fungerar som den ska och att den är enkel att underhålla. Fortsätt utforska Java-programmering och ta dig an nya spännande utmaningar för att förbättra dina färdigheter som utvecklare!

## Obligatorisk dad joke:

Varför kunde inte astronomen som blev programmerare sluta skriva kod?
För att han hittade sig själv i en oändlig loop! 😄
