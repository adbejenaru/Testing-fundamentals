Testele parametrizate în Java permit rularea aceleiași metode de testare cu diferite seturi de date. Aceste teste sunt foarte utile pentru a reduce duplicarea codului de testare și pentru a acoperi mai multe scenarii de testare cu efort minim.

### Beneficii ale testelor parametrizate:
1. **Reducerea codului de testare**: Scrie metoda de testare o singură dată și ruleaz-o cu diferite seturi de date.
2. **Acoperire mai mare**: Permite testarea unei funcționalități cu multiple seturi de date.
3. **Ușurința în întreținere**: Adăugarea de noi cazuri de testare devine simplă și curată.

### Implementarea testelor parametrizate în JUnit 5

JUnit 5 oferă suport pentru teste parametrizate prin adnotarea `@ParameterizedTest` și diferite surse de date, cum ar fi `@ValueSource`, `@CsvSource`, `@MethodSource`, etc.

#### Exemplu simplu cu `@ValueSource`

Să considerăm o metodă care verifică dacă un număr este par:

```java
public class NumberUtils {
    public static boolean isEven(int number) {
        return number % 2 == 0;
    }
}
```

Putem scrie un test parametrizat pentru această metodă astfel:

```java
import static org.junit.jupiter.api.Assertions.assertTrue;
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.ValueSource;

public class NumberUtilsTest {

    @ParameterizedTest
    @ValueSource(ints = {2, 4, 6, 8, 10})
    void testIsEven(int number) {
        assertTrue(NumberUtils.isEven(number));
    }
}
```

În acest exemplu, testul `testIsEven` va fi rulat de cinci ori, fiecare dată cu un număr diferit din `@ValueSource`.

`@NullSource` și `@EmptySource` sunt două anotări oferite de JUnit 5 care ajută la testarea codului cu valori speciale, cum ar fi `null` și șiruri de caractere goale. Aceste anotări sunt folosite în cadrul testelor parametrizate pentru a furniza date de intrare specifice fără a trebui să le declarăm explicit în fiecare test.

### @NullSource

`@NullSource` este utilizat pentru a furniza o valoare `null` ca dată de intrare pentru un test parametrizat. Aceasta este utilă pentru a verifica comportamentul codului atunci când se confruntă cu valori `null`.

### @EmptySource

`@EmptySource` este utilizat pentru a furniza date de intrare goale. Aceasta poate fi utilizată pentru a verifica comportamentul codului atunci când se confruntă cu șiruri de caractere goale, colecții goale sau alte tipuri de date care pot fi considerate "goale".

### Exemple de Utilizare

Mai jos sunt exemple care demonstrează utilizarea `@NullSource` și `@EmptySource` în testele parametrizate cu JUnit 5.

#### Exemplu cu @NullSource

```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.NullSource;
import static org.junit.jupiter.api.Assertions.assertFalse;

public class StringUtilTest {

    private final StringUtil util = new StringUtil();

    @ParameterizedTest
    @NullSource
    void testIsAllUpperCaseWithNull(String input) {
        // Presupunem că metoda isAllUpperCase returnează false pentru input null
        assertFalse(util.isAllUpperCase(input));
    }
}
```

În acest exemplu:
- `@NullSource` furnizează valoarea `null` ca dată de intrare pentru test.
- Metoda `testIsAllUpperCaseWithNull` verifică dacă metoda `isAllUpperCase` gestionează corect valoarea `null`.

#### Exemplu cu @EmptySource

```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.EmptySource;
import static org.junit.jupiter.api.Assertions.assertTrue;

public class StringUtilTest {

    private final StringUtil util = new StringUtil();

    @ParameterizedTest
    @EmptySource
    void testIsAllUpperCaseWithEmptyString(String input) {
        // Presupunem că metoda isAllUpperCase returnează true pentru un șir gol
        assertTrue(util.isAllUpperCase(input));
    }
}
```

În acest exemplu:
- `@EmptySource` furnizează un șir de caractere gol (`""`) ca dată de intrare pentru test.
- Metoda `testIsAllUpperCaseWithEmptyString` verifică dacă metoda `isAllUpperCase` gestionează corect un șir gol.

#### Combinarea Anotărilor

De asemenea, este posibil să combinați `@NullSource` și `@EmptySource` într-un singur test parametrizat folosind `@NullAndEmptySource`.

```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.NullAndEmptySource;
import static org.junit.jupiter.api.Assertions.assertTrue;

public class StringUtilTest {

    private final StringUtil util = new StringUtil();

    @ParameterizedTest
    @NullAndEmptySource
    void testIsAllUpperCaseWithNullAndEmpty(String input) {
        // Presupunem că metoda isAllUpperCase returnează true pentru input null sau șir gol
        assertTrue(util.isAllUpperCase(input));
    }
}
```

În acest exemplu:
- `@NullAndEmptySource` furnizează atât valoarea `null`, cât și un șir de caractere gol ca date de intrare pentru test.
- Metoda `testIsAllUpperCaseWithNullAndEmpty` verifică dacă metoda `isAllUpperCase` gestionează corect ambele cazuri.

Aceste anotări simplifică foarte mult procesul de testare pentru scenarii comune și asigură că codul este robust și tratează corect valorile speciale.

### Exemple mai complexe

#### Utilizarea `@CsvSource`

`@CsvSource` permite furnizarea mai multor argumente pentru testele parametrizate. Fiecare rând din `@CsvSource` reprezintă un set de argumente.

```java
import static org.junit.jupiter.api.Assertions.assertEquals;
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.CsvSource;

public class CalculatorTest {

    @ParameterizedTest
    @CsvSource({
        "1, 1, 2",
        "2, 3, 5",
        "3, 7, 10",
        "4, 6, 10"
    })
    void testAddition(int a, int b, int expected) {
        Calculator calculator = new Calculator();
        assertEquals(expected, calculator.add(a, b));
    }
}
```

#### Utilizarea `@MethodSource`

`@MethodSource` permite folosirea unei metode pentru a furniza datele de testare. Metoda trebuie să returneze un stream de argumente.

```java
import static org.junit.jupiter.api.Assertions.assertEquals;
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.MethodSource;

import java.util.stream.Stream;

public class CalculatorTest {

    @ParameterizedTest
    @MethodSource("additionProvider")
    void testAddition(int a, int b, int expected) {
        Calculator calculator = new Calculator();
        assertEquals(expected, calculator.add(a, b));
    }

    static Stream<Arguments> additionProvider() {
        return Stream.of(
            Arguments.of(1, 1, 2),
            Arguments.of(2, 3, 5),
            Arguments.of(3, 7, 10),
            Arguments.of(4, 6, 10)
        );
    }
}
```

În acest exemplu, metoda `additionProvider` furnizează seturile de argumente pentru testul `testAddition`.

### Concluzie

Testele parametrizate în JUnit 5 sunt o modalitate puternică și flexibilă de a îmbunătăți testarea unităților, reducând duplicarea codului și acoperind mai multe cazuri de testare. Utilizând adnotările și sursele de date disponibile, putem crea teste care sunt mai ușor de întreținut și extins.
