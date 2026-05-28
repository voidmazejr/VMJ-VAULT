**Class:** [[AnaLina]]  
**Date:** 27-12-2025  
**Topics:** #Mengen #Logik #Mengenlehre #Aussagenlogik

---
## 🎯 Lernziele der Vorlesung

- Definition und Notation von Mengen
- Grundlegende Mengenoperationen
- Aussagenlogik und Wahrheitswerte
- Beweistechniken

---

## 1. Mengen

### Definition nach Georg Cantor

**Definition (Menge):**  
Eine Menge ist die Zusammenfassung von wohlunterschiedenen Objekten unserer Anschauung oder unseres Denkens zu einem Ganzen.

**Notation:**

- $m \in M$: m ist Element von M
- $m \notin M$: m ist kein Element von M

**Wichtig:** Bei Mengen kommt es nicht auf die Reihenfolge an, jedes Element wird nur einmal gezählt.

**Beispiel:** ${1, 2, 3, 4} = {2, 3, 1, 4} = {1, 3, 1, 2, 3, 4}$

### Darstellung von Mengen

1. **Aufzählung:** $A = {1, 2, 3, 4}$
2. **Eigenschaft:** $B = {x \in \mathbb{N} \mid x^2 = 4}$

### Mengenoperationen

|**Operation**|**Notation**|**Definition**|**Bedeutung**|
|---|---|---|---|
|**Teilmenge**|$A \subseteq B$|$x \in A \Rightarrow x \in B$|Alle Elemente von A sind auch in B|
|**Gleichheit**|$A = B$|$x \in A \Leftrightarrow x \in B$|A und B haben dieselben Elemente|
|**Vereinigung**|$A \cup B$|${x \mid x \in A \text{ oder } x \in B}$|Alle Elemente von A oder B|
|**Schnitt**|$A \cap B$|${x \mid x \in A \text{ und } x \in B}$|Elemente, die in beiden Mengen sind|
|**Differenz**|$A \setminus B$|${x \mid x \in A \text{ und } x \notin B}$|Elemente von A, die nicht in B sind|
|**Kartesisches Produkt**|$A \times B$|${(a, b) \mid a \in A, b \in B}$|Menge aller geordneten Paare|

**Beispiele:**

- ${1, 2} \cup {1, 3} = {1, 2, 3}$
- ${1, 2} \cap {1, 3} = {1}$
- ${1, 2} \setminus {1, 3} = {2}$
- ${1, 2} \times {1, 3} = {(1,1), (1,3), (2,1), (2,3)}$

### Intervalle

Für $a, b \in \mathbb{R}$ mit $a < b$:

