**Class:** [[FoG - Formal-mathematische Grundlagen]]
**Date:** 21-04-2026
**Topics:** #Inferenzregeln #Ableitungsbäume #PatternMatching #InduktiveDefinitionen #Logik #Aussagenlogik #Prädikatenlogik
**Link:** [[VL.02 FoG Skript-12-19.pdf]]

---

## 🎯 Lernziele der Vorlesung

Inferenzregeln sind das zentrale Werkzeug zur regelbasierten Definition und Ableitung von Mengen und Fakten.

- **Inferenzregeln** als Wenn-dann-Aussagen; Axiome, Prämissen, Konklusion
- **Ableitungsbäume** durch Komposition von Regeln
- **Regelschemata** und Metavariablen
- **Pattern Matching** zur Zugehörigkeitsprüfung
- **Induktive Definitionen** und Minimalitätsforderung
- **Syntax der Aussagenlogik** als induktiv definierte Menge
- **Syntax der Prädikatenlogik**, Quantoren, Scope, freie und gebundene Variablen

---

## 2. Inferenzregeln

Inferenzregeln stellen ein **definitorisches Prinzip** dar: aus angenommenen Fakten können regelbasiert weitere Fakten abgeleitet werden — potenziell unendlich viele, mit lediglich endlich vielen Regeln.

Die regelbasierte Vorgehensweise ist für IT von zentraler Bedeutung.

Inferenzregeln werden verwendet für:

- **Induktive Definition** von Mengen (§2.2)
- **Dekonstruktion**: entscheidbares Verfahren zur Überprüfung von Zugehörigkeit
- **Natürliches Schließen** (Teil II)
- **Operationale Ableitungsketten und -bäume**

---

## 2.1 Regeln und Ableitungen

### Definition (Inferenzregel)

Eine Inferenzregel ist eine **Wenn-dann-Aussage**:

> Wenn endlich viele Annahmen (**Prämissen**) gelten, dann kann man bestimmte Schlüsse (**Konklusion**) ziehen.

Regeln ohne Prämissen heißen **Axiome**.

Prämissen und Konklusion sind typischerweise textuelle Objekte — Ausdrücke, Terme oder Formeln.

### Schreibweisen

**Zweidimensional (Standard):**

$$
\text{(Regelname)} \quad \frac{\text{Präm}_1 \quad \text{Präm}_2 \quad \cdots \quad \text{Präm}_n}{\text{Konkl}}
$$

**Eindimensional:**

$$
\text{Präm}_1, \text{Präm}_2, \ldots, \text{Präm}_n \vdash \text{Konkl}
$$

**Schrittweise (rechtsassoziativ, wenn Reihenfolge wichtig):**

$$
[\text{Präm}_1; \text{Präm}_2; \ldots; \text{Präm}_n] \Rightarrow \text{Konkl}
$$

$$
\text{Präm}_1 \Rightarrow (\text{Präm}_2 \Rightarrow (\cdots(\text{Präm}_n \Rightarrow \text{Konkl})\cdots))
$$

### Use Cases

Regeln können in zwei Richtungen gelesen werden:

- **Vorwärts**: Ausgehend von existierenden Prämissen — welche weiteren Fakten lassen sich ableiten?
- **Rückwärts**: Ausgehend von einer gewünschten Konklusion — welche Prämissen müsste man voraussetzen?

### Ableitungsbäume

Wenn die Prämissen einer Regel mit den Konklusionen anderer Regeln übereinstimmen, können Regeln zu einem **Ableitungsbaum** zusammengesetzt werden.

Beispiel — gegebene Regeln:

$$
\frac{x \quad y \quad z}{k} \qquad \frac{u \quad w \quad e}{x} \qquad \frac{f \quad o \quad g}{z}
$$

Zusammengesetzter Ableitungsbaum von $k$ aus $u, w, e, y, f, o, g$:

$$
\frac{\dfrac{u \quad w \quad e}{x} \quad y \quad \dfrac{f \quad o \quad g}{z}}{k}
$$

### Regelschemata

Regeln werden durch **Metavariablen** schematisch beschrieben. Beim Benutzen muss jede Metavariable **konsistent** ersetzt werden. Das Ergebnis heißt **Instanz** des Regelschemas.

Beispiele:

$$
(S1)\;\frac{A}{B} \qquad (S2)\;\frac{A \quad \neg A}{B} \qquad (S3)\;\frac{A \land B}{A \lor B}
$$

- $A$ und $B$ sind Metavariablen.
- $(S3)$ erzwingt eine inhaltliche Verbindung zwischen Prämisse und Konklusion.

### Pattern Matching

