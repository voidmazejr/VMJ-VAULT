**Class:** [[IntroProg]]  
**Date:** VL.11  
**Topics:** #AVLBaum #BinaererSuchbaum #Rotation #Balancierung #Einfügen #Löschen #Traversierung #Komplexität #SelbstBalancierend

---

## 🎯 Lernziele der Vorlesung

Diese Vorlesung behandelt **AVL-Bäume** als selbst-balancierende Suchbäume.

- Motivation für balancierte Bäume (Problem degenerierter Bäume)
- **AVL-Definition** und Höhenbeweis
- **Rotationen** (Links- und Rechtsrotation, Doppelrotation)
- **Balance-Funktion** zur Wiederherstellung der AVL-Eigenschaft
- **Einfügen** und **Löschen** im AVL-Baum
- Laufzeit aller Operationen: $\Theta(\log n)$
- Traversierungsmethoden

---

## 1. Wiederholung: Binäre Suchbäume

### Binäre Suchbaumeigenschaft

Sei $x$ ein Knoten im binären Suchbaum:

- Ist $y$ Knoten im **linken** Unterbaum von $x$, dann gilt $\text{key}(y) \leq \text{key}(x)$
- Ist $y$ Knoten im **rechten** Unterbaum von $x$, dann gilt $\text{key}(y) > \text{key}(x)$

### Darstellung im Rechner

Jeder Knoten $v$ enthält:

- Schlüssel $\text{key}$
- Zeiger $\text{lc}(v)$ auf linkes Kind, $\text{rc}(v)$ auf rechtes Kind
- Parentzeiger $p(v)$ auf den Elternknoten
- Wurzelzeiger $\text{root}(T)$ auf die Wurzel des Baums $T$

### Problem: Degenerierte Bäume

⚠️ **Kernproblem:** Die Komplexität der Operationen hängt von der Höhe $h$ ab.

- Ein **freier** (unkontrollierter) Baum kann degenerieren → wird zur linearen Liste
- Im Worst Case: $h = O(n)$ → alle Operationen $O(n)$
- **Formgebung und -erhaltung** sind essenziell für die Effizienz

---

## 2. Balancierte Suchbäume

### Ziel

Sicherstellen, dass die Höhe der Teilbäume **ungefähr gleich** ist → Höhe des Baumes: $O(\log n)$

### Selbst-balancierende Bäume

Bei jeder Operation (Einfügen/Löschen) wird sichergestellt, dass der Baum **relativ balanciert** bleibt:

- Einfügen und Löschen werden teurer
- Aber Suchen garantiert $O(\log n)$

**Beispiele selbst-balancierender Bäume:** AVL-Bäume, 2-3-Bäume, 2-3-4-Bäume, Rot-Schwarz-Bäume

### Typen von Optimierungen

|Typ|Beschreibung|Beispiel|
|---|---|---|
|**Dynamisch optimiert**|Einfügen/Löschen wirken form-erhaltend|AVL-Bäume|
|**Dynamisch mit Gewichten**|Häufiger zugegriffene Elemente günstiger platziert|Splay Trees|
|**Statisch konstruiert**|Neustrukturierung nur bei Bedarf|—|

---

## 3. AVL-Bäume: Definition

### Definition

**AVL-Baum** [Adelson-Velsky und Landis]: Ein binärer Suchbaum heißt AVL-Baum, wenn für **jeden Knoten** gilt:

$$\boxed{|h(\text{lc}(v)) - h(\text{rc}(v))| \leq 1}$$

Die Höhe des linken und rechten Teilbaums unterscheidet sich **höchstens um 1**.

---

## 4. AVL-Bäume: Höhenbeweis

### Satz

Für jeden AVL-Baum der Höhe $h \geq 0$ mit $n$ Knoten gilt:

$$\left(\frac{3}{2}\right)^h \leq n \leq 2^{h+1} - 1$$

### Beweis: Obere Schranke $n \leq 2^{h+1} - 1$

- AVL-Baum ist ein Binärbaum
- Ein **vollständiger Binärbaum** hat maximale Knotenanzahl unter allen Binärbäumen der Höhe $h$:

$$N(h) = \sum_{i=0}^{h} 2^i = 2^{h+1} - 1$$

### Beweis: Untere Schranke $\left(\frac{3}{2}\right)^h \leq n$

Beweis per **Induktion über die Struktur** von AVL-Bäumen.

Sei $T(h)$ die minimale Anzahl Knoten in einem AVL-Baum der Tiefe $h$.

**Induktionsanfang:**

