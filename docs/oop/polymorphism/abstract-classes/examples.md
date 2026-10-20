---
title: Exempel
grand_parent: Polymorfism
author: Marcus Ackre Medina
parent: Abstrakta Klasser
nav_order: 10
---
# Exempel

Vi ska skapa en Abstrakt Klass för Webbskrapning i Java

## Introduktion

I den här övningen ska vi titta på hur man skapar en abstrakt klass med abstrakta och virtuella metoder i Java för att hantera webbskrapning. Webbskrapning är en teknik där vi extraherar data från webbsidor och använder den för att utföra olika uppgifter eller analysera informationen.

För att kunna genomföra övningen behöver vi använda Maven-biblioteket JSoup 1.14.3 eller senare för att hantera HTML-dokument. JSoup är ett populärt Java-bibliotek som gör det lätt att arbeta med HTML och XML-dokument.

Låt oss nu dyka in i övningen och se hur vi kan skapa vår abstrakta klass för webbskrapning!

## TL;DR

I den här övningen har vi lärt oss att skapa en abstrakt klass för webbskrapning i Java. Genom att använda abstrakta metoder kan vi separera implementationen av specifik funktionalitet från själva klassen och därmed skapa en modulär och återanvändbar kodstruktur. Vi har även använt JSoup-biblioteket för att hantera HTML-dokument, vilket underlättar webbskrapningsprocessen. Fortsätt öva och experimentera med abstrakta klasser för att bli en skicklig Java-programmerare!

## När du läst detta ska du kunna

- Förstå och förklara hur man skapar en abstrakt klass med abstrakta och virtuella metoder i Java.
- Implementera en abstrakt klass för att hantera webbskrapning.
- Använda JSoup-biblioteket för att hämta och bearbeta HTML-dokument.

## Beskrivning

Vi ska skapa en abstrakt klass som hanterar webbskrapning för olika sidor. Denna abstrakta klass kommer att innehålla metoder för att hämta och bearbeta webbsidor, och den kommer att definiera vissa metoder som måste implementeras i subklasser.

För att genomföra webbskrapningen behöver vi JSoup-biblioteket. Se till att inkludera det i ditt projekt genom att lägga till följande Maven-dependency:

```xml
<dependency>
    <groupId>org.jsoup</groupId>
    <artifactId>jsoup</artifactId>
    <version>1.14.3</version>
</dependency>
```

## Steg 1: Skapa den Abstrakta Klassen

Först ska vi skapa vår abstrakta klass för webbskrapning. Denna klass kommer att ha vissa attribut och metoder som vi kan använda för att hämta och bearbeta webbsidor. Låt oss kalla klassen `WebScraper`:

```java
import org.jsoup.Jsoup;
import org.jsoup.nodes.Document;
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.io.IOException;

public abstract class WebScraper {
    private String url;
    private String title;
    private String description;
    private String tags;
    private Document htmlDocument;

    // Konstruktor för att initiera URL:en för webbskrapningen
    public WebScraper(String url) {
        this.url = url;
        // Använd JSoup för att hämta HTML-dokumentet från URL:en
        try {
            this.htmlDocument = Jsoup.connect(url).get();
            this.title = htmlDocument.title();
            this.description = htmlDocument.select("meta[name=description]").attr("content");
            this.tags = htmlDocument.select("meta[name=keywords]").attr("content");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    // Abstrakt metod för att implementera webbskrapningen
    public abstract void scrape();

    // Metoder för att hämta olika delar av webbsidan
    public String getTitle() {
        return title;
    }

    public String getDescription() {
        return description;
    }

    public String getTags() {
        return tags;
    }

    public Document getHtmlDocument() {
        return htmlDocument;
    }

    // Metod för att hämta HTML-dokumentet som en sträng
    public String getHtml() {
        return htmlDocument.outerHtml();
    }

    // Metod för att hämta all text på webbsidan utan HTML-taggar
    public String getText() {
        return htmlDocument.text();
    }
}
```

I den här abstrakta klassen har vi definierat ett antal attribut för att lagra URL:en för webbskrapningen, titeln på webbsidan, beskrivningen och meta-nyckelorden. Vi har också en referens till det hämtade HTML-dokumentet från JSoup.

Märk att vi har en konstruktor som tar emot URL:en som argument och använder JSoup för att hämta HTML-dokumentet och fylla i de relevanta attributen.

Vi har också en abstrakt metod `scrape()` som vi inte har implementerat än. Denna metod kommer att vara ansvarig för att utföra själva webbskrapningen, och den måste implementeras i de konkreta subklasserna.