Beim Prüfen, ob ein Ausdruck zu einer induktiv definierten Menge gehört, wird die Konklusion einer Regel mit dem Ausdruck **abgeglichen**. Das nennt man **Pattern Matching**.

Beispiel — natürliche Zahlen als Regeln:

$$
\frac{}{0 \in \mathbb{N}} \qquad \frac{n \in \mathbb{N}}{n+1 \in \mathbb{N}}
$$

Frage: Gilt $m = (0+1)+1 \in \mathbb{N}$?

Abgleich mit Konklusion $n+1 \in \mathbb{N}$ ergibt: $n \triangleq (0+1)$.

Ableitungsbaum:

$$
\frac{\dfrac{\dfrac{}{0 \in \mathbb{N}}}{0+1 \in \mathbb{N}}}{(0+1)+1 \in \mathbb{N}}
$$

Für jede natürliche Zahl $x \in \mathbb{N}$ genügen $x+1$ Regelanwendungen.

---

## 2.2 Induktive Definitionen

Die Menge $\mathbb{N}$ ist ein Beispiel für eine **induktive Definition durch Inferenzregeln**. Dies lässt sich verallgemeinern.

### Aufbau einer induktiven Definition

- Prämissen und Konklusion haben alle dieselbe Form: $\text{Ausdruck} \in \text{Mengenbezeichner}$
- **Basisfälle** (Axiome): keine Prämissen — Elemente werden direkt deklariert
- **Konstruktionen**: aus bereits zugehörigen Elementen werden weitere konstruiert

### Minimalitätsforderung

Gemeint ist stets die **kleinste Menge**, deren Elemente sich ohne weitere Annahmen mit den Regeln herleiten lassen.

Das bedeutet:

- Alle Elemente sind durch Regelanwendung konstruiert.
- Die Zugehörigkeit kann mechanisch durch **Rückwärtsanwendung** geprüft werden.
- Für die Dekonstruktion ist entscheidend, dass der **äußerste Konstruktor** eindeutig erkennbar ist.

---

## 2.3 Beispiel: Logische Formeln

Dieses Beispiel illustriert den Unterschied zwischen **Syntax** (Form/Zeichen) und **Semantik** (Bedeutung).

### 2.3.1 Notation (Junktoren und Quantoren)

Logische Konnektive als symbolische Abkürzungen:

| Symbol | Name | Bedeutung |
|--------|------|----------|
| $\top$ | Verum | „wahr" |
| $\bot$ | Falsum | „falsch" |
| $\neg$ | Negation | „nicht" |
| $\land$ | Konjunktion | „und" |
| $\lor$ | Disjunktion | „oder" |
| $\rightarrow$ | Implikation | „impliziert" |
| $\leftrightarrow$ | Biimplikation | „genau dann, wenn" |
| $\forall$ | Universelle Quantifikation | „für alle" |
| $\exists$ | Existentielle Quantifikation | „es gibt" |

⚠️ „oder" ist in natürlicher Sprache mehrdeutig. Ebenso werden „wenn…dann…"-Aussagen oft als Biimplikation interpretiert — formal sind sie Implikationen.

### 2.3.2 Definition (Syntax der Aussagenlogik)

Sei $V$ eine Menge von aussagenlogischen Variablen mit $V \cap \{\top, \bot, \neg, \land, \lor, \rightarrow, \leftrightarrow, (, )\} = \emptyset$.

Die Menge $\mathbf{A}(V)$ der aussagenlogischen Formeln ist die **kleinste** Menge, definiert durch:

$$
\frac{}{\varphi \in \mathbf{A}(V)} \quad \text{für } \varphi \in V \cup \{\top, \bot\}
$$

$$
\frac{\varphi \in \mathbf{A}(V)}{\neg\varphi \in \mathbf{A}(V)}
$$

$$
\frac{\varphi_1 \in \mathbf{A}(V) \qquad \varphi_2 \in \mathbf{A}(V)}{(\varphi_1 \land \varphi_2) \in \mathbf{A}(V)}
\qquad
\frac{\varphi_1 \in \mathbf{A}(V) \qquad \varphi_2 \in \mathbf{A}(V)}{(\varphi_1 \lor \varphi_2) \in \mathbf{A}(V)}
$$

$$
\frac{\varphi_1 \in \mathbf{A}(V) \qquad \varphi_2 \in \mathbf{A}(V)}{(\varphi_1 \rightarrow \varphi_2) \in \mathbf{A}(V)}
\qquad
\frac{\varphi_1 \in \mathbf{A}(V) \qquad \varphi_2 \in \mathbf{A}(V)}{(\varphi_1 \leftrightarrow \varphi_2) \in \mathbf{A}(V)}
$$

