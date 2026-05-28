**Class:** [[AlgoDat - Algorithmen und Datenstrukturen]]
**Date:** 27-04-2026
**Topics:** #Laufzeit #Komplexität #PriorityQueue #BinaryHeap #UnionFind #Datenstrukturen #TU-Berlin
**Link:** [[VL.03 AlgoDat.pdf]]

---

## 🎯 Lernziele der Vorlesung

VL.03 behandelt theoretische Grundlagen der Berechenbarkeit, Werkzeuge zur Laufzeitanalyse und drei wichtige Datenstrukturen mit effizienten Operationen in $O(\log N)$.

- **Church-Turing-These**: Formale Grundlage der Berechenbarkeit
- **P vs. NP**: Praktische Bedeutung von Komplexitätsklassen
- **Wachstumsordnungen**: $O$, $\Theta$, $\Omega$, $o$, $\omega$ und deren Anwendung
- **Laufzeitanalyse-Regeln**: Sequenz, Schachtelung, Rekursion, Halbierung
- **Kombinationsschemata**: Wie Schleifenkombinationen die Komplexität bestimmen
- **Priority Queue (Vorrangwarteschlange)**: API und binäre Heap-Implementierung
- **Binary Heap**: `swim()` und `sink()` als Kernoperationen
- **Indizierte Priority Queue**: Erweiterung für aktualisierbare Schlüssel
- **Union-Find**: Dynamische Verwaltung von Zusammenhangskomponenten (lazy vs. eager)

---

## 1. Church-Turing-These & Berechenbarkeit

### Definition (Church-Turing-These)

$$\boxed{\text{Die Klasse der Turing-berechenbaren Funktionen } = \text{ die Klasse der intuitiv berechenbaren Funktionen.}}$$

**Rolle:** Diese These verbindet das mathematische Konzept der Turing-Maschine mit dem, was wir intuitiv als „algorithmisch lösbar" verstehen. Sie begründet, warum moderne Computer und Turing-Maschinen theoretisch äquivalent sind.

> 💡 **Merkhilfe:** Alles, was ein Mensch durch einen klaren schrittweisen Prozess berechnen kann, kann auch eine Turing-Maschine berechnen – und umgekehrt.

**Wichtige Begriffe:**
- **Turing-Maschine**: Abstraktes Berechnungsmodell mit unendlichem Speicherband und endlichem Zustandsautomaten
- **Berechenbar**: Eine Funktion ist berechenbar, wenn eine Turing-Maschine sie für jede Eingabe in endlicher Zeit berechnet
- **Intuitiv berechenbar**: Alles, was durch einen klaren algorithmischen Prozess lösbar ist

⚠️ **Achtung:** Die Church-Turing-These ist eine *These*, kein Beweis – sie kann durch Gegenbeispiel widerlegt, aber nicht formal bewiesen werden.

---

## 2. Komplexitätsklassen: P, NP, NP-Vollständigkeit

### Definition der Klassen

$$\boxed{P \subseteq NP}$$

**P – Polynomiell lösbare Probleme:**
- Probleme, die von einem Algorithmus mit Laufzeit $O(p(n))$ für ein Polynom $p(n)$ gelöst werden können
- **Merkhilfe**: P = praktisch lösbar (grob)

**NP – Polynomiell verifizierbare Probleme:**
- Lösungskandidaten können in polynomieller Zeit *verifiziert* werden
- Wie lange es dauert, eine Lösung zu *finden*, ist egal

**NP-schwer (NP-hard):**
- Jedes Problem aus NP kann in polynomieller Zeit auf dieses Problem reduziert werden

**NP-vollständig:**

$$\boxed{X \text{ ist NP-vollständig} \iff X \in NP \text{ und } X \text{ ist NP-schwer}}$$

### P = NP?

⚠️ **Achtung:** $P = NP$ ist eines der Millennium-Probleme (1.000.000 $ Preisgeld) – bis heute ungelöst. Fast alle Wissenschaftler vermuten $P \neq NP$.

### Beispiele für NP-vollständige Probleme

