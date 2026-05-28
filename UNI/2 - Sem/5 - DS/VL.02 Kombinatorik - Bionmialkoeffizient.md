**Class:** [[DS - Diskrete Strukturen]] 
**Date:** 24-04-2026
**Topics:** #Kombinatorik #Teilmengen #Permutationen #Binomialkoeffizient #Produktregel #Summenregel #InklusionExklusion #PascalschesDreieck

---

## 🎯 Lernziele der Vorlesung

VL.02 behandelt **§2.2 Auswählen von Elementen** und **§2.3 Eigenschaften des Binomialkoeffizienten** sowie den Beginn von **§3.1 Grundlegende kombinatorische Prinzipien**.

- Vier Arten, $k$ Elemente aus einer $n$-elementigen Menge zu ziehen
- Herleitung des Binomialkoeffizienten $\binom{n}{k}$ und der Permutationen $n!$
- Symmetrie und Rekursionsformel (Pascalsches Dreieck)
- Binomische Formel
- Rückbezug auf Laufzeiten der Algorithmen kTM und rec-IS
- Produktregel, Summenregel, Inklusion-Exklusion

---

## 2.2 Auswählen von Elementen

### k-elementige Teilmengen

**Definition.** Sei $M$ eine Menge und $k \in \mathbb{N}$. Die Menge $\mathcal{P}_k(M)$ aller $k$-elementigen Teilmengen von $M$:

$$\mathcal{P}_k(M) := \{U : U \subseteq M \text{ und } |U| = k\}$$

Das Bilden von $U$ entspricht dem Auswählen von $k$ verschiedenen Elementen aus $M$. Da $U$ eine **Menge** ist, spielt die Reihenfolge keine Rolle.

### Die vier Arten zu ziehen

Beim Ziehen von $k$ Elementen aus einer $n$-elementigen Menge unterscheidet man:

|  | **Reihenfolge wichtig (geordnet)** | **Reihenfolge nicht wichtig (ungeordnet)** |
|--|--|--|
| **Mit Zurücklegen** | $n^k$ | $\binom{k+n-1}{k}$ |
| **Ohne Zurücklegen** | $n^{\underline{k}} := \binom{n}{k} \cdot k! = \dfrac{n!}{(n-k)!}$ | $\binom{n}{k}$ |

**Einordnung von Beispielen:**

| Beispiel | Art |
|---------|-----|
| Siegertreppchen (Top 3 beim Rennen) | Ohne Zurücklegen, **geordnet** |
| Passwörter (8 Zeichen aus a–z, A–Z) | Mit Zurücklegen, **geordnet** |
| Lotto-Gewinnchance | Ohne Zurücklegen, **ungeordnet** |
| Sammelbilder in Müslipäckchen | Mit Zurücklegen, **ungeordnet** |

$\mathcal{P}_k(M)$ gehört in die Kategorie: **ohne Zurücklegen, ungeordnet** $\Rightarrow \binom{n}{k}$

---

### Ziehen ohne Zurücklegen und ohne Reihenfolge

**Herleitung (geordnet, ohne Zurücklegen):**

| Ziehung | Möglichkeiten |
|--------|--------------|
| 1. Element | $n$ |
| 2. Element | $n-1$ |
| 3. Element | $n-2$ |
| $\vdots$ | $\vdots$ |
| $k$-tes Element | $n-(k-1)$ |
| **Insgesamt** | $n \cdot (n-1) \cdot (n-2) \cdots (n-(k-1))$ |

⚠️ **Problem:** Wir haben doppelt gezählt — $(a_1, a_2, a_3)$ und $(a_3, a_2, a_1)$ liefern dasselbe Ergebnis, da die Reihenfolge nicht beachtet wird.

**Lösung:** Durch die Zahl der Anordnungen von $k$ Elementen teilen, also durch $k!$:

$$\boxed{\text{Anzahl} = \frac{n \cdot (n-1) \cdot (n-2) \cdots (n-(k-1))}{k!} = \frac{n!}{k! \cdot (n-k)!}}$$

---

