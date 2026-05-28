**Class:** [[IntroProg]]  
**Date:** VL.5  
**Topics:** #Binärbäume #BinäreSuchbäume #Traversierung #InorderTreeWalk #Suchen #Einfügen #Löschen #Baumhöhe

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt **Binäre Suchbäume** als effiziente Datenstruktur für dynamische Datenspeicherung ein.

- Verständnis von **Binärbäumen** und ihrer rekursiven Struktur
- **Binäre Suchbaumeigenschaft** und ihre Bedeutung
- **Traversierung** (Inorder-Tree-Walk)
- **Suchen, Minimum, Maximum** in $O(h)$
- **Nachfolger und Vorgänger** finden
- **Einfügen und Löschen** von Knoten
- **Laufzeitanalyse** in Abhängigkeit der Baumhöhe $h$

---

## 1. Motivation

### Problem

- **Listen:** $O(n)$ für Suchen, Einfügen, Löschen → zu langsam!
- **Bedarf:** Schnellere Datenstrukturen

### Anforderungen

- ✅ **Schneller Zugriff** (schneller als $O(n)$)
- ✅ **Schnelles Einfügen** neuer Datensätze
- ✅ **Schnelles Löschen** bestehender Datensätze

### Anwendungen

- Stammbaum
- Dateisysteme
- Entscheidungsbäume
- **Suchbäume** (Lexikon, Datenbanken)
- Rekursionsbäume

---

## 2. Binärbaum - Definition

### Formale Definition

Ein **Binärbaum** $T$ ist:
1. Entweder die **leere Menge** (leerer Baum)
2. Oder ein **Tripel** $(v, T_1, T_2)$, wobei:
   - $v$ der **Wurzelknoten** ist
   - $T_1$ der **linke Unterbaum** ist
   - $T_2$ der **rechte Unterbaum** ist
   - $V_1 \cap V_2 = \emptyset$ (disjunkte Knotenmengen)
   - $v \notin V_1 \cup V_2$

### Visualisierung

```
        6
       / \
      4   7
     /   / \
    3   7   9
```

---

## 3. Begriffe und Terminologie

### Wichtige Begriffe

| Begriff                 | Bedeutung                       | Beispiel im obigen Baum    |
| ----------------------- | ------------------------------- | -------------------------- |
| **Wurzel (root)**       | Knoten ohne Vorgänger           | 6                          |
| **Blatt (leaf)**        | Knoten ohne Nachfolger          | 3, 7 (links), 9            |
| **Interner Knoten**     | Alle Nachfolger besetzt         | 6, 7 (rechts)              |
| **Randknoten**          | Nicht alle Nachfolger besetzt   | 3, 4, 7, 9                 |
| **Vorgänger**           | Elternknoten                    | 4 ist Vorgänger von 3      |
| **Nachfolger**          | Kindknoten                      | 3 ist Nachfolger von 4     |
| **Pfad**                | Knotenfolge von Anfang bis Ende | 6 → 4 → 3                  |
| **Pfadlänge**           | Anzahl der Kanten               | Pfad 6 → 4 → 3 hat Länge 2 |
| **Tiefe eines Knotens** | Pfadlänge zur Wurzel            | Tiefe von 3 ist 2          |
| **Höhe eines Knotens**  | Höhe seines Teilbaums           | Höhe von 4 ist 1           |
| **Höhe des Baumes**     | Größte Tiefe                    | 2                          |

### Höhe eines Baumes

**Definition:** Die Höhe eines Binärbaumes ist die **Länge des längsten Pfades** von der Wurzel zu einem Blatt.

**Rekursive Formel:**
$$\text{Höhe}(v) = 1 + \max(\text{Höhe}(T_1), \text{Höhe}(T_2))$$

**Beispiele:**
- Baum mit 1 Knoten: Höhe = 0
- Baum mit 2 Ebenen: Höhe = 1

---

## 4. Binäre Suchbäume

### Suchbaumeigenschaft

**Für jeden Knoten $x$ gilt:**
- Alle Knoten im **linken Unterbaum:** $\text{key}(y) \leq \text{key}(x)$
- Alle Knoten im **rechten Unterbaum:** $\text{key}(y) > \text{key}(x)$

