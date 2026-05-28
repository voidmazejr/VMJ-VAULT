**Class:** [[AnaLina]]  
**Date:** 27-12-2025
**Topics:** #VollständigeInduktion #Binomialkoeffizient #BinomischerLehrsatz #Beweistechnik

---

## 🎯 Lernziele der Vorlesung

- Prinzip der vollständigen Induktion verstehen und anwenden
- Aussagen für alle $n \in \mathbb{N}$ beweisen können
- Binomialkoeffizienten berechnen
- Binomischen Lehrsatz kennen und anwenden
- Häufige Fehler bei Induktionsbeweisen vermeiden

---

## 1. Prinzip der vollständigen Induktion

### Grundidee

Wenn man bei einem Startwert beginnt und "immer eins weiterzählt", erreicht man jede natürliche Zahl. Eine Aussage $A(n)$, die für den Startwert gilt und beim "Weiterzählen" wahr bleibt, gilt dann für alle natürlichen Zahlen ≥ Startwert.

### Schema für Induktionsbeweise

Um eine Aussage $A(n)$ für alle $n \in \mathbb{N}$ mit $n \geq n_0$ zu beweisen:

**1. Induktionsanfang (IA):**

- Zeige, dass $A(n_0)$ gilt (Verankerung)

**2. Induktionsschritt (IS):**

- Zeige: $A(n) \Rightarrow A(n+1)$ für beliebiges $n \geq n_0$

Der Induktionsschritt wird oft unterteilt in:

**a) Induktionsvoraussetzung (IV):**

- Nehme an, dass $A(n)$ für ein $n \geq n_0$ richtig ist

**b) Induktionsbehauptung (IB):**

- "Dann gilt auch $A(n+1)$"

**c) Induktionsbeweis:**

- Beweise die Induktionsbehauptung unter Verwendung der IV

⚠️ **Alternative Namen:** IA = Induktionsverankerung, IV = Induktionsannahme, IS = Induktionsschluss

---

## 2. Beispiele für Induktionsbeweise

### Beispiel 1: Geometrische Summe

**Aussage:** Für $q \neq 1$ und alle $n \in \mathbb{N}$ gilt: $$\sum_{k=0}^{n} q^k = \frac{1-q^{n+1}}{1-q}$$

**Beweis:**

**IA:** Für $n = 0$: $$\sum_{k=0}^{0} q^k = q^0 = 1 = \frac{1-q^1}{1-q} \checkmark$$

**IV:** Die Behauptung gelte für ein $n \geq 0$, d.h.: $$\sum_{k=0}^{n} q^k = \frac{1-q^{n+1}}{1-q}$$

**IS:** Zeige die Aussage für $n+1$: $$\sum_{k=0}^{n+1} q^k = \sum_{k=0}^{n} q^k + q^{n+1} \stackrel{IV}{=} \frac{1-q^{n+1}}{1-q} + q^{n+1}$$ $$= \frac{1-q^{n+1}}{1-q} + \frac{q^{n+1} - q^{n+2}}{1-q} = \frac{1-q^{n+2}}{1-q} \checkmark$$

### Beispiel 2: Summe der ersten n natürlichen Zahlen

**Aussage:** Für alle $n \in \mathbb{N}$, $n \geq 1$ gilt: $$\sum_{k=1}^{n} k = 1 + 2 + ... + n = \frac{n(n+1)}{2}$$

**Beweis:**

**IA:** Für $n = 1$: $$\sum_{k=1}^{1} k = 1 = \frac{1 \cdot 2}{2} \checkmark$$

**IV:** Für ein $n \geq 1$ gelte: $$\sum_{k=1}^{n} k = \frac{n(n+1)}{2}$$

