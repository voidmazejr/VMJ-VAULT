**Class:** [[DS - Diskrete Strukturen]]  
**Date:** 15-05-2026  
**Topics:** #Graphentheorie #DS #Algorithmen #Bäume #Zusammenhang
**Link:** [[VL.05 DS 1.pdf]]

***

## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt in die grundlegenden Konzepte der Graphentheorie ein – von der formalen Definition eines Graphen über Wege, Bäume und Spannbäume bis hin zu Suchalgorithmen und Zusammenhangskonzepten.

- **Graphdefinitionen**: Formale Definitionen einfacher, gerichteter und ungerichteter Graphen
- **Grundbegriffe**: Grad, Adjazenz, Inzidenz, Nachbarschaft, Handshaking-Lemma
- **Teilgraphen**: Untergraph, induzierter Teilgraph, aufspannender Teilgraph
- **Wege & Pfade**: Weg, Pfad, Zyklus, Länge, Zusammenhang
- **Bäume & Wälder**: Azyklizität, Blätter, Kantenanzahl-Satz
- **Spannbäume**: Existenz, Konstruktion, Routing
- **Suchalgorithmen**: Tiefensuche (DFS) und Breitensuche (BFS)
- **Distanzen**: Distanzfunktion, Durchmesser, Radius
- **Mehrfachzusammenhang**: Schnittknoten, Brücken, k-Zusammenhang, Konnektivität

***

## 1. Einleitung & Motivation

### Definition – Einfacher, ungerichteter Graph

$$\boxed{G = (V(G),\ E(G)) \text{ mit } E(G) \subseteq \mathcal{P}_2[V(G)]}$$

- $V(G)$: **Knotenmenge** (auch: Ecken)
- $E(G)$: **Kantenmenge** – jede Kante ist eine 2-elementige Teilmenge von $V(G)$
- „einfach" bedeutet: **keine Schleifen** (keine Kante von $v$ nach $v$)

> 💡 **Merkhilfe:** Eine Kante $\{u, v\}$ ist eine *ungeordnete* Menge – Richtung spielt keine Rolle.

### Definition – Gerichteter Graph

$$\boxed{G = (V(G),\ E(G)) \text{ mit } E(G) \subseteq V \times V}$$

- Kanten sind **geordnete Paare** $(u, v)$ – Richtung ist relevant
- Beispiele: WWW (Links), soziale Netzwerke (Follows)

### Reale Anwendungen

| Domäne | Knoten | Kanten |
|---|---|---|
| **Computernetze** | Computer/Router | Verbindungen (Glasfaser, Funk) |
| **Schienennetze** | Bahnhöfe | Gleisverbindungen |
| **WWW** | Webseiten | Hyperlinks |
| **Soziale Netze** | Nutzer | Follows/Freundschaften |
| **Interaktionsnetzwerke** | Proteine | Biologische Interaktionen |

⚠️ **Vereinbarung:** In dieser Vorlesung sind alle Graphen – sofern nicht anders angegeben – **endlich, einfach und ungerichtet**.

***

## 2. Grundlagen

### Grundbegriffe: Ordnung und Kantenzahl

$$\boxed{|G| := |V(G)|} \quad \text{(Knotenzahl / Ordnung)}$$

$$\boxed{\|G\| := |E(G)|} \quad \text{(Kantenzahl)}$$

- **Schleife**: Kante von $v$ zu sich selbst ($\{v,v\}$) – in einfachen Graphen verboten
- **Endlich**: $|G|$ ist endlich

### Definition – Adjazenz, Inzidenz, Nachbarschaft

$$\boxed{N_G(u) := \{v \in V(G) : \{u,v\} \in E(G)\}}$$

$$\boxed{N_G[u] := N_G(u) \cup \{u\}}$$

- $u, v$ sind **adjazent** $\Leftrightarrow$ $\{u,v\} \in E(G)$
- Kante $e = \{u,v\}$ und Knoten $u$ sind **inzident** $\Leftrightarrow$ $u$ ist Endpunkt von $e$
- $N_G(u)$: **offene Nachbarschaft** von $u$
- $N_G[u]$: **geschlossene Nachbarschaft** von $u$ (inkl. $u$ selbst)

### Definition – Grad eines Knotens

$$\boxed{\deg_G(v) := |N_G(v)|}$$

$$\Delta(G) := \max\{\deg_G(v) : v \in V(G)\} \quad \text{(Maximalgrad)}$$

$$\delta(G) := \min\{\deg_G(v) : v \in V(G)\} \quad \text{(Minimalgrad)}$$

