**Class:** [[AnaLina]]  
**Date:** 10-01-2026  
**Topics:** #Rang #Lösbarkeit #InverseMatrix #GaußJordan #Invertierbarkeit

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung erweitert die Anwendungen des Gauß-Algorithmus auf zwei fundamentale Konzepte: den Rang einer Matrix und die Berechnung inverser Matrizen. Diese Werkzeuge ermöglichen präzise Aussagen über die Lösbarkeit linearer Gleichungssysteme.

- **Rang einer Matrix** als zentrales Konzept
- **Lösbarkeitskriterium** für LGS mittels Rang
- **Berechnung der Inversen** mit dem Gauß-Jordan-Verfahren
- **Invertierbarkeit** charakterisiert durch Rang
- **Unterschiede** zwischen Matrizen und Zahlen

---

## 1. Der Rang einer Matrix

### Definition

Der **Rang** von $A \in K^{m,n}$ ist die Anzahl der Zeilen ungleich Null in einer Zeilenstufenform von $A$ und wird mit $\text{Rang}(A)$ bezeichnet.

### Eigenschaften des Rangs

**Grenzen des Rangs:**
- $\text{Rang}(A) \geq 0$
- $\text{Rang}(A) = 0$ genau dann, wenn $A = 0$ (Nullmatrix)
- $\text{Rang}(A) \leq m$ (höchstens so viele wie Zeilen)
- $\text{Rang}(A) \leq n$ (höchstens so viele wie Spalten, da höchstens so viele Stufen wie Spalten)

Also: $0 \leq \text{Rang}(A) \leq \min(m,n)$

### Alternative Charakterisierung

**Bemerkung:** Der Rang einer Matrix ist:
- Die **maximale Anzahl linear unabhängiger Zeilen** von $A$, oder
- Die **maximale Anzahl linear unabhängiger Spalten** von $A$

(Beide sind gleich!)

### Beispiele

**Beispiel 1:**
$$A = \begin{bmatrix} 0 & 2 & 1 & 1 \\ 0 & 0 & 1 & -2 \\ 0 & 0 & 0 & 3 \end{bmatrix}$$

Dies ist bereits in ZSF mit 3 Nichtnullzeilen → $\text{Rang}(A) = 3$

**Beispiel 2:**
$$A = \begin{bmatrix} 1 & 1 \\ 2 & 2 \end{bmatrix} \xrightarrow{\text{II} - 2\text{I}} \begin{bmatrix} 1 & 1 \\ 0 & 0 \end{bmatrix}$$

ZSF hat 1 Nichtnullzeile → $\text{Rang}(A) = 1$

**Beispiel 3:**
$$A = \begin{bmatrix} 1 & 2 & 0 & 3 \\ 0 & 0 & 1 & 4 \\ 0 & 0 & 0 & 0 \end{bmatrix}$$

Bereits in ZSF mit 2 Nichtnullzeilen → $\text{Rang}(A) = 2$

---

## 2. Lösbarkeitskriterium für LGS

### Hauptsatz

**Satz (Lösbarkeitskriterium):** Seien $A \in K^{m,n}$ und $b \in K^m$. Das LGS $Ax = b$ hat:

1. **Keine Lösung** genau dann, wenn $\text{Rang}([A \mid b]) > \text{Rang}(A)$

2. **Genau eine Lösung** genau dann, wenn $\text{Rang}([A \mid b]) = \text{Rang}(A) = n$

3. **Unendlich viele Lösungen** genau dann, wenn $\text{Rang}([A \mid b]) = \text{Rang}(A) < n$

### Begründung

Bringe die erweiterte Koeffizientenmatrix $[A \mid b]$ in ZSF:

