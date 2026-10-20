---
title: Stringformat
grand_parent: Variabler
author: Marcus Ackre Medina
parent: Stränghantering
nav_order: 10
---
# Stringformat

## Introduktion

Nu ska vi att utforska hur vi kan hantera text på ett strukturerat och roligt sätt med hjälp av "String format". Det är verkligen coolt, för det låter oss skapa textsträngar med dynamiska variabler som ger oss en personlig touch i våra applikationer. Låt oss ta reda på hur vi kan göra textbehandling till en kul och inspirerande upplevelse!

Tänk dig mardrömmen att skriva ut fem personer med namn och ålder

```java
String name = "Anakin";
int age1 = 9;
String name = "Padme";
int age2 = 14;
String name = "Obi Wan";
int age3 = 25;
String name = "Qui Gon";
int age4 = 38;

System.out.println("Namn: " + name + ", Ålder: " + age1);
System.out.println("Namn: " + name + ", Ålder: " + age2);
System.out.println("Namn: " + name + ", Ålder: " + age3);
System.out.println("Namn: " + name + ", Ålder: " + age4);
```

Det funkar men det ser rörigt ut, med String.format kan vi göra det snyggare

```java
System.out.println(String.format("Namn: %s, Ålder: %d", name, age1));
System.out.println(String.format("Namn: %s, Ålder: %d", name, age2));
System.out.println(String.format("Namn: %s, Ålder: %d", name, age3));
System.out.println(String.format("Namn: %s, Ålder: %d", name, age4));
```

## TL;DR

"String format" i Java låter oss skapa strukturerade textsträngar med variabler för att göra textbehandlingen lättläst och anpassningsbar. Det ger oss möjlighet att skapa imponerande användargränssnitt och ge våra applikationer en personlig touch.

## När du läst detta ska du kunna

- Förstå konceptet av "String format" i Java.
- Använda formatmönster för att skapa strukturerad och dynamisk text.
- Använda olika specifikatorer för att formatera olika typer av variabler.
- Använda "String format" för att förbättra användarupplevelsen i Java-applikationer.

## Vad är "String format" i Java?

"String format" är som en magisk trollformel i Java, och den låter oss skapa strukturerade textsträngar med dynamiska variabler. Istället för att bygga texten manuellt, kan vi använda speciella platshållare i formatmönster, och sedan fylla i dessa platshållare med riktiga värden vid körningstid. Det är coolt, för det ger oss en flexibel och dynamisk textbehandling!

## Användning av Formatmönster

Vi skapar våra formatmönster med speciella tecken som representerar platshållare för variabler. Ett vanligt exempel är "%s", som används för att ersätta med en sträng. Kolla här:

```java
String name = "Alice"; // Who the f*ck is Alice?
String formattedString = String.format("Hej, mitt namn är %s.", name);
System.out.println(formattedString);

System.out.println();

String name = "Luka"; // Detta är en hänvisning till en sång av Suzanne Vega :)
String floor ="andra";
String song = String.format("My name is %s, I live on the %s floor", name, floor);
System.out.println(song);
```

Resultatet blir:

```
Hej, mitt name is Alice.

My name is Luka, I live on the other floor
```

## Användning av Specifikatorer

Det finns massor av olika specifikatorer för olika typer av variabler. Till exempel:

- "%d" för heltal (int).
- "%f" för flyttal (float eller double).
- "%c" för ett tecken (char).
- "%b" för en boolean (true eller false).
- "%s" för en sträng (String).

Kolla in det här exemplet:

```java
int age = 30;
double height = 1.75;
char gender = 'M';
boolean isStudent = true;

String formattedInfo = String.format("Ålder: %d, Längd: %.2f m, Kön: %c, Student: %b"
                                    , age, height, gender, isStudent);

System.out.println(formattedInfo);
```

Resultatet blir:

```
Age: 30, Length: 1.75 m, Gender: M, Student: true
```

## Anpassningsbarhet med "String format"