> 💡 **Merkhilfe:** Der Grad zählt, wie viele Nachbarn ein Knoten hat – also wie viele Kanten an ihm hängen.

### Satz – Handshaking-Lemma

$$\boxed{\sum_{v \in V(G)} \deg_G(v) = 2 \cdot \|G\| = 2 \cdot |E(G)|}$$

**Intuition:** Jede Kante verbindet genau zwei Knoten und trägt daher zum Grad beider Endpunkte je einmal bei – also insgesamt 2-mal zur Gradsumme.

**Folgesatz:** In jedem Graphen $G$ mit mindestens zwei Knoten gibt es zwei Knoten $u \neq v$ mit $\deg_G(u) = \deg_G(v)$.

**Beweis des Folgesatzes:**  
Sei $|G| = n \geq 2$. Mögliche Gradwerte: $0, 1, \ldots, n-1$. Aber $0$ und $n-1$ können nicht gleichzeitig auftreten (wenn ein Knoten mit allen verbunden ist, kann kein Knoten isoliert sein). Also liegen die Grade von $n$ Knoten in höchstens $n-1$ Werten → nach **Schubfachprinzip** müssen zwei Knoten denselben Grad haben. $\square$

⚠️ **Folgerung:** Die Anzahl der Knoten mit ungeradem Grad ist stets **gerade**.

***

## 3. Teilgraphen

### Definition – Teilgraphtypen

$$\boxed{H \subseteq G \Leftrightarrow V(H) \subseteq V(G) \text{ und } E(H) \subseteq E(G)}$$

**Drei Varianten:**

| Typ | Bedingung | Knotenmenge | Kantenmenge |
|---|---|---|---|
| **Untergraph / Teilgraph** | $H \subseteq G$ | $V(H) \subseteq V(G)$ | $E(H) \subseteq E(G)$ |
| **Induzierter Teilgraph** | $H \subseteq G$ | $V(H) \subseteq V(G)$ | $E(H) = E(G) \cap \mathcal{P}_2(V(H))$ |
| **Aufspannender Teilgraph** | $H \subseteq G$ | $V(H) = V(G)$ | $E(H) \subseteq E(G)$ |

> 💡 **Merkhilfe:** Induziert = alle Kanten „automatisch" dabei, die zwischen den gewählten Knoten liegen. Aufspannend = alle Knoten bleiben erhalten.

### Notation – Induzierte Teilgraphen

- $G[X]$: der von $X \subseteq V(G)$ **induzierte Teilgraph** mit $V(G[X]) = X$
- $G - H$: induzierter Teilgraph durch $V(G) \setminus V(H)$
- $G - v$: $G[V(G) \setminus \{v\}]$
- $G - S$: $G[V(G) \setminus S]$ für $S \subseteq V(G)$
- $G - e$: Graph mit $V(G)$ und $E(G) \setminus \{e\}$

### Definition – Vereinigung und Schnitt

$$G \cup H: \quad V = V(G) \cup V(H),\quad E = E(G) \cup E(H)$$

$$G \cap H: \quad V = V(G) \cap V(H),\quad E = E(G) \cap E(H)$$

- **Disjunkte Vereinigung**: $G \cup H$ wenn $V(G) \cap V(H) = \emptyset$

***

## 4. Wege, Pfade und Zusammenhang

### Definition – Weg, Pfad, Zyklus

Ein **Weg** $W$ in $G$ ist eine Folge:

$$\boxed{W = v_0\, e_1\, v_1\, e_2\, \ldots\, v_{k-1}\, e_k\, v_k}$$

mit $v_i \in V(G)$ und $e_i = \{v_{i-1}, v_i\} \in E(G)$ für alle $i$.

**Übersicht der Wegtypen:**

| Begriff | Bedingung | Bedeutung |
|---|---|---|
| **Weg** (Kantenzug) | beliebig | Folge von Knoten/Kanten |
| **Länge von $W$** | – | Anzahl $k$ der Kanten |
| **Geschlossener Weg** | $v_0 = v_k$ | Anfangs- = Endknoten |
| **Pfad** | $v_i \neq v_j$ für $i \neq j$ | keine Wiederholung von Knoten |
| **Zyklus / Kreis** | geschlossener Weg, $v_0 e_1 \ldots e_k v_k$ ist Pfad, $k \geq 2$ | kreisförmiger Pfad |

