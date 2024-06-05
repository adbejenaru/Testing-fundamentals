`Assertions` sunt o parte esențială a testării unitare, folosite pentru a verifica dacă rezultatele unui test sunt cele așteptate. În contextul JUnit, `assertions` sunt metode statice care evaluează anumite condiții și, în funcție de rezultat, marchează testul ca fiind trecut sau eșuat. Dacă o aserțiune eșuează, testul este marcat ca eșuat și se afișează un mesaj de eroare specific.

### Tipuri de Assertions în JUnit

JUnit oferă o varietate de metode de aserțiune pentru a verifica diferite condiții. Iată câteva dintre cele mai utilizate:

1. **`assertEquals`**: Verifică dacă două valori sunt egale.
    ```java
    assertEquals(expected, actual);
    ```

2. **`assertNotEquals`**: Verifică dacă două valori nu sunt egale.
    ```java
    assertNotEquals(unexpected, actual);
    ```

3. **`assertTrue`**: Verifică dacă o condiție este adevărată.
    ```java
    assertTrue(condition);
    ```

4. **`assertFalse`**: Verifică dacă o condiție este falsă.
    ```java
    assertFalse(condition);
    ```

5. **`assertNull`**: Verifică dacă un obiect este `null`.
    ```java
    assertNull(object);
    ```

6. **`assertNotNull`**: Verifică dacă un obiect nu este `null`.
    ```java
    assertNotNull(object);
    ```

7. **`assertSame`**: Verifică dacă două referințe indică același obiect.
    ```java
    assertSame(expected, actual);
    ```

8. **`assertNotSame`**: Verifică dacă două referințe nu indică același obiect.
    ```java
    assertNotSame(unexpected, actual);
    ```

9. **`assertThrows`**: Verifică dacă o anumită excepție este aruncată.
    ```java
    assertThrows(expectedException.class, () -> {
        // codul care ar trebui să arunce excepția
    });
    ```

10. **`assertAll`**: Permite gruparea mai multor aserțiuni care vor fi toate evaluate, raportând toate eșecurile.
    ```java
    assertAll("heading",
        () -> assertEquals(1, 1),
        () -> assertTrue(true),
        () -> assertNotNull(new Object())
    );
    ```

### Exemple de utilizare

Să vedem câteva exemple practice de utilizare a aserțiunilor în JUnit.

#### Exemplu de test simplu

Vom testa metodele din clasa `Calculator`.

```java
import org.calculator.Calculator;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {

    @Test
    public void testAdd() {
        Calculator calculator = new Calculator();
        int result = calculator.add(2, 3);
        assertEquals(5, result);
    }

    @Test
    public void testSubtract() {
        Calculator calculator = new Calculator();
        int result = calculator.subtract(5, 3);
        assertEquals(2, result);
    }

    @Test
    public void testMultiply() {
        Calculator calculator = new Calculator();
        int result = calculator.multiply(4, 5);
        assertEquals(20, result);
    }

    @Test
    public void testDivide() {
        Calculator calculator = new Calculator();
        int result = calculator.divide(10, 2);
        assertEquals(5, result);
    }

    @Test
    public void testDivideByZero() {
        Calculator calculator = new Calculator();
        Exception exception = assertThrows(IllegalArgumentException.class, () -> {
            calculator.divide(10, 0);
        });
        assertEquals("Cannot divide by zero", exception.getMessage());
    }
}
```

### Explicația exemplului

1. **`testAdd`**:
    - Creează un obiect `Calculator`.
    - Apelează metoda `add` cu valorile `2` și `3`.
    - Verifică dacă rezultatul este `5` folosind `assertEquals`.

2. **`testSubtract`**:
    - Creează un obiect `Calculator`.
    - Apelează metoda `subtract` cu valorile `5` și `3`.
    - Verifică dacă rezultatul este `2` folosind `assertEquals`.

3. **`testMultiply`**:
    - Creează un obiect `Calculator`.
    - Apelează metoda `multiply` cu valorile `4` și `5`.
    - Verifică dacă rezultatul este `20` folosind `assertEquals`.

4. **`testDivide`**:
    - Creează un obiect `Calculator`.
    - Apelează metoda `divide` cu valorile `10` și `2`.
    - Verifică dacă rezultatul este `5` folosind `assertEquals`.

5. **`testDivideByZero`**:
    - Creează un obiect `Calculator`.
    - Verifică dacă metoda `divide` aruncă o excepție `IllegalArgumentException` când `b` este `0`.
    - Verifică dacă mesajul excepției este "Cannot divide by zero" folosind `assertEquals`.

### Concluzie

Aserțiunile în JUnit sunt instrumente esențiale pentru verificarea rezultatelor testelor unitare. Ele permit dezvoltatorilor să verifice dacă metodele funcționează corect și să identifice rapid problemele atunci când rezultatele nu sunt cele așteptate. Utilizarea corectă a aserțiunilor face ca testele să fie mai clare, mai ușor de întreținut și mai eficiente.
