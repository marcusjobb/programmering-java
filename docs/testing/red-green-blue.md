---
title: Röd Grön Blå
author: Marcus Ackre Medina
parent: Testa din kod
nav_order: 20
---
# Röd Grön Blå

Red-Green-Blue (RGB) är en förkortning som används inom Testdriven Utveckling (TDD) för att beskriva den arbetsprocess som används vid implementeringen av tester och kod. RGB-metoden hjälper till att styra utvecklingscykeln och säkerställa att koden fungerar som förväntat innan nya funktioner eller förbättringar införs. Låt oss förklara varje steg, och sedan ge ett kodexempel för att förtydliga processen.

1. **Red**: I detta första steg skriver vi testet som beskriver den funktionalitet vi vill ha i vårt program. Testet kommer initialt att misslyckas eftersom den nödvändiga funktionaliteten inte är implementerad ännu. Röd symboliserar det misslyckade testet, och det är det första steget i RGB-metoden.

2. **Green**: I det här steget skriver vi den minimala koden som krävs för att få testet att passera. Syftet är att göra testet grönt, vilket betyder att testet lyckas och den önskade funktionaliteten är implementerad och fungerar som förväntat.

3. **Blue**: När vi har skrivit koden som passerar testet, är det dags att refaktorera koden. Här kan vi förbättra koden utan att ändra dess funktionalitet. Blue symboliserar stabilitet, och genom att refaktorera koden efter att ha fått testet grönt, kan vi säkerställa att vår kod är ren och välstrukturerad.

Låt oss nu illustrera RGB-processen med ett enkelt exempel i Java.

#### Exempel: Implementera en Adderingsfunktion med RGB

Vi vill implementera en adderingsfunktion som tar två heltal och returnerar deras summa.

##### Steg 1 - Red (Skriva testet)

Vi skriver testet för vår adderingsfunktion först. Detta test kommer att misslyckas eftersom funktionen inte är implementerad ännu:

```java
import static org.junit.jupiter.api.Assertions.assertEquals;
import org.junit.jupiter.api.Test;

public class CalculatorTest {
    @Test
    public void testAdd() {
        Calculator calculator = new Calculator();
        int result = calculator.add(2, 3);
        assertEquals(5, result);
    }
}
```

##### Steg 2 - Green (Implementera koden)

Nu skriver vi den nödvändiga koden för att få testet att passera:

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

Nu när vi kör testet igen, kommer det att passera eftersom vår adderingsfunktion returnerar rätt summa.

##### Steg 3 - Blue (Refaktorera koden)

Nu när vi har fått testet att passera, kan vi refaktorera koden för att förbättra dess kvalitet:

```java
public class Calculator {
    public int add(int a, int b) {
        // Bättre namngivning för variabler
        int sum = a + b;
        return sum;
    }
}
```

Genom att refaktorera koden kan vi göra den mer läsbar och lättförståelig.

Med detta RGB-exempel har vi framgångsrikt implementerat en adderingsfunktion med hjälp av Testdriven Utveckling (TDD). RGB-metoden hjälpte oss att säkerställa att vår kod var testad, fungerade korrekt och var välstrukturerad. Genom att följa detta mönster kan vi känna oss trygga i att vårt program fungerar som förväntat.

## Varför?

Jag vet, det låter hur knäppt som helst, men det är genialiskt faktiskt.

Då skriver först kod som kontrollerar dina förväntningar på koden, och sedan skriver du koden som uppfyller dessa förväntningar. Du kommer att skriva smartare och mindre mängd kod. Din kod kommer att fungera precis som förväntat och din kod kommer att vara lätt att förstå och underhålla. Win Win situation på många plan.

En annan fördel är att du med tiden kommer att skriva din kod "testsäkert" även om du inte ens har tester, för att du har vant dig vid att skriva kod som uppfyller specifika kriterier och när du planerar din kod kommer du att tänka direkt på dina kriterier innan du tänker på koden.

Som sagt, Win Win situation på många plan.

## Summan av Kardemumman

RGB är en metod som används inom Testdriven Utveckling (TDD) för att beskriva den arbetsprocess som används vid implementeringen av tester och kod. RGB-metoden hjälper till att styra utvecklingscykeln och säkerställa att koden fungerar som förväntat innan nya funktioner eller förbättringar införs. RGB står för Red-Green-Blue, och det är en förkortning som används för att beskriva de tre stegen i processen:
