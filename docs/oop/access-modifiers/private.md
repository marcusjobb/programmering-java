---
title: Private
grand_parent: Objektorienterad programmering (OOP)
author: Marcus Ackre Medina
parent: Åtkomstmoderator
nav_order: 10
---
# Private

Håll Dina Hemligheter Säkra i Java!

## Introduktion

I Java är `private` en åtkomstmodifikator som används för att göra en klassmedlem endast tillgänglig inom den klass där den är deklarerad. Genom att använda `private` kan vi säkerställa att vissa delar av vår klass är dolda för andra klasser och bara kan användas internt i klassen. Detta ger oss en viktig princip inom objektorienterad programmering, känd som "inkapsling," som hjälper oss att skydda och hålla våra klasser organiserade och säkra.

## Beskrivning

Genom att deklarera en klassmedlem som `private` i Java begränsar vi dess synlighet till endast den klass där den är deklarerad. Det innebär att ingen annan klass kan komma åt eller ändra denna medlem direkt. Detta ger oss kontroll över hur vår klass interagerar med andra klasser och skyddar våra interna detaljer från obehörig åtkomst.

## Exempel

Låt oss ta ett exempel där vi använder `private` för att skydda egenskaper i en klass:

```java
public class Person {
    private String name;
    private int age;
}
```

I detta exempel har vi en klass som heter `Person`. Vi har två egenskaper, `name` och `age`, som är deklarerade som `private`. Detta innebär att `name` och `age` endast är tillgängliga inom `Person`-klassen. Ingen annan klass kan direkt få åtkomst till dessa egenskaper och ändra deras värden.

För att ge åtkomst till dessa privata egenskaper brukar vi använda s.k. "getter" och "setter" metoder, som är publika metoder i klassen som ger oss möjlighet att läsa och ändra på de privata egenskaperna på ett kontrollerat sätt.

Jaja det är ju bara ett exempel. Det får räcka som Dad-Joke för den här artikeln.

```text
 ___       _______   ___
 |   |     |   _   | |   |
 |.  |     |.  |   | |.  |
 |.  |___  |.  |   | |.  |___
 |:  1   | |:  1   | |:  1   |
 |::.. . | |::.. . | |::.. . |
 `-------' `-------' `-------'

```

## Slutsats

`private` är en viktig åtkomstmodifikator i Java som hjälper oss att skydda våra klassers integritet och hålla våra hemligheter säkra. Genom att använda `private` kan vi enkelt definiera interna detaljer i våra klasser och samtidigt erbjuda en kontrollerad åtkomst till dessa detaljer genom "getter" och "setter" metoder. Så nästa gång du skapar en klass, överväg att använda `private` för att hålla dina hemligheter säkra och implementera den viktiga principen om inkapsling i din Java-kod!
