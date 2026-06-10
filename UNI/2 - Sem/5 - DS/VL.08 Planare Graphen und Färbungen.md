**Class:** [[DS - Diskrete Strukturen]]  
**Date:** 05-06-2026  
**Topics:** #PlanareGraphen #Färbung #ChromatischeZahl #GerichteteGraphen #Zusammenhangskomponenten #EulerFormel
**Link:** [[VL.08 DS.pdf]]

***

## 🎯 Lernziele der Vorlesung

Diese Vorlesung verlässt die rein abstrakte Sicht auf Graphen und betrachtet ihre **geometrische Darstellung** (planare Zeichnungen), das **Färbungsproblem** sowie die Erweiterung des Modells um **Beschriftungen und Richtungen**.

- **Planare Graphen**: Wann lässt sich ein Graph kreuzungsfrei in die Ebene zeichnen?
- **Eulersche Polyederformel**: Der zentrale Zusammenhang $|F| = |E| - |V| + 2$ und seine Korollare
- **Planaritätskriterien**: $K_5$, $K_{3,3}$ und der Satz von Kuratowski
- **Graphfärbungen**: Knotenfärbung, chromatische Zahl $\chi(G)$ und Anwendungen
- **Degenerierte Graphen**: Verallgemeinerung der Färbbarkeit planarer Graphen
- **Gerichtete & beschriftete Graphen**: Modell, Erreichbarkeit, starke/schwache Zusammenhangskomponenten

***

## 1. Zeichnen von Graphen

### Motivation

Bisher dienten Graphen als **mathematische Abstraktion** zur Lösung algorithmischer Probleme. Eine andere wichtige Anwendung ist die **Strukturierung und Visualisierung** von Zusammenhängen in Daten.

- **Graphzeichnen**: Wie zeichnet man Graphen so, dass ihre Struktur leicht erkennbar ist?
- **Färben von Graphen**: Knoten sollen so farblich markiert werden, dass *benachbarte* Knoten verschiedene Farben erhalten — mit möglichst wenigen Farben.

> [!example] **Anwendungsbeispiele**
> Landkarten (Färbung), aber auch **Scheduling**-Probleme, Mobilfunk-Frequenzen und Registerzuweisung im Compilerbau.

### Zeichnungen in der Ebene

Wir betrachten Zeichnungen „auf einem Blatt Papier“, also Zeichnungen des Graphen im $\mathbb{R}^2$. Formal:
- jedem Knoten $v \in V(G)$ wird ein Punkt $\pi(v) \in \mathbb{R}^2$ zugeordnet,
- jede Kante $e = \{u,v\} \in E(G)$ wird durch eine Verbindungslinie dargestellt.

**Gewünschte Eigenschaften:**
- Kanten werden durch „einfache“ Kurven dargestellt (kein Selbstschnitt).
- Die Kurve einer Kante $\{u,v\}$ läuft durch keinen anderen Knoten $x \in V(G) \setminus \{u,v\}$.
- Idealerweise schneiden sich zwei Kanten nicht.

***

## 2. Planare Graphen

### Definition (Zeichnung / Einbettung)

$$\boxed{\text{Zeichnung } \pi: \begin{cases} v \in V(G) \mapsto \pi(v) \in \mathbb{R}^2 \\ e=\{u,v\} \in E(G) \mapsto \pi(e) \subseteq \mathbb{R}^2 \end{cases}}$$

Die Kurve $\pi(e)$ verbindet $\pi(u)$ mit $\pi(v)$ und enthält **keinen** weiteren Knotenpunkt $\pi(x)$ mit $x \in V(G) \setminus \{u,v\}$.

### Definition (Planare Einbettung / planar)

> [!abstract] **Eben (plane) und planar**
> Eine Zeichnung $\pi$ heißt **eben** (engl. *plane*), wenn es keine zwei Kanten $e \ne f \in E(G)$ gibt, deren Kurven $\pi(e)$ und $\pi(f)$ einen gemeinsamen Punkt haben, der **kein** gemeinsamer Endpunkt ist.

$$\boxed{G \text{ ist } \textbf{planar} \iff G \text{ besitzt eine ebene Einbettung}}$$

### Definition (Gebiete / Faces)

