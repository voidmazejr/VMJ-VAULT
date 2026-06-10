**Class:** [[DS - Diskrete Strukturen]]
**Date:** 08-05-2026
**Topics:** #InklusionExklusion #Beweis #Schubfachprinzip #HandshakeLemma #Ramsey #Bäume #Binärbäume #Induktion #Kombinatorik #TU-Berlin #DS

---

## 🎯 Lernziele der Vorlesung

VL.03 behandelt den Beweis des Inklusion-Exklusion-Prinzips, einen Exkurs über das Wesen mathematischer Beweise, das Schubfachprinzip mit Anwendungen sowie Grundbegriffe zu Bäumen und Binärbäumen mit Induktionsbeweis.

- **Inklusion-Exklusion (Beweis)**: Jedes Element einer Vereinigung trägt genau den Beitrag 1 zur Summe – gezeigt über Binomialformel
- **Was ist ein Beweis?**: Schrittweise Herleitung aus Axiomen; formale vs. mathematische Beweise
- **Schubfachprinzip**: Wenn $|X| > |Y|$, dann ist keine $f: X \to Y$ injektiv; verallgemeinerte Form
- **Handshake Lemma**: Anwendung des Schubfachprinzips auf Grad-Sequenzen
- **Satz von Ramsey (Spezialfall)**: $R(c,i) = 2^{c+i-1}$; jeder hinreichend große Graph hat Clique oder unabhängige Menge
- **Bäume & Binärbäume**: Definitionen, Höhe, vollständig, balanciert
- **Induktionsbeweis**: Knotenzahl vollständiger balancierter Binärbaum $= 2^{h+1}-1$

---

## 1. Beweis des Inklusion-Exklusion-Prinzips

### Satz (Inklusion-Exklusion)

$$\boxed{\left|\bigcup_{i=1}^{n} A_i\right| = \sum_{r=1}^{n} \left((-1)^{r-1} \sum_{1 \leq i_1 < i_2 < \cdots < i_r \leq n} \left|\bigcap_{j=1}^{r} A_{i_j}\right|\right)}$$

> 💡 **Intuition:** Mengen, die sich überschneiden, werden zu oft gezählt. Das Prinzip korrigiert dies durch abwechselndes Addieren und Subtrahieren der Schnittmengengrößen.

---

### Beweis (Schritt für Schritt)

**Beweisidee:** Sei $a \in \bigcup_{i=1}^n A_i$ beliebig. Links wird $a$ genau **einmal** gezählt. Zu zeigen: auch rechts leistet $a$ genau Beitrag $1$.

**Schritt 1 – Zählargument:**

Angenommen $a$ kommt in $\ell$ der Mengen vor ($\ell \leq n$).

In $\displaystyle\sum_{1 \leq i_1 < \cdots < i_r \leq n} \left|\bigcap_{j=1}^r A_{i_j}\right|$ wird $a$ genau $\binom{\ell}{r}$ mal gezählt.

> **Warum?** $a \in \bigcap_{j=1}^r A_{i_j}$ gdw. $\{i_1,\ldots,i_r\}$ eine $r$-elementige Teilmenge von $\{j : a \in A_j\}$ ist. Diese Menge hat genau $\ell$ Elemente → $\binom{\ell}{r}$ Teilmengen. ✅

**Schritt 2 – Vereinfachung:**

Da $\binom{\ell}{r} = 0$ für $r > \ell$:

$$\sum_{r=1}^{n}(-1)^{r-1}\binom{\ell}{r} = \sum_{r=1}^{\ell}(-1)^{r-1}\binom{\ell}{r}$$

**Schritt 3 – Binomialformel:**

$$\sum_{r=1}^{\ell}(-1)^{r-1}\binom{\ell}{r}$$
$$= -1 \cdot \sum_{r=1}^{\ell}\binom{\ell}{r}(-1)^r \qquad \text{(rausziehen von } {-1}\text{)}$$
$$= -1 \cdot \left(\sum_{r=0}^{\ell}\binom{\ell}{r}(-1)^r - 1\right) \qquad \text{(Index von 0 laufen lassen)}$$
$$= 1 - \sum_{r=0}^{\ell}\binom{\ell}{r}(-1)^r \cdot 1^{\ell-r} \qquad \text{(umformen + } 1^{\ell-r} \text{ hinzu)}$$
$$= 1 - (-1+1)^{\ell} = 1 - 0 = 1 \quad \blacksquare$$

> 💡 **Erinnerung:** $(a+b)^n = \displaystyle\sum_{k=0}^{n}\binom{n}{k}a^k b^{n-k}$

