**Class:** [[DS - Diskrete Strukturen]]  
**Date:** 22-05-2026  
**Topics:** #Graph #Zusammenhang #Menger #EulerTour #Hamilton #Blockgraph #Separator
**Link:** [[VL.06 DS.pdf]]

***

## 🎯 Lernziele der Vorlesung

Diese Vorlesung behandelt tiefere Struktur verbundener Graphen: Wie robust ist der Zusammenhang, wie kann man ihn zerlegen, und welche Rundtouren existieren?

- **Isomorphismus**: Wann sind zwei Graphen „strukturell gleich"?
- **k-Zusammenhang & Konnektivität**: Wie viele Knoten müssen entfernt werden, um einen Graphen zu trennen?
- **Schnittknoten & Brücken**: Einzelne kritische Elemente im Graphen
- **Blockgraph**: Hierarchische Zerlegung in 2-zusammenhängende Teile
- **Separatoren & Trenner**: Formalisierung von Trennmengen
- **Satz von Menger**: Dualität zwischen disjunkten Pfaden und Trennmengen
- **Euler-Touren**: Wann kann man alle Kanten genau einmal durchlaufen?
- **Hamilton-Kreise**: Wann kann man alle Knoten genau einmal besuchen?

***

## 1. Isomorphismus

### Definition

Zwei Graphen $G$ und $H$ können dieselbe Struktur haben, obwohl ihre Knoten unterschiedlich benannt sind. Ein Isomorphismus formalisiert diese Gleichheit.

$$\boxed{h: V(G) \to V(H) \text{ ist Isomorphismus} \iff h \text{ bijektiv und } \{u,v\} \in E(G) \Leftrightarrow \{h(u), h(v)\} \in E(H)}$$

**Merkhilfe:** Ein Isomorphismus ist eine „Umbenennung" der Knoten, die die Kantenstruktur vollständig erhält. Zwei isomorphe Graphen sind strukturell identisch.

**Beispiel:**
```
G: Knoten {1,...,8}    H: Knoten {a,...,h}
   (gleiche Struktur, andere Bezeichnungen)
```

> 💡 **Intuition:** Wenn man $G$ auf Transparentpapier zeichnet und es so über $H$ legen kann, dass alle Kanten übereinstimmen, sind die Graphen isomorph.

***

## 2. Wiederholung: Zusammenhang & k-Zusammenhang

### Definitionen (Zusammenhang)

$$\boxed{G \text{ zusammenhängend} \iff \forall u,v \in V(G): \exists \text{ Pfad von } u \text{ nach } v \text{ in } G}$$

- **Zusammenhängend in $G$**: $U \subseteq V(G)$ heißt zusammenhängend in $G$, wenn $G[U]$ zusammenhängend ist.
- **Zusammenhangskomponenten**: Die maximalen zusammenhängenden Teilgraphen von $G$.

### k-Zusammenhang & Konnektivität

$$\boxed{G \text{ ist } k\text{-zusammenhängend} \iff |G| > k \;\text{ und }\; G - X \text{ zusammenhängend für alle } X \subseteq V(G) \text{ mit } |X| < k}$$

- **Konnektivität** $\kappa(G)$: Das maximale $k \geq 0$, für das $G$ $k$-zusammenhängend ist.

**Beispiele:**

| Graph | $\kappa(G)$ | Begründung |
|-------|------------|------------|
| Vollständiger Graph $K_n$ | $n-1$ | Jede Teilmenge mit $< n-1$ Knoten lässt den Rest zusammenhängend |
| Pfad $P_n$ | $1$ | Ein innerer Knoten trennt den Pfad |
| Kreis $C_n$ | $2$ | Zwei Knoten müssen entfernt werden |

### Schnittknoten & Brücken

$$\boxed{v \in V(G) \text{ ist Schnittknoten} \iff G - v \text{ nicht zusammenhängend}}$$

$$\boxed{e = \{u,v\} \text{ ist Brücke} \iff G - e \text{ nicht zusammenhängend}}$$

- **Schnittknoten** sind 1-Trenner im Graphen.
- **Brücken** sind Kanten, deren Entfernung den Graphen trennt.

![[VL.05 DS-1779629071238.webp]]

Knoten 4, 7, 8 sind Schnittknoten
Kante {7,8} ist eine Brücke (rot markiert)

⚠️ **Achtung:** Ein Graph kann Schnittknoten haben, ohne Brücken zu haben, und umgekehrt.

***

## 3. Blockgraphen

### Motivation: Zerlegung in 2-zusammenhängende Teile

