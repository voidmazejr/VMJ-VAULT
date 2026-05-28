**Class:** [[FoG - Formal-mathematische Grundlagen]]
**Date:** 14-04-2026
**Topics:** #Gleichheit #Mengen #Extensionalität #InduktiveDefinition #Intensionalität #Algebra #Potenzmenge #RussellParadox
**Link:** [[VL.01 FoG Skript-8-11.pdf]]

---

## 🎯 Lernziele der Vorlesung

FoG führt formal-mathematische und logische Grundlagen der Informatik ein, mit besonderem Fokus auf Beweiskompetenzen.

- Unterschied zwischen **definierender**, **konstatierender** und **Äquivalenz**-Gleichheit
- **Extensionale**, **induktive**, **intensionale** und **algebraische** Mengendefinitionen
- **Vergleich** von Mengen: Teilmengen, Gleichheit, echte Teilmengen
- **Algebra der Mengen**: Vereinigung, Schnitt, Differenz, kartesisches Produkt
- **Potenzmenge** und ihre Größe

---
### 0.1 Kompetenzziele

Absolventinnen und Absolventen dieses Moduls:

- beherrschen einen Grundstock an **formal-mathematischen und logischen Grundlagen** der Informatik
- haben eine substanzielle **Beweiskompetenz** erworben: sie können die formale Korrektheit von Argumentationsmustern auf Basis von Aussagen- und Prädikatenlogik bewerten
- können eigenständig **strukturiert und logisch korrekt argumentieren**
- können durch **Abstraktion** von konkreten auf allgemeine Sachverhalte wechseln — und zurück
- sind sich der unterschiedlichen Ebenen von **Objekt- und Metasprache** bewusst
- können Aufgaben sowohl selbständig (auch rechnergestützt) als auch in **Kleingruppen** bearbeiten

### 0.2 Mathematische Grundlagen Ana1/LinA

| Thema | FoG-Abschnitt | Erweiterung gegenüber Ana1/LinA |
|-------|-------------|--------------------------------|
| Mengenlehre | §1, §10.1 | Potenzmenge; Erweiterung durch Funktionen |
| Zahlenräume | §1 | bekannt, wird formalisiert |
| Aussagen- und Prädikatenlogik | §2.3, §6.2 | deutlich formaler; Semantik der Aussagenlogik formalisiert |
| Vollständige Induktion | §13 | Formalisierung und Verallgemeinerung |
| Abbildungen | §7, §8, §8.3 | als Spezialisierung von Relationen; Kardinalitäten; $\lambda$-Notation |

### 0.3 Gleichheit(en)

Das generische Symbol „$=$" wird in der Mathematik für unterschiedliche Zwecke verwendet. FoG unterscheidet explizit:

| Symbol | Art | Bedeutung |
|--------|-----|----------|
| $\triangleq$ | **definierend** | $\text{Bez} \triangleq \text{Ausdruck}$: Bezeichner darf metasprachlich durch Ausdruck ersetzt werden — *per Definition dasselbe Objekt* |
| $=$ | **konstatierend** | eine bestehende Gleichheit wird festgestellt |
| $\equiv$ | **Äquivalenz** | semantische Gleichwertigkeit (z.B. logische Formeln in §6.2) |

**gdw** = Abkürzung für „genau dann, wenn" (konstatierend oder definierend verwendbar).

**Syntax vs. Semantik am Beispiel Brüche:**

$\frac{2}{3}$ und $\frac{4}{6}$ sind syntaktisch **verschieden** ($\neq$), aber semantisch **äquivalent** — sie bezeichnen dieselbe rationale Zahl.

$$\mathbb{Q} \triangleq \text{Äquivalenzklassen von Brüchen bzgl. Kürzbarkeit}$$

Ebenso: $0{,}\overline{9}$ und $1{,}0$ sind syntaktisch verschieden, bezeichnen aber dieselbe reelle Zahl. Dies ist ein weiteres Beispiel für Syntax vs. Semantik.

**Umgangssprachliche Merkhilfe:** *das Gleiche* und *dasselbe* werden auch in der natürlichen Sprache unterschiedlich benutzt, obwohl beide den Charakter einer Gleichheit besitzen.

---

## Teil I: Beschreiben

## 1. Mengen

Eine **Menge** ist eine Zusammenfassung von eindeutig unterscheidbaren Objekten.