| Problem | Beschreibung |
|---|---|
| **TSP** (Traveling Salesman) | Minimaler Zyklus, der jeden Knoten genau einmal besucht |
| **Hamiltonpfad** | Pfad, der jeden Knoten genau einmal besucht |
| **Maximaler Schnitt** | Schnitt mit maximalem Gewicht in gewichtetem Graph |
| **0/1-Rucksackproblem** | Optimale Auswahl von Objekten mit Gewichtsbeschränkung |

### Strategien für NP-vollständige Probleme

- **Heuristische Algorithmen**: Effizient in bestimmten praktischen Fällen, kein worst-case-Garantie
- **Approximative Algorithmen**: Polynomielle Laufzeit, aber suboptimale Lösung mit Gütegarantie
- **Branch-and-Bound**: Systematische Suche mit Abschneiden aussichtsloser Zweige

---

## 3. Wachstumsordnungen

### Definitionen der Funktionenklassen

$$\boxed{O(f) = \{g : \mathbb{N} \to \mathbb{N} \mid \exists\, c > 0,\, n_0 \in \mathbb{N} : g(n) < c \cdot f(n) \;\forall\, n > n_0\}}$$

Die fünf Klassen im Überblick:

$$\Omega(f) = \{g \mid \exists\, c > 0,\, n_0 : g(n) > c \cdot f(n) \;\forall\, n > n_0\}$$

$$\Theta(f) = O(f) \cap \Omega(f)$$

| Notation | Bedeutung | Analogie |
|---|---|---|
| $O(f)$ | höchstens so schnell wachsend wie $f$ | $\leq$ |
| $\Theta(f)$ | genauso schnell wachsend wie $f$ | $=$ |
| $\Omega(f)$ | mindestens so schnell wachsend wie $f$ | $\geq$ |
| $o(f)$ | echt langsamer als $f$ | $<$ |
| $\omega(f)$ | echt schneller als $f$ | $>$ |

> 💡 **Merkhilfe:** $O$ ist eine obere Schranke, $\Omega$ eine untere, $\Theta$ ist scharf (beides zugleich).

### Hierarchie der Wachstumsordnungen

LANGSAM SCHNELL │ ▼ O(1) → O(log N) → O(N) → O(N log N) → O(N²) → O(N³) → O(2^N) → O(N!)

### Auswirkung der Wachstumsordnung (Laufzeit-Tabelle)

Annahme: Programm mit $N=1000$ braucht **1 Minute**.

| Wachstumsordnung | $N=1000$ | $N=10.000$ | $N=100.000$ | $N=1.000.000$ |
|---|---|---|---|---|
| **konstant** $O(1)$ | 1 Min | 1 Min | 1 Min | 1 Min |
| **logarithmisch** $O(\log N)$ | 1 Min | $1{,}\overline{3}$ Min | $1{,}\overline{6}$ Min | 2 Min |
| **linear** $O(N)$ | 1 Min | 10 Min | 2 Std | 1 Tag |
| **überlinear** $O(N \log N)$ | 1 Min | 13 Min | 3 Std | $1\frac{1}{2}$ Tage |
| **quadratisch** $O(N^2)$ | 1 Min | 2 Std | 5 Tage | 23 Wochen |
| **kubisch** $O(N^3)$ | 1 Min | 1 Tag | 2 Jahre | 2000 Jahre |
| **exponentiell** $O(2^N)$ | 1 Min | $\infty$ | $\infty$ | $\infty$ |

⚠️ **Achtung:** Konstante Faktoren und Offsets spielen in der asymptotischen Analyse *keine* Rolle, können aber für kleine $N$ entscheidend sein.

✅ **Wichtig:** $O(\log_2 N) = O(\log_{10} N)$, da sich Logarithmen zu verschiedenen Basen nur um einen konstanten Faktor unterscheiden.

### Beispiel: Softwarevergleich

```

Software A: A(n) = 1.000·n + 10.000 ms → O(N) Software B: B(n) = n² → O(N²)

n = 5: A = 15s, B = 0,025s → B besser (kleines N) n = 100: A = 110s, B = 10s → B noch besser n = 10⁵: A = 10⁵s, B = 10⁷s → A deutlich besser (großes N)

```

