**Class:** [[FoG - Formal-mathematische Grundlagen]]  
**Date:** 17-10-2025  
**Topics:** #Aussagenlogik #Semantik #LogischeÄquivalenz #Implikation #Beweisstrategien #NatürlichesSchließen
**Link:** [[VL.05 FoG Skript-32-35 1.pdf]]

---

## 🎯 Lernziele der Vorlesung

VL.05 behandelt das Kapitel **„Natürliches Schließen III"**: Syntax und Semantik der Aussagenlogik, die materiale Implikation mit ihren mehreren Rechtfertigungen sowie logische Äquivalenz und daraus abgeleitete Beweisstrategien.

- **Syntax der Aussagenlogik**: Induktive Definition der Formelmenge $\mathbf{A}(V)$ mit Junktoren
- **Semantik & Auswertung**: Variablenbelegung $\beta$, Auswertungsfunktion $[\![\cdot]\!]^\beta$, Wahrheitstabellen
- **Materiale Implikation**: Wahrheitstabelle verstehen und mit 4 Strategien rechtfertigen
- **Logische Äquivalenz**: Definition, Allgemeingültigkeit, Kontradiktion, Erfüllbarkeit
- **Äquivalenzgesetze (Prop. 6.2.2/6.2.3)**: De Morgan, Kontraposition, Distributivität, Quantoren
- **Beweisstrategien**: Direkter Beweis, Beweis durch Widerspruch, Modus Tollens, Falsum, Doppelnegation
- **Ableitbare Regeln**: ¬¬E/I, MT, ⊥E, BW als Konsequenzen aus Äquivalenzen

***

## 1. Syntax der Aussagenlogik

### Definition 2.3.2 – Formelmenge A(V)

Sei $V$ eine Menge von aussagenlogischen Variablen mit $V \cap \{\top, \bot, \neg, \wedge, \vee, \rightarrow, \leftrightarrow, (, )\} = \emptyset$.

$$\boxed{\mathbf{A}(V) \text{ ist die kleinste Menge, definiert durch folgende Regeln:}}$$

$$
(A_\text{BASE})\;\frac{\varphi \in V \cup \{\top, \bot\}}{\varphi \in \mathbf{A}(V)}
\qquad
(A_\text{NOT})\;\frac{\varphi \in \mathbf{A}(V)}{\neg\varphi \in \mathbf{A}(V)}
$$

$$
(A_\text{AND})\;\frac{\varphi_1 \in \mathbf{A}(V)\quad \varphi_2 \in \mathbf{A}(V)}{(\varphi_1 \wedge \varphi_2) \in \mathbf{A}(V)}
\qquad
(A_\text{OR})\;\frac{\varphi_1 \in \mathbf{A}(V)\quad \varphi_2 \in \mathbf{A}(V)}{(\varphi_1 \vee \varphi_2) \in \mathbf{A}(V)}
$$

$$
(A_\text{IMP})\;\frac{\varphi_1 \in \mathbf{A}(V)\quad \varphi_2 \in \mathbf{A}(V)}{(\varphi_1 \rightarrow \varphi_2) \in \mathbf{A}(V)}
\qquad
(A_\text{BI})\;\frac{\varphi_1 \in \mathbf{A}(V)\quad \varphi_2 \in \mathbf{A}(V)}{(\varphi_1 \leftrightarrow \varphi_2) \in \mathbf{A}(V)}
$$

**Wichtige Begriffe:**
- **Junktoren / Operatoren**: $\neg,\; \wedge,\; \vee,\; \rightarrow,\; \leftrightarrow$
- **$\top$ (Verum)**: stets wahr; **$\bot$ (Falsum)**: stets falsch
- **Atomare Formel**: jedes $\varphi \in V \cup \{\top,\bot\}$ (Basis der Induktion)

> 💡 **Merkhilfe:** Die Definition ist *induktiv* – komplexere Formeln entstehen durch schrittweise Anwendung der Regeln. Man liest die Bruchstriche als „daraus folgt".

