---
title: Decimalformat
grand_parent: Variabler
author: Marcus Ackre Medina
parent: Stränghantering
nav_order: 40
---
# Decimalformat

## Introduktion

Nu ska vi titta på textformatering med hjälp av "DecimalFormat"!

Att få siffror och tal att se snygga och välorganiserade ut har aldrig varit så coolt som med DecimalFormat! Häng med mig när vi utforskar detta charmiga verktyg som kommer att ge din Java-kod en touch av elegans och stil!

## Förkunskaper

Innan vi börjar leka med decimaltal, är det viktigt att du förstår de olika numeriska datatyperna i Java. Om du inte redan har gjort det, se till att kolla in dessa dokument innan du fortsätter:

- [String](index.md)
- [Decimal](../decimal.md)
- [Double](../double.md)
- [Float](../float.md)

## Vad är DecimalFormat?

Innan vi dyker in i det roliga måste vi förstå vad DecimalFormat handlar om. I Java, när vi behöver visa tal i specifika format med antal decimaler, tusentalsavgränsare eller valutor, är DecimalFormat vårt hemliga vapen! 🗡️ Det tillåter oss att formatera numeriska värden på ett sätt som gör att de ser ut precis som vi vill ha dem, vilket ger våra applikationer en professionell och polerad touch.

```java
float price = 55.75;
double quantity = 3.14159265359;
Decimal distance = 55.75;
```

## TL;DR

DecimalFormat är en Java-klass som hjälper oss att formatera numeriska värden i önskat format, inklusive antal decimaler, tusentalsavgränsare och valutasymboler. Det ger oss kontroll över hur våra tal ska presenteras och gör vår kod mer elegant och användarvänlig! 🎉

## När du läst detta ska du kunna

- Förstå konceptet av DecimalFormat i Java.
- Använda olika formatmönster för att formatera tal.
- Skapa textrepresentationer av tal med önskad precision och stil.
- Använda DecimalFormat för att förbättra användarupplevelsen i Java-applikationer.

## Hur Använder Vi Det?

Det charmiga med DecimalFormat ligger i dess enkelhet. Genom att skapa en instans av DecimalFormat kan vi sedan använda olika formatmönster för att få våra tal att se precis ut som vi vill ha dem. Vi kan kontrollera antalet decimaler, använda tusentalsavgränsare och till och med lägga till valutasymboler!

Låt mig visa dig ett exempel:

```java
import java.text.DecimalFormat;

public class CharmingFormatting {
    public static void main(String[] args) {
        double price = 55.75;
        DecimalFormat formatter = new DecimalFormat("#,##0.00 kr");

        String formattedPrice = formatter.format(price);
        System.out.println("Produktpris: " + formattedPrice);
    }
}
```

Resultatet blir:

```text
Produktpris: 55,75 kr
```

Coolt, eller hur? :)

## Större exempel

Vi ska ta en kontrollrunda in i Millenium Falcon och kolla vad Han Solo i lagret. Han har en massa varor som han vill sälja, och han behöver hjälp med att formatera sina priser. Tänk på att det är viktigt att fixa fram krediter till Jabba innan han kommer och hälsar på, så vi måste se till att priserna är korrekta!

```java
import java.text.DecimalFormat;
import java.util.HashMap;
import java.util.Map;

public class HanSoloCargo {

    public static void main(String[] args) {

        float javaDebt = 55000.0f;

        // Han Solos last och priser i krediter
        Map<String, Double> cargo = new HashMap<>();
        cargo.put("Spice", 5000.0);
        cargo.put("Stöldgods (juveler)", 10000.0);
        cargo.put("Arkeologiska artefakter", 15000.0);
        cargo.put("Replikas av kända konstvärk", 20000.0);
        cargo.put("Olovlig teknologi", 25000.0);
        cargo.put("Vapen", 30000.0);

        // Beräkna totalt värde av lasten
        double totalValue = 0.0;
        for (Double value : cargo.values()) {
            totalValue += value;
        }

        // Formatera värden med tusentalsavgränsare och två decimaler
        DecimalFormat formatter = new DecimalFormat("#,##0.00");

        // Skriv ut rapporten
        System.out.println("Han Solos Last och Dess Värde");
        System.out.println("-----------------------------");
        for (Map.Entry<String, Double> entry : cargo.entrySet()) {
            String cargoName = entry.getKey();
            double cargoValue = entry.getValue();
            String formattedValue = formatter.format(cargoValue);
            System.out.println(cargoName + ": " + formattedValue + " krediter");
        }

        System.out.println("-----------------------------");
        String formattedTotalValue = formatter.format(totalValue);
        System.out.println("Totalt värde av lasten: " + formattedTotalValue + " krediter");
        System.out.println("-----------------------------");
        String formattedJavaDebt = formatter.format(javaDebt);
        System.out.println("Skuld till Java: " + formattedJavaDebt + " krediter");
        System.out.println("-----------------------------");
        String formattedProfit = formatter.format(totalValue - javaDebt);
        System.out.println("Vinst: " + formattedProfit + " krediter");
        System.out.println("-----------------------------");

    }
}
```