⚠️ **Warnung:** Für kleine $n$ kann eine Funktion mit größerer Wachstumsordnung schneller sein! Erst ab einem gewissen $n_0$ gilt die asymptotische Ordnung.

---

## 4. Laufzeitanalyse: Regeln & Beispiele

### Regeln für Funktionen ohne Rekursion

$$\boxed{\text{Hauptregel: Betrachte die am häufigsten ausgeführte Codezeile (innerste Schleife).}}$$

| Regel | Beschreibung | Ergebnis |
|---|---|---|
| **1** | Sequenz (nacheinander) | $\max$ der Einzelkomplexitäten |
| **2** | Schleife | maximale Durchläufe $\times$ Komplexität des Rumpfs |
| **3** | Schleife mit Halbierung | $\Theta(\log N)$ |
| **4** | Geschachtelte Schleifen | Multiplikation der Komplexitäten |
| **5** | Konstante Faktoren | können weggelassen werden |

### Beispiele

```java

// f1: Eine Schleife → Θ(N)
for (int i = 0; i < N; i++)
    x += i * i;            // --> Θ(N)

// f2: Zwei geschachtelte Schleifen → Θ(N²)
for (int i = 0; i < N; i++)       // Θ(N)
    for (int j = 0; j < N; j++)   // Θ(N)
        x += i * j;               // --> Θ(N²)

// f4: Abhängige Schleifengrenzen → Θ(N²)
for (int i = 0; i < N; i++)       // Θ(N)
    for (int j = 0; j <= i; j++)  // O(N) → Summe = N(N+1)/2 → Θ(N²)
        x += i * j;               // --> Θ(N²)

// f5: Verdopplung der Laufvariable → Θ(log N)
for (int i = 1; i < N; i *= 2)   // Θ(log N)
    x += i * i;                    // --> Θ(log N)

// f6: Schachtelung mit verdoppelter Variable → Θ(N), nicht Θ(N log N)!
for (int i = 1; i < N; i *= 2)   // Θ(log N)
    for (int j = 0; j < i; j++)  // O(N) → Summe = 1+2+4+...+N = N-1
        x += i * j;               // --> Θ(N) ❌ nicht O(N log N)!

```

> 💡 **Merkhilfe für f6:** $1 + 2 + 4 + \cdots + N = 2N - 1 \in \Theta(N)$ (geometrische Reihe!)

### Regeln für rekursive Funktionen

$$\boxed{T_{\text{gesamt}} = \text{Anzahl Knoten im Rekursionsbaum} \times \text{Komplexität des Restkodes}}$$

|Situation|Baumhöhe|Knoten|Komplexität|
|---|---|---|---|
|Argument $-$ konst., $k=1$|$\Theta(N)$|$\Theta(N)$|$\Theta(N)$|
|Argument $/$ konst., $k=1$|$\Theta(\log N)$|$\Theta(\log N)$|$\Theta(\log N)$|
|$k$ Verzweigungen, lin. Höhe|$\Theta(N)$|$\Theta(k^N)$|$O(k^N)$|
|$k=2$ Verzweig., log. Höhe|$\Theta(\log N)$|$\Theta(2^{\log N}) = \Theta(N)$|$\Theta(N)$|

**Beispiele:**

```java
// r1: N-1 → linearer Baum → Θ(N)
int r1(int N) { return N==0 ? 1 : r1(N-1)+1; }

// r2: N/2 → logarithmischer Baum → Θ(log N)
int r2(int N) { return N<=1 ? 1 : r2(N/2)+1; }

// r3: 3 Äste, lineare Höhe → O(3^N)
int r3(int N) { return N<=1 ? 1 : r3(N-1)+r3(N-2)+r3(N-3); }

// r4: 2 Äste, log. Höhe → Θ(2^{log N}) = Θ(N)
int r4(int N) { return N<=0 ? 1 : r4(N/2)+r4(N/2); }
```

### Amortisierte Laufzeitanalyse

$$\boxed{\text{Amortisierte Kosten} = \frac{\text{Gesamtkosten über } N \text{ Operationen}}{N}}$$

**Beispiel: Dynamisches Array (Stack mit Array-Verdoppelung)**

