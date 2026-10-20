---
title: Rekursiva loopar
author: Marcus Ackre Medina
parent: Loopar
nav_order: 70
---
# Rekursiva loopar

Nu ska vi utforska Magin i Rekursion!

## Introduktion

Välkommen till världen av rekursion! Det är en spännande teknik inom programmering där en funktion kallar sig själv för att lösa problem genom att bryta ner dem i mindre deluppgifter. I den här övningen kommer vi att dyka in i rekursionens förtrollande värld och utforska hur det kan användas för att beräkna det berömda Fibonacci-talet. Vi kommer att titta på en rekursiv funktion som kan lösa detta matematiska mysterium och förklara flödet steg för steg. Låt oss upptäcka skönheten i rekursion tillsammans!

## TL;DR

Rekursion är en teknik där en funktion anropar sig själv för att lösa problem. I denna övning tittar vi på hur man kan använda rekursion för att beräkna Fibonacci-talet. Vi utforskar hur funktionen beräknar de olika delvärdena genom flera anrop och slutligen returnerar det önskade Fibonacci-talet.

## När du läst detta ska du kunna

- Förstå vad rekursion är och hur den fungerar inom programmering.
- Tillämpa rekursion för att beräkna Fibonacci-talet.
- Förklara steg för steg hur rekursionsfunktionen evalueras för att få det slutgiltiga resultatet.

## Rekursion och Fibonacci-talet

Rekursion är som magi - en programmeringsteknik där en funktion kan kalla på sig själv för att lösa problem på ett elegant sätt. Ett klassiskt exempel på rekursion är beräkningen av det n:te Fibonacci-talet. Låt oss utforska hur det fungerar!

Fibonacci-talen bildar en sekvens där varje tal är summan av de två föregående talen. Det kan uttryckas som:

F(n) = F(n-1) + F(n-2)

Låt oss titta på en rekursiv funktion som beräknar Fibonacci-talet:

```java
int Fibonacci(int n) {
    if (n <= 1)
        return n;
    else
        return Fibonacci(n - 1) + Fibonacci(n - 2);
}
```

## Steg-för-steg genom funktionen

För att förstå hur rekursionsfunktionen beräknar Fibonacci-talet, låt oss titta på ett exempel med n = 6:

1. Funktionen anropas med värdet 6.
2. Eftersom 6 inte är mindre än eller lika med 1, går vi vidare till else-blocket.
3. Funktionen anropar sig själv två gånger med de två föregående talen i Fibonacci-sekvensen, det vill säga `Fibonacci(6 - 1)` och `Fibonacci(6 - 2)`.
4. Nu fortsätter vi att evaluera dessa anrop separat.
5. Första anropet `Fibonacci(6 - 1)` utvärderas till `Fibonacci(5)`.
6. För att beräkna `Fibonacci(5)` måste vi fortsätta att anropa metoden med mindre värden tills vi når basfallet.
7. Detta resulterar i en serie anrop `Fibonacci(4)`, `Fibonacci(3)`, `Fibonacci(2)`, och `Fibonacci(1)`.
8. När vi når basfallet `Fibonacci(1)` returneras värdet 1.
9. Därefter fortsätter vi att evaluera anropen på vägen tillbaka. `Fibonacci(2)` returneras också med värdet 1.
10. Nu kan vi beräkna `Fibonacci(3)` genom att addera `Fibonacci(2)` och `Fibonacci(1)`, vilket ger 2.
11. Vi fortsätter att evaluera anropen och beräkna värdena för `Fibonacci(4)` och `Fibonacci(5)`.
12. Slutligen, när vi har beräknat `Fibonacci(6)` genom att addera `Fibonacci(5)` och `Fibonacci(4)`, returneras värdet 8.

Så resultatet av att anropa `Fibonacci(6)` är 8 enligt definitionen av Fibonacci-sekvensen.

## Rekursion i Java - Utforska Kreativiteten

Rekursion är en kraftfull teknik som låter oss lösa komplexa problem genom att bryta ner dem i mindre delar. I Java kan vi använda rekursion för att skapa eleganta och effektiva lösningar. Ta en titt på exemplet nedan som använder rekursion för att beräkna summan av heltal från 1 till ett givet tal `n`:

```java
public class RecursionExample {
    public static void main(String[] args) {

        int result = summarise(5);
        System.out.println("Summan är: " + result);
    }

    public static int summarise(int n) {
        if (n == 1) {
            return 1;
        } else {
            return n + summarise(n - 1);
        }
    }
}
```

I det här enkla exemplet använder vi en rekursiv funktion `summarise` för att beräkna summan av alla heltal från 1 till det givna talet `n`. Funktionen anropar sig själv med ett minskande värde tills den når basfallet då `n` är 1. Sedan börjar den returnera värden på vägen tillbaka och summerar dem för att få det slutliga resultatet. Detta ger oss summan av alla heltal från 1 till 5, vilket är 15.

Rekursion kan vara lite knepigt i början, men med övning och förståelse för hur det fungerar kan du upptäcka nya möjligheter att skapa elegant kod och lösa komplexa problem. Utforska rekursionens kreativa potential och låt din programmeringsfantasi flöda!

## Inspirerande Filmtips

För att fortsätta inspireras av kreativitet och fantasifulla idéer, varför inte titta på några filmer som bjuder på oväntade vändningar och spännande äventyr? Här är några filmtips som kan kittla din fantasi:

- [Source Code](https

://www.imdb.com/title/tt0945513/)
- [Happy Death Day](https://www.imdb.com/title/tt5308322/)
- [Happy Death Day 2U](https://www.imdb.com/title/tt8155288/)
- [Groundhog Day](https://www.imdb.com/title/tt0107048/)
- [Edge of Tomorrow](https://www.imdb.com/title/tt1631867/)

## Obligatorisk dad-joke

Varför gillar programmerare att använda rekursion i skämt?

För att förstå rekursion i skämt måste du först förstå rekursion i skämt. Ha det skoj med programmering och fortsätt skapa magi!
