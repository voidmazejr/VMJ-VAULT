**Class:** [[ISDA - Informationsysteme und Datenanalyse]]  
**Date:** 27-05-2026  
**Topics:** #RelationaleAlgebra #Datenbanken #Anfragesprache #ISDA  
**Link:** [[VL.07 ISDA.pdf]]

---

## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt die relationale Algebra als theoretische Grundlage für Datenbankanfragen ein und zeigt, wie komplexe Abfragen systematisch aufgebaut werden.

- **Basisoperatoren**: Selektion, Projektion, Vereinigung, Differenz, Kartesisches Produkt, Umbenennung ($\sigma, \pi, \cup, -, \times, \rho$)
- **Abgeleitete Operatoren**: Schnitt, natürlicher Join, Theta-Join, Division — ausdrückbar durch Basisoperatoren
- **Komplexe Ausdrücke**: Schachtelung und Baumdarstellung von Operatorfolgen
- **Erweiterte Operatoren**: Aggregation ($\gamma$), Sortierung ($\tau$), Erweiterte Projektion
- **Eigenschaften der Algebra**: Abgeschlossenheit, Vollständigkeit, Unabhängigkeit der Basisoperatoren
- **Anhang**: Duplikateneliminierung ($\delta$), Outer Joins, Outer Union, Semi-Join

---

## 1. Einführung & Grundbegriffe

### Motivation

Die relationale Algebra behandelt Relationen wie Mengen und berechnet daraus **virtuelle (abgeleitete) Relationen**. Die Basisrelationen bleiben dabei unverändert. Sie bildet die theoretische Grundlage für Anfrageoptimierung und -ausführung in relationalen DBMS.

### Menge vs. Multimenge

| Eigenschaft | Menge                         | Multimenge          |
| ----------- | ----------------------------- | ------------------- |
| Duplikate   | ❌ nicht erlaubt               | ✅ erlaubt           |
| Verwendung  | Relationale Algebra (Theorie) | SQL / DBMS (Praxis) |
| Vorteil     | Saubere Semantik              | Effizienzsteigerung |

>💡 **Merkhilfe:** Eine Relation ist eine **Menge** von Tupeln, eine Datenbanktabelle ist eine **Multimenge** von Tupeln.

### Kriterien für Anfragesprachen

- **Ad-Hoc-Formulierung**: Keine vollständige Programmierung notwendig
- **Deskriptivität / Deklarativ**: „Was will ich?" — nicht „Wie komme ich daran?"
- **Mengenorientiertheit**: Operationen auf ganzen Datenmengen, nicht tuple-at-a-time
- **Abgeschlossenheit**: Jede Anfrage liefert wieder eine Relation
- **Adäquatheit**: Alle Konstrukte des Datenmodells werden abgedeckt
- **Orthogonalität**: Gleiche Konstrukte in ähnlichen Situationen verwendbar
- **Optimierbarkeit**: Wenige Operationen mit bekannten Optimierungsregeln
- **Effizienz**: Jede Operation hat Komplexität $\leq O(n^2)$, wobei $n$ = Anzahl der Tupel
- **Sicherheit**: Keine korrekte Anfrage kann in Endlosschleifen geraten oder unendliche Ergebnisse produzieren
- **Vollständigkeit**: Mindestens so ausdrucksstark wie die relationale Algebra

### Klassifikation der Operatoren

| Klasse | Operatoren |
|---|---|
| Mengenoperatoren | $\cup$ (Vereinigung), $\cap$ (Schnitt), $-$ (Differenz) |
| Entfernende Operatoren | $\sigma$ (Selektion), $\pi$ (Projektion) |
| Kombinierende Operatoren | $\times$ (Kreuzprodukt), $\bowtie$ (Join), Joinvarianten |
| Schema-Operator | $\rho$ (Umbenennung) |

---

## 2. Basisoperatoren ($\cup,\ -,\ \times,\ \pi,\ \sigma,\ \rho$)

Es gibt **5+1 Basisoperatoren**, die die minimale relationale Algebra bilden. Kein einziger kann ohne Vollständigkeitsverlust weggelassen werden.

### Vereinigung (Union, $\cup$)

Sammelt alle Tupel aus beiden Relationen in einer Ergebnisrelation. Duplikate werden entfernt.

$$\boxed{R \cup S := \{t \mid t \in R \lor t \in S\}}$$

**Voraussetzung:** $R$ und $S$ müssen **schemaverträglich** sein (gleiche Anzahl, Namen und Reihenfolge der Attribute).

