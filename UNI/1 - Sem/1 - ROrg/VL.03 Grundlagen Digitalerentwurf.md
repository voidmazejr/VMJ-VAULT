**Class:** [[ROrg]]  
**Date:** 2025  
**Topics:** #Digitaltechnik #Logikgatter #BooleescheAlgebra #ALU #Multiplexer #Decoder #CarryLookAhead #Schaltwerke #FlipFlops #Register

---

## 🎯 Lernziele der Vorlesung

Grundlegende digitale Bausteine verstehen und kombinieren können.

- **Grundlegende logische Gatter** verstehen
- **Wahrheitstabellen** aufstellen und interpretieren
- **Disjunktive (DNF)** und **konjunktive Normalform (KNF)** ableiten
- **Funktional vollständige Operatorensätze** beweisen
- **Arithmetisch logische Einheit (ALU)** konstruieren
- **Carry-Look-Ahead (CLA) Addierer** erklären
- **Speicherelemente** verstehen: SR-Latch, D-Latch, Flip-Flop, Registersatz

---

## 1. Digitalentwurf und Hierarchie

### Hierarchischer Entwurf

Digitale Hardware wird auf verschiedenen Abstraktionsebenen konstruiert:

```
┌─────────────────────────┐
│   Mikroarchitektur      │
│  ┌────────────────────┐ │
│  │ Funktionale        │ │
│  │ Einheiten          │ │
│  │  ┌──────────────┐  │ │
│  │  │ Logikgatter  │  │ │
│  │  │  ┌─────────┐ │  │ │
│  │  │  │Transist.│ │  │ │
│  │  │  └─────────┘ │  │ │
│  │  └──────────────┘  │ │
│  └────────────────────┘ │
└─────────────────────────┘
```

**Hardware Description Language (HDL):** Höhere Sprache für abstrakteren Entwurf

**Digitale Schaltungen:** Verarbeiten 2 diskrete Signalzustände
- **Logisch 0:** LOW, GND, aus
- **Logisch 1:** HIGH, $V_{DD}$, ein

---

## 2. Grundlegende Logikgatter

### Die drei Basis-Gatter

| Gatter          | Symbol                                          | Aussagelogik          | C-Syntax             | Schaltalgebra               |
| --------------- | ----------------------------------------------- | --------------------- | -------------------- | --------------------------- |
| **UND** (AND)   | ![[AND.png\|100]]                               | $Q = A \land B$       | `Q = A & B`          | $Q = A \cdot B = AB$        |
| **ODER** (OR)   | ![[Screenshot 2026-01-22 at 11.04.52.png\|100]] | $Q = A \lor B$        | `Q = A \| B`         | $Q = A + B$                 |
| **NICHT** (NOT) | ![[Screenshot 2026-01-22 at 11.05.15.png\|100]] | $\text{out} = \neg A$ | `out = !A` oder `~A` | $\text{out} = \overline{A}$ |

### Wahrheitstabellen

**UND (AND):**

| $A$ | $B$ | $AB$ |
|-----|-----|------|
| 0   | 0   | 0    |
| 0   | 1   | 0    |
| 1   | 0   | 0    |
| 1   | 1   | 1    |

**ODER (OR):**

| $A$ | $B$ | $A+B$ |
|-----|-----|-------|
| 0   | 0   | 0     |
| 0   | 1   | 1     |
| 1   | 0   | 1     |
| 1   | 1   | 1     |

**NICHT (NOT):**

| $A$ | $\overline{A}$ |
|-----|----------------|
| 0   | 1              |
| 1   | 0              |

---

## 3. Weitere wichtige Gatter

### NAND, NOR, XOR

**NAND (NOT AND):**

$$\boxed{\text{NAND: } Q = \overline{AB} = \overline{A} + \overline{B}}$$

| $A$ | $B$ | $A$ NAND $B$ |
|-----|-----|--------------|
| 0   | 0   | 1            |
| 0   | 1   | 1            |
| 1   | 0   | 1            |
| 1   | 1   | 0            |