### Permutationen

**Satz.** Die Elemente einer Menge mit $n$ Elementen können auf $n!$ verschiedene Arten angeordnet werden.

**Definition (Fakultät):**

$$\boxed{n! := \begin{cases} 1 & \text{für } n = 0 \\ n \cdot (n-1)! & \text{für } n > 0 \end{cases}}$$

Eine **Anordnung** von $M$ ist eine Folge $(a_1, \ldots, a_n)$, in der jedes Element von $M$ genau einmal vorkommt.

**Beweis (per Induktion über $n$):**

- **Induktionsverankerung** $n = 0$: Es gibt $0! = 1$ Möglichkeit, die leere Menge anzuordnen. ✓
- **Induktionsannahme:** Es gibt $n!$ Anordnungen einer $n$-elementigen Menge.
- **Induktionsschluss:** Sei $M = \{a_1, \ldots, a_{n+1}\}$. Eine Anordnung wird eindeutig bestimmt durch:
  1. die Wahl des ersten Elements $a_{i_1} \in M$ → $n+1$ Möglichkeiten
  2. die Anordnung der restlichen $n$ Elemente aus $M \setminus \{a_{i_1}\}$ → nach IA: $n!$ Möglichkeiten
  - Insgesamt: $(n+1) \cdot n! = (n+1)!$ $\square$

---

### Ziehen mit Zurücklegen und ohne Reihenfolge

**Satz.** Die Zahl der Möglichkeiten, $k$ Elemente aus einer $n$-elementigen Menge mit Zurücklegen ohne Reihenfolge zu ziehen, ist $\binom{k+n-1}{k}$.

**Beweis (Strichlisten-Argument):**

Wir führen eine **Strichliste** mit $n$ nummerierten Feldern. Jedes Mal, wenn wir $a_i$ ziehen, malen wir einen Punkt $\bullet$ in Feld $a_i$.

Beispiel für $a_3, a_1, a_4, a_1, a_1, a_3, a_n$:

```
●●● |   | ●● | ● |   |   | ●
 a₁   a₂   a₃   a₄        aₙ
```

Eine Strichliste ist eine Folge von $\bullet$ und $|$ mit genau $n-1$ Strichen und $k$ Punkten.

- Länge der Strichliste: $k + n - 1$
- Strichlisten unterscheiden sich nur durch die **Position der Striche**
- Zahl verschiedener Strichlisten = Zahl der Möglichkeiten, $k$ Punkte auf $k+n-1$ Positionen zu verteilen

$$= \binom{k+n-1}{k} = \binom{k+n-1}{n-1} \quad \square$$

---

## 2.3 Eigenschaften des Binomialkoeffizienten

### Definition

**Definition.** Für alle $n \in \mathbb{N}$ und $0 \leq k \leq n$:

$$\boxed{\binom{n}{k} := \frac{n!}{k! \cdot (n-k)!}}$$

Für $k > n$ und $k < 0$: $\binom{n}{k} := 0$

**Korollar:** Für jede Menge $M$ mit $n$ Elementen gilt $|\mathcal{P}_k(M)| = \binom{n}{k}$.

> $\binom{n}{k}$ gibt die Zahl der $k$-elementigen Teilmengen einer $n$-elementigen Menge an.

---

### Symmetrie

**Satz.** Für $n \in \mathbb{N}$ und $k \in \{0, \ldots, n\}$ gilt:

$$\boxed{\binom{n}{k} = \binom{n}{n-k}}$$

**Beweis:**

$$\binom{n}{k} := \frac{n!}{k!(n-k)!} = \frac{n!}{(n-(n-k))!(n-k)!} =: \binom{n}{n-k} \quad \square$$

**Intuitive Bedeutung:** Um eine $k$-elementige Teilmenge $U \subseteq M$ zu konstruieren, ist es unerheblich, ob wir die $k$ Elemente von $U$ oder die $n-k$ Elemente von $M \setminus U$ auswählen.

---

### Rekursionsformel (Pascalsches Dreieck)