### Visualisierung

```
        6
       / \
      4   7
     /   / \
    3   7   9

Links ≤ 6 < Rechts
```

⚠️ **Wichtig:** Mehrfache Schlüssel sind erlaubt (hier zwei 7er).

### Darstellung im Rechner

Jeder Knoten enthält:
- `key`: Schlüssel und ggf. weitere Daten
- `lc(v)`: Zeiger auf linkes Kind (left child)
- `rc(v)`: Zeiger auf rechtes Kind (right child)
- `p(v)`: Zeiger auf Elter (parent) – optional aber nützlich
- `root(T)`: Zeiger auf Wurzel

---

## 5. Traversierung: Inorder-Tree-Walk

### Idee

Durchlaufe Baum **in sortierter Reihenfolge**.

### Algorithmus

```
Inorder-Tree-Walk(x)
1. if x ≠ nil then
2.     Inorder-Tree-Walk(lc(x))    // Linker Teilbaum
3.     Ausgabe key(x)               // Wurzel
4.     Inorder-Tree-Walk(rc(x))    // Rechter Teilbaum
```

**Aufruf:** `Inorder-Tree-Walk(root(T))`

### Funktionsweise

```
Baum:       6
           / \
          4   7
         /   / \
        3   7   9

Reihenfolge: 3, 4, 6, 7, 7, 9
```

**Ablauf:**
1. Gehe **ganz links** runter (3)
2. Ausgabe: 3
3. Zurück zu 4, Ausgabe: 4
4. Gehe rechts (nil)
5. Zurück zu 6, Ausgabe: 6
6. Gehe rechts zu 7
7. Linkes Kind von 7: Ausgabe 7
8. Ausgabe: 7 (Wurzel)
9. Rechts zu 9, Ausgabe: 9

### Laufzeitanalyse

**Jeder Knoten wird genau einmal besucht:**
- Anzahl Aufrufe für Knoten: $n$
- Anzahl Aufrufe für `nil`: $< n$ (Blätter)

$$T(n) = \Theta(n)$$

---

## 6. Suchen in Binären Suchbäumen

### Rekursive Suche

```
Baumsuche(x, k)
1. if x = nil or k = key(x) then return x
2. if k < key(x) then return Baumsuche(lc(x), k)
3. else return Baumsuche(rc(x), k)
```

**Aufruf:** `Baumsuche(root(T), k)`

### Funktionsweise

```
Suche nach 9 in:
        6
       / \
      4   7
     /   / \
    3   7   9

Schritte:
1. Start bei 6: 9 > 6 → gehe rechts
2. Bei 7: 9 > 7 → gehe rechts
3. Bei 9: gefunden! → return 9
```

### Iterative Suche

```
IterativeBaumsuche(x, k)
1. while x ≠ nil and k ≠ key(x) do
2.     if k < key(x) then x ← lc(x)
3.     else x ← rc(x)
4. return x
```

### Laufzeit

$$T(n) = O(h)$$

wobei $h$ die **Höhe des Baumes** ist.

**Best Case:** $h = \log n$ (balancierter Baum)  
**Worst Case:** $h = n$ (degeneriert zur Liste)

---

## 7. Minimum und Maximum

### Minimum suchen

**Idee:** Gehe immer **nach links**, solange möglich.

```
MinimumSuche(x)
1. while lc(x) ≠ nil do x ← lc(x)
2. return x
```

**Laufzeit:** $O(h)$

### Maximum suchen

**Idee:** Gehe immer **nach rechts**, solange möglich.

```
MaximumSuche(x)
1. while rc(x) ≠ nil do x ← rc(x)
2. return x
```

**Laufzeit:** $O(h)$

---

## 8. Nachfolger und Vorgänger

### Nachfolgersuche

**Nachfolger:** Der **nächstgrößere** Schlüssel im Baum (bzgl. Inorder-Reihenfolge).

#### Fall 1: Rechter Unterbaum nicht leer

**Nachfolger = linkester Knoten im rechten Unterbaum**

```
        6
       / \
      4   7
     /   / \
    3   7   9

Nachfolger von 6: 7 (linkester in rechtem Unterbaum)
```

#### Fall 2: Rechter Unterbaum leer