**NOR (NOT OR):**

$$\boxed{\text{NOR: } Q = \overline{A+B} = \overline{A} \cdot \overline{B}}$$

| $A$ | $B$ | $A$ NOR $B$ |
|-----|-----|-------------|
| 0   | 0   | 1           |
| 0   | 1   | 0           |
| 1   | 0   | 0           |
| 1   | 1   | 0           |

**XOR (Exklusiv-ODER):**

$$\boxed{\text{XOR: } Q = A \oplus B = A\overline{B} + \overline{A}B}$$

| $A$ | $B$ | $A$ XOR $B$ |
|-----|-----|-------------|
| 0   | 0   | 0           |
| 0   | 1   | 1           |
| 1   | 0   | 1           |
| 1   | 1   | 0           |

### Größere Gatter (n-Input)

**n-Input AND-Gatter:**
- Ausgang = 1, **nur wenn ALLE** Eingänge = 1

**n-Input OR-Gatter:**
- Ausgang = 0, **nur wenn ALLE** Eingänge = 0

**Beispiel: 3-Input AND:**

| $A$ | $B$ | $C$ | $Q = ABC$ |
|-----|-----|-----|-----------|
| 0   | 0   | 0   | 0         |
| 0   | 0   | 1   | 0         |
| 0   | 1   | 0   | 0         |
| 0   | 1   | 1   | 0         |
| 1   | 0   | 0   | 0         |
| 1   | 0   | 1   | 0         |
| 1   | 1   | 0   | 0         |
| 1   | 1   | 1   | 1         |

---

## 4. Boolesche Algebra

### Grundlagen nach George Boole (1815-1864)

**Algebra der Logik mit zwei Werten: 0 und 1**

### Axiome der Booleschen Algebra

**Neutrale Elemente:**
- $a \cdot 1 = a$
- $a + 0 = a$

**Komplementäre Elemente:**
- $a \cdot \overline{a} = 0$
- $a + \overline{a} = 1$

**Kommutativgesetze:**
- $a \cdot b = b \cdot a$
- $a + b = b + a$

**Distributivgesetze:**
- $(a + b) \cdot c = a \cdot c + b \cdot c$
- $a + (b \cdot c) = (a + b) \cdot (a + c)$

⚠️ **Operator-Priorität:** UND ($\cdot$) hat höhere Priorität als ODER ($+$)
- $a + b \cdot c = a + (b \cdot c)$

### Weitere wichtige Gesetze

**Idempotenzgesetze:**
- $a \cdot a = a$
- $a + a = a$

**Assoziativgesetze:**
- $a \cdot (b \cdot c) = (a \cdot b) \cdot c$
- $a + (b + c) = (a + b) + c$

**De Morgansche Gesetze:**

$$\boxed{\overline{a + b} = \overline{a} \cdot \overline{b}}$$

$$\boxed{\overline{a \cdot b} = \overline{a} + \overline{b}}$$

**Beweis (Wahrheitstabelle):**

| $a$ | $b$ | $\overline{a+b}$ | $\overline{a} \cdot \overline{b}$ |
|-----|-----|------------------|-----------------------------------|
| 0   | 0   | 1                | 1                                 |
| 0   | 1   | 0                | 0                                 |
| 1   | 0   | 0                | 0                                 |
| 1   | 1   | 0                | 0                                 |

---

## 5. Normalformen

### Schaltnetz (Combinational Logic)

$$\boxed{\text{Schaltnetz: Ausgänge hängen NUR von aktuellen Eingängen ab}}$$

**Eigenschaften:**
- Bausteine, die Daten verarbeiten
- Keine internen Zustände
- Keine Rückkopplung ohne Speicherelemente

### Disjunktive Normalform (DNF)

**Definition:** Disjunktion (ODER-Verknüpfung) von Konjunktionen (UND-Verknüpfungen)

$$\boxed{\text{DNF} = \sum \text{ (Produkte)} = \text{Sum of Products}}$$

