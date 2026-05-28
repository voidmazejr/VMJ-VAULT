**Class:** [[IntroProg]]  
**Date:** VL.1  
**Topics:** #Algorithmen #Pseudocode #InsertionSort #Sortieren #Informatik

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt in die Grundlagen der **Algorithmik** ein – ein zentraler Teil der Informatik. Ziel ist es, algorithmisches Denken zu entwickeln und erste Sortieralgorithmen zu verstehen.

- Verständnis von **Algorithmus vs. Programm**
- Arbeiten mit **Pseudocode**
- Kenntnis von **Insertion Sort**
- Verständnis der Begriffe **Korrektheit, Effizienz, Terminierung**

---

## 1. Was ist Informatik?

### Verschiedene Definitionen

**Donald Knuth:**  
> "The study of algorithms"
- Algorithmen = was man einem Computer beibringen kann
- Welche Funktionen können effizient berechnet werden?

**Juris Hartmanis:**  
> "Study of information"
- Wie man Information repräsentiert und verarbeitet
- Und die Maschinen, die das tun

**Fred Brooks:**  
> "CS = engineering"
- Informatik ist mehr Engineering als Wissenschaft
- Fokus auf "making": Computer bauen, Software-Systeme entwickeln

**Peter Denning:**  
> "Computing is a 4th great domain of science"
- Neben Physik, Biowissenschaften und Sozialwissenschaften
- Informatik = discovery (Wissenschaft) + implementation (Engineering) von Informationsprozessen

### Kernaussage

⚠️ **Algorithmisches Denken ist die Grundlage der Informatik**  
Algorithmen und Datenstrukturen finden sich überall in der Informatik wieder.

---

## 2. Programm vs. Algorithmus

### Unterschiede

| Aspekt | Algorithmus | Programmiersprache |
|--------|-------------|-------------------|
| **Fokus** | Korrektheit, Vollständigkeit, Komplexität | Alle Details des Computers |
| **Beschreibung** | Prinzipielle Elemente | Exakte Syntax und Semantik |
| **Abstraktionslevel** | Hoch | Niedrig (maschinenorientiert) |

**Algorithmus:**
- Beschreibt in prinzipiellen Elementen, was ein Computer ausführen soll
- "Die Essenz eines Programms"

**Programmiersprache:**
- Stellt Schnittstelle dar, um Algorithmen zu definieren und auszuführen
- Muss alle technischen Details berücksichtigen

---

## 3. Wichtige Aspekte von Algorithmen

Ein **Algorithmus** ist eine Liste von Anweisungen für den Computer.

### Drei zentrale Eigenschaften:

1. **Korrektheit**  
   Erfüllt der Algorithmus seine Anforderungen?

2. **Effizienz**  
   Wie viel Zeit und Speicherplatz braucht er?

3. **Terminierung**  
   Hält der Algorithmus immer an?

---

## 4. Pseudocode

### Was ist Pseudocode?

- **Beschreibungssprache** für Algorithmen
- **Losgelöst** von spezifischer Programmiersprache
- Manchmal ist ein vollständiger Satz die beste Beschreibung

### Was wird ignoriert?

- Variablen-Deklaration
- Bibliotheken
- Modularität
- Fehlerbehandlung

🎯 **Ziel:** Exakte, kompakte, einfache Notation

### Pseudocode-Konventionen

#### Zuweisungen
```
x ← 5
key ← A[j]
```

#### Schleifen
```
for j ← 2 to length(A) do
    // Anweisungen

while i > 0 and A[i] > key do
    // Anweisungen
```

#### Bedingte Verzweigungen
```
if summe > 9000 then
    print "over nine thousand"
```

#### Arrays
```
A[1]        // Erstes Element (Indizierung beginnt bei 1!)
A[i]        // i-tes Element
A[i+1]      // Nächstes Element
length(A)   // Länge des Arrays
```

⚠️ **Wichtig:** In Pseudocode beginnt die Indizierung bei **1**, nicht bei 0!

#### Blockstruktur
- Durch **Einrücken** dargestellt
- Klammern nicht unbedingt benötigt

#### Funktionen
- **Call-by-value:** Kopie der Variable wird übergeben
- Bei Objekten: Zeiger wird kopiert → Änderungen am Objekt sind global sichtbar
- **return** für Rückgabewerte

#### Kommentare
```
// Kommentar
> Alternativer Kommentar
```

### Beispiel: Zweier-Potenzen

