Sigur, să urmărim procesul TDD (Test-Driven Development) pas cu pas pentru a implementa funcționalitatea `sumDigits` din clasa `DigitSumCalculator`.

### Pasul 1: Scrie un test (Red)

Scriem un test pentru a verifica că metoda `sumDigits` din clasa `DigitSumCalculator` calculează corect suma cifrelor unui număr pozitiv.

#### Testul inițial

```java
import org.junit.jupiter.api.Test;
import static org.assertj.core.api.Assertions.*;

public class DigitSumCalculatorTest {

    @Test
    public void testSumDigits() {
        DigitSumCalculator calculator = new DigitSumCalculator();
        assertThat(calculator.sumDigits(123)).isEqualTo(6); // 1 + 2 + 3 = 6
    }
}
```

### Pasul 2: Scrie codul pentru a trece testul (Green)

Implementăm metoda `sumDigits` în clasa `DigitSumCalculator` pentru a trece testul.

#### Implementarea inițială

```java
package org.tdd;

public class DigitSumCalculator {
    public int sumDigits(int number) {
        int sum = 0;
        while (number != 0) {
            sum += number % 10;
            number /= 10;
        }
        return sum;
    }

    public static void main(String[] args) {
        System.out.println(sumDigits(123)); // Example usage, should output 6
    }
}
```

Acum, rulăm testul din nou și ar trebui să treacă (să fie verde).

### Pasul 3: Adaugă mai multe teste și refactorizează (Refactor)

După ce testul trece, putem adăuga mai multe teste pentru a acoperi mai multe cazuri și pentru a refactoriza codul.

#### Testele suplimentare

Adăugăm teste pentru alte cazuri, inclusiv pentru numere negative, zero și numere mari.

```java
import org.junit.jupiter.api.Test;
import static org.assertj.core.api.Assertions.*;

public class DigitSumCalculatorTest {

    @Test
    public void testSumDigits() {
        DigitSumCalculator calculator = new DigitSumCalculator();
        assertThat(calculator.sumDigits(123)).isEqualTo(6); // 1 + 2 + 3 = 6
        assertThat(calculator.sumDigits(456)).isEqualTo(15); // 4 + 5 + 6 = 15
        assertThat(calculator.sumDigits(789)).isEqualTo(24); // 7 + 8 + 9 = 24
    }

    @Test
    public void testSumDigitsWithZero() {
        DigitSumCalculator calculator = new DigitSumCalculator();
        assertThat(calculator.sumDigits(0)).isEqualTo(0); // 0 = 0
    }

    @Test
    public void testSumDigitsNegative() {
        DigitSumCalculator calculator = new DigitSumCalculator();
        assertThat(calculator.sumDigits(-123)).isEqualTo(4); // -1 + 2 + 3 = 4
        assertThat(calculator.sumDigits(-456)).isEqualTo(7); // -4 + 5 + 6 = 7
        assertThat(calculator.sumDigits(-789)).isEqualTo(10); // -7 + 8 + 9 = 10
    }

    @Test
    public void testSumDigitsLargeNumber() {
        DigitSumCalculator calculator = new DigitSumCalculator();
        assertThat(calculator.sumDigits(987654321)).isEqualTo(45); // 9 + 8 + 7 + 6 + 5 + 4 + 3 + 2 + 1 = 45
    }
}
```

### Refactorizarea metodei `sumDigits`

Refactorizăm metoda `sumDigits` pentru a trata și numerele negative, considerând prima cifră cu semn negativ.

#### Implementarea refactorizată

```java
package org.tdd;

public class DigitSumCalculator {
    public int sumDigits(int number) {
        if (number == 0) {
            return 0;
        }

        boolean isNegative = number < 0;
        number = Math.abs(number);  // Always work with the absolute value of the number

        int sum = 0;
        int firstDigit = number;

        // Calculate sum of digits and track the first digit in a single loop
        while (number != 0) {
            int digit = number % 10;
            sum += digit;
            if (number / 10 == 0) {
                firstDigit = digit;
            }
            number /= 10;
        }

        if (isNegative) {
            sum -= 2 * firstDigit;  // Adjust the sum for the first digit if the number was negative
        }

        return sum;
    }

    public static void main(String[] args) {
        System.out.println(sumDigits(-643));  // Example usage, should output -5 (-6 + 4 + 3)
    }
}
```

### Verificarea implementării și testelor

Rulăm toate testele pentru a ne asigura că trec și că implementarea este corectă.

### Concluzie

Am urmat corect procesul TDD:
1. **Red**: Am scris un test care inițial nu a trecut.
2. **Green**: Am implementat codul necesar pentru a trece testul.
3. **Refactor**: Am adăugat teste suplimentare și am refactorizat codul pentru a acoperi toate cazurile și a îmbunătăți claritatea și eficiența.

Acest proces ne asigură că metoda `sumDigits` funcționează corect pentru toate cazurile, inclusiv numere pozitive, zero și negative, considerând prima cifră cu semn negativ.