**Nachfolger = erster Vorfahr, der größer ist**

Gehe den Pfad zur Wurzel hoch, bis du von einem **linken Kind** kommst.

```
        6
       / \
      4   7
     /   / \
    3   5   9

Nachfolger von 5:
- Kein rechter Unterbaum
- Gehe hoch zu 4 (5 ist rechtes Kind → weiter)
- Gehe hoch zu 6 (4 ist linkes Kind → STOP)
- Nachfolger = 6
```

### Algorithmus

```
Nachfolgersuche(x)
1. if rc(x) ≠ nil then return MinimumSuche(rc(x))
2. y ← p(x)
3. while y ≠ nil and x = rc(y) do
4.     x ← y
5.     y ← p(y)
6. return y
```

**Laufzeit:** $O(h)$

### Vorgängersuche

**Analog zur Nachfolgersuche**, aber spiegelbildlich:
- **Fall 1:** Linker Unterbaum vorhanden → rechtester Knoten
- **Fall 2:** Gehe hoch bis du von rechtem Kind kommst

**Laufzeit:** $O(h)$

---

## 9. Einfügen in Binäre Suchbäume

### Idee

1. **Suche** die Position (wie bei Baumsuche)
2. **Finde Blatt**, an das der neue Knoten angehängt wird
3. **Ersetze `nil`-Zeiger** durch neuen Knoten

### Algorithmus

```
Einfügen(T, z)
1. y ← nil; x ← root(T)
2. while x ≠ nil do
3.     y ← x                          // y wird Elter von z
4.     if key(z) ≤ key(x) then x ← lc(x)
5.     else x ← rc(x)
6. p(z) ← y                           // Setze Elter von z
7. if y = nil then root(T) ← z        // Baum war leer
8. else
9.     if key(z) ≤ key(y) then lc(y) ← z
10.     else rc(y) ← z
```

### Beispiel: Einfügen von 8

```
Vor:            6              Nach:           6
               / \                            / \
              4   7                          4   7
             /   / \                        /   / \
            3   7   9                      3   7   9
                                                  /
                                                 8

Schritte:
1. Start bei 6: 8 > 6 → rechts
2. Bei 7: 8 > 7 → rechts
3. Bei 9: 8 < 9 → links (nil)
4. Füge 8 als linkes Kind von 9 ein
```

### Laufzeit

$$T(n) = O(h)$$

---

## 10. Löschen aus Binären Suchbäumen

### Drei Fälle

#### Fall A: Zu löschendes Element hat **keine Kinder** (Blatt)

**Lösung:** Einfach entfernen.

```
        6                    6
       / \                  / \
      4   7       →        4   7
     /   / \                  / \
    3   7   9                7   9
   (lösche 3)
```

#### Fall B: Zu löschendes Element hat **ein Kind**

**Lösung:** Ersetze Element durch sein Kind.

```
        6                    6
       / \                  / \
      4   7       →        4   9
     /   / \                  /
    3   7   9                7
   (lösche 7 rechts)
```

#### Fall C: Zu löschendes Element hat **zwei Kinder**

**Lösung:**
1. Finde **Nachfolger** des Elements
2. **Entferne Nachfolger** (hat maximal ein Kind!)
3. **Ersetze** zu löschendes Element durch Nachfolger

⚠️ **Wichtig:** Der Nachfolger hat **maximal ein rechtes Kind** (kein linkes, sonst wäre er nicht der Nachfolger).

```
        6                    7
       / \                  / \
      4   7       →        4   9
     /   / \                  /
    3   7   9                7
   (lösche 6)

Schritte:
1. Nachfolger von 6 ist 7 (linkestes in rechtem Unterbaum)
2. Entferne 7 (hat rechtes Kind 9)
3. Ersetze 6 durch 7
```

### Algorithmus

```
Löschen(T, z)
1. if lc(z) = nil or rc(z) = nil then y ← z
2. else y ← NachfolgerSuche(z)
3. if lc(y) ≠ nil then x ← lc(y)
4. else x ← rc(y)
5. if x ≠ nil then p(x) ← p(y)
6. if p(y) = nil then root(T) ← x
7. else if y = lc(p(y)) then lc(p(y)) ← x
8. else rc(p(y)) ← x
9. if y ≠ z then key(z) ← key(y)
```