## Steg 2: Implementera Subklassen för Webbskrapning av Kattbilder

Nu ska vi skapa en konkret subklass som ärver från `WebScraper` och implementerar `scrape()`-metoden för att hämta kattbilder från en specifik sida. Låt oss kalla subklassen `GetKittens`:

```java
import org.jsoup.nodes.Element;
import org.jsoup.select.Elements;

import java.util.Random;

public class GetKittens extends WebScraper {
    // Konstruktor för att initiera URL:en för webbskrapningen av kattbilder
    public GetKittens(String url) {
        super(url);
    }

    // Överskrida abstrakt metoden för att implementera webbskrapningen av kattbilder
    @Override
    public void scrape() {
        System.out.println("Downloading page");
        // Inget behov av att hämta HTML-dokument igen, eftersom vi redan gjorde det i konstruktorn
        // Document htmlDocument = getHtmlDocument();
        System.out.println("Getting image list");
        Elements images = getHtmlDocument().select("img");
        System.out.println("Removing non-kitten images");
        images.removeIf(image -> !image.attr("src").contains("kitten"));
        if (images.isEmpty()) {
            System.out.println("No kitten images found.");
            return;

 }

        // Hämtar en slumpmässig bild från listan
        Random random = new Random();
        System.out.println("Selecting random kitten image");
        Element randomImage = images.get(random.nextInt(images.size()));
        String imageUrl = randomImage.attr("src");
        System.out.println("Downloading kitten image");
        // Implementera kod för att ladda ner kattbilden från imageUrl här
        // ...
        System.out.println("Kitten image downloaded successfully!");
    }
}
```

I subklassen `GetKittens` har vi överskridit den abstrakta metoden `scrape()` för att implementera webbskrapningen av kattbilder från den angivna URL:en.

I `scrape()`-metoden använder vi metoden `getHtmlDocument()` från den överordnade klassen `WebScraper` för att hämta HTML-dokumentet för den aktuella sidan. Sedan använder vi JSoup för att filtrera ut alla bilder med "kitten" i URL:en, eftersom vi bara vill ha kattbilder.

Vi hämtar en slumpmässig kattbild från den filtrerade listan och extraherar URL:en för bilden. Sedan kan du implementera koden för att ladda ner kattbilden från `imageUrl`. I det här exemplet har vi lämnat denna del av koden tom eftersom nedladdningsmekanismen kan variera beroende på hur du vill hantera bilden (till exempel spara den på din dator, visa den i ett GUI-fönster etc.).

## Steg 3: Använda den Konkreta Subklassen

Nu när vi har vår abstrakta klass `WebScraper` och den konkreta subklassen `GetKittens`, låt oss använda den konkreta subklassen för att hämta kattbilder från en specifik sida:

```java
public class Main {
    public static void main(String[] args) {
        String url = "https://www.example.com/kittens"; // Byt ut detta med den riktiga URL:en för kattbilder

        // Skapa en instans av den konkreta subklassen GetKittens
        GetKittens getKittens = new GetKittens(url);

        // Utför webbskrapning av kattbilder
        getKittens.scrape();
    }
}
```

I `Main`-klassen skapar vi en instans av `GetKittens`-klassen och anger den riktiga URL:en för kattbilder. Sedan anropar vi `scrape()`-metoden för att utföra webbskrapningen.

Observera att `GetKittens`-klassen använder den abstrakta klassens konstruktor genom `super(url)` för att initiera URL:en för webbskrapningen.

## Slutsats

I den här övningen har vi skapat en abstrakt klass för webbskrapning i Java och en konkret subklass för att hämta kattbilder från en specifik sida. Genom att använda abstrakta metoder kan vi separera implementationen av webbskrapningen från den abstrakta klassen och skapa en mer modulär och återanvändbar kodstruktur.

JSoup-biblioteket har varit till stor hjälp för att hantera HTML-dokumentet och filtrera ut kattbilder från webbsidan.

Nu är det dags för dig att fortsätta öva och experimentera med abstrakta klasser och webbskrapning i Java. Var inte rädd för att prova nya idéer och utmana dig själv i din programmeringsresa. Fortsätt inspireras och ha roligt med programmering! 😺💻🚀

## Termer

[Samma termlista som tidigare]

## Referenser

- [JSoup](https://jsoup.org/)
- [Java](https://www.java.com/)
- [Wikipedia](https://en.wikipedia.org/wiki/Abstract_type)