**Beispiel:**

$$Z = AB + \overline{A}B$$

**Algorithmus (aus Wahrheitstabelle):**

1. Für jede Zeile mit Ausgang = 1:
2. Bilde eine Konjunktion aller Variablen:
   - Variable = 1 → nicht negiert
   - Variable = 0 → negiert
3. Verknüpfe alle Konjunktionen mit ODER

### Konjunktive Normalform (KNF)

**Definition:** Konjunktion (UND-Verknüpfung) von Disjunktionen (ODER-Verknüpfungen)

$$\boxed{\text{KNF} = \prod \text{ (Summen)} = \text{Product of Sums}}$$

**Beispiel:**

$$F = (A+B)(\overline{A}+B)$$

**Algorithmus (aus Wahrheitstabelle):**

1. Für jede Zeile mit Ausgang = 0:
2. Bilde eine Disjunktion aller Variablen:
   - Variable = 1 → negiert
   - Variable = 0 → nicht negiert
3. Verknüpfe alle Disjunktionen mit UND

### Beispiel: Volladdierer (Full Adder)

**Wahrheitstabelle:**

| $A$ | $B$ | $C_{in}$ | $C_{out}$ | $S$ |
|-----|-----|----------|-----------|-----|
| 0   | 0   | 0        | 0         | 0   |
| 0   | 0   | 1        | 0         | 1   |
| 0   | 1   | 0        | 0         | 1   |
| 0   | 1   | 1        | 1         | 0   |
| 1   | 0   | 0        | 0         | 1   |
| 1   | 0   | 1        | 1         | 0   |
| 1   | 1   | 0        | 1         | 0   |
| 1   | 1   | 1        | 1         | 1   |

**DNF für $C_{out}$:**

$$C_{out} = \overline{A}BC_{in} + A\overline{B}C_{in} + AB\overline{C_{in}} + ABC_{in}$$

**DNF für $S$:**

$$S = \overline{A}\,\overline{B}C_{in} + \overline{A}B\overline{C_{in}} + A\overline{B}\,\overline{C_{in}} + ABC_{in}$$

---

## 6. Funktional vollständige Operatorensätze

### Definition

$$\boxed{\text{Funktional vollständig} = \text{Alle Booleschen Funktionen darstellbar}}$$

### Wichtige vollständige Operatorensätze

| Operatorensatz | ODER darstellen als |
|----------------|---------------------|
| **{NOT, AND, OR}** | — |
| **{NOT, AND}** | $a + b = \overline{\overline{a} \cdot \overline{b}}$ |
| **{NOT, OR}** | $a \cdot b = \overline{\overline{a} + \overline{b}}$ |
| **{NAND}** | Alle Gatter aus NAND konstruierbar |
| **{NOR}** | Alle Gatter aus NOR konstruierbar |

**Beweis für {NOT, AND}:**

| $a$ | $b$ | $\overline{a} \cdot \overline{b}$ | $\overline{\overline{a} \cdot \overline{b}}$ | $a+b$ |
|-----|-----|-----------------------------------|----------------------------------------------|-------|
| 0   | 0   | 1                                 | 0                                            | 0     |
| 0   | 1   | 0                                 | 1                                            | 1     |
| 1   | 0   | 0                                 | 1                                            | 1     |
| 1   | 1   | 0                                 | 1                                            | 1     |

### Programmable Logic Array (PLA)

**Implementierung:**
- Maximal 3 Stufen: NOT → AND → OR
- NOT, AND und OR bilden funktional vollständigen Operatorensatz
- Jede Boolesche Funktion als DNF darstellbar

---

## 7. Logikminimierung

### Ziel

**Reduzierung der Gatter bei gleicher Funktionalität**

**Früher:** Kostenfaktor (weniger Gatter = billiger)

**Heute:** Verbindungsleitungen und Energieverbrauch wichtiger

### Beispiel: Carry-Out minimieren

**Original (DNF):**

