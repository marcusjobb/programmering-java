---
title: Else if
author: Marcus Ackre Medina
parent: If
nav_order: 20
---
# Else if

## Introduktion I Detta avsnitt kommer vi att utforska den viktiga
programmeringskonstruktionen "Else if" i Java. Vi kommer att upptäcka hur denna
konstruktion erbjuder flexibilitet och tydlighet när det gäller att hantera
olika villkor och beslut. "Else if" är användbart i olika situationer där vi
behöver göra flera olika val baserat på olika förutsättningar.

## Vad är Else if?

"Else if" är en del av det så kallade "if-else" uttalandet i Java. Det låter oss skapa flera villkor som utvärderas i ordning, och om inget av de tidigare villkoren är sanna, kontrolleras ytterligare villkor. Om något av de senare villkoren är sant, exekveras den tillhörande kodblocket.

## Fördelar

Användningen av "Else if" ger flera fördelar inom programmering:

1. **Betygsberäkning**: Genom att använda "Else if" kan vi enkelt tilldela olika
   betyg baserat på poängintervall, vilket gör det möjligt att effektivt hantera
   en elevs prestation.

2. **Validering**: "Else if" ger oss möjlighet att validera olika typer av data
eller användarinput och vidta olika åtgärder baserat på innehållet.

3. **Menyval**: Det blir enkelt att skapa ett menyvalsystem där olika
handlingar kan utföras beroende på användarens val.

4. **Datum- och tidshantering**: Genom att använda "Else if" kan vi hantera
olika tidsrelaterade scenarier och utföra olika åtgärder beroende på tiden på
dygnet.

## Begränsningar

Även om "Else if" ger oss flexibilitet, kan överdriven användning av denna konstruktion leda till komplex kod. Det är viktigt att vara medveten om att när antalet "Else if" uttalanden ökar, blir det svårare att underhålla och förstå koden. Ibland kan det vara lämpligare att använda andra konstruktioner, som "switch" uttalande, för att hantera större menyval.

## Användningsområden

Låt oss titta på några exempel där "Else if" kan tillämpas:

1. **Betygsberäkning**: Se exempelkoden i avsnittet nedan för att förstå hur vi
kan tilldela betyg baserat på elevens poäng.

2. **Validering**: I exemplet nedan kan vi validera åldersinmatning och reagera
på olika åldersintervall.

3. **Menyval**: Visa saldo, gör insättningar eller uttag - allt är möjligt med
"Else if" som hanterar användarens menyval.

4. **Datum- och tidshantering**: Hälsa användare med lämpliga hälsningar
baserat på tiden på dygnet, som visas i kodexemplet nedan.

## Exempelkod - Else if i en berättelse

### Betygsberäkning

```java
int score = 75;
if (score >= 90) {
    System.out.println("A");
} else if (score >= 80) {
    System.out.println("B");
} else if (score >= 70) {
    System.out.println("C");
} else if (score >= 60) {
    System.out.println("D");
} else {
    System.out.println("F");
}
```

I denna kodexempel berättar vi historien om hur vi tilldelar betyg till en elev baserat på deras poäng.

### Validering

```java
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.println("Vänligen ange din ålder:");
        int age = scanner.nextInt();

        if (age < 0) {
            System.out.println("Åldern kan inte vara negativ.");
        } else if (age < 3) {
            System.out.println("Barnrumpa, du är för söt!");
        } else if (age < 18) {
            System.out.println("Ung och full av energi!");
        } else if (age < 40) {
            System.out.println("Medelålders och i sin bästa form!");
        } else if (age < 60) {
            System.out.println("Gamling, men fortfarande aktiv!");
        } else if (age < 100) {
            System.out.println("Jisses, du är gammal!");
        } else {
            System.out.println("Du är uråldrig! Respekt!");
        }

        scanner.close();
    }
}
```

I detta kodexempel berättar vi historien om hur vi validerar åldersinmatning och ger passande meddelanden beroende på åldersintervall.

### Menyval

```java
System.out.println("Välj ett alternativ:");
System.out.println("1. Visa saldo");
System.out.println("2. Gör en insättning");
System.out.println("3. Gör ett uttag");
int choice = Integer.parseInt(System.console().readLine());
if (choice == 1) {
    // Visa saldo
} else if (choice == 2) {
    // Gör en insättning
} else if (choice == 3) {
    // Gör ett uttag
} else {
    System.out.println("Ogiltigt val");
}
```

I detta kodexempel berättar vi historien om hur vi hanterar användarens menyval och utför olika åtgärder baserat på deras val.

### Datum- och tidshantering

```java
import java.time.LocalTime;

LocalTime nu = LocalTime.now();
if (nu.getHour() < 12) {
    System.out.println("God morgon!");
} else if (nu.getHour() < 18) {
    System.out.println("God eftermiddag!");
} else {
    System.out.println("God kväll!");
}
```

I detta kodexempel berättar vi historien om hur vi hanterar aktuell tid och hälsar användare med lämpliga hälsningar baserat på tiden på dygnet.

## Termer

Här är en lista på termer som används i artikeln:

| Term       | Förklaring                                      |
| ---------- | ---------------------------------------------- |
| Else if    | En programmeringskonstruktion som används för att utvärdera flera villkor sekventiellt. Om inget av de tidigare villkoren är sant, kontrolleras ytterligare villkor. Om något av de senare villkoren är sant, exekveras den tillhörande kodblocket.       |
| Kodexempel | Illustrationer av kod som visar användningen av "Else if" i olika scenarier.          |
| Validering | Processen att kontrollera data eller input för att säkerställa att det uppfyller fördefinierade villkor eller kriterier.        |
| Menyval    | En uppsättning alternativ som användaren kan välja mellan.        |

## Slutsats

Genom att använda "Else if" i Java får vi tillgång till en kraftfull konstruktion för att hantera flera olika beslutspunkter. Detta erbjuder flexibilitet och tydlighet i koden. Men vi bör vara medvetna om att överdriven användning av "Else if" kan leda till komplexitet och svårighet att underhålla koden. Genom att använda "Else if" på ett balanserat sätt kan vi skapa effektiva och lättförståeliga program som uppfyller våra behov.

## TL;DR

I Detta avsnitt har vi utforskat "Else if" i Java, en viktig konstruktion som erbjuder flexibilitet och tydlighet för hantering av olika villkor och beslut. "Else if" kan användas för betygsberäkning, validering, menyval och datum- och tidshantering. Genom att använda "Else if" på ett balanserat sätt kan vi skapa effektiva och lättförståeliga program som uppfyller våra behov.

## Obligatorisk dad-joke:

Varför gillar programmerare att använda Else if?

För att de har så många val i livet och villkorlig kärlek är bara en av dem! 😄
