---
title: Komposition över arv
author: Marcus Ackre Medina
parent: Objektorienterad programmering (OOP)
nav_order: 50
---
# Komposition över arv

## Vad är det för något?

Komposition över arv är ett designmönster inom objektorienterad programmering som förespråkar att "sammansättning" (komposition) bör användas istället för "arv" (inheritance) för att uppnå återanvändbarhet och flexibilitet i kod. Detta mönster är baserat på principen om att klasser bör sammansättas av andra klasser snarare än att ärva från dem.

## Varför är det viktigt?

Komposition över arv är ett viktigt koncept inom objektorienterad programmering eftersom det hjälper oss att skapa flexibla och återanvändbara klasser. Genom att använda komposition kan vi enkelt kombinera olika klasser för att skapa nya klasser med olika beteenden och egenskaper. Detta gör det möjligt för oss att skapa modulära och flexibla program som är lätta att underhålla och utöka.

## Fördelar

Komposition över arv erbjuder flera fördelar och används i olika situationer:

1. **Flexibilitet**: Genom att använda komposition kan vi enkelt kombinera olika klasser för att skapa nya klasser med olika beteenden och egenskaper. Detta gör det möjligt för oss att skapa modulära och flexibla program som är lätta att underhålla och utöka.

2. **Återanvändbarhet**: Genom att använda komposition kan vi återanvända befintlig kod och undvika att duplicera kod. Detta gör det möjligt för oss att skapa modulära och flexibla program som är lätta att underhålla och utöka.

3. **Moduläritet**: Genom att använda komposition kan vi skapa modulära program som är lätta att underhålla och utöka. Detta gör det möjligt för oss att skapa modulära och flexibla program som är lätta att underhålla och utöka.

4. **Minskad beroende**: Genom att använda komposition kan vi minska beroendet mellan klasser och undvika att duplicera kod. Detta gör det möjligt för oss att skapa modulära och flexibla program som är lätta att underhålla och utöka.

## Begränsningar

Komposition över arv har vissa begränsningar att vara medveten om:

1. **Ökad komplexitet**: Genom att använda komposition kan vi öka komplexiteten i vårt program. Detta kan göra det svårare att förstå och underhålla koden.

2. **Mer kod att skriva**: Genom att använda komposition kan vi behöva skriva mer kod för att uppnå samma resultat som med arv. Detta kan göra det svårare att förstå och underhålla koden.

## Enkel förklaring

Man skulle förenkla det hela med att säga att vi simulerar "arv av flera klasser" och undvika att duplicera kod. Detta gör det möjligt för oss att skapa modulära och flexibla program som är lätta att underhålla och utöka.

## Exempel 1

Känns det rörigt? Lugnt, vi kollar på ett exempel... Vi har faktiskt använt detta innan...

kolla koden nedan

```java
class Pet
{
    private String name;
    private int age;
    private String breed;

    public Pet(String name, int age, String breed)
    {
        this.name = name;
        this.age = age;
        this.breed = breed;
    }

    public String getName(){ return name; }
    public int getAge(){ return age; }
    public String getBreed(){ return breed; }
    public void setName(String name){ this.name = name; }
    public void setAge(int age){ this.age = age; }
    public void setBreed(String breed){ this.breed = breed; }
}
class Person
{
    private String name;
    private int age;

    public Person(String name, int age)
    {
        this.name = name;
        this.age = age;
    }

    public String getName(){ return name; }
    public int getAge(){ return age; }
    public void setName(String name){ this.name = name; }
    public void setAge(int age){ this.age = age; }
}

class HumanPet
{
    private Person person;
    private Pet pet;

    public HumanPet(Person person, Pet pet)
    {
        this.person = person;
        this.pet = pet;
    }

    public Person getPerson(){ return person; }
    public Pet getPet(){ return pet; }
    public void setPerson(Person person){ this.person = person; }
    public void setPet(Pet pet){ this.pet = pet; }
}

```

Här hade vi kunnat ärva `Person` eller `Pet` men vi väljer självklart kompostion över arv. Oavsett variant skulle det orsakat problem. Så nu kan vi ärva `HumanPet` och få med oss både `Person` och `Pet`... om vi nu vill det.

