---
title: Array övningar
author: Marcus Ackre Medina
parent: Datastrukturer
nav_order: 10
has_children: true
---
# Array övningar

Här finns några övningar för att träna på att använda arrayer i Java.

## 1. Skapa en array

Skapa en array med namnet `numbers` som innehåller följande tal: 1, 2, 3, 4, 5.

<details><summary markdown="span">Lösning</summary>

```java
int[] numbers = {1, 2, 3, 4, 5};
```

</details>

## 2. Tilldela värden till en array

Skapa en array med namnet `fruits` som kan hålla 3 fruktnamn. Tilldela värdena "äpple", "banan" och "apelsin" till arrayen.

<details><summary markdown="span">Lösning</summary>

```java
String[] fruits = {"äpple", "banan", "apelsin"};
```

</details>

## 3. Hämta värden från en array

Använd indexering för att hämta det andra värdet från arrayen `numbers`.
int andraTalet = numbers[1];

## 4. Uppdatera värden i en array

Uppdatera det första värdet i arrayen `fruits` till "päron".

<details><summary markdown="span">Lösning</summary>

```java
fruits[0] = "päron";
```

</details>

## 5. Loopa igenom en array

Använd en `for`-loop för att skriva ut varje frukt i arrayen `fruits`.

<details><summary markdown="span">Lösning</summary>

```java
for (int i = 0; i < fruits.length; i++) {
    System.out.println(fruits[i]);
}
```

</details>

## 6. Array av objekt

Skapa en array med namnet `characters` som kan hålla objekt av typen `Character`. Skapa två `Character`-objekt med namnen "Iron Man" och "Captain America" och placera dem i arrayen.

<details><summary markdown="span">Lösning</summary>

```java
Character[] characters = new Character[2];
characters[0] = new Character("Iron Man");
characters[1] = new Character("Captain America");
```

</details>

## 7. Tvådimensionell array

Skapa en tvådimensionell array med namnet `matrix` som har 3 rader och 3 kolumner. Fyll arrayen med värdena 1, 2, 3, 4, 5, 6, 7, 8, 9.

<details><summary markdown="span">Lösning</summary>

```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}};
```

</details>

## 8. Sök efter ett värde i en array

Skriv en metod med namnet `containsValue` som tar emot en array av heltal och ett heltal att söka efter. Metoden ska returnera `true` om värdet finns i arrayen, annars `false`.

<details><summary markdown="span">Lösning</summary>

```java
public static boolean containsValue(int[] array, int value) {
    for (int i = 0; i < array.length; i++) {
        if (array[i] == value) {
            return true;
        }
    }
    return false;
}
```

</details>

## 9. Sortera en array

Skriv en metod med namnet `sortArray` som tar emot en array av heltal och sorterar den i stigande ordning.

<details><summary markdown="span">Lösning</summary>

```java
public static void sortArray(int[] array) {
    Arrays.sort(array);
}
```

</details>

## 10. Summera värden i en array

Skriv en metod med namnet `sumArray` som tar emot en array av heltal och returnerar summan av alla värden i arrayen.

<details><summary markdown="span">Lösning</summary>

```java
public static int sumArray(int[] array) {
    int sum = 0;
    sum += array[i];
    return sum;
}
```

</details>

Lycka till med övningarna!