**IS:** Zeige für $n+1$: $$\sum_{k=1}^{n+1} k = \sum_{k=1}^{n} k + (n+1) \stackrel{IV}{=} \frac{n(n+1)}{2} + (n+1)$$ $$= \frac{n(n+1)}{2} + \frac{2(n+1)}{2} = \frac{n(n+1) + 2(n+1)}{2}$$ $$= \frac{(n+1)(n+2)}{2} \checkmark$$

**Bemerkung:** Die Formel gilt sogar für $n = 0$, da $\sum_{k=1}^{0} k = 0 = \frac{0 \cdot 1}{2}$.

### Beispiel 3: Produktformel

**Aussage:** Für alle $n \in \mathbb{N}$, $n \geq 1$ gilt: $$\prod_{k=1}^{n} \left(\frac{k+1}{k}\right)^k = \frac{(n+1)^n}{n!}$$

**Beweis:**

**IA:** Für $n = 1$: $$\prod_{k=1}^{1} \left(\frac{k+1}{k}\right)^k = \left(\frac{2}{1}\right)^1 = 2 = \frac{2^1}{1!} \checkmark$$

**IV:** Für ein $n \geq 1$ gelte: $$\prod_{k=1}^{n} \left(\frac{k+1}{k}\right)^k = \frac{(n+1)^n}{n!}$$

**IS:** Zeige für $n+1$: $$\prod_{k=1}^{n+1} \left(\frac{k+1}{k}\right)^k = \prod_{k=1}^{n} \left(\frac{k+1}{k}\right)^k \cdot \left(\frac{n+2}{n+1}\right)^{n+1}$$ $$\stackrel{IV}{=} \frac{(n+1)^n}{n!} \cdot \left(\frac{n+2}{n+1}\right)^{n+1} = \frac{(n+2)^{n+1}}{n!(n+1)} = \frac{(n+2)^{n+1}}{(n+1)!} \checkmark$$

### Beispiel 4: Bernoulli-Ungleichung

**Aussage:** Sei $x \in \mathbb{R}$ mit $x \geq -1$. Dann gilt für alle $n \in \mathbb{N}$: $$(1+x)^n \geq 1 + nx$$

**Beweis:**

**IA:** Für $n = 0$: $$(1+x)^0 = 1 \geq 1 = 1 + 0 \cdot x \checkmark$$

**IV:** Für ein $n \in \mathbb{N}$ gelte: $$(1+x)^n \geq 1 + nx$$

**IS:** Es gilt $1 + x \geq 0$ (wegen $x \geq -1$). Damit: $$(1+x)^{n+1} = (1+x)^n \cdot (1+x) \stackrel{IV}{\geq} (1+nx)(1+x)$$ $$= 1 + x + nx + nx^2 = 1 + (n+1)x + nx^2$$ $$\geq 1 + (n+1)x \checkmark$$

(da $nx^2 \geq 0$)

### Beispiel 5: Anzahl der Permutationen

**Aussage:** n Elemente lassen sich auf genau $n!$ verschiedene Weisen anordnen.

**Beweis:**

**IA:** Ein Element lässt sich auf $1 = 1!$ Weise anordnen. ✓

**IV:** n Elemente lassen sich auf $n!$ Weisen anordnen.

**IS:** Bei $n+1$ Elementen:

- Lasse ein Element weg → verbleibende n Elemente auf $n!$ Weisen anordnen (IV)
- Das weggelassene Element kann an $n+1$ Stellen eingefügt werden (vor dem ersten oder nach jedem der n Elemente)
- Gesamt: $(n+1) \cdot n! = (n+1)!$ Möglichkeiten ✓

---

## 3. Binomialkoeffizienten

### Definition

Für $n, k \in \mathbb{N}$ und $0 \leq k \leq n$ ist der **Binomialkoeffizient**: $$\binom{n}{k} := \frac{n!}{k!(n-k)!}$$

Lies: "n über k"

### Alternative Darstellung

