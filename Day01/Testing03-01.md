JUnit 5 este o platformă de testare pentru limbajul de programare Java, folosită pentru a scrie și a executa teste unitare. Este succesorul versiunii JUnit 4 și aduce multe îmbunătățiri și noi caracteristici. JUnit 5 este de fapt un grup de mai multe module și componente, care împreună formează o platformă flexibilă și extensibilă pentru testare.

### Componentele JUnit 5

JUnit 5 este format din trei sub-proiecte principale:

1. **JUnit Platform**:
    - Este fundația pe care rulează framework-urile de testare.
    - Oferă un API pentru a descoperi și a executa teste.
    - Suportă integrarea cu diverse instrumente și IDE-uri.

2. **JUnit Jupiter**:
    - Este noul model de programare pentru scrierea testelor în JUnit 5.
    - Include noi anotări și caracteristici față de JUnit 4.
    - Oferă suport pentru scrierea de teste și extensii utilizând API-urile Jupiter.

3. **JUnit Vintage**:
    - Oferă compatibilitate înapoi pentru a rula teste scrise în JUnit 3 și JUnit 4 pe JUnit 5 Platform.

### Caracteristici Cheie ale JUnit 5

1. **Noul model de extensii**:
    - JUnit 5 introduce un model de extensii mai flexibil, permițând dezvoltatorilor să extindă comportamentul testelor prin adăugarea de extensii personalizate.

2. **Anotări noi**:
    - JUnit Jupiter include multe noi anotări pentru scrierea testelor, cum ar fi:
      - `@Test`: Marca o metodă ca test.
      - `@ParameterizedTest`: Permite testarea parametrizată.
      - `@RepeatedTest`: Permite rularea repetată a unui test.
      - `@BeforeEach` și `@AfterEach`: Anotări pentru metode care rulează înainte și după fiecare test.
      - `@BeforeAll` și `@AfterAll`: Anotări pentru metode care rulează înainte și după toate testele dintr-o clasă.

3. **Testare parametrizată**:
    - JUnit 5 suportă testarea parametrizată prin `@ParameterizedTest`, permițând rularea aceleași metode de testare cu seturi diferite de date.

4. **Integrare îmbunătățită cu IDE-uri și instrumente de build**:
    - JUnit 5 este suportat de principalele IDE-uri (IntelliJ IDEA, Eclipse, etc.) și instrumente de build (Maven, Gradle, etc.), oferind o experiență de utilizare fluentă.

5. **Lambda și Stream API**:
    - JUnit 5 integrează mai bine funcționalitățile oferite de Java 8, inclusiv lambda expressions și Stream API.

### Exemplu Simplu de Test în JUnit 5

Pentru a demonstra cum se scrie un test în JUnit 5, vom folosi clasa `Calculator` de mai devreme.

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

#### Testul în JUnit 5

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

### Cum să rulezi testele

Pentru a rula testele JUnit 5, trebuie să adaugi dependențele necesare în proiectul tău. Iată un exemplu de configurare pentru Maven:

#### Pom.xml pentru Maven

```xml
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.7.0</version>
        <scope>test</scope>
    </dependency>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-engine</artifactId>
        <version>5.7.0</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

Aceasta este o introducere de bază în JUnit 5. Platforma este foarte robustă și flexibilă, permițând dezvoltatorilor să scrie teste unitare mai eficiente și mai expresive.