**Beispiel:**
```
Graph: 1--3--5--6--4--3--2
                 a  b  c  d  e  f

W = (1, a, 3, d, 5, h, 6, e, 4, c, 3, b, 2)
→ Weg der Länge 6 von 1 nach 2
→ Knoten 3 wird zweimal besucht → kein Pfad!
```

> 💡 **Merkhilfe:** Pfad = Weg ohne Knotenwiederholung. Zyklus = geschlossener Pfad (min. Länge 3 für einfache Graphen).

### Definition – Zusammenhang

$$\boxed{G \text{ ist zusammenhängend} \Leftrightarrow \forall u,v \in V(G)\ \exists \text{ Pfad von } u \text{ nach } v \text{ in } G}$$

- $U \subseteq V(G)$ ist **zusammenhängend in $G$**, wenn $G[U]$ zusammenhängend ist
- **Zusammenhangskomponenten**: maximale zusammenhängende Teilgraphen von $G$

**Beobachtung:** Jeder Graph ist die disjunkte Vereinigung seiner Zusammenhangskomponenten.

```
Beispiel mit 3 Komponenten:

Komponente 1: {1, 2, ..., 11}  (verbundenes Teilnetz)
Komponente 2: {a, b, c}        (kleinere Gruppe)
Komponente 3: {A}              (isolierter Knoten)
```

***

## 5. Bäume und Wälder

### Definition – Azyklisch, Wald, Baum

$$\boxed{\text{Baum} = \text{zusammenhängender, azyklischer Graph}}$$

| Begriff | Definition |
|---|---|
| **Azyklisch** | Enthält keinen Kreis |
| **Wald** | Azyklischer Graph (mehrere Komponenten möglich) |
| **Baum** | Zusammenhängender Wald |

```
Beispiel Baum (n=8):

        1
       / \
      4   2
     / \   \
    5   6   3
   /
  7
   \
    8
```

### Lemma – Minimalgrad in Bäumen

$$\boxed{\text{Jeder endliche Baum } T \text{ hat } \delta(T) \leq 1}$$

**Beweis (durch Widerspruch):**

**Annahme:** $\delta(T) > 1$.

**IA:** Wähle $\{u_0, u_1\} \in E(G)$ beliebig. Definiere $P_1 := u_0 u_1$.

**IV:** Sei $P_i := u_0 \ldots u_i$ schon definiert.

**IS:** Betrachte $u_i$. Da $\delta(G) > 1$, gibt es $v_1 \neq v_2 \in V(G)$ mit $\{u_i, v_1\}, \{u_i, v_2\} \in E(G)$. Also gibt es $v' \neq u_{i-1}$ mit $\{u_i, v'\} \in E(G)$.  
Definiere $P_{i+1} := u_0 \ldots u_i v'$.

Betrachte $P := P_{|T|+1}$: Da $T$ azyklisch ist, ist $P$ ein Pfad. Aber $P$ enthält $|T| + 2$ verschiedene Knoten – **Widerspruch** zu $|V(T)| = |T|$. $\square$

> 💡 **Intuition:** In jedem Baum gibt es mindestens ein **Blatt** (Knoten mit Grad 1). Sonst könnte man ewig einen Pfad verlängern.

### Satz – Kantenanzahl eines Baums

$$\boxed{\text{Ein Baum } T \text{ mit } n > 0 \text{ Knoten hat genau } n - 1 \text{ Kanten.}}$$

**Beweis (Induktion über $n$):**

**Induktionsanfang ($n = 1$):** $T$ hat einen Knoten und keine Kante. ✅

**Induktionsvoraussetzung:** Die Behauptung gelte für alle $j < n$.

**Induktionsschritt:** Es gilt $|V(T)| = n > 1$. Nach dem Lemma hat $T$ ein Blatt $u \in V(T)$ mit $\deg_T(u) = 1$. Sei $v$ der Nachbar von $u$.  
Dann ist $T' := T - u$ ein Baum mit $n - 1$ Knoten und hat nach IV genau $n - 2$ Kanten.  
$T$ hat eine Kante $\{u, v\}$ mehr als $T'$. Also hat $T$ genau $n - 1$ Kanten. $\square$

***

## 6. Spannbäume

### Definition – Spannbaum

$$\boxed{T \subseteq G \text{ ist Spannbaum} \Leftrightarrow T \text{ ist aufspannend, zusammenhängend und azyklisch}}$$

- Ein Spannbaum enthält **genau die Knoten von $G$**, aber eine minimale Kantenmenge um Zusammenhang zu sichern
- Hat $G$ $n$ Knoten, hat jeder Spannbaum genau $n - 1$ Kanten

