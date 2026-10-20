---
title: Åtkomstmoderator
author: Marcus Ackre Medina
parent: Objektorienterad programmering (OOP)
nav_order: 50
has_children: true
---
# Åtkomstmoderator

Nu ska du få lära dig hur du kontrollerar åtkomsten till dina Klassmedlemmar!

## Introduktion

I Java spelar åtkomstmodifikatorer en viktig roll i att definiera hur vi kan komma åt och använda klassmedlemmar i våra program. Genom att använda åtkomstmodifikatorer kan vi bestämma vilka delar av en klass som ska vara synliga för andra klasser och vilka som ska vara privata för bara den aktuella klassen. Detta ger oss möjligheten att skapa robusta och säkra program genom att hantera åtkomsten till våra klassmedlemmar på ett kontrollerat sätt.

## TL;DR

I Detta avsnitt kommer vi att utforska de olika åtkomstmodifikatorerna i Java och hur de påverkar synligheten av klassmedlemmar.

## Översikt av Åtkomstmodifikatorer

Här är en översikt av de viktigaste åtkomstmodifikatorerna och deras betydelser:

1. **public**: Tillåter åtkomst från alla klasser. Synlighet över hela programmet.
2. **private**: Tillåter endast åtkomst från samma klass. Skyddar klassens interna detaljer.
3. **protected**: Tillåter åtkomst från samma klass och dess underklasser. Används för att dela data och funktionalitet med underklasser.
4. **(Ingen åtkomstmodifikator)** (package-private): Tillåter åtkomst inom samma paket. Ger en balans mellan synlighet och säkerhet.
5. **final**: Förhindrar ändring av en klassmedlem efter deklaration. Används för att skapa konstanta värden och förhindra över-ridning av metoder och ändring av variabler.
6. **static**: Tillåter åtkomst utan att skapa en instans av klassen. Används för att skapa metoder och variabler som tillhör klassen istället för instanser av klassen.
7. **abstract**: Saknar implementation och kräver att subklasser implementerar den. Används för att skapa abstrakta metoder och klasser.
8. **transient**: Förhindrar sparande vid serialisering. Används när vi inte vill spara ett visst attribut vid serialisering av ett objekt.
9. **volatile**: Förhindrar att en klassmedlem cachas av JVM. Används för att hantera trådsäkerhet.
10. **synchronized**: Används för att kontrollera trådåtkomst till en klassmedlem. Används för att hantera trådsäkerhet och förhindra att flera trådar ändrar en klassmedlem samtidigt.
11. **native**: Implementeras i en annan programmeringsspråk. Används när vi behöver använda en extern implementation för en metod.
12. **sealed**: Förhindrar att en klassmedlem ärver från andra klasser. Används för att skapa slutna klasser som inte kan ärvas.

## Exempel

Låt oss titta på ett exempel som visar hur vi kan använda åtkomstmodifikatorerna i Java:

```java
public class Person {
    public String name; // Tillgänglig från alla klasser
    private int age; // Endast tillgänglig från Person-klassen
    protected String address; // Tillgänglig från Person-klassen och dess underklasser
    String phoneNumber; // Endast tillgänglig inom samma paket som Person-klassen

    public void displayInfo() {
        System.out.println("Name: " + name + ", Age: " + age + ", Address: " + address + ", Phone Number: " + phoneNumber);
    }
}
```

I detta exempel har vi en klass `Person` med olika medlemmar som har olika åtkomstmodifikatorer. `name` är en publik medlem och är tillgänglig från alla klasser. `age` är privat och kan bara nås inom `Person`-klassen. `address` är skyddad och kan nås av `Person`-klassen och dess underklasser. `phoneNumber` har ingen åtkomstmodifikator och är därmed endast tillgänglig inom samma paket som `Person`-klassen.

## Slutsats

Åtkomstmodifikatorer ger oss möjligheten att styra hur våra klassmedlemmar kan nås av andra delar av vårt program. Genom att välja rätt åtkomstmodifikatorer kan vi skapa säkra och välstrukturerade program som främjar återanvändbarhet och underhållbarhet. Så använd åtkomstmodifikatorer klokt och skapa robusta Java-program som glänser med kontrollerad åtkomst till klassmedlemmar!