Für $0 < k \leq n$: $$\binom{n}{k} = \frac{n \cdot (n-1) \cdot ... \cdot (n-k+1)}{1 \cdot 2 \cdot ... \cdot k} = \prod_{j=1}^{k} \frac{n-j+1}{j}$$

(Zähler und Nenner haben jeweils k Faktoren)

### Spezialfälle

$$\binom{n}{0} = \frac{n!}{0! \cdot n!} = 1$$ $$\binom{n}{n} = \frac{n!}{n! \cdot 0!} = 1$$

### Rechenregeln

Für $n, k \in \mathbb{N}$ und $0 \leq k \leq n$:

1. **Symmetrie:** $$\binom{n}{k} = \binom{n}{n-k}$$
    
2. **Rekursionsformel:** Für $1 \leq k \leq n$: $$\binom{n}{k-1} + \binom{n}{k} = \binom{n+1}{k}$$
    

**Beweis der Rekursionsformel:** $$\binom{n}{k-1} + \binom{n}{k} = \frac{n!}{(k-1)!(n-k+1)!} + \frac{n!}{k!(n-k)!}$$ $$= \frac{n! \cdot k}{k!(n-k+1)!} + \frac{n!(n-k+1)}{k!(n-k+1)!}$$ $$= \frac{n!(k + n - k + 1)}{k!(n-k+1)!} = \frac{n!(n+1)}{k!(n-k+1)!} = \frac{(n+1)!}{k!(n-k+1)!} = \binom{n+1}{k}$$

### Pascalsches Dreieck

Die Rekursionsformel führt zum **Pascalschen Dreieck**:

![[Screenshot 2025-12-24 at 14.03.43.png]]

**Regel:** Jeder Eintrag ist die Summe der beiden darüberliegenden Einträge (außer Randeinträge = 1).

### Kombinatorische Interpretation

**Problem:** Auf wie viele Arten kann man k Kugeln aus einer Urne mit n Kugeln ziehen?

|                      |             |              **Reihenfolge relevant**              |             **Reihenfolge irrelevant**             |
| -------------------- | ----------- | :------------------------------------------------: | :------------------------------------------------: |
|                      | ........... | .................................................. | .................................................. |
| **Mit Zurücklegen**  | ........... |                       $n^k$                        |                 $\binom{n+k-1}{k}$                 |
| **Ohne Zurücklegen** | ........... |                $\frac{n!}{(n-k)!}$                 |                   $\binom{n}{k}$                   |


**Beispiele:**

- **Lotto 6 aus 49:** $\binom{49}{6} = 13.983.816$ Möglichkeiten
- **n=4, k=2 ohne Zurücklegen, Reihenfolge irrelevant:** $\binom{4}{2} = 6$ Möglichkeiten: ${1,2}, {1,3}, {1,4}, {2,3}, {2,4}, {3,4}$

**Interpretation von** $\binom{n}{k}$: Anzahl der k-elementigen Teilmengen einer n-elementigen Menge.

---

## 4. Binomischer Lehrsatz

### Satz (Binomischer Lehrsatz)

Für alle $n \in \mathbb{N}$ und reelle oder komplexe $a, b$ gilt: $$(a+b)^n = \sum_{k=0}^{n} \binom{n}{k} a^{n-k} b^k$$

**Beweis:** Mit vollständiger Induktion (siehe Skript für Details)

### Spezialfälle und Beispiele

**n = 2:** (Bekannte binomische Formel) $$(a+b)^2 = a^2 + 2ab + b^2$$

**n = 3:** $$(a+b)^3 = a^3 + 3a^2b + 3ab^2 + b^3$$

**n = 4:** $$(a+b)^4 = a^4 + 4a^3b + 6a^2b^2 + 4ab^3 + b^4$$

**n = 5:** Mit Binomialkoeffizienten $1, 5, 10, 10, 5, 1$: $$(a+b)^5 = a^5 + 5a^4b + 10a^3b^2 + 10a^2b^3 + 5ab^4 + b^5$$