```
Beispiel: G mit 8 Knoten und mehreren Kanten
Spannbaum T ⊆ G: wähle 7 Kanten, die alle 8 Knoten verbinden, ohne Kreis

G:                    Spannbaum T:
1--2--3               1--2--3
|  |  |               |     |
4--5--6     →         4     6
|     |               |
7-----8               7--8
```

### Lemma – Existenz von Spannbäumen

$$\boxed{\text{Jeder zusammenhängende Graph } G \text{ enthält einen Spannbaum.}}$$

**Beweis (durch minimale Gegenbeispiele + Widerspruch):**

Angenommen, die Behauptung sei falsch. Wähle $G$ als zusammenhängenden Graphen ohne Spannbaum mit **minimaler Kantenanzahl**.

**Beobachtung:** $|V| > 2$, da sonst $G$ selbst ein Baum wäre.

Da $G$ zusammenhängend aber kein Baum ist, enthält $G$ einen Kreis $C = (v_1, e_1, v_2, \ldots, v_k)$.

**Behauptung:** $G - e_1$ ist zusammenhängend.  
**Beweis:** Jeder Pfad, der $e_1$ benutzt, kann „um den Kreis herum" entlang $C - e_1$ umgeleitet werden. ⊣

Also ist $G - e_1$ zusammenhängend und hat weniger Kanten als $G$, enthält aber keinen Spannbaum — **Widerspruch** zur Wahl von $G$. $\square$

**Praktische Relevanz:** Spannbäume sind kantenminimale Netzwerke, die alle Knoten verbinden → nützlich bei teuren Verbindungen (z.B. Netzwerkinfrastruktur).

⚠️ **Achtung:** Der Pfad zwischen zwei Knoten im Spannbaum kann **deutlich länger** sein als der kürzeste Pfad in $G$.

***

## 7. Tiefen- und Breitensuche

### Motivation

Der Existenzbeweis für Spannbäume ist rein existenziell – er liefert keinen Algorithmus. **DFS** und **BFS** sind konstruktive Verfahren, die als Nebeneffekt Spannbäume erzeugen.

### Algorithmus – Tiefensuche (DFS)

**Idee:** Gehe immer so tief wie möglich, bevor du zurückgehst.

```pseudocode
DFS(G, v):
  Definiere T_1 := ({v}, ∅),  I_1(v) := 1
  i := 1
  while i < n:
    Sei w_j für 1 ≤ j ≤ i mit I_i(w_j) = j
    m := max{j : N_G(w_j) \ V(T_i) ≠ ∅}   // tiefster Knoten mit Nachbar außerhalb
    Wähle u ∈ N_G(w_m) \ V(T_i)
    V(T_{i+1}) := V(T_i) ∪ {u}
    E(T_{i+1}) := E(T_i) ∪ {{w_m, u}}
    I_{i+1}(u) := i+1,  I_{i+1}(w_j) := j
    i := i + 1
  return T_n
```

**Schritt-für-Schritt-Beispiel (Graph mit 11 Knoten, Wurzel = 1):**
```
Start: T_1 = ({1}, ∅)

Schritt 1: m = max{j: hat Nachbar außerhalb} = 1 (Knoten w_1 = 1)
           Wähle Nachbar, z.B. 2 → T_2 = ({1,2}, {{1,2}})

Schritt 2: m = max{...} = 2 (Knoten 2 hat noch Nachbarn)
           Wähle Nachbar von 2, z.B. 3 → T_3 = ({1,2,3}, ...)

... (Tiefensuche geht immer tiefer) ...

✅ Ergebnis: Spannbaum T_n mit n Knoten und n-1 Kanten
```

### Algorithmus – Breitensuche (BFS)

**Idee:** Erkunde alle Nachbarn der aktuellen Ebene, bevor du tiefer gehst.

```pseudocode
BFS(G, v):
  Definiere T_1 := ({v}, ∅),  I_1(v) := 1
  i := 1
  while i < n:
    Sei w_j für 1 ≤ j ≤ i mit I_i(w_j) = j
    m := min{j : N_G(w_j) \ V(T_i) ≠ ∅}   // frühester Knoten mit Nachbar außerhalb
    Wähle u ∈ N_G(w_m) \ V(T_i)
    V(T_{i+1}) := V(T_i) ∪ {u}
    E(T_{i+1}) := E(T_i) ∪ {{w_m, u}}
    I_{i+1}(u) := i+1,  I_{i+1}(w_j) := j
    i := i + 1
  return T_n
```

