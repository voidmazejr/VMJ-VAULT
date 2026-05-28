**Class:** [[IntroProg]]  
**Date:** VL.4  
**Topics:** #Arrays #LinkedList #DoppeltVerketteListe #Stack #Queue #Structs #DynamischeDatenstrukturen

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung behandelt **fundamentale Datenstrukturen**, die als Grundlage für alle weiteren Algorithmen dienen.

- Verständnis von **Arrays** und ihre Limitationen
- **Dynamic Arrays** für flexibles Einfügen/Löschen
- **Verkettete Listen** (Linked Lists) und deren Implementierung in C
- **Structs in C** für zusammengesetzte Datentypen
- **Doppelt verkettete Listen** für bidirektionales Traversieren
- **Stack** (LIFO-Prinzip) und **Queue** (FIFO-Prinzip)
- **Laufzeitanalyse** der Operationen

---

## 1. Arrays

### Eigenschaften

- Speicherung **größerer Mengen** gleichartiger Elemente
- **Größe wird bei Initialisierung festgelegt**
- **Zugriff durch Index:** `A[0]`, `A[1]`, ..., `A[n-1]`
- **Direkter Zugriff** auf beliebiges Element in $O(1)$

### Limitationen

❌ **Probleme:**
- Anzahl der Elemente oft **vorher nicht bekannt**
- Anzahl **ändert sich** während des Programmdurchlaufs
- **Löschen:** Lücken im Array
- **Einfügen:** Neues Array notwendig, alle Daten müssen kopiert werden → $O(n)$

### Visualisierung: Löschen und Einfügen

```
Ursprünglich: [3, 7, 9, 2, 5]
              
Löschen von 9: [3, 7, _, 2, 5]  ← Lücke!

Einfügen von 4: Neues Array nötig
[3, 7, _, 2, 5] → [3, 7, 4, _, 2, 5]  ← Verschieben nötig!
```

---

## 2. Dynamic Arrays

### Idee

Erweiterung des klassischen Arrays für **effizientes Einfügen/Löschen am Ende**.

### Unterscheidung: Capacity vs. Length

- **Capacity:** Größe im Speicher (reservierter Platz)
- **Length:** Anzahl der tatsächlich verwendeten Elemente

```
[3, 7, 9, 2, _, _, _, _]
 ←-length=4-→
 ←------capacity=8-------→
```

### Eigenschaften

✅ **Vorteile:**
- Vorteile des klassischen Arrays bleiben erhalten
- **Einfügen am Ende:** $\approx O(1)$ (amortisiert)
- **Löschen am Ende:** $\approx O(1)$

❌ **Nachteile:**
- **Einfügen/Löschen an beliebiger Stelle** immer noch teuer: $O(n)$

---

## 3. Structs in C (Zusammengesetzte Datentypen)

### Definition

**Structs** fassen zusammengehörige Daten in einen eigenen Datentyp zusammen.

### Syntax

```c
struct produkt {
    char name[255];
    float preis;
};

struct produkt beispiel;  // Deklaration
```

### Zugriff mit Punkt-Operator

```c
beispiel.preis = 0.79;
strncpy(beispiel.name, "Apfel", 255);
printf("Ware %s mit Preis %f\n", beispiel.name, beispiel.preis);
```

### Arrays von Structs

```c
struct produkt warenkorb[100];  // Array von 100 Produkten
```

### Pointer auf Structs

```c
struct produkt *ware = warenkorb;
```

### Zugriff mit Pfeil-Operator

Bei **Pointern** auf Structs verwendet man `->` statt `.`:

```c
printf("Produkt %s mit Preis %f\n", ware->name, ware->preis);
```

### Typedef für bessere Lesbarkeit

```c
typedef struct produkt {
    char name[255];
    float preis;
} produkt_t;

produkt_t produkt1, produkt2;  // Einfachere Deklaration
```

---

## 4. Verkettete Listen (Linked Lists)

### Idee