**n = 6:** $$(a+b)^6 = a^6 + 6a^5b + 15a^4b^2 + 20a^3b^3 + 15a^2b^4 + 6ab^5 + b^6$$

**Trick:** Koeffizienten direkt aus der entsprechenden Zeile im Pascalschen Dreieck ablesen!

### Anwendungsbeispiele

**Beispiel 1:** $(x+1)^5$ $$(x+1)^5 = x^5 + 5x^4 + 10x^3 + 10x^2 + 5x + 1$$

**Beispiel 2:** $(2x-3y)^3$ $$(2x-3y)^3 = \sum_{k=0}^{3} \binom{3}{k} (2x)^{3-k}(-3y)^k$$ $$= (2x)^3 + 3(2x)^2(-3y) + 3(2x)(-3y)^2 + (-3y)^3$$ $$= 8x^3 - 36x^2y + 54xy^2 - 27y^3$$

---

## 5. Häufige Fehler bei Induktionsbeweisen

### Beispiel für eine falsche Induktion

**Falsche Behauptung:** Seien $a_1, ..., a_n \in \mathbb{R}$. Dann gilt $a_1 = a_2 = ... = a_n$.

**"Beweis":**

**IA:** Für $n = 1$ gilt $a_1 = a_1$ ✓

**IV:** Die Aussage gelte für ein $n \in \mathbb{N} \setminus {0}$.

**IS:** Seien $a_1, ..., a_{n+1} \in \mathbb{R}$. Nach IV gilt:

- $a_1 = a_2 = ... = a_n$ (n Zahlen)
- $a_2 = a_3 = ... = a_{n+1}$ (n Zahlen)

Also: $a_1 = a_2 = ... = a_n = a_{n+1}$ ✓

### Wo ist der Fehler? ⚡

Der Induktionsbeweis benötigt **mindestens 2 Zahlen**, um die beiden Gleichungsketten verbinden zu können. Der Beweis funktioniert also nur für $n \geq 2$.

Aber der Induktionsanfang war für $n = 1$!

**Problem:** Zwischen $n_0 = 1$ und dem ersten funktionierenden Schritt $n = 2$ gibt es eine **Lücke**.

**Lehre:** Der Induktionsanfang muss mit dem kleinsten Wert beginnen, für den der Induktionsschritt funktioniert!

---

## 📌 Zusammenfassung

|**Konzept**|**Beschreibung**|**Wichtig**|
|---|---|---|
|**Vollst. Induktion**|Beweistechnik für Aussagen über ℕ|IA + (IV $\Rightarrow$ IB)|
|**Induktionsanfang**|Zeige $A(n_0)$|Verankerung|
|**Induktionsschritt**|Zeige $A(n) \Rightarrow A(n+1)$|Unter Verwendung von IV|
|**Binomialkoeffizient**|$\binom{n}{k} = \frac{n!}{k!(n-k)!}$|Anzahl k-Teilmengen|
|**Pascalsches Dreieck**|Rekursive Darstellung|Jeder Eintrag = Summe der 2 darüber|
|**Binomischer Lehrsatz**|$(a+b)^n = \sum \binom{n}{k}a^{n-k}b^k$|Verallgemeinerung von $(a+b)^2$|

**Wichtige Formeln:**

- Summe: $\sum_{k=1}^{n} k = \frac{n(n+1)}{2}$
- Bernoulli: $(1+x)^n \geq 1 + nx$ für $x \geq -1$
- Rekursion: $\binom{n}{k-1} + \binom{n}{k} = \binom{n+1}{k}$

---
## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Zahlen]] Summen- und Produktzeichen, Fakultät
- [[VL.08 Polynome]] Binomischer Lehrsatz für Polynome
- [[VL.17 Konvergenz]] Konvergenzbeweise mit Induktion
- [[VL.40 Reihen]] Konvergenz von Reihen, oft mit Induktion

