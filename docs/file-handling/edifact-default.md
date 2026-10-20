---
title: Edifact grundform
author: Marcus Ackre Medina
parent: Filhantering
nav_order: 70
---
# Edifact grundform

Edifact, eller Electronic Data Interchange for Administration, Commerce, and Transport, är en global standard för elektroniskt datautbyte. Men vad är Edifact, och varför är det relevant i Java-programmering? Hur använder DC-hjältar som Batman och Superman det för att göra affärer? Läs vidare för att utforska!

## TL;DR

Edifact är en internationell standard för elektroniskt datautbyte. Denna avsnitt fokuserar på Edifact i traditionell form, illustrerat med ett kodexempel där DC-hjältar engagerar sig i en affärstransaktion.

## När du läst detta ska du kunna

- Förstå vad Edifact i grundform är.
- Se dess relevans i programmering och affärstransaktioner.
- Identifiera hur DC-hjältar som Batman och Superman kan använda Edifact.
- Förstå ett kodexempel i Java som använder Edifact.
- Känna glädjen i att skapa och lära dig mer!

## Vad är Edifact grundform?

Edifact är en standard som används för elektroniskt datautbyte mellan företag. Grundformen av Edifact, utan användning av XML, används ofta för enkelhet och hastighet.

## Fördelar

Edifact i grundform kan vara mer kompakt och snabbare än XML-baserade format. Det är som om Superman levererade ditt paket – snabbt och effektivt!

## Begränsningar

Liksom Batman har sina svagheter, har Edifact i grundform också begränsningar, såsom potentiella kompatibilitetsproblem med vissa system.

## Användningsområden

Edifact kan användas inom en rad affärsområden, inklusive detaljhandel, finans och transport. Från Gotham City till Metropolis, Edifact i grundform kan användas i handel, transport och mycket mer.

## Exempelkod - Edifact i en berättelse

Låt oss föreställa oss att Batman köper några nya Batarangs från Wonder Woman. Här är ett kodexempel som illustrerar användningen av Edifact:

```plaintext
NAD+BY+BAT123::91++Wayne Enterprises+Gotham City++
INV+PAY+WON456::91++Wonder Woman's Armory+Themyscira++100000'
```

Och om Superman betalar en faktura till Flash:

```plaintext
NAD+BY+SUP789::91++Superman's Fortress+Metropolis++
INV+PAY+FLA321::91++Flash's Speedy Services+Central City++50000'
```

Självklart! Här nedan hittar du en artikel som beskriver hur man kan hantera Edifact-meddelanden i Java, inklusive att ta emot och skicka dem via HTTP. Jag har också inkluderat kod för att skapa modellklasser för Köp, Betalning, Faktura och Kvitto.

## Hantering av Edifact-meddelanden i Java

Edifact är inte bara en serie tecken; det är ett verktyg som underlättar affärskommunikation mellan system. Hur tar man emot och skickar Edifact-meddelanden via HTTP i Java? Vad betyder begrepp som Köp, Betalning, Faktura och Kvitto inom Edifact? Låt oss utforska tillsammans!

### Vad är Edifact-meddelanden?

Edifact-meddelanden är standardiserade elektroniska meddelanden som används i affärstransaktioner som Köp, Betalning, Faktura och Kvitto.

### Fördelar

Användning av Edifact i ditt system kan förbättra effektiviteten och minska misstagen i affärstransaktioner.

### Begränsningar

Edifact-implementationer kan vara komplexa och kräva noggrann konfiguration.

## Exempelkod - Edifact-Handler i Java

Först, här är modellklasser för Köp, Betalning, Faktura och Kvitto:

```java

public interface EdifactConvertable {
    static EdifactConvertable fromString(String edifact) {
        return null; // Det här är en platsfyllare, faktisk logik skulle vara i fabriksklassen
    }

    @Override
    String toString();
}

class Purchase implements EdifactConvertable {
    private final String buyerCode;
    private final String buyerName;
    private final String buyerAddress;
    private final String product;
    private final int quantity;

    public Purchase(String buyerCode, String buyerName, String buyerAddress, String product, int quantity) {
        this.buyerCode = buyerCode;
        this.buyerName = buyerName;
        this.buyerAddress = buyerAddress;
        this.product = product;
        this.quantity = quantity;
    }

    public static Purchase fromString(String edifact) {
        String[] lines = edifact.split("\n");
        String[] nadDetails = lines[0].split("\\+|:");
        String[] buyDetails = lines[1].split("\\+");

        return new Purchase(nadDetails[2], nadDetails[5], nadDetails[6], buyDetails[1], Integer.parseInt(buyDetails[2]));
    }

    @Override
    public String toString() {
        return "NAD+BY+" + buyerCode + "::91++" + buyerName + "+" + buyerAddress + "++" +
                "'\n" + "BUY+" + product + "+" + quantity + "'";
    }
}

class Payment implements EdifactConvertable {
    private final String payerCode;
    private final String payerName;
    private final String payerAddress;
    private final double amount;

    public Payment(String payerCode, String payerName, String payerAddress, double amount) {
        this.payerCode = payerCode;
        this.payerName = payerName;
        this.payerAddress = payerAddress;
        this.amount = amount;
    }

    public static Payment fromString(String edifact) {
        String[] lines = edifact.split("\n");
        String[] nadDetails = lines[0].split("\\+|:");
        String[] payDetails = lines[1].split("\\+");

        return new Payment(nadDetails[2], nadDetails[5], nadDetails[6], Double.parseDouble(payDetails[1]));
    }

    @Override
    public String toString() {
        return "NAD+BY+" + payerCode + "::91++" + payerName + "+" + payerAddress + "++" +
                "'\n" + "PAY+" + amount + "'";
    }
}

class Invoice implements EdifactConvertable {
    private final String customerCode;
    private final String customerName;
    private final String customerAddress;
    private final double totalAmount;

    public Invoice(String customerCode, String customerName, String customerAddress, double totalAmount) {
        this.customerCode = customerCode;
        this.customerName = customerName;
        this.customerAddress = customerAddress;
        this.totalAmount = totalAmount;
    }

    public static Invoice fromString(String edifact) {
        String[] lines = edifact.split("\n");
        String[] nadDetails = lines[0].split("\\+|:");
        String[] invDetails = lines[1].split("\\+");

        return new Invoice(nadDetails[2], nadDetails[5], nadDetails[6], Double.parseDouble(invDetails[1]));
    }

    @Override
    public String toString() {
        return "NAD+BY+" + customerCode + "::91++" + customerName + "+" + customerAddress + "++" +
                "'\n" + "INV+" + totalAmount + "'";
    }
}

class Receipt implements EdifactConvertable {
    private final String transactionId;
    private final double amountPaid;

    public Receipt(String transactionId, double amountPaid) {
        this.transactionId = transactionId;
        this.amountPaid = amountPaid;
    }

    public static Receipt fromString(String edifact) {
        String[] recDetails = edifact.split("\\+");

        return new Receipt(recDetails[1], Double.parseDouble(recDetails[2]));
    }

    @Override
    public String toString() {
        return "REC+" + transactionId + "+" + amountPaid + "'";
    }
}
```

Nu skapar vi en Factory klass som ska hjälpa oss att hantera de inkommande Edifact-meddelandena:

```java
public class EdifactFactory {
    public static EdifactConvertable fromString(String edifact) {
        if (edifact.contains("BUY")) {
            return Purchase.fromString(edifact);
        } else if (edifact.contains("PAY")) {
            return Payment.fromString(edifact);
        } else if (edifact.contains("INV")) {
            return Invoice.fromString(edifact);
        } else if (edifact.contains("REC")) {
            return Receipt.fromString(edifact);
        } else {
            throw new IllegalArgumentException("Unknown Edifact format");
        }
    }
}
```