```
Syntax-Überblick:

  Atom (V, ⊤, ⊥)
      │
      ├─ ¬φ          (Negation)
      ├─ φ₁ ∧ φ₂     (Konjunktion)
      ├─ φ₁ ∨ φ₂     (Disjunktion)
      ├─ φ₁ → φ₂     (Implikation)
      └─ φ₁ ↔ φ₂     (Biimplikation)
```

***

## 2. Semantik der Aussagenlogik

### Definition 6.1.1 – Variablenbelegung und Auswertung

$$\boxed{\beta : V \to \mathbb{B} = \{0, 1\} \quad \text{(Variablenbelegung)}}$$

$$\boxed{[\![\cdot]\!]^\beta : \mathbf{A}(V) \to \mathbb{B} \quad \text{(Auswertung zu } \beta \text{)}}$$

**Basisregeln der Auswertung:**

$$[\![\top]\!]^\beta \triangleq 1, \qquad [\![\bot]\!]^\beta \triangleq 0, \qquad [\![p]\!]^\beta \triangleq \beta(p)$$

> 💡 **Rolle:** Die Variablenbelegung $\beta$ ist die „Eingabe" – sie weist jeder Variable einen Wahrheitswert zu. Die Auswertung $[\![\varphi]\!]^\beta$ propagiert diesen Wert durch die Formelstruktur.

**Beispiel:** $V \triangleq \{p, q, r\}$, mit $n = 3$ Variablen gibt es $2^n = 8$ Belegungen.

### Bemerkung 6.1.2 – Algebraische Darstellung der Junktoren

$$\boxed{[\![\neg\varphi]\!] = 1 - [\![\varphi]\!]}$$

$$\boxed{[\![\varphi_1 \wedge \varphi_2]\!] = \min([\![\varphi_1]\!],\; [\![\varphi_2]\!])}$$

$$\boxed{[\![\varphi_1 \vee \varphi_2]\!] = \max([\![\varphi_1]\!],\; [\![\varphi_2]\!])}$$

$$\boxed{[\![\varphi_1 \rightarrow \varphi_2]\!] = 1 \iff [\![\varphi_1]\!] \leq [\![\varphi_2]\!]}$$

$$\boxed{[\![\varphi_1 \leftrightarrow \varphi_2]\!] = 1 \iff [\![\varphi_1]\!] = [\![\varphi_2]\!]}$$

### Wahrheitstabellen aller Junktoren

| $[\![\varphi]\!]$ | $[\![\neg\varphi]\!]$ |
|:-:|:-:|
| 0 | 1 |
| 1 | 0 |

| $[\![\varphi_1]\!]$ | $[\![\varphi_2]\!]$ | $[\![\varphi_1 \wedge \varphi_2]\!]$ | $[\![\varphi_1 \vee \varphi_2]\!]$ | $[\![\varphi_1 \rightarrow \varphi_2]\!]$ | $[\![\varphi_1 \leftrightarrow \varphi_2]\!]$ |
|:-:|:-:|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 0 | **1** | 1 |
| 0 | 1 | 0 | 1 | **1** | 0 |
| 1 | 0 | 0 | 1 | **0** | 0 |
| 1 | 1 | 1 | 1 | **1** | 1 |

