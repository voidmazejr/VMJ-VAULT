**Class:** [[AnaLina]]  
**Date:** 27-12-2025
**Topics:** #RationaleFunktionen #Partialbruchzerlegung #Polstellen #Polynomdivision

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung behandelt rationale Funktionen als Brüche von Polynomen und führt die Partialbruchzerlegung ein, eine fundamentale Technik zur Zerlegung komplexer rationaler Ausdrücke in einfachere Summanden.

- **Definition** rationaler Funktionen und ihrer Polstellen
- **Komplexe Partialbruchzerlegung** für beliebige rationale Funktionen
- **Reelle Partialbruchzerlegung** für Funktionen mit reellen Koeffizienten
- Systematisches **Berechnungsverfahren** mit Polynomdivision, Zuhaltemethode und Koeffizientenvergleich
- **Anwendungen** in Integration und Laplace-Transformation

---

## 1. Rationale Funktionen

### Definition

Eine **rationale Funktion** ist ein Bruch von Polynomen:

$$f(z) = \frac{p(z)}{q(z)}$$

wobei $p$ und $q$ Polynome sind.

**Definitionsbereich:** $$f : D \to \mathbb{C} \text{ mit } D = \mathbb{C} \setminus {z \mid q(z) = 0}$$

Für reelle Polynome $p, q$: $$f : D \to \mathbb{R} \text{ mit } D = \mathbb{R} \setminus {z \mid q(z) = 0}$$

### Polstellen

Sei $z_0$ eine Nullstelle des Nenners, also $q(z_0) = 0$:

1. **Polstelle:** Falls $p(z_0) \neq 0$ heißt $z_0$ ein **Pol** oder **Polstelle** von $f$
    
    - $z_0$ ist ein **Pol der Ordnung** $k$, wenn $z_0$ eine $k$-fache Nullstelle von $q$ ist
    - **Einfacher Pol:** Ordnung 1
    - **Mehrfacher Pol:** Ordnung $\geq 2$
2. **Hebbare Singularität:** Falls auch $p(z_0) = 0$, kürze $(z - z_0)$ so oft wie möglich
    

### Beispiele

**Beispiel 1:** $f(z) = \frac{1}{z-3}$

- Einfacher Pol in $z = 3$

**Beispiel 2:** $f(z) = \frac{z^4 + 3z + 5}{z^2 + 1} = \frac{z^4 + 3z + 5}{(z-i)(z+i)}$

- Einfache Pole in $z = i$ und $z = -i$

**Beispiel 3:** $f(z) = \frac{z^4 + 3z + 5}{(z+1)^2}$

- Pol der Ordnung 2 in $z = -1$

**Beispiel 4:** $f(z) = \frac{(z-1)(z+1)}{(z-1)(z+2)}$

- Nach Kürzen: $f(z) = \frac{z+1}{z+2}$ mit einfachem Pol in $z = -2$
- Bei $z = 1$ sind Zähler und Nenner null → hebbar durch Kürzen

**Beispiel 5:** $f(z) = \frac{(z-1)(z+1)}{(z-1)^2(z+2)}$

- Nach Kürzen: $f(z) = \frac{z+1}{(z-1)(z+2)}$
- Einfacher Pol in $z = -2$ und einfacher Pol in $z = 1$ (bleibt nach Kürzen)

---

## 2. Komplexe Partialbruchzerlegung

### Hauptsatz

**Satz (Komplexe Partialbruchzerlegung):** Sei $f(z) = \frac{p(z)}{q(z)}$ eine rationale Funktion.

**Fall 1: Nur einfache Nullstellen**

Hat $q$ die einfachen Nullstellen $z_1, \ldots, z_n$, also $$q(z) = a_n \prod_{k=1}^{n} (z - z_k)$$

so hat $f$ die eindeutige Partialbruchzerlegung: $$f(z) = s(z) + \sum_{k=1}^{n} \frac{A_k}{z - z_k} = s(z) + \frac{A_1}{z-z_1} + \ldots + \frac{A_n}{z-z_n}$$

mit einem Polynom $s(z)$ und eindeutig bestimmten Koeffizienten $A_1, \ldots, A_n \in \mathbb{C}$.

**Fall 2: Mehrfache Nullstellen**