```java
class Family
{
    private HumanPet father;
    private HumanPet mother;
    private HumanPet[] child;
    private Pet[] familyPets;

    public Family(HumanPet father, HumanPet mother, HumanPet[] child, Pet[] familyPets)
    {
        this.father = father;
        this.mother = mother;
        this.child = child;
        this.familyPets = familyPets;
    }

    public HumanPet getFather(){ return father; }
    public HumanPet getMother(){ return mother; }
    public HumanPet getChild(){ return child; }
    public Pet[] getFamilyPets(){ return familyPets; }
    public void setFather(HumanPet father){ this.father = father; }
    public void setMother(HumanPet mother){ this.mother = mother; }
    public void setChild(HumanPet child){ this.child = child; }
    public void setFamilyPets(Pet[] familyPets){ this.familyPets = familyPets; }
}
```

Nu kan vi skapa en familj där alla har var sitt husdjur.

## Exempel 2

För att förstå hur man implementerar "Komposition över Arv" i praktiken, låt oss titta på ett exempel med Java-kod. Anta att vi har ett program som hanterar karaktärer i en Star Wars-värld. Vi har två klasser: `Character` och `Weapon`.

```java
public class Character {
private String name;
private Weapon weapon;

public Character(String name, Weapon weapon) {
this.name = name;
this.weapon = weapon;
}

public void attack() {
if (weapon != null) {
weapon.use();
} else {
System.out.println(name + " has no weapon.");
}
}
}

```

Ovan skapade vi karaktärer, vapen och använde dem i vår applikation. Vi skapade en instans av `Character` och tilldelade den ett vapen. Sedan anropade vi `attack()`-metoden för att se hur karaktären använder sitt tilldelade vapen.

Nu ska vi skapa vapen.

```java
public interface Weapon {
void use();
}

public class Lightsaber implements Weapon {
@Override
public void use() {
System.out.println("Swinging lightsaber!");
}
}

public class Blaster implements Weapon {
@Override
public void use() {
System.out.println("Shooting blaster!");
}
}
```

I det här exemplet representerar `Character` en karaktär i Star Wars och `Weapon` representerar ett vapen som kan användas av karaktären. Istället för att använda arv för att definiera olika typer av karaktärer med specifika vapen, använder vi komposition för att sammansätta karaktärer med vapen.

En karaktär har ett namn och en referens till ett vapen. I `Character`-klassen finns en metod `attack()` som anropar `use()`-metoden för det tilldelade vapnet. Om karaktären inte har något vapen skrivs ett meddelande ut.

Vi har också en `Weapon`-gränssnitt som definierar en enda metod `use()`. Både `Lightsaber`- och `Blaster`-klasserna implementerar detta gränssnitt och tillhandahåller implementationer för `use()`-metoden.

För att använda detta i vår applikation kan vi skapa instanser av `Character` och `Weapon` och sätta ihop dem genom att tilldela ett vapen till en karaktär.

```java
public class Main {
public static void main(String[] args) {
Weapon lightsaber = new Lightsaber();
Character jedi = new Character("Luke Skywalker", lightsaber);
jedi.attack(); // Output: Swinging lightsaber!

Weapon blaster = new Blaster();
Character bountyHunter = new Character("Boba Fett", blaster);
bountyHunter.attack(); // Output: Shooting blaster!

Character padawan = new Character("Ahsoka Tano", null);
padawan.attack(); // Output: Ahsoka Tano has no weapon.
}
}
```

I `Main`-klassen skapar vi instanser av `Lightsaber` och `Blaster` som representerar vapen. Sedan skapar vi instanser av `Character` och tilldelar respektive vapen till dem. Genom att anropa `attack()`-metoden för varje karaktär kan vi se hur de använder sina tilldelade vapen.

Detta exempel visar hur vi kan använda komposition för att sammansätta klasser och uppnå flexibilitet och återanvändbarhet. Istället för att ha en hierarki av klasser med olika kombinationer av vapen, kan vi enkelt kombinera olika karaktärer och vapen genom att ändra vilka objektinstanser som tilldelas till varje karaktär.

## Summan av kardemumman

I Detta avsnitt har vi utforskat konceptet "Komposition över Arv" och dess betydelse inom programmering. Vi har sett fördelarna med att använda komposition, såsom flexibilitet, moduläritet, återanvändbarhet och minskat beroende. Vi har också identifierat begränsningar som ökad komplexitet och mer kod att skriva. Genom ett kodexempel har vi sett hur man kan implementera komposition i praktiken med hjälp av Java.

För vidare läsning rekommenderas att utforska olika designmönster och principer inom objektorienterad programmering, såsom SOLID-principerna och Design Patterns-boken av Erich Gamma m.fl.