$$[C \mid d] = \begin{bmatrix} 
0 & c_{1,j_1} & * & * & * & * & * & * & * & * & \mid & d_1 \\
0 & 0 & 0 & c_{2,j_2} & * & * & * & * & * & * & \mid & d_2 \\
0 & 0 & 0 & 0 & 0 & c_{3,j_3} & * & * & * & * & \mid & d_3 \\
\vdots & \vdots & \vdots & \vdots & \vdots & \ddots & \ddots & \ddots & \vdots & \vdots & \mid & \vdots \\
0 & 0 & 0 & 0 & 0 & 0 & \cdots & 0 & c_{r,j_r} & * & \mid & d_r \\
0 & 0 & 0 & 0 & 0 & 0 & 0 & \cdots & 0 & 0 & \mid & d_{r+1} \\
\vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \vdots & \mid & \vdots \\
0 & 0 & 0 & 0 & 0 & 0 & 0 & \cdots & 0 & 0 & \mid & d_m
\end{bmatrix}$$

mit Pivotelementen $c_{1,j_1}, c_{2,j_2}, \ldots, c_{r,j_r} \neq 0$.

Es gilt:
$$\text{Rang}(A) = r = \text{Rang}(C)$$
$$\text{Rang}([A \mid b]) = \text{Rang}([C \mid d]) \geq r = \text{Rang}(A)$$

**Fall 1: Mindestens ein** $d_{r+1}, \ldots, d_m \neq 0$

Dann ist $\text{Rang}([A \mid b]) = r + 1 > \text{Rang}(A)$

Die entsprechende Gleichung lautet:
$$0x_1 + 0x_2 + \ldots + 0x_n = d_j \neq 0$$

Dies ist **unmöglich** → **Keine Lösung**

**Fall 2: Alle** $d_{r+1} = \ldots = d_m = 0$

Dann ist $\text{Rang}([A \mid b]) = r = \text{Rang}(A)$

Das LGS **hat Lösungen**.

Für $i = 1, \ldots, r$ sind die $c_{i,j_i} \neq 0$ → Die zugehörigen Variablen $x_{j_i}$ können **eindeutig bestimmt** werden (durch Auflösen der $i$-ten Gleichung nach $x_{j_i}$).

- **Anzahl Pivotvariablen:** $r = \text{Rang}(A)$
- **Anzahl freie Variablen:** $n - r = n - \text{Rang}(A)$

**Unterfall 2a:** $r = n$ (alle Variablen sind Pivotvariablen)  
→ **Genau eine Lösung**

**Unterfall 2b:** $r < n$ (mindestens eine freie Variable)  
→ **Unendlich viele Lösungen**

### Entscheidungsschema

![[Screenshot 2026-01-08 at 12.08.50.png]]

### Beispiele

**Beispiel 1: Keine Lösung**

$$[A \mid b] = \begin{bmatrix} 1 & 1 & \mid & 2 \\ 2 & 2 & \mid & 0 \end{bmatrix} \xrightarrow{\text{II} - 2\text{I}} \begin{bmatrix} 1 & 1 & \mid & 2 \\ 0 & 0 & \mid & -4 \end{bmatrix}$$

- $\text{Rang}(A) = 1$
- $\text{Rang}([A \mid b]) = 2$
- $\text{Rang}([A \mid b]) > \text{Rang}(A)$ → **Keine Lösung**

**Beispiel 2: Genau eine Lösung**

$$[A \mid b] = \begin{bmatrix} 1 & 2 & \mid & 3 \\ 0 & 1 & \mid & 1 \end{bmatrix}$$

Bereits in ZSF:
- $\text{Rang}(A) = 2 = n$
- $\text{Rang}([A \mid b]) = 2 = \text{Rang}(A)$ → **Genau eine Lösung**

**Beispiel 3: Unendlich viele Lösungen**

$$[A \mid b] = \begin{bmatrix} 2 & 3 & \mid & 2 \\ 0 & 0 & \mid & 0 \end{bmatrix}$$

- $\text{Rang}(A) = 1 < 2 = n$
- $\text{Rang}([A \mid b]) = 1 = \text{Rang}(A)$ → **Unendlich viele Lösungen**
- Anzahl freier Variablen: $n - \text{Rang}(A) = 2 - 1 = 1$

---

## 3. Invertierbarkeit von Matrizen

### Wiederholung: Definition Inverse

Eine quadratische Matrix $A \in K^{n,n}$ heißt **invertierbar**, falls es eine Matrix $B \in K^{n,n}$ gibt mit:

$$BA = I_n \quad \text{und} \quad AB = I_n$$

