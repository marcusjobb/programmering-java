---
title: XML
author: Marcus Ackre Medina
parent: Filhantering
nav_order: 90
---
# XML

Har du någonsin undrat vad som driver datans bakom många applikationer, konfigurationsfiler eller datautbyte mellan system? Möt XML! Men vad är XML egentligen? Och varför är det så populärt inom programmeringsvärlden? Låt oss utforska tillsammans!

## TL;DR

XML, som står för "Extensible Markup Language", är ett märkspråk som används för att lagra och transportera data. Det är självbeskrivande, läsbart för både människor och maskiner, och det kan användas tillsammans med ett brett spektrum av applikationer.

## När du läst detta ska du kunna

- Förstå och förklara vad XML är och dess relevans inom programmering.
- Diskutera fördelar och begränsningar med XML.
- Identifiera olika användningsområden där XML kan tillämpas.
- Förstå och tolka flera kodexempel som använder XML.
- Sammanfatta viktiga insikter och rekommendationer för vidare läsning.

## Vad är XML?

XML är ett verktyg för att strukturera information, påminnande om HTML. Medan HTML beskriver hur data ska presenteras (som en webbsida), beskriver XML vad data är. Det gör det lättare för program och system att förstå och tolka datan.

### Taggar och Element

Varje element i XML definieras med en starttagg (<tagg>) och en sluttagg (</tagg>). Allt som finns mellan dessa två taggar kallas elementets värde.

```xml
    <element>element value</element>
```

### Attribut

Förutom element kan XML också ha attribut som tillhandahåller extra information. Ett attribut placeras i starttaggen. Det består av ett namn och ett värde, separerade av ett likhetstecken. Ett element kan ha flera attribut.

```xml
    <element attribute="värde">element information</element>
```

## Fördelar

1. **Plattformsoberoende:** XML-data kan läsas av alla system, oavsett operativsystem eller programmeringsspråk.
2. **Utökningsbar:** XML är flexibelt, vilket innebär att du kan skapa egna taggar och attribut.
3. **Självbeskrivande:** XML-dokument innehåller både data och information om den datan, vilket gör det enklare att förstå.
4. **Universell**: XML kan användas på alla plattformar och med de flesta programmeringsspråk.

## Begränsningar

1. **För stor overhead:** XML-dokument kan bli stora och därmed långsamma att processa.
2. **Säkerhet:** Precis som alla datatyper, kan XML-dokument vara sårbara för attacker.
3. **Verbositet**: XML kan ibland bli för lång och omständlig.
4. **Säkerhetsrisker**: XML-dokument kan vara mottagliga för vissa typer av attacker.

## Användningsområden

1. **Konfigurationsfiler:** Många program använder XML för sina konfigurationsfiler.
2. **Datautbyte:** XML används ofta för att skicka och ta emot data mellan klient och server i webbapplikationer.
3. **Beskrivningsspråk:** För exempelvis webbservicar som SOAP.

## Exempelkod

Tänk dig att du vill lagra information om ditt favoritbibliotek och de böcker det innehåller. Nedan är ett exempel på hur det kan se ut med XML:

```xml
<library>
    <book id="152101">
        <title>Plans for Gotham</title>
        <author>Joker</author>
    </book>
    <book id="152113">
        <title>Icy Manipulation</title>
        <author>Mr. Freeze</author>
    </book>
    <book id="152129">
        <title>Förföringens Rules</title>
        <author>Catwoman</author>
    </book>
    <book id="152143">
        <title>Shadows Call</title>
        <author>Ra's al Ghul</författare>
    </book>
    <book id="152158">
        <title>Riddlarens Riddles</title>
        <author>Riddler</author>
    </book>
    <book id="152169">
        <title>Bird Escape</title>
        <author>Penguin</author>
    </book>
</library>
```

## XML-attack

En XML-attack syftar vanligen till att utnyttja sårbarheter i en applikation som behandlar XML-data. Dessa attacker kan leda till olika säkerhetsproblem, från tjänstenedsättning till obehörig åtkomst till systemdata. Här är några vanliga former av XML-attacker:

### XML Bomb (eller "Billion Laughs Attack")

