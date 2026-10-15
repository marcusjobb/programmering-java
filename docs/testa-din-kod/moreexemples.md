---
title: Fler exempel
author: Marcus Ackre Medina
parent: Testa din kod
nav_order: 50
---
# Fler exempel

I den här övningen fokuserar vi på att skapa testfall för en enkel Java-klass, som hanterar
information om en person. Vi kommer att utforska konstruktorer, strängar och DateTime. Låt oss
börja med att skapa klassen Person.java.

```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Lägg till getters och setters för name och age här
}
```

Självklart måste du förse din Maven med JUnit för att kunna köra testerna. Detta gör du genom att
lägga till följande kod i din pom.xml:

```xml
<dependencies>
    <dependency>
        <groupId>junit</groupId>
        <artifactId>junit</artifactId>
        <version>4.13.2</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

Detta är en enkel kod som inte gör mycket, men vi kommer att testa den för att se att den fungerar korrekt.

## TL;DR

Denna övning handlar om att testa en Java-klass som hanterar information om en person. Vi kommer
att utforska konstruktorer, strängar och DateTime. Genom att använda TDD-metoden (Test-Driven
Development) bygger vi upp tester för att säkerställa att vår kod fungerar korrekt.

## När du läst detta ska du kunna

- Förstå vikten av enhetstestning och TDD.
- Skapa grundläggande testfall för en Java-klass.
- Utforska konstruktorer, strängar och DateTime i Java.

## Skapa testfall för konstruktorn

Låt oss börja med att skapa några testfall för konstruktorn i vår Person-klass. Vi vill se till att
properties sätts rätt och att konstruktorn fungerar korrekt. Vi börjar med ett enkelt testfall för
att verifiera att namn och ålder sätts korrekt när vi skapar en person.

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class PersonTest {

    @Test
    public void testConstructor() {
        Person person = new Person("Pelle", 25);
        assertEquals("Pelle", person.getName());
        assertEquals(25, person.getAge());
    }
}
```

Nu har vi ett grundläggande testfall som kontrollerar att properties sätts korrekt när vi skapar en person. Låt oss fortsätta med att testa om konstruktorn kan hantera ett null-värde som namn.

```java
@Test
public void testConstructorNullName() {
    Person person = new Person(null, 32);
    assertNull(person.getName());
    assertEquals(32, person.getAge());
}
```

Det fungerar alldeles utmärkt! Nu har vi verifierat att det går att skapa en person utan att det kraschar, och vi vet nu med säkerhet att en sträng (namn) kan vara null.

## Utforska DateTime-beräkningar

Nu när vi har testat konstruktorn, ska vi titta på DateTime-beräkningar. Vi kommer att räkna ut åldern på personen genom att ändra vår konstruktor så att den tar emot ett Date-objekt istället för en ålder som en int.

```java
import java.util.Date;

public class Person {
    private String name;
    private Date birthDate;

    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public Date getBirthDate() { return birthDate; }
    public void setBirthDate(Date birthDate) { this.birthDate = birthDate; }
    public void setBirthDate(string birthDate) { this.birthDate = new Date(birthDate); } // för att vara snäll mot användaren
}
```

Eftersom vi använder oss av en metod för att beräkna åldern i konstruktorn, låt oss skapa den metoden.

```java
import java.util.Date;

public class Person {
    // kod för name och birthDate

    public Person(String name, Date birthDate) {
        this.name = name;
        this.birthDate = birthDate;
        this.age = calculateAge(birthDate);
    }

    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public Date getBirthDate() { return birthDate; }
    public void setBirthDate(Date birthDate) { this.birthDate = birthDate; }
    public void setBirthDate(string birthDate) { this.birthDate = new Date(birthDate); } // för att vara snäll mot användaren

    private int calculateAge(Date birthDate) {
        // implementera beräkning av ålder här
    }
}
```

Nu har vi skapat en metod för att beräkna åldern. Låt oss implementera den genom att använda Date-klassen i Java.

```java
import java.util.Date;

public class Person {
    // kod för name och birthDate

    public Person(String name, Date birthDate) {
        this.name = name;
        this.birthDate = birthDate;
        this.age = calculateAge(birthDate);
    }

    // getters och setters för name och birthDate

    private int calculateAge(Date birthDate) {
        // Dagens datum
        long currentTime = System.currentTimeMillis();
        // Ålder i millisekunder
        long ageInMillis = currentTime - birthDate.getTime();
        // Ålder i år
        return (int) (ageInMillis / (1000 * 60 * 60 * 24 * 365.25));
    }
}
```