Die Matrix $B$ ist dann eindeutig bestimmt, wird die **Inverse** von $A$ genannt und mit $A^{-1}$ bezeichnet.

### Charakterisierung durch den Rang

**Satz:** Für $A \in K^{n,n}$ gilt:

$$A \text{ ist invertierbar} \iff \text{Rang}(A) = n$$

**Interpretation:** Eine quadratische Matrix ist invertierbar genau dann, wenn sie vollen Rang hat (d.h., in der ZSF keine Nullzeilen auftreten).

---

## 4. Berechnung der Inversen

### Gauß-Jordan-Verfahren

Um die Inverse $X = A^{-1}$ zu finden (falls sie existiert), lösen wir:

$$AX = I_n$$

Betrachte die Spalten von $X$ und $I_n$:

$$X = [x_1 \mid \ldots \mid x_n], \quad I_n = [e_1 \mid \ldots \mid e_n]$$

Dann:
$$AX = A[x_1 \mid \ldots \mid x_n] = [Ax_1 \mid \ldots \mid Ax_n] = [e_1 \mid \ldots \mid e_n]$$

Spaltenvergleich ergibt $n$ lineare Gleichungssysteme:
$$Ax_1 = e_1, \quad Ax_2 = e_2, \quad \ldots, \quad Ax_n = e_n$$

Da die Koeffizientenmatrix immer $A$ ist, lösen wir alle Systeme **gleichzeitig**:

$$[A \mid e_1 \mid \ldots \mid e_n] = [A \mid I_n]$$

### Algorithmus

**Berechnung der Inversen:** Ist $A \in K^{n,n}$ (quadratisch), gehe wie folgt vor:

**Schritt 1:** Bringe $[A \mid I_n]$ mit elementaren Zeilenoperationen in NZSF $[C \mid D]$

**Schritt 2:** Prüfe den Rang:
- Falls $\text{Rang}(A) \neq n$ → $A$ ist **nicht invertierbar** → Stopp
- Falls $\text{Rang}(A) = n$ → Fahre fort

**Schritt 3:** Dann ist $C = I_n$ und $A^{-1} = D$

**Begründung:** Wenn $\text{Rang}(A) = n$, hat die NZSF keine Nullzeilen und muss $I_n$ sein. Die Operationen transformieren $[A \mid I_n] \to [I_n \mid A^{-1}]$.

### Beispiele

**Beispiel 1: Nicht invertierbare Matrix**

$$A = \begin{bmatrix} 1 & 1 \\ 1 & 1 \end{bmatrix}$$

$$[A \mid I_2] = \begin{bmatrix} 1 & 1 & \mid & 1 & 0 \\ 1 & 1 & \mid & 0 & 1 \end{bmatrix} \xrightarrow{\text{II} - \text{I}} \begin{bmatrix} 1 & 1 & \mid & 1 & 0 \\ 0 & 0 & \mid & -1 & 1 \end{bmatrix}$$

$$\xrightarrow{\text{I} + \text{II}} \begin{bmatrix} 1 & 1 & \mid & 0 & 1 \\ 0 & 0 & \mid & -1 & 1 \end{bmatrix} \xrightarrow{-\text{II}} \begin{bmatrix} 1 & 1 & \mid & 0 & 1 \\ 0 & 0 & \mid & 1 & -1 \end{bmatrix}$$

Da $C = \begin{bmatrix} 1 & 1 \\ 0 & 0 \end{bmatrix} \neq I_2$ ist → $\text{Rang}(A) = 1 < 2$ → **Nicht invertierbar**

**Beispiel 2: Invertierbare 3×3-Matrix**

$$A = \begin{bmatrix} 1 & 3 & 1 \\ 1 & 4 & 3 \\ 1 & 2 & 0 \end{bmatrix} \in \mathbb{C}^{3,3}$$

$$[A \mid I_3] = \begin{bmatrix} 1 & 3 & 1 & \mid & 1 & 0 & 0 \\ 1 & 4 & 3 & \mid & 0 & 1 & 0 \\ 1 & 2 & 0 & \mid & 0 & 0 & 1 \end{bmatrix}$$