Nästa, vi kommer att skapa en `EdifactHandler` för att ta emot och sända meddelanden:

men först måste vi fylla på vårt POM.xml med följande beroenden:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```
Nu kan vi skapa vår klass

```java
import org.springframework.http.*;
import org.springframework.web.bind.annotation.*;
import org.springframework.web.client.RestTemplate;

@RestController
public class EdifactHandler {
    private static final String API_URL = "http://api.localhost/gamestore";
    private static final String API_KEY = "123abc";

    @PostMapping("/sendEdifact")
    public ResponseEntity<String> sendEdifact(@RequestBody String edifactMessage) {
        RestTemplate restTemplate = new RestTemplate();

        HttpHeaders headers = new HttpHeaders();
        headers.setContentType(MediaType.TEXT_PLAIN);
        headers.set("apikey", API_KEY);

        HttpEntity<String> request = new HttpEntity<>(edifactMessage, headers);
        ResponseEntity<String> response = restTemplate.postForEntity(API_URL, request, String.class);

        return ResponseEntity.status(response.getStatusCode()).body("Edifact sent!");
    }

    @GetMapping("/receiveEdifact")
    public ResponseEntity<String> receiveEdifact() {
        RestTemplate restTemplate = new RestTemplate();

        HttpHeaders headers = new HttpHeaders();
        headers.set("apikey", API_KEY);

        HttpEntity<String> request = new HttpEntity<>(headers);
        ResponseEntity<String> response = restTemplate.exchange(API_URL, HttpMethod.GET, request, String.class);

        return ResponseEntity.status(response.getStatusCode()).body(response.getBody());
    }
}
```

och nu kan vi testa koden

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ConfigurableApplicationContext;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        // Start Spring Application
        ConfigurableApplicationContext context = SpringApplication.run(Application.class, args);

        // Create EdifactHandler bean to send edifact messages
        EdifactHandler handler = context.getBean(EdifactHandler.class);

        // 1. Purchase a cat
        Purchase catPurchase = new Purchase(
            "BAT123",
            "Bruce Wayne",
            "Wayne Manor, Gotham City",
            "Cat",
            1
        );

        // Convert Purchase object to Edifact string
        String purchaseEdifact = catPurchase.toString();

        // Send the Edifact message
        handler.sendEdifact(purchaseEdifact);

        // 2. Make a payment for the cat
        Payment catPayment = new Payment(
            "BAT123",
            "Bruce Wayne",
            "Wayne Manor, Gotham City",
            100.0
        );

        // Convert Payment object to Edifact string
        String paymentEdifact = catPayment.toString();

        // Send the Edifact message
        handler.sendEdifact(paymentEdifact);

        // Close the Spring context
        context.close();
    }
}
```

## Termer

| Term        | Förklaring                              |
| ----------- | --------------------------------------- |
| Edifact     | Elektroniskt datautbyte mellan system   |
| Köp         | Transaktion för att köpa något          |
| Betalning   | Transaktion för att betala något        |
| Faktura     | Begäran om betalning                    |
| Kvitto      | Bekräftelse på betalning                |
| Grundform   | Traditionell form utan XML              |
| senderEdifact | Meddelande som skickas till API:et |
| receiveEdifact | Meddelande som tas emot från API:et |

## Slutsats

Att arbeta med Edifact i Java kan vara både utmanande och givande. Med rätt kunskaper och verktyg kan du skapa effektiva och tillförlitliga affärsprocesser! Edifact i grundform är en fascinerande och viktig del av modern datakommunikation, till och med för DC-hjältar! Förståelsen för detta ämne kan hjälpa dig att bli en hjälte i din programmeringsresa!

## Obligatorisk dad joke:

Varför körde Flash aldrig fast i trafiken? För att han alltid hade en snabbfil!