⚠️ **Achtung:** Falls Schemata inkompatibel sind, muss vor der Vereinigung mit $\rho$ umbenannt werden.

### Differenz (Difference, $-$)

Eliminiert aus $R$ alle Tupel, die auch in $S$ vorkommen.

$$\boxed{R - S := \{t \mid t \in R \land t \notin S\}}$$

⚠️ **Achtung:** Nicht kommutativ — $R - S \neq S - R$.

### Kartesisches Produkt (Cross Product, $\times$)

Paart jedes Tupel aus $R$ mit jedem Tupel aus $S$. Das Ergebnis enthält $|R| \cdot |S|$ Tupel und alle Attribute beider Relationen.

$$\boxed{R \times S}$$

- Bei **Namensgleichheit** von Attributen: Umbenennung mit $\rho$ notwendig
- Neue Relation: $n \cdot m$ Tupel, $\sum$ der Attribute aus $R$ und $S$

### Projektion (Projection, $\pi$)

Erzeugt eine neue Relation mit nur einer **Teilmenge der Attribute** (vertikale Auswahl).

$$\boxed{\pi_{A_1, A_2, \dots, A_n}(R)}$$

### Selektion (Selection, $\sigma$)

Erzeugt eine neue Relation mit gleichem Schema, aber nur den Tupeln, die die Bedingung $C$ erfüllen (horizontale Auswahl).

$$\boxed{\sigma_C(R)}$$
**Beispiel:**

$$\sigma_{\text{Länge} \geq 100 \;\land\; \text{Studio} = \text{'Fox'}}(\text{Film})$$

### Umbenennung (Rename, $\rho$)

Benennt eine Relation und/oder deren Attribute um. Verändert keine Tupel, nur das Schema.

$$\boxed{\rho_{S(A_1, \dots, A_n)}(R)}$$

| Notation | Bedeutung |
|---|---|
| $\rho_S(R)$ | Nur Relation umbenennen |
| $\rho_{(A_1, \dots, A_n)}(R)$ | Nur Attribute umbenennen |
| $\rho_{S(A_1, \dots, A_n)}(R)$ | Relation und Attribute umbenennen |

**Anwendungsfälle:**
- Joins ermöglichen, wo Attribute gleich heißen müssen
- Kartesische Produkte ermöglichen, wo Attribute unterschiedliche Namen brauchen
- Schemaverträglichkeit für Mengenoperationen herstellen

---

## 3. Abgeleitete Operatoren

Diese Operatoren sind nützliche Abkürzungen, aber **nicht essentiell** — jeder lässt sich durch Basisoperatoren ausdrücken.

### Schnittmenge (Intersection, $\cap$)

Liefert alle Tupel, die in **beiden** Relationen vorkommen.

$$\boxed{R \cap S := \{t \mid t \in R \land t \in S\}}$$

**Ableitung durch Basisoperatoren:**

$$R \cap S = R - (R - S)$$

### Natürlicher Join (Natural Join, $\bowtie$)

Verbindet zwei Relationen über **alle gemeinsamen Attribute**. Das Ergebnis enthält jedes gemeinsame Attribut nur einmal.

$$\boxed{R \bowtie S}$$

**Ableitung:**

$$R \bowtie S = \pi_L\bigl(\sigma_{R.A_1 = S.A_1 \;\land\; \dots \;\land\; R.A_n = S.A_n}(R \times S)\bigr)$$

>💡 **Rolle:** Wird zur verlustfreien Wiederherstellung nach Dekomposition verwendet (vgl. [[VL.05 Relationale Entwurfstheorie]]).

### Theta-Join ($\bowtie_\theta$)

Verallgemeinerter Join mit einer **beliebigen Bedingung** $\theta$. Theta ist ein Vergleichsoperator aus $\{=, <, \leq, >, \geq, \neq\}$.

$$\boxed{R \bowtie_\theta S = \sigma_\theta(R \times S)}$$

- Schema des Ergebnisses: wie beim Kartesischen Produkt (beide Attributmengen vollständig)
- Der natürliche Join ist ein **Spezialfall** des Theta-Joins

⚠️ **Achtung:** Beim Theta-Join bleiben doppelte Attribute im Schema erhalten — beim Natural Join nicht.

**Beispiel:**

$$R \bowtie_{A < D \;\land\; R.B \neq S.B} S$$

### Division (Division, $/$)

Findet alle $x$-Werte, die mit **allen** $y$-Werten aus $S$ in $R$ kombiniert vorkommen.

$$\boxed{R / S = \{ x \in \pi_x(R) \mid \forall\, y \in S : (x, y) \in R \}}$$