**Beobachtung:** Wenn $G$ zusammenhängend aber nicht 2-zusammenhängend ist, dann hat $G$ einen Schnittknoten *oder* besteht nur aus einer einzelnen Kante bzw. einem einzelnen Knoten.

> 💡 **Idee:** Man kann jeden zusammenhängenden Graphen an seinen Schnittknoten in seine maximalen schnittknoten-freien Teile zerlegen – die **Blöcke**.

### Definition: Block

$$\boxed{\text{Block von } G = \text{maximaler zusammenhängender Teilgraph von } G \text{ ohne Schnittknoten}}$$

**Eigenschaften von Blöcken:**
- Jeder Block ist entweder eine Einzelkante, ein einzelner Knoten, oder ein 2-zusammenhängender Graph.
- Zwei verschiedene Blöcke teilen höchstens einen gemeinsamen Knoten (einen Schnittknoten).

![[VL.05 DS-1779630060798.webp]]

### Definition: Blockgraph $B(G)$

Sei $A \subseteq V(G)$ die Menge der Schnittknoten und $\mathcal{B}$ die Menge der Blöcke von $G$.

$$\boxed{B(G) = \text{bipartiter Graph mit Knotenmenge } A \cup \mathcal{B} \text{ und Kanten } \{\{a, B\} : B \in \mathcal{B},\, a \in A,\, a \in V(B)\}}$$

**Rolle:** Der Blockgraph kodiert, wie die Blöcke über Schnittknoten miteinander verbunden sind.

![[VL.05 Mehrfachzusammenhang und Rundtouren-1779630248883.webp|251x353]]

### Proposition & Satz: Azyklizität des Blockgraphen

$$\boxed{\text{Für jeden Graphen } G \text{ ist } B(G) \text{ ein Wald. Ist } G \text{ zusammenhängend, so ist } B(G) \text{ ein Baum.}}$$

**Beweis (Widerspruch):**

Angenommen, $B(G)$ enthält einen Kreis $C := a_1 B_1 a_2 B_2 \ldots a_n B_n a_1$. Definiere $a_{n+1} := a_1$.

**Schritt 1:** Nach Definition gilt $a_i, a_{i+1} \in V(B_i)$ für alle $1 \leq i \leq n$.

**Schritt 2:** Da alle $B \in \mathcal{B}$ zusammenhängend sind, existiert in $B_i$ ein Pfad $P_i$ von $a_i$ nach $a_{i+1}$.

**Schritt 3:** Da in $C$ kein Schnittknoten und kein Block wiederholt wird, liefert $P_1 \cup P_2 \cup \ldots \cup P_n$ einen Kreis in $G$, der mindestens zwei Schnittknoten und mindestens zwei Blöcke enthält.

**Schritt 4 (Widerspruch):** Dann wären $B_1$ und $B_2$ keine Blöcke, denn durch Löschen eines einzigen Knotens kann man $B_1$ und $B_2$ nicht trennen. $\square$

***

## 4. Separatoren und Trenner

### Definitionen

Sei $G$ ein Graph und $A, B \subseteq V(G)$, $X \subseteq V(G)$.

$$\boxed{X \text{ trennt } A \text{ und } B \text{ in } G \iff \text{jeder } A\text{-}B\text{-Pfad in } G \text{ enthält einen Knoten aus } X}$$

- **$A$-$B$-Pfad**: Ein Pfad mit je einem Endpunkt in $A$ und $B$.
- **Trenner** (Separator): $X$ trennt zwei Knoten $u, v \notin X$ derselben Komponente von $G$.
- **$k$-Trenner**: Ein Trenner $X$ mit $|X| = k$.

> 💡 **Notation:** „Trenner" und „Separator" sind Synonyme.

### Zusammenhang mit Schnittknoten

$$\boxed{X = \{v\} \text{ ist Trenner in } G \implies v \text{ ist Schnittknoten in } G}$$

### Charakterisierung über Trenner

$$\boxed{G \text{ ist } k\text{-zusammenhängend} \iff |G| > k \;\text{ und }\; \nexists \text{ Trenner } X \subseteq V(G) \text{ mit } |X| < k}$$

![[VL.06 Mehrfachzusammenhang und Rundtouren-1779725848868.webp|882x402]]
***

## 5. Der Satz von Menger

### Motivation: Positive Sichtweise auf k-Zusammenhang

Bisher: $G$ ist $k$-zusammenhängend, wenn das Entfernen von $< k$ Knoten den Zusammenhang nicht zerstört.