**Erklärung:**
- **Zeilen 1-2:** Bestimme Knoten `y`, der tatsächlich gelöscht wird
- **Zeilen 3-4:** `x` ist das Kind von `y` (falls vorhanden)
- **Zeilen 5-8:** Verbinde `x` mit Elter von `y`
- **Zeile 9:** Kopiere Inhalt von `y` nach `z` (falls `y` Nachfolger war)

### Laufzeit

$$T(n) = O(h)$$

(wegen Nachfolgersuche)

---

## 11. Zusammenfassung der Operationen

### Laufzeiten

| Operation | Laufzeit | Bemerkung |
|-----------|----------|-----------|
| **Durchlaufen** (Inorder) | $\Theta(n)$ | Alle Knoten besuchen |
| **Suchen** | $O(h)$ | Pfad von Wurzel zu Knoten |
| **Minimum / Maximum** | $O(h)$ | Pfad nach links/rechts |
| **Nachfolger / Vorgänger** | $O(h)$ | Höchstens Pfad zur Wurzel |
| **Einfügen** | $O(h)$ | Suche + Einhängen |
| **Löschen** | $O(h)$ | Nachfolgersuche + Umlegen |

### Abhängigkeit von der Baumhöhe

**Best Case (balancierter Baum):**
$$h = O(\log n)$$
Alle Operationen: $O(\log n)$ ✅

**Worst Case (degenerierter Baum):**
$$h = O(n)$$
Alle Operationen: $O(n)$ ❌ (wie Liste!)

```
Balanciert:        Degeneriert:
      4                 1
     / \                 \
    2   6                 2
   / \ / \                 \
  1  3 5  7                 3
                             \
h = 2 (log n)                 4
                               \
                                5
                              h = 4 (n-1)
```

---

## 12. Balancierung

### Problem

- Bei **ungünstiger Einfügereihenfolge** degeneriert der Baum zur Liste
- Beispiel: Einfügen von 1, 2, 3, 4, 5 → Liste!

### Lösung

**Selbstbalancierende Suchbäume:**
- **AVL-Bäume** (später in VL.11)
- **Rot-Schwarz-Bäume**

Diese garantieren $h = O(\log n)$ auch bei beliebigen Einfüge-/Löschoperationen.

### Erhoffter Fall

Bei **zufälliger Einfügereihenfolge**:
- Baum ist **halbwegs balanciert**
- Erwartete Höhe: $O(\log n)$

---

## 📌 Zusammenfassung

### Binäre Suchbäume

**Eigenschaften:**
- Rekursive Struktur: Wurzel + zwei Unterbäume
- **Suchbaumeigenschaft:** Links ≤ Wurzel < Rechts
- Ermöglichen schnelle Operationen (wenn balanciert)

### Wichtige Algorithmen

| Algorithmus | Strategie | Laufzeit |
|-------------|-----------|----------|
| **Inorder-Tree-Walk** | Links → Wurzel → Rechts | $\Theta(n)$ |
| **Suchen** | Vergleiche und gehe links/rechts | $O(h)$ |
| **Minimum/Maximum** | Gehe ganz links/rechts | $O(h)$ |
| **Nachfolger** | Rechter Unterbaum oder Pfad hoch | $O(h)$ |
| **Einfügen** | Suche Blatt und hänge ein | $O(h)$ |
| **Löschen** | 3 Fälle: 0, 1, 2 Kinder | $O(h)$ |

### Laufzeitgarantien

- **Bester Fall:** $h = O(\log n)$ → $O(\log n)$ Operationen
- **Schlechtester Fall:** $h = O(n)$ → $O(n)$ Operationen
- **Lösung:** Selbstbalancierende Bäume (AVL, Rot-Schwarz)

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.04 Einfache Datenstrukturen]] – Bäume als erweiterte verkettete Strukturen
- [[VL.11 AVL-Bäume]] – Selbstbalancierende Suchbäume
- [[VL.09 Heaps]] – Spezielle Baumstruktur für Prioritätswarteschlangen
- [[VL.03 Komplexität]] – Laufzeitanalyse $O(h)$ vs. $O(\log n)$ vs. $O(n)$