|**Intervall**|**Notation**|**Bedeutung**|
|---|---|---|
|Offenes Intervall|$]a, b[$|${x \in \mathbb{R} \mid a < x < b}$|
|Halboffenes Intervall|$[a, b[$|${x \in \mathbb{R} \mid a \leq x < b}$|
|Halboffenes Intervall|$]a, b]$|${x \in \mathbb{R} \mid a < x \leq b}$|
|Abgeschlossenes Intervall|$[a, b]$|${x \in \mathbb{R} \mid a \leq x \leq b}$|

**Kompaktes Intervall:** Ein abgeschlossenes und beschränktes Intervall

**Unbeschränkte Intervalle:**

- $]a, +\infty[ = {x \in \mathbb{R} \mid a < x}$
- $[a, +\infty[ = {x \in \mathbb{R} \mid a \geq x}$
- $]-\infty, b[ = {x \in \mathbb{R} \mid x < b}$
- $]-\infty, b] = {x \in \mathbb{R} \mid x \leq b}$
- $]-\infty, +\infty[ = \mathbb{R}$

⚠️ **Wichtig:** Die Symbole $\infty$ und $-\infty$ sind keine reellen Zahlen!

---

## 2. Grundlagen der Logik

### Aussagen

**Definition:** Eine Aussage ist ein Satz, dem genau einer der beiden Wahrheitswerte "wahr" (w) oder "falsch" (f) zugeordnet werden kann.

**Beispiele:**

- ✓ "Berlin ist eine Stadt." (wahre Aussage)
- ✓ "3 + 7 = 11" (falsche Aussage)
- ✗ "Berlin!" (keine Aussage)

### Quantifizierung

"$x^2 - 1 = 0$" ist keine Aussage, aber:

- "Es gibt $x \in \mathbb{R}$ mit $x^2 - 1 = 0$" (wahre Aussage)
- "Für alle $x \in \mathbb{R}$ gilt $x^2 - 1 = 0$" (falsche Aussage)

### Logische Operationen

**Negation ($\neg A$):**

|A|$\neg A$|
|---|---|
|w|f|
|f|w|

**Bei Negation gilt:** "für alle" $\leftrightarrow$ "es gibt"

**UND-Verknüpfung ($A \land B$):**

|A|B|$A \land B$|
|---|---|---|
|w|w|w|
|w|f|f|
|f|w|f|
|f|f|f|

**ODER-Verknüpfung ($A \lor B$):**

|A|B|$A \lor B$|
|---|---|---|
|w|w|w|
|w|f|w|
|f|w|w|
|f|f|f|

**Implikation ($A \Rightarrow B$):**  
"Aus A folgt B" oder "Wenn A, dann B"

|A|B|$A \Rightarrow B$|
|---|---|---|
|w|w|w|
|w|f|f|
|f|w|w|
|f|f|w|

⚠️ **Wichtig:** Eine falsche Aussage impliziert alles!

**Äquivalenz ($A \Leftrightarrow B$):**  
A und B haben denselben Wahrheitswert

|A|B|$A \Leftrightarrow B$|
|---|---|---|
|w|w|w|
|w|f|f|
|f|w|f|
|f|f|w|

$A \Leftrightarrow B$ ist wahr $\Leftrightarrow$ $(A \Rightarrow B) \land (B \Rightarrow A)$ ist wahr

---

## 3. Beweistechniken

### 1. Direkter Beweis (Logisches Folgern)

Wenn A wahr ist und $A \Rightarrow B$ wahr ist, dann ist auch B wahr.

### 2. Kontraposition

$A \Rightarrow B$ ist genau dann wahr, wenn $\neg B \Rightarrow \neg A$ wahr ist.

**Beispiel:** Zeige: Für alle $n \in \mathbb{N}$ gilt: $n^2$ ist gerade $\Rightarrow$ n ist gerade

_Beweis durch Kontraposition:_ Zeige stattdessen: n ist ungerade $\Rightarrow$ $n^2$ ist ungerade

- n ungerade $\Rightarrow$ $n = 2k + 1$ für ein $k \in \mathbb{N}$
- $n^2 = (2k + 1)^2 = 4k^2 + 4k + 1 = 2(2k^2 + 2k) + 1$
- $\Rightarrow$ $n^2$ ist ungerade ✓

### 3. Beweis durch Widerspruch

Man nimmt an, dass die zu zeigende Aussage falsch ist, und führt dies zu einem Widerspruch.

**Klassisches Beispiel:** $\sqrt{2}$ ist irrational

_Beweis:_ Annahme: $\sqrt{2}$ ist rational, also $\sqrt{2} = \frac{m}{n}$ als gekürzter Bruch

- $\Rightarrow$ $m^2 = 2n^2$ $\Rightarrow$ $m^2$ gerade $\Rightarrow$ m gerade $\Rightarrow$ $m = 2k$
- $\Rightarrow$ $4k^2 = 2n^2$ $\Rightarrow$ $n^2 = 2k^2$ $\Rightarrow$ $n^2$ gerade $\Rightarrow$ n gerade
- Widerspruch: m und n beide gerade, aber Bruch war gekürzt! ⚡

---

## 📌 Wichtige Hinweise für Gleichungen

**Äquivalenzumformungen:** Beim Lösen von Gleichungen muss man aufpassen!

- $2x = 4$ $\Leftrightarrow$ $x = 2$ (Multiplikation mit $\frac{1}{2}$) ✓
- $2x = 4$ $\Rightarrow$ $0 \cdot x = 0$ (Multiplikation mit 0) ⚠️ **keine Äquivalenz!**

Die Lösungsmenge verändert sich: links nur $x = 2$, rechts alle $x \in \mathbb{R}$.

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.05 Abbildungen]] Mengen als Grundlage für Definitionsbereiche von Funktionen
- [[VL.17 Konvergenz]]
- [[VL.18 Berechnung von Grenzwerten]]
- [[VL.19 Stetigkeit]]
- [[VL.20 Sätze über stetige Funktionen]] Intervalle wichtig für Grenzwerte und Stetigkeit