$$C_{out} = \overline{A}BC_{in} + A\overline{B}C_{in} + AB\overline{C_{in}} + ABC_{in}$$

**Minimiert:**

$$\boxed{C_{out} = BC_{in} + AC_{in} + AB}$$

**Einsparung:** Von 4 Produkttermen auf 3 Produktterme

⚠️ **Karnaugh-Veitch-Diagramm:** Nicht klausurrelevant, aber nützliches Werkzeug zur Minimierung

---

## 8. Multiplexer (MUX)

### Definition

$$\boxed{\text{MUX: Wählt je nach Steuersignal } S \text{ einen der Inputs aus}}$$

**2-zu-1 Multiplexer:**

$$Y = \overline{S} \cdot A + S \cdot B$$

**Pseudocode:**

| ![[Screenshot 2026-01-22 at 11.09.37.png\|200]] | ``Y = (S) ? B:A`` |
| ----------------------------------------------- | ----------------- |


### Wahrheitstabelle

| $S$ | $A$ | $B$ | $Y$ |
|-----|-----|-----|-----|
| 0   | 0   | 0   | 0   |
| 0   | 0   | 1   | 0   |
| 0   | 1   | 0   | 1   |
| 0   | 1   | 1   | 1   |
| 1   | 0   | 0   | 0   |
| 1   | 0   | 1   | 1   |
| 1   | 1   | 0   | 0   |
| 1   | 1   | 1   | 1   |

### Wahrheitstabelle mit Don't-Cares

**Don't-Care (X oder -):** Wert hat keinen Einfluss auf die Funktion

| $S$ | $A$ | $B$ | $Y$ |
|-----|-----|-----|-----|
| 0   | 0   | X   | 0   |
| 0   | 1   | X   | 1   |
| 1   | X   | 0   | 0   |
| 1   | X   | 1   | 1   |

### Funktionsweise

**Wenn $S = 0$:**

$$Y = 1 \cdot A + 0 \cdot B = A$$

**Wenn $S = 1$:**

$$Y = 0 \cdot A + 1 \cdot B = B$$

### 4-Input MUX

**Steuerung:** 2 Bit ($S_1, S_0$)

| $S_1$ | $S_0$ | Ausgewählter Input |
|-------|-------|--------------------|
| 0     | 0     | A                  |
| 0     | 1     | B                  |
| 1     | 0     | C                  |
| 1     | 1     | D                  |

### n-Bit breiter MUX

**32-Bit 2-zu-1 MUX:**
- Eigentlich 32 parallele 1-Bit MUX
- Alle haben dasselbe Steuersignal $S$
- Wählen gleichzeitig zwischen $A_{31:0}$ und $B_{31:0}$

---

## 9. Decoder

### 1-aus-n-Decoder

**Definition:** Schaltung mit $m$ Eingängen und $n = 2^m$ Ausgängen

$$\boxed{\text{Ausgang } y_i = 1 \iff \text{ Eingänge } = i \text{ (binär)}}$$

Alle anderen Ausgänge = 0

### Beispiel: 1-aus-4-Decoder

**Wahrheitstabelle:**

| $a_1$ | $a_0$ | $y_3$ | $y_2$ | $y_1$ | $y_0$ |
|-------|-------|-------|-------|-------|-------|
| 0     | 0     | 0     | 0     | 0     | 1     |
| 0     | 1     | 0     | 0     | 1     | 0     |
| 1     | 0     | 0     | 1     | 0     | 0     |
| 1     | 1     | 1     | 0     | 0     | 0     |

**Implementierung:**

$$y_0 = \overline{a_1} \cdot \overline{a_0}$$

$$y_1 = \overline{a_1} \cdot a_0$$

$$y_2 = a_1 \cdot \overline{a_0}$$

$$y_3 = a_1 \cdot a_0$$

**Verwendete Gatter:** AND-Gatter mit invertierten Eingängen

---

## 10. Arithmetisch-Logische Einheit (ALU)

### 1-Bit ALU