Nach elementaren Zeilenoperationen (Details im Skript):

$$\xrightarrow{\substack{\text{II} - \text{I} \\ \text{III} - \text{I}}} \begin{bmatrix} 1 & 3 & 1 & \mid & 1 & 0 & 0 \\ 0 & 1 & 2 & \mid & -1 & 1 & 0 \\ 0 & -1 & -1 & \mid & -1 & 0 & 1 \end{bmatrix}$$

$$\xrightarrow{\text{III} + \text{II}} \begin{bmatrix} 1 & 3 & 1 & \mid & 1 & 0 & 0 \\ 0 & 1 & 2 & \mid & -1 & 1 & 0 \\ 0 & 0 & 1 & \mid & -2 & 1 & 1 \end{bmatrix}$$

Bereits $\text{Rang}(A) = 3$ → $A$ ist invertierbar!

Weiter auf NZSF:

$$\xrightarrow{\substack{\text{II} - 2\text{III} \\ \text{I} - \text{III}}} \begin{bmatrix} 1 & 3 & 0 & \mid & 3 & -1 & -1 \\ 0 & 1 & 0 & \mid & 3 & -1 & -2 \\ 0 & 0 & 1 & \mid & -2 & 1 & 1 \end{bmatrix}$$

$$\xrightarrow{\text{I} - 3\text{II}} \begin{bmatrix} 1 & 0 & 0 & \mid & -6 & 2 & 5 \\ 0 & 1 & 0 & \mid & 3 & -1 & -2 \\ 0 & 0 & 1 & \mid & -2 & 1 & 1 \end{bmatrix}$$

Daher ist:

$$A^{-1} = \begin{bmatrix} -6 & 2 & 5 \\ 3 & -1 & -2 \\ -2 & 1 & 1 \end{bmatrix}$$

**Probe:** Berechne $A^{-1}A$ oder $AA^{-1}$ – muss $I_3$ ergeben!

---

## 5. Spezialfall: Inverse von 2×2-Matrizen

### Formel

Für eine invertierbare Matrix $A = \begin{bmatrix} a & b \\ c & d \end{bmatrix} \in K^{2,2}$ gilt:

$$A^{-1} = \frac{1}{ad - bc} \begin{bmatrix} d & -b \\ -c & a \end{bmatrix}$$

**Hinweis:** Bei invertierbaren $(2 \times 2)$-Matrizen ist $ad - bc \neq 0$ (siehe Determinante, VL.32).

### Beispiel

$$A = \begin{bmatrix} 2 & -3 \\ 1 & 5 \end{bmatrix}$$

Berechne $ad - bc = 2 \cdot 5 - 1 \cdot (-3) = 10 + 3 = 13$

$$A^{-1} = \frac{1}{13} \begin{bmatrix} 5 & 3 \\ -1 & 2 \end{bmatrix}$$

**Probe:**
$$AA^{-1} = \begin{bmatrix} 2 & -3 \\ 1 & 5 \end{bmatrix} \cdot \frac{1}{13} \begin{bmatrix} 5 & 3 \\ -1 & 2 \end{bmatrix} = \frac{1}{13} \begin{bmatrix} 13 & 0 \\ 0 & 13 \end{bmatrix} = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix} = I_2 \, \checkmark$$

---

## 6. LGS lösen mit der Inversen

Ist $A \in K^{n,n}$ **invertierbar** mit Inverse $A^{-1}$, so ist das LGS $Ax = b$ **eindeutig lösbar** mit:

$$x = A^{-1}b$$

**Aber:** Ist man nur an der Lösung von $Ax = b$ interessiert, ist es **effizienter**, das LGS direkt mit dem Gauß-Algorithmus zu lösen, statt erst die Inverse zu berechnen!

---

## 7. Unterschiede zwischen Matrizen und Zahlen

### Wichtige Unterschiede

**1. Keine Kommutativität der Multiplikation**

Im Allgemeinen gilt: $AB \neq BA$, selbst wenn beide Produkte definiert sind.

**Beispiel:**
$$A = \begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix}, \quad B = \begin{bmatrix} 0 & 1 \\ 0 & 0 \end{bmatrix}$$