Med "String format" kan vi skapa superanpassningsbar text som passar olika språk och regioner. Genom att ändra formatmönster och ersättningsvärden dynamiskt kan vi göra texten ännu mer tilltalande för våra användare och skapa en personlig touch i våra Java-applikationer. Hur coolt är inte det?

## Exempelkod - Användning av "String format" för Valuta

Vi kan använda "String format" för att formatera belopp till olika valutor. Kolla in detta:

```java
import java.util.Locale;
import java.util.Currency;

public class CurrencyFormatter {
    public static void main(String[] args) {
        double amount = 1000.50;
        Locale swedishLocale = new Locale("sv", "SE");
        Currency swedishCurrency = Currency.getInstance(swedishLocale);

        String formattedAmount = String.format("%,.2f %s"
                        , amount, swedishCurrency.getSymbol(swedishLocale));
        System.out.println("Belopp i svensk valuta: " + formattedAmount);
    }
}
```

Resultatet blir:

```
Amount i swedish currency: 1 000,50 kr
```

## Slutsats

Visst är  "String format" coolt?. Det är så grymt att kunna skapa strukturerade och dynamiska textsträngar med detta verktyg. Genom att använda formatmönster och specifikatorer kan vi göra textbehandlingen roligare och mer engagerande för våra användare. Så var kreativ och låt din Java-kod glänsa med "String format" och sprid glädje och effektivitet i dina applikationer!

## Funktioner

| Funktion   | Beskrivning                                               | Exempel                                | Resultat                |
| -----------| -------------------------------------------------------- | -------------------------------------- | ----------------------- |
| String.format(String format, Object... args) | Skapar en formatterad sträng baserat på angivet format och variabler | `String name = "Alice";`<br>`int age = 30;`<br>`String formattedString = String.format("Hej, mitt namn är %s och jag är %d år gammal.", name, age);`<br>`System.out.println(formattedString);` | `Hej, mitt name is Alice och jag is 30 year old.` |
| %s         | Specifikator för att ersätta med en sträng               | `String name = "Alice";`<br>`String greeting = String.format("Hej, %s!", name);`<br>`System.out.println(greeting);` | `Hej, Alice!` |
| %d         | Specifikator för att ersätta med ett heltal             | `int apples = 5;`<br>`String message = String.format("Jag har %d äpplen.", apples);`<br>`System.out.println(message);` | `Jag has 5 apples.` |
| %f         | Specifikator för att ersätta med ett flyttal             | `double price = 19.99;`<br>`String formattedPrice = String.format("Priset är %.2f kr.", price);`<br>`System.out.println(formattedPrice);` | `Price is 19.99 kr.` |
| %c         | Specifikator för att ersätta med ett tecken               | `char grade = 'A';`<br>`String message = String.format("Ditt betyg är: %c", grade);`<br>`System.out.println(message);` | `Ditt grade is: A` |
| %b         | Specifikator för att ersätta med en boolean (true eller false) | `boolean isSunny = true;`<br>`String weather = String.format("Är det soligt idag? %b", isSunny);`<br>`System.out.println(weather);` | `Is it soligt today? true` |
| %n         | Ny rad specifikator (ersätter med ett radbrytning)         | `String multiLine = String.format("Första raden.%nAndra raden.");`<br>`System.out.println(multiLine);` | `First row.`<br>`Other row.` |
| %%         | Escapar procenttecken så att det visas som det är          | `double discount = 0.25;`<br>`String message = String.format("Rabatt: %.0f%%", discount * 100);`<br>`System.out.println(message);` | `Discount: 25%` |

`String.format` ger dig möjlighet att skapa strängar med variabler på ett flexibelt och lättläst sätt, vilket är användbart när du vill presentera information på ett dynamiskt sätt! ;)

## Obligatorisk dad joke:

Varför älskar Java-utvecklare "String format" så mycket?

För att de vet att "String" och "format" tillsammans kan skapa fantastiska strängar! 😄