**Unterstützte Operationen:**
- AND: $a \cdot b$
- OR: $a + b$
- ADD: $a + b + C_{in}$ (mit Volladdierer)

**Aufbau:**
1. Alle Operationen parallel ausführen
2. MUX wählt richtiges Ergebnis

**Steuersignale:**
- `Operation[1:0]`: Wählt Funktion
- `Ainvert`: Invertiert Eingang $a$
- `Binvert`: Invertiert Eingang $b$
- `CarryIn`: Carry für Addierer

### ALU-Steuersignale

| Operation | Ainvert | Binvert | Operation[1:0] | Beschreibung |
|-----------|---------|---------|----------------|--------------|
| AND       | 0       | 0       | 00             | $a \cdot b$ |
| OR        | 0       | 0       | 01             | $a + b$ |
| ADD       | 0       | 0       | 10             | $a + b$ |
| SUB ($a-b$) | 0     | 1       | 10             | $a + \overline{b} + 1$ |
| SUB ($-a+b$) | 1    | 0       | 10             | $\overline{a} + b + 1$ |
| NAND      | 1       | 1       | 01             | $\overline{a} + \overline{b}$ |
| NOR       | 1       | 1       | 00             | $\overline{a} \cdot \overline{b}$ |

### Subtraktion mit 2-Komplement

$$\boxed{a - b = a + (\overline{b} + 1) = a + \overline{b} + C_{in}}$$

**Implementierung:**
- `Binvert = 1`: Invertiert $b$
- `CarryIn = 1`: Addiert 1 (für 2-Komplement)
- `Operation = 10`: Wählt Addierer-Ausgang

### NAND und NOR in der ALU

**Verwendung De Morganscher Gesetze:**

$$\text{NAND: } \overline{a \cdot b} = \overline{a} + \overline{b}$$

$$\text{NOR: } \overline{a + b} = \overline{a} \cdot \overline{b}$$

**Implementierung:**
- NAND: `Ainvert=1`, `Binvert=1`, `Operation=01` (OR)
- NOR: `Ainvert=1`, `Binvert=1`, `Operation=00` (AND)

---

## 11. Addierer

### Ripple-Carry-Addierer

**32-Bit Addierer:** Kette von 32 Volladdierern (FA)

```
FA₀ → FA₁ → FA₂ → ... → FA₃₁
c₀   c₁   c₂   c₃       c₃₁  c₃₂
```

**Problem:** Lange Durchlaufzeit für Übertrag (Carry Ripple)

**Beispiel:** Bei $1111...1111 + 0000...0001$:
- Carry muss durch alle 32 Stufen propagieren
- Sehr langsam bei großer Bitbreite!

### Carry-Look-Ahead (CLA) Addierer

**Idee:** Parallelisierung der Übertragsbildung

**Definitionen:**

$$\boxed{g_i = a_i \cdot b_i \quad \text{(Generate)}}$$

$$\boxed{p_i = a_i \oplus b_i \quad \text{(Propagate)}}$$

**Bedeutung:**
- $g_i = 1$: FA$_i$ **generiert** einen Übertrag (unabhängig von $c_{i-1}$)
- $p_i = 1$: FA$_i$ **propagiert** den Übertrag $c_{i-1}$

### CLA-Gleichungen

**Carry-Gleichungen:**

$$c_1 = g_0 + p_0 c_0$$

$$c_2 = g_1 + p_1 g_0 + p_1 p_0 c_0$$

$$c_3 = g_2 + p_2 g_1 + p_2 p_1 g_0 + p_2 p_1 p_0 c_0$$

$$c_4 = g_3 + p_3 g_2 + p_3 p_2 g_1 + p_3 p_2 p_1 g_0 + p_3 p_2 p_1 p_0 c_0$$

**Summen:**

$$s_i = a_i \oplus b_i \oplus c_i = p_i \oplus c_i$$

**Vorteil:** Alle Carries können **parallel** berechnet werden!

