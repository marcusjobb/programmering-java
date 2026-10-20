---
title: Filhantering
author: Marcus Ackre Medina
parent: Java
nav_order: 90
has_children: true
---
# Filhantering

Välkommen till det spännande äventyret där vi ska utforska filhantering i Java! I den avlägsna galaxen Star Wars, där kraften flödar och äventyr väntar, kommer vi att lära oss hur man skapar och hanterar filer som riktiga jedimästare!

## Skapa en klass

Först och främst behöver vi en klass för våra modiga hjältar i denna filhanteringssaga. Låt oss skapa en mäktig klass kallad "Person" som kommer att representera våra karaktärer.

```java
class Person {
    String name;
    int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String toString() {
        return "Namn: " + name + " Ålder:" + age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

## Läsa en textfil

För att läsa en textfil i denna galax använder vi kraften i klassen "FileReader". Vi öppnar en portal till filen vi vill läsa och använder den mäktiga metoden "readLine()" för att läsa in rader från filen.

```java
try {
    FileReader fr = new FileReader("filnamn.txt");
    BufferedReader br = new BufferedReader(fr);
    String row = br.readLine();
    while (row != null) {
        System.out.println(row);
        row = br.readLine();
    }
    br.close();
    fr.close();
} catch (IOException e) {
    System.out.println("Fel! Filen finns inte eller kan inte läsas.");
}
```

## Skriva till en textfil

Nu när vi har våra tappra karaktärer i klassen "Person", låt oss skapa en ny fil och skriva ner dem i den! Vi använder kraften från "FileWriter" för detta uppdrag.

```java
try {
    // Skapa en person
    Person p = new Person("Luke Skywalker", 23);

    // Serialisera personen
    String person = p.toString();

    // Skapa en ny fil och skriv personen till den
    FileWriter fw = new FileWriter("person.txt");
    BufferedWriter bw = new BufferedWriter(fw);
    bw.write(person);
    bw.close();
    fw.close();
} catch (IOException e) {
    System.out.println("Fel! Kunde inte skriva till filen.");
}
```

## Läsa och skriva till en Json-fil

I denna galax vill vi även kunna kommunicera med andra över hela universum. Därför använder vi magin av "Gson" för att skriva ner våra hjältar i ett format som alla kan förstå - Json!

```java
try {
    // Skapa en person
    Person p = new Person("Leia Skywalker", 23);

    // Serialisera personen med hjälp av kraften från Gson
    Gson gson = new Gson();
    String person = gson.toJson(p);

    // Skapa en ny fil och skriv personen till den
    FileWriter fw = new FileWriter("person.json");
    BufferedWriter bw = new BufferedWriter(fw);
    bw.write(person);
    bw.close();
    fw.close();

    // Nu när vi har skrivit till filen, låt oss läsa från den och hämta vår person tillbaka
    FileReader fr = new FileReader("person.json");
    BufferedReader br = new BufferedReader(fr);
    Person p2 = gson.fromJson(br, Person.class);
    br.close();
    fr.close();
    System.out.println(p2);
} catch (IOException e) {
    System.out.println("Fel! Kunde inte läsa eller skriva till Json-filen.");
}
```

## Läsa och skriva binära filer

I Star Wars vill vi också kunna spara våra hjältar i binära filer. För detta uppdrag använder vi kraften av "ObjectOutputStream" och "ObjectInputStream".

```java
try {
    // Skapa en person
    Person p = new Person("Han Solo", 33);

    // Serialisera personen
    ByteArrayOutputStream baos = new ByteArrayOutputStream();
    ObjectOutputStream oos = new ObjectOutputStream(baos);
    oos.writeObject(p);

    // Skapa en ny fil och skriv personen till den
    FileOutputStream fos = new FileOutputStream("person.bin");
    fos.write(baos.toByteArray());
    fos.close();

    // Läs in personen från filen
    FileInputStream fis = new FileInputStream("person.bin");
    ObjectInputStream ois = new ObjectInputStream(fis);
    Person p2 = (Person) ois.readObject();
    ois.close();
    fis.close();
    System.out.println(p2);
} catch (IOException e) {
    System.out.println("Fel! Kunde inte läsa eller skriva till den binära filen.");
} catch (ClassNotFoundException e) {
    System.out.println("Fel! Hittade inte klassen för att deserialisera objektet.");
}
```

## Läsa och skriva binära filer med Base64

I vår galax vill vi även kunna läsa och skriva binära filer med hjälp av Base64-kodning. Det gör vi genom att använda den mäktiga kraften av "Base64" för att konvertera våra binära data till en läsbar textsträng.

```java
try {
    // Skapa en person
    Person p = new Person("Chewbacca", 53); // Rrrrr-ghghghghgh!

    // Serialisera personen
    ByteArrayOutputStream baos = new ByteArrayOutputStream();
    ObjectOutputStream oos = new ObjectOutputStream(baos);
    oos.writeObject(p);

    // Skapa en ny fil och skriv personen till den med Base64-kodning
    FileOutputStream fos = new FileOutputStream("person.bin");
    fos.write(Base.getEncoder().encode(baos.toByteArray()));
    fos.close();

    // Läs in personen från filen med Base64-kodning
    FileInputStream fis = new FileInputStream("person.bin");
    byte[] data = fis.readAllBytes();
    fis.close();

    // Avkoda data med Base64
    byte[] decodedData = Base.getDecoder().decode(data);
    ObjectInputStream ois = new ObjectInputStream(new ByteArrayInputStream(decodedData));
    Person p2 = (Person) ois.readObject();
    ois.close();
    System.out.println(p2);
} catch (IOException e) {
    System.out.println("Fel! Kunde inte läsa eller skriva till den binära

 file.");
} catch (ClassNotFoundException e) {
    System.out.println("Fel! Hittade inte klassen för att deserialisera objektet.");
}
```

## Läsa och skriva binära filer med Base64 och GZIP

Men vi slutar inte där! Vi tar det ett steg längre och använder både Base64-kodning och GZIP-komprimering för att spara våra hjältar på ett effektivt sätt!

```java
try {
    // Skapa en person
    Person p = new Person("Obi-Wan Kenobi", 53); // I have the high ground!

    // Serialisera personen
    ByteArrayOutputStream baos = new ByteArrayOutputStream();
    ObjectOutputStream oos = new ObjectOutputStream(baos);
    oos.writeObject(p);

    // Skapa en ny fil och skriv personen till den med Base64-kodning och GZIP-komprimering
    FileOutputStream fos = new FileOutputStream("person.gzis");
    GZIPOutputStream gzos = new GZIPOutputStream(fos);
    gzos.write(Base.getEncoder().encode(baos.toByteArray()));
    gzos.close();

    // Läs in personen från filen med Base64-kodning och GZIP-komprimering
    FileInputStream fis = new FileInputStream("person.gzis");
    GZIPInputStream gzis = new GZIPInputStream(fis);
    byte[] data = gzis.readAllBytes();
    gzis.close();

    // Avkoda data med Base64
    byte[] decodedData = Base.getDecoder().decode(data);
    ObjectInputStream ois = new ObjectInputStream(new ByteArrayInputStream(decodedData));
    Person p2 = (Person) ois.readObject();
    ois.close();
    System.out.println(p2);
} catch (IOException e) {
    System.out.println("Fel! Kunde inte läsa eller skriva till den binära filen.");
} catch (ClassNotFoundException e) {
    System.out.println("Fel! Hittade inte klassen för att deserialisera objektet.");
}
```

## Övrig filhantering

Självklart har vi många andra tricks i rockärmen när det gäller filhantering. Låt oss utforska några av dem:

### Kolla om en fil finns

```java
File f = new File("person.txt");
if (f.exists()) {
    System.out.println("Filen finns");
}
```

### Skapa en tom fil om den inte finns

```java
File f = new File("person.txt");
try {
    if (!f.exists()) {
        f.createNewFile();
    }
} catch (IOException e) {
    System.out.println("Fel! Kunde inte skapa filen.");
}
```

### Skapa en mapp om den inte finns

```java
File f = new File("mapp");
if (!f.exists()) {
    f.mkdir();
}
```

### Radera en fil

```java
File f = new File("person.txt");
if (f.exists()) {
    f.delete();
}
```

### Radera en mapp om den är tom

```java
File f = new File("mapp");
if (f.exists()) {
    if (f.isDirectory() && f.list().length == 0) {
        f.delete();
    }
}
```

### Flytta en fil

```java
File f = new File("person.txt");
if (f.exists()) {
    f.renameTo(new File("person2.txt"));
}
```

### Lista alla filer i en mapp

```java
File f = new File("mapp");
if (f.exists()) {
    File[] files = f.listFiles();
    for (File file : files) {
        System.out.println(file.getName());
    }
}
```

### Lista alla filer i en mapp och dess undermappar

```java
File f = new File("mapp");
if (f.exists()) {
    listAllFiles(f);
}

private void listAllFiles(File folder) {
    File[] files = folder.listFiles();
    for (File file : files) {
        if (file.isDirectory()) {
            listAllFiles(file);
        } else {
            System.out.println(file.getName());
        }
    }
}
```

### Hitta en fil som med namn som innehåller "Katt"

```java
File f = new File("mapp");
if (f.exists()) {
    findFileContainingName(f, "Katt");
}

private void findFileContainingName(File folder, String name) {
    File[] files = folder.listFiles();
    for (File file : files) {
        if (file.getName().contains(name)) {
            System.out.println(file.getName());
        }
    }
}
```

### Hitta en fil som med namn som innehåller "Hemlighet" och radera den

```java
File f = new File("mapp");
if (f.exists()) {
    findAndDeleteFileContainingName(f, "Hemlighet");
}

private void findAndDeleteFileContainingName(File folder, String name) {
    File[] files = folder.listFiles();
    for (File file : files) {
        if (file.getName().contains(name)) {
            file.delete();
        }
    }
}
```

### Hitta en fil med texten "Lösenord" i sig

```java
File f = new File("mapp");
if (f.exists()) {
    findFileWithText(f, "Lösenord");
}

private void findFileWithText(File folder, String text) {
    File[] files = folder.listFiles();
    for (File file : files) {
        if (file.isFile()) {
            try {
                BufferedReader br = new BufferedReader(new FileReader(file));
                String line;
                while ((line = br.readLine()) != null) {
                    if (line.contains(text)) {
                        System.out.println(file.getName());
                        break;
                    }
                }
                br.close();
            } catch (IOException e) {
                System.out.println("Fel! Kunde inte läsa filen.");
            }
        }
    }
}
```

### Få information om filen

```java
File f = new File("person.txt");

if (f.exists()) {
    System.out.println("Filnamn: " + f.getName());
    System.out.println("Filtyp: " + f.getType());
    System.out.println("Mapp: " + f.getParent());
    System.out.println("Sökväg: " + f.getAbsolutePath());
    System.out.println("Storlek: " + f.length());
    System.out.println("Senast ändrad: " + f.lastModified());
    System.out.println("Är fil: " + f.isFile());
    System.out.println("Är mapp: " + f.isDirectory());
    System.out.println("Är dold: " + f.isHidden());
    System.out.println("Är läsbar: " + f.canRead());
    System.out.println("Är skrivbar: " + f.canWrite());
    System.out.println("Är exekverbar: " + f.canExecute());
    System.out.println("Är samma fil: " + f.equals(new File("person.txt")));
}
```

## Termer och förklaringar

Nu när vi har erö

vrat filhanteringsuniversum i Star Wars, låt oss sammanfatta några av de termer och deras förklaringar som vi stött på i vårt äventyr:

| Term                    | Förklaring                                                                     |
| ----------------------- | ------------------------------------------------------------------------------ |
| `FileReader`            | En klass som används för att läsa textfiler.                                   |
| `FileWriter`            | En klass som används för att skriva till textfiler.                            |
| `Gson`                  | En klass som används för att läsa och skriva till Json-filer.                  |
| `Base`                | En klass som används för att läsa och skriva binära filer.                     |
| `GZIPOutputStream`      | En klass som används för att läsa och skriva binära filer med Base64 och GZIP. |
| `ObjectOutputStream`    | En klass som används för att läsa och skriva binära filer.                     |
| `ObjectInputStream`     | En klass som används för att läsa och skriva binära filer.                     |
| `ByteArrayOutputStream` | En klass som används för att läsa och skriva binära filer.                     |
| `FileInputStream`       | En klass som används för att läsa och skriva binära filer.                     |
| `FileOutputStream`      | En klass som används för att läsa och skriva binära filer.                     |
| `GZIPInputStream`       | En klass som används för att läsa och skriva binära filer med Base64 och GZIP. |
| `readLine()`            | En metod som används för att läsa en rad från en textfil.                      |
| `write()`               | En metod som används för att skriva till en textfil.                           |
| `toJson()`              | En metod som används för att skriva till en Json-fil.                          |
| `fromJson()`            | En metod som används för att läsa från en Json-fil.                            |
| `read()`                | En metod som används för att läsa från en binär fil.                           |
| `write()`               | En metod som används för att skriva till en binär fil.                         |
| `encode()`              | En metod som används för att läsa från en binär fil med Base64.                |
| `decode()`              | En metod som används för att skriva till en binär fil med Base64.              |
| `close()`               | En metod som används för att stänga en fil.                                    |
| `split()`               | En metod som används för att dela upp en sträng i en array.                    |
| `toString()`            | En metod som används för att konvertera ett objekt till en sträng.             |
| `getName()`             | En metod som används för att hämta namnet på en person.                        |
| `getAge()`            | En metod som används för att hämta åldern på en person.                        |
| `setName()`             | En metod som används för att sätta namnet på en person.                        |
| `setAge()`            | En metod som används för att sätta åldern på en person.                        |
| `Person`                | En klass som används för att representera en person.                           |
| `name`                  | En variabel som används för att lagra namnet på en person.                     |
| `age`                 | En variabel som används för att lagra åldern på en person.                     |
| `p`                     | En variabel som används för att representera en person.                        |
| `p2`                    | En variabel som används för att representera en person.                        |
| `row`                   | En variabel som används för att representera en rad i en textfil.              |
| `parts`                 | En variabel som används för att representera en array av strängar.             |
| `fr`                    | En variabel som används för att representera en textfil.                       |
| `fw`                    | En variabel som används för att representera en textfil.                       |
| `gson`                  | En variabel som används för att representera en Json-fil.                      |
| `baos`                  | En variabel som används för att representera en binär fil.                     |
| `oos`                   | En variabel som används för att representera en binär fil.                     |
| `fos`                   | En variabel som används för att representera en binär fil.                     |
| `fis`                   | En variabel som används för att representera en binär fil.                     |
| `gzos`                  | En variabel som används för att representera en binärfil med Base64 och GZIP.  |
| `gzis`                  | En variabel som används för att representera en binärfil med Base64 och GZIP.  |
| `ois`                   | En variabel som används för att representera en binär fil.                     |
| `fr`                    | En variabel som används för att representera en textfil.                       |

## Summan av kardemumman

Grattis! Nu har du blivit en äkta mästare i filhantering i Star Wars-stil. Du kan nu spara och läsa data i olika format och utföra m

äktiga filhanteringsoperationer med hjälp av Java. Må kraften vara med dig i dina framtida äventyr i programmeringens galax!
