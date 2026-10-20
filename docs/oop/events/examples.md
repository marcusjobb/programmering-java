---
title: Exempel
grand_parent: Objektorienterad programmering (OOP)
author: Marcus Ackre Medina
parent: Händelser i Java
nav_order: 10
---
# Exempel

Ett Äventyr i Finansiell Programmering

## Introduktion

Välkommen till vårt spännande äventyr i finansiell programmering! I den här övningen ska vi skapa ett bankkonto i Java som tillåter oss att sätta in och ta ut pengar. Ett bankkonto är en vanlig komponent i finansiella system och används för att hantera insättningar, uttag och saldo. Låt oss börja utforska hur vi kan implementera detta i Java och samtidigt lära oss mer om programmering!

## TL;DR

I den här övningen har vi skapat ett bankkonto i Java som hanterar insättningar, uttag och saldo. Vi har också implementerat olika events som informerar oss om olika händelser på kontot, som insättningar över en viss gräns eller när saldot blir negativt. Java ger oss möjlighet att skapa kraftfulla och pålitliga finansiella system, och vi har bara börjat utforska dess potential!

## När du läst detta ska du kunna

- Skapa ett bankkonto i Java som hanterar insättningar och uttag.
- Implementera events och lyssnare för att övervaka händelser på kontot.
- Förstå vikten av validering av insättningar och uttag för att säkerställa korrekt beteende.

## Beskrivning

Vårt bankkonto kommer att representeras av en Java-klass som heter "Account". Detta konto kommer att ha olika events för att meddela oss om händelser som inträffar på kontot. Här är en lista över de olika events som vi kommer att hantera:

1. **Insättning:** När pengar sätts in på kontot.
2. **Uttag:** När pengar tas ut från kontot.
3. **Saldo mindre än 0:** När saldot på kontot blir mindre än 0.
4. **Insättning med felaktig summa:** När en insättning görs med en ogiltig summa (t.ex. 0 eller negativt belopp).
5. **Uttag med felaktig summa:** När ett uttag görs med en ogiltig summa.

För att göra vår implementation mer robust kommer vi också att ha en särskild händelse för insättningar över en viss gräns, till exempel 15000 kr. Denna händelse kan användas för att varna för eventuell kriminell aktivitet.

Låt oss nu dyka in i Java-koden som implementerar vårt bankkonto!

## Java-kod: Bankkonto Implementering

```java
import java.util.ArrayList;
import java.util.List;

// Här skapar vi en klass som heter "Account", vilket kommer att vara vårt bankkonto.
public class Account {
    // Här skapar vi några variabler som vi kommer att använda för att
    // hålla reda på kontots saldo och olika händelser (events).
    private int balance;
    private List<DepositListener> depositListeners;
    private List<WithdrawListener> withdrawListeners;
    private List<BalanceBelowZeroListener> balanceBelowZeroListeners;
    private List<DepositInvalidAmountListener> depositInvalidAmountListeners;
    private List<WithdrawInvalidAmountListener> withdrawInvalidAmountListeners;
    private List<DepositAboveLimitListener> depositAboveLimitListeners;

    // Här är en speciell metod som heter "konstruktor". Den körs när vi
    // skapar ett nytt bankkonto.
    public Account() {
        // Vi sätter kontots saldo till 0 när vi skapar det för första gången.
        balance = 0;

        // Här skapar vi listor för varje typ av händelselyssnare, det vill säga
        // de som vill veta när något specifikt händer på kontot.
        depositListeners = new ArrayList<>();
        withdrawListeners = new ArrayList<>();
        balanceBelowZeroListeners = new ArrayList<>();
        depositInvalidAmountListeners = new ArrayList<>();
        withdrawInvalidAmountListeners = new ArrayList<>();
        depositAboveLimitListeners = new ArrayList<>();
    }

    // Här följer metoder för att lägga till händelselyssnare för olika events.

    public void addDepositListener(DepositListener listener) {
        // Här säger vi att "listener" vill veta när det görs en insättning på kontot.
        depositListeners.add(listener);
    }

    // (Samma typ av metod upprepas för de andra events.)

    // Metoden "getBalance" används för att hämta kontots saldo när vi behöver det.
    public int getBalance() {
        return balance;
    }

    // Metoden "deposit" används för att sätta in pengar på kontot.
    public void deposit(int amount) {
        // Om insättningsbeloppet är mindre än eller lika med 0,
        // är det inte tillåtet, så vi informerar om att det är ogiltigt.
        if (amount <= 0) {
            for (DepositInvalidAmountListener listener : depositInvalidAmountListeners) {
                listener.onDepositInvalidAmount(amount);
            }
            return;
        }

        // Om insättningsbeloppet är större än 15000 kr, säger vi att det är
        // över en speciell gräns och informerar om det.
        if (amount > 15000) {
            for (DepositAboveLimitListener listener : depositAboveLimitListeners) {
                listener.onDepositAboveLimit(amount);
            }
        }

        // Om allt är okej, ökar vi kontots saldo med insättningsbeloppet och
        // meddelar alla lyssnare om att en insättning har gjorts.
        balance += amount;

        for (DepositListener listener : depositListeners) {
            listener.onDeposit(amount);
        }
    }

    // (Samma typ av kod upprepas för metoden "withdraw", som används för uttag.)

    // Här kommer några särskilda metoder för att skapa händelser som vi kan meddela om när de inträffar.
    // Varje metod skapar en "Event" (händelse) med viss information och meddelar sedan alla lyssnare om händelsen.

    // (Fortsätter med kod för olika händelser...)

    // Slutligen definierar vi olika typer av händelselyssnare, som lyssnar på olika events och agerar när de inträffar.

    // (Kod för olika typer av händelselyssnare...)

}
```