### 4-Bit CLA-Addierer

**Bausteine:**
1. Generate/Propagate-Logik: Berechnet $g_i, p_i$
2. Carry-Logik: Berechnet $c_1, c_2, c_3, c_4$ parallel
3. Summen-Logik: Berechnet $s_i = p_i \oplus c_i$

**Gruppensignale (für hierarchischen Aufbau):**

$$\boxed{GG = g_3 + p_3 g_2 + p_3 p_2 g_1 + p_3 p_2 p_1 g_0}$$

$$\boxed{PG = p_3 p_2 p_1 p_0}$$

- **GG (Group Generate):** 4-Bit-Block generiert Carry
- **PG (Group Propagate):** 4-Bit-Block propagiert Carry

### 16-Bit CLA-Addierer (hierarchisch)

**Aufbau:**
- 4 × 4-Bit CLA-Addierer
- 1 × 16-Bit Lookahead Carry Unit

**Carry-Gleichungen der obersten Ebene:**

$$C_4 = G_0 + P_0 c_0$$

$$C_8 = G_1 + P_1 G_0 + P_1 P_0 c_0$$

$$C_{12} = G_2 + P_2 G_1 + P_2 P_1 G_0 + P_2 P_1 P_0 c_0$$

**Vorteil:** Deutlich schneller als Ripple-Carry bei großen Bitbreiten!

---

## 12. Schaltwerke (Sequential Logic)

### Schaltnetz vs. Schaltwerk

**Schaltnetz (Combinational Logic):**

$$\boxed{\text{Ausgänge} = f(\text{aktuelle Eingänge})}$$

- Keine internen Zustände
- Keine Speicher
- Beispiele: ALU, MUX, Decoder

**Schaltwerk (Sequential Logic):**

$$\boxed{\text{Ausgänge} = f(\text{Eingänge}, \text{interner Zustand})}$$

- Verfügt über internen Speicher
- Kann Zustände speichern
- Beispiele: Register, Speicher, Flip-Flops

### Synchrone vs. Asynchrone Schaltwerke

**Asynchron:**
- Zustandsänderung bei Input-Änderung
- Schwer zu kontrollieren

**Synchron:**
- Zustandsänderung durch Taktsignal (Clock) gesteuert
- **Taktsignal gibt an, WANN Zustand sich ändert**
- In modernen Prozessoren Standard

---

## 13. SR-Latch (Ungetakteter Speicher)

### Aufbau

**Kreuzgekoppelte NOR-Gatter**

- **S (Set):** Setzt Ausgang $Q = 1$
- **R (Reset):** Setzt Ausgang $Q = 0$
- **Q:** Ausgang
- **$\overline{Q}$:** Invertierter Ausgang

### Funktionsweise

**Set ($S=1, R=0$):**

$$Q = 1, \quad \overline{Q} = 0$$

**Reset ($R=1, S=0$):**

$$Q = 0, \quad \overline{Q} = 1$$

**Halten ($S=0, R=0$):**

$$Q = Q_{\text{vorher}}, \quad \overline{Q} = \overline{Q}_{\text{vorher}}$$

**Verboten ($S=1, R=1$):**

$$Q = 0, \quad \overline{Q} = 0 \quad \text{(Widerspruch!)}$$

Beim Übergang zu $S=R=0$ oszilliert der Ausgang oder wird zufällig!

### Wahrheitstabelle

| $S$ | $R$ | $Q$ | Zustand |
|-----|-----|-----|---------|
| 0   | 0   | $Q$ | Halten  |
| 0   | 1   | 0   | Reset   |
| 1   | 0   | 1   | Set     |
| 1   | 1   | ?   | **Verboten** |

---

## 14. D-Latch (Getakteter Speicher)

### Aufbau

**Komponenten:**
- D (Data): Eingang
- C (Clock): Takt
- Q: Ausgang
- Intern: SR-Latch mit NAND-Gattern

### Funktionsweise

$$\boxed{C = 1: Q \text{ übernimmt } D}$$

