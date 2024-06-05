Test-Driven Development (TDD) este o metodologie de dezvoltare software care pune testele în centrul procesului de dezvoltare. Ideea principală este de a scrie mai întâi teste pentru funcționalitatea pe care dorești să o implementezi și apoi de a scrie codul necesar pentru a trece aceste teste. TDD ajută la asigurarea calității și fiabilității codului, deoarece codul este testat continuu pe măsură ce este scris.

### Principalele Etape ale TDD

TDD urmează un ciclu iterativ cunoscut sub numele de "Red-Green-Refactor". Acesta constă în trei pași principali:

1. **Red (Roșu)**:
    - Scrie un test care să verifice o funcționalitate specifică.
    - Rulează testul pentru a verifica că nu trece (testul trebuie să eșueze, deoarece funcționalitatea nu a fost încă implementată).
    - Acest pas confirmă că testul este valid și că testul poate detecta o problemă reală.

2. **Green (Verde)**:
    - Scrie codul minim necesar pentru a trece testul.
    - Rulează testul din nou pentru a verifica că trece (testul trebuie să fie verde).
    - Codul nu trebuie să fie perfect sau optimizat în această fază; scopul este doar de a trece testul.

3. **Refactor (Refactorizare)**:
    - Îmbunătățește codul scris pentru a-l face mai curat și mai eficient, fără a schimba funcționalitatea.
    - Asigură-te că toate testele trec după refactorizare.
    - Acest pas ajută la îmbunătățirea calității codului, păstrând în același timp comportamentul dorit.

### Beneficiile TDD

- **Calitate îmbunătățită a codului**: Codul este testat în mod continuu, ceea ce reduce numărul de defecte și bug-uri.
- **Design îmbunătățit**: TDD încurajează dezvoltarea de cod modular și testabil, ceea ce duce la un design mai bun.
- **Documentație vie**: Testele servesc ca documentație pentru modul în care ar trebui să funcționeze codul.
- **Feedback rapid**: Problemele sunt identificate și rezolvate mai devreme în procesul de dezvoltare.
- **Încredere crescută**: Dezvoltatorii au mai multă încredere în codul lor, deoarece știu că este bine testat.

### Exemplu de TDD

Să luăm un exemplu simplu pentru a ilustra TDD. Vom implementa o funcționalitate de adunare într-o clasă `Calculator`.

#### Pasul 1: Scrie un test (Red)

Scriem un test pentru a verifica că metoda `add` din clasa `Calculator` adună corect două numere.

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {

    @Test
    public void testAdd() {
        Calculator calculator = new Calculator();
        int result = calculator.add(2, 3);
        assertEquals(5, result);
    }
}
```

În acest moment, testul va eșua deoarece clasa `Calculator` și metoda `add` nu sunt încă implementate.

#### Pasul 2: Scrie codul pentru a trece testul (Green)

Implementăm metoda `add` în clasa `Calculator` pentru a trece testul.

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

Acum, rulăm testul din nou și ar trebui să treacă (să fie verde).

#### Pasul 3: Refactorizează codul (Refactor)

În acest exemplu simplu, codul este deja curat și nu necesită refactorizare. Totuși, în cazuri mai complexe, am îmbunătăți structura codului păstrând funcționalitatea intactă.

### Ciclu complet de TDD

Acest ciclu se repetă pentru fiecare funcționalitate nouă sau modificată. Dezvoltatorii scriu mai întâi teste, apoi implementează codul necesar pentru a trece acele teste și, în final, refactorizează codul pentru a-l îmbunătăți.

### Concluzie

TDD este o metodologie puternică pentru dezvoltarea software, care pune testele în centrul procesului de dezvoltare. Prin scrierea de teste înainte de cod și prin refactorizarea continuă, TDD ajută la crearea de cod de înaltă calitate, bine testat și ușor de întreținut.
