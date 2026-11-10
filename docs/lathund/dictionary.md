---
title: "Lathund: Dictionary (Map och HashMap)"
author: Marcus Ackre Medina
description: "Map och HashMap i Java: nyckel-värde-par, sök med nyckel, loopa och varför Java inte kallar det Dictionary."
parent: Lathund
nav_order: 74
---
# Lathund: Dictionary (Map och HashMap)

Det som ofta kallas dictionary i andra språk heter `Map` i Java. `Map` är gränssnittet som beskriver nyckel-värde-par, och `HashMap` är den vanligaste implementationen. Du skriver variabeln som `Map` och skapar den som `HashMap`. Java har också en gammal klass som heter `Dictionary`, men den är föråldrad och används inte. Använd `Map`.

Läs mer: [Datastrukturer](../data-structures/index.md).

## Snabbfakta

| Egenskap | Värde |
|---|---|
| Typ | `Map<K, V>` (gränssnitt). Skapas som `HashMap<K, V>` |
| Nycklar | Unika. En nyckel kan bara finnas en gång |
| Värden | Kan vara dubbletter |
| Ordning | Ingen garanterad ordning i `HashMap` |
| Null | En nyckel och flera värden får vara `null` i `HashMap` |
| Import | `java.util.HashMap`, `java.util.Map` |

## Operationer

Exemplen utgår från `Map<String, Integer> skattkoder = new HashMap<>();` där den innehåller `Guld` med värdet `1000`.

| Operation | Betydelse | Exempel | Resultat |
|---|---|---|---|
| Lägg till eller uppdatera | `put(nyckel, värde)` | `skattkoder.put("Guld", 1000);` | Paret finns i mappen |
| Hämta | `get(nyckel)`, `null` om nyckeln saknas | `skattkoder.get("Guld")` | `1000` |
| Hämta med standard | `getOrDefault(nyckel, standard)` | `skattkoder.getOrDefault("Silver", 0)` | `0` |
| Finns nyckeln | `containsKey(nyckel)` | `skattkoder.containsKey("Guld")` | `true` |
| Ta bort | `remove(nyckel)` | `skattkoder.remove("Guld");` | Tar bort paret |
| Antal par | `size()` | `skattkoder.size()` | `1` |
| Alla nycklar | `keySet()` | `skattkoder.keySet()` | `[Guld]` |
| Alla värden | `values()` | `skattkoder.values()` | `[1000]` |
| Tom | `isEmpty()` | `skattkoder.isEmpty()` | `false` |

Samma sak i ett körbart program:

```java
import java.util.HashMap;
import java.util.Map;

public class MapExempel {
    public static void main(String[] args) {
        // Skapar en mapp som kopplar en kod till ett värde
        Map<String, Integer> skattkoder = new HashMap<>();

        skattkoder.put("Guld", 1000);
        skattkoder.put("Silver", 500);

        // get returnerar null om nyckeln saknas, så vi kontrollerar först
        if (skattkoder.containsKey("Brons")) {
            System.out.println(skattkoder.get("Brons"));
        } else {
            System.out.println("Brons finns inte");
        }

        // Loopar genom alla nyckel-värde-par
        for (Map.Entry<String, Integer> par : skattkoder.entrySet()) {
            System.out.println(par.getKey() + ": " + par.getValue());
        }
    }
}
```

## Jämförelser

### Tre implementationer av Map

Alla tre implementerar `Map`. De skiljer sig i ordningen som elementen kommer i när du loopar.

<details>
<summary>HashMap: ingen ordning</summary>

```java
Map<String, Integer> kod = new HashMap<>();
```

Snabbast. Ordningen går inte att förutsäga. Det är oftast det du vill ha.

</details>

<details>
<summary>LinkedHashMap: i den ordning du lade in dem</summary>

```java
Map<String, Integer> kod = new LinkedHashMap<>();
```

Använd när du vill att utskriften ska följa insättningsordningen.

</details>

<details>
<summary>TreeMap: sorterad på nyckeln</summary>

```java
Map<String, Integer> kod = new TreeMap<>();
```

Använd när du vill ha nycklarna sorterade. Nycklarna måste gå att jämföra.

</details>

## Vanliga misstag

- `get` returnerar `null` när nyckeln saknas. Om du skriver `int värde = skattkoder.get("Brons");` kastar Java `NullPointerException` när den packar upp värdet. Använd `getOrDefault` eller kontrollera med `containsKey`.
- Att lägga till en nyckel som redan finns skriver över det gamla värdet. Det kastar inget fel.
- Ordningen i en `HashMap` är inte garanterad. Förvänta dig inte samma ordning två gånger.
- Egna klasser som nycklar behöver `equals` och `hashCode`. En `record` får dem automatiskt.

## Terminologi

| Term | Betydelse |
|---|---|
| Map | Gränssnitt för nyckel-värde-par. Kallas dictionary i många andra språk |
| HashMap | Implementation av `Map` som använder hashning för snabb sökning |
| Nyckel | Värdet du söker med, till exempel `"Guld"` |
| Värde | Det som är kopplat till nyckeln |
| Par (entry) | En nyckel tillsammans med sitt värde, `Map.Entry` |
| Hashning | Att räkna fram ett tal ur nyckeln så att sökningen blir snabb |
| Generics (`<K, V>`) | Anger typen för nycklarna (K) och värdena (V) |