Metavariablen: $p, q, \ldots$ für Elemente von $V$; $\varphi, \psi, \ldots$ für Elemente von $\mathbf{A}(V)$.

**Klassen von Formeln:**

| Klasse | Beschreibung |
|--------|-------------|
| **Aussagen** | keine aussagenlogischen Variablen |
| **Aussagenschemata** | mit aussagenlogischen Variablen |
| **atomar** | nur ein Element aus $V \cup \{\top, \bot\}$ |
| **zusammengesetzt** | alle anderen |
| **trivial** | höchstens eine Variable, höchstens ein weiterer Operator |

### 2.3.3 Notation (Operatorvorrang)

Zur besseren Lesbarkeit können Klammern entfallen. Es gilt:

$$
\neg \quad > \quad \land \quad > \quad \lor \quad > \quad \rightarrow \quad > \quad \leftrightarrow
$$

- $\rightarrow$ ist **rechtsassoziativ**
- Außenklammern dürfen weggelassen werden
- Syntaktisch korrekte Formeln beinhalten dennoch alle Klammern

### 2.3.4 Notation (Prädikate)

In der **Prädikatenlogik** werden aussagenlogische Variablen durch **Prädikate** in $Pr(X)$ ersetzt, parametrisiert über eine Menge $X$ von Termvariablen.

Typische Form: $r(t_1, \ldots, t_n)$ mit $n \in \mathbb{N}^+$, wobei:

- $r \in S_{rel}$: Relationssymbol (üblicherweise enthält $S_{rel}$ das Gleichheitszeichen $=$)
- $t_i$: Terme aus Variablen in $X$ und Funktionssymbolen $S_{fun}$

### 2.3.5 Definition (Syntax der Prädikatenlogik)

Sei $X$ eine Menge von Termvariablen, $Pr(X)$ eine Menge von Prädikaten über $X$.

Die Menge $\mathbf{P}(X)$ der prädikatenlogischen Formeln ist die **kleinste** Menge, definiert durch:

$$
\frac{}{\varphi \in \mathbf{P}(X)} \quad \text{für } \varphi \in Pr(X) \cup \{\top, \bot\}
$$

$$
\frac{\varphi \in \mathbf{P}(X)}{\neg\varphi \in \mathbf{P}(X)}
$$

$$
\frac{\varphi_1 \in \mathbf{P}(X) \qquad \varphi_2 \in \mathbf{P}(X)}{(\varphi_1 \land \varphi_2) \in \mathbf{P}(X)}
\qquad
\frac{\varphi_1 \in \mathbf{P}(X) \qquad \varphi_2 \in \mathbf{P}(X)}{(\varphi_1 \lor \varphi_2) \in \mathbf{P}(X)}
$$

$$
\frac{\varphi_1 \in \mathbf{P}(X) \qquad \varphi_2 \in \mathbf{P}(X)}{(\varphi_1 \rightarrow \varphi_2) \in \mathbf{P}(X)}
\qquad
\frac{\varphi_1 \in \mathbf{P}(X) \qquad \varphi_2 \in \mathbf{P}(X)}{(\varphi_1 \leftrightarrow \varphi_2) \in \mathbf{P}(X)}
$$

$$
\frac{\varphi \in \mathbf{P}(X)}{(\forall x.\,\varphi) \in \mathbf{P}(X)} \quad x \in X
\qquad
\frac{\varphi \in \mathbf{P}(X)}{(\exists x.\,\varphi) \in \mathbf{P}(X)} \quad x \in X
$$

Abkürzung: $(\nexists x.\,\varphi) \triangleq \neg(\exists x.\,\varphi)$

### 2.3.6 Notation (Quantoren und Klammerung)

Operatorvorrang aus 2.3.3 gilt weiterhin. Zusätzlich:

- $\forall$ und $\exists$ binden **gleich stark**
- $\forall$ und $\exists$ binden **schwächer** als alle anderen Konnektive

### 2.3.7 Definition (Quantoren und Variablen)

Sei $Q \in \{\forall, \exists\}$, $x \in X$ und $\varphi \in \mathbf{P}(X)$.

1. In $(Qx.\,\varphi)$ bezeichnet $\varphi$ den **Scope** (Gültigkeitsbereich) von $Qx$.
2. Eine Variable $z$ in einer Formel $\psi$ heißt **frei**, wenn sie nicht im Scope eines $Qz$ liegt.
3. Eine Variable $z$ in einer Formel $\psi$ heißt **gebunden**, wenn sie im Scope eines $Qz$ vorkommt.
4. $Qx$ bindet alle freien Vorkommen von $x$ in $\varphi$.

Formeln mit freien Variablen $\vec{x}$ werden notiert als $\varphi(\vec{x})$.