>💡 **Anwendungsfall:** „Welche Studenten haben **alle** Module besucht, die auch Jon Snow besucht hat?"

**Ableitung durch Basisoperatoren:**

$$R / S = \pi_x(R) - \pi_x\bigl((\pi_x(R) \times S) - R\bigr)$$

**Vorgehen:** Disqualifiziere alle $x$-Werte, bei denen irgendein $y \in S$ fehlt.

#### Divisions-Beispiel: Jon Snow

```

JOHN_SNOW <- σ_{Name='John_Snow'}(Student) JOHN_SNOW_MODUL <- π_{ModNr}(Besucht ⋈ JOHN_SNOW) ALLE_TEILNEHMER <- π_{MatrNr, ModNr}(Besucht)

TEILNEHMER_SNOW <- ALLE_TEILNEHMER / JOHN_SNOW_MODUL

```

- $R$ = `ALLE_TEILNEHMER`, $S$ = `JOHN_SNOW_MODUL`, $X$ = `MatrNr`
- Ergebnis: `MatrNr` aller Studenten, die mindestens dieselben Module wie Jon Snow besucht haben

---

## 4. Unabhängigkeit und Vollständigkeit

### Minimale relationale Algebra

$$\boxed{\{\cup,\; -,\; \times,\; \pi,\; \sigma,\; \rho\}}$$

- **Unabhängig:** Kein Operator kann weggelassen werden, ohne Vollständigkeit zu verlieren
- **Vollständig:** Jede relationale Anfrage lässt sich mit diesen Operatoren ausdrücken
- **Abgeschlossen:** Jeder Ausdruck liefert wieder eine Relation

Abgeleitete Operatoren sind **redundant** (Beweise):

| Operator | Ableitung |
|---|---|
| $R \cap S$ | $R - (R - S)$ |
| $R \bowtie_C S$ | $\sigma_C(R \times S)$ |
| $R \bowtie S$ | $\pi_L(\sigma_{R.A_1=S.A_1 \land \ldots}(R \times S))$ |
| $R / S$ | $\pi_x(R) - \pi_x((\pi_x(R) \times S) - R)$ |

---

## 5. Komplexe Ausdrücke & Ausführungsbäume

### Idee und Methodik

Komplexe Anfragen entstehen durch **Schachtelung von Operatoren**. Die Abgeschlossenheit der relationalen Algebra erlaubt es, Output direkt als neuen Input zu verwenden.

**Vorgehensweise:**
1. Welche **Relationen** werden benötigt?
2. Welche **Operationen** sind notwendig?
3. In welcher **Reihenfolge** sollen die Operationen ausgeführt werden?

**Darstellung:**
- Als **geschachtelter Ausdruck** mit Klammerung
- Als **Operatorbaum** (Blätter = Basisrelationen, innere Knoten = Operatoren)

### Beispiel: 3. Versuch ISDA-Modul

**Anfrage:** Welche Studenten (`MatrNr`, `Name`) müssen im ISDA-Modul im 3. Versuch mündlich geprüft werden?

- Relationen: `Student`, `Modul`, `Besucht`
- Operationen: $\sigma, \sigma, \bowtie, \bowtie, \pi$

$$\pi_{\text{MatrNr},\, \text{Name}}\Bigl(\text{Student} \bowtie \bigl(\sigma_{\text{MName}=\text{'ISDA'}}(\text{Modul})\bigr) \bowtie \bigl(\sigma_{\text{Note}=\text{'5'} \;\land\; \text{Versuch}=\text{'2'}}(\text{Besucht})\bigr)\Bigr)$$

>💡 **Optimierung:** Selektionen $\sigma$ werden so früh wie möglich angewendet, um die Zwischenergebnismengen zu minimieren.

### Vorschau: Algebraische Optimierungsregeln

| Regel | Beschreibung |
|---|---|
| $R \bowtie S = S \bowtie R$ | Kommutativität des Joins |
| $(R \bowtie S) \bowtie T = R \bowtie (S \bowtie T)$ | Assoziativität |
| $\pi_Y(\pi_{X,Y}(R)) = \pi_Y(R)$ | Projektion vereinfachen |
| $\sigma_{A=a}(\sigma_{B=b}(R)) = \sigma_{B=b \land A=a}(R)$ | Selektionen zusammenfassen |
| $\pi_X(\sigma_{A=a}(R)) = \sigma_{A=a}(\pi_X(R))$ | Selektion durch Projektion schieben |
| $\sigma_{A=a}(R \cup S) = \sigma_{A=a}(R) \cup \sigma_{A=a}(S)$ | Selektion in Union ziehen |