Ist $z_k$ eine $m_k$-fache Nullstelle von $q$, wird der Summand $\frac{A_k}{z-z_k}$ ersetzt durch: $$\frac{A_{k,1}}{z-z_k} + \frac{A_{k,2}}{(z-z_k)^2} + \ldots + \frac{A_{k,m_k}}{(z-z_k)^{m_k}}$$

---

## 3. Berechnungsverfahren

### Schritt 1: Polynomdivision

Falls $\deg(p) \geq \deg(q)$: Führe Polynomdivision durch $$p(z) = s(z) \cdot q(z) + r(z) \text{ mit } \deg(r) < \deg(q)$$

Dann: $$f(z) = \frac{p(z)}{q(z)} = s(z) + \frac{r(z)}{q(z)}$$

Falls $\deg(p) < \deg(q)$: Setze $s(z) = 0$ und $r(z) = p(z)$ (keine Division nötig).

### Schritt 2: Ansatz für die Partialbruchzerlegung

Für $\frac{r(z)}{q(z)}$ mache den entsprechenden Ansatz basierend auf den Nullstellen von $q$.

### Schritt 3: Koeffizienten bestimmen

**Möglichkeit 1: Zuhaltemethode** (besonders für einfache Pole)

Multipliziere den Ansatz mit $(z - z_k)$ und setze $z = z_k$ ein:

Für einfache Nullstelle $z_k$: $$\frac{r(z)}{(z-z_1)(z-z_2)\cdots(z-z_n)} = \frac{A_1}{z-z_1} + \frac{A_2}{z-z_2} + \ldots + \frac{A_n}{z-z_n}$$

Multipliziere mit $(z - z_1)$ und setze $z = z_1$ ein: $$A_1 = \frac{r(z_1)}{(z_1-z_2)\cdots(z_1-z_n)}$$

**Praktisches Vorgehen:** Halte $(z - z_k)$ in $\frac{r(z)}{q(z)}$ zu und setze $z = z_k$ in den Rest ein.

**Möglichkeit 2: Koeffizientenvergleich**

Multipliziere den Ansatz mit $q(z)$ und vergleiche die Koeffizienten auf beiden Seiten. Dies ergibt ein lineares Gleichungssystem.

### Beispiel: Einfache Pole

$$f(z) = \frac{z^2 + z + 4}{(z-3)(z^2+1)} = \frac{z^2 + z + 4}{(z-3)(z-i)(z+i)}$$

**Ansatz:** $f(z) = \frac{A}{z-3} + \frac{B}{z-i} + \frac{C}{z+i}$

**Zuhaltemethode:** $$A = \frac{3^2 + 3 + 4}{3^2 + 1} = \frac{16}{10} = \frac{8}{5}$$

$$B = \frac{i^2 + i + 4}{(i-3)(2i)} = -\frac{1}{2} \cdot \frac{3+i}{1+3i} = -\frac{3}{10} + \frac{2}{5}i$$

$$C = \frac{(-i)^2 - i + 4}{(-i-3)(-2i)} = -\frac{3}{10} - \frac{2}{5}i$$

**Ergebnis:** $$f(z) = \frac{8/5}{z-3} + \frac{-3/10 + 2i/5}{z-i} + \frac{-3/10 - 2i/5}{z+i}$$

### Beispiel: Mehrfacher Pol

$$f(z) = \frac{5z^2 - 4z + 7}{(z-1)^2(z+3)}$$

**Ansatz:** $f(z) = \frac{A}{z-1} + \frac{B}{(z-1)^2} + \frac{C}{z+3}$

**Zuhaltemethode für** $B$ und $C$: $$C = \frac{5 \cdot 9 + 12 + 7}{16} = 4$$

$$B = \frac{5 - 4 + 7}{4} = 2$$

Für $A$ multipliziere mit $(z-1)^2(z+3)$: $$5z^2 - 4z + 7 = A(z-1)(z+3) + 2(z+3) + 4(z-1)^2$$

Koeffizientenvergleich vor $z^2$: $5 = A + 4 \implies A = 1$

**Ergebnis:** $$f(z) = \frac{1}{z-1} + \frac{2}{(z-1)^2} + \frac{4}{z+3}$$

---

## 4. Reelle Partialbruchzerlegung

### Motivation

