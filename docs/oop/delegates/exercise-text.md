---
title: Övning - Textbehandling
grand_parent: Objektorienterad programmering (OOP)
author: Marcus Ackre Medina
parent: Delegater
nav_order: 20
---
# Övning - Textbehandling

I denna övning ska vi skapa en interaktiv "ordbehandlingsapp" i Java där användaren kan manipulera text på olika sätt. Vi kommer att använda delegater för att representera olika textmanipulationsmetoder och ge användaren möjlighet att välja och utföra önskad manipulation på en given textsträng.

## Instruktioner

1. Skapa ett Java-program med en klass kallad `TextManipulator`.
2. Definiera en delegat med namnet `TextManipulation`, som har en metod `manipulate` som tar en textsträng som parameter och returnerar en manipulerad textsträng.
3. Implementera metoder i `TextManipulator` för olika textmanipulationsfunktioner, till exempel:
   - `toUpperCase`: Konverterar hela texten till versaler.
   - `toLowerCase`: Konverterar hela texten till gemener.
   - `reverse`: Vänder ordningen på tecken i texten.
   - `removeSpaces`: Tar bort alla mellanslag från texten.
4. Skapa en metod i `TextManipulator` med namnet `performManipulation`, som tar en textsträng och en `TextManipulation`-delegat som parametrar. Denna metod ska använda delegaten för att manipulera den givna textsträngen och returnera resultatet.
5. Implementera en interaktiv användargränssnitt där användaren kan ange en textsträng och välja en manipulationsfunktion från en meny. Användaren ska sedan kunna se det manipulerade resultatet.

## Exempelkörning

```text
Välkommen till Text Manipulation-appen!

Ange en textsträng: Hello, World!

Välj en textmanipulation:
1. Konvertera till versaler
2. Konvertera till gemener
3. Vänd texten
4. Ta bort mellanslag
5. Avsluta

Ange ditt val (1/2/3/4/5): 2

Resultatet av textmanipulationen är: hello, world!

Vill du göra en annan textmanipulation? (Ja/Nej): Ja

Ange en textsträng: Programming is Fun!

Välj en textmanipulation:
1. Konvertera till versaler
2. Konvertera till gemener
3. Vänd texten
4. Ta bort mellanslag
5. Avsluta

Ange ditt val (1/2/3/4/5): 3

Resultatet av textmanipulationen är: !nuF si gnimmargorP

Vill du göra en annan textmanipulation? (Ja/Nej): Nej

Tack för att du använde Text Manipulation-appen!
```

## Tips

- För att implementera metoden `performManipulation`, använd delegaten som en vanlig metodanrop med hjälp av `manipulate`-metoden.
- Använd en loop för att fråga användaren om de vill göra fler textmanipulationer.
- Använd `Scanner`-klassen för att läsa in användarens input.

## Utmaning

Om du vill göra övningen mer avancerad, kan du lägga till fler textmanipulationsfunktioner och låta användaren kombinera flera manipulationssteg i en sekvens!

## Lösningsförslag

<summary><details><code>Här är lösningen</code></details></summary>

```java
import java.util.Scanner;

public class TextManipulator {
    // Definiera delegaten TextManipulation
    interface TextManipulation {
        String manipulate(String text);
    }

    // Metoder för olika textmanipulationsfunktioner
    public static String toUpperCase(String text) {
        return text.toUpperCase();
    }

    public static String toLowerCase(String text) {
        return text.toLowerCase();
    }

    public static String reverse(String text) {
        return new StringBuilder(text).reverse().toString();
    }

    public static String removeSpaces(String text) {
        return text.replaceAll("\\s+", "");
    }

    // Metod för att utföra textmanipulation baserat på vald delegat
    public static String performManipulation(String text, TextManipulation manipulation) {
        return manipulation.manipulate(text);
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        System.out.println("Välkommen till Text Manipulation-appen!\n");

        String inputText;
        do {
            System.out.print("Ange en textsträng: ");
            inputText = scanner.nextLine();

            System.out.println("\nVälj en textmanipulation:");
            System.out.println("1. Konvertera till versaler");
            System.out.println("2. Konvertera till gemener");
            System.out.println("3. Vänd texten");
            System.out.println("4. Ta bort mellanslag");
            System.out.println("5. Avsluta");

            System.out.print("\nAnge ditt val (1/2/3/4/5): ");
            int choice = Integer.parseInt(scanner.nextLine());

            String manipulatedText = "";
            switch (choice) {
                case 1:
                    manipulatedText = performManipulation(inputText, TextManipulator::toUpperCase);
                    break;
                case 2:
                    manipulatedText = performManipulation(inputText, TextManipulator::toLowerCase);
                    break;
                case 3:
                    manipulatedText = performManipulation(inputText, TextManipulator::reverse);
                    break;
                case 4:
                    manipulatedText = performManipulation(inputText, TextManipulator::removeSpaces);
                    break;
                case 5:
                    System.out.println("\nTack för att du använde Text Manipulation-appen!");
                    scanner.close();
                    return;
                default:
                    System.out.println("\nOgiltigt val. Försök igen.");
            }

            System.out.println("\nResultatet av textmanipulationen är: " + manipulatedText);
            System.out.print("\nVill du göra en annan textmanipulation? (Ja/Nej): ");
        } while (scanner.nextLine().equalsIgnoreCase("Ja"));

        System.out.println("\nTack för att du använde Text Manipulation-appen!");
        scanner.close();
    }
}
```