---

## 6. Erweiterte Operatoren

### Aggregation

Fasst Werte einer Spalte zusammen. Doppelte Werte fließen doppelt in die Berechnung ein.

| Funktion | Beschreibung |
|---|---|
| `SUM(A)` | Summe aller Werte in Attribut $A$ |
| `AVG(A)` | Durchschnittswert |
| `MIN(A)` / `MAX(A)` | Kleinster / Größter Wert |
| `COUNT(A)` | Anzahl der Tupel (bei beliebigem Attribut) |

### Gruppierung ($\gamma$)

Partitioniert Tupel nach gemeinsamen Attributwerten und wendet Aggregatfunktionen auf jede Gruppe an.

$$\boxed{\gamma_L(R)}$$

Dabei ist $L$ eine Liste aus:
- **Gruppierungsattribute**: Attribut, nach dem gruppiert wird
- **Aggregatoperatoren**: z.B. `AVG(Note) → Notendurchschnitt`

**Ohne Gruppierungsattribut:** Gesamte Relation $R$ ist eine Gruppe → Ergebnis hat genau ein Tupel.

**Beispiel I:**

$$\gamma_{\text{PNr},\; \text{COUNT(MatrNr)} \to \text{AnzahlStud},\; \text{AVG(Note)} \to \text{NoteDurchschnitt}}(\text{Prüft})$$

**Beispiel II:** Durchschnittsnoten im 1. Versuch im Sommersemester 'SS2021' im Modul 'ISDA':

$$\pi_{m.\text{Name},\, \text{Notendurchschnitt}}\Bigl(\sigma_{m.\text{Name}=\text{'ISDA'}}\bigl(\gamma_{m.\text{Name};\; \text{AVG(Note)} \to \text{Notendurchschnitt}}\bigl(\sigma_{m.\text{ModNr}=hb.\text{ModNr} \;\land\; hb.\text{Versuch}=1 \;\land\; hb.\text{Sem}=\text{'SS2021'}}(\rho_m \text{Modul} \times \rho_{hb} \text{Besucht})\bigr)\bigr)\Bigr)$$

### Erweiterte Projektion

Erlaubt arithmetische Ausdrücke und Umbenennungen innerhalb der Projektion.

$$\boxed{\pi_L(R) \quad \text{wobei L Ausdrücke enthält:}}$$

Ein Element von $L$ kann sein:
- Ein Attribut von $R$ (wie bisher)
- $X \to Y$: Attribut $X$ umbenennen in $Y$
- $E \to Z$: Ausdruck $E$ (Arithmetik, String-Operationen) mit neuem Name $Z$

**Beispiele:**
- $A1 + A2 \to \text{Summe}$
- $\text{Vorname} \| \text{Nachname} \to \text{Name}$

### Generalisierte Projektion

Die Kombination von Gruppierung und Aggregation wird als **generalisierte Projektion** verstanden:

$$\pi_{G,\, \text{Agg}(A)} = \pi_{G,\, A}\Bigl(\gamma_{G,\; \text{Agg}(A) \to A}(R)\Bigr)$$

### Sortierung ($\tau$)

Sortiert Tupel nach einer Attributliste.

$$\boxed{\tau_L(R)}$$

Falls $L = (A_1, A_2, \dots, A_n)$: Erst nach $A_1$ sortieren, bei Gleichheit nach $A_2$, usw.

⚠️ **Achtung:** Das Ergebnis der Sortierung ist eine **Liste**, keine Menge! Daher muss $\tau$ immer der **letzte Operator** sein — andernfalls geht die Sortierung verloren.

---

## 7. Anhang: Weitere Erweiterungen

### Duplikateneliminierung ($\delta$)

Wandelt eine **Multimenge** in eine **Menge** um, indem alle Tupel-Kopien entfernt werden.

$$\boxed{\delta(R)}$$

### Semi-Join ($\ltimes$)

Berechnet einen Join über $R$ und $S$, behält aber nur die Attribute von $R$ im Ergebnis.

$$\boxed{R \ltimes S := \pi_A(R \bowtie_F S) = R \bowtie_F \pi_{A \cap B}(S)}$$

⚠️ **Nicht symmetrisch:** $R \ltimes S \neq S \ltimes R$.

### Outer Joins (Äußere Verbünde)

Übernahme von „dangling tuples" (nicht matchende Tupel) in das Ergebnis, aufgefüllt mit **Nullwerten**.