- $h=0$: Ein Knoten. Es gilt $\left(\frac{3}{2}\right)^0 = 1 \leq 1$ ✅
- $h=1$: 2 oder 3 Knoten. Es gilt $\left(\frac{3}{2}\right)^1 = \frac{3}{2} \leq 2$ ✅

**Induktionsschritt** ($h \geq 1$): Betrachte AVL-Baum $T$ der Höhe $h+1$ mit Wurzel $v$, linkem Teilbaum $A$, rechtem Teilbaum $B$:

- $A$ oder $B$ (oder beide) hat Höhe $h$
- Wegen AVL-Eigenschaft haben $A$ und $B$ Höhe mindestens $h-1 \geq 0$
- Da $T$ AVL-Baum, sind auch $A$ und $B$ AVL-Bäume → Induktionshypothese anwendbar:

$$T(h+1) \geq T(h) + T(h-1) + 1 \geq \left(\frac{3}{2}\right)^h + \left(\frac{3}{2}\right)^{h-1} + 1 \geq \left(\frac{3}{2}\right)^{h+1}$$

### Korollar: Höhe $\Theta(\log n)$

**Beweis $h = O(\log n)$:** Aus $n \geq \left(\frac{3}{2}\right)^h$ folgt:

$$\log n \geq h \cdot \log!\left(\frac{3}{2}\right) \implies h \leq \frac{\log n}{\log(3/2)} \implies h = O(\log n)$$

**Beweis $h = \Omega(\log n)$:** Aus $n \leq 2^{h+1} - 1 \leq 2^{h+1}$ folgt:

$$\log n \leq h + 1 \implies h \geq \log n - 1 \implies h = \Omega(\log n)$$

$$\boxed{h = \Theta(\log n)}$$

---


### Motivation

Rotationen sind die grundlegende Umstrukturierungsoperation, um die AVL-Eigenschaft nach Einfügen/Löschen wiederherzustellen. Sie **erhalten die Suchbaumeigenschaft**.

### Rechtsrotation

```
Vorher:          Nachher:
    x                y
   / \              / \
  y   C            A   x
 / \                   / \
A   B                 B   C
```

Rechtsrotation von $y$: $x$ wird neue Wurzel, $B$ wird linkes Kind von $y$.

### Linksrotation (symmetrisch)

```
Vorher:          Nachher:
  x                  y
 / \                / \
A   y              x   C
   / \            / \
  B   C          A   B
```

### Pseudocode: Linksrotation

```
Linksrotation(x):
1. y ← rc[x]
2. rc[x] ← lc[y]
3. if lc[y] ≠ nil then p[lc[y]] ← x
4. p[y] ← p[x]
5. if p[x] = nil then root[T] ← y      // x war Wurzel!
6. else if x = lc[p[x]] then lc[p[x]] ← y
7. else rc[p[x]] ← y
8. lc[y] ← x
9. p[x] ← y
```

⚠️ **Wichtig:** Wenn $x$ die Wurzel war ($p[x] = \texttt{nil}$), muss `root[T]` aktualisiert werden!

### Symmetrie

$$\text{Rechtsrotation}(y) \circ \text{Linksrotation}(x) = \text{Identität}$$

Die beiden Rotationen sind **inverse Operationen** zueinander.

---

## 6. Balance-Funktion

### Beinahe-AVL-Baum

**Definition:** Ein Baum heißt **beinahe-AVL-Baum**, wenn:

- Die AVL-Eigenschaft in jedem Knoten **außer der Wurzel** erfüllt ist
- Die Höhen der Unterbäume der Wurzel sich um **höchstens 2** unterscheiden

### Balance-Algorithmus

```
Balance(y):
1. if h[lc[y]] > h[rc[y]] + 1 then       // Linker Teilbaum zu hoch
2.     if h[lc[lc[y]]] < h[rc[lc[y]]] then
3.         Linksrotation(lc[y])            // Fall 2: Doppelrotation
4.     Rechtsrotation(y)                   // Fall 1 oder nach Linksrotation
5. else if h[rc[y]] > h[lc[y]] + 1 then   // Rechter Teilbaum zu hoch
6.     if h[rc[rc[y]]] < h[lc[rc[y]]] then
7.         Rechtsrotation(rc[y])           // Doppelrotation (symmetrisch)
8.     Linksrotation(y)
```

⚠️ **Hinweis:** Die Höhe $h$ muss als **zusätzliches Feld** im Knoten gespeichert und bei jeder Operation aktualisiert werden.

### Fall 1: Einfache Rechtsrotation

