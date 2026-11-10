---
title: "Lathund: MongoDB"
author: Marcus Ackre Medina
description: "MongoDB i Java i lathundsform: Docker, Atlas, Compass, konfiguration, CRUD, transaktioner med replica set och seeding."
parent: Lathund
nav_order: 30
---
# Lathund: MongoDB

MongoDB är en dokumentdatabas. Du lagrar dokument i en collection, och du behöver ingen tabellstruktur i förväg. Samma kapitel finns för C#, med MongoDB C#-drivern.

## Välj hur du kör MongoDB

| Alternativ | När du väljer det | Connection string |
|------------|-------------------|-------------------|
| **Docker** | Du vill ha en databas på din egen dator | `mongodb://localhost:27017` |
| **MongoDB Atlas** | Du vill nå databasen från flera datorer, eller slippa installera något | `mongodb+srv://...` från Atlas |

## Dependency

```xml
<dependency>
    <groupId>org.mongodb</groupId>
    <artifactId>mongodb-driver-sync</artifactId>
    <version>5.14.0</version>
</dependency>
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
    <version>2.23.0</version>
</dependency>
```

Drivern är versionsnumrerad efter de senaste utgåvorna. Kontrollera senaste version på Maven Central.

## Konfiguration

I `config.json`:

```json
{
  "ConnectionStrings": {
    "MongoLocal": "mongodb://localhost:27017",
    "MongoAtlas": "mongodb+srv://<användarnamn>:<lösenord>@<kluster>.mongodb.net/?retryWrites=true&w=majority"
  }
}
```

Lösenordet kommer från en miljövariabel. Sätt den i terminalen innan du startar programmet:

```bash
export MONGO_ATLAS="mongodb+srv://<användarnamn>:<riktigt lösenord>@<kluster>.mongodb.net/?retryWrites=true&w=majority"
```

```java
ObjectMapper mapper = new ObjectMapper();
JsonNode config = mapper.readTree(new File("config.json"));

String connectionString = config.get("ConnectionStrings").get("MongoLocal").asText();

// Tänk på att lägga till try/catch där anslutningen kan misslyckas
MongoClient client = MongoClients.create(connectionString);
MongoDatabase database = client.getDatabase("webshop");
MongoCollection<Document> products = database.getCollection("products");
```

Byt `MongoLocal` mot `MongoAtlas` när du vill ansluta till Atlas. Koden är densamma.

## Docker

```bash
docker run --name mongo1 -p 27017:27017 -v mongo-data:/data/db -d mongo
```

Volymen `mongo-data` gör att datan finns kvar om du tar bort containern.

## Atlas

1. Skapa ett konto på mongodb.com/cloud/atlas. Gratisnivån (M0) räcker.
2. Skapa ett kluster: *Build a Database* → *M0 Free*.
3. Under *Security* → *Database Access*: skapa en databasanvändare med eget lösenord. Spara det direkt.
4. Under *Security* → *Network Access*: lägg till din egen IP-adress med *Add Current IP Address*.
5. Klicka på *Connect* → *Drivers* → Java och kopiera connection string. Byt ut `<password>`.

**På lektionerna** lägger vi till `0.0.0.0/0`, som betyder alla adresser. Ta bort posten efter lektionen.

## Compass

Ladda ner MongoDB Compass från mongodb.com/try/download/compass. Klistra in connection string i fältet *URI* och klicka på *Connect*.

## CRUD

I Java använder vi `Document` för dokument. Det är ett nyckel-värde-objekt, lika enkelt som en `Map`:

```java
// Create
products.insertOne(new Document("name", "Kaffe").append("price", 49.0));

// Read
for (Document doc : products.find(Filters.lt("price", 100.0))) {
    System.out.println(doc.toJson());
}

// Update
products.updateOne(
        Filters.eq("name", "Kaffe"),
        Updates.set("price", 39.0));

// Delete
products.deleteOne(Filters.eq("name", "Kaffe"));
```

Till skillnad från JDBC sparar varje operation direkt. Det finns ingen `commit()` att komma ihåg.

## Transaktioner

Transaktioner över flera dokument kräver ett **replica set**. Atlas är redan ett replica set. En lokal Docker-container måste startas som ett:

```bash
docker run --name mongo-rs -p 27017:27017 -d mongo --replSet rs0
docker exec mongo-rs mongosh --eval "rs.initiate()"
```

Om `mongosh` inte finns i containern kan du köra `rs.initiate()` från Compass.

Transaktionen körs i en session:

```java
try (ClientSession session = client.startSession()) {
    session.startTransaction();
    try {
        products.updateOne(session,
                Filters.eq("name", "Kaffe"),
                Updates.inc("price", -5.0));
        orders.insertOne(session, new Document("productName", "Kaffe"));
        session.commitTransaction();
    } catch (RuntimeException e) {
        session.abortTransaction();
        throw e;
    }
}
```

Varje operation får `session` som första argument. Glömmer du det körs den utanför transaktionen.

## Seeding

Fyll collectionen bara om den är tom:

```java
if (products.countDocuments() == 0) {
    products.insertMany(List.of(
            new Document("name", "Kaffe").append("price", 49.0),
            new Document("name", "Te").append("price", 35.0)));
}
```

## Koppla på från IDE

- **Compass** är det enklaste verktyget.
- **IntelliJ IDEA:** installera pluginet *MongoDB* eller använd Compass vid sidan av.
- **VS Code:** installera *MongoDB for VS Code* av MongoDB.

## Terminologi

| Term | Betydelse |
|------|-----------|
| **Dokument** | En post i MongoDB. Ett objekt med fält, inte en rad |
| **Collection** | En samling dokument. Motsvarar en tabell |
| **Database** | En samling collections |
| **BSON** | Det binära formatet dokumenten lagras i. Liknar JSON |
| **_id** | Dokumentets unika nyckel. Skapas automatiskt |
| **Replica set** | Flera servrar som håller samma data. Krävs för transaktioner |
| **Session** | Ramen för en transaktion. Skickas som första argument |
| **IP access list** | Adresser som får ansluta till Atlas |

## Tips och tricks

- Connection string fungerar inte mot Atlas? Kontrollera att din IP-adress finns i Network Access.
- Ingen data syns? Kontrollera databasens namn. Det måste vara samma i koden och i Compass.
- Lägg inte `0.0.0.0/0` och glöm bort den. Ta bort posten efter lektionen.
- `toJson()` är bra när du vill se vad som faktiskt finns i ett dokument.