**Satz.** Für alle $n, k \in \mathbb{N}$ mit $0 \leq k \leq n$:

$$\boxed{\binom{n}{k} = \binom{n-1}{k-1} + \binom{n-1}{k}}$$

**Beweis.** Sei $M := \{a_1, \ldots, a_n\}$. Partitioniere $\mathcal{P}_k(M)$ in zwei disjunkte Mengen:

$$\mathcal{P}_k(M) = \underbrace{\{X \subseteq M : |X| = k \text{ und } a_1 \in X\}}_{P^+} \;\dot{\cup}\; \underbrace{\{X \subseteq M : |X| = k \text{ und } a_1 \notin X\}}_{P^-}$$

Es gilt also:

$$\binom{n}{k} = |\mathcal{P}_k(M)| = |P^+| + |P^-|$$

$$= |\{X \subseteq M \setminus \{a_1\} : |X| = k-1\}| + |\{X \subseteq M \setminus \{a_1\} : |X| = k\}|$$

$$= \binom{n-1}{k-1} + \binom{n-1}{k} \quad \square$$

---

### Binomische Formel

**Satz.** Seien $x, y \in \mathbb{R}$ und $n \in \mathbb{N}$. Dann gilt:

$$\boxed{(x + y)^n = \sum_{k=0}^{n} \binom{n}{k} x^k y^{n-k}}$$

Der Name „Binomialkoeffizient" kommt von seiner Rolle in dieser Formel.

---

### Gesamtübersicht Binomialkoeffizient

**Satz.** Für $n \in \mathbb{N}$ und $k \in \{0, \ldots, n\}$:

$$\boxed{\binom{n}{k} = \binom{n}{n-k} = \binom{n-1}{k-1} + \binom{n-1}{k} = \frac{n!}{k! \cdot (n-k)!}}$$

→ Die Rekursionsformel $\binom{n}{k} = \binom{n-1}{k-1} + \binom{n-1}{k}$ ist die Bauvorschrift des **Pascalschen Dreiecks**.

---

### Rückbezug: Laufzeiten der Algorithmen

| Algorithmus | Laufzeit | Begründung |
|-----------|---------|-----------|
| **kTM** (iteriert über $k$-elem. Mengen) | $\Theta\!\left(\binom{n}{k}\right)$ | Zahl der $k$-elementigen Teilmengen |
| **rec-IS** (rekursiv über Knoten) | $L(n,k) = L(n-1,k-1) + L(n-1,k)$ | Rekursion $= \binom{n-1}{k-1} + \binom{n-1}{k} = \binom{n}{k}$ |

✅ Beide Algorithmen haben im Wesentlichen die Laufzeit $\Theta\!\left(\binom{n}{k}\right)$.

---

## 3.1 Grundlegende kombinatorische Prinzipien

### Produktregel

**$k$-stufiger Prozess:** $k$-mal hintereinander eine Aktion ausführen.

**Produktregel:**

$$\boxed{\text{Anzahl der Möglichkeiten} = n_1 \cdot n_2 \cdots n_k}$$

wobei $n_i$ die Zahl der Möglichkeiten in der $i$-ten Stufe ist.

**Alternative Formulierung.** Seien $M_1, \ldots, M_k$ endliche Mengen, aus denen wir je ein Element $a_i \in M_i$ ziehen:

$$\prod_{i=1}^{k} |M_i| = |M_1| \cdot |M_2| \cdots |M_k|$$

**Beispiel:** $k$ Elemente mit Zurücklegen und Reihenfolge: $\underbrace{n \cdot n \cdots n}_{k \text{ mal}} = n^k$

---

### Summenregel

**Summenregel.** Seien $A_1, \ldots, A_k$ paarweise disjunkte Mengen ($A_i \cap A_j = \emptyset$ für alle $1 \leq i < j \leq k$):

$$\boxed{\left|\bigcup_{i=1}^{k} A_i\right| = \sum_{i=1}^{k} |A_i|}$$

**Anwendung im Beweis der Rekursionsformel:** Da $P^+$ und $P^-$ disjunkt sind, gilt $|\mathcal{P}_k| = |P^+| + |P^-|$.