Denna attack involverar att skapa en välformad XML-struktur som leder till en enorm expansion när den tolkas av en XML-parser. Syftet med denna attack är att förbruka systemresurser och orsaka en tjänstenedsättning (DoS).

### XML External Entity (XXE) Attack

XXE-attacken syftar till att utnyttja sårbarheter i XML-parsers. Angriparen kan försöka få åtkomst till externa filer på servern eller utföra andra skadliga handlingar genom att infoga skadlig kod i XML-data.

### XPath Injection

Liknande SQL-injektion, XPath-injektionsattacker uppstår när en angripare kan manipulera en XPath-fråga genom att skjuta in skadlig kod. Detta kan ge obehörig åtkomst till data eller till och med möjligheten att ändra data.

### Skräddarsydda XML-attacker

Utöver de vanligaste formerna av XML-attacker finns det möjlighet att skräddarsy attacker för att utnyttja specifika sårbarheter i en applikation som behandlar XML.

### Förebyggande av XML-attacker

För att skydda mot dessa och andra XML-baserade attacker, bör utvecklare:

- Använda uppdaterade XML-parsers som har säkerhetsfunktioner.
- Inaktivera onödiga funktioner, som externt laddade entiteter.
- Validera all inkommande XML-data mot en känd god skematyp.
- Undvik att visa felmeddelanden som kan ge bort kritisk information om systemets interna struktur.

Kom ihåg att säkerheten för en applikation bör vara ett ständigt pågående arbete. Att vara medveten om sårbarheter och angreppsmetoder hjälper utvecklare att bygga mer robusta och säkra system. Och det är inte bara roligt att lära sig och skapa, utan också att skydda det du har skapat!

## Slutsats

XML är ett kraftfullt verktyg för att lagra och transportera data på ett sätt som både människor och maskiner kan förstå. Trots sina begränsningar förblir det ett populärt val inom programmering och systemintegration. Om du är intresserad av att fördjupa dig i XML, rekommenderar jag att du utforskar dess relation med andra teknologier såsom XSLT och XPath.

## Termer

## Termer

| Term             | Förklaring                                                                                                                                                                   |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| XML              | Extensible Markup Language, ett språk för att definiera och transportera data.                                                                                               |
| Tagg             | Markerar start och slut på en element i XML (ex. `<name>`).                                                                                                                  |
| Attribut         | En extra upplysning eller egenskap som kan läggas till en tagg i XML, t.ex. `id="1234"`.                                                                                     |
| Element          | Datastrukturen skapad av en starttagg, sluttagg och dess värde.                                                                                                              |
| Deklaration      | En inledande rad i XML-dokument, t.ex. `<?xml version="1.0" encoding="UTF-8"?>`. Den specificerar versionen av XML och (eventuellt) teckenkodningen som dokumentet använder. |
| CDATA            | En sektion inom XML där data inte ska tolkas av parsern. Används för att inkludera tecken som "<" och "&" utan att de tolkas som kod.                                        |
| Namespace        | Används för att undvika namnkonflikter i XML. Med namespace kan element med samma namn men från olika källor användas tillsammans i ett enda XML-dokument.                   |
| Parser           | Ett program eller verktyg som läser XML-dokument och omvandlar det till ett format som kan förstås och användas av applikationer.                                            |
| Well-formed XML  | Ett XML-dokument som följer grundläggande XML-regler: t.ex. varje starttagg har en motsvarande sluttagg, och taggar överlappar inte varandra.                                |
| Valid XML        | Ett well-formed XML-dokument som också följer en särskild uppsättning regler definierade i en DTD (Document Type Definition) eller ett XML-schema.                           |
| DTD              | Document Type Definition, en uppsättning regler för XML-dokument som definierar struktur och tillåtna värden.                                                                |
| XML-schema (XSD) | En mer modern och flexibel metod än DTD för att definiera struktur och datatyper för XML-dokument.                                                                           |
| XPath            | Ett språk för att navigera och fråga data i ett XML-dokument.                                                                                                                |
| XSLT             | Extensible Stylesheet Language Transformations, ett språk för att omvandla XML-dokument till andra format (som andra XML, HTML, eller text).                                 |

## Obligatorisk dad joke:

Varför gillar datorer XML?
För att de tycker om att märka upp saker!