Resultatet blir:

```text
Han Solos Last och Dess Värde
-----------------------------
Spice: 5 000,00 krediter
Stöldgods (juveler): 10 000,00 krediter
Arkeologiska artefakter: 15 000,00 krediter
Replikas av kända konstvärk: 20 000,00 krediter
Olovlig teknologi: 25 000,00 krediter
Vapen: 30 000,00 krediter
-----------------------------
Totalt värde av lasten: 105 000,00 krediter
-----------------------------
Skuld till Java: 55 000,00 krediter
-----------------------------
Vinst: 50 000,00 krediter
-----------------------------
```

## Formatmönster och Sinnesro

Med DecimalFormat kan vi använda olika formatmönster för att uppnå exakt den formatering vi vill ha. Vi kan använda "#" för att representera siffror, och "," för att ange tusentalsavgränsare. Om vi inte vill ha några decimaler, lägger vi bara till "0" i formatet.

Till exempel:

- "###,###,##0.00" kommer att ge oss två decimaler och tusentalsavgränsare, som vi såg i exemplet ovan.
- "###,###" ger oss heltal med tusentalsavgränsare, utan några decimaler.
- "#0.##" kommer att ge oss upp till två decimaler, men om det inte finns några decimaler kommer de inte att visas.

## Enkelhet med Kreativitet!

Med DecimalFormat kan du vara så kreativ du vill! Du kan skapa anpassade format för tal och låta din kod utstråla både elegans och precision. Det charmiga med det hela är att det är så enkelt att använda och ändå så kraftfullt i resultatet!

## Funktioner

Absolut! Här är tabellen med exempel för DecimalFormat:

| Funktion   | Beskrivning                                               | Exempel                                | Resultat                |
| -----------| -------------------------------------------------------- | -------------------------------------- | ----------------------- |
| DecimalFormat(String pattern) | Skapar ett DecimalFormat-objekt med det angivna formatmönstret | `DecimalFormat the = new DecimalFormat("#,###.00");` | `#,###.00` |
| setMinimumFractionDigits(int minDigits) | Ställer in det minsta antalet decimaler för formattering | `the.setMinimumFractionDigits(2); System.out.println(the.format(1234.5));` | `1,234.50` |
| setMaximumFractionDigits(int maxDigits) | Ställer in det högsta antalet decimaler för formattering | `the.setMaximumFractionDigits(4); System.out.println(the.format(1234.56789));` | `1,234.5679` |
| setMinimumIntegerDigits(int minDigits) | Ställer in det minsta antalet siffror för formattering före decimaltecknet | `the.setMinimumIntegerDigits(3); System.out.println(the.format(12.345));` | `012.345` |
| setMaximumIntegerDigits(int maxDigits) | Ställer in det högsta antalet siffror för formattering före decimaltecknet | `the.setMaximumIntegerDigits(5); System.out.println(the.format(123456.789));` | `123,456.79` |
| setGroupingUsed(boolean useGrouping) | Aktiverar eller inaktiverar gruppering av siffror | `the.setGroupingUsed(false); System.out.println(the.format(123456.789));` | `123456.79` |
| setDecimalSeparatorAlwaysShown(boolean alwaysShown) | Anger om decimaltecknet alltid ska visas | `the.setDecimalSeparatorAlwaysShown(true); System.out.println(the.format(1234));` | `1,234.` |
| setParseBigDecimal(boolean newValue) | Anger om metoden `parse` ska returnera ett BigDecimal-objekt | `the.setParseBigDecimal(true); BigDecimal num = (BigDecimal) the.parse("1234.56789"); System.out.println(num);` | `1234.56789` |

DecimalFormat ger dig möjlighet att anpassa formatteringen av decimaltal på olika sätt, vilket är användbart när du vill visa siffror på ett specifikt och överskådligt sätt! ;)

## Slutsats

Så kära vänner, om ni vill ta er Java-kod till nästa nivå och ge era tal och siffror en touch av elegans, låt mig säga att DecimalFormat är nyckeln till framgång! Genom att använda formatmönster och kreativitet kan vi skapa vackra och välskötta textrepresentationer av tal, som imponerar på både användare och kollegor.

Så se till att utforska detta charmiga verktyg och låt din kod blomstra som aldrig förr! DecimalFormat kommer att ge dina numeriska värden en unik stil och göra din Java-kod till något alldeles extra!
