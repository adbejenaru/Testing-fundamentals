Conceptul de `Given-When-Then` este un tipar de scriere a testelor utilizat frecvent în dezvoltarea software, în special în testarea comportamentului (Behavior-Driven Development - BDD). Acest tipar ajută la structurarea testelor într-un mod clar și ușor de înțeles, atât pentru dezvoltatori, cât și pentru părțile interesate non-tehnice. Iată o explicație detaliată a acestui tipar, aplicată în contextul testării în Java:

### Structura `Given-When-Then`

1. **Given (Dat fiind)**: Configurarea stării inițiale a sistemului sau a contextului de testare. Aici se pregătește tot ceea ce este necesar pentru test, cum ar fi inițializarea obiectelor, setarea valorilor de intrare și orice altă configurare necesară.
   
2. **When (Când)**: Acțiunea specifică pe care o testezi. Aceasta este operația sau metoda pe care dorești să o verifici, cum ar fi apelarea unei metode sau trimiterea unei cereri.

3. **Then (Atunci)**: Verificarea rezultatelor acțiunii. Aici se verifică dacă rezultatele sunt conforme cu așteptările definite. Se folosesc afirmații (assertions) pentru a compara rezultatele obținute cu cele așteptate.

### Exemplu de Test `Given-When-Then` în Java

Să presupunem că vrem să testăm metoda `divide` din clasa `Calculator` pe care am discutat-o anterior.

#### Clasa `Calculator`

```java
package org.calculator;

public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public int subtract(int a, int b) {
        return a - b;
    }

    public int multiply(int a, int b) {
        return a * b;
    }

    public int divide(int a, int b) {
        if (b == 0) {
            throw new IllegalArgumentException("Cannot divide by zero");
        }
        return a / b;
    }
}
```

#### Testul `Given-When-Then`

Vom folosi JUnit pentru a scrie testele noastre în Java. Iată un exemplu de test pentru metoda `divide`:

```java
import org.calculator.Calculator;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {

    @Test
    public void testDivide() {
        // Given
        Calculator calculator = new Calculator();
        int a = 10;
        int b = 2;

        // When
        int result = calculator.divide(a, b);

        // Then
        assertEquals(5, result);
    }

    @Test
    public void testDivideByZero() {
        // Given
        Calculator calculator = new Calculator();
        int a = 10;
        int b = 0;

        // When & Then
        Exception exception = assertThrows(IllegalArgumentException.class, () -> {
            calculator.divide(a, b);
        });

        assertEquals("Cannot divide by zero", exception.getMessage());
    }
}
```

### Explicație Exemplu

1. **Testul `testDivide`**:
    - **Given**: Inițializează un obiect `Calculator` și definește valorile `a` și `b`.
    - **When**: Apelează metoda `divide` cu valorile `a` și `b`.
    - **Then**: Verifică dacă rezultatul este `5` folosind `assertEquals`.

2. **Testul `testDivideByZero`**:
    - **Given**: Inițializează un obiect `Calculator` și definește valorile `a` și `b` (unde `b` este `0`).
    - **When & Then**: Apelează metoda `divide` și verifică dacă aruncă o excepție `IllegalArgumentException`. De asemenea, verifică dacă mesajul excepției este "Cannot divide by zero".

### Beneficiile Tiparului `Given-When-Then`

- **Claritate**: Structurarea testelor în acest mod face ca intenția testului să fie clară și ușor de înțeles.
- **Separare**: Separă clar starea inițială, acțiunea și rezultatele așteptate, ceea ce ajută la identificarea rapidă a problemei în caz de eșec al testului.
- **Comunicare**: Este un mod eficient de a comunica comportamentul așteptat atât dezvoltatorilor, cât și părților interesate non-tehnice.

Prin utilizarea tiparului `Given-When-Then`, testele devin mai structurate și mai intuitive, facilitând atât dezvoltarea, cât și întreținerea codului de testare.
