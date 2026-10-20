---
title: Edifact med XML
author: Marcus Ackre Medina
parent: Filhantering
nav_order: 80
---
# Edifact med XML

Edifact och XML är två teknologier som används för att hantera datautbyte mellan olika system. Men hur kombinerar vi dessa två? Vad kan vi göra med dem, och varför skulle vi vilja använda dem tillsammans? Svaren på dessa frågor kommer att uppenbara sig genom att vi går igenom detta avsnitt. Edifact står för "Electronic Data Interchange for Administration, Commerce, and Transport." Det är ett internationellt system för att överföra data. XML används ofta tillsammans med Edifact för att presentera data i en läsbar och strukturerad form.

## TL;DR

I detta avsnitt kommer vi att utforska hur Edifact kan användas med XML, inklusive exempel på filer, en Maven POM.xml och ett kodexempel i Java. Detta ger en djupare förståelse för hur dessa teknologier kan användas tillsammans.

## När du läst detta ska du kunna

- Förstå och förklara vad Edifact och XML är och deras relevans inom programmering.
- Skapa och läsa Edifact-filer med XML-struktur.
- Använda Maven för att hantera projekt som involverar Edifact och XML.
- Implementera ett Java-kodexempel som använder Edifact med XML.

## Vad är Edifact med XML?

Edifact står för "Electronic Data Interchange for Administration, Commerce, and Transport." Det är ett internationellt system för att överföra data. XML används ofta tillsammans med Edifact för att presentera data i en läsbar och strukturerad form.

## Exempel på Edifact-fil med XML

Här är ett grundläggande exempel på en Edifact-fil i XML-format:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<EDIFACT>
  <!-- Din Edifact-data här -->
</EDIFACT>
```

Här följer några exempel:

### Kvitto till Batman på inköp av en Batmobil

```xml
<?xml version="1.0" encoding="UTF-8"?>
<EDIFACT>
  <INVOICE>
    <CUSTOMER>Batman</CUSTOMER>
    <ITEM>Batmobil</ITEM>
    <QUANTITY>1</QUANTITY>
    <PRICE>1000000</PRICE>
    <TOTAL>1000000</TOTAL>
  </INVOICE>
</EDIFACT>
```

### Faktura till Lex Luthor med grön kryptonit

```xml
<?xml version="1.0" encoding="UTF-8"?>
<EDIFACT>
  <INVOICE>
    <CUSTOMER>Lex Luthor</CUSTOMER>
    <ITEM>Green Kryptonit</ITEM>
    <QUANTITY>1</QUANTITY>
    <PRICE>5000</PRICE>
    <TOTAL>5000</TOTAL>
  </INVOICE>
</EDIFACT>
```

### Räkning på kameralinser till Jimmy Olsen

```xml
<?xml version="1.0" encoding="UTF-8"?>
<EDIFACT>
  <INVOICE>
    <CUSTOMER>Jimmy Olsen</CUSTOMER>
    <ITEM>CameraLenses</ITEM>
    <QUANTITY>3</QUANTITY>
    <PRICE>300</PRICE>
    <TOTAL>900</TOTAL>
  </INVOICE>
</EDIFACT>
```

```XML
<?xml version="1.0" encoding="UTF-8"?>
<EDIFACT>
  <PAYMENT>
    <PAYEE>Peter Parker</PAYEE>
    <PAYER>Daily Bugle</PAYER>
    <DESCRIPTION>Photos on Spindelmannen</DESCRIPTION>
    <AMOUNT>2000</AMOUNT>
    <CURRENCY>USD</CURRENCY>
    <DATE>2023-08-10</DATE>
  </PAYMENT>
</EDIFACT>
```

#### Poster

| Tag         | Beskrivning                         |
| ----------- | ----------------------------------- |
| AMOUNT      | Beloppet som ska betalas            |
| CURRENCY    | Valutan som ska användas            |
| CUSTOMER    | Namnet på kunden                    |
| DATE        | Datum för betalningen               |
| DESCRIPTION | Beskrivning av betalningen          |
| ITEM        | Namnet på produkten                 |
| PAYEE       | Namnet på den som ska betalas       |
| PAYER       | Namnet på den som betalar           |
| PRICE       | Priset på varje produkt             |
| QUANTITY    | Antalet produkter som köpts         |
| Tag         | Beskrivning                         |
| TOTAL       | Totala kostnaden för alla produkter |

Dessa exempel visar hur du kan representera olika fakturor och kvitton med Edifact och XML. Du kan sedan använda lämpliga Java-bibliotek för att bearbeta dessa filer som beskrivet tidigare.

Hoppas detta inspirerar dig att utforska vidare och skapa ännu mer med Edifact och XML. Kom ihåg, att skapa är roligt! Att lära sig mer är roligt! Programmering är roligt!

## Maven POM.xml

För att hantera ditt projekt som involverar Edifact och XML kan du använda Maven. Här är en grundläggande POM.xml-struktur. Fyll i de nödvändiga beroendena för ditt specifika projekt:

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>edifactxml</artifactId>
    <version>1.0-SNAPSHOT</version>
    <dependencies>
        <!-- Dina beroenden här -->
        <dependency>
            <groupId>org.apache.camel</groupId> // camel är ett populärt bibliotek för att hantera Edifact och XML
            <artifactId>camel-core</artifactId>
            <version>3.11.1</version>
        </dependency>
    </dependencies>
</project>
```