Bei $N$ Einfügungen (Verdoppelungsstrategie): $$\text{Gesamte Kopierschritte} = 1 + 2 + 4 + \cdots + N = 2N - 1$$

$$\text{Amortisiert pro push()} = \frac{2N-1}{N} \approx 2 \in O(1)$$

✅ **Fazit:** Obwohl einzelne `push()`-Operationen $O(N)$ kosten können, sind die amortisierten Kosten $O(1)$.

---

## 5. Laufzeiten einfacher Java-Datenstrukturen

### Referenz-Tabelle

|Datenstruktur|Operation|Laufzeit (worst case)|
|---|---|---|
|**Stack**|`push()`, `pop()`|$O(1)$|
|**Queue**|`enqueue()`, `dequeue()`|$O(1)$|
|**LinkedList**|`addFirst()`, `pollFirst()`, `peekFirst()`|$O(1)$|
|**LinkedList**|`get(i)`, `contains()`, `remove(i)`|$O(N)$|
|**PriorityQueue**|`add()`, `poll()`|$O(\log N)$|

⚠️ **Achtung:** `Stack` und `Queue` in Java haben auch Methoden wie `remove()` mit linearer Laufzeit – immer Dokumentation prüfen!

---

## 6. Tests & Fehlerbehandlung

### Teststrategie in Java

- **Exceptions** für Laufzeitfehler (z.B. `IllegalArgumentException`, `NullPointerException`)
- **Unit-Tests** testen einzelne Methoden/Klassen isoliert (vs. Integrationstests)
- **Test-Driven Development (TDD)**: Zuerst Tests schreiben, dann Implementierung

```java
// Beispiel: JUnit Test
@Test
public void testAdd() {
    PriorityQueue<Integer> pq = new PriorityQueue<>(10, 1);
    pq.add(5);
    pq.add(3);
    assertEquals(5, (int) pq.poll()); // Max-PQ erwartet 5
}
```

> 💡 **Merkhilfe:** TDD zwingt zu klarem API-Design, da man erst den Nutzungskontext (Test) definiert, bevor man implementiert.

---

## 7. Priority Queue (Vorrangwarteschlange)

### Definition

$$\boxed{\text{Priority Queue} = \text{Warteschlange, bei der } \texttt{poll()} \text{ immer das Element mit höchster Priorität entfernt.}}$$

**Anwendungsbeispiel:** Die $M$ größten Elemente aus einem Datenstrom extrahieren.

**API:**

```java
public class MaxPQ<K extends Comparable<K>>
    MaxPQ(int capacity)   // Erstellt PQ mit Kapazität
    void add(K item)      // Fügt Element ein: O(log N)
    K poll()              // Entfernt & gibt größten Schlüssel zurück: O(log N)
    boolean isEmpty()     // O(1)
    int size()            // O(1)
```

### Implementierungsvergleich

|Implementierung|`add()`|`poll()`|Bemerkung|
|---|---|---|---|
|Unsortierte Liste|$O(1)$|$O(N)$|Suche bei Entnahme|
|Sortierte Liste|$O(N)$|$O(1)$|Einfügen aufwändig|
|**Binärer Heap**|$O(\log N)$|$O(\log N)$|✅ Optimal|

### Definition: Binärer Heap

$$\boxed{\text{Binärer Heap} = \text{Array } A[1..N], \text{ interpretiert als vollständiger Binärbaum mit Heap-Ordnung}}$$

**Struktureigenschaften:**

- Wurzel: $A$ (Index 0 wird **nicht** benutzt)
- Elternknoten von $k$: $\lfloor k/2 \rfloor$
- Linkes Kind von $k$: $2k$
- Rechtes Kind von $k$: $2k+1$

**Heap-Ordnungsbedingung (MaxHeap):**

$$\boxed{\forall k : A[\lfloor k/2 \rfloor] \geq A[k]}$$

Jeder Knoten ist ≥ seinen Kindern.

### ASCII-Darstellung: Array → Binärbaum

```
Array: [_, 10, 8, 6, 5, 3, 2, 4]  (Index 0 unbenutzt)

            10           ← Wurzel (A)
           /   \
          8     6        ← A, A
         / \   / \
        5   3 2   4      ← A, A, A, A

Eltern-Kind-Beziehungen:
  A=10 → Kinder: A=8, A=6
  A=8  → Kinder: A=5, A=3
  A=6  → Kinder: A=2, A=4
```