$$AB = \begin{bmatrix} 0 & 1 \\ 0 & 0 \end{bmatrix}, \quad BA = \begin{bmatrix} 0 & 0 \\ 0 & 0 \end{bmatrix}$$

Also $AB \neq BA$ ✓

**2. Nicht-null bedeutet nicht invertierbar**

Aus $A \neq 0$ folgt **nicht**, dass $A$ invertierbar ist (auch nicht bei quadratischen Matrizen).

**Beispiel:**
$$A = \begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix} \neq 0, \quad \text{aber } \text{Rang}(A) = 1 < 2$$

Also ist $A$ nicht invertierbar.

**3. Nullteiler existieren**

Aus $AB = 0$ folgt im Allgemeinen **nicht**, dass $A = 0$ oder $B = 0$ sein muss.

**Beispiel:**
$$A = \begin{bmatrix} 1 & 0 \\ 0 & 0 \end{bmatrix}, \quad B = \begin{bmatrix} 0 & 0 \\ 0 & 1 \end{bmatrix}$$

Beide sind $\neq 0$, aber:
$$AB = \begin{bmatrix} 0 & 0 \\ 0 & 0 \end{bmatrix} = 0$$

**4. Kürzungsregel bei Invertierbarkeit**

**Satz:** Ist $AB = 0$ und $A$ invertierbar, so folgt:
$$B = A^{-1}AB = A^{-1} \cdot 0 = 0$$

Ist $AB = 0$ und $B$ invertierbar, so folgt genauso:
$$A = ABB^{-1} = 0 \cdot B^{-1} = 0$$

**Interpretation:** Kürzung funktioniert nur mit invertierbaren Matrizen!

---

## 📌 Zusammenfassung

### Rang

| Konzept | Definition | Bedeutung |
|---------|------------|-----------|
| **Rang** | Anzahl Nichtnullzeilen in ZSF | Max. Anzahl linear unabh. Zeilen/Spalten |
| **Schranken** | $0 \leq \text{Rang}(A) \leq \min(m,n)$ | Begrenzt durch Zeilen und Spalten |

### Lösbarkeitskriterium

$$\begin{array}{c|c|c}
\text{Bedingung} & \text{Anzahl Lösungen} & \text{Interpretation} \\ \hline
\text{Rang}([A|b]) > \text{Rang}(A) & 0 & \text{Widerspruch: } 0 = c \neq 0 \\
\text{Rang}([A|b]) = \text{Rang}(A) = n & 1 & \text{Alle Variablen eindeutig bestimmt} \\
\text{Rang}([A|b]) = \text{Rang}(A) < n & \infty & n - \text{Rang}(A) \text{ freie Variablen}
\end{array}$$

### Invertierbarkeit

| Aussage | Bedeutung |
|---------|-----------|
| $A$ invertierbar $\iff \text{Rang}(A) = n$ | Voller Rang = invertierbar |
| Berechnung: $[A \mid I_n] \to [I_n \mid A^{-1}]$ | Gauß-Jordan-Verfahren |
| $(2 \times 2)$-Formel: $A^{-1} = \frac{1}{ad-bc}\begin{bmatrix} d & -b \\ -c & a \end{bmatrix}$ | Schnellformel für kleine Matrizen |

### Wichtige Unterschiede zu Zahlen

- ❌ Matrizenmultiplikation ist **nicht kommutativ**: $AB \neq BA$ im Allgemeinen
- ❌ $A \neq 0$ bedeutet **nicht** $A$ invertierbar
- ❌ $AB = 0$ bedeutet **nicht** $A = 0$ oder $B = 0$ (Nullteiler!)
- ✅ Kürzung nur mit invertierbaren Matrizen: $AB = 0$ und $A$ invertierbar $\implies B = 0$

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.11 Basis und Dimension]]: Rang als Dimension des Spaltenraums
- [[VL.12 Matrizen]]: Definition der Inversen
- [[VL.13 Lineare Gleichungssysteme]]: Gauß-Algorithmus
- [[VL.15 Lineare Abbildungen]]: Rang und Dimension des Bildes