Für reelle rationale Funktionen $f(x) = \frac{p(x)}{q(x)}$ mit reellen Koeffizienten können komplexe Nullstellen auftreten. Diese treten in **konjugiert komplexen Paaren** auf: $\lambda = a + ib$ und $\overline{\lambda} = a - ib$.

### Zusammenfassen komplexer Pole

**Linearfaktoren zusammenfassen:** $$(x - \lambda)(x - \overline{\lambda}) = (x - (a+ib))(x - (a-ib)) = (x-a)^2 + b^2$$

**Entsprechende Terme in der PBZ:** $$\frac{A}{x-(a+ib)} + \frac{B}{x-(a-ib)} = \frac{Cx + D}{(x-a)^2 + b^2}$$

mit reellen Koeffizienten $C, D$.

### Ansatz für reelle PBZ

|Faktor des Nenners|Ansatzterm|
|---|---|
|$z - z_0$|$\frac{A}{z-z_0}$|
|$(z - z_0)^m$|$\frac{A_1}{z-z_0} + \frac{A_2}{(z-z_0)^2} + \ldots + \frac{A_m}{(z-z_0)^m}$|
|$(z-a)^2 + b^2$|$\frac{Cz + D}{(z-a)^2 + b^2}$|
|$((z-a)^2 + b^2)^m$|$\frac{C_1z + D_1}{(z-a)^2 + b^2} + \frac{C_2z + D_2}{((z-a)^2 + b^2)^2} + \ldots + \frac{C_mz + D_m}{((z-a)^2 + b^2)^m}$|

### Beispiel: Reelle PBZ

$$f(z) = \frac{z^2 + z + 4}{(z-3)(z^2+1)}$$

**Reeller Ansatz:** $$f(z) = \frac{A}{z-3} + \frac{Cz + D}{z^2 + 1}$$

Multiplikation mit Nenner: $$z^2 + z + 4 = A(z^2 + 1) + (Cz + D)(z - 3)$$ $$= (A + C)z^2 + (-3C + D)z + (A - 3D)$$

Koeffizientenvergleich:

- $A + C = 1$
- $-3C + D = 1$
- $A - 3D = 4$

Lösung: $A = \frac{8}{5}$, $C = -\frac{3}{5}$, $D = -\frac{4}{5}$

**Ergebnis:** $$f(z) = \frac{8/5}{z-3} + \frac{-3z/5 - 4/5}{z^2 + 1}$$

---

## 5. Systematisches Vorgehen

### Zusammenfassung des Algorithmus

**Schritt 1: Polynomdivision**

- Nur falls $\deg(p) \geq \deg(q)$
- Ergibt $p(z) = s(z) \cdot q(z) + r(z)$ mit $\deg(r) < \deg(q)$
- Sonst: $s(z) = 0$, $r(z) = p(z)$

**Schritt 2: Zerlegung des Nenners**

- Bestimme alle Nullstellen von $q(z)$
- Komplex: Zerlege in Linearfaktoren
- Reell: Zerlege in Linearfaktoren und irreduzible quadratische Faktoren
- Fasse gleiche Faktoren zu Potenzen zusammen

**Schritt 3: Ansatz**

- Der Ansatz bestimmt sich aus den Faktoren des Nenners
- Gesamtanzahl der Koeffizienten = $\deg(q)$

**Schritt 4: Koeffizienten bestimmen**

- **Zuhaltemethode:** Für einfache Pole und höchsten Koeffizienten mehrfacher Pole
- **Koeffizientenvergleich:** Für verbleibende Koeffizienten
- **Einsetzen spezieller Werte:** Alternative zum Koeffizientenvergleich

---
## 📌 Anwendungen

**Integration:** Partialbruchzerlegung ermöglicht die Integration rationaler Funktionen durch Integration der einzelnen Terme (siehe VL.31).

**Laplace-Transformation:** Zentral in:

- Regelungstechnik
- Netzwerktheorie
- Signalverarbeitung
- Lösung von Differentialgleichungen

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.08 Polynome]]: Grundlagen zu Polynomen und ihren Nullstellen
- [[VL.10 Vektorräume]]: Lineare Unabhängigkeit im Beweis der Existenz
- [[VL.11 Basis und Dimension]]: Basis des Vektorraums der Polynome
- [[VL.13 Lineare Gleichungssysteme]]: Lösung bei Koeffizientenvergleich