### 2.3.8 Definition (Alpha-Konversion)

Sei $Q \in \{\forall, \exists\}$, $x \in X$, $\varphi \in \mathbf{P}(X)$.

1. Sei $z$ eine Variable, die nicht gebunden in $\varphi$ vorkommt. Dann bezeichnet $\varphi_{x \mapsto z}$ die Umbenennung aller freien Vorkommen von $x$ in $z$.
2. Die Formeln $(Qx.\,\varphi)$ und $(Qz.\,\varphi_{x \mapsto z})$ heißen **$\alpha$-konvertibel**.
3. Zwei Formeln heißen **$\alpha$-gleich** ($\varphi =_\alpha \psi$), wenn sie durch endlich viele $\alpha$-Konvertierungen ineinander überführt werden können.

⚠️ Um Missverständnisse durch verschachtelte Bindung zu vermeiden: nach Möglichkeit immer **paarweise verschiedene Variablen** in Quantoren verwenden.

### 2.3.9 Definition (Substitution)

Seien $x \in X$, $\varphi \in \mathbf{P}(X)$, $t$ ein Term. Dann bezeichnet $\varphi\left[\tfrac{t}{x}\right]$ die Formel, die durch Ersetzung aller **freien** Vorkommen von $x$ durch $t$ entsteht.

Kurznotation: $\varphi(t)$ für $\varphi(x)\left[\tfrac{t}{x}\right]$.

⚠️ Enthält $t$ Variablen, die in $\varphi$ gebunden vorkommen, muss $\varphi$ vorher $\alpha$-konvertiert werden, um neue Bindungen zu vermeiden.

### 2.3.10 Definition (Beschränkte Quantoren)

Quantoren werden häufig in beschränkter Form verwendet:

$$
(\forall x \in A.\,\varphi) \;\triangleq\; (\forall x.\, x \in A \rightarrow \varphi)
$$

$$
(\exists x \in A.\,\varphi) \;\triangleq\; (\exists x.\, x \in A \land \varphi)
$$

### 2.3.11 Notation (Eindeutigkeit)

„Es gibt genau ein $e$, für das $\varphi(e)$ gilt":

$$
\exists! e.\,\varphi(e) \;\triangleq\; \Bigl(\exists z.\,(\varphi(z))\Bigr) \land \Bigl(\forall x, y.\,(x \neq y) \rightarrow \neg(\varphi(x) \land \varphi(y))\Bigr)
$$

---

## 📌 Zusammenfassung

### Kernbegriffe

| Begriff | Bedeutung |
|--------|----------|
| **Inferenzregel** | Wenn-dann-Aussage; Prämissen $\Rightarrow$ Konklusion |
| **Axiom** | Regel ohne Prämissen |
| **Ableitungsbaum** | Komposition von Regeln |
| **Regelschema** | Regel mit Metavariablen |
| **Instanz** | Konkrete Ersetzung der Metavariablen |
| **Pattern Matching** | Abgleich eines Ausdrucks mit der Konklusion einer Regel |
| **Kleinste Menge** | Minimalitätsforderung induktiver Definitionen |
| **Scope** | Gültigkeitsbereich eines Quantors |
| **Freie Variable** | Variable außerhalb eines Quantorscopes |
| **Gebundene Variable** | Variable innerhalb eines Quantorscopes |
| **$\alpha$-Konversion** | Umbenennung gebundener Variablen |
| **Substitution** | Ersetzung freier Vorkommen einer Variable durch einen Term |

### Kernaussagen

✅ Inferenzregeln erlauben mit endlich vielen Regeln unendlich große Mengen zu definieren.

✅ Die **Minimalitätsforderung** sichert, dass Zugehörigkeit mechanisch überprüfbar ist.

✅ Aussagen- und Prädikatenlogik werden als **induktiv definierte syntaktische Mengen** beschrieben.

✅ Freie Variablen können substituiert werden; gebundene Variablen können $\alpha$-konvertiert werden.

✅ Syntax und Semantik werden klar getrennt — dieser Abschnitt behandelt nur Syntax.

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.01 Mengen]]: Mengen und induktive Definitionen (§1.2) als Vorstufe
- [[VL.04 Natürliches Schließen II]]: Natürliches Schließen (Teil II) — baut direkt auf Inferenzregeln auf
- [[VL.06 Relationen]]: Relationen und Relationssymbole $S_{rel}$
- [[VL.07 Abbildunge Funktionen & Kardinalität]]: Funktionen und Funktionssymbole $S_{fun}$
- [[VL.05 Natürliches Schließen III]]: Strukturelle Induktion — Verallgemeinerung des Prinzips aus §2.2
