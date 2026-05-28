**Class:** [[FoG - Formal-mathematische Grundlagen]]
**Date:** 25-05-2026
**Topics:** #Relationen #KartesischesProdukt #Komposition #Umkehrrelation #Totalität #Eindeutigkeit
**Link:** [[VL.06 FoG Skript-36-38 1.pdf]]

---

## 🎯 Lernziele der Vorlesung

Relationen sind ein grundlegendes Strukturierungswerkzeug der Informatik – sie formalisieren Beziehungen zwischen Mengen und bilden die Basis für Datenbanken, Prozessmodellierung und Funktionen.

- **Kartesisches Produkt**: Definition von $n$-Tupeln aus mehreren Mengen.
- **Relation**: Teilmenge eines kartesischen Produkts mit Graph und Typ.
- **Spezialrelationen**: Leere Relation, Allrelation, 0-stellige Relationen.
- **Totalität & Eindeutigkeit**: links-/rechtstotal, links-/rechtseindeutig.
- **Umkehrrelation**: Vertauschen von Quelle und Ziel einer Relation.
- **Komposition**: Hintereinanderschalten zweier Relationen.
- **Eigenschaften**: Assoziativität, Vererbung von Eigenschaften, Zusammenspiel mit Umkehrung.

---

## 1. Kartesisches Produkt

### Definition (7.1.1)

Das kartesische Produkt fasst alle möglichen geordneten $n$-Tupel zusammen, die aus je einem Element jeder Menge bestehen.

$$\boxed{\prod_{i=1}^{n} A_i \triangleq \{(a_1,\ldots,a_n) \mid \forall i \in [1,n].\ a_i \in A_i\}}$$

**Terminologie:**
- Elemente von $\prod_{i=1}^{n} A_i$ heißen $n$-Tupel.
- 2-Tupel heißen Paare.
- Das 0-Tupel $()$ heißt leeres Tupel.

Für eine beliebige Menge $A$ und $n \in \mathbb{N}$ gilt:

$$A^n \triangleq \prod_{i=1}^{n} A$$

> 💡 **Merkhilfe:** Denke an eine Tabelle – das kartesische Produkt liefert alle möglichen Zeilen, wobei Spalte $i$ aus Menge $A_i$ stammt.

### Spezialfälle (7.1.2)

$$A^0 = \{()\}$$

$$\prod_{i=1}^{n} A_i = \emptyset, \quad \text{falls } A_k = \emptyset \text{ für mindestens ein } k \in [1,n]$$

**Beispiel:**
$$\mathbb{N} \times \emptyset = \{(n,x) \mid n \in \mathbb{N} \land x \in \emptyset\} = \emptyset$$

> 💡 **Merkhilfe:** Ein leerer Faktor macht das gesamte Produkt leer – wie bei der Multiplikation mit 0.

### Anzahl der Relationen (Denkaufgabe)

Gegeben drei endliche Mengen $A, B, C$: Wie viele Relationen des Typs $(A, B, C)$ gibt es?

$$\#\left(\prod_{i=1}^{3} A_i\right) = \#(A) \cdot \#(B) \cdot \#(C)$$