---

### Vereinigung nicht-disjunkter Mengen

**Zwei Mengen** ($A \cap B \neq \emptyset$):

$$|A \cup B| = |A| + |B| - |A \cap B|$$

Die Elemente in $A \cap B$ werden ohne Korrektur doppelt gezählt.

**Drei Mengen:**

$$|A \cup B \cup C| = |A| + |B| + |C| - |A \cap B| - |A \cap C| - |B \cap C| + |A \cap B \cap C|$$

⚠️ Ohne den letzten Term $+|A \cap B \cap C|$ würden die Elemente im Dreifachschnitt dreifach abgezogen und gar nicht gezählt.

**Muster:** $+, -, +, -, \ldots$ (alternierend)

---

### Prinzip der Inklusion-Exklusion

**Satz.** Seien $A_1, \ldots, A_n$ endliche Mengen:

$$\boxed{\left|\bigcup_{i=1}^{n} A_i\right| = \sum_{r=1}^{n} \left( (-1)^{r-1} \sum_{1 \leq i_1 < i_2 < \cdots < i_r \leq n} \left|\bigcap_{j=1}^{r} A_{i_j}\right| \right)}$$

**Beweis-Idee.** Sei $a \in \bigcup_{i=1}^{n} A_i$ beliebig und sei $a$ in genau $m$ der Mengen enthalten. Der Beitrag von $a$ zur rechten Seite:

$$\binom{m}{1} - \binom{m}{2} + \binom{m}{3} - \cdots \pm \binom{m}{m} = \sum_{r=1}^{m} (-1)^{r-1} \binom{m}{r} = 1 \quad \square$$

(Beweis wird am 29.04.2026 fortgesetzt.)

---

## 📌 Alle Formeln auf einen Blick

| Ziehen | Geordnet | Ungeordnet |
|-------|---------|-----------|
| **Mit Zurücklegen** | $n^k$ | $\binom{k+n-1}{k}$ |
| **Ohne Zurücklegen** | $\dfrac{n!}{(n-k)!}$ | $\binom{n}{k} = \dfrac{n!}{k!(n-k)!}$ |

| Prinzip                 | Formel                                                                               |
| ----------------------- | ------------------------------------------------------------------------------------ |
| **Produktregel**        | $n_1 \cdot n_2 \cdots n_k$                                                           |
| **Summenregel**         | $\left\|\bigcup A_i\right\| = \sum A_i$ (disjunkt)                                   |
| **Inklusion-Exklusion** | $\sum_{r=1}^{n} (-1)^{r-1} \sum_{i_1 < \cdots < i_r} \left\|\bigcap A_{i_j}\right\|$ |

---

## ✅ Kernaussagen

- Die Unterscheidung geordnet/ungeordnet und mit/ohne Zurücklegen führt zu **vier grundlegend verschiedenen Zählproblemen**
- $\mathcal{P}_k(M)$ ist **ungeordnet ohne Zurücklegen** $\Rightarrow |\mathcal{P}_k(M)| = \binom{n}{k}$
- Permutationen: Spezialfall von geordnet ohne Zurücklegen mit $k = n$: $n!$
- Die Rekursionsformel $\binom{n}{k} = \binom{n-1}{k-1} + \binom{n-1}{k}$ entspricht exakt der Laufzeit-Rekursion von rec-IS
- Inklusion-Exklusion verallgemeinert die Summenregel auf **nicht-disjunkte Mengen**

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[DS VL.01]]: Unabhängige Mengen, kTM und rec-IS — Grundlage für Laufzeitanalyse
- [[DS VL.03]]: Fortsetzung §3 — vollständiger Beweis von Inklusion-Exklusion (29.04.2026)
- [[FoG §3]]: Vollständige Induktion — Permutationssatz per Induktion
- [[FoG §1]]: Mengenlehre — Schnitt, Vereinigung, disjunkte Vereinigung
- [[AlgoDat]]: Laufzeitanalyse; $\binom{n}{k}$ als Laufzeitschranke