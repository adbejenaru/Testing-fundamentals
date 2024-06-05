Sigur, să luăm un alt exemplu. Vom crea o nouă clasă `BankAccount` care va reprezenta un cont bancar și vom testa metoda de retragere (`withdraw`). Vom utiliza același tipar `Given-When-Then` pentru a structura testele.

### Clasa `BankAccount`

```java
package org.bank;

public class BankAccount {
    private double balance;

    public BankAccount(double initialBalance) {
        if (initialBalance < 0) {
            throw new IllegalArgumentException("Initial balance cannot be negative");
        }
        this.balance = initialBalance;
    }

    public double getBalance() {
        return balance;
    }

    public void deposit(double amount) {
        if (amount < 0) {
            throw new IllegalArgumentException("Deposit amount cannot be negative");
        }
        balance += amount;
    }

    public void withdraw(double amount) {
        if (amount < 0) {
            throw new IllegalArgumentException("Withdrawal amount cannot be negative");
        }
        if (amount > balance) {
            throw new IllegalArgumentException("Insufficient funds");
        }
        balance -= amount;
    }
}
```

### Teste `Given-When-Then`

Vom folosi JUnit pentru a scrie testele pentru metoda `withdraw`.

#### Testele `BankAccountTest`

```java
import org.bank.BankAccount;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class BankAccountTest {

    @Test
    public void testWithdraw() {
        // Given
        BankAccount account = new BankAccount(100.0);
        double amountToWithdraw = 50.0;

        // When
        account.withdraw(amountToWithdraw);

        // Then
        assertEquals(50.0, account.getBalance());
    }

    @Test
    public void testWithdrawInsufficientFunds() {
        // Given
        BankAccount account = new BankAccount(100.0);
        double amountToWithdraw = 150.0;

        // When & Then
        Exception exception = assertThrows(IllegalArgumentException.class, () -> {
            account.withdraw(amountToWithdraw);
        });

        assertEquals("Insufficient funds", exception.getMessage());
    }

    @Test
    public void testWithdrawNegativeAmount() {
        // Given
        BankAccount account = new BankAccount(100.0);
        double amountToWithdraw = -50.0;

        // When & Then
        Exception exception = assertThrows(IllegalArgumentException.class, () -> {
            account.withdraw(amountToWithdraw);
        });

        assertEquals("Withdrawal amount cannot be negative", exception.getMessage());
    }
}
```

### Explicație Exemplu

1. **Testul `testWithdraw`**:
    - **Given**: Inițializează un cont bancar `BankAccount` cu un sold inițial de `100.0` și definește suma de retras `50.0`.
    - **When**: Apelează metoda `withdraw` cu suma de `50.0`.
    - **Then**: Verifică dacă soldul contului este `50.0` folosind `assertEquals`.

2. **Testul `testWithdrawInsufficientFunds`**:
    - **Given**: Inițializează un cont bancar `BankAccount` cu un sold inițial de `100.0` și definește suma de retras `150.0`.
    - **When & Then**: Apelează metoda `withdraw` și verifică dacă aruncă o excepție `IllegalArgumentException` cu mesajul "Insufficient funds".

3. **Testul `testWithdrawNegativeAmount`**:
    - **Given**: Inițializează un cont bancar `BankAccount` cu un sold inițial de `100.0` și definește suma de retras `-50.0`.
    - **When & Then**: Apelează metoda `withdraw` și verifică dacă aruncă o excepție `IllegalArgumentException` cu mesajul "Withdrawal amount cannot be negative".

### Beneficiile acestui tipar

Aceste teste structurate în formatul `Given-When-Then` fac codul de testare mai lizibil și ușor de înțeles. Prin separarea clară a fiecărei etape, putem vedea exact ce condiții inițiale sunt stabilite, ce acțiuni sunt întreprinse și ce rezultate sunt așteptate, ceea ce facilitează diagnosticarea problemelor și îmbunătățirea calității codului.