## Kodexempel i Java

För att arbeta med Edifact och XML i Java behöver du använda specifika bibliotek. Tyvärr har vi inte en fullständig kod här, men du kan använda bibliotek som Smooks eller Apache Camel för att hantera Edifact-meddelanden i Java.

```java
import java.io.Serializable;

public interface Transaction {
    String getType();
    double getTotalAmount();
}

public class Purchase implements Transaction {
    private String buyer;
    private String product;
    private int quantity;
    private double price;

    public Purchase(String buyer, String product, int quantity, double price) {
        this.buyer = buyer;
        this.product = product;
        this.quantity = quantity;
        this.price = price;
    }

    // getters and setters

    @Override
    public String toString() {
        return "PURCHASE: " + buyer + " bought " + quantity + " " + product + " for " + price;
    }
}

public class Payment implements Transaction {
    private String payee;
    private String payer;
    private double amount;

    // Konstruktor, getters och setters

    @Override
    public String getType() {
        return "PAYMENT";
    }

    @Override
    public double getTotalAmount() {
        return amount;
    }
}

public class Receipt implements Transaction {
    private String seller;
    private String buyer;
    private double total;

    // Konstruktor, getters och setters

    @Override
    public String getType() {
        return "RECEIPT";
    }

    @Override
    public double getTotalAmount() {
        return total;
    }
}
```

vi skapar även en factory för att kunna hantera dem
```java
public class TransactionFactory {

    public static Transaction createTransaction(String type) {
        switch (type) {
            case "PURCHASE":
                return new Purchase(/* parametrar */);
            case "PAYMENT":
                return new Payment(/* parametrar */);
            case "INVOICE":
                return new Invoice(/* parametrar */);
            case "RECEIPT":
                return new Receipt(/* parametrar */);
            default:
                throw new IllegalArgumentException("Invalid type: " + type);
        }
    }
}
```

och en serialiserare

```java
import java.io.*;

public class SerializationUtil {

    public static void serialize(Object obj, String fileName) throws IOException {
        try (FileOutputStream fileOut = new FileOutputStream(fileName);
             ObjectOutputStream out = new ObjectOutputStream(fileOut)) {
            out.writeObject(obj);
        }
    }

    public static Object deserialize(String fileName) throws IOException, ClassNotFoundException {
        try (FileInputStream fileIn = new FileInputStream(fileName);
             ObjectInputStream in = new ObjectInputStream(fileIn)) {
            return in.readObject();
        }
    }
}
```

och vi testar det i main

```java
public class Main {
    public static void main(String[] args) {
        // Skapa en Purchase
        Purchase purchase = new Purchase("Batman", "Katt", 1, 100.0);

        // Skapa en Payment
        Payment payment = new Payment("Batman", "Cat Store", 100.0);

        // Serialisera
        try {
            SerializationUtil.serialize(purchase, "purchase.ser");
            SerializationUtil.serialize(payment, "payment.ser");
        } catch (IOException e) {
            e.printStackTrace();
        }

        // Deserialisera
        try {
            Purchase deserializedPurchase = (Purchase) SerializationUtil.deserialize("purchase.ser");
            Payment deserializedPayment = (Payment) SerializationUtil.deserialize("payment.ser");

            System.out.println(deserializedPurchase);
            System.out.println(deserializedPayment);
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

## Slutsats

Att kombinera Edifact med XML är en kraftfull teknik som kan underlätta datautbyte mellan olika system. Genom att förstå hur dessa teknologier kan användas tillsammans, har du ökat din förmåga att arbeta med komplex datahantering.

## Obligatorisk dad joke:

Varför gillade programmeraren XML så mycket? För att han kunde märka upp allt han ville!