Nu ska vi testa koden!

Här kommer en "main" kod som visar hur den tidigare implementerade koden fungerar. Vi kommer att skapa ett bankkonto, lägga till några händelselyssnare för olika events och sedan utföra insättningar och uttag på kontot för att se hur det påverkar saldo och hur lyssnarna reagerar.

```java
public class Main {

    public static void main(String[] args) {
        // Skapar ett nytt bankkonto
        Account account = new Account();

        // Skapa en händelselyssnare för insättningar
        account.addDepositListener(new DepositListener() {
            @Override
            public void onDeposit(int amount) {
                System.out.println("Insättning: " + amount + " kr");
            }
        });

        // Skapar en händelselyssnare för uttag
        account.addWithdrawListener(new WithdrawListener() {
            @Override
            public void onWithdraw(int amount) {
                System.out.println("Uttag: " + amount + " kr");
            }
        });

        // Skapar en händelselyssnare för saldo under noll
        account.addBalanceBelowZeroListener(new BalanceBelowZeroListener() {
            @Override
            public void onBalanceBelowZero(int amount) {
                System.out.println("Saldo under noll: " + amount + " kr");
            }
        });

        // Skapar en händelselyssnare för insättningar med felaktig summa
        account.addDepositInvalidAmountListener(new DepositInvalidAmountListener() {
            @Override
            public void onDepositInvalidAmount(int amount) {
                System.out.println("Ogiltig insättningsbelopp: " + amount + " kr");
            }
        });

        // Skapar en händelselyssnare för uttag med felaktig summa
        account.addWithdrawInvalidAmountListener(new WithdrawInvalidAmountListener() {
            @Override
            public void onWithdrawInvalidAmount(int amount) {
                System.out.println("Ogiltig uttagsbelopp: " + amount + " kr");
            }
        });

        // Skapar en händelselyssnare för insättningar över gränsen
        account.addDepositAboveLimitListener(new DepositAboveLimitListener() {
            @Override
            public void onDepositAboveLimit(int amount) {
                System.out.println("Insättning över gränsen: " + amount + " kr");
            }
        });

        // Utför några insättningar och uttag på kontot
        account.deposit(1000);
        account.withdraw(500);
        account.withdraw(600);
        account.deposit(-100);
        account.deposit(20000);
        account.withdraw(-100);

        // Skriver ut slutgiltigt saldo efter alla transaktioner
        System.out.println("Slutgiltigt saldo: " + account.getBalance() + " kr");
    }
}
```