---

## 2. Was ist ein mathematischer Beweis?

### Definition (formaler Beweis)

$$\boxed{\text{Beweis von } A = \text{schrittweise Herleitung aus Voraussetzungen + Axiomen, jeder Schritt überprüfbar}}$$

- Bewiesene Aussagen dürfen als Beweisschritte **wiederverwendet** werden.
- Einsatz in **Theorembeweisern** (Isabelle, Coq, Lean).

### Formale vs. mathematische Beweise

| Eigenschaft | Formaler Beweis | Mathematischer Beweis |
|---|---|---|
| Schrittgröße | Sehr klein | Größere Einzelschritte erlaubt |
| Erklärungsgehalt | Gering | Soll „Warum" erklären |
| Fehleranfälligkeit | Gering | Höher – „Man sieht leicht..." |
| Verwendung | Theorembeweiser | Normale Mathematik |

> ⚠️ **Warnung:** „Man sieht leicht..." ist kein Beweis – Fehler bleiben leicht unentdeckt!

---

## 3. Schubfachprinzip (Pigeonhole Principle)

### Theorem

$$\boxed{(1)\;\; |X| > |Y| \Rightarrow \forall f: X \to Y\; \exists\, y \in Y: |f^{-1}(y)| \geq 2}$$

$$\boxed{(2)\;\; |X| > r \cdot s,\; X \text{ in } r \text{ Klassen} \Rightarrow \text{mind. eine Klasse hat} \geq s+1 \text{ Elemente}}$$

> 💡 **Merkhilfe:** 8 Döner in 7 Tagen → mind. ein Tag mit ≥2 Döner. (PHP = *pigeon-hole principle*)

```

n Personen → n-1 Felder → mind. 2 Personen auf einem Feld ✅

```

---

## 4. Anwendung I: Handshake Lemma

### Lemma

$$\boxed{|M| \geq 2 \Rightarrow \exists\, i \neq j: h_i = h_j}$$

$h_i$ = Anzahl Händeschütteln von $P_i$, mit $0 \leq h_i < n$.

### Beweis

**Schlüsselbeobachtung:** $h_i = 0$ und $h_j = n-1$ können nie gleichzeitig gelten (unmöglich: $P_j$ schüttelt allen die Hand, aber $P_i$ niemandem – Widerspruch!).

Also nehmen die $h_i$ effektiv nur $n-1$ verschiedene Werte an (entweder $\{0,\ldots,n-2\}$ oder $\{1,\ldots,n-1\}$).

```

n Personen, n-1 Felder: Feld 1/0: P mit h=0 oder h=n-1 (zusammengefasst!) Feld 1: P mit h=1 ... Feld n-2: P mit h=n-2

Schubfachprinzip: n > n-1 → mind. 2 Personen auf gleichem Feld ✅

````

---

## 5. Anwendung II: Satz von Ramsey (Spezialfall)

### Satz

$$\boxed{\exists\, R: \mathbb{N} \times \mathbb{N} \to \mathbb{N}: |V| \geq R(c,i) \Rightarrow \text{Clique der Größe } c \;\text{oder}\; \text{unabh. Menge der Größe } i}$$

$$\boxed{R(c,i) = 2^{c+i-1}}$$

### Beweiskonstruktion (Entscheidungsbaum)

```pseudocode
Konstruiere Binärbaum für V = {P₁,...,Pₙ}:
  P₁ belegt Wurzel (obersten freien Platz)
  for i = 2,...,n:
    Pᵢ startet an Wurzel
    while Platz besetzt durch Pⱼ:
      if {Pᵢ,Pⱼ} ∈ E:       // kennen sich
        gehe zum RECHTEN Nachfolger
      else:                   // kennen sich nicht
        gehe zum LINKEN Nachfolger
    Pᵢ belegt den freien Platz
````

**Eigenschaften:**

- Rechter Teilbaum von $v$: alle kennen $v$
- Linker Teilbaum von $v$: niemand kennt $v$

**Folgerung:**

- $c-1$ mal rechts → Clique der Größe $c$ ✅
- $i-1$ mal links → unabhängige Menge der Größe $i$ ✅
- Baumhöhe $\leq c+i-2$
- Max. Knoten: $2^{c+i-1}-1$
- Schubfachprinzip: $|V| \geq 2^{c+i-1}$ → Clique oder unabh. Menge $\blacksquare$

---

## 6. Bäume (Grundbegriffe)

### Definition (Wurzelbaum, informell)

$$\boxed{\text{Wurzelbaum} = \text{Graph mit Wurzel; Knoten haben endlich viele Kinder (Teilbaumwurzeln)}}$$

