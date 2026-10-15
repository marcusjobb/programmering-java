---
title: Budgetexempel
author: Marcus Ackre Medina
parent: Testa din kod
nav_order: 30
---
# Budgetexempel

Vi ska nu utforska hur du kan använda TDD-metodiken för att skapa en budgetapplikation som hjälper användare att hålla koll på sina inkomster och utgifter per månad. Vi kommer att gå igenom processen steg för steg, börjande med att skapa pseudoklasser med tomma metoder, sedan skriva testerna för att säkerställa att allt fungerar som förväntat, och till sist implementera funktionaliteten för applikationen.

### Pseudoklasser med tomma metoder

Först börjar vi med att skapa pseudoklasser som representerar `Income` (inkomst) och `Expense` (utgift) utan att implementera några faktiska funktioner. Dessa klasser kommer att fungera som våra modeller för att hantera inkomst- och utgiftsdata.

```java
public class Income {
    public void Income(double amount, String description, String date) {
    }

    public double getAmount() {return 0;}
    public String getDescription() {return 0;}
    public String getDate() {return 0;}
}

public class Expense {
    public void Expense(double amount, String description, String date) {
    }

    public double getAmount() {return 0;}
    public String getDescription() {return 0;}
    public String getDate() {return 0;}
}

public class Budget {
    // Tomma metoder för pseudoklassen
    public void addIncome(Income income) {

    }

    public void addExpense(Expense expense) {

    }

    public String printBudget() {
        return null;
    }
}
```

### Testfall för Budgetapplikationen

Nu när vi har våra pseudoklasser, ska vi skriva testfall för att säkerställa att våra framtida implementationer fungerar som förväntat. Vi kommer att använda JUnit för att skapa våra testfall.

```java
import org.junit.Test;
import static org.junit.Assert.assertEquals;

public class BudgetTest {
    private Budget budget;
    @beforeTest
    public void setUp() {
        // Skapa instanser av pseudoklasserna
        budget = new Budget();
        budget.addIncome(new Income(1000, "Startdeposition", "2021-01-01"));
    }
    @Test
    public void testAddIncome() {
        // Testfall för att testa lägg till inkomst
        budget.addIncome(new Income(100, "Swish", "2021-01-01"));
        assertEquals(1000, budget.getIncome());
    }

    @Test
    public void testAddExpense() {
        // Testfall för att testa lägg till utgift
        budget.addExpense(new Expense(100, "Mat", "2021-01-01"));
        assertEquals(100, budget.getExpense());
    }

    @Test
    public void testPrintBudget() {
        // Testfall för att testa utskrift av budget
        String output = budget.printBudget();
        assertEquals("Inkomster: 1000\nUtgifter: 100\n", output);
    }
}
```

### Implementering av Budgetapplikationen

Nu är det dags att implementera funktionaliteten för vår Budgetapplikation med hjälp av TDD-metoden. Vi börjar med att implementera metoderna för att lägga till inkomster och utgifter i `Budget`-klassen.

```java
import java.util.ArrayList;
import java.util.List;

import java.text.DecimalFormat;
import java.text.MessageFormat;
import java.util.ArrayList;
import java.util.List;
import java.util.StringJoiner;

public class Budget {
    private List<Income> incomes;
    private List<Expense> expenses;

    public Budget() {
        incomes = new ArrayList<>();
        expenses = new ArrayList<>();
    }

    public void addIncome(Income income) {
        incomes.add(income);
    }

    public void addExpense(Expense expense) {
        expenses.add(expense);
    }

    public String printBudget() {
        double totalIncome = incomes.stream().mapToDouble(Income::getAmount).sum();
        double totalExpense = expenses.stream().mapToDouble(Expense::getAmount).sum();
        double balance = totalIncome - totalExpense;

        StringBuilder sb = new StringBuilder();
        sb.append("Budget Overview\n");
        sb.append("=================\n");

        sb.append("\nIncome\n");
        for (Income income : incomes) {
            sb.append(String.format("Description: %s, Amount: %.2f, Category: %s\n",
                    income.getDescription(), income.getAmount(), income.getCategory()));
        }

        sb.append("\nExpenses\n");
        for (Expense expense : expenses) {
            sb.append(String.format("Description: %s, Amount: %.2f, Category: %s\n",
                    expense.getDescription(), expense.getAmount(), expense.getCategory()));
        }

        sb.append("\nSummary\n");
        sb.append("---------------\n");
        sb.append(MessageFormat.format("Total Income: {0}\n", formatAmount(totalIncome)));
        sb.append(MessageFormat.format("Total Expenses: {0}\n", formatAmount(totalExpense)));
        sb.append(MessageFormat.format("Balance: {0}\n", formatAmount(balance)));

        return sb.toString();
    }

    private String formatAmount(double amount) {
        DecimalFormat decimalFormat = new DecimalFormat("#,##0.00");
        return decimalFormat.format(amount);
    }
}
```

### Avslutning

Grattis! Nu har du skapat en Budgetapplikation genom Test-driven Development i Java. Du började med
att skapa pseudoklasser med tomma metoder, skrev sedan testfall för att säkerställa funktionalitet,
och avslutade med att implementera applikationen. Test-driven Development är en kraftfull metodik
som hjälper dig att bygga robusta och pålitliga applikationer.

Fortsätt att öva och experimentera med TDD-metoden och Java-programmering för att förbättra dina
färdigheter och bli en ännu skickligare utvecklare!

### Obligatorisk dad joke:

Varför gillar programmerare att arbeta sent på kvällen? <br> För att kodningen är bättre när det är
nattklasser!