### Algorithmus: swim() – Aufsteigen

**Rolle:** Stellt Heap-Ordnung nach Einfügen am Ende wieder her.

```pseudocode
swim(k):
  solange k > 1 und A[k/2] < A[k]:
    swap(A[k/2], A[k])   // tausche mit Elternknoten
    k = k/2              // gehe einen Level höher
```

```java
private void swim(int k) {
    while (k > 1 && !order(k/2, k)) {
        swap(k/2, k);
        k = k/2;
    }
}
```

**Schritt-für-Schritt: add(9) in bestehenden Heap:**

```
Vor add(9):
        10
       /   \
      8     6
     / \
    5   3

Nach Einfügen am Ende (Position 6):
        10
       /   \
      8     6
     / \   /
    5   3 9     ← 9 < 6? Nein: 9 > 6 → swim!

swim(6): 9 > 6? ja → tausche:
        10
       /   \
      8     9   ← 9 aufgestiegen
     / \   /
    5   3 6

swim(3): 9 > 10? nein → fertig ✅
```

### Algorithmus: sink() – Absinken

**Rolle:** Stellt Heap-Ordnung nach Entfernen der Wurzel wieder her.

```pseudocode
sink(k):
  solange 2*k ≤ N:           // solange Kinder vorhanden
    j = 2*k                  // linkes Kind
    falls j < N und A[j] < A[j+1]:
      j = j + 1              // rechtes Kind ist größer
    falls A[k] ≥ A[j]:
      break                  // Heap-Ordnung hergestellt
    swap(A[k], A[j])
    k = j
```

```java
private void sink(int k) {
    while (2*k <= N) {
        int j = 2*k;
        if (j < N && !order(j, j+1)) j++;
        if (order(k, j)) break;
        swap(k, j);
        k = j;
    }
}
```

**Schritt-für-Schritt: poll() aus MaxHeap:**

```
Ausgangslage:
        10
       /   \
      8     6
     / \
    5   3

Schritt 1: Entferne Wurzel (10), setze letztes Element (3) an Wurzel:
        3
       / \
      8   6
     /
    5

Schritt 2: sink(1): 3 < 8 (linkes Kind ist größer) → tausche:
        8
       / \
      3   6
     /
    5

Schritt 3: sink(2): 3 < 5 → tausche:
        8
       / \
      5   6
     /
    3

✅ Ergebnis: poll() gibt 10 zurück, Heap korrekt mit neuer Wurzel 8
```

### Vollständige Implementierung

```java
public class PriorityQueue<E extends Comparable<E>> {
    private E[] pq;
    private int N;
    private int sign; // +1 für MaxPQ, -1 für MinPQ

    public PriorityQueue(int capacity, int sign) {
        pq = (E[]) new Comparable[capacity + 1];
        this.sign = sign;
    }

    public void add(E e) {
        pq[++N] = e;
        swim(N);              // neu eingefügtes Element aufsteigen lassen
    }

    public E poll() {
        E head = pq;       // größtes Element sichern
        swap(1, N);           // Wurzel ↔ letztes Element
        pq[N--] = null;       // letztes Element entfernen
        sink(1);              // neue Wurzel absinken lassen
        return head;
    }

    private boolean order(int i, int j) {
        return sign * pq[i].compareTo(pq[j]) >= 0;
    }

    private void swap(int i, int j) {
        E e = pq[i]; pq[i] = pq[j]; pq[j] = e;
    }

    private void swim(int k) {
        while (k > 1 && !order(k/2, k)) { swap(k/2, k); k = k/2; }
    }

    private void sink(int k) {
        while (2*k <= N) {
            int j = 2*k;
            if (j < N && !order(j, j+1)) j++;
            if (order(k, j)) break;
            swap(k, j); k = j;
        }
    }
}
```

### Laufzeitanalyse Binary Heap

$$\boxed{T_{\text{add}} = T_{\text{poll}} = O(\log N)}$$

