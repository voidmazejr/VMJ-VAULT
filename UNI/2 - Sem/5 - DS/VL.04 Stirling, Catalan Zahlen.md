**Class:** [[Diskrete Strukturen]]  
**Date:** 29-04-2026  
**Topics:** #DiskreteStrukturen #Binaerbaeume #CatalanZahlen #Permutationen #StirlingZahlen #Partitionen

---

## 🎯 Lernziele der Vorlesung

- Verstehen, was ein Binärbaum ist und welche Spezialfälle (vollständig, balanciert) es gibt.
- Nachvollziehen, warum ein vollständiger, balancierter Binärbaum der Höhe $h$ genau $2^{h+1}-1$ Knoten und $2^h$ Blätter hat.
- Die Catalan-Rekursion $B_n=\sum_{k=1}^n B_{k-1}B_{n-k}$ verstehen und die explizite Formel $B_n=\frac{1}{n+1}\binom{2n}{n}$ kennen.
- Korrekte Klammerausdrücke als Catalan-Objekt erkennen und die zugehörige Rekursion herleiten.
- Permutationen, Zykelschreibweise und Fixpunkte verstehen.
- Stirling-Zahlen 1. Art $s_{n,k}$ (Permutationen mit $k$ Zyklen) und ihre Rekursion $s_{n,k}=s_{n-1,k-1}+(n-1)s_{n-1,k}$ lernen.
- Stirling-Zahlen 2. Art $S_{n,k}$ (Anzahl $k$-Partitionen) mit $S_{n,k}=S_{n-1,k-1}+kS_{n-1,k}$ verstehen.

---

## 1. Definitionen & Grundlagen

### Definition: Binärbaum

Ein Baum, in dem jeder Knoten höchstens zwei Nachfolger hat; linker und rechter Nachfolger sind unterscheidbar.

$$\boxed{\text{Binärbaum} = \text{Baum, in dem jeder Knoten höchstens 2 Nachfolger hat}}$$

Wichtige Begriffe:

- Vollständig: jeder Knoten hat Grad $0$ oder $2$.
- Balanciert: alle Blätter haben denselben Abstand zur Wurzel.
- Höhe $h$: Länge des längsten Pfades von der Wurzel zu einem Blatt.

⚠️ Achtung: „vollständig“ wird hier als „jeweils Grad $0$ oder $2$“ verwendet (nicht unbedingt dieselbe Konvention wie in manchen Implementierungskontexten).

### ASCII-Diagramm (Binärbaum-Beispiel)

```
       root
      /    \
   left   right
   /  \     / \
  o    o   o   o
```

---

## 2. Vollständiger, balancierter Binärbaum — Knoten & Blätter

### Satz (Knotenzahl)

Sei $T=(V,E)$ ein vollständiger, balancierter Binärbaum der Höhe $h$. Dann gilt:

$$\boxed{|V| = 2^{h+1} - 1}$$

### Beweis (Induktion über $h$)

- Anfang ($h=0$): Baum besteht aus einem Knoten. $2^{0+1}-1=1$. ✅
- Voraussetzung: Für alle $j<h$ gilt die Formel.
- Schritt ($h\to h$): Wurzel $v$ hat zwei Teilbäume $T_1,T_2$ der Höhe $h-1$. Per IV hat jeder $2^h-1$ Knoten. Also $$|V| = 1 + (2^h-1) + (2^h-1) = 2^{h+1}-1.$$  
    Damit ist die Induktion abgeschlossen. ✅

### Satz (Blattanzahl)

Für dieselben Voraussetzungen gilt:

$$\boxed{\text{Blätter} = 2^h}$$

### Beweis (Induktion über $h$)

- Anfang ($h=0$): Ein Knoten $\Rightarrow$ 1 Blatt; $2^0=1$. ✅
- Voraussetzung: Für alle $j<h$ gilt Blattanzahl $2^j$.
- Schritt: Zwei Teilbäume der Höhe $h-1$ haben zusammen $2^{h-1}+2^{h-1}=2^h$ Blätter. ✅

> Merkhilfe: Auf jeder Ebene verdoppelt sich die Anzahl der Positionen; die unterste Ebene hat $2^h$ mögliche Blätter.