**Situation:** Linker Teilbaum von Höhe $h$, rechter von Höhe $h-1$, linkes Kind des linken Teilbaums hat Höhe $h$ oder $h-1$.

```
Vorher (beinahe-AVL):      Nachher (AVL):
        y (h+1)                  x
       / \                      / \
      x   C(h-1)            A(h/h-1) y
     / \                          / \
  A(h/h-1) B(h)              B(h)  C(h-1)
```

→ **Eine** Rechtsrotation reicht aus.

### Fall 2: Doppelrotation (Links-Rechts)

**Situation:** Linker Teilbaum von Höhe $h$, rechter von Höhe $h-1$, **rechtes** Kind des linken Teilbaums hat Höhe $h-1$.

```
Vorher:              Nach Linksrotation(x):    Nach Rechtsrotation(y):
    y                        y                          z
   / \                      / \                        / \
  x   C(h-1)              z   C(h-1)                 x   y
 / \                     / \                         /\ /\
A(h-1) z(h-1)          x   B''                     A B' B'' C
      / \             / \
     B'  B''      A(h-1) B'
```

→ **Zwei** Rotationen: erst Links-, dann Rechtsrotation.

---

## 7. AVL-Einfügen

### Algorithmus

```
AVL-Einfügen(t, x):
1. if t = nil then
2.     t ← new node(x); h[t] ← 0; return
3. else if key[x] < key[t] then AVL-Einfügen(lc[t], x)
4. else if key[x] > key[t] then AVL-Einfügen(rc[t], x)
5. else return                         ▷ Schlüssel schon vorhanden
6. h[t] ← 1 + max{h[lc[t]], h[rc[t]]}
7. Balance(t)
```

**Aufruf:** `AVL-Einfügen(root[T], x)`

### Vorgehen

1. Suche rekursiv die richtige Position (wie bei normalem BST)
2. Füge neuen Knoten als Blatt ein
3. Aktualisiere auf dem Rückweg die **Höhen**
4. Rufe **Balance** auf, um AVL-Eigenschaft wiederherzustellen

### Satz: Höhe nach Einfügen

> Wird ein Element in einen AVL-Baum der Höhe $h$ eingefügt, so ist der resultierende Baum ein AVL-Baum der Höhe $h$ oder $h+1$.

**Beweis (Induktion):**

- **I.A.:** Für Bäume der Höhe 0 und 1 korrekt.
- **I.V.:** Der Satz gilt für Bäume der Höhe $j$, $1 \leq j \leq h$.
- **I.S.:** Nach I.V. hat $\text{lc}[t]$ nach Einfügen Höhe $r$ oder $r+1$:
    - Falls Höhe $\leq h$: $t$ bleibt AVL-Baum
    - Falls Höhe $h+1$: $t$ ist u.U. beinahe-AVL-Baum → `Balance` korrigiert dies
    - `Balance` erhöht Höhe nicht und verringert sie maximal um 1

---

## 8. AVL-Löschen

### Algorithmus

```
AVL-Löschen(t, x):
1. if t = nil then return               ▷ x nicht im Baum
2. else if x < key[t] then AVL-Löschen(lc[t], x)
3. else if x > key[t] then AVL-Löschen(rc[t], x)
4. else if lc[t] = nil then ersetze t durch rc[t]
5. else if rc[t] = nil then ersetze t durch lc[t]
6. else u = MaximumSuche(lc[t])         ▷ Inorder-Vorgänger
7.     Kopiere Informationen von u nach t
8.     AVL-Löschen(lc[t], key[u])
9. if t ≠ nil then h[t] = 1 + max{h[lc[t]], h[rc[t]]}
10. Balance(t)
```

### Fälle beim Löschen

|Fall|Bedingung|Aktion|
|---|---|---|
|Nicht gefunden|`t = nil`|Abbruch|
|Linkes Kind fehlt|`lc[t] = nil`|Ersetze `t` durch `rc[t]`|
|Rechtes Kind fehlt|`rc[t] = nil`|Ersetze `t` durch `lc[t]`|
|Beide Kinder vorhanden|sonst|Inorder-Vorgänger $u$ kopieren, $u$ rekursiv löschen|

⚠️ **Achtung:** Eventuell muss die Wurzel des Baums (`root[T]`) angepasst werden!

### Satz: Höhe nach Löschen

> Wird ein Element aus einem AVL-Baum der Höhe $h$ gelöscht, so ist der resultierende Baum ein AVL-Baum der Höhe $h$ oder $h-1$.

**Beweis:** Analog zum Einfügen.

---

