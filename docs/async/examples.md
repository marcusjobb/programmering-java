---
title: Exempel
author: Marcus Ackre Medina
parent: Asynkron
nav_order: 10
---
# Exempel

Välkommen till en spännande resa in i asynkron programmeringens värld tillsammans med Java! Här kommer vi att utforska ett coolt exempel där vi skapar en metod för asynkron sökning i filer, vilket möjliggör effektivt sökande efter specifik text i en mapp.

### Asynkrona metoder och deras fördelar

Först och främst, låt oss ta en titt på vad asynkrona metoder faktiskt är och varför de är så fantastiska. Asynkrona metoder i Java låter oss utföra operationer parallellt utan att blockera huvudtråden. Detta innebär att vi kan köra flera metoder samtidigt och undvika att vårt program blir trögt och långsamt när vi utför långvariga operationer. Genom att använda asynkrona metoder kan vi öka responsiviteten i våra applikationer och göra dem mer användarvänliga.

### Skapa en asynkron metod för filersökning

Nu när vi har en grundläggande förståelse för asynkrona metoder, låt oss gå vidare och skapa vår egen metod för asynkron sökning i filer. Metoden vi kommer att skapa heter `searchFilesAsync`. Den tar emot en sökväg till en mapp, ett sökmönster och den text vi vill söka efter i filerna. Genom att använda `Files.walk`, får vi en ström av alla filer i den angivna sökvägen. Sedan skapar vi en lista med `CompletableFuture` som kommer att köra metoden `searchFileAsync` för varje fil asynkront.

### Hantera asynkrona operationer med CompletableFuture

För att effektivt hantera de asynkrona operationerna använder vi `CompletableFuture.allOf`. Genom att vänta på att alla asynkrona uppgifter (CompletableFuture) ska bli klara innan vi fortsätter, kan vi samla resultaten från varje `CompletableFuture` som inte är null och returnera en lista med de filer som innehåller den sökta texten.

### Utforska asynkron sökning i en enskild fil

Vi låter inte nöjet stanna där! Låt oss nu ta reda på hur vi kan söka efter den sökta texten i en enskild fil med metoden `searchFileAsync`. Denna metod tar emot sökvägen till filen och den sökta texten. Genom att använda `CompletableFuture.supplyAsync` startar vi en asynkron uppgift som kommer att läsa innehållet i filen och söka efter den angivna texten. Om texten hittas returnerar vi sökvägen till filen och radnumret där texten hittades, annars returnerar vi null.

### Applicera vår sökmetod i Main-metoden

Nu när vi har våra asynkrona metoder klara, låt oss använda dem i vår `Main`-metod för att se sökningen i aktion. Vi skapar en instans av `DirReader` och definierar sökvägen till vår mapp. Sedan kör vi metoden `searchFilesAsync` och sparar resultatet i en variabel. Slutligen skriver vi ut alla resultat i konsolen för att se vilka filer som innehåller den sökta texten.

### Exempelkod för asynkron filersökning i Java

```java
// Importera nödvändiga paket och klasser
import java.io.File;
import java.io.IOException;
import java.nine.file.Files;
import java.nine.file.Path;
import java.nine.file.Paths;
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.CompletableFuture;
import java.util.stream.Collectors;
import java.util.stream.Stream;

// Huvudklassen
public class Main {
    public static void main(String[] args) throws Exception {
        // Skapa en ny instans av DirReader-klassen
        DirReader dir = new DirReader();

        // Hämta användarens hemkatalog
        String profile = System.getProperty("user.home");

        // Definiera sökvägen till källmappen
        String source = Paths.get(profile, "source").toString();

        // Sök efter alla .java-filer i källmappen asynkront
        List<String> result = dir.searchFilesAsync(source, "*.java", "asynkron").get();

        // Skriv ut resultaten till konsolen
        System.out.println(String.join(System.lineSeparator(), result));
    }
}

// Hjälpklassen för filersökning
class DirReader {
    // Sök efter alla filer i en mapp som matchar ett angivet mönster och innehåller en viss text asynkront
    public CompletableFuture<List<String>> searchFilesAsync(String path, String searchPattern, String searchText) {
        try (Stream<Path> paths = Files.walk(Paths.get(path))) {
            // Skapa en lista med uppgifter för att söka varje fil asynkront
            List<CompletableFuture<String>> tasks = paths
                    .filter(Files::isRegularFile) // Endast vanliga filer beaktas
                    .filter(p -> p.getFileName().toString().endsWith(searchPattern)) // Endast filer som matchar sökmönstret beaktas
                    .map(p -> searchFileAsync(p.toString(), searchText)) // Sök i varje fil asynkront
                    .collect(Collectors.toList());

            // Vänta på att alla uppgifter ska slutföras och samla resultaten
            CompletableFuture<Void> allTasks = CompletableFuture.allOf(tasks.toArray(new CompletableFuture[tasks.size()]));
            return allTasks.thenApply(v -> tasks.stream()
                    .map(CompletableFuture::join)
                    .filter(x -> x != null)
                    .collect(Collectors.toList()));
        } catch (IOException e) {
            // Om ett fel inträffar, returnera ett misslyckat CompletableFuture med undantaget
            e.printStackTrace();
            return CompletableFuture.failedFuture(e);
        }
    }

    // Sök efter en given text i en enskild fil asynkront och returnera resultatet
    public CompletableFuture<String> searchFileAsync(String path, String searchText) {
        return CompletableFuture.supplyAsync(() -> {
            try {
                // Läs in alla rader i filen
                List<String> lines = Files.readAllLines(Paths.get(path));

                // Sök efter texten i filen
                int index = lines.indexOf(searchText);

                // Om texten hittas, returnera filens sökväg och radnummer
                return index >= 0 ? path + " - " + index : null;
            } catch (IOException e) {
                // Om ett fel inträffar, returnera null
                e.printStackTrace();
                return null;
            }
        });
    }
}
```

### Slutsats: Framtiden är asynkron!

Genom att använda asynkrona metoder kan vi skapa mer responsiva och effektiva applikationer. I vårt exempel har vi sett hur vi kan söka igenom filer asynkront och samtidigt undvika att blockera huvudtråden. Asynkron programmering är användbart för uppgifter som tar tid, som att söka igenom filer eller kommunicera med externa system. Genom att utnyttja asynkrona metoder kan vi skapa applikationer som är mer responsiva, effektiva och skalbara.

### Termtabell: Få koll på begreppen

- **Asynkrona metoder**: Metoder som inte blockerar tråden och tillåter parallell exekvering av flera metoder samtidigt.
- **Responsivitet**: Förmågan hos en applikation att snabbt svara på användarinteraktioner och andra händelser.
- **Parallellism**: Exekvering av flera operationer samtidigt för att utnyttja flera processorkärnor och förbättra prestanda.
- **Skalbarhet**: Förmågan hos en applikation att hantera en ökad arbetsbelastning och trafik utan att försämra prestanda och responsivitet.

### Slutord: Fortsätt utforska och ha kul!

Det är verkligen fantastiskt att kunna använda asynkron programmering för att förbättra responsiviteten och effektiviteten i våra applikationer. Som programmerare är det alltid viktigt att fortsätta utforska och lära sig nya saker. Så fortsätt koda med glädje och upptäck de många möjligheterna med asynkron programmering!

### Obligatorisk Dad-joke: Lite humor för vägen!

Varför kallas asynkrona metoder för "coola"?

För att de jobbar i sin egen "takt"!