---

## 3. Catalan-Zahlen (Binärbäume & Klammerausdrücke)

### 3.1 Definition und Rekursion für Binärbäume

Sei $B_n$ die Anzahl binärer, geordneter Binärbäume mit $n$ Knoten.

$$\boxed{B_0 = 1}$$ $$\boxed{B_n = \sum_{k=1}^{n} B_{k-1},B_{n-k} \quad (n>0)}$$

Begründung (Aufbau): Wurzel + linker Teilbaum mit $\ell$ Knoten + rechter Teilbaum mit $r$ Knoten, $\ell+1+r=n$; summiere über alle $\ell$.

### 3.2 Korrekte Klammerausdrücke (Catalan-Objekt)

Definition: Folge aus "(" und ")", gleiche Anzahl von "(" und ")", und in jedem Präfix ist Anzahl "(" $\ge$ Anzahl ")".

Grammatik: $S \to \epsilon \mid SS \mid (S)$.

Sei $C_n$ die Anzahl korrekter Ausdrücke mit $n$ Paaren. Dann:

$$\boxed{C_0=1}$$ $$\boxed{C_n = \sum_{k=1}^{n} C_{k-1},C_{n-k}}$$

Beweisidee: Die erste "(" schließt an Position $2k$; der Ausdruck zerfällt in inneren Teil mit $k-1$ Paaren und den Rest mit $n-k$ Paaren.

### 3.3 Beziehung & explizite Formel

Die Zahlen sind identisch: $B_n = C_n$ (gleiche Rekursion + gleicher Anfangsfall). Explizit:

$$\boxed{B_n = C_n = \frac{1}{n+1}\binom{2n}{n}}$$

⚠️ Hinweis: Der Explizit-Beweis (via Generating Functions oder Ballot/Catalan-Argumente) ist hier nicht ausgeführt.

---

## 4. Rekursive/Induktive Definitionen (allgemein)

- Rekursive Definition auf $\mathbb{N}$: Anfangswerte angeben, für $n>n_0$ $f(n)$ mittels vorheriger Werte definieren.
- Explizite Form: Funktion $g$ mit $f(n)=g(n)$ für alle $n$ heißt explizite Form.

### Beispiel: Höhe eines Baums (induktiv)

$$ \boxed{h(T) = \begin{cases} 0, & \text{falls } T \text{ nur einen Knoten hat}, [4pt] 1 + \max{h(T_i) : 1\le i\le \ell}, & \text{sonst (Teilbäume }T_i). \end{cases}} $$

---

## 5. Permutationen & Zyklen

### Definition: Permutation

Eine Permutation einer Menge $A={a_1,\dots,a_n}$ ist eine bijektive Abbildung $\pi:A\to A$.

Zwei-Zeilen-Notation: 
$$ 
\pi = \begin{pmatrix}
a_1 & a_2 & \cdots & a_n \\
\pi(a_1) & \pi(a_2) & \cdots & \pi(a_n)
\end{pmatrix}
$$

Anzahl der Permutationen: $\boxed{n!}$.

### Zyklen

Ein Zyklus $(i_1\ i_2\ \dots\ i_t)$ hat die Eigenschaft $\pi(i_j)=i_{j+1}$ für $j<t$ und $\pi(i_t)=i_1$; $t$ ist die Länge.

Jede Permutation zerfällt in disjunkte Zyklen; Fixpunkte sind Zyklen der Länge 1.

### Beispiel (Zykluszerlegung)

Gegeben $\pi$ mit $\pi(1)=5,\ \pi(5)=2,\ \pi(2)=8,\ \pi(8)=1$ ist ein Zyklus $(1\ 5\ 2\ 8)$.

---

## 6. Stirling-Zahlen erster Art (Zyklen in Permutationen)

### Definition

$s_{n,k}$ = Anzahl Permutationen einer $n$-elementigen Menge mit genau $k$ Zyklen.

### Rekursion

$$\boxed{s_{n,k} = s_{n-1,k-1} + (n-1),s_{n-1,k}}$$

### Beweis (Fallunterscheidung)

Sei $a_n$ das neue Element:

- Fall 1: $a_n$ bildet eigenen Zyklus $(a_n)$ → $s_{n-1,k-1}$ Möglichkeiten.
- Fall 2: $a_n$ wird in einen bestehenden Zyklus eingebaut. Zuerst $s_{n-1,k}$ Permutationen der $n-1$ übrigen Elemente; in jeden Zyklus gibt es Einfügepositionen, insgesamt $n-1$ mögliche Einfügestellen → $(n-1)s_{n-1,k}$.

Zusammen ergibt das die Rekursion.


---

## 7. Partitionen & Stirling-Zahlen zweiter Art

### Definition: $k$-Partition

Eine Zerlegung einer $n$-elementigen Menge $A$ in $k$ nicht-leere, paarweise disjunkte Blöcke.

### Notation

$S_{n,k}$ = Anzahl $k$-Partitionen einer $n$-elementigen Menge.

Randfälle:

- $S_{n,k}=0$ falls $k>n$.
- $S_{n,0}=0$ für $n>0$.
- $S_{0,0}:=1$.

### Rekursion

$$\boxed{S_{n,k} = S_{n-1,k-1} + k,S_{n-1,k}}$$

### Beweis (Fallunterscheidung)

Sei $a_n$ das neue Element:

- Fall 1: $a_n$ bildet eigenen Block ${a_n}$ → $S_{n-1,k-1}$ Möglichkeiten.
- Fall 2: $a_n$ wird in einen der $k$ vorhandenen Blöcke eingefügt → für jede Partition der übrigen $n-1$ Elemente ($S_{n-1,k}$ Möglichkeiten) gibt es $k$ Möglichkeiten, in welchen Block $a_n$ eingefügt wird → $k S_{n-1,k}$.

---

## 8. Vergleich & Tabellen

### Vergleichstabelle der Rekursionen

|Objekt|Symbol|Rekursion|Anfangswert|
|---|--:|---|---|
|Binärbäume (geordnete)|$B_n$|$B_n=\sum_{k=1}^n B_{k-1}B_{n-k}$|$B_0=1$|
|Klammerausdrücke|$C_n$|$C_n=\sum_{k=1}^n C_{k-1}C_{n-k}$|$C_0=1$|
|Permutationen mit $k$ Zyklen|$s_{n,k}$|$s_{n,k}=s_{n-1,k-1}+(n-1)s_{n-1,k}$|$s_{0,0}=1$|
|$k$-Partitionen|$S_{n,k}$|$S_{n,k}=S_{n-1,k-1}+kS_{n-1,k}$|$S_{0,0}=1$|

Merkhilfe: Bei Zyklen ist der Einfügefaktor $(n-1)$ (Einfügepositionen in Zyklen), bei Partitionen ist der Faktor $k$ (Anzahl existierender Blöcke).

---

## 11. 📌 Zusammenfassung (Kernaussagen & Formeln)

|Thema|Kernaussage / Formel|
|---|---|
|Vollst. balancierter Binärbaum|$|
|Catalan (rekursiv)|$B_n=\sum_{k=1}^n B_{k-1}B_{n-k}$, $B_0=1$|
|Catalan (explizit)|$B_n=\dfrac{1}{n+1}\binom{2n}{n}$|
|Stirling 1. Art|$s_{n,k}=s_{n-1,k-1}+(n-1)s_{n-1,k}$|
|Stirling 2. Art|$S_{n,k}=S_{n-1,k-1}+kS_{n-1,k}$|

✅ Wichtige Tatsache: Catalan-Folge zählt mehrere unterschiedliche kombinatorische Objekte (z.B. geordnete Binärbäume, korrekte Klammerausdrücke).  
⚠️ Vorsicht: Stirling 1. und 2. Art sind unterschiedlich—Faktor $(n-1)$ vs. $k$.  
❌ Fehlerquelle: Verwechslungsgefahr zwischen „vollständig“ (Vorlesungssinn) und anderen technischen Definitionen.

---

## 🔗 Verbindungen

- [[VL.03 Beweise & Bäume]] — Beweistechniken und rekursive Definitionen.
- [[VL.06 Mehrfachzusammenhang und Rundtouren]] — Allgemeine Baumbegriffe und Anwendungen.
