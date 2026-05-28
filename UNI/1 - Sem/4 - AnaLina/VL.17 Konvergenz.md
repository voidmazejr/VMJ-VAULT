**Class:** [[AnaLina]]  
**Date:** 10-01-2026  
**Topics:** #Folgen #Konvergenz #Grenzwert #Nullfolge #BestimmteDivergenz #Beschränktheit

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung führt Folgen und den zentralen Begriff der Konvergenz ein – ein fundamentales Konzept der Analysis. Konvergenz beschreibt das Verhalten von Folgen "für $n \to \infty$".

- **Definition** von Zahlenfolgen (explizit und rekursiv)
- **Beschränktheit und Monotonie** von Folgen
- **Konvergenz** und der $\varepsilon$-$N$-Formalismus
- **Grenzwert** als eindeutig bestimmter Wert
- **Eigenschaften** konvergenter Folgen
- **Bestimmte Divergenz** gegen $\pm\infty$

---

## 1. Zahlenfolgen

### Definition

Eine **Folge reeller Zahlen** ist eine Abbildung:

$$\mathbb{N} \to \mathbb{R}, \quad n \mapsto a_n$$

**Schreibweisen:** $(a_n)_{n \in \mathbb{N}}$ oder $(a_0, a_1, a_2, \ldots)$ oder kurz $(a_n)_n$ oder $(a_n)$

- Das Element $a_n$ heißt **$n$-tes Folgenglied**
- $n$ heißt der zugehörige **Index**

**Bemerkungen:**
- Der Indexname ist unerheblich: $(a_n)_n = (a_k)_k = (a_j)_j$
- Allgemeiner: Folgen $(a_n)_{n \geq n_0}$ für beliebiges $n_0 \in \mathbb{Z}$
- Analog: **Folgen komplexer Zahlen** $\mathbb{N} \to \mathbb{C}$, $n \mapsto a_n$ mit $a_n \in \mathbb{C}$

### Explizite Definition

Die Folgenglieder sind durch eine direkte Formel gegeben.

**Beispiele:**

1. **Konstante Folge:** $a_n = c$ für ein $c \in \mathbb{R}$  
   → $c, c, c, \ldots$  
   Schreibweise: $(c)_n$

2. $a_n = \frac{1}{2^n}$  
   → $1, \frac{1}{2}, \frac{1}{4}, \frac{1}{8}, \ldots$

3. $a_n = \frac{1}{n}$ für $n \geq 1$  
   → $1, \frac{1}{2}, \frac{1}{3}, \frac{1}{4}, \ldots$

4. $a_n = \frac{(-1)^n}{n}$ für $n \geq 1$  
   → $-1, \frac{1}{2}, -\frac{1}{3}, \frac{1}{4}, \ldots$

5. $a_n = (-1)^n$  
   → $1, -1, 1, -1, \ldots$

### Rekursive Definition

Ein Folgenglied hängt von einem (oder mehreren) Vorgänger(n) ab.

**Beispiele:**

1. **Fakultät:** $a_1 = 1$, $a_{n+1} = (n+1) \cdot a_n$ für $n \geq 1$  
   → $1, 2, 6, 24, 120, \ldots$

2. **Fibonacci-Folge:** $a_0 = 0$, $a_1 = 1$, $a_{n+2} = a_{n+1} + a_n$ für $n \geq 0$  
   → $0, 1, 1, 2, 3, 5, 8, 13, 21, 34, \ldots$  
   (Modelliert Vermehrung unsterblicher Kaninchen)

---

## 2. Beschränktheit und Monotonie

### Definitionen

Die Folge $(a_n)_{n \in \mathbb{N}}$ heißt:

**Beschränktheit:**

1. **Nach unten beschränkt**, wenn es eine Zahl $m \in \mathbb{R}$ gibt mit $m \leq a_n$ für alle $n \in \mathbb{N}$

2. **Nach oben beschränkt**, wenn es eine Zahl $m \in \mathbb{R}$ gibt mit $a_n \leq m$ für alle $n \in \mathbb{N}$

3. **Beschränkt**, wenn es eine Zahl $M \in \mathbb{R}$ gibt mit $|a_n| \leq M$ für alle $n \in \mathbb{N}$

**Monotonie:**

4. **Monoton wachsend**, wenn $a_n \leq a_{n+1}$ für alle $n \in \mathbb{N}$

5. **Streng monoton wachsend**, wenn $a_n < a_{n+1}$ für alle $n \in \mathbb{N}$

6. **Monoton fallend**, wenn $a_n \geq a_{n+1}$ für alle $n \in \mathbb{N}$

7. **Streng monoton fallend**, wenn $a_n > a_{n+1}$ für alle $n \in \mathbb{N}$