- Jedes **Element verweist auf seinen Nachfolger**
- Elemente können an **beliebiger Stelle** eingefügt/gelöscht werden
- **Nur Pointer werden umgesetzt**, keine Daten kopiert

### Visualisierung

```
[3]→[7]→[9]→[2]→NULL

Einfügen von 4 nach 7:
[3]→[7]→[4]→[9]→[2]→NULL

Löschen von 9:
[3]→[7]→[4]→[2]→NULL
```

### Struktur eines Listenelements

```c
typedef struct _slist {
    int value;              // Daten
    struct _slist *next;    // Nachfolger
} slist;
```

⚠️ **Wichtig:** `struct _slist *next` ist notwendig, da der Typ noch nicht vollständig definiert ist.

### Wurzel (Root/Head) der Liste

Das **erste Element** wird oft "Wurzel", "Anker" oder "Kopf" genannt.

```
root → [3]→[7]→[9]→NULL
```

### Durchlaufen einer Liste

```c
slist *root, *tmp;
tmp = root;                    // Anfang an der Wurzel
while(tmp != NULL) {           // Solange Nachfolger existiert
    printf("%d\n", tmp->value); // Wert ausgeben
    tmp = tmp->next;            // Zum Nächsten Element
}
```

**Laufzeit:** $O(n)$

### Einfügen am Anfang

```c
slist *insert(slist *list_pointer, int value) {
    slist *new;
    new = (slist *) calloc(1, sizeof(slist));  // Allozieren
    
    new->value = value;                         // Initialisieren
    new->next = NULL;
    
    if(list_pointer)                            // Einhängen
        new->next = list_pointer;
    
    return(new);
}
```

**Laufzeit:** $O(1)$ (wenn Position bekannt)

---

## 5. Liste mit separater Wurzel

### Problem

Oft benötigt man zusätzliche Informationen:
- Anzahl der Listenelemente
- Pointer auf letztes Element

### Lösung: Separate Wurzelstruktur

```c
// Datentyp für Listenelement
typedef struct _list_el {
    int value;
    struct _list_el *next;
} list_el;

// Datentyp für Wurzel (Verwaltungsinformationen)
typedef struct _list {
    int count;          // Anzahl der Elemente
    list_el *first;     // Erstes Element
} list;
```

### Initialisierung

```c
list *warenliste = calloc(1, sizeof(list));

void init_list(list *list_pointer) {
    list_pointer->first = NULL;
    list_pointer->count = 0;
}

init_list(warenliste);
```

### Einfügen

```c
void list_insert(list *list_pointer, int value) {
    list_el *new = (list_el *) calloc(1, sizeof(list_el));
    new->value = value;
    new->next = list_pointer->first;
    
    list_pointer->first = new;
    list_pointer->count++;
}
```

### Ausgabe

```c
void list_print(list *list_pointer) {
    list_el *tmp = list_pointer->first;
    while(tmp) {
        printf("cur: %d ", tmp->value);
        tmp = tmp->next;
    }
    printf("\n");
}
```

---

## 6. Operationen auf Verketteten Listen

### Suchen

**Durchlaufen** bis Element gefunden oder Ende erreicht.

**Laufzeit:** $O(n)$

```
root → [3]→[7]→[9]→[2]→NULL
       ↓   ↓   ↓   ↓
     Suche nach 9...
```

### Einfügen

**An bekannter Position:** $O(1)$  
**An unbekannter Position:** $O(n)$ (muss erst gesucht werden)

```
[3]→[7]→[9]→NULL

Einfügen von 4 nach 7:
[3]→[7]→[4]→[9]→NULL  (nur Pointer umsetzen)
```

### Löschen

**An bekannter Position:** $O(1)$  
**An unbekannter Position:** $O(n)$

```
[3]→[7]→[9]→[2]→NULL

Löschen von 9:
[3]→[7]────→[2]→NULL  (Pointer umbiegen, Speicher freigeben)
```

### Versetzen eines Elements