**Kritischer Unterschied zu DFS:**

| Eigenschaft | DFS | BFS |
|---|---|---|
| **Auswahl** | $m = \max\{j : N_G(w_j) \setminus V(T_i) \neq \emptyset\}$ | $m = \min\{j : N_G(w_j) \setminus V(T_i) \neq \emptyset\}$ |
| **Reihenfolge** | Tiefster bekannter Knoten zuerst | Frühester bekannter Knoten zuerst |
| **Kürzeste Pfade** | ❌ Nicht garantiert | ✅ Garantiert |
| **Anwendung** | Zusammenhangskomponenten, Zyklensuche | Kürzeste Wege (ungewichtet) |

**BFS-Eigenschaft (Satz):** Sei $T_v$ der durch BFS in $G$ von $v$ erzeugte Spannbaum. Dann ist für jedes $u \in V(G)$ der Pfad von $v$ nach $u$ in $T_v$ ein **kürzester Pfad** von $v$ nach $u$ in $G$.

> 💡 **Merkhilfe:** DFS = Stack-Verhalten (LIFO – letzter Knoten zuerst weiter). BFS = Queue-Verhalten (FIFO – erster Knoten zuerst weiter).

### Berechnung von Zusammenhangskomponenten

```pseudocode
KomponentenBerechnen(G):
  markiert := ∅
  Komponenten := []
  while es gibt v ∈ V(G) \ markiert:
    T_v := DFS(G, v)         // oder BFS
    Komponenten.add(G[V(T_v)])
    markiert := markiert ∪ V(T_v)
  return Komponenten
```

**Laufzeit:** $O(|V| + |E|)$ — jeder Knoten und jede Kante wird höchstens einmal betrachtet.

***

## 8. Distanzen in Graphen

### Definition – Distanz, Durchmesser, Radius

$$\boxed{\text{dist}_G(u,v) := \min\{\ell : \exists \text{ Pfad der Länge } \ell \text{ von } u \text{ nach } v \text{ in } G\}}$$

$$\text{Durchmesser}(G) := \max\{\text{dist}_G(u,v) : u, v \in V(G)\}$$

$$\text{Radius}(G) := \min_{v \in V(G)} \max\{\text{dist}_G(u,v) : u \in V(G)\}$$

**Beispiel:**
```
Graph G:
1 - 3 - 4 - 7
|       |
2       5 - 6 - 8

dist_G(1, 7) = 3  →  kürzester Pfad: 1 → 3 → 4 → 7
```

> 💡 **Merkhilfe:** Durchmesser = maximale Distanz im Graphen. Radius = wie nah kann man am „Zentrum" des Graphen sein?

⚠️ **BFS liefert kürzeste Pfade!** Deshalb ist BFS der Standard-Algorithmus für ungewichtete Distanzberechnungen.

***

## 9. Mehrfachzusammenhang

### Definition – Schnittknoten und Brücken

$$\boxed{v \in V(G) \text{ ist Schnittknoten} \Leftrightarrow G - v \text{ ist nicht zusammenhängend}}$$

$$\boxed{e \in E(G) \text{ ist Brücke} \Leftrightarrow G - e \text{ ist nicht zusammenhängend}}$$

**Fragen & Antworten:**

1. *Enthält jeder Graph mit einer Brücke auch einen Schnittknoten?*  
   **Ja**, es sei denn, die Brücke verbindet zwei Knoten vom Grad 1.

2. *Enthält jeder Graph mit einem Schnittknoten auch eine Brücke?*  
   **Nein.** (Gegenbeispiel: $K_4$ minus eine Kante kann Schnittknoten ohne Brücke haben.)

### Definition – k-Zusammenhang und Konnektivität

$$\boxed{G \text{ ist } k\text{-zusammenhängend} \Leftrightarrow |G| > k \text{ und } G - X \text{ ist zusammenhängend für alle } X \subseteq V(G) \text{ mit } |X| < k}$$

$$\boxed{\kappa(G) := \max\{k \geq 0 : G \text{ ist } k\text{-zusammenhängend}\}}$$

$\kappa(G)$ heißt **Konnektivität** oder **Zusammenhang** von $G$.

**Zusammenhang vs. k-Zusammenhang:**

| Begriff | Bedeutung |
|---|---|
| **Zusammenhängend** | $\equiv$ 1-zusammenhängend oder isolierter Knoten |
| **1-zusammenhängend** | Entfernen eines beliebigen Knotens $\Rightarrow$ Graph bleibt zusammenhängend |
| **2-zusammenhängend** | Kein Schnittknoten; Entfernen eines Knotens reicht nicht zum Trennen |
| **k-zusammenhängend** | Erst Entfernen von $k$ Knoten kann den Zusammenhang brechen |