$$\boxed{C = 0: Q \text{ hält vorherigen Wert}}$$

**Wahrheitstabelle:**

| $C$ | $D$ | $Q(t)$ | $S$ | $R$ |
|-----|-----|--------|-----|-----|
| 0   | 0   | $Q(t-1)$ | 0 | 0 |
| 0   | 1   | $Q(t-1)$ | 0 | 0 |
| 1   | 0   | 0      | 0   | 1   |
| 1   | 1   | 1      | 1   | 0   |

⚠️ **Achtung: Transparent bei $C=1$!**
- Solange Clock = 1, folgt Ausgang dem Eingang
- Nicht ideal für synchrone Systeme

---

## 15. D-Flip-Flop (DFF)

### Aufbau

**Master-Slave-Prinzip:** 2 D-Latches mit invertiertem Clock

```
D → [D-Latch 1] → [D-Latch 2] → Q
        ↑C              ↑C̄
```

### Funktionsweise

$$\boxed{\text{Ausgang wechselt NUR bei Taktflanke}}$$

**Flankengesteuert (Edge-Triggered):**
- Bei **steigender Flanke:** DFF übernimmt D (positive edge-triggered)
- Bei **fallender Flanke:** DFF übernimmt D (negative edge-triggered)

**Vorteile gegenüber D-Latch:**
- Nicht transparent
- Zustandsänderung nur zu definierten Zeitpunkten
- Besser für synchrone Systeme

### Taktverfahren (Clocking Methodology)

**Definiert:**
- Wann Signale geschrieben werden
- Was gelesen wird, wenn Signal zur gleichen Zeit gelesen und geschrieben wird

**Taktsignal:**
- **Steigende Flanke:** $0 \to 1$ Übergang
- **Fallende Flanke:** $1 \to 0$ Übergang
- **Periode $T$:** Zeit für einen vollständigen Zyklus

---

## 16. Registersatz (Register File)

### Definition

**Register:** Speicherbereiche innerhalb eines Prozessors
- Direkt mit Recheneinheit verbunden
- Speichern unmittelbare Operanden und Ergebnisse
- Wortbreite = Prozessorbreite (8, 16, 32 oder 64 Bit)

### Beispiel: MIPS Registersatz

**Spezifikation:**
- 32 Register
- Jedes Register: 32 Bit breit
- **Gesamtgröße:** $32 \times 32 = 1024$ D-Flip-Flops

**Schnittstelle:**
- **Read Register Number 1** (5 Bit): Welches Register lesen (Port 1)?
- **Read Register Number 2** (5 Bit): Welches Register lesen (Port 2)?
- **Write Register** (5 Bit): In welches Register schreiben?
- **Write Data** (32 Bit): Daten zum Schreiben
- **RegWrite** (1 Bit): Schreiben aktivieren?
- **Read Data 1** (32 Bit): Gelesene Daten (Port 1)
- **Read Data 2** (32 Bit): Gelesene Daten (Port 2)

### Implementierung der Leseports

**2 Leseports mit Multiplexern:**

```
Register 0  ──┐
Register 1  ──┤
    ...     ──┼─→ MUX → Read Data 1
Register 30 ──┤    ↑
Register 31 ──┘    │
              Read Register Number 1

Register 0  ──┐
Register 1  ──┤
    ...     ──┼─→ MUX → Read Data 2
Register 30 ──┤    ↑
Register 31 ──┘    │
              Read Register Number 2
```

**Funktionsweise:**
- Multiplexer wählt basierend auf Register-Nummer
- Beide Ports können **gleichzeitig** lesen
- Zwei **verschiedene** Register gleichzeitig lesbar

### Implementierung des Schreibports

**Decoder + D-Flip-Flops:**

```
Write Register ──→ [Decoder] ──→ Enable-Signale
                                      ↓
Write Data ───────────────────→ [DFF 0]
                            └──→ [DFF 1]
                            └──→  ...
                            └──→ [DFF 31]
                                      ↑
RegWrite ─────────────────────────── AND
```