## 9. Laufzeit aller Operationen

### Satz

> Mithilfe von AVL-Bäumen kann man **Suche, Einfügen, Löschen, Minimum und Maximum** in einer Menge von $n$ Zahlen in $\Theta(\log n)$ Laufzeit durchführen.

|Operation|Laufzeit|
|---|---|
|**Suche**|$\Theta(\log n)$|
|**Einfügen**|$\Theta(\log n)$|
|**Löschen**|$\Theta(\log n)$|
|**Minimum / Maximum**|$\Theta(\log n)$|
|**Rotation**|$\Theta(1)$|

**Begründung:** Da $h = \Theta(\log n)$ und alle Operationen $O(h)$ kosten, folgt $\Theta(\log n)$ für alle Operationen.

---

## 10. Bäume: Allgemeines

### t-ärer Baum

**Definition:** Ein $t$-ärer Baum ist entweder die **leere Menge** oder ein Knoten, der ein Datum und $t$ Kindbäume enthält.

- **Binärbaum** = 2-ärer Baum

### Typen nach Datenspeicherung

- **Knotenorientierte Bäume:** Daten liegen in den Knoten
- **Blattorientierte Bäume:** Daten nur in den Blättern; innere Knoten enthalten nur Zugriffsinformation
- **Kantenorientierte Bäume:** Daten in den Kanten

### Implementierung

**Im Array (dichte Speicherung):**

- Vorgänger/Nachfolger durch Indexrechnung
- Gut für linksvolle oder rechtsvolle Bäume

**Per Pointer (gestreute Speicherung):**

- Baumklasse hat Referenz auf Wurzel
- Zeiger zu den Kindern
- Optional: Rückverweis von Blättern zur Wurzel

---

## 11. Traversierung von Bäumen

### Die vier Traversierungsarten

| Traversierung   | Reihenfolge                        | Kategorie     |
| --------------- | ---------------------------------- | ------------- |
| **In-order**    | Links → Knoten → Rechts            | Depth-first   |
| **Pre-order**   | Knoten → Links → Rechts            | Depth-first   |
| **Post-order**  | Links → Rechts → Knoten            | Depth-first   |
| **Level-order** | Schicht für Schicht von der Wurzel | Breadth-first |


### Wichtige Eigenschaft: In-order bei BST

⚠️ **In-order-Traversierung** eines binären Suchbaums liefert die Schlüssel in **aufsteigend sortierter Reihenfolge**!

### Implementierung

- **Depth-first** (Pre-, In-, Post-order): Rekursiv oder mit **Stack**
- **Level-order** (Breadth-first): Mit **Queue**

---

## 📌 Zusammenfassung

### AVL-Baum auf einen Blick

**Definition:** BST, bei dem sich die Höhe von linkem und rechtem Teilbaum jedes Knotens um **höchstens 1** unterscheidet.

**Höhe:** $h = \Theta(\log n)$, da $\left(\frac{3}{2}\right)^h \leq n \leq 2^{h+1} - 1$

**Alle Operationen:** $\Theta(\log n)$

### Rotationsregeln beim Einfügen/Löschen

|Situation|Lösung|
|---|---|
|Linker Teilbaum zu hoch, linkes Kind des linken TB höher|Einfache **Rechtsrotation**|
|Linker Teilbaum zu hoch, rechtes Kind des linken TB höher|**Links-Rechts-Doppelrotation**|
|Rechter Teilbaum zu hoch, rechtes Kind des rechten TB höher|Einfache **Linksrotation**|
|Rechter Teilbaum zu hoch, linkes Kind des rechten TB höher|**Rechts-Links-Doppelrotation**|

### Vergleich: Freier BST vs. AVL-Baum

|Aspekt|Freier BST|AVL-Baum|
|---|---|---|
|**Höhe**|$O(n)$ im Worst Case|$\Theta(\log n)$ garantiert|
|**Suche**|$O(n)$ WC|$\Theta(\log n)$|
|**Einfügen**|$O(n)$ WC|$\Theta(\log n)$|
|**Löschen**|$O(n)$ WC|$\Theta(\log n)$|
|**Overhead**|Keiner|Rotationen + Höhenspeicherung|

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.05 Bäume]] – Binärbäume, Traversierung, BST-Grundlagen
- [[VL.03 Komplexität]] – Komplexitätsanalyse, $O$-, $\Omega$-, $\Theta$-Notation
- [[VL.06 Divide and Conquer]] – Rekursionsprinzip
- [[VL.09 Heaps]] – Andere Baumstruktur mit Heap-Eigenschaft