**Beobachtung:** Jeder Graph kann eindeutig in seine Zusammenhangskomponenten zerlegt werden, und jede Komponente ist 1-zusammenhängend oder ein isolierter Knoten. Diese 1-zusammenhängenden Komponenten können weiter in ihre 2-zusammenhängenden Teile zerlegt werden.

```
Beispiel:
G = 1-2-3-4-5-6  mit 3 als Schnittknoten:

  1-2     4-5-6
     \   /
      3          ← Schnittknoten: G-3 hat 2 Komponenten

κ(G) = 1
```

⚠️ **Achtung:** Einfacher Zusammenhang garantiert **nicht** Robustheit! Ein einziger Ausfall kann das Netzwerk trennen.

***

## 📌 Zusammenfassung

### Wichtige Konzepte

| Konzept | Bedeutung |
|---|---|
| **Graph $G$** | $(V(G), E(G))$ mit $E \subseteq \mathcal{P}_2[V]$ (ungerichtet) |
| **Grad $\deg_G(v)$** | Anzahl der Nachbarn von $v$ |
| **Handshaking-Lemma** | $\sum_v \deg_G(v) = 2 \cdot \|G\|$ |
| **Pfad** | Weg ohne Knotenwiederholung |
| **Zyklus** | Geschlossener Pfad, $k \geq 2$ |
| **Baum** | Zusammenhängender, azyklischer Graph |
| **Spannbaum** | Aufspannender Teilbaum eines Graphen |
| **DFS** | Tiefensuche: max-Index-Knoten zuerst |
| **BFS** | Breitensuche: min-Index-Knoten zuerst, liefert kürzeste Pfade |
| **Distanz** | Länge des kürzesten Pfades |
| **Schnittknoten / Brücke** | Knoten/Kante, deren Entfernung Zusammenhang zerstört |
| **Konnektivität $\kappa(G)$** | Max. $k$, für das $G$ $k$-zusammenhängend ist |

### Kernaussagen

✅ **Handshaking-Lemma** – Gradsumme = doppelte Kantenzahl; Anzahl Knoten mit ungeradem Grad ist gerade  
✅ **Bäume haben $n-1$ Kanten** – beweisbar durch Induktion unter Nutzung des Blatt-Lemmas  
✅ **Jeder zshg. Graph hat einen Spannbaum** – konstruierbar via DFS oder BFS  
✅ **BFS liefert kürzeste Pfade** – DFS nicht  
⚠️ **Zusammenhang ≠ Robustheit** – ein Schnittknoten genügt, um den Zusammenhang zu zerstören  
❌ **Falsch:** „Jeder Graph mit Schnittknoten hat auch eine Brücke" – stimmt nicht  

### Algorithmen & Formeln

| Algorithmus / Satz    | Kernformel / Eigenschaft                                                |
| --------------------- | ----------------------------------------------------------------------- |
| **Handshaking-Lemma** | $\sum_{v} \deg_G(v) = 2\|G\|$                                           |
| **Kantenanzahl Baum** | $\|T\| = n - 1$ für $T = n$                                             |
| **DFS-Auswahl**       | $m = \max\{j : N_G(w_j) \setminus V(T_i) \neq \emptyset\}$              |
| **BFS-Auswahl**       | $m = \min\{j : N_G(w_j) \setminus V(T_i) \neq \emptyset\}$              |
| **Distanz**           | $\text{dist}_G(u,v) = \min\{\ell : \exists\text{Pfad der Länge }\ell\}$ |
| **Konnektivität**     | $\kappa(G) = \max\{k : G \text{ ist }k\text{-zusammenhängend}\}$        |

***

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.01 Kombinatorik]]: Graphen nutzen Mengenoperationen ($V, E, \mathcal{P}_2$); Äquivalenzrelationen entsprechen Zusammenhangskomponenten
- [[VL.02 Kombinatorik - Bionmialkoeffizient]]: Induktionsbeweise für Baumstruktur (Kantenanzahl, Minimalgrad)
- [[VL.03 Beweise & Bäume]]: Schubfachprinzip im Beweis des Handshaking-Folgesatzes
- [[VL.06 Mehrfachzusammenhang und Rundtouren]]: Euler-Touren, Hamiltonkreise, planare Graphen, Färbung