**Alternative Sichtweise:** $k$-facher Zusammenhang könnte auch bedeuten, dass es zwischen je zwei Knoten mindestens $k$ voneinander verschiedene Pfade gibt.

### Definition: Disjunkte Pfade

$$\boxed{P_1, P_2 \text{ knoten-disjunkt} \iff V(P_1) \cap V(P_2) = \emptyset}$$

$$\boxed{P_1, P_2 \text{ intern knoten-disjunkt} \iff \text{kein innerer Knoten von } P_1 \text{ liegt auf } P_2 \text{ (und umgekehrt)}}$$

⚠️ **Unterschied:** Intern knoten-disjunkte Pfade dürfen **gemeinsame Endpunkte** haben, aber kein innerer Knoten des einen Pfades darf auf dem anderen liegen.

### Satz von Menger (1927)

$$\boxed{\text{Minimale Trennergröße}(A,B) = \text{Maximale Anzahl knotendisjunkter } A\text{-}B\text{-Pfade}}$$

Formal: Sei $G$ ein Graph, $A, B \subseteq V(G)$. Dann gilt:

$$\min_{X \text{ trennt } A,B} |X| = \max_{|\mathcal{P}|:\, \mathcal{P} \text{ knoten-disjunkte } A\text{-}B\text{-Pfade}} |\mathcal{P}|$$

**Beispiel (3 disjunkte Pfade = 3-Trenner):**

![[VL.06 Mehrfachzusammenhang und Rundtouren-1779726281860.webp|974x459]]
### Beweis (Induktion über $|V(\mathcal{P})|$)

**Ziel (stärkere Aussage):** Wenn $\mathcal{P}$ weniger als $k$ disjunkte $A$-$B$-Pfade enthält, dann gibt es eine Menge $\mathcal{Q}$ von $|\mathcal{P}|+1$ disjunkten $A$-$B$-Pfaden, die $\mathcal{P}$ **erweitert**.

**$\mathcal{Q}$ erweitert $\mathcal{P}$:** $A \cap V(\mathcal{P}) \subset A \cap V(\mathcal{Q})$ und $B \cap V(\mathcal{P}) \subset B \cap V(\mathcal{Q})$

**Induktionsbasis** $|V(\mathcal{P})| = 0$:

Sei $R$ ein $A$-$B$-Pfad. Setze $\mathcal{Q} := \{R\}$. ✅

**Induktionsschritt** $|V(\mathcal{P})| > 0$:

Sei $R$ ein $A$-$B$-Pfad, der die $(<k)$ Knoten aus $B$ in $V(\mathcal{P})$ vermeidet.

```pseudocode
Fall 1: R trifft keinen Pfad aus P
  → Q := P ∪ {R}  ✅

Fall 2: R trifft einen Pfad P ∈ P
  Sei x der letzte Knoten aus R auf einem P ∈ P
  Setze B' := B ∪ V(xP ∪ xR)
  Setze P' := (P \ {P}) ∪ {Px}
  
  [|V(P')| < |V(P)| → Induktionshypothese anwendbar]
  
  Q' = Menge mit |P'|+1 disjunkten A-B'-Pfaden (per IV)
  Q' enthält:
    - Pfad Q, der in x endet
    - Pfad Q', dessen letzter Knoten y ∉ letzten Endknoten von P'
  
  Fall 2a: y ∉ V(xP)
    → Q ersetzen durch Q mit angehängtem xP
    → Falls y ∈ V(xR): Q' mit angehängtem yR
    → Falls y ∉ V(xR): Q' bleibt
  
  Fall 2b: y ∈ V(xP)
    → Q: xR anhängen
    → Q': yP anhängen
    
  → In beiden Fällen erweitert Q die Menge P  ✅  □
```

**Notation:**
- $xP$ = Teilpfad von $x$ bis zum Ende von $P$
- $Px$ = Teilpfad vom Anfang von $P$ bis $x$

### Varianten des Satzes von Menger

| Variante | Aussage |
|---------|---------|
| **Knotendisjunkt (ungerichtet)** | min. $A$-$B$-Trenner = max. knotendisjunkte Pfade |
| **Kantendisjunkt** | min. Kantenanzahl zum Trennen = max. kantendisjunkte Pfade |
| **Gerichtete Graphen** | Analoge Aussage für gerichtete Pfade |

### Dualität (Kernaussage)

$$\boxed{\text{Entweder gibt es } k \text{ disjunkte } A\text{-}B\text{-Pfade, oder es gibt einen } k\text{-Trenner.}}$$