Bei Arrays: Alle Elemente dazwischen verschieben → $O(k)$  
Bei Listen: Nur Pointer umsetzen → $O(1)$ (bei bekannten Positionen)

```
[3]→[7]→[9]→[2]→NULL

Versetze 9 nach 3:
[3]→[9]→[7]→[2]→NULL  (nur Pointer ändern)
```

---

## 7. Implementierungsvarianten

### Einfacher Kopfzeiger

```
head → [A]→[B]→[C]→NULL

Leere Liste:
head → NULL
```

### Zyklische Verkettung

```
head → [A]→[B]→[C]→[D]
        ↑______________|
```

Erleichtert das Ablaufen in vielen Fällen.

### Kopfzeiger mit Nullelement (Dummy)

```
head → [dummy]→[A]→[B]→[C]→NULL

Leere Liste:
head → [dummy]→NULL
```

**Vorteil:** Vereinfacht viele Operationen (kein Sonderfall für leere Liste).

### Zyklisch mit Nullelement

```
head → [dummy]→[A]→[B]→[C]
        ↑__________________|
```

Elegante Formulierung vieler Listenoperationen.

---

## 8. Doppelt Verkettete Listen

### Motivation

- **Rückwärtsdurchlauf** soll effizient möglich sein
- **Invertieren** nicht notwendig

### Struktur

Jedes Element hat **zwei Pointer**:
- `next`: Nachfolger
- `prev`: Vorgänger

```
NULL←[A]⇄[B]⇄[C]⇄[D]→NULL
```

### Implementierungsvarianten

**Mit Kopf- und Schlusszeiger:**
```
head → [A]⇄[B]⇄[C]⇄[D] ← tail
```

**Mit Nullelement (zyklisch):**
```
dummy ⇄ [A]⇄[B]⇄[C]⇄[D] ⇄ dummy
  ↑__________________________|
```

### Vorteile

✅ **Delete/Insert bei bekannter Position:** $O(1)$ (kein Vorgänger-Suchen nötig)  
✅ **Durchlaufrichtung frei wählbar**  
✅ **Invertieren nicht notwendig**

### Nachteile

❌ **Erhöhter Speicherbedarf** (zwei Pointer pro Element)

---

## 9. Invertieren einer Liste

### Problem

Einfach verkettete Listen können nicht rückwärts durchlaufen werden.

### Lösung: Invertierung in $O(n)$

```
Vorher:
root → [A]→[B]→[C]→[D]→NULL

Nachher:
root → [D]→[C]→[B]→[A]→NULL
```

### Algorithmus

1. Durchlaufe Liste
2. Drehe jeden Pointer um
3. Aktualisiere `root`

**Zweimaliges Invertieren** ergibt wieder die ursprüngliche Folge.

---

## 10. Stack (Stapel / Kellerspeicher)

### Definition

**Stack:** Datenstruktur mit **Last-In-First-Out (LIFO)** Prinzip.

- **Push:** Element hinzufügen
- **Pop:** Letztes Element entfernen

### Visualisierung

```
     ┌───┐
pop→ │ 5 │ ←push
     ├───┤
     │ 25│
     ├───┤
     │ 17│
     ├───┤
     │ 3 │
     └───┘
```

**"Top of Stack"** = Oberstes Element

### Anwendungen

- **Tellerstapel**
- **Browser-Historie** (Zurück-Button)
- **Funktionsaufrufe** (Call Stack)
- **Rekursion**
- **Undo/Redo-Funktionalität**

### Implementierung als Liste

```c
// push: Einfügen am Kopf
// pop: Entfernen vom Kopf
// head = "top of stack"
```

**Laufzeit:** Push und Pop in $O(1)$

### Implementierung als Array

```c
int stack[MAX_SIZE];
int tos = -1;  // Top of Stack

// Push
void push(int value) {
    tos++;
    stack[tos] = value;
}

// Pop
int pop() {
    int value = stack[tos];
    tos--;
    return value;
}
```

