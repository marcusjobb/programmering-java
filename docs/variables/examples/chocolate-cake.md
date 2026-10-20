---
title: Kladdkaka
author: Marcus Ackre Medina
parent: Variabler
nav_order: 20
---
# Kladdkaka

Vi ska göra en kladdkaka, vi gör detta genom att skapa variabler för varje ingrediens, sedan skapar vi en variabel för hela kladdkakan.

## Kod

Vi kommer att använda oss av `float` för att kunna använda decimaler, för att float är i jämförelse mot `double` mindre minneskrävande och vi behöver inte så många decimaler.

```java
class Main {
  public static void main(String[] args) {

    int count = 1; // 1 kladdkaka
    // Ingredienser
    float cocoa = 1.5f * count; // 1.5 dl kakao
    float sugar = 3 * count; // 3 dl socker
    float flour = 2.5f * count; // 2.5 dl mjöl
    float butter = 150 * count; // 150 gram smör
    float eggs = 2 * count; // 2 ägg
    float vanillaSugar = 1 * count; // 1 tsk vaniljsocker
    float bakingPowder = 2 * count; // 2 tsk bakpulver
    float salt = 1 * count; // 1 krm salt
    float bakingTime = 20; // 20 minuter i ugnen

    // Kladdkaka
    float stickyCake = cocoa + sugar + flour + butter + eggs + vanillaSugar + bakingPowder + salt;

    System.out.println("Kladdkaka (" + count + " stycken kladdkakor))");
    System.out.println("Ingredienser:");
    System.out.println("Kakao: " + cocoa + " dl");
    System.out.println("Socker: " + sugar + " dl");
    System.out.println("Mjöl: " + flour + " dl");
    System.out.println("Smör: " + butter + " gram");
    System.out.println("Ägg: " + eggs + " st");
    System.out.println("Vaniljsocker: " + vanillaSugar + " tsk");
    System.out.println("Bakpulver: " + bakingPowder + " tsk");
    System.out.println("Salt: " + salt + " krm");
    System.out.println("Totalt: " + stickyCake + " dl");
    System.out.println(); // Tomrad
    System.out.println("Blanda alla ingredienser i en bunke");
    System.out.println("Häll smeten i en smord form per kladdkaka");
    System.out.println("Grädda i ugnen i " + bakingTime + " minuter per kladdkaka");
    System.out.println("Låt svalna");
    System.out.println("Servera med grädde eller glass");
    System.out.println("Mumsa vilt!");
  }
}
```

## Resultat

```text
Kladdkaka (1 stycken kladdkakor))
Ingredienser:
Kakao: 1.5 dl
Socker: 3.0 dl
Mjöl: 2.5 dl
Smör: 150.0 gram
Ägg: 2.0 st
Vaniljsocker: 1.0 tsk
Bakpulver: 2.0 tsk
Salt: 1.0 krm
Totalt: 162.0 dl

Blanda alla ingredienser i en bunke
Häll smeten i en smord form per kladdkaka
Grädda i ugnen i 20.0 minuter per kladdkaka
Låt svalna
Servera med grädde eller glass
Mumsa vilt!
```

Som du ser i exemplet ovan så har vi skapat en variabel för varje ingrediens, sedan har vi skapat en variabel för hela kladdkakan. Vi har också skapat en variabel för hur lång tid det tar att grädda kladdkakan. Vi ger även möjligheten att skapa flera kladdkakor genom att ändra värdet på variabeln `count`. Om du vill göra den mindre söt ändrar du värdet på variabeln `sugar` till 2 dl istället för 3 dl. Du kan prova med att ändra i olika variabler och det kommer att ge dig olika resultat.

En annan lösning du skulle kunna använda en sådan här kod till är om du har ett amerikansk recept men vill ha ditt recept i deciliter istället för cups (1 cup (amerikansk) = 2.36 deciliter). Då kan du skapa en variabel för varje ingrediens göra beräkningen i variabeln, utan att ändra hur det skrivs ut.

## Summan av kardemumman

Variabler är bra för att hålla koll på värden, funktioner och objekt. På så sätt behöver vi inte hålla reda på allt i huvudet, vi kan skriva ner det och låta datorn hålla reda på det åt oss. Vi låter datorn räkna ut det till oss så vi inte behöver göra det själva.

Jag ska berätta en hemlighet för dig: Du behöver inte vara matte-expert för att vara programmerare, du behöver bara veta vilka ekvationer som används och hur ;), resten sköter variablerna åt dig.