**Begründung:** `swim()` und `sink()` traversieren höchstens die Höhe des Binärbaums. Ein vollständiger Binärbaum mit $N$ Elementen hat Höhe $\lfloor \log_2 N \rfloor$.

### Anwendungsbeispiel: M größte Elemente

```java
// Extrahiere die M=4 größten Elemente aus testArray via MinPQ
int[] testArray = {4, 2, -17, 5, 23, 45, 0, 34, -7, 2, 0, 34};
int M = 4;
PriorityQueue<Integer> pq = new PriorityQueue<>(M+1, -1); // MinPQ

for (int k : testArray) {
    pq.add(k);
    if (pq.size() > M) pq.poll(); // entferne kleinsten → behalte M größte
}
// pq enthält jetzt: {5, 23, 34, 45}
```

---

## 8. Indizierte Priority Queue

### Motivation & Definition

$$\boxed{\text{Indizierte PQ} = \text{Priority Queue, bei der Schlüssel über einen Index } i \in {0, \ldots, N-1} \text{ direkt aktualisierbar sind.}}$$

**Problem mit normaler PQ:** Wenn sich die Priorität eines Elements ändert (z.B. kürzerer Weg gefunden in Dijkstra), kann man es in einer normalen PQ nicht effizient lokalisieren und aktualisieren.

**Lösung:** Drei parallele Arrays:

- `keys[i]`: Schlüssel/Priorität des Elements mit Index $i$
- `pq[j]`: Welcher Index $i$ steht an Heap-Position $j$?
- `qp[i]`: Auf welcher Heap-Position $j$ befindet sich Index $i$?

```
Invariante: pq[qp[i]] = i  und  qp[pq[j]] = j
```

### API

```java
public class IndexPQ<K extends Comparable<K>>
    IndexPQ(int capacity)           // erstellt PQ für Indizes 0..capacity-1
    void insert(int i, K key)       // füge Index i mit Schlüssel key ein
    void decreaseKey(int i, K key)  // verringere Schlüssel von Index i → swim
    void increaseKey(int i, K key)  // erhöhe Schlüssel von Index i → sink
    int poll()                      // entferne und gib Index mit höchster Prio zurück
    boolean contains(int i)         // ist Index i in der PQ?
    K keyOf(int i)                  // Schlüssel von Index i
```

### Laufzeit Indizierte PQ

|Operation|Laufzeit|Bemerkung|
|---|---|---|
|`insert()`|$O(\log N)$|swim|
|`decreaseKey()`|$O(\log N)$|swim|
|`increaseKey()`|$O(\log N)$|sink|
|`poll()`|$O(\log N)$|sink|
|`contains()`|$O(1)$|via `qp` Array|
|`keyOf()`|$O(1)$|direkt via `keys`|

> 💡 **Merkhilfe:** Die indizierte PQ ist das Herzstück von Dijkstras Algorithmus und Prims MST-Algorithmus, da Kantenwerte aktualisiert werden müssen.

---

## 9. Union-Find: Dynamische Zusammenhangskomponenten

### Definition & API

$$\boxed{\text{Union-Find} = \text{Datenstruktur zur dynamischen Verwaltung von Partitionen einer Menge } {0, \ldots, V-1}}$$

**API:**

```java
public class UnionFind
    UnionFind(int V)                 // V Komponenten, je 1 Knoten
    void union(int v, int w)         // verbinde Komponenten von v und w
    int find(int v)                  // ID der Komponente von v
    boolean connected(int v, int w)  // sind v und w in derselben Komponente?
    int count()                      // Anzahl der Komponenten
```

### Schritt-für-Schritt-Beispiel

```
Startzustand: {0}, {1}, {2}, {3}, {4}, {5}, {6}, {7}  (8 Komponenten)

union(0,5): {0,5}, {1}, {2}, {3}, {4}, {6}, {7}
union(2,3): {0,5}, {1}, {2,3}, {4}, {6}, {7}
union(6,7): {0,5}, {1}, {2,3}, {4}, {6,7}
union(0,1): {0,1,5}, {2,3}, {4}, {6,7}
union(2,5): {0,1,2,3,5}, {4}, {6,7}   (3 Komponenten)

connected(0,5)? → true   (selbe Komponente)
connected(1,2)? → true   (nach union(2,5))
connected(5,6)? → false  (verschiedene Komponenten)
```