|Begriff|Definition|
|---|---|
|**Wurzel**|Oberster Knoten|
|**Kind**|Direkter Nachfolger; selbst Wurzel eines Teilbaums|
|**Blatt**|Knoten ohne Nachfolger|
|**Innerer Knoten**|Knoten mit ≥1 Nachfolger|
|**Höhe**|Max. Kantenanzahl auf Wurzel-Blatt-Pfad|

> ⚠️ Ein Baum mit einem Knoten hat Höhe **0**.

```
        [Wurzel]          Höhe = 3
        /       \
    [v₁]        [v₂]
    /   \           \
 [v₃] [v₄]        [v₅]
  /
[Blatt]
```

---

## 7. Binärbäume

### Definition

$$\boxed{\text{Binärbaum: jeder Knoten hat höchstens 2 Nachfolger (links / rechts)}}$$

|Eigenschaft|Definition|
|---|---|
|**vollständig**|Jeder Knoten hat Grad 0 oder 2|
|**balanciert**|Alle Blätter haben denselben Abstand zur Wurzel|

### Satz (Knotenzahl)

$$\boxed{|V| = 2^{h+1}-1 \qquad |\text{Blätter}| = 2^h}$$

für vollständige, balancierte Binärbäume der Höhe $h$.

### Induktionsbeweis

**Induktionsanfang** ($h=0$): $T$ hat 1 Knoten. $2^{0+1}-1 = 1$. ✅

**Induktionsvoraussetzung (IV):** Für alle $j < h$ hat ein vollst. bal. Binärbaum der Höhe $j$ genau $2^{j+1}-1$ Knoten.

**Induktionsschritt** ($h-1 \to h$):

Sei $v$ die Wurzel mit Nachfolgern $s_1, s_2$. Teilbäume $T_1, T_2$ haben Höhe $h-1$.

Nach IV: $|V(T_1)| = |V(T_2)| = 2^h - 1$.

$$|V| = 1 + (2^h-1) + (2^h-1) = 1 + 2^{h+1} - 2 = 2^{h+1}-1 \quad \blacksquare$$

```
        v              ← 1 Knoten
       / \
     T₁   T₂          ← je (2^h - 1) Knoten nach IV
   (h-1) (h-1)

|V| = 1 + 2·(2^h - 1) = 2^{h+1} - 1  ✅
```

---

## 📌 Zusammenfassung

### Wichtige Konzepte

|Konzept|Kernaussage|
|---|---|
|**Inklusion-Exklusion (Beweis)**|Beitrag jedes Elements = 1 via $(−1+1)^\ell = 0$|
|**Mathematischer Beweis**|Schrittweise aus Axiomen; formale vs. math. Beweise|
|**Schubfachprinzip**|$|
|**Handshake Lemma**|$0$ und $n-1$ nie gleichzeitig → $n-1$ Schubfächer für $n$ Personen|
|**Ramsey**|$R(c,i)=2^{c+i-1}$; Entscheidungsbaum-Beweis|
|**Baum**|Höhe = max. Kantenzahl Wurzel–Blatt; Einzelknoten hat Höhe 0|
|**Vollst. bal. Binärbaum**|Höhe $h$ → $2^{h+1}-1$ Knoten, $2^h$ Blätter|

### Kernaussagen

✅ Inklusion-Exklusion korrekt: jedes Element trägt genau 1 bei  
✅ Schubfachprinzip: einfach aber mächtig  
✅ Handshake: $0$ und $n-1$ schließen sich gegenseitig aus  
✅ Ramsey-Beweis: algorithmisch via beschränktem Entscheidungsbaum  
✅ Induktionsbeweis Binärbaum: klassisches Muster IA → IV → IS  
⚠️ „Man sieht leicht..." ist kein gültiger Beweisschritt  
⚠️ Höhe Einzelknoten = 0, nicht 1  
❌ Falsch: vollständig = alle Blätter gleich tief; richtig: jeder Knoten hat 0 oder 2 Kinder

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Kombinatorik - Bionmialkoeffizient]]: Produktregel, Summenregel, IE-Einführung – VL.03 liefert den Beweis
- [[VL.04 Stirling, Catalan Zahlen]]: Bäume als kombinatorische Objekte; Catalan-Zahlen zählen Binärbäume
- [[VL.XX-DS – Graphentheorie]]: Formale Baumdefinition, Handshake Lemma in Graphen
- [[VL.XX-DS – Vollständige Induktion]]: Induktionsprinzip; hier auf Baumstruktur angewendet