Nu kan vi beräkna åldern korrekt baserat på birthDate. Vi har skrivit en kort och enkel kod för att ta reda på antal år som passerat och sedan dividerat med 365.25 för att få fram antal år (inklusive skottår).

## Skapa egenskaper och tester för olika åldersbegränsningar

Nu när vi kan beräkna åldern på personen, låt oss skapa egenskaper för olika åldersbegränsningar. Vi kommer att använda boolean-värden för att indikera om personen uppfyller åldersbegränsningen eller inte.

```java
import java.util.Date;

public class Person {
    // kod för name och birthDate

    public Person(String name, Date birthDate) {
        this.name = name;
        this.birthDate = birthDate;
        this.age = calculateAge(birthDate);
    }

    // kod för calculateAge-metoden

    public boolean canGetMarried() {
        // Vi returnerar svaret på jämförelsen, så slipper vi skapa en extra variabel och if-sats
        return age >= 18;
    }

    public boolean canRetireByAge() {
        // Vi returnerar svaret på jämförelsen, så slipper vi skapa en extra variabel och if-sats
        return age >= 62;
    }
}
```

Vi har skapat två egenskaper som kontrollerar om personen kan gifta sig och gå i pension baserat på åldern. Låt oss nu skriva tester för dessa egenskaper.

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class PersonTest {

    @Test
    public void testCanGetMarried() {
        // Vi skapar en person som är 18 år gammal
        int year = Calendar.getInstance().get(Calendar.YEAR)-16;
        Date birthDate = new Date(year, 0, 1);
        Person person = new Person("Pelle", birthDate);
        assertFalse(person.canGetMarried()); // Person är för ung för att gifta sig
        assertEquals(16, person.getAge()); // Vi kontrollerar att åldern är 16 år
    }

    @Test
    public void testCanRetireByAge() {
        // Vi skapar en person som är 66 år gammal
        int birthYear = Calendar.getInstance().get(Calendar.YEAR)-62;
        Date birthDate = new Date(1959 - 1900, 0, 1);
        Person person = new Person("Johan", birthDate);
        assertFalse(person.canRetireByAge());
        assertEquals(62, person.getAge());
    }
}
```

Varför skapar vi en person som är 16 år gammal i testet för canGetMarried? Detta är för att vi vill
testa att personen inte kan gifta sig om den är för ung. Vi vill också kontrollera att åldern är 16
år, eftersom vi har skapat en person som är 16 år gammal. På samma sätt skapar vi en person som är
66 år gammal i testet för canRetireByAge. Vi vill kontrollera att personen inte kan gå i pension om
den är för ung, och vi vill också kontrollera att åldern är 62 år.

Nu undrar du varför vi använder `Calendar.getInstance().get(Calendar.YEAR)` för att få året. Detta
är för att vi vill ha ett dynamiskt värde för året, så att testerna fungerar även nästa år. Om vi
använder `Date birthDate = new Date(2023, 0, 1);` kommer testet att misslyckas 2024, eftersom
personen då är 17 år gammal.

Nu har vi två tester som kontrollerar om egenskaperna canGetMarried och canRetireByAge fungerar
korrekt beroende på åldern. Genom att använda TDD-metoden har vi säkerställt att vår kod fungerar
korrekt och har skapat testfall för olika scenarier.

Ibland måste vi skapa smartare tester, för att dynamisk föränderlig information inte ska sabba det
för oss. Datum och tid är svåra att testa mot, därför måste vi se till att grundmaterialet för
testerna är lika anpassningsbar som det vi testar. Detta är en av anledningarna till att vi använder
oss av `Calendar.getInstance().get(Calendar.YEAR)` istället för att hårdkoda året.

## Summan av kardemumman

Grattis! Du har nu utforskat TDD-övningar i Java, där du har testat en enkel Java-klass för att
hantera information om en person. Du har också utforskat konstruktorer, strängar och DateTime i
Java-programmering. Fortsätt att öva på TDD och enhetstestning, och låt din programmeringsresa bli
ännu roligare och mer inspirerande! Happy coding! 🚀😊