> 💡 **Merkhilfe:** Der Satz von Menger ist ein Min-Max-Theorem: Das Maximum der einen Seite ist gleich dem Minimum der anderen. Dies ist vergleichbar mit dem Max-Flow-Min-Cut-Theorem in Netzwerken.

⚠️ **Algorithmus:** Aus dem Beweis folgt nicht sofort ein effizienter Algorithmus. Am einfachsten berechnet man maximale disjunkte Pfade mit **Netzwerkflussalgorithmen** (→ Modul „Algorithmen und Datenstrukturen").

***

## 6. Euler-Touren

### Definition

$$\boxed{\text{Euler-Tour in } G = \text{geschlossener Kantenzug, der jede Kante aus } G \text{ genau einmal durchläuft}}$$

**Beispiel:**
![[VL.06 Mehrfachzusammenhang und Rundtouren-1779726597657.webp|378x557]]

### Satz: Charakterisierung Euler-Touren

$$\boxed{G \text{ zusammenhängend hat Euler-Tour} \iff \deg(v) \text{ gerade für alle } v \in V(G)}$$

### Beweis (Hinrichtung: Euler-Tour $\Rightarrow$ gerade Grade)

Sei $(v_0, e_1, v_1, e_2, \ldots, e_m, v_m = v_0)$ eine Euler-Tour. Definiere $e_{m+1} = e_1$.

Für $u \in V(G)$ sei $I(u) := \{i : 1 \leq i \leq m,\, v_i = u\}$.

Dann gilt:
$$\{e \in E(G) : u \text{ inzident zu } e\} = \{e_i, e_{i+1} : i \in I(u)\}$$

Da $G$ keine Schleifen enthält und $e_i \neq e_j$ für $i \neq j$, sind die Paare $\{e_i, e_{i+1}\}$ für $i \in I(u)$ paarweise disjunkt.

$$\deg_G(u) = 2 \cdot |I(u)| \implies \deg_G(u) \text{ gerade} \quad \dashv$$

> 💡 **Intuition:** Jedes Mal, wenn die Tour einen Knoten $u$ besucht, werden genau 2 Kanten „verbraucht" (Einfahrt + Ausfahrt). Also hat jeder Knoten einen geraden Grad.

### Beweis (Rückrichtung: gerade Grade $\Rightarrow$ Euler-Tour)

**Behauptung 1:** $G$ enthält einen geschlossenen Kantenzug ohne Kantenwiederholung.

```pseudocode
Konstruktion:
1. Wähle e1 = {v0, v1} ∈ E(G) beliebig, setze C1 = (v0, e1, v1)
2. Sei Ci = (v0, e1, ..., ei, vi) schon konstruiert:
   - Falls vi zu unbenutzter Kante e = {vi, v'} inzident:
       Ci+1 := (v0, ..., vi, e, v')
   - Sonst: Stopp
3. Da alle Grade gerade: Stopp nur wenn vi = v0 (geschlossener Zug) ✅
```

**Hauptbeweis (Erweiterungsargument):**

```pseudocode
1. Wähle maximalen geschlossenen Kantenzug T ohne Kantenwiederholung
   (existiert nach Behauptung 1)
2. Behauptung: T ist Euler-Tour
   Beweis (Widerspruch):
   - Sei F = Kantenmenge von T
   - Falls F ≠ E(G): ∃ Knoten vj in T inzident zu e ∈ E(G)\F
     (da G zusammenhängend)
   - In G-F hat jeder Knoten geraden Grad
   - ∴ ∃ geschlossener Kantenzug C in G-F durch vj mit e
   - T kann durch C erweitert werden → Widerspruch zur Maximalität ✅ □
```

**Alternative Konstruktion (iterative Erweiterung):**

```pseudocode
i := 1
T1 = geschlossener Kantenzug (Behauptung 1)
while Ti nicht alle Kanten enthält:
    Finde vj in Ti und Kante f1 = {vj, u1} ∉ Ti
    Konstruiere geschlossenen Kantenzug C = (vj, f1, u1, ..., vj)
      ohne Kanten aus Ti (mögl. da G - {e1,...,el} gerade Grade hat)
    Ti+1 = (v0,...,vj, f1, u1,...,vj,...,v0)
    i := i+1
return Ti  // Euler-Tour
```

### Definition: Eulersche Graphen

$$\boxed{G \text{ eulersch} \iff \deg(v) \text{ gerade für alle } v \in V(G)}$$

**Eigenschaften:**
- Eulersche Graphen sind die **Vereinigung paarweise kantendisjunkter Kreise**.
- Ist ein eulerscher Graph zusammenhängend, hat er eine Euler-Tour.

***

## 7. Hamilton-Kreise

### Definition

$$\boxed{\text{Hamilton-Kreis in } G = \text{Kreis, der jeden Knoten aus } V(G) \text{ genau einmal enthält}}$$

**Beispiel:**

```
Graph mit Hamilton-Kreis (dick gezeichnet):
1-a-2-h-7-i-3-c-4-d-5-k-8-l-6-f-1

Nicht benutzte Kanten: j (3-5), b (2-3), e (5-6), g (2-6)
```

### Vergleich: Euler-Tour vs. Hamilton-Kreis

| Eigenschaft | Euler-Tour | Hamilton-Kreis |
|-------------|-----------|----------------|
| **Durchläuft** | jede Kante genau einmal | jeden Knoten genau einmal |
| **Charakterisierung** | ✅ Vollständig bekannt (gerade Grade) | ⚠️ Kein einfaches Kriterium bekannt |
| **Komplexität** | Polynomiell entscheidbar | NP-vollständig (allgemein) |
| **Knoten/Kanten** | Knoten dürfen wiederholt werden | Kanten dürfen wiederholt werden |

⚠️ **Warnung:** Es gibt kein einfaches, vollständiges Kriterium für Hamilton-Kreise analog zum Euler-Kriterium. Das Hamilton-Kreis-Problem ist NP-vollständig.

***

## 📌 Zusammenfassung

### Wichtige Konzepte

| Konzept | Bedeutung |
|---------|-----------|
| **Isomorphismus** | Bijektive, strukturerhaltende Abbildung zwischen Graphen |
| **$k$-Zusammenhang** | Graph bleibt zusammenhängend nach Entfernen von $<k$ Knoten |
| **Konnektivität $\kappa(G)$** | Maximales $k$, für das $G$ $k$-zusammenhängend ist |
| **Schnittknoten** | Knoten, dessen Entfernung den Graphen trennt |
| **Brücke** | Kante, deren Entfernung den Graphen trennt |
| **Block** | Maximaler zusammenhängender Teilgraph ohne Schnittknoten |
| **Blockgraph $B(G)$** | Bipartiter Graph aus Blöcken und Schnittknoten |
| **$A$-$B$-Trenner** | Knotenmenge, die alle $A$-$B$-Pfade blockiert |
| **Satz von Menger** | min. Trennergröße = max. knotendisjunkte Pfade |
| **Euler-Tour** | Geschlossener Kantenzug, jede Kante genau einmal |
| **Eulerscher Graph** | Graph mit ausschließlich geraden Knotengraden |
| **Hamilton-Kreis** | Kreis, der jeden Knoten genau einmal besucht |

### Kernaussagen

✅ **Blockgraph ist azyklisch** – $B(G)$ ist stets ein Wald (Baum bei zusammenhängendem $G$)  
✅ **Satz von Menger** – Dualität: min. Trenner = max. disjunkte Pfade  
✅ **Euler-Charakterisierung** – Euler-Tour $\iff$ alle Knotengrade gerade (+ Zusammenhang)  
✅ **Eulersche Graphen** – Vereinigung paarweise kantendisjunkter Kreise  
⚠️ **Hamilton ≠ Euler** – Für Hamilton-Kreise gibt es kein einfaches Kriterium  
⚠️ **Algorithmus für Menger** – Beweis konstruktiv, aber für effiziente Berechnung: Netzwerkfluss  
❌ **Falsch:** „Ein Graph ohne Schnittknoten ist 2-zusammenhängend" – stimmt nur für $|G| > 2$  

### Wichtige Sätze & Formeln

| Satz / Formel | Aussage | Anwendung |
|--------------|---------|-----------|
| **Menger (1927)** | $\min\|$Trenner$\| = \max\|$disj. Pfade$\|$ | Netzwerkzuverlässigkeit |
| **Euler-Kriterium** | Euler-Tour $\iff$ alle Grade gerade | Graphenstruktur prüfen |
| **Blockgraph-Satz** | $B(G)$ ist Wald/Baum | Strukturanalyse |
| **$k$-Zusammenhang** | $G-X$ zusammenhängend $\forall \|X\|<k$ | Robustheitsanalyse |

***

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.04 Stirling, Catalan Zahlen]]: Grundbegriffe Graphen, Pfade, Kreise, Grad
- [[VL.05 Graphentheorie]]: Netzwerkfluss zur Berechnung maximaler disjunkter Pfade (Menger)