### Lazy Union-Find (Quick-Union)

**Idee:** Jeder Knoten zeigt auf seinen Elternknoten. `find()` folgt dem Pfad bis zur Wurzel (Komponenten-ID = Wurzel).

```pseudocode
find(v):
  solange parent[v] ≠ v:
    v = parent[v]
  return v

union(v, w):
  rv = find(v)
  rw = find(w)
  parent[rv] = rw   // hänge einen Baum unter den anderen
```

```
Lazy Union-Find Baum (ungünstige Form):
  5
  |
  4
  |
  3
  |
  2
  |
  1
  |
  0
Mittlere Distanz zur Wurzel: 5,11  ⚠️ (entarteter Baum)
```

**Laufzeiten:**

|Operation|Lazy (Quick-Union)|
|---|---|
|`union()`|$O(N)$ worst case|
|`find()`|$O(N)$ worst case|
|`connected()`|$O(N)$ worst case|

❌ **Problem:** Im worst case entartet der Baum zu einer langen Kette → lineare Laufzeit.

### Eager Union-Find (Weighted Quick-Union)

**Idee:** Beim Verbinden immer den kleineren Baum unter den größeren hängen (nach Gewicht/Größe). Hält Bäume flach.

```pseudocode
union(v, w):
  rv = find(v)
  rw = find(w)
  falls size[rv] < size[rw]:
    parent[rv] = rw
    size[rw] += size[rv]
  sonst:
    parent[rw] = rv
    size[rv] += size[rw]
```

```
Eager Union-Find (flache Bäume):
      0
    / | \
   1  5  2
         |
         3
Mittlere Distanz zur Wurzel: 1,52  ✅ (viel flacher)
```

**Laufzeiten:**

$$\boxed{T_{\text{union}} = T_{\text{find}} = O(\log N)}$$

**Beweis (Baumhöhe $\leq \log_2 N$):**

**Induktionsanfang ($N=1$):** Baum hat Höhe 0 $\leq \log_2 1 = 0$. ✅

**Induktionsvoraussetzung:** Für alle Bäume mit $< N$ Knoten gilt Höhe $\leq \log_2 N$.

**Induktionsschritt:** Sei $T_1$ kleiner (Größe $s_1$), $T_2$ größer (Größe $s_2 \geq s_1$). Nach Verbinden hat $T_1$ Wurzel Tiefe um 1 erhöht. Der neue Baum hat $s_1 + s_2 \geq 2s_1$ Knoten. Also:

$$\text{Höhe}(T_1 \text{ nach Verbinden}) \leq \log_2 s_1 + 1 \leq \log_2 \frac{s_1 + s_2}{2} + 1 = \log_2(s_1 + s_2) \quad \square$$

### Erweiterung: Pfadkompression (Path Compression)

**Idee:** Beim `find(v)` alle besuchten Knoten direkt an die Wurzel hängen.

```pseudocode
find(v):
  root = v
  solange parent[root] ≠ root:
    root = parent[root]
  // Pfadkompression:
  solange parent[v] ≠ root:
    next = parent[v]
    parent[v] = root
    v = next
  return root
```

**Laufzeit mit Pfadkompression:**

$$\boxed{T_{\text{amortisiert}} = O(\alpha(N)) \approx O(1)}$$

wobei $\alpha(N)$ die inverse Ackermann-Funktion ist (praktisch $\leq 4$ für alle realen $N$).

⚠️ **Achtung:** Der Beweis dieser Laufzeit geht weit über den Skriptinhalt hinaus – Ergebnis wird aus der Literatur zitiert.

### Laufzeitvergleich Union-Find Varianten

|Variante|`union()`|`find()`|Bemerkung|
|---|---|---|---|
|**Quick-Find** (eager Array)|$O(N)$|$O(1)$|find trivial, union zu teuer|
|**Quick-Union** (lazy Baum)|$O(N)$|$O(N)$|entarteter Baum möglich|
|**Weighted QU**|$O(\log N)$|$O(\log N)$|✅ praktisch gut|
|**Weighted QU + Pfadkompression**|$O(\alpha(N))$|$O(\alpha(N))$|✅ praktisch optimal|

