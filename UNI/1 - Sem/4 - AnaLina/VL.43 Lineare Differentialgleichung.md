**Class:** [[AnaLina]]  
**Date:** 12-12-2025  
**Topics:** #Differentialgleichungen #DGL #Anfangswertproblem #Matrixexponential #Diagonalisierung #GedämpfteSchwingung

---

## 🎯 Lernziele der Vorlesung

Differentialgleichungen beschreiben viele physikalische Prozesse. Wir untersuchen lineare Differentialgleichungen und ihre Lösungsmethoden.

- **Lineare Differentialgleichungen 1. Ordnung** und ihre Lösungen
- **Anfangswertprobleme** (AWP)
- **Systeme linearer DGL** mit Matrixexponential
- **Lineare DGL 2. Ordnung** (harmonische Schwingungen)
- **Gedämpfte Schwingungen** (Kriechfall, Grenzfall, Schwingfall)

---

## 1. Grundbegriffe

### Definition (Differentialgleichung)

Eine **Differentialgleichung (DGL)** ist eine Gleichung, deren Lösung eine **Funktion** ist. In der Gleichung können sowohl die gesuchte Funktion als auch ihre Ableitungen auftreten.

### Ordnung einer DGL

Die **Ordnung** einer DGL ist die **höchste auftretende Ableitung**.

**Beispiele:**
- $y' = ay$ hat **Ordnung 1** (wegen $y'$)
- $y'' = -ay$ hat **Ordnung 2** (wegen $y''$)
- $y^{(4)} + 3y'' - y = 0$ hat **Ordnung 4** (wegen $y^{(4)}$)

### Lineare Differentialgleichungen

Eine DGL heißt **linear**, wenn nur **Linearkombinationen** der Funktion $y$ und ihrer Ableitungen vorkommen.

**Beispiele:**
- ✅ $y' = ay$ ist **linear**
- ✅ $y'' + 2y' + 3y = 0$ ist **linear**
- ❌ $y' = y^2$ ist **nicht linear** (wegen $y^2$)

---

## 2. Lineare Differentialgleichungen 1. Ordnung

### Skalare DGL 1. Ordnung

Betrachte die lineare DGL 1. Ordnung