Die **Gebiete** einer Zeichnung $\pi$ sind die maximalen zusammenhängenden Teile von $\Sigma := \mathbb{R}^2$, die keinen Punkt einer Kante oder eines Knotens enthalten.

> [!info] **Merkhilfe**
> Ein Gebiet ist eine durch die Zeichnung „eingeschlossene Fläche“. **Wichtig:** Auch das *unbeschränkte äußere* Gebiet zählt mit!

***

## 3. Ein nicht-planarer Graph: $K_{3,3}$

> [!failure] **Behauptung**
> Der Graph $K_{3,3} := \big(\{a_1,a_2,a_3,b_1,b_2,b_3\},\ \{\{a_i,b_j\} : 1 \le i,j \le 3\}\big)$ ist **nicht planar**.

**Beweisskizze (Widerspruch):** Angenommen, $K_{3,3}$ hätte eine ebene Zeichnung.
1. Dann müsste der Kreis $(a_1, b_1, a_2, b_2)$ in die Ebene gezeichnet werden → er teilt die Ebene in zwei Gebiete.
2. Der Pfad $(a_1, b_3, a_2)$ muss in **einem** der beiden Gebiete liegen.
3. Danach gibt es **kein** Gebiet mehr, das $b_1, b_2, b_3$ gemeinsam im Rand hat.
4. Da $a_3$ mit $b_1, b_2, b_3$ benachbart ist, kann $a_3$ **nirgendwo** mehr gezeichnet werden. $\Rightarrow$ Widerspruch.

***

## 4. Beobachtungen über Gebiete

> [!note] **Lemma (Kanten und Gebietsränder)**
> Sei $G$ planar, $\pi$ eine ebene Einbettung in $\mathbb{R}^2$ und $e \in E(G)$.
> 1. Sei $F$ ein Gebiet von $\pi$ mit Rand $R$. Dann gilt $\pi(e) \subseteq R$, **oder** $\pi(e) \cap R \subseteq \{\pi(v) : v \in V(G)\}$, **oder** $\pi(e) \cap R = \emptyset$.
> 2. Liegt $e$ auf einem **Kreis** $C \subseteq G$, dann liegt $e$ auf dem Rand von **genau zwei** Gebieten.
> 3. Liegt $e$ auf **keinem** Kreis, dann liegt $e$ auf dem Rand von **genau einem** Gebiet.

**Zwei Leitfragen:**
- [?] Wieviele Gebiete hat die ebene Einbettung $\pi$ eines **Baums** $T$?
  → $\pi(T)$ hat **genau ein** Gebiet (keine Kante liegt auf einem Kreis).
- [?] Wenn bei zusammenhängendem $G$ zwei *verschiedene* Gebiete den **gleichen** Rand haben — was folgt?
  → Dann ist $G$ ein **Kreis**.

***

## 5. Eulersche Polyederformel

> [!success] **Satz (Eulersche Polyederformel)**
> Sei $G$ ein **zusammenhängender, planarer** Graph und $\pi$ eine ebene Zeichnung von $G$ in $\mathbb{R}^2$. Sei $F$ die Menge der Gebiete von $\pi$. Dann gilt:

$$\boxed{|F| = |E(G)| - |V(G)| + 2}$$

> [!quote] **Erinnerung (Bäume)**
> Jeder Baum $T$ mit $n \ge 1$ Knoten hat genau $n-1$ Kanten. Jeder zusammenhängende Graph enthält einen Spannbaum, also $\ge n-1$ Kanten. Somit: ein zusammenhängender Graph $G$ ist **genau dann** ein Baum, wenn $|E(G)| = |V(G)| - 1$.

### Beweis (Induktion über $m := |E(G)|$, festes $n := |V(G)|$)

Da $G$ zusammenhängend ist, gilt $m \ge n - 1$.

**(IA) Basisfall $m = n-1$:** $G$ ist ein Baum, also hat jede ebene Zeichnung genau ein Gebiet:
$$|F| = 1 = |E(G)| - |V(G)| + 2 = (n-1) - n + 2.$$