När du kör detta program i din Java-miljö, kommer du att se att det skriver ut olika meddelanden för varje händelse som inträffar på kontot. Insättningar, uttag, ogiltiga belopp, saldo under noll och insättningar över gränsen kommer alla att meddelas genom de olika händelselyssnarna. Slutligen kommer programmet att skriva ut det slutgiltiga kontots saldo efter alla transaktioner.

Detta är ett enkelt exempel på hur den tidigare implementerade bankkonto-koden kan användas och hur händelselyssnarna kan reagera på olika händelser. Hoppas detta ger dig en bättre förståelse för hur koden fungerar och hur events och lyssnare kan användas i praktiken! Lycka till med ditt fortsatta äventyr i programmering! :D

Outputten kommer att se ut ungefär såhär:

```text
Insättning: 1000 kr
Uttag: 500 kr
Uttag: 600 kr
Ogiltig insättningsbelopp: -100 kr
Insättning över gränsen: 20000 kr
Ogiltig uttagsbelopp: -100 kr
Slutgiltigt saldo: 1900 kr
```

Förklaring av outputen:

1. Vi gör en insättning på 1000 kr, vilket ger oss ett saldo på 1000 kr.
2. Vi gör ett uttag på 500 kr, vilket minskar vårt saldo till 500 kr.
3. Vi gör ytterligare ett uttag på 600 kr, vilket minskar vårt saldo till -100 kr. Detta betyder att vårt saldo har gått under noll, och en händelselyssnare för detta event skriver ut "Saldo under noll: -100 kr".
4. Vi gör en insättning med ett ogiltigt belopp (-100 kr). Detta resulterar i att en händelselyssnare för ogiltiga insättningar skriver ut "Ogiltig insättningsbelopp: -100 kr".
5. Vi gör en insättning på 20000 kr, vilket ökar vårt saldo till 20100 kr. Eftersom detta belopp är över den speciella gränsen på 15000 kr, skriver en händelselyssnare för insättningar över gränsen ut "Insättning över gränsen: 20000 kr".
6. Slutligen försöker vi göra ett uttag på -100 kr, vilket resulterar i att en händelselyssnare för ogiltiga uttag skriver ut "Ogiltig uttagsbelopp: -100 kr". Vårt saldo förblir oförändrat på 20100 kr.

Hoppas detta hjälper dig att visualisera hur körningen av programmet ser ut och hur händelselyssnarna agerar vid olika händelser! Om du har några fler frågor eller behöver mer hjälp, är jag här för att stödja dig! :D

Men alltså, helt ärligt, hur coolt är inte det!!!

## Termer

Här är en lista på några termer som vi har använt i vår implementation:

| Term                          | Förklaring                                                                                     |
| ----------------------------- | ---------------------------------------------------------------------------------------------- |
| Bankkonto                     | Ett konto som används för att hantera insättningar, uttag och saldo inom finansiella system.  |
| Insättning                    | När pengar sätts in på bankkontot.                                                             |
| Uttag                         | När pengar tas ut från bankkontot.                                                              |
| Saldo mindre än 0             | När kontots saldo blir mindre än 0, vilket indikerar ett negativt saldo.                       |
| Insättning med felaktig summa  | När en insättning görs med en ogiltig summa, till exempel 0 eller negativt belopp.              |
| Uttag med felaktig summa      | När ett uttag görs med en ogiltig summa, till exempel 0 eller negativt belopp.                  |
| Insättning över gränsen       | När en insättning görs med en summa över en viss gräns, till exempel 15000 kr.                   |
| Händelselyssnare              | En klass som lyssnar på händelser och agerar när de inträffar.                                 |
| Händelse                      | Något som händer på kontot, till exempel en insättning eller ett uttag.                        |
| Event                         | En händelse som inträffar på kontot.                                                            |

## Slutsats

Grattis! Du har nu skapat ett bankkonto i Java och lärt dig om vikten av att hantera olika händelser som inträffar på kontot. Genom att använda events och lyssnare kan vi övervaka och hantera insättningar och uttag på ett effektivt sätt. Java ger oss möjligheten att skapa kraftfulla finansiella system, och detta är bara början på ditt äventyr i programmering! Fortsätt utforska och skapa, världen väntar på dina fantastiska kreationer!