Wir sagen kurz **(streng) monoton**, wenn die Folge (streng) monoton wachsend oder (streng) monoton fallend ist.

### Unterschied zu Funktionen

Bei Folgen (definiert auf $\mathbb{N}$) reicht es, **zwei aufeinanderfolgende Punkte** ($n$ und $n+1$) zu betrachten.

Bei Funktionen (definiert auf einem Intervall) gibt es nicht "die nächste" reelle Zahl – daher müssen **beliebige Punkte** $x < y$ verglichen werden.

### Beispiele

1. $a_n = n$: **(streng) monoton wachsend**, nach unten beschränkt ($a_n \geq 0$), **nicht** nach oben beschränkt

2. $a_n = \frac{1}{n}$ (für $n \geq 1$): **(streng) monoton fallend**, beschränkt ($0 \leq a_n \leq 1$)

3. $a_n = (-1)^n$: **beschränkt** ($|a_n| = 1$), **nicht monoton**

### Beobachtung

- Eine **monoton wachsende** Folge ist nach unten durch $a_0$ beschränkt
- Eine **monoton fallende** Folge ist nach oben durch $a_0$ beschränkt

---

## 3. Konvergenz

### Definition

Sei $(a_n)_n$ eine Folge reeller Zahlen. Die Folge heißt **konvergent gegen** $a \in \mathbb{R}$, falls gilt:

**Für alle** $\varepsilon > 0$ **existiert ein** $N_\varepsilon \in \mathbb{N}$, so dass für alle $n \geq N_\varepsilon$ gilt:

$$|a_n - a| < \varepsilon$$

Die Zahl $a$ heißt der **Grenzwert** (oder **Limes**) der Folge.

**Schreibweisen:**
- $\lim_{n \to \infty} a_n = a$
- "$a_n \to a$ für $n \to \infty$"
- Kurz: "$a_n \to a$"

**Terminologie:**
- Die Folge $(a_n)_n$ heißt **konvergent**, falls $(a_n)_n$ einen Grenzwert hat
- Die Folge $(a_n)_n$ heißt **divergent**, falls sie nicht konvergent ist
- Eine Folge, die gegen Null konvergiert, heißt **Nullfolge**

### Interpretation

Die Folge $(a_n)_n$ konvergiert gegen $a \in \mathbb{R}$ bedeutet:

Für jede (noch so kleine) **Toleranz** $\varepsilon > 0$ liegen alle bis auf endlich viele Folgenglieder (nämlich höchstens die mit $n < N_\varepsilon$) im Intervall $]a - \varepsilon, a + \varepsilon[$.

### Visualisierung: Zahlengerade

![[Screenshot 2026-01-09 at 15.59.09.png]]
### Visualisierung: ε-Schlauch

![[Screenshot 2026-01-09 at 15.59.30.png]]

### Beispiele

**Beispiel 1: Nullfolge**

Die Folge $\left(\frac{1}{n}\right)_{n \geq 1}$ konvergiert gegen $0$:

$$\lim_{n \to \infty} \frac{1}{n} = 0$$

**Beweis:** Sei $\varepsilon > 0$ beliebig. Wähle $N_\varepsilon \in \mathbb{N}$ mit $N_\varepsilon > \frac{1}{\varepsilon}$.

Dann gilt für alle $n \geq N_\varepsilon$:

$$\left|\frac{1}{n} - 0\right| = \frac{1}{n} \leq \frac{1}{N_\varepsilon} < \varepsilon$$ 

**Beispiel 2: Konstante Folge**

Die konstante Folge $c, c, c, \ldots$ konvergiert gegen $c$.

**Beispiel 3: Divergente Folge**

Die Folge $((-1)^n)_n = (1, -1, 1, -1, \ldots)$ ist **divergent**.

**Beweis durch Widerspruch:** Angenommen, die Folge konvergiert gegen $a \in \mathbb{R}$.

Zu $\varepsilon = 1$ gibt es dann $N \in \mathbb{N}$ mit $|a_n - a| < 1$ für alle $n \geq N$.

Dann gilt insbesondere:
$$|a_N - a_{N+1}| = |a_N - a + a - a_{N+1}| \leq |a_N - a| + |a_{N+1} - a| < 1 + 1 = 2$$

Andererseits ist aber:
$$|a_N - a_{N+1}| = |(-1)^N - (-1)^{N+1}| = |(-1)^N + (-1)^N| = 2$$

Dies ergibt den Widerspruch $2 < 2$ ✗

Also ist die Annahme falsch → $((-1)^n)_n$ ist divergent ✓

---

## 4. Eigenschaften konvergenter Folgen

### Hauptsätze

**Satz:** 

1. Der Grenzwert einer konvergenten Folge ist **eindeutig**

2. Konvergente Folgen sind **beschränkt**

3. Unbeschränkte Folgen sind **divergent**

### Beweis-Skizzen

**Beweis von (1) – Eindeutigkeit:**

Angenommen, $(a_n)_n$ hat zwei verschiedene Grenzwerte $a \neq a'$.

Setze $\varepsilon = \frac{|a - a'|}{2} > 0$.

Dann existiert $N_\varepsilon \in \mathbb{N}$, so dass $|a_n - a| < \varepsilon$ für alle $n \geq N_\varepsilon$.

Das bedeutet: Fast alle Folgenglieder liegen in $]a - \varepsilon, a + \varepsilon[$.

Damit können höchstens endlich viele Folgenglieder in $]a' - \varepsilon, a' + \varepsilon[$ liegen.

**Widerspruch** zur Annahme, dass die Folge auch gegen $a'$ konvergiert ✗

```
    a-ε    a    a+ε        a'-ε   a'   a'+ε
     │─────┼─────│          │─────┼─────│
     └─────┴─────┘          └─────┴─────┘
      Fast alle aₙ      Höchstens endlich viele
```

Also ist die Annahme falsch → Der Grenzwert ist eindeutig ✓

**Beweis von (2) – Beschränktheit:**

Sei $(a_n)_{n \geq n_0}$ konvergent gegen $a \in \mathbb{R}$.

Zu $\varepsilon = 1$ gibt es $N \in \mathbb{N}$ mit $|a_n - a| < 1$ für alle $n \geq N$.

Dann ist:
$$|a_n| = |a_n - a + a| \leq |a_n - a| + |a| < 1 + |a| \text{ für } n \geq N$$

Wähle $M := \max\{|a_{n_0}|, |a_{n_0+1}|, \ldots, |a_{N-1}|, 1 + |a|\}$.

Dann gilt $|a_n| \leq M$ für alle $n \geq n_0$ → Folge ist beschränkt 

**Beweis von (3):** Folgt aus (2) durch Kontraposition 

### Wichtige Bemerkung

**Die Umkehrung von (2) gilt NICHT:**

Es gibt beschränkte Folgen, die nicht konvergieren.

**Beispiel:** $((-1)^n)_n$ ist beschränkt ($|a_n| = 1$), aber **nicht konvergent**.

### Beispiele für Divergenz

Die folgenden Folgen sind **unbeschränkt**, also **divergent**:
- $a_n = n$
- $b_n = (-1)^n \cdot n$
- $c_n = n^2$

---

## 5. Bestimmte Divergenz

### Definition

Eine reelle Zahlenfolge $(a_n)_n$ heißt:

**1. Bestimmt divergent gegen** $+\infty$, falls zu jedem $M \in \mathbb{R}$ ein $N \in \mathbb{N}$ existiert mit:

$$a_n > M \text{ für alle } n \geq N$$

Schreibweise: $\lim_{n \to \infty} a_n = +\infty$

**2. Bestimmt divergent gegen** $-\infty$, falls zu jedem $M \in \mathbb{R}$ ein $N \in \mathbb{N}$ existiert mit:

$$a_n < M \text{ für alle } n \geq N$$

Schreibweise: $\lim_{n \to \infty} a_n = -\infty$

### Terminologie

Manche Autoren verwenden statt "bestimmt divergent gegen $+\infty$" auch den Begriff "**uneigentlich konvergent gegen** $+\infty$".

**Wir machen das nicht!** "**Konvergent**" bedeutet bei uns **immer** "konvergent gegen eine reelle Zahl".

### Beispiele

**Beispiel 1:** Die Folge $(n)_{n \in \mathbb{N}}$ ist bestimmt divergent gegen $+\infty$

Für $M \in \mathbb{R}$ wähle $N \in \mathbb{N}$ mit $N > M$. Dann gilt $a_n = n \geq N > M$ für alle $n \geq N$ ✓

Ebenso: $(n^2)_n$, $(n^3)_n$, ... sind bestimmt divergent gegen $+\infty$

**Beispiel 2:** Die Folge $(\ln(1/n))_{n \geq 1}$ ist bestimmt divergent gegen $-\infty$

Ebenso: $(-n)_n$, $(-n^2)_n$, ... sind bestimmt divergent gegen $-\infty$

**Beispiel 3: Divergent, aber nicht bestimmt divergent**

$((-1)^n)_n$ ist **divergent**, aber **nicht bestimmt divergent** (weder gegen $+\infty$ noch gegen $-\infty$)

**Beispiel 4:**

$$x_n = \begin{cases} n & \text{falls } n \text{ gerade} \\ 0 & \text{falls } n \text{ ungerade} \end{cases}$$

Die Folge $(x_n) = (0, 0, 2, 0, 4, 0, 6, \ldots)$ ist **divergent**, aber **nicht bestimmt divergent gegen** $+\infty$ (wegen der unendlich vielen Nullen).

---

## 6. Wichtige Bemerkung: "Ende gut, alles gut"

**Satz:** Das Verhalten der ersten $m$ Folgenglieder $a_0, a_1, \ldots, a_{m-1}$ hat **keinen Einfluss** auf das Konvergenzverhalten.

Genauer: Die Folge $(a_n)_{n \geq 0}$ ist genau dann konvergent, wenn für ein $n_0$ die Folge $(a_n)_{n \geq n_0}$ konvergent ist.

**Konsequenz:** Man kann Konvergenz **nicht** durch Berechnung von endlich vielen Folgengliedern nachweisen. Will man Aussagen über Konvergenz machen, muss man etwas **beweisen**!

---

## 7. Komplexe Zahlenfolgen

### Definition

Analog definiert man Konvergenz für **komplexe Zahlen** $a_n \in \mathbb{C}$:

$(a_n)_{n \in \mathbb{N}}$ ist genau dann konvergent gegen $a \in \mathbb{C}$, wenn zu jedem $\varepsilon > 0$ (hier: $\varepsilon \in \mathbb{R}$) ein $N_\varepsilon \in \mathbb{N}$ existiert, so dass:

$$|a_n - a| < \varepsilon \text{ für alle } n \geq N_\varepsilon$$

**Beschränktheit:** $(a_n)_{n \in \mathbb{N}}$ ist genau dann beschränkt, wenn es eine Zahl $M \in \mathbb{R}$ gibt mit $|a_n| \leq M$ für alle $n \in \mathbb{N}$.

**Monotonie:** Kann für komplexe Zahlen **nicht** erklärt werden, da wir komplexe Zahlen nicht anordnen können.

### Beispiel

Die Folge $\left(\frac{1}{(3+4i)^k}\right)_{k \in \mathbb{N}}$ konvergiert gegen $0$, denn:

$$\left|\frac{1}{(3+4i)^k} - 0\right| = \frac{1}{|3+4i|^k} = \frac{1}{(\sqrt{9+16})^k} = \frac{1}{5^k} \to 0$$

---

## 📌 Zusammenfassung

### Definitionen

|        Begriff         |                       Definition                       |        Notation        |
| :--------------------: | :----------------------------------------------------: | :--------------------: |
|       **Folge**        | Abbildung $\mathbb{N} \to \mathbb{R}$, $n \mapsto a_n$ | $(a_n)_n$ oder $(a_n)$ |
|     **Konvergent**     |              $\|a_n - a\| < \varepsilon$               |      $a_n \to a$       |
|     **Divergent**      |                    Nicht konvergent                    |           –            |
|     **Nullfolge**      |                  Konvergent gegen $0$                  |      $a_n \to 0$       |
| **Bestimmt divergent** | $\forall M \, \exists N : a_n > M \, \forall n \geq N$ |  $a_n \to +/-\infty$   |

### Eigenschaften

$$\begin{array}{c|c}
\text{Konvergent} & \text{Divergent} \\ \hline
\text{Beschränkt} & \text{Kann beschränkt oder unbeschränkt sein} \\
\text{Eindeutiger Grenzwert} & \text{Kein Grenzwert} \\
\text{Erste } m \text{ Glieder egal} & \text{Erste } m \text{ Glieder egal}
\end{array}$$

### Wichtige Implikationen

$$\text{Unbeschränkt} \implies \text{Divergent}$$

$$\text{Konvergent} \implies \text{Beschränkt}$$

**Aber NICHT umgekehrt:** Beschränkt $\not\!\!\!\implies$ Konvergent (Gegenbeispiel: $((-1)^n)_n$)

### Klassifikation von Folgen

```
                    Alle Folgen
                         │
        ┌────────────────┴────────────────┐
        │                                 │
   Konvergent                         Divergent
        │                                 │
    (beschränkt,                  ┌───────┴────────┐
  eindeutiger Grenzwert)          │                │
                            Bestimmt div.    Nicht bestimmt div.
                                 │             (z.B. (-1)ⁿ)
                         ┌───────┴────────┐
                         │                │
		                     +∞              -∞
```

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.18 Berechnung von Grenzwerten]]: Grenzwertsätze und Rechenregeln
- [[VL.19 Stetigkeit]]: Unendliche Summen als spezielle Folgen
- [[VL.20 Sätze über stetige Funktionen]]: Konvergenz und stetige Funktionen
- [[VL.23 Mittelwertsatz]]: Verallgemeinerung des Konvergenzbegriffs