$$a \in A \quad \text{„Objekt } a \text{ ist Element der Menge } A\text{"}$$

Metavariablen für Mengen: $A, B, C, \ldots$ (ggf. mit Indizes).
Standardmengen: $\mathbb{N}, \mathbb{N}^+, \mathbb{Z}, \mathbb{Q}, \mathbb{R}$ — eigener Schriftsatz.

---

### 1.1 Extensionalität

**Notation 1.1.1 (Beschreibungsformen 1: Extensionale Definition)**

Eine endliche Menge als explizite Aufzählung:

$$A \triangleq \{a_1, a_2, a_3\}$$

- Reihenfolge spielt keine Rolle
- Dopplungen werden ignoriert
- Leere Menge: $\emptyset \triangleq \{\}$

⚠️ Die Verwendung von „$\ldots$" in extensionalen Definitionen ist zu **vermeiden**, da nicht immer eindeutig interpretierbar.

**Definition 1.1.2 (Zahlenmengen)**

- $\mathbb{N}$: natürliche Zahlen inkl. $0$
- $\mathbb{N}^+$: natürliche Zahlen exkl. $0$
- $\mathbb{Z}$: ganze Zahlen
- $\mathbb{Q}$: rationale Zahlen
- $\mathbb{R}$: reelle Zahlen

**Definition 1.1.3 (Größe von Mengen)**

Sei $A$ eine beliebige Menge. Dann bezeichnet $\#(A)$ (auch $|A|$) die Anzahl der Elemente:

$$\#(A) \in \mathbb{N} \quad \text{oder} \quad \#(A) = \infty$$

---

### 1.2 Induktion

**Notation 1.2.1 (Beschreibungsformen 2: Induktive Definition)**

Unendliche Mengen können durch **endlich viele Regeln** induktiv definiert werden.

**Beispiel: $\mathbb{N}$**

$$\textbf{Basis:} \quad 0 \in \mathbb{N}$$

$$\textbf{Konstruktion:} \quad n \in \mathbb{N} \;\Rightarrow\; n+1 \in \mathbb{N}$$

$\mathbb{N}$ besteht aus **genau** den Elementen, die sich durch diese Regeln herleiten lassen — alle solchen, aber keine anderen.

**Allgemeine Form (Definition durch strukturelle Induktion):**

$$\textbf{Basis:} \quad B \subseteq M$$

Dazu kommen endlich viele **Konstruktionsregeln**, die aus bereits enthaltenen Elementen neue erzeugen. Definition 2.3.2 liefert ein typisches Beispiel.

---

### 1.3 Vergleich

**Definition 1.3.1 (Teilmengen, Gleichheit von Mengen)**

Seien $A$ und $B$ zwei beliebige Mengen:

$$A \subseteq B \;\triangleq\; \forall x \in A:\; x \in B \qquad \text{($A$ ist Teilmenge von $B$)}$$

$$A = B \;\triangleq\; A \subseteq B \;\land\; B \subseteq A$$

$$A \neq B \;\triangleq\; \neg(A = B)$$

$$A \subset B \;\triangleq\; A \subseteq B \;\land\; A \neq B \qquad \text{($A$ ist echte Teilmenge von $B$)}$$

Wenn $A$ (echte) Teilmenge von $B$, dann heißt $B$ **(echte) Obermenge** von $A$.

⚠️ $\in$ setzt Objekte auf **unterschiedlichen** Hierarchieebenen in Beziehung; $\subseteq$ setzt Objekte auf **gleicher** Ebene in Beziehung. Beide Symbole werden häufig verwechselt!

Es gilt für jede beliebige Menge $A$: $\emptyset \subseteq A$ — und als Spezialfall: $\emptyset \subseteq \emptyset$.

---

### 1.4 Intensionalität

**Notation 1.4.1 (Beschreibungsformen 3: Intensionale Definition)**

$$\{ x \in B \mid P(x) \} \qquad \text{bzw.} \qquad \{ x \mid P(x) \}$$

Definiert die Menge aller $x$ (aus $B$), die das Prädikat $P$ erfüllen.
$\mid$ liest sich als „so dass". Angabe von $B$ kann entfallen, wird aber empfohlen.
$P(x)$ kann umgangssprachlich oder als logische Formel (§2.3) angegeben werden.

Dieser Mechanismus heißt auch **Komprehension** — ein Prädikat dient als „Filter" für Elemente aus $B$.

⚠️ Nur gültig, wenn $P(x)$ für jedes $x$ eindeutig **wahr** oder **falsch** ist.

**Bemerkung 1.4.2 (Russell'sches Paradox)**

$$\{ x \mid x \notin x \} \quad \text{ist \textbf{keine} Menge!}$$

Begründung: Es bedürfte einer zirkulären Hierarchie von Mengen, um diese „Menge" zu definieren.

**Definition 1.4.3 (Zahlenmengen als Intervalle)**

$$[m, n] \;\triangleq\; \{ i \in \mathbb{Z} \mid m \leq i \leq n \} \quad \text{für } m, n \in \mathbb{Z}$$

$$[n] \;\triangleq\; [0,\, n-1]$$

$$\mathbf{n} \;\triangleq\; [n]$$

Beispiele: $\mathbf{0} = \emptyset$ und $\mathbf{2} = \{0, 1\}$

⚠️ Diese Intervall-Notation ist **nicht** zu verwechseln mit der aus Ana1/LinA bekannten Intervall-Notation auf reellen Zahlen. In FoG wird Letztere nicht verwendet.

**Proposition 1.4.4 (Mengen und Elemente)**

1. Für beliebige Prädikate $P$ gilt: $\{ y \mid P(y) \} = \{ x \mid P(x) \}$
2. Für beliebige Mengen $A$ gilt: $A = \{ x \mid x \in A \}$
3. Für beliebige Prädikate $P$, Mengen $A$, Objekte $x \in A$ gilt:
   $P(x)$ ist wahr $\;\text{gdw}\;$ $x \in \{ y \in A \mid P(y) \}$

---

### 1.5 Rechnen mit und auf Mengen: „Algebra"

**Definition 1.5.1 (Beschreibungsformen 4: Algebraische Definition)**

Seien $A$ und $B$ beliebige Mengen:

$$A \cup B \;\triangleq\; \{ x \mid x \in A \;\text{oder}\; x \in B \} \qquad \text{(Vereinigung)}$$

$$A \cap B \;\triangleq\; \{ x \mid x \in A \;\text{und}\; x \in B \} \qquad \text{(Schnitt)}$$

$$B \setminus A \;\triangleq\; \{ x \mid x \in B \;\text{und}\; x \notin A \} \qquad \text{(Differenz / Komplement)}$$

$$A \times B \;\triangleq\; \{ (a, b) \mid a \in A \;\text{und}\; b \in B \} \qquad \text{(kartesisches Produkt)}$$

**Definition 1.5.2 (Potenzmenge)**

$$\mathcal{P}(A) \;\triangleq\; \{ B \mid B \subseteq A \}$$

Alternativ: $2^A \triangleq \mathcal{P}(A)$

**Proposition 1.5.3**

$$\#(\mathcal{P}(A)) = \begin{cases} 2^{\#(A)} & \text{falls } \#(A) < \infty \\ \infty & \text{falls } \#(A) = \infty \end{cases}$$

💡 Empfehlung aus dem Skript: $\mathcal{P}(\mathcal{P}(\mathcal{P}(\mathcal{P}(\emptyset))))$ schrittweise berechnen, um ein gutes Verständnis von Potenzmengen zu entwickeln.

---

## 📌 Zusammenfassung

### Vier Beschreibungsformen für Mengen

| Form | Notation | Wann sinnvoll |
|------|---------|--------------|
| **Extensional** | $\{a_1, a_2, a_3\}$ | endliche Mengen |
| **Induktiv** | Basis + Konstruktionsregeln | unendliche Mengen mit endlich vielen Regeln |
| **Intensional** | $\{x \mid P(x)\}$ | wenn Eigenschaft klar formulierbar und entscheidbar |
| **Algebraisch** | $A \cup B$, $A \cap B$, $A \times B$, … | Kombination bekannter Mengen |

### Wichtige Formeln

| Begriff | Formal |
|--------|--------|
| **Teilmenge** | $A \subseteq B \;\triangleq\; \forall x \in A: x \in B$ |
| **Gleichheit** | $A = B \;\triangleq\; A \subseteq B \land B \subseteq A$ |
| **Potenzmenge** | $\mathcal{P}(A) \triangleq \{B \mid B \subseteq A\}$, $\quad \#(\mathcal{P}(A)) = 2^{\#(A)}$ |
| **Intervall (FoG)** | $[m,n] \triangleq \{i \in \mathbb{Z} \mid m \leq i \leq n\}$ |

### Kernaussagen

✅ FoG unterscheidet strikt: $\triangleq$ (definierend), $=$ (konstatierend), $\equiv$ (Äquivalenz).

✅ Mengen werden durch strukturelle Induktion mit endlich vielen Regeln potenziell unendlich groß.

✅ Intensionale Definitionen sind nur sinnvoll, wenn $P(x)$ für jedes $x$ entscheidbar ist.

✅ Russells Paradox zeigt: $\{x \mid x \notin x\}$ ist **keine** Menge — zirkuläre Hierarchie nicht erlaubt.

✅ Die Potenzmenge von $A$ hat $2^{\#(A)}$ Elemente (für endliches $A$).

✅ $\in$ und $\subseteq$ operieren auf **verschiedenen** Hierarchieebenen — nicht verwechseln!

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Inferenz und Regelschemata]]: Inferenzregeln bauen direkt auf induktiven Definitionen aus §1.2 auf
- [[FoG §6.2]]: Semantik der Aussagenlogik formalisiert den Begriff der Äquivalenz aus §0.3
- [[FoG §9.2]]: Äquivalenzrelationen formalisieren den abstrakten Begriff der Äquivalenz
- [[FoG §10.1]]: Funktionen erweitern die Möglichkeiten zur Mengenbeschreibung
- [[FoG §13]]: Strukturelle Induktion verallgemeinert das Prinzip aus §1.2
- [[DS]]: Mengenlehre als Grundlage für Graphen und kombinatorische Strukturen
- [[AlgoDat]]: Mengen als Datenstrukturen (Sets, Maps, Filter)