| Operator | Symbol | Beschreibung |
|---|---|---|
| Inner Join | $R \bowtie S$ | Nur matchende Tupel |
| Left Outer Join | $R\ \text{⟕}\ S$ | Alle Tupel aus $R$, nicht matchende $S$-Seite mit $\bot$ |
| Right Outer Join | $R\ \text{⟖}\ S$ | Alle Tupel aus $S$, nicht matchende $R$-Seite mit $\bot$ |
| Full Outer Join | $R\ \text{⟗}\ S$ | Alle Tupel beider Seiten, fehlende Seite mit $\bot$ |

**Anwendung:** Outer Joins werden in der **Informationsintegration** genutzt, bei der möglichst viele Daten (Tupel + Attribute) aus überlappenden Quellen erhalten werden sollen. Dazu sind **Schema Matching** (Attributüberlappungen erkennen) und **Duplikaterkennung** notwendig.

### Outer Union ($\uplus$)

Wie die normale Vereinigung, aber auch mit **inkompatiblen Schemata** möglich.

$$\boxed{R \uplus S}$$

- Schema: Vereinigung der Attributmengen beider Relationen
- Fehlende Werte werden mit Nullwerten ($\bot$) aufgefüllt

---

## 📌 Zusammenfassung

### Alle Operatoren im Überblick

| Operator | Symbol | Typ | Beschreibung |
|---|---|---|---|
| Selektion | $\sigma_C(R)$ | Basis | Filtert Zeilen nach Bedingung $C$ |
| Projektion | $\pi_L(R)$ | Basis | Wählt Spalten aus, entfernt Duplikate |
| Vereinigung | $R \cup S$ | Basis | Alle Tupel aus $R$ oder $S$ |
| Differenz | $R - S$ | Basis | Tupel in $R$, nicht in $S$ |
| Kreuzprodukt | $R \times S$ | Basis | Alle Tupelkombinationen |
| Umbenennung | $\rho_{S(L)}(R)$ | Basis | Schema umbenennen |
| Schnitt | $R \cap S$ | Abgeleitet | Tupel in $R$ und $S$ |
| Nat. Join | $R \bowtie S$ | Abgeleitet | Join über gleiche Attribute |
| Theta-Join | $R \bowtie_\theta S$ | Abgeleitet | Join mit freier Bedingung |
| Division | $R / S$ | Abgeleitet | $x$ kommt mit allen $y \in S$ vor |
| Gruppierung | $\gamma_L(R)$ | Erweitert | Partitionierung + Aggregation |
| Sortierung | $\tau_L(R)$ | Erweitert | Liefert Liste (kein Mengenoperator) |
| Duplikatext. | $\delta(R)$ | Erweitert | Multimenge → Menge |
| Outer Join | $R\ \text{⟗}\ S$ | Erweitert | Erhält alle Tupel (mit $\bot$) |
| Outer Union | $R \uplus S$ | Erweitert | Vereinigung inkomp. Schemata |
| Semi-Join | $R \ltimes S$ | Erweitert | Join, nur Attribute von $R$ |

### Kernaussagen

✅ **Abgeschlossenheit** — Jeder Operator erzeugt wieder eine Relation, die als neuer Operand dient.  
✅ **Minimale Algebra** — Die 5+1 Basisoperatoren sind vollständig und unabhängig voneinander.  
✅ **Methodik für komplexe Anfragen** — Relationen wählen → Operationen bestimmen → Reihenfolge optimieren.  
⚠️ **Menge vs. Multimenge** — Relationale Algebra: Menge. DBMS/SQL: Multimenge. Duplikate können unbemerkt entstehen.  
⚠️ **Sortierung immer zuletzt** — $\tau$ liefert eine Liste, nicht mehr eine Menge. Nachfolgende Mengenoperationen würden die Reihenfolge zerstören.  
❌ **Theta-Join ≠ Natural Join im Schema** — Beim Theta-Join bleiben doppelte Attribute erhalten, beim Natural Join nicht.

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.04 Relationaler Entwurf]]: Der natürliche Join wird zur **verlustfreien Wiederherstellung** dekomponierter Relationen eingesetzt.
- [[VL.08 SQL-DQL]]: SQL implementiert die relationale Algebra deklarativ; Konzepte wie `SELECT`, `WHERE`, `JOIN`, `GROUP BY` entsprechen direkt $\pi$, $\sigma$, $\bowtie$, $\gamma$.
- [[VL.05 Relationale Entwurfstheorie]]: Grundlage: Wie Basisrelationen erstellt und manipuliert werden, auf denen die Algebra aufbaut.