```
m ← 0
p ← 1
while p < n do
    Ausgabe von: "2^m ist p"
    m ← m + 1
    p ← p * 2
```

---

## 5. Insertion Sort

### Das Sortierproblem

**Eingabe:** Folge von $n$ Zahlen $(a_1, a_2, \ldots, a_n)$

**Ausgabe:** Permutation $(a'_1, a'_2, \ldots, a'_n)$ von $(a_1, a_2, \ldots, a_n)$,  
sodass gilt: $a'_1 \leq a'_2 \leq \ldots \leq a'_n$

**Beispiel:**
- Eingabe: `15, 7, 3, 18, 8, 4`
- Ausgabe: `3, 4, 7, 8, 15, 18`

### Insertion Sort Algorithmus

```
InsertionSort(Array A)
1. for j ← 2 to length(A) do
2.     key ← A[j]
3.     i ← j-1
4.     while i>0 and A[i]>key do
5.         A[i+1] ← A[i]
6.         i ← i-1
7.     A[i+1] ← key
```

### Idee von Insertion Sort

1. Die ersten $j-1$ Elemente sind **sortiert** (zu Beginn $j=2$)
2. In jedem Schleifendurchlauf wird das $j$-te Element **in die sortierte Folge eingefügt**
3. Am Ende ist die gesamte Folge sortiert

### Funktionsweise Schritt für Schritt

**Gegeben:** `8 15 3 14 7 6 18 19`

#### Iteration j=2:
- `key = 15`
- 15 ist bereits größer als 8
- Array: `8 15 3 14 7 6 18 19` ✓

#### Iteration j=3:
- `key = 3`
- Verschiebe alle Elemente > 3 nach rechts
- 15 → Position 3
- 8 → Position 2
- Füge 3 an Position 1 ein
- Array: `3 8 15 14 7 6 18 19` ✓

#### Iteration j=4:
- `key = 14`
- Verschiebe 15 nach rechts
- Füge 14 zwischen 8 und 15 ein
- Array: `3 8 14 15 7 6 18 19` ✓

#### Iteration j=5:
- `key = 7`
- Verschiebe 15, 14, 8 nach rechts
- Füge 7 zwischen 3 und 8 ein
- Array: `3 7 8 14 15 6 18 19` ✓

#### Iteration j=6:
- `key = 6`
- Verschiebe 15, 14, 8, 7 nach rechts
- Füge 6 zwischen 3 und 7 ein
- Array: `3 6 7 8 14 15 18 19` ✓

#### Iteration j=7 und j=8:
- 18 und 19 sind bereits an der richtigen Position
- **Fertig!** Array: `3 6 7 8 14 15 18 19` ✓

### Invariante (wichtig für Korrektheit!)

Nach jedem Durchlauf der äußeren Schleife gilt:
> Die Elemente $A[1 \ldots j-1]$ sind sortiert und enthalten die ursprünglichen Elemente aus diesen Positionen.

### Visualisierung

```
Sortiert | Unsortiert
---------|----------
[8]      | 15 3 14 7 6 18 19    (j=2)
[8 15]   | 3 14 7 6 18 19       
[3 8 15] | 14 7 6 18 19         (j=3)
[3 8 14 15] | 7 6 18 19         (j=4)
[3 7 8 14 15] | 6 18 19         (j=5)
[3 6 7 8 14 15] | 18 19         (j=6)
[3 6 7 8 14 15 18 19] |         FERTIG!
```

---

## 📌 Zusammenfassung

- **Informatik:** Studie von Algorithmen und Informationsverarbeitung
- **Algorithmus:** Liste von Anweisungen mit Fokus auf Korrektheit, Effizienz, Terminierung
- **Pseudocode:** Abstrakte, kompakte Beschreibungssprache für Algorithmen
- **Insertion Sort:** Einfacher Sortieralgorithmus, der Elemente nacheinander in sortierte Sequenz einfügt
- **Kernfragen:**
  - Wie bestimmt man die Laufzeit eines Algorithmus?
  - Wie beweist man die Korrektheit eines Algorithmus?

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Simple-Sort]] – Weitere Sortieralgorithmen (Selection Sort, Bubble Sort, Count Sort)
- [[VL.3 Laufzeit und Speicherplatz]] – Laufzeitanalyse von Insertion Sort
- [[VL.4 Datenstrukturen]] – Arrays als Grundlage für Sortieralgorithmen
- [[VL.7 Korrektheitsbeweise]] – Beweis der Korrektheit von Insertion Sort