---

## 📌 Zusammenfassung

### Wichtige Konzepte

|Konzept|Bedeutung|
|---|---|
|**Church-Turing-These**|Turing-berechenbar = intuitiv berechenbar|
|**P**|Polynomiell lösbare Probleme|
|**NP**|Polynomiell verifizierbare Probleme; $P \subseteq NP$|
|**NP-vollständig**|In NP + NP-schwer; härteste Probleme in NP|
|**$O(f)$**|Obere Schranke der Wachstumsordnung|
|**$\Theta(f)$**|Exakte Wachstumsordnung (= $O \cap \Omega$)|
|**Amortisierte Laufzeit**|Durchschnittliche Kosten über $N$ Operationen|
|**Binary Heap**|Array als vollst. Binärbaum; Heap-Ordnung $\Rightarrow$ $O(\log N)$|
|**swim()**|Wiederherstellen von unten nach oben (add)|
|**sink()**|Wiederherstellen von oben nach unten (poll)|
|**Indizierte PQ**|PQ mit direktem Zugriff/Update via Index|
|**Union-Find**|Partition einer Menge; union/find Operationen|
|**lazy (Quick-Union)**|Bäume, keine Größenkontrolle → $O(N)$|
|**eager (Weighted QU)**|Größenkontrolle → $O(\log N)$, mit PK → $O(\alpha(N))$|

### Kernaussagen

✅ **Wachstumsordnung entscheidet** – für große $N$ dominiert der Exponent absolut über konstante Faktoren  
✅ **Binary Heap** ermöglicht $O(\log N)$ für add und poll dank Baumhöhe $= \lfloor \log_2 N \rfloor$  
✅ **swim() für add()**, **sink() für poll()** – Merkregel: Einfügen schwimmt auf, Entfernen sinkt ab  
✅ **Weighted Union-Find** hält Bäume mit Höhe $\leq \log N$ durch Gewichtsstrategie  
⚠️ **f6-Falle:** Äußere Schleife verdoppelt + innere läuft bis $i$ → kein $\Theta(N \log N)$ sondern $\Theta(N)$  
⚠️ **Lazy Union-Find** entartet leicht → immer Weighted-Variante bevorzugen  
❌ **Falsch:** "O und Θ sind dasselbe" – $O$ ist nur eine obere Schranke, $\Theta$ ist exakt  
❌ **Falsch:** "swim() bei poll()" – sink() bei poll(), swim() bei add()

### Wichtige Algorithmen / Formeln

|Algorithmus/Formel|Laufzeit|Anwendung|
|---|---|---|
|**TwoSum-Count**|$\Theta(N^2)$|$\frac{3}{2}N^2 - \frac{1}{2}N + 3$ Operationen analytisch|
|**Amortisierter Stack-push**|$O(1)$ amort.|Array-Verdoppelungsstrategie|
|**Binary Heap add/poll**|$O(\log N)$|swim() / sink() ≤ Baumhöhe|
|**Indizierte PQ update**|$O(\log N)$|Dijkstra, Prim|
|**Weighted Union-Find**|$O(\log N)$|MST-Algorithmen, Graphen|
|**UF + Pfadkompression**|$O(\alpha(N))$|Nahezu konstant amortisiert|

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Object Oriented Programming (OOP)]]: Einführung Wachstumsordnungen, Stack, Queue, TwoSum
- [[VL.04 Backtracking & Gierige Algo]]: Backtracking als Suche im Lösungsbaum; nutzt rekursive Laufzeitanalyse aus VL.03
- [[VL.05 Branch-&-Bound, Minimax & Alpha-Beta Suche]]: Greedy-Suche im Teillösungsbaum; Laufzeitanalyse mit PQ ($O(\log N)$)
- [[VL.10 – Minimale Spannbäume]]: Prims Algorithmus benutzt Indizierte PQ; Kruskals nutzt Union-Find
- [[VL.11 – Kürzeste Wege]]: Dijkstra nutzt Indizierte Priority Queue direkt
- [[IntroProg]]: Grundlagen Wachstumsordnungen, Divide-and-Conquer, Binary Heap Einführung