**Vorteil:** Schneller Zugriff  
**Nachteil:** Maximale Größe fest ("Stack Overflow" möglich)

---

## 11. Queue (Warteschlange)

### Definition

**Queue:** Datenstruktur mit **First-In-First-Out (FIFO)** Prinzip.

- **Enqueue:** Element hinten hinzufügen
- **Dequeue:** Element vorne entfernen

### Visualisierung

```
dequeue ← [5]→[25]→[17]→[3] ← enqueue
          head              tail
```

### Anwendungen

- **Mensa-Schlange**
- **Druckjobs**
- **Warteschlangen** in Betriebssystemen
- **Breadth-First-Search** (BFS) in Graphen

### Implementierung als Linked List

```c
// enqueue: Einfügen am Ende (tail)
// dequeue: Entfernen vom Anfang (head)
```

**Laufzeit:** Enqueue und Dequeue in $O(1)$

### Implementierung als Ringpuffer (Array)

```
Array: [_, _, 3, 17, 25, 5, _, _]
              ↑           ↑
             head        tail
```

Zwei Indizes `head` und `tail` wandern zyklisch durch das Array.

**Vorteil:** Schneller Zugriff  
**Nachteil:** Maximale Größe fest

---

## 12. Vergleich der Datenstrukturen

| Operation | Static Array | Dynamic Array | Linked List |
|-----------|--------------|---------------|-------------|
| **Element Access** | $O(1)$ | $O(1)$ | $O(n)$ |
| **Insert at begin** | $O(n)$ | $O(n)$ | $O(1)$ |
| **Insert at end** | $O(n)$ | $O(1)$ | $O(1)*$ |
| **Insert at known pos** | $O(n)$ | $O(n)$ | $O(1)$ |
| **Delete at known pos** | $O(n)$ | $O(n)$ | $O(1)$ |
| **Extra space** | $0$ | $O(n)$ | $O(n)$ |

\* Wenn Pointer auf Ende verfügbar

### Wann welche Datenstruktur?

**Array:**
- Wenn Größe bekannt und konstant
- Wenn häufiger Zugriff auf beliebige Elemente

**Dynamic Array:**
- Wenn Größe variiert
- Wenn hauptsächlich am Ende eingefügt/gelöscht wird

**Linked List:**
- Wenn häufiges Einfügen/Löschen in der Mitte
- Wenn Größe stark variiert
- Wenn kein direkter Zugriff nötig

**Stack:**
- LIFO-Semantik benötigt
- Funktionsaufrufe, Backtracking, Undo

**Queue:**
- FIFO-Semantik benötigt
- Warteschlangen, BFS, Puffer

---

## 📌 Zusammenfassung

### Grundlegende Konzepte

- **Arrays:** Schneller Zugriff $O(1)$, aber statische Größe
- **Dynamic Arrays:** Flexibler, aber Einfügen in Mitte teuer
- **Linked Lists:** Flexibles Einfügen/Löschen $O(1)$ bei bekannter Position

### Structs in C

- `struct` für zusammengesetzte Datentypen
- `.` für direkten Zugriff
- `->` für Zugriff über Pointer
- `typedef` für bessere Lesbarkeit

### Spezielle Datenstrukturen

| Struktur | Prinzip | Operationen | Laufzeit |
|----------|---------|-------------|----------|
| **Stack** | LIFO | push, pop | $O(1)$ |
| **Queue** | FIFO | enqueue, dequeue | $O(1)$ |

### Typische Operationen

- **Suchen:** $O(n)$ bei Listen, $O(1)$ bei Arrays (Index bekannt)
- **Einfügen:** $O(1)$ bei bekannter Position (Liste), $O(n)$ (Array)
- **Löschen:** $O(1)$ bei bekannter Position (Liste), $O(n)$ (Array)

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.05 Bäume]] – Baumstrukturen als erweiterte verkettete Strukturen
- [[VL.09 Heaps]] – Prioritätswarteschlangen
- [[VL.03 Komplexität]] – Laufzeitanalyse der Operationen