**(IS) Induktionsschritt $m \ge n$:** *(IV: Aussage gilt für alle kleineren $m$.)*
- $G$ enthält einen Kreis $C \subseteq G$. Wähle eine beliebige Kante $e$ von $C$, setze $G' := G - e$.
- Sei $\pi'$ die Einbettung ohne $e$. Da $e$ auf einem Kreis liegt, grenzt $e$ an **zwei** Gebiete, die in $\pi'$ zu **einem** verschmelzen ⇒ $|F'| = |F| - 1$.
- Mit $|V(G')| = |V(G)|$, $|E(G')| = |E(G)| - 1$ und (IV):
$$|F'| = |E(G')| - |V(G')| + 2 = (m-1) - n + 2 = m - n + 1.$$
- Also $|F| = |F'| + 1 = m - n + 2 = |E(G)| - |V(G)| + 2.$ $\square$

***

## 6. Korollare der Eulerformel

### Kantenschranke

> [!success] **Korollar (Kantenobergrenze)**
> Für jeden planaren Graphen $G$ mit $|V(G)| \ge 3$ gilt:

$$\boxed{|E(G)| \le 3\,|V(G)| - 6}$$

**Beweis:** O.B.d.A. $G$ zusammenhängend.
- Falls $G$ drei Knoten, aber nur 2 Kanten hat, ist die Aussage klar.
- Andernfalls wird jedes Gebiet von $\ge 3$ Kanten begrenzt, und jede Kante begrenzt $\le 2$ Gebiete: $3|F| \le 2|E(G)|$.
- Mit der Eulerformel: $\tfrac{2}{3}|E(G)| \ge |F| = |E(G)| - |V(G)| + 2 \Rightarrow |E(G)| \le 3|V(G)| - 6.$ $\square$

### Minimalgrad

> [!success] **Korollar (Knoten kleinen Grades)**
> Jeder planare Graph hat einen Knoten vom Grad **höchstens 5**.

**Beweis (Widerspruch):** Angenommen $\delta(G) \ge 6$, d.h. jeder Knoten hat $\ge 6$ Nachbarn. Dann
$$|E(G)| \ge \frac{6 \cdot |V(G)|}{2} = 3\,|V(G)|,$$
im Widerspruch zu $|E(G)| \le 3|V(G)| - 6$.

### $K_5$ ist nicht planar

> [!failure] **Korollar**
> $K_5$ ist **nicht planar**: Mit $|V| = 5$, $|E| = 10$ wäre $10 \le 3\cdot 5 - 6 = 9$ nötig — falsch.

***

## 7. Kombinatorische Planaritätskriterien

### Minimale Nicht-Planarität & Abschluss

> [!tip] **Beobachtungen**
> - $K_5$ und $K_{3,3}$ sind **minimal nicht-planar**: Löscht man eine beliebige Kante *oder* einen Knoten, wird das Ergebnis planar.
> - **Abschluss unter Teilgraphen**: Ist $G$ planar und $H \subseteq G$, dann ist auch $H$ planar.

### Definition (Unterteilung / Subdivision)

Eine **Unterteilung** (engl. *subdivision*) von $G$ ist ein Graph $G'$, den man aus $G$ erhält, indem man eine oder mehrere Kanten durch **Pfade beliebiger Länge $> 0$** ersetzt. Dabei haben die Pfade verschiedener Kanten keinen inneren Knoten gemeinsam.

### Satz von Kuratowski

> [!success] **Satz (Kuratowski, 1930)**
> $$\boxed{G \text{ planar} \iff G \text{ enthält weder eine Unterteilung von } K_5 \text{ noch von } K_{3,3} \text{ als Teilgraph}}$$

> [!info] **Rolle**
> Kuratowski liefert eine rein **kombinatorische** Charakterisierung der Planarität — ganz ohne Bezug auf eine konkrete Zeichnung.

***

## 8. Färbungen von Graphen

### Definition (Knotenfärbung & $k$-färbbar)

Eine **Knotenfärbung** von $G$ mit $k$ Farben ist eine Abbildung
$$\boxed{c : V(G) \to \{1, \dots, k\}, \quad c(u) \ne c(v)\ \text{ für alle } \{u,v\} \in E(G)}$$
$G$ heißt **$k$-färbbar**, wenn es eine Färbung mit $k$ Farben gibt.

### Definition (Chromatische Zahl)

$$\boxed{\chi(G) := \min\{ k : G \text{ ist } k\text{-färbbar}\}}$$

### Beispiele

| Graph                        | Färbbarkeit                                  |
| ---------------------------- | -------------------------------------------- |
| **Clique** $K_n$             | $n$-färbbar, aber **nicht** $(n-1)$-färbbar  |
| **Vollst. bipartit** $K_{n,m}$ | $2$-färbbar                                |
| **Kreis** $C_n$, $n$ gerade  | $2$-färbbar                                  |
| **Kreis** $C_n$, $n$ ungerade | $3$-färbbar, aber **nicht** $2$-färbbar     |

$$\chi(C_n) = \begin{cases} 2 & \text{falls } n \text{ gerade} \\ 3 & \text{falls } n \text{ ungerade} \end{cases} \quad (n \ge 3)$$

### Anwendungen

- **Lagern von Chemikalien**: Knoten = Chemikalien; Kante = „dürfen nicht zusammen gelagert werden“. Dann ist $\chi(G)$ die minimale Anzahl getrennter Lagerbereiche.
- **Mobilfunk**: Zuordnung von Frequenzen zu Sendern, sodass benachbarte Sender verschiedene Frequenzen nutzen.
- **Compilerbau**: Zuordnung von Variablen zu Registern, sodass gleichzeitig benutzte Variablen in verschiedenen Registern liegen (Register-Allocation).

***

## 9. Färbbarkeit: Sätze & Komplexität

### 2-Färbbarkeit

> [!note] **Lemma (Erinnerung)**
> $G$ ist genau dann **$2$-färbbar**, wenn er **keinen Kreis ungerader Länge** als Teilgraph enthält. Der Beweis liefert direkt einen **effizienten** Algorithmus zur Entscheidung der 2-Färbbarkeit.

### Färbbarkeit planarer Graphen

> [!success] **Beobachtung**
> Jeder planare Graph ist **6-färbbar**.

**Beweisidee (Rekursion):** Sei $G$ planar.
1. $G$ hat einen Knoten $v$ mit $\deg_G(v) \le 5$.
2. $G - v$ ist planar und wird rekursiv mit $\{1,\dots,6\}$ gefärbt.
3. Da $v$ nur $\le 5$ Nachbarn hat, bleibt in $N_G(v)$ eine Farbe $c \in \{1,\dots,6\}$ frei.
4. Färbe $v$ mit $c$. $\square$

> [!success] **Satz (Appel & Haken, 1977 — Vierfarbensatz)**
> Jeder planare Graph ist **4-färbbar**.

### Komplexität der Färbung

| Problem ($k$-Färbbarkeit)        | Komplexität                               |
| -------------------------------- | ----------------------------------------- |
| $k = 2$ (allgemeine Graphen)     | in **Polynomialzeit** entscheidbar        |
| $k > 2$ (allgemeine Graphen)     | **NP-vollständig**                        |

Für **planare** Graphen speziell:

$$\text{$k$-Färbbarkeit planarer Graphen} = \begin{cases} \text{einfach} & k = 1,\ k = 2 \\ \text{schwer} & k = 3 \\ \text{einfach} & k \ge 4 \ (\text{Vierfarbensatz!}) \end{cases}$$

> [!warning] **Achtung**
> $\chi(G)$ allgemein zu berechnen ist für $k > 2$ algorithmisch sehr schwer (NP-vollständig) — **selbst für planare Graphen** im Fall $k=3$.

***

## 10. Degenerierte Graphen

> [!abstract] **Kernidee**
> Im Beweis der 6-Färbbarkeit wurde gar nicht die Planarität direkt genutzt, sondern nur: *„$G$ besitzt einen Knoten vom Grad $\le 5$, und diese Eigenschaft bleibt beim Löschen erhalten.“* Das verallgemeinert man:

### Definition ($r$-degeneriert)

$$\boxed{G \text{ ist } r\text{-degeneriert} \iff \text{jeder Teilgraph } H \subseteq G \text{ hat einen Knoten } v \text{ mit } \deg_H(v) \le r}$$

> [!success] **Lemma**
> Jeder $r$-degenerierte Graph ist **$(r+1)$-färbbar**, und eine $(r+1)$-Färbung kann **effizient** berechnet werden (gleicher rekursiver Algorithmus wie bei planaren Graphen).

> [!info] **Zusammenhang**
> Jeder planare Graph ist $5$-degeneriert (Minimalgrad $\le 5$), also $6$-färbbar — genau die Beobachtung von oben.

***

## 11. Beschriftete Graphen

In vielen Anwendungen liegen zusätzlich zur Graphstruktur Informationen über Kanten/Knoten vor (z.B. Straßenlängen in Karten).

### Definition (Kanten- & knotenbeschrifteter Graph)

$$\boxed{(V, E, \lambda_V, \lambda_E) \quad \text{mit } \lambda_V : V \to D_V,\ \ \lambda_E : E \to D_E}$$
wobei $(V,E)$ ein Graph ist und $\lambda_V, \lambda_E$ **Beschriftungsfunktionen** in Wertebereiche $D_V, D_E$ sind.

> [!example] **Beispiel**
> $V := \{1,2,3,4,5\}$, $\lambda_V(1)=\text{Das}$, $\lambda_V(2)=\text{ist}$, $\lambda_V(3)=\text{ein}$, $\lambda_V(4)=\text{kleines}$, $\lambda_V(5)=\text{Haus}$ — ein Graph als Träger sprachlicher Information.

***

## 12. Gerichtete Graphen

### Definition

Ein **gerichteter Graph** $G$ besteht aus einer Knotenmenge $V(G)$ und einer Menge gerichteter Kanten:
$$\boxed{E(G) \subseteq V(G) \times V(G)}$$
Eine Kante $e = (u,v)$ ist eine **ausgehende** Kante von $u$ und eine **eingehende** Kante von $v$.

### Nachbarschaften und Grade

| Begriff                  | Definition                                                |
| ------------------------ | --------------------------------------------------------- |
| Ausgehende Nachbarschaft | $N_G^+(v) := \{u \in V(G) : (v,u) \in E(G)\}$             |
| Eingehende Nachbarschaft | $N_G^-(v) := \{u \in V(G) : (u,v) \in E(G)\}$             |
| Ausgangsgrad             | $\deg_G^+(v) := \lvert N_G^+(v) \rvert$                  |
| Eingangsgrad             | $\deg_G^-(v) := \lvert N_G^-(v) \rvert$                  |

### Gerichtete Wege & Pfade

Ein **gerichteter Weg** ist eine Folge
$$W = (s_1, e_1, \dots, s_k, e_k, s_{k+1}), \quad e_i = (s_i, s_{i+1}),$$
mit Länge $k$ (Anzahl der Kanten). Gilt zusätzlich $s_i \ne s_j$ für alle $i < j$, so ist $W$ ein **gerichteter Pfad**. $s_1$ ist **Start-**, $s_{k+1}$ **Zielknoten**.

> [!example] **Anwendung: Endliche Automaten**
> Ein Automat akzeptiert ein Wort $w = w_1 \dots w_n$, wenn es einen gerichteten, mit $w$ beschrifteten Weg von einem **Startzustand** zu einem **Endzustand** gibt.

***

## 13. Zusammenhang in gerichteten Graphen

### Definitionen

- **Erreichbarkeit**: $u$ ist von $v$ aus erreichbar, wenn ein gerichteter Pfad in $v$ beginnt und in $u$ endet.
- **Stark zusammenhängend**: jeder Knoten ist von jedem anderen erreichbar.
- **Schwach zusammenhängend**: der zugrundeliegende **ungerichtete** Graph $H$ mit $V(H) = V(G)$ und $E(H) = \{\{u,v\} : (u,v) \in E(G)\}$ ist zusammenhängend.

$$\boxed{\text{Zusammenhangskomponente} = \text{maximaler stark/schwach zusammenhängender Teilgraph}}$$

```mermaid
%%{init: {'theme':'base', 'themeVariables': {
'primaryColor':'#EEE6DD',
'primaryBorderColor':'#6E5E4C',
'primaryTextColor':'#3A332B',
'lineColor':'#6E5E4C',
'secondaryColor':'#EEE6DD',
'tertiaryColor':'#EEE6DD'
}}}%%
graph LR
  A((a)) --> B((b))
  B --> C((c))
  C --> A
  C --> D((d))
  D --> E((e))
  E --> D
  subgraph SCC1[Starke Komp. 1]
    A; B; C
  end
  subgraph SCC2[Starke Komp. 2]
    D; E
  end
````

---

## 14. Berechnen starker Zusammenhangskomponenten

Die starken Zusammenhangskomponenten lassen sich durch eine **zweifache Tiefensuche** berechnen.

### Gerichtete Tiefensuche (Post-Order)

> [!info] **Idee der Nummerierung** Werden von $v$ aus die Nachfolger $u_1, \dots, u_l$ besucht, erhalten diese **kleinere** Nummern als $v$ (Post-Order-Nummerierung).

```
Eingabe: gerichteter Graph G
Datenstrukturen:
   globaler Zähler c = 1
   Abbildung m : V(G) -> N   (initial: alle v nicht besucht)

Algorithmus:
   Solange es nicht besuchten v in V(G) gibt:
       wähle nicht besuchten v und führe rec-DFS(v) aus

rec-DFS(v):
   markiere v als besucht
   für jeden nicht besuchten Nachbarn u in N+(v):
       rec-DFS(u)
   setze m(v) = c;  c = c + 1
```

### Eigenschaften der Nummerierung

> [!success] **Eigenschaften**
> 
> - Wenn $u$ von $v$, aber $v$ **nicht** von $u$ erreichbar ist, dann gilt $m(v) > m(u)$.
> - Wenn $m(u) = 1$, dann sind die von $u$ erreichbaren Knoten **genau** die Knoten der Zusammenhangskomponente von $u$.

---

## 📌 Zusammenfassung

### Wichtige Konzepte

|Konzept|Bedeutung|
|---|---|
|**Planar**|besitzt eine kreuzungsfreie (ebene) Einbettung in $\mathbb{R}^2$|
|**Gebiet (Face)**|maximale zusammenhängende Fläche ohne Kanten/Knoten (inkl. äußerem)|
|**Eulerformel**|$\lvert F\rvert = \lvert E\rvert - \lvert V\rvert + 2$|
|**Kuratowski**|planar $\iff$ keine Unterteilung von $K_5$ oder $K_{3,3}$|
|**$\chi(G)$**|minimale Farbzahl einer gültigen Knotenfärbung|
|**$r$-degeneriert**|jeder Teilgraph hat Knoten mit Grad $\le r$ $\Rightarrow (r{+}1)$-färbbar|
|**Stark zhgd.**|jeder Knoten von jedem anderen erreichbar|

### Kernaussagen

- [p] **$|E| \le 3|V| - 6$** – Direkte Folge der Eulerformel für planare Graphen ($|V|\ge 3$)
- [p] **Jeder planare Graph** hat einen Knoten vom Grad $\le 5$ und ist damit 6-färbbar
- [p] **Vierfarbensatz (Appel & Haken)** – planare Graphen sind sogar 4-färbbar
- [!] **Achtung:** Das äußere (unbeschränkte) Gebiet zählt bei der Eulerformel mit!
- [c] **Falsch:** „2-färbbar = bipartit“ ohne Bedingung – korrekt ist: 2-färbbar $\iff$ kein **ungerader** Kreis
- [!] **NP-vollständig:** $k$-Färbbarkeit für $k>2$ – bei planaren Graphen ist $k=3$ schwer, $k\ge 4$ wieder leicht

### Wichtige Sätze & Schranken

|Satz / Größe|Aussage|Bedingung|
|---|---|---|
|**Eulersche Polyederformel**|$\lvert F\rvert=\lvert E\rvert-\lvert V\rvert+2$|$G$ zshgd., planar|
|**Kantenschranke**|$\lvert E\rvert\le 3\lvert V\rvert-6$|$\lvert V\rvert\ge 3$, planar|
|**$\chi(K_n)$**|$= n$|vollständiger Graph|
|**$\chi(K_{n,m})$**|$= 2$|bipartit|
|**$\chi(C_n)$**|$2$ (gerade) / $3$ (ungerade)|$n \ge 3$|
|**SCC-Berechnung**|zweifache Tiefensuche|gerichteter Graph|

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.07 Matching]]: Bäume, Spannbäume und Kreise – Grundlage für den Induktionsbeweis der Eulerformel
- [[VL.06 Mehrfachzusammenhang und Rundtouren]]: Grundlagen ungerichteter Graphen, Grad, Nachbarschaft und Zusammenhang
- [[VL.07 Graphen, Tiefen- & Breitensuche, Topologische Sortierung]]: Gerichtete DFS mit Post-Order als Baustein der SCC-Berechnung
- [[Komplexitätstheorie]]: NP-Vollständigkeit der $k$-Färbbarkeit