**Funktionsweise:**

1. **Decoder:** Wandelt Register-Nummer in One-Hot-Code
   - Nur ein Ausgang = 1
   - Beispiel: Register 3 → Ausgang 3 = 1, alle anderen = 0

2. **Enable-Logik:** Decoder-Ausgang AND RegWrite
   - Nur wenn RegWrite = 1, wird geschrieben

3. **D-Flip-Flops:** Speichern Daten bei Clock-Flanke
   - Nur aktiviertes Register übernimmt neue Daten

**Beispiel Schreibaktion:**

```
Write Register = 3
Write Data = 0x11223344
RegWrite = 1

Decoder-Ausgänge:
  Reg 0: 0
  Reg 1: 0
  Reg 2: 0
  Reg 3: 1  ← aktiviert!
  ...
  Reg 31: 0

→ Nur Register 3 übernimmt 0x11223344
```

**Clock-Signal:**
- Wird nicht explizit angezeigt
- Steuert alle D-Flip-Flops
- Bestimmt **wann** geschrieben wird (bei Taktflanke)

---

## 📌 Zusammenfassung

### Logikgatter und Boolesche Algebra

**Funktional vollständige Operatorensätze:**

$\boxed{\{NOT, AND, OR\}, \{NOT, AND\}, \{NOT, OR\}, \{NAND\}, \{NOR\}}$

**De Morgansche Gesetze:**

$\overline{a + b} = \overline{a} \cdot \overline{b}, \quad \overline{a \cdot b} = \overline{a} + \overline{b}$

### Normalformen

**Disjunktive Normalform (DNF):**
- Sum of Products
- Für Zeilen mit Ausgang = 1

**Konjunktive Normalform (KNF):**
- Product of Sums
- Für Zeilen mit Ausgang = 0

### Kombinatorische Bausteine

**Multiplexer:**

$Y = \overline{S} \cdot A + S \cdot B$

**Decoder:**
- $m$ Eingänge → $2^m$ Ausgänge
- Genau ein Ausgang = 1

### ALU (Arithmetic Logic Unit)

**Operationen:** AND, OR, ADD, SUB, NAND, NOR

**Subtraktion via 2-Komplement:**

$a - b = a + \overline{b} + 1$

**Steuersignale:** Ainvert, Binvert, Operation[1:0]

### Addierer

**Ripple-Carry:** Langsam, einfach, Carry propagiert sequenziell

**Carry-Look-Ahead (CLA):**
- Schnell, komplex
- Parallele Carry-Berechnung
- Generate: $g_i = a_i \cdot b_i$
- Propagate: $p_i = a_i \oplus b_i$

### Speicherelemente

| Element | Getaktet? | Transparent? | Änderung |
|---------|-----------|--------------|----------|
| **SR-Latch** | Nein | — | Bei S/R-Änderung |
| **D-Latch** | Ja | Ja (bei C=1) | Während C=1 |
| **D-Flip-Flop** | Ja | Nein | Nur bei Taktflanke |

### Schaltnetz vs. Schaltwerk

**Schaltnetz:**
- Ausgänge = $f$(aktuelle Eingänge)
- Keine Speicher
- Beispiele: ALU, MUX, Decoder

**Schaltwerk:**
- Ausgänge = $f$(Eingänge, interner Zustand)
- Mit Speicher
- Beispiele: Register, Flip-Flops

### Registersatz

**MIPS Beispiel:**
- 32 Register × 32 Bit = 1024 D-Flip-Flops
- 2 Leseports (gleichzeitig)
- 1 Schreibport (Decoder + DFFs)
- Taktgesteuert

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.01 Grundlegenden Ideen]]: Abstraktion, Prozessor
- [[VL.02 Zahlensysteme]]: 2-Komplement für Subtraktion
- [[VL.04 Befehle]]: Register in MIPS
- [[VL.05 Single Cycle]]: ALU und Register im Prozessor