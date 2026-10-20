---
title: Public
grand_parent: Objektorienterad programmering (OOP)
author: Marcus Ackre Medina
parent: Åtkomstmoderator
nav_order: 30
---
# Public

Öppenheten som Skapar Samarbete!

## Introduktion

I den här övningen kommer vi att utforska "public", en accessmodifier i Java som öppnar dörrarna för samarbete mellan klasser. Public tillåter oss att göra en klass, metod eller egenskap tillgänglig för alla klasser, vilket är särskilt användbart när vi vill dela kod mellan olika projekt. Låt oss dyka in i detaljerna om hur "public" fungerar och dess fördelar och begränsningar.

## TL;DR

I den här övningen har vi lärt oss om "public" i Java, en accessmodifier som skapar öppenhet för klasser, metoder och egenskaper att vara tillgängliga för alla. Detta främjar samarbete och kodåteranvändning mellan olika delar av våra projekt. Medan "public" är en kraftfull funktion, bör vi vara medvetna om att det också medför några överväganden när det gäller säkerhet och kodorganisation.

## När du läst detta ska du kunna

- Förstå och förklara vad "public" är och dess relevans inom Java-programmering.
- Diskutera fördelar och begränsningar med att använda "public".
- Förstå skillnaden mellan användningen av "public" och getters/setters.

## Vad är "public"?

I Java är "public" en accessmodifier som gör en klass, metod eller egenskap tillgänglig för alla andra klasser. Det innebär att om en klass deklareras som "public", kan den användas och åberopas från andra delar av koden och från andra projekt utan hinder. Detta främjar samarbete och kodåteranvändning, vilket kan bidra till att skapa mer effektiva och välstrukturerade program.

## Fördelar

Det finns flera fördelar med att använda "public" i Java:

1. **Kodåteranvändning:** Genom att göra klasser, metoder och egenskaper "public", kan vi enkelt dela kod mellan olika klasser och projekt. Detta sparar tid och möjliggör en mer strömlinjeformad utvecklingsprocess.

2. **Samarbete mellan klasser:** När klasser är "public" kan de enkelt samarbeta med varandra genom att använda varandras funktioner och egenskaper. Detta underlättar skapandet av komplexa program med modulär design.

3. **Enkel åtkomst:** "Public" gör det enkelt för externa klasser att använda och interagera med den deklarerade klassen eller metoden. Detta skapar en öppen miljö för utveckling och innovation.

## Begränsningar

Det finns också några viktiga begränsningar och överväganden att tänka på när du använder "public":

1. **Säkerhet:** När en klass eller metod görs "public", blir den tillgänglig för alla, inklusive tredjepartsprogram. Detta kan potentiellt utgöra en säkerhetsrisk om vissa delar av koden inte ska vara tillgängliga för externa användare.

2. **Kodunderhåll:** Eftersom "public" tillåter extern åtkomst, kan ändringar i en "public" metod eller egenskap påverka andra delar av koden. Detta kräver noggrannhet och testning vid uppdateringar för att undvika oväntade buggar.

## Getters och Setters?

En annan teknik för att möjliggöra åtkomst till klassens variabler är genom att använda "getters" och "setters". Dessa är metoder som låter oss hämta (get) eller sätta (set) värden för privata variabler.

| Namn | Fördel | Nackdel |
| --- | --- | --- |
| Getter | Du kan göra mer än bara returnera en variabel. Till exempel kan du validera värdet innan du returnerar det, eller beräkna det baserat på andra värden i klassen. | Det kräver några extra rader kod att implementera en getter. |
| Setter | Du kan göra mer än bara sätta en variabel. Till exempel kan du validera värdet innan du tilldelar det, eller utföra andra åtgärder baserat på det nya värdet. Om värdet inte är lämpligt kan du också kasta ett felmeddelande eller vägra att spara värdet. | Precis som för getters, kräver setters några extra rader kod att implementera. |
| Public | Det är enklare och snabbare att använda publika variabler, eftersom de kan nås direkt. | Det begränsar möjligheterna att validera eller behandla datan vid åtkomst eller tilldelning.

## Exempel

Här är några exempel på getters och setters för en klass som representerar en persons ålder:

```java
// Setter som inte accepterar negativa tal
public void setAge(int age) {
    if (age < 0) {
        throw new IllegalArgumentException("Age cannot be negative");
    }
    this.age = age;
}

// Getter som returnerar åldern på en person baserat på ett annat värde (Date)
public int getAge(Date currentDate) {
    return currentDate.getYear() - this.birthDate.getYear();
}
```

## Summan av kardemumman

"Public" är en kraftfull åtkomstmodifikator som skapar öppenhet för klasser, metoder och egenskaper att vara tillgängliga för alla. Detta främjar samarbete och kodåteranvändning mellan olika delar av våra projekt. När vi använder "public" bör vi dock vara medvetna om säkerhetsaspekter och kodunderhåll för att säkerställa en stabil och säker programvara. Användningen av getters och setters ger oss mer kontroll över hur data hanteras och kan vara fördelaktig i vissa situationer. Med detta kunskapsrika förhållningssätt kan vi skapa välstrukturerade och samarbetande Java-program! Happy coding! 😊