⚠️ **Achtung:** Das logische $\vee$ ist **inklusiv** (auch „beide wahr" → wahr). Umgangssprache verwendet „oder" oft exklusiv – das ist **nicht** dasselbe wie $\vee$.

### Beispiel – Auswertung von $p \rightarrow (q \vee r)$

| $p$ | $q$ | $r$ | $q \vee r$ | $p \rightarrow (q \vee r)$ |
|:-:|:-:|:-:|:-:|:-:|
| 0 | 0 | 0 | 0 | 1 |
| 0 | 0 | 1 | 1 | 1 |
| 0 | 1 | 0 | 1 | 1 |
| 0 | 1 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 | **0** |
| 1 | 0 | 1 | 1 | 1 |
| 1 | 1 | 0 | 1 | 1 |
| 1 | 1 | 1 | 1 | 1 |

> 💡 **Merkhilfe:** Jede Zeile entspricht einer Belegung $\beta$. Bei $n$ Variablen: $2^n$ Zeilen.

***

## 3. Die materiale Implikation – Rechtfertigungen

### Das Problem

Die Implikation $\varphi_1 \rightarrow \varphi_2$ wird oft mit „wenn $\varphi_1$, dann $\varphi_2$" assoziiert – dies führt zu kontraintuitiven Fällen:

$$\boxed{[\![\varphi_1 \rightarrow \varphi_2]\!] = 1 \iff [\![\varphi_1]\!] \leq [\![\varphi_2]\!] \quad \text{(„}\varphi_2 \text{ ist mindestens so wahr wie } \varphi_1 \text{")} }$$

⚠️ **Kontraintuitives Kernproblem:** Wenn die Prämisse $\varphi_1$ **falsch** ist ($[\![\varphi_1]\!] = 0$), gilt die Implikation **immer als wahr** – unabhängig von $\varphi_2$.

### Rechtfertigung 1 – Lügner-Analogie (Kelly/Solow)

> „Eine Implikation ist genau dann wahr, wenn ein Mensch, der sie äußert, nicht Lügner genannt werden kann."

**Beispiel 3.2:**

| Zeile | $[\![\varphi_1]\!]$ | $[\![\varphi_2]\!]$ | Satz | Bewertung |
|:-:|:-:|:-:|:--|:-:|
| 4 | 1 | 1 | „Wenn die Erde ein Planet ist, ist 7 prim." | ✅ wahr |
| 2 | 0 | 1 | „Wenn die Erde **kein** Planet ist, ist 7 prim." | ✅ wahr (kein Widerlegungsgrund) |
| 1 | 0 | 0 | „Wenn die Erde kein Planet ist, ist 7 **keine** Primzahl." | ✅ wahr (kein Widerlegungsgrund) |
| 3 | 1 | 0 | „Wenn die Erde ein Planet ist, ist 7 **keine** Primzahl." | ❌ **falsch** – Lügner! |

### Rechtfertigung 2 – Mathematische Beispiele

**Beispiel 4.1:** $A(x,y) \equiv (x = y)$, $B(x,y) \equiv (x^2 = y^2)$

$$A(x,y) \rightarrow B(x,y): \quad \text{„Wenn } x = y, \text{ dann } x^2 = y^2\text{." ✅}$$

- Wenn $x = y$ (Zeile 4): beide wahr ✅
- Wenn $x \neq y$ (Zeile 1/2): $A$ falsch, Implikation trivial wahr ✅
- Fall $A=1, B=0$ (Zeile 3): mathematisch **unmöglich** – kein Gegenbeispiel konstruierbar

**Beispiel 4.2 – Teilmengenrelation:**

$$\boxed{A \subseteq B \iff (\forall x)\, (x \in A \rightarrow x \in B)}$$

Hier entsprechen Zeile 1/2 der Tabelle Elementen außerhalb von $A$ – sie widersprechen $A \subseteq B$ nicht. Zeile 3 würde $A \subseteq B$ direkt widersprechen.

### Rechtfertigung 3 – Ordnungsinterpretation (Kreutzer)

$$\boxed{[\![\varphi_1 \rightarrow \varphi_2]\!] \triangleq [\![\varphi_1]\!] \leq [\![\varphi_2]\!]}$$

> „$B$ ist **mindestens so wahr** wie $A$."
> Äquivalent: „$A$ ist höchstens so wahr wie $B$."

Dies deckt alle 4 Fälle konsistent ab und vermeidet jede natürlichsprachliche Analogie. ✅

### Rechtfertigung 4 – Modus Ponens (Internalisierung)

Der **Modus Ponens** ist die fundamentalste Schlussregel:

$$\boxed{(MP)\;\frac{\varphi_1 \quad \varphi_1 \rightarrow \varphi_2}{\varphi_2}}$$

Forderung: Die internalisierte Formel $\heartsuit \triangleq ((\varphi_1 \wedge (\varphi_1 \rightarrow \varphi_2)) \rightarrow \varphi_2)$ soll **allgemeingültig** ($\equiv \top$) sein.

Tabellenanalyse zeigt: nur die klassische Wahrheitstabelle der Implikation erfüllt diese Forderung für alle Belegungen. ✅

### Rechtfertigung 5 – Curry-Howard / Propositions-as-Types (PaT)

| Fall | Typ-Analogie | Bewertung $[\![\varphi_1 \rightarrow \varphi_2]\!]$ |
|:--|:--|:-:|
| $A$ wahr, $B$ wahr | $f : A \to B$ existiert, $f(a)$ liefert Bewohner von $B$ | 1 ✅ |
| $A$ falsch, $B$ beliebig | Typ $A$ unbewohnt → leere Funktion existiert trivial | 1 ✅ |
| $A$ wahr, $B$ falsch | $f(a)$ müsste Bewohner von $B$ liefern – Widerspruch | 0 ✅ |

> 💡 **Merkhilfe PaT:** Beweise ↔ Programme, Aussagen ↔ Typen (Curry-Howard-Isomorphie). Eine Implikation $A \rightarrow B$ entspricht dem Funktionstyp $A \to B$.

***

## 4. Logische Äquivalenz

### Definition 6.2.1

$$\boxed{\varphi \equiv \psi \iff \forall \beta:\; [\![\varphi]\!]^\beta = [\![\psi]\!]^\beta}$$

| Begriff | Definition | Notation |
|:--|:--|:-:|
| **logisch äquivalent** | gleiche Wahrheitswerte bei jeder Belegung | $\varphi \equiv \psi$ |
| **allgemeingültig** (Tautologie) | immer wahr | $\varphi \equiv \top$ |
| **kontradiktorisch** | immer falsch | $\varphi \equiv \bot$ |
| **erfüllbar** | mindestens eine erfüllende Belegung | $\exists\beta: [\![\varphi]\!]^\beta = 1$ |

**Ohne Beweis verwendbare Äquivalenzen:**

$$p \wedge \top \equiv p,\quad p \wedge \bot \equiv \bot,\quad p \vee \bot \equiv p,\quad p \vee \top \equiv \top$$
$$p \rightarrow p \equiv \top,\quad p \leftrightarrow p \equiv \top$$

### Proposition 6.2.2 – Äquivalenzgesetze (Aussagenlogik)

| Gesetz | Formel |
|:--|:--|
| **Idempotenz** $\wedge$ | $\varphi_1 \wedge \varphi_1 \equiv \varphi_1$ |
| **Idempotenz** $\vee$ | $\varphi_1 \vee \varphi_1 \equiv \varphi_1$ |
| **Kommutativität** $\wedge$ | $\varphi_1 \wedge \varphi_2 \equiv \varphi_2 \wedge \varphi_1$ |
| **Kommutativität** $\vee$ | $\varphi_1 \vee \varphi_2 \equiv \varphi_2 \vee \varphi_1$ |
| **Assoziativität** $\wedge$ | $(\varphi_1 \wedge \varphi_2) \wedge \varphi_3 \equiv \varphi_1 \wedge (\varphi_2 \wedge \varphi_3)$ |
| **Assoziativität** $\vee$ | $(\varphi_1 \vee \varphi_2) \vee \varphi_3 \equiv \varphi_1 \vee (\varphi_2 \vee \varphi_3)$ |
| **Distributivität** $\vee$ über $\wedge$ | $(\varphi_1 \wedge \varphi_2) \vee \varphi_3 \equiv (\varphi_1 \vee \varphi_3) \wedge (\varphi_2 \vee \varphi_3)$ |
| **Distributivität** $\wedge$ über $\vee$ | $(\varphi_1 \vee \varphi_2) \wedge \varphi_3 \equiv (\varphi_1 \wedge \varphi_3) \vee (\varphi_2 \wedge \varphi_3)$ |
| **Negation** (konstruktiv) | $\neg\varphi \equiv \varphi \rightarrow \bot$ |
| **Reductio ad absurdum** | $\varphi \equiv \neg\varphi \rightarrow \bot$ |
| **Doppelte Negation** | $\neg\neg\varphi_1 \equiv \varphi_1$ |
| **Widerspruch** | $\varphi_1 \wedge \neg\varphi_1 \equiv \bot$ |
| **Tertium Non Datur** | $\varphi_1 \vee \neg\varphi_1 \equiv \top$ |
| **De Morgan I** | $\neg(\varphi_1 \wedge \varphi_2) \equiv \neg\varphi_1 \vee \neg\varphi_2$ |
| **De Morgan II** | $\neg(\varphi_1 \vee \varphi_2) \equiv \neg\varphi_1 \wedge \neg\varphi_2$ |
| **Implikation** | $\varphi_1 \rightarrow \varphi_2 \equiv \neg\varphi_1 \vee \varphi_2$ |
| **Kontraposition** | $\varphi_1 \rightarrow \varphi_2 \equiv \neg\varphi_2 \rightarrow \neg\varphi_1$ |
| **Biimplikation** | $\varphi_1 \leftrightarrow \varphi_2 \equiv (\varphi_1 \rightarrow \varphi_2) \wedge (\varphi_2 \rightarrow \varphi_1)$ |

> 💡 **Merkhilfe De Morgan:** „Negation verteilt sich und dreht den Junktor um": $\neg(\wedge) = \vee\,\neg$, $\neg(\vee) = \wedge\,\neg$.

### Proposition 6.2.3 – Äquivalenzgesetze (Prädikatenlogik)

$$\boxed{\neg(\forall x.\,\varphi) \equiv \exists x.\,\neg\varphi}$$

$$\boxed{\neg(\exists x.\,\varphi) \equiv \forall x.\,\neg\varphi}$$

> 💡 **Merkhilfe:** Negation „schiebt sich hinein" und tauscht den Quantor: $\forall \leftrightarrow \exists$.

### Beispiel – Nachweis $\neg\varphi_1 \vee \varphi_2 \equiv \varphi_1 \rightarrow \varphi_2$

| $[\![\varphi_1]\!]$ | $[\![\varphi_2]\!]$ | $[\![\neg\varphi_1 \vee \varphi_2]\!]$ | $[\![\varphi_1 \rightarrow \varphi_2]\!]$ |
|:-:|:-:|:-:|:-:|
| 0 | 0 | 1 | 1 |
| 0 | 1 | 1 | 1 |
| 1 | 0 | 0 | 0 |
| 1 | 1 | 1 | 1 |

✅ Beide Spalten identisch → $\neg\varphi_1 \vee \varphi_2 \equiv \varphi_1 \rightarrow \varphi_2$

***

## 5. Logische Äquivalenz und Beweisstrategien

### Geschenkte Regeln aus Äquivalenzen

Hat man $\varphi \equiv \psi$ bewiesen, erhält man **zwei nützliche Regeln geschenkt**:

$$(\Rrightarrow)\;\frac{\varphi}{\psi} \qquad (\Lleftarrow)\;\frac{\psi}{\varphi}$$

**Auf der Zielseite** einer Sequenz kann man äquivalent umformulieren:

$$\{\} \Rightarrow \varphi_1 \quad\leadsto\quad \{\} \Rightarrow \varphi_2 \qquad \text{(wenn } \varphi_1 \equiv \varphi_2)$$

**Auf der Annahmenseite** kann man Äquivalenzen zur Erzeugung neuer Annahmen nutzen:

$$\{\varphi_1\} \Rightarrow \psi \quad\leadsto\quad \{\varphi_1, \varphi_2\} \Rightarrow \psi \qquad \text{(wenn } \varphi_1 \equiv \varphi_2)$$

### Abgeleitete Beweisregeln (Ausblick 6.4)

#### Doppelte Negation (aus $\neg\neg\varphi \equiv \varphi$)

$$\boxed{(\neg\neg E)\;\frac{\neg\neg\varphi}{\varphi}} \qquad \boxed{(\neg\neg I)\;\frac{\varphi}{\neg\neg\varphi}}$$

#### Modus Tollens (aus Kontraposition)

$$\boxed{(MT)\;\frac{\varphi \rightarrow \psi \quad \neg\psi}{\neg\varphi}}$$

> 💡 **Rolle:** MT erlaubt, aus „wenn $A$, dann $B$" und „$B$ ist falsch" zu schließen, dass $A$ falsch ist. Entspricht der Kontraposition als Schlussregel.

#### Falsum-Elimination (gilt für alle $\varphi$)

$$\boxed{(\bot E)\;\frac{\bot}{\varphi}}$$

> 💡 **Merkhilfe:** „Aus dem Widerspruch folgt alles" (*ex falso quodlibet*). Wenn $\bot$ herleitbar ist, ist jede Formel herleitbar.

#### Beweis durch Widerspruch (aus Reductio ad absurdum: $\varphi \equiv \neg\varphi \rightarrow \bot$)

$$\boxed{(BW)\;\frac{\neg\varphi \overset{!}{\Rightarrow} \bot}{\varphi}}$$

***

## 6. Beweisbeispiel – $\sqrt{2}$ ist irrational

### Beweis durch Widerspruch (Beispiel 1.12)

**Behauptung:** $\sqrt{2}$ ist keine rationale Zahl.

**Induktionsanfang (Annahme des Gegenteils):**
- Annahme: $\sqrt{2}$ ist rational, d.h. $\exists\, m, n \in \mathbb{Z},\, n \neq 0$:

$$\sqrt{2} = \frac{m}{n} \quad \text{wobei } \gcd(m, n) = 1 \text{ (gekürzter Bruch)}$$

**Induktionsvoraussetzung (verwendetes Lemma):**
- Wenn $k^2$ gerade, dann ist $k$ gerade. (Beispiel 1.11)

**Induktionsschritt (Widerspruch herleiten):**

$$\sqrt{2} = \frac{m}{n} \;\Rightarrow\; m^2 = 2n^2$$

- $m^2$ gerade $\Rightarrow$ $m$ gerade $\Rightarrow$ $m = 2k$
- $2n^2 = (2k)^2 = 4k^2 \;\Rightarrow\; n^2 = 2k^2$
- $n^2$ gerade $\Rightarrow$ $n$ gerade
- $\Rightarrow$ $m$ und $n$ **beide gerade** – Widerspruch zu $\gcd(m,n) = 1$ $\;\bot$

**Schluss:** Annahme falsch $\Rightarrow$ $\sqrt{2} \notin \mathbb{Q}$. $\square$

***

## 📌 Zusammenfassung

### Wichtige Konzepte

| Konzept | Bedeutung |
|:--|:--|
| **$\mathbf{A}(V)$** | Menge aller aussagenlogischen Formeln über $V$, induktiv definiert |
| **Variablenbelegung $\beta$** | Funktion $V \to \{0,1\}$; bei $n$ Variablen gibt es $2^n$ Belegungen |
| **Auswertung $[\![\cdot]\!]^\beta$** | Wertet Formel unter $\beta$ zu 0 oder 1 aus |
| **Materiale Implikation** | $[\![\varphi_1 \rightarrow \varphi_2]\!] = 1 \iff [\![\varphi_1]\!] \leq [\![\varphi_2]\!]$ |
| **Logische Äquivalenz $\equiv$** | Gleichheit der Auswertung für **alle** Belegungen |
| **Allgemeingültig (Tautologie)** | $\varphi \equiv \top$ |
| **Kontradiktorisch** | $\varphi \equiv \bot$ |
| **Erfüllbar** | mind. eine Belegung mit Wert 1 |
| **Modus Ponens (MP)** | $\frac{\varphi \quad \varphi \rightarrow \psi}{\psi}$ – Quintessenz des natürlichen Schließens |
| **Modus Tollens (MT)** | $\frac{\varphi \rightarrow \psi \quad \neg\psi}{\neg\varphi}$ – folgt aus Kontraposition |
| **Beweis per Widerspruch (BW)** | Annahme $\neg\varphi$ führt zu $\bot$ $\Rightarrow$ $\varphi$ gilt |
| **Curry-Howard-Isomorphie (PaT)** | Aussagen $\leftrightarrow$ Typen, Beweise $\leftrightarrow$ Programme |

### Kernaussagen

✅ **Die Implikation $\varphi_1 \rightarrow \varphi_2$ ist falsch genau dann, wenn die Prämisse wahr und die Konklusion falsch ist** – der einzige „Lügenfall".

✅ **$[\![\varphi_1 \rightarrow \varphi_2]\!] = 1 \iff [\![\varphi_1]\!] \leq [\![\varphi_2]\!]$** – die algebraisch sauberste Rechtfertigung.

✅ **Allgemeingültigkeit des Modus Ponens** erzwingt eindeutig die klassische Wahrheitstabelle der Implikation.

⚠️ **Achtung:** „Wenn $A$, dann $B$" in natürlicher Sprache suggeriert Kausalität – die Aussagenlogik bewertet **nur Wahrheitswerte**, keinen inhaltlichen Zusammenhang.

❌ **Falsch:** „Eine Implikation mit falscher Prämisse ist sinnlos" – sie ist per Definition **wahr** und essentiell für konsistente Logik.

### Wichtige Äquivalenzen als Referenz

| Name | Formel |
|:--|:--|
| **Implikation** | $\varphi_1 \rightarrow \varphi_2 \equiv \neg\varphi_1 \vee \varphi_2$ |
| **Kontraposition** | $\varphi_1 \rightarrow \varphi_2 \equiv \neg\varphi_2 \rightarrow \neg\varphi_1$ |
| **De Morgan I** | $\neg(\varphi_1 \wedge \varphi_2) \equiv \neg\varphi_1 \vee \neg\varphi_2$ |
| **De Morgan II** | $\neg(\varphi_1 \vee \varphi_2) \equiv \neg\varphi_1 \wedge \neg\varphi_2$ |
| **Tertium Non Datur** | $\varphi \vee \neg\varphi \equiv \top$ |
| **Reductio ad absurdum** | $\varphi \equiv \neg\varphi \rightarrow \bot$ |
| **Doppelte Negation** | $\neg\neg\varphi \equiv \varphi$ |
| **Neg. Allquantor** | $\neg(\forall x.\,\varphi) \equiv \exists x.\,\neg\varphi$ |
| **Neg. Existenzquantor** | $\neg(\exists x.\,\varphi) \equiv \forall x.\,\neg\varphi$ |

***

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.01-FoG – Natürliches Schließen I]]: Grundlegende Beweisregeln ($\wedge$I/E, $\vee$I/E, →I/E); bilden Basis für die ableitbaren Regeln in VL.05
- [[VL.04 Natürliches Schließen II]]: Negationsregeln und Einführung des Falsum $\bot$; direkte Vorstufe zu BW und $\bot$E
- [[VL.04-FoG – Prädikatenlogik]]: Quantoren $\forall$, $\exists$; Prop. 6.2.3 knüpft direkt an VL.04 an
- [[VL.01 Mengen und Logik]]: Wahrheitstafeln und Implikation „bekannt aus Ana1/LinA" – Brücke zur Mathematik-Ausbildung  