$$\boxed{y' = ay}$$

mit gegebenem $a \in K$ (wobei $K = \mathbb{R}$ oder $K = \mathbb{C}$) und gesuchter Funktion $y: \mathbb{R} \to K$.

### Satz (Allgemeine Lösung)

Jede Lösung der DGL $y' = ay$ ist von der Form

$$\boxed{y(t) = ce^{at}}$$

mit einer Konstanten $c \in K$.

**Insbesondere:** Die Lösungsmenge ist ein **eindimensionaler Teilraum** der differenzierbaren Funktionen, und $\{e^{at}\}$ ist eine **Basis** dieses Teilraums.

### Beweis

**Zeigen:** Wenn $y'(t) = ay(t)$, dann ist $y(t) = ce^{at}$.

Sei $y(t)$ eine Lösung der DGL. Betrachte die Funktion

$$f(t) = e^{-at}y(t)$$

Dann gilt:

$$f'(t) = (e^{-at}y(t))' = -ae^{-at}y(t) + e^{-at}y'(t) = -ae^{-at}y(t) + e^{-at}ay(t) = 0$$

Daher ist $f$ auf ganz $\mathbb{R}$ **konstant** (nach dem Konstanzkriterium), d.h. es gibt eine Konstante $c$ mit

$$c = f(t) = e^{-at}y(t)$$

und daher ist $y(t) = ce^{at}$. ✓

---

## 3. Anfangswertprobleme 1. Ordnung

### Definition (Anfangswertproblem)

Erfüllt die Funktion $y$ die Differentialgleichung $y' = ay$ und hat die Funktion zu einem Zeitpunkt $t_0$ einen bekannten Wert $y_0$, d.h. gilt auch $y(t_0) = y_0$, so spricht man von einem **Anfangswertproblem (AWP)**.

- $t_0$ heißt **Anfangszeitpunkt**
- $y_0$ heißt **Anfangswert** der Funktion

### Satz (Eindeutige Lösung des AWP)

Das Anfangswertproblem

$$\boxed{\begin{cases} y' = ay \\ y(t_0) = y_0 \end{cases}}$$

mit $a \in K$ hat die **eindeutige Lösung**

$$\boxed{y(t) = e^{a(t-t_0)}y_0, \quad t \in \mathbb{R}}$$

### Beweis

Jede Lösung der DGL hat die Form $y(t) = ce^{at}$.

Aus der Anfangsbedingung: $y_0 = y(t_0) = ce^{at_0}$

Also: $c = e^{-at_0}y_0$

Damit: $y(t) = e^{-at_0}y_0 \cdot e^{at} = e^{a(t-t_0)}y_0$ ✓

### Beispiel: Radioaktiver Zerfall

Radioaktives Kalium-42 zerfällt gemäß der DGL $y' = -0.055y$, wobei $y(t)$ die Masse (in Gramm) an vorhandenem Kalium zum Zeitpunkt $t$ (in Stunden) ist.

**Allgemeine Lösung:** $y(t) = ce^{-0.055t}$

**Mit Anfangswert:** Beträgt die Masse zum Zeitpunkt $t_0 = 0$ dann 12 g, so ist

$$y(t) = 12e^{-0.055t}$$

die Masse zum Zeitpunkt $t$.

---

## 4. Systeme linearer DGL 1. Ordnung

### Matrixexponential

Für eine **Diagonalmatrix** $D = \text{diag}(\lambda_1, \ldots, \lambda_n)$ definieren wir:

$$\boxed{e^{tD} = \begin{pmatrix} e^{t\lambda_1} & & \\ & \ddots & \\ & & e^{t\lambda_n} \end{pmatrix}}$$

Für eine **diagonalisierbare Matrix** $A = SDS^{-1}$ definieren wir:

$$\boxed{e^{tA} = Se^{tD}S^{-1}}$$

**Alternative Definition** (auch für nicht-diagonalisierbare Matrizen):

$$\boxed{e^{tA} = \sum_{k=0}^{\infty} \frac{t^k A^k}{k!}}$$

Diese Definition funktioniert **immer**, auch wenn $A$ nicht diagonalisierbar ist.

### Satz (Systeme linearer DGL 1. Ordnung)

Sei $A \in K^{n,n}$.

**1. Allgemeine Lösung:** Das lineare Differentialgleichungssystem 1. Ordnung

$$\boxed{\vec{y}' = A\vec{y}}$$

hat die allgemeine Lösung

$$\boxed{\vec{y}(t) = e^{tA}\vec{c}}$$

mit $\vec{c} \in K^n$. Insbesondere ist die Lösungsmenge ein **$n$-dimensionaler Vektorraum**.

**2. Anfangswertproblem:** Das AWP

$$\boxed{\begin{cases} \vec{y}' = A\vec{y} \\ \vec{y}(t_0) = \vec{y}_0 \in K^n \end{cases}}$$

hat die **eindeutige Lösung**

$$\boxed{\vec{y}(t) = e^{(t-t_0)A}\vec{y}_0}$$

### Herleitung für diagonalisierbare Matrizen

Sei $A = SDS^{-1}$ mit Diagonalmatrix $D = \text{diag}(\lambda_1, \ldots, \lambda_n)$.

**Schritt 1:** Die DGL $\vec{y}' = A\vec{y}$ wird zu:

$$\vec{y}' = SDS^{-1}\vec{y}$$

Multipliziere mit $S^{-1}$:

$$(S^{-1}\vec{y})' = S^{-1}\vec{y}' = D(S^{-1}\vec{y})$$

**Schritt 2:** Setze $\vec{z} = S^{-1}\vec{y}$. Dann gilt:

$$\vec{z}' = D\vec{z}$$

Dies ist ein **entkoppeltes System**:

$$\begin{cases} z_1' = \lambda_1 z_1 \\ z_2' = \lambda_2 z_2 \\ \vdots \\ z_n' = \lambda_n z_n \end{cases}$$

**Schritt 3:** Löse die skalaren DGL:

$$z_k(t) = c_k e^{\lambda_k t}, \quad k = 1, \ldots, n$$

Also:

$$\vec{z}(t) = \begin{pmatrix} c_1 e^{\lambda_1 t} \\ \vdots \\ c_n e^{\lambda_n t} \end{pmatrix} = e^{tD}\vec{c}$$

**Schritt 4:** Rücktransformation:

$$\vec{y}(t) = S\vec{z}(t) = Se^{tD}S^{-1}S\vec{c} = e^{tA}\vec{c}$$

### Beispiel 1: Diagonalmatrix

Die DGL $\vec{y}' = \begin{pmatrix} 2 & 0 \\ 0 & 3 \end{pmatrix} \vec{y}$ hat die Lösungen:

$$\vec{y}(t) = \begin{pmatrix} e^{2t} & 0 \\ 0 & e^{3t} \end{pmatrix} \begin{pmatrix} c_1 \\ c_2 \end{pmatrix} = \begin{pmatrix} c_1 e^{2t} \\ c_2 e^{3t} \end{pmatrix}$$

Mit Anfangswert $\vec{y}(1) = \begin{pmatrix} 5 \\ 7 \end{pmatrix}$:

$$\vec{y}(t) = \begin{pmatrix} 5e^{2(t-1)} \\ 7e^{3(t-1)} \end{pmatrix}$$

### Beispiel 2: Nicht-diagonale Matrix

$\vec{y}' = \begin{pmatrix} 2 & 1 \\ 0 & 3 \end{pmatrix} \vec{y}$

**Diagonalisierung:**

$$A = SDS^{-1} = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} 2 & 0 \\ 0 & 3 \end{pmatrix} \begin{pmatrix} 1 & -1 \\ 0 & 1 \end{pmatrix}$$

**Matrixexponential:**

$$e^{tA} = \begin{pmatrix} 1 & 1 \\ 0 & 1 \end{pmatrix} \begin{pmatrix} e^{2t} & 0 \\ 0 & e^{3t} \end{pmatrix} \begin{pmatrix} 1 & -1 \\ 0 & 1 \end{pmatrix} = \begin{pmatrix} e^{2t} & e^{3t} - e^{2t} \\ 0 & e^{3t} \end{pmatrix}$$

**Allgemeine Lösung:**

$$\vec{y}(t) = \begin{pmatrix} e^{2t} & e^{3t} - e^{2t} \\ 0 & e^{3t} \end{pmatrix} \begin{pmatrix} c_1 \\ c_2 \end{pmatrix} = \begin{pmatrix} (c_1 - c_2)e^{2t} + c_2 e^{3t} \\ c_2 e^{3t} \end{pmatrix}$$

Mit Anfangswert $\vec{y}(1) = \begin{pmatrix} 5 \\ 7 \end{pmatrix}$:

$$\vec{y}(t) = \begin{pmatrix} -2e^{2(t-1)} + 7e^{3(t-1)} \\ 7e^{3(t-1)} \end{pmatrix}$$

---

## 5. Lineare skalare DGL 2. Ordnung

### Harmonische Schwingung

Betrachte die lineare DGL 2. Ordnung:

$$\boxed{x'' + \omega^2 x = 0}$$

wobei $\omega > 0$ gegeben und $x = x(t)$ die gesuchte Funktion ist.

**Beobachtung:** $\cos(\omega t)$ und $\sin(\omega t)$ sind Lösungen.

Da die DGL linear ist, sind auch alle Linearkombinationen Lösungen.

### Trick: Reduktion auf System 1. Ordnung

Betrachte die **Hilfsfunktion**:

$$\vec{y}(t) = \begin{pmatrix} x'(t) \\ x(t) \end{pmatrix}$$

Dann ist:

$$\vec{y}'(t) = \begin{pmatrix} x''(t) \\ x'(t) \end{pmatrix} = \begin{pmatrix} -\omega^2 x(t) \\ x'(t) \end{pmatrix} = \begin{pmatrix} 0 & -\omega^2 \\ 1 & 0 \end{pmatrix} \begin{pmatrix} x'(t) \\ x(t) \end{pmatrix} = A\vec{y}(t)$$

Dies ist ein **lineares DGL-System 1. Ordnung**: $\vec{y}' = A\vec{y}$

**Lösung:** $\vec{y}(t) = e^{tA}\vec{c}$

Der Lösungsraum ist **zweidimensional**. Da $\sin(\omega t)$ und $\cos(\omega t)$ für $\omega > 0$ linear unabhängig sind, bilden sie eine **Basis** des Lösungsraums.

### Satz (Allgemeine Lösung)

Alle Lösungen von $x'' + \omega^2 x = 0$ haben die Gestalt:

$$\boxed{x(t) = c_1 \cos(\omega t) + c_2 \sin(\omega t)}$$

mit Konstanten $c_1, c_2 \in \mathbb{R}$.

Die Lösungen sind **harmonische Schwingungen**.

### Berechnung von $e^{tA}$

Die Matrix $A = \begin{pmatrix} 0 & -\omega^2 \\ 1 & 0 \end{pmatrix}$ hat charakteristisches Polynom:

$$p_A(z) = z^2 + \omega^2 = (z - i\omega)(z + i\omega)$$

**Eigenwerte:** $\lambda_1 = i\omega$, $\lambda_2 = -i\omega$

**Eigenräume:**

$$\text{Kern}(A - i\omega I) = \text{span}\left\{\begin{pmatrix} i\omega \\ 1 \end{pmatrix}\right\}, \quad \text{Kern}(A + i\omega I) = \text{span}\left\{\begin{pmatrix} -i\omega \\ 1 \end{pmatrix}\right\}$$

**Diagonalisierung:** $A = SDS^{-1}$ mit

$$S = \begin{pmatrix} i\omega & -i\omega \\ 1 & 1 \end{pmatrix}, \quad D = \begin{pmatrix} i\omega & 0 \\ 0 & -i\omega \end{pmatrix}, \quad S^{-1} = \frac{1}{2i\omega}\begin{pmatrix} 1 & i\omega \\ -1 & i\omega \end{pmatrix}$$

**Matrixexponential** (mit Euler-Formel $e^{i\omega t} = \cos(\omega t) + i\sin(\omega t)$):

$$\boxed{e^{tA} = \begin{pmatrix} \cos(\omega t) & -\omega\sin(\omega t) \\ \frac{1}{\omega}\sin(\omega t) & \cos(\omega t) \end{pmatrix}}$$

**Euler-Formel Umformungen:**

$$\cos(\omega t) = \text{Re}(e^{i\omega t}) = \frac{1}{2}(e^{i\omega t} + e^{-i\omega t})$$

$$\sin(\omega t) = \text{Im}(e^{i\omega t}) = \frac{1}{2i}(e^{i\omega t} - e^{-i\omega t})$$

---

## 6. Gedämpfte harmonische Schwingung

### Differentialgleichung

Betrachte die **linear gedämpfte Schwingung**:

$$\boxed{x'' + 2\beta x' + \omega_0^2 x = 0}$$

wobei:
- $\beta = \frac{b}{2m} > 0$ die **Abklingkonstante**
- $\omega_0 = \sqrt{\frac{k}{m}}$ die **ungedämpfte Eigenkreisfrequenz**

### Lösung über Matrixexponential

Mit $\vec{y}(t) = \begin{pmatrix} x'(t) \\ x(t) \end{pmatrix}$ ist:

$$\vec{y}'(t) = \begin{pmatrix} -2\beta & -\omega_0^2 \\ 1 & 0 \end{pmatrix} \vec{y}(t) = A\vec{y}(t)$$

**Charakteristisches Polynom:**

$$p_A(z) = z^2 + 2\beta z + \omega_0^2$$

**Eigenwerte:**

$$\boxed{\lambda_\pm = -\beta \pm \sqrt{\beta^2 - \omega_0^2}}$$

Das Verhalten der Lösungen hängt von $\beta^2 - \omega_0^2$ ab:

### Fall 1: Kriechfall ($\beta^2 > \omega_0^2$)

Der Term unter der Wurzel ist **positiv**, also hat $A$ zwei verschiedene **reelle Eigenwerte** $\lambda_+, \lambda_- < 0$.

**Lösung:**

$$\boxed{x(t) = c_1 e^{\lambda_+ t} + c_2 e^{\lambda_- t}}$$

mit Konstanten $c_1, c_2$.

Da beide Eigenwerte **negativ** sind, klingt die Lösung **exponentiell ab** ohne zu schwingen.

**Name:** **Kriechfall** (aperiodischer Fall, starke Dämpfung)

### Fall 2: Aperiodischer Grenzfall ($\beta^2 = \omega_0^2$)

$A$ hat zwei **gleiche Eigenwerte** $\lambda_+ = \lambda_- = -\beta$.

Die Matrix $A$ ist **nicht diagonalisierbar**.

**Lösung:**

$$\boxed{x(t) = c_1 e^{-\beta t} + c_2 t e^{-\beta t}}$$

**Name:** **Aperiodischer Grenzfall** (kritische Dämpfung)

### Fall 3: Schwingfall ($\beta^2 < \omega_0^2$)

Der Term unter der Wurzel ist **negativ**, also hat $A$ zwei verschiedene **komplexe Eigenwerte**:

$$\lambda_\pm = -\beta \pm i\sqrt{\omega_0^2 - \beta^2} = -\beta \pm i\omega_d$$

wobei $\omega_d = \sqrt{\omega_0^2 - \beta^2} > 0$ die **gedämpfte Eigenkreisfrequenz** ist.

**Lösung:**

$$x(t) = c_1 e^{\lambda_+ t} + c_2 e^{\lambda_- t} = e^{-\beta t}(c_1 e^{i\omega_d t} + c_2 e^{-i\omega_d t})$$

Mit Euler-Formel:

$$\boxed{x(t) = e^{-\beta t}(d_1 \sin(\omega_d t) + d_2 \cos(\omega_d t))}$$

Der zweite Faktor beschreibt eine **Schwingung** (mit Frequenz $\omega_d$), der erste Faktor $e^{-\beta t}$ **dämpft** die Schwingung exponentiell ab.

**Name:** **Schwingfall** (schwache Dämpfung)

### Spezialfall: Ungedämpfte Schwingung ($\beta = 0$)

Ist $\beta = 0$ (keine Dämpfung), so ist die DGL $x'' + \omega_0^2 x = 0$.

Der Dämpfungsterm verschwindet und wir haben wieder eine **freie harmonische Schwingung**:

$$x(t) = c_1 \cos(\omega_0 t) + c_2 \sin(\omega_0 t)$$

### Grafische Darstellung

```
    |
  2 |                Kriechfall (β² > ω₀²)
    |               /
  1 |              /  Grenzfall (β² = ω₀²)
    |    ________/
  0 |---/-------------------- Schwingfall (β² < ω₀²)
    |  /      ~~~~~
 -1 |        ~   ~
    |___________________________
      0   5   10  15  20  25  30
```

- **Kriechfall:** Langsames exponentielles Abklingen ohne Schwingung
- **Grenzfall:** Schnellstes Abklingen ohne Überschwingen
- **Schwingfall:** Gedämpfte Schwingung

---

## 7. Allgemeine Methode für DGL höherer Ordnung

### DGL $n$-ter Ordnung

Eine allgemeine lineare DGL $n$-ter Ordnung:

$$x^{(n)} + a_{n-1}x^{(n-1)} + \ldots + a_1 x' + a_0 x = 0$$

kann durch den **gleichen Trick** gelöst werden:

Setze:

$$\vec{y} = \begin{pmatrix} x^{(n-1)} \\ \vdots \\ x' \\ x \end{pmatrix}$$

Dann ist $\vec{y}' = A\vec{y}$ für eine geeignete Matrix $A$, und die Lösung ist $\vec{y} = e^{tA}\vec{c}$.

---

## 📌 Zusammenfassung

### DGL 1. Ordnung

| DGL | Allgemeine Lösung | AWP-Lösung |
|-----|-------------------|------------|
| $y' = ay$ | $y(t) = ce^{at}$ | $y(t) = e^{a(t-t_0)}y_0$ |
| $\vec{y}' = A\vec{y}$ | $\vec{y}(t) = e^{tA}\vec{c}$ | $\vec{y}(t) = e^{(t-t_0)A}\vec{y}_0$ |

### Matrixexponential

**Diagonalisierbar:** Wenn $A = SDS^{-1}$, dann

$$e^{tA} = Se^{tD}S^{-1} = S\begin{pmatrix} e^{t\lambda_1} & & \\ & \ddots & \\ & & e^{t\lambda_n} \end{pmatrix}S^{-1}$$

**Allgemein:**

$$e^{tA} = \sum_{k=0}^{\infty} \frac{t^k A^k}{k!}$$

### DGL 2. Ordnung

| DGL | Lösung |
|-----|--------|
| $x'' + \omega^2 x = 0$ | $x(t) = c_1\cos(\omega t) + c_2\sin(\omega t)$ |
| $x'' + 2\beta x' + \omega_0^2 x = 0$ | Abhängig von $\beta^2 - \omega_0^2$ |

### Gedämpfte Schwingung

**Eigenwerte:** $\lambda_\pm = -\beta \pm \sqrt{\beta^2 - \omega_0^2}$

| Fall | Bedingung | Name | Lösung |
|------|-----------|------|--------|
| 1 | $\beta^2 > \omega_0^2$ | **Kriechfall** | $x(t) = c_1 e^{\lambda_+ t} + c_2 e^{\lambda_- t}$ |
| 2 | $\beta^2 = \omega_0^2$ | **Grenzfall** | $x(t) = (c_1 + c_2 t)e^{-\beta t}$ |
| 3 | $\beta^2 < \omega_0^2$ | **Schwingfall** | $x(t) = e^{-\beta t}(c_1\sin(\omega_d t) + c_2\cos(\omega_d t))$ |

mit $\omega_d = \sqrt{\omega_0^2 - \beta^2}$

### Wichtige Formeln

**Euler-Formel:**

$$e^{i\omega t} = \cos(\omega t) + i\sin(\omega t)$$

$$\cos(\omega t) = \frac{1}{2}(e^{i\omega t} + e^{-i\omega t}), \quad \sin(\omega t) = \frac{1}{2i}(e^{i\omega t} - e^{-i\omega t})$$

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.23 Mittelwertsatz]]: Beweis für DGL 1. Ordnung
- [[VL.26 Elementare Funktionen 2]]: $e^{at}$ als Lösung
- [[VL.27 Elementare Funktionen 3]]: Harmonische Schwingungen
- [[VL.33 Eigenwerte]]: Diagonalisierung für Systeme
- [[VL.34 Diagonalisierbarkeit]]: Definition von $e^{tA}$
- [[VL.42 Potenzreihen]]: Exponentialreihe für Matrixexponential