$$\text{Anzahl der Relationen} = 2^{\#(A)\cdot\#(B)\cdot\#(C)}$$

Da jede Relation eine Teilmenge des kartesischen Produkts ist und $\#(\mathcal{P}(M)) = 2^{\#(M)}$ gilt.

### ⚠️ Schreibweise $A_1 \times \cdots \times A_n$

Die Schreibweise mit dem binären Operator $\times$ ist zu vermeiden, da sie eine implizite Klammerung erzeugt:

$$A_1 \times (A_2 \times A_3) \Rightarrow \text{Elemente der Form } (a_1, (a_2, a_3))$$

im Gegensatz zum intendierten $(a_1, a_2, a_3)$.

---

## 2. Relationen – Grundbegriffe

### Definition Relation (7.1.3)

Seien $A_1, \ldots, A_n$ beliebige Mengen, sei $R \subseteq \prod_{i=1}^{n} A_i$. Dann heißt

$$\boxed{\underbrace{R}_{\text{Graph}} : \underbrace{(A_1,\ldots,A_n)}_{\text{Typ}}}$$

$n$-stellige Relation.

- **Graph** = die Menge der Tupel.
- **Typ** = die Signatur der Mengen, aus denen die Tupel stammen.
- Der Spezialfall $n=2$ heißt binäre Relation; Infixschreibweise: $a\,R\,b$ für $(a,b) \in R$.

**Gleichheit zweier Relationen** $R_A : (A_1,\ldots,A_n)$ und $R_B : (B_1,\ldots,B_m)$:
1. $n = m$.
2. $A_i = B_i$ für alle $1 \le i \le n$.
3. $R_A = R_B$ als Mengen.

⚠️ **Achtung:** Zwei leere Relationen $\emptyset : (A_1, A_2)$ und $\emptyset : (B_1, B_2)$ sind verschieden, wenn $A_1 \neq B_1$ oder $A_2 \neq B_2$ – der Typ gehört zur Relation.

### Definition Spezialfälle (7.1.4)

| Relation | Notation | Graph | Bedeutung |
|---|---|---|---|
| Leere Relation | $\emptyset_{A,B} : (A,B)$ | $\emptyset_{A,B} \triangleq \emptyset$ | Keine Paare |
| Allrelation | $\nabla_{A,B} : (A,B)$ | $\nabla_{A,B} \triangleq A \times B$ | Alle Paare |
| 0-stellig (falsch) | $\emptyset : ()$ | $\emptyset$ | Immer falsch |
| 0-stellig (wahr) | $\{()\} : ()$ | $\{()\}$ | Immer wahr |

> 💡 **Merkhilfe:** 0-stellige Relationen sind wie boolesche Werte – entweder leer (falsch) oder das leere Tupel enthaltend (wahr).

### Relationen als Mengen

Da Relationen Mengen sind, gelten alle Mengenoperationen:

```text
R   := { (a₁,b₁), (a₂,b₂), (a₃,b₂) } ⊆ A × B   ✅
R'  := R ∪ {(a₂,b₁)}                  ⊆ A × B   ✅
R'' := R' \ {(a₁,b₁)}                 ⊆ A × B   ✅
R''' := R'' ∪ {1}                    ⊄ A × B   ❌ keine Relation mit Typ (A,B)!
```

---

## 3. Totalität und Eindeutigkeit

### Definition (7.1.6)

Sei $R : (A,B)$ eine binäre Relation. $R$ heißt:

$$\boxed{
\begin{array}{ll}
\text{linkstotal:} & \forall a \in A.\ \exists b \in B.\ aRb \\[4pt]
\text{rechtstotal:} & \forall b \in B.\ \exists a \in A.\ aRb \\[4pt]
\text{linkseindeutig:} & \forall a_1,a_2 \in A.\ \forall b \in B.\ (a_1Rb \land a_2Rb \to a_1 = a_2) \\[4pt]
\text{rechtseindeutig:} & \forall a \in A.\ \forall b_1,b_2 \in B.\ (aRb_1 \land aRb_2 \to b_1 = b_2)
\end{array}
}$$

### Äquivalente Kontrapositiv-Formen

Durch Kontraposition und De Morgan erhält man:

$$\forall a_1,a_2 \in A.\ \forall b \in B.\ \bigl(a_1 \neq a_2 \to \neg(a_1Rb) \lor \neg(a_2Rb)\bigr)$$

$$\forall a \in A.\ \forall b_1,b_2 \in B.\ \bigl(b_1 \neq b_2 \to \neg(aRb_1) \lor \neg(aRb_2)\bigr)$$

> 💡 **Merkhilfe:** Rechtseindeutig = funktional, linkseindeutig = injektiv in Gegenrichtung.

### Übersicht der Eigenschaften

| Eigenschaft | Quantifizierung | Anschauung |
|---|---|---|
| linkstotal | Jedes $a$ hat mindestens ein Bild | „Alle Quellen belegt" |
| rechtstotal | Jedes $b$ hat mindestens ein Urbild | „Alle Ziele erreicht" |
| linkseindeutig | Jedes $b$ hat höchstens ein Urbild | „Kein geteiltes Ziel" |
| rechtseindeutig | Jedes $a$ hat höchstens ein Bild | „Kein geteilter Ursprung" |

---

## 4. Algebra binärer Relationen

### Umkehrrelation (7.2.1)

Seien $A, B$ beliebige Mengen, $R : (A,B)$. Die Umkehrrelation $R^{-1} : (B,A)$ ist definiert durch:

$$\boxed{R^{-1} \triangleq \{(b,a) \mid (a,b) \in R\}}$$

Elementregel: $(b,a) \in R^{-1} \iff (a,b) \in R$.

```text
R:                          R⁻¹:
A ──────→ B                 B ──────→ A
a₁ ──→  b₁                 b₁ ──→  a₁
a₂ ──→  b₁                 b₁ ──→  a₂
a₃ ──→  b₂                 b₂ ──→  a₃
```

### Eigenschaften der Umkehrrelation (7.2.2)

Seien $A, B$ beliebige Mengen, $R : (A,B)$. Dann gilt:

1. $(R^{-1})^{-1} = R$.
2. Ist $R$ linkstotal, so ist $R^{-1}$ rechtstotal.
3. Ist $R$ rechtstotal, so ist $R^{-1}$ linkstotal.
4. Ist $R$ linkseindeutig, so ist $R^{-1}$ rechtseindeutig.
5. Ist $R$ rechtseindeutig, so ist $R^{-1}$ linkseindeutig.

> 💡 **Merkhilfe:** Umkehrung spiegelt alle Eigenschaften links ↔ rechts. Das ist ähnlich wie bei doppelter Negation: $(R^{-1})^{-1} = R$.

### Komposition (7.2.3)

Seien $A, B, C$ beliebige Mengen, $P : (A,B)$ und $Q : (B,C)$.

$$\boxed{P \mathbin{;} Q \triangleq \{(a,c) \in A \times C \mid \exists b \in B.\ aPb \land bQc\}}$$

**Notationen:**
- $PQ$ statt $P \mathbin{;} Q$.
- $Q \circ P \triangleq P \mathbin{;} Q$ (konsistent mit der Komposition von Abbildungen aus §8).

⚠️ **Achtung:** Die Richtung von $\circ$ variiert je nach Anwendungsbereich – immer explizit klären.

**Beispiel 1 (nicht-leere Komposition):**

```text
A ──P──→ B ──Q──→ C
a  ──→  b₁ ──→  x        P;Q = { (a,x), (b,x) }
b  ──→  b₁
```

**Beispiel 2 (leere Komposition):**

```text
A ──P──→ B ──Q──→ C
a  ──→  1              2 ──→ x
b  ──→  1
                      (kein b in B verbindet P und Q)
P;Q = ∅
```

### Assoziativität der Komposition (7.2.5)

$$\boxed{P \mathbin{;} (Q \mathbin{;} R) = (P \mathbin{;} Q) \mathbin{;} R}$$

```text
A ──P──→ B ──Q──→ C ──R──→ D

P;(Q;R)  →  erst Q;R berechnen, dann mit P verketten
(P;Q);R  →  erst P;Q berechnen, dann mit R verketten

Beide liefern dasselbe Ergebnis ✅
```

### Eigenschaften der Komposition (7.2.6)

Seien $P : (A,B)$ und $Q : (B,C)$ beliebige Relationen:

| Eigenschaft von $P$ und $Q$ | Eigenschaft von $PQ$ |
|---|---|
| Beide linkstotal | $PQ$ linkstotal ✅ |
| Beide rechtstotal | $PQ$ rechtstotal ✅ |
| Beide linkseindeutig | $PQ$ linkseindeutig ✅ |
| Beide rechtseindeutig | $PQ$ rechtseindeutig ✅ |

> 💡 **Merkhilfe:** Eigenschaften vererben sich bei Komposition – wenn beide Relationen eine Eigenschaft haben, hat auch ihre Komposition sie.

### Komposition und Umkehrrelation (7.2.7)

$$\boxed{(PQ)^{-1} = Q^{-1}P^{-1}}$$

$$\boxed{(Q \circ P)^{-1} = P^{-1} \circ Q^{-1}}$$

```text
PQ:      A ──P──→ B ──Q──→ C

(PQ)⁻¹: C ──Q⁻¹──→ B ──P⁻¹──→ A  =  Q⁻¹P⁻¹
```

> 💡 **Merkhilfe:** Entspricht $(AB)^T = B^T A^T$ bei Matrizen – die Reihenfolge kehrt sich immer um.

---

## 📌 Zusammenfassung

### Wichtige Konzepte

| Konzept | Bedeutung |
|---|---|
| Kartesisches Produkt $\prod_{i=1}^{n} A_i$ | Menge aller $n$-Tupel $(a_1,\ldots,a_n)$ mit $a_i \in A_i$ |
| Relation $R : (A_1,\ldots,A_n)$ | Teilmenge von $\prod_{i=1}^{n} A_i$ mit Graph und Typ |
| Leere Relation $\emptyset_{A,B}$ | Graph $= \emptyset$, keine Paare |
| Allrelation $\nabla_{A,B}$ | Graph $= A \times B$, alle Paare |
| Linkstotal | Jedes $a \in A$ hat mindestens ein Bild in $B$ |
| Rechtstotal | Jedes $b \in B$ hat mindestens ein Urbild in $A$ |
| Linkseindeutig | Jedes $b \in B$ hat höchstens ein Urbild in $A$ |
| Rechtseindeutig | Jedes $a \in A$ hat höchstens ein Bild in $B$ |
| Umkehrrelation $R^{-1}$ | Tupel werden umgedreht: $(b,a)$ statt $(a,b)$ |
| Komposition $P \mathbin{;} Q$ | Transitiver Pfad durch Zwischenmenge $B$ |

### Kernaussagen

✅ $(R^{-1})^{-1} = R$ – Doppelte Umkehrung ist die Identität  
✅ Komposition ist assoziativ – Klammerung ist irrelevant  
✅ $(PQ)^{-1} = Q^{-1}P^{-1}$ – Umkehrung kehrt die Reihenfolge um  
✅ Eigenschaften vererben sich – Links-/Rechtstotal und Links-/Rechtseindeutig bleiben unter Komposition erhalten  
⚠️ Typ gehört zur Relation – $\emptyset:(A,B) \neq \emptyset:(C,D)$, wenn $A \neq C$ oder $B \neq D$  
⚠️ $A_1 \times \cdots \times A_n$ Notation vermeiden – erzeugt verschachtelte Tupel statt flache $n$-Tupel  
❌ $Q \circ P$ ist nicht universell – Richtungskonvention variiert je nach Kontext  

### Wichtige Formeln

| Name | Formel |
|---|---|
| Kartesisches Produkt | $\prod_{i=1}^{n} A_i = \{(a_1,\ldots,a_n) \mid \forall i \in [1,n].\ a_i \in A_i\}$ |
| Umkehrrelation | $R^{-1} = \{(b,a) \mid (a,b) \in R\}$ |
| Komposition | $P \mathbin{;} Q = \{(a,c) \in A \times C \mid \exists b \in B.\ aPb \land bQc\}$ |
| Komposition + Umkehrung | $(PQ)^{-1} = Q^{-1}P^{-1}$ |

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.05 Mengen & Mengenoperationen]]: Relationen sind spezielle Mengen – alle Mengenoperationen ($\cup$, $\cap$, $\setminus$) anwendbar.
- [[VL.08 Abbildungen & Funktionen]]: Funktionen sind spezielle Relationen (linkstotal + rechtseindeutig); Kompositionsbegriff konsistent mit $Q \circ P$.
- [[VL.09 Äquivalenzrelationen]]: Binäre Relationen mit Reflexivität, Symmetrie, Transitivität.
- [[VL.10 Ordnungsrelationen]]: Partielle und totale Ordnungen als spezielle binäre Relationen.