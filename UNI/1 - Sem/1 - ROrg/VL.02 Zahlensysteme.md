**Class:** [[ROrg]]  
**Date:** 2025  
**Topics:** #Zahlensysteme #2Komplement #Binärarithmetik #Gleitkommazahlen #IEEE754 #Overflow #Konvertierung

---

## 🎯 Lernziele der Vorlesung

Zahlendarstellung in Computersystemen verstehen und arithmetische Operationen durchführen können.

- **Binär-/Oktal-/Hexadezimalzahlen** in Dezimal konvertieren und umgekehrt
- **2-Komplement-Zahlen** berechnen und negieren
- **Arithmetische Operationen** mit Binärzahlen durchführen
- **Überlauf (Overflow)** erklären und erkennen
- **IEEE 754 Floating-Point-Standard** verstehen und anwenden
- Arithmetische Operationen mit Gleitkommazahlen durchführen

---

## 1. Zahlensysteme und Konvertierung

### Allgemeine Zahlendarstellung

Natürliche Zahlen können in jeder Basis $B$ repräsentiert werden:

$$\boxed{(a_{n-1}a_{n-2} \ldots a_1a_0)_B = \sum_{i=0}^{n-1} a_i \cdot B^i}$$

Dabei gilt:
- $B$: **Basis** (radix), z.B. 10 (dezimal), 2 (binär), 8 (oktal), 16 (hexadezimal)
- $B^i$: **Gewicht** (weight) der $i$-ten Ziffer
- $a_i$: $i$-te **Ziffer** (digit) aus der Menge $\{0, 1, \ldots, B-1\}$

**Beispiel (binär):**

$$1011_B = 1 \cdot 2^3 + 0 \cdot 2^2 + 1 \cdot 2^1 + 1 \cdot 2^0 = 8 + 0 + 2 + 1 = 11_D$$

### Binärzahlen (Dualzahlen)

**Menschen:** Dezimalzahlen (Basis 10)

$$2435_D = 2 \cdot 10^3 + 4 \cdot 10^2 + 3 \cdot 10^1 + 5 \cdot 10^0$$

**Rechner:** Binärzahlen (Basis 2)

$$\boxed{b_{n-1}b_{n-2} \ldots b_1b_0 = \sum_{i=0}^{n-1} b_i \cdot 2^i}$$

**Hintergrund:** Zwei Zustände sind einfach darstellbar
- Ein / Aus
- Hohes / Niedriges Potenzial ($V_{DD}$ / $GND$)
- Schwarz / Weiß

### Bits und Bytes

**Definitionen:**
- **1 Bit** = kleinste Einheit = eine Ziffer einer Dualzahl
- **1 Byte** = 8 Bit

**Beispiel:**

$$1 \text{ Byte} = 8 \text{ Bit} = \underbrace{1100\,1}_{\text{MSB}} \underbrace{1010}_{\text{LSB}}$$

- **MSB** (Most Significant Bit): Höchstwertiges Bit
- **LSB** (Least Significant Bit): Niedrigstwertiges Bit

**Darstellbarer Wertebereich:**

$$\boxed{\text{Mit } n \text{ Bit: } 0 \text{ bis } (2^n - 1)}$$

**Beispiel für $n = 3$:**

$$111_2 = 1 \cdot 2^2 + 1 \cdot 2^1 + 1 \cdot 2^0 = 4 + 2 + 1 = 7 = 2^3 - 1$$

⚠️ **Vorsicht bei Präfixen:**
- **Allgemein:** $1\text{ MB} = 10^6\text{ B} = 1\,000\,000\text{ B}$
- **Informatik:** $1\text{ MB} = 2^{20}\text{ B} = 1\,048\,576\text{ B}$
- Nicht immer eindeutig definiert!

---

## 2. Konvertierung zwischen Zahlensystemen

### Dezimal → Binär

**Algorithmus:** Wiederholte Division durch 2, Reste von unten nach oben lesen

**Beispiel:** $167_D \to \text{Binär}$

```
167 ÷ 2 = 83  Rest 1  ← LSB
 83 ÷ 2 = 41  Rest 1
 41 ÷ 2 = 20  Rest 1
 20 ÷ 2 = 10  Rest 0
 10 ÷ 2 =  5  Rest 0
  5 ÷ 2 =  2  Rest 1
  2 ÷ 2 =  1  Rest 0
  1 ÷ 2 =  0  Rest 1  ← MSB
```

$$\boxed{167_D = 10100111_B}$$

### Oktalzahlen (Basis 8)

**Oktal = $2^3$**, daher: **3 Binärstellen** entsprechen **1 Oktalziffer**

**Dezimal → Oktal:**

```
167 ÷ 8 = 20  Rest 7
 20 ÷ 8 =  2  Rest 4
  2 ÷ 8 =  0  Rest 2
```

$$167_D = 247_O$$

**Binär → Oktal:** Gruppierung in 3er-Blöcken von rechts

$$111\,000\,001\,011_B = 7\,0\,1\,3_O$$

### Hexadezimalzahlen (Basis 16)

**Hexadezimal = $2^4$**, daher: **4 Binärstellen** entsprechen **1 Hexziffer**

**Ziffernmenge:** $\{0, 1, 2, \ldots, 9, A, B, C, D, E, F\}$

**Dezimal → Hexadezimal:**

```
167 ÷ 16 = 10  Rest 7
 10 ÷ 16 =  0  Rest A
```

$$167_D = \text{A7}_H$$

In C/Java: `0xa7`

**Binär → Hexadezimal:** Gruppierung in 4er-Blöcken von rechts

$$0001\,0011\,0101\,0111\,1001\,1011\,1101\,1111_B = 13579\text{BDF}_H$$

---

## 3. Darstellung negativer Zahlen

### Drei Darstellungsmöglichkeiten

**1. Vorzeichen-/Betragszahlen (Sign-Magnitude)**
- MSB = Vorzeichenbit (0: positiv, 1: negativ)
- Restliche $(n-1)$ Bits = Betrag
- Beispiel: $5_D = 0101_B \to -5_D = 1101_B$

**2. 1-Komplement (One's Complement)**
- Negation durch Invertierung aller Bits
- Beispiel: $5_D = 0101_B \to -5_D = 1010_B$

**3. 2-Komplement (Two's Complement)** ✅ **Der Gewinner!**

$$\boxed{b_{n-1}b_{n-2} \ldots b_1b_0 = -b_{n-1} \cdot 2^{n-1} + \sum_{i=0}^{n-2} b_i \cdot 2^i}$$

- MSB hat **negatives Gewicht** ($-2^{n-1}$)
- Beispiel: $-5_D = -8 + 3 = 1000_B + 0011_B = 1011_B$

### Vergleich (4-Bit Beispiel)

| Dezimal | Sign-Magnitude | 1-Komplement | 2-Komplement |
|---------|----------------|--------------|--------------|
| -0      | 1000           | 1111         | —            |
| -1      | 1001           | 1110         | 1111         |
| -2      | 1010           | 1101         | 1110         |
| -3      | 1011           | 1100         | 1101         |
| -4      | 1100           | 1011         | 1100         |
| -5      | 1101           | 1010         | 1011         |
| -6      | 1110           | 1001         | 1010         |
| -7      | 1111           | 1000         | 1001         |
| -8      | —              | —            | 1000         |

### Warum 2-Komplement?

✅ **Vorteile:**
- Arithmetik ist einfacher (identisch zu vorzeichenlos)
- Es gibt nur **eine Darstellung der 0**
- Keine Sonderfälle bei Addition/Subtraktion

### Wertebereich (n-Bit 2-Komplement)

**Beispiel: 8 Bit**

$$\boxed{\text{Minimum: } -2^{n-1} = -2^7 = -128}$$

$$\boxed{\text{Maximum: } 2^{n-1} - 1 = 2^7 - 1 = 127}$$

**Beispiel: 32 Bit**

$$b_{31}b_{30} \ldots b_1b_0 = -b_{31} \cdot 2^{31} + \sum_{i=0}^{30} b_i \cdot 2^i$$

### Negation im 2-Komplement

$$\boxed{\text{Negation} = \text{Alle Bits invertieren} + 1}$$

**Beispiel (8-Bit):**

```
+105:  0110 1001
       ↓ invertieren
       1001 0110
       ↓ +1
-105:  1001 0111 = -128 + 16 + 7 = -105
```

**Rückwärts (Probe):**

```
-105:  1001 0111
       ↓ invertieren
       0110 1000
       ↓ +1
+105:  0110 1001 ✓
```

---

## 4. Arithmetische Operationen

### Binäre Addition

**Rechenregeln:**
- $0 + 0 = 0$
- $0 + 1 = 1$
- $1 + 0 = 1$
- $1 + 1 = 10$ (= 0 mit Übertrag 1)

**Beispiele (4-Bit, 2er-Komplement):**

```
  0010    (+2)
+ 0011    (+3)
------
  0101    (+5) ✓
  
    1
  0101    (+5)
+ 0110    (+6)
------
  1011    (-5) ⚠️ Overflow!
```

### Binäre Subtraktion

**Rechenregeln:**
- $0 - 0 = 0$
- $0 - 1 = 1$ (mit borrow = 1)
- $1 - 0 = 1$
- $1 - 1 = 0$

**Beispiel (4-Bit, 2er-Komplement):**

```
  0010    (+2)
- 0011    (-3)
------
  1111    (-1) ✓

borrows: 111_
```

**Alternative: Subtraktion durch Addition der Negation**

$$\boxed{A - B = A + (-B)}$$

Dieser Trick wird in der **ALU (Arithmetic Logic Unit)** genutzt!

**Beispiel:**

```
  0010    (+2)
- 0011    (-3)

Negiere 0011:
  0011 → 1100 (invertieren) → 1101 (+1)

  0010    (+2)
+ 1101    (-3)
------
  1111    (-1) ✓
```

---

## 5. Überlauf (Overflow)

### Definition

$$\boxed{\text{Overflow} = \text{Ergebnis zu groß für endliches Computer-Wort}}$$

**Problem:** Addition von zwei $n$-Bit-Zahlen kann $(n+1)$-Bit-Zahl ergeben!

### Wann tritt KEIN Overflow auf?

✅ **Addition von Zahlen mit entgegengesetztem Vorzeichen**
- Betrag der Summe immer $<$ Beträge der Operanden
- Beispiel: $-10 + 6 = -4$

✅ **Subtraktion von Zahlen mit demselben Vorzeichen**

### Wann tritt Overflow auf?

| Operation | $A$ | $B$ | Overflow wenn Vorzeichen des Ergebnisses |
|-----------|-----|-----|------------------------------------------|
| $A + B$   | $> 0$ | $> 0$ | $< 0$ (MSB = 1) |
| $A + B$   | $< 0$ | $< 0$ | $> 0$ (MSB = 0) |
| $A - B$   | $> 0$ | $< 0$ | $< 0$ (MSB = 1) |
| $A - B$   | $< 0$ | $> 0$ | $> 0$ (MSB = 0) |

### Overflow-Erkennung

$$\boxed{\text{Overflow} \iff \text{carry}_{\text{in}}^{\text{MSB}} \neq \text{carry}_{\text{out}}^{\text{MSB}}}$$

**Beispiel (4-Bit):**

```
     carry out → 0 1 ← carry in
                0101    (+5)
              + 0110    (+6)
                ----
                1011    (-5) ⚠️ Overflow!
                
carry_in(MSB) = 1 ≠ 0 = carry_out(MSB)
```

**Spezialfälle:**
- Kann Overflow auftreten, wenn $B = 0$? **Nein!**
- Kann Overflow auftreten, wenn $A = 0$? **Ja!** (z.B. $0 - (-2) = 2$ bei 2-Bit)

---

## 6. Multiplikation und Division

### Multiplikation

**Algorithmus:** Schulmathematik mit Binärzahlen

**Beispiel:** $13 \times 11$

```
Multiplikand:     1101    (13)
Multiplikator:  × 1011    (11)
              ----------
                  1101    (1101 × 1)
                 1101     (1101 × 1)
                0000      (1101 × 0)
             + 1101       (1101 × 1)
              ----------
Produkt:      10001111    (143)
```

⚠️ **Wichtig:** Produkt erfordert **doppelte Stellenanzahl**!

$$\boxed{n\text{-Bit} \times n\text{-Bit} = 2n\text{-Bit Produkt}}$$

### Division

**Algorithmus:** Schulmathematik (wiederholte Subtraktion)

**Beispiel:** $74 \div 8$

```
Dividend:  1001010  (74)
Divisor:      1000  (8)
           --------
Quotient:     1001  (9)
Rest:           10  (2)

→ 74 ÷ 8 = 9 Rest 2
```

**Schrittweise:**
1. $1001010 - 1000 = 1010$ (Quotient: 1)
2. $10100 - 1000 = 100$ (Quotient: 10)
3. $1000 - 1000 = 0$ (Quotient: 100)
4. $10 < 1000$ → Rest = 2 (Quotient: 1001)

---

## 7. Gleitkommazahlen (Floating Point)

### Gebrochene Zahlen in Binär

**Allgemeine Darstellung:**

$$\boxed{a_{n-1} \ldots a_0 , a_{-1}a_{-2} \ldots a_{-m} = \sum_{i=0}^{n-1} a_i B^i + \sum_{i=-m}^{-1} a_i B^i}$$

**Beispiel (binär):**

$$11,1010_B = 1 \cdot 2^1 + 1 \cdot 2^0 + 1 \cdot 2^{-1} + 0 \cdot 2^{-2} + 1 \cdot 2^{-3} + 0 \cdot 2^{-4}$$

$$= 2 + 1 + 0{,}5 + 0 + 0{,}125 + 0 = 3{,}625_D$$

### Konvertierung Dezimal → Binär (Nachkommastellen)

**Algorithmus:** Wiederholte Multiplikation mit 2

**Beispiel:** $0{,}24_D$

```
0,24 × 2 = 0,48 + 0  ← MSB
0,48 × 2 = 0,96 + 0
0,96 × 2 = 0,92 + 1
0,92 × 2 = 0,84 + 1
0,84 × 2 = 0,68 + 1
0,68 × 2 = 0,36 + 1
0,36 × 2 = 0,72 + 0
0,72 × 2 = 0,44 + 1  ← LSB (bei Abbruch nach 8 Stellen)
```

$$0{,}24_D \approx 0{,}00111101_B$$

⚠️ **Rundungsfehler** durch Ziffernbegrenzung möglich!

---

## 8. IEEE 754 Floating-Point-Standard

### Normalisierte Darstellung

$$\boxed{(-1)^s \times 1.f \times 2^e}$$

Dabei:
- $s$: **Vorzeichenbit** (sign): 0 = positiv, 1 = negativ
- $1.f$: **Mantisse** (significand) als normalisierte Zahl
  - Zahl wird geschoben, bis führende 1 vorhanden ist
  - Binärpunkt rechts von dieser 1: $1.0 \leq 1.f < 2.0$
- $f$: **Fraction** (Bruch) – nur $f$ wird gespeichert, führende 1 ist implizit!
- $e$: **Exponent** (vorzeichenbehaftet)
- $E$: **Transformierter Exponent** (unsigned)

$$\boxed{E = e + \text{bias}}$$

### IEEE 754 Formate

**Einfache Genauigkeit (Single Precision, 32 Bit):**

```
|  s  |     E     |           f           |
| 1 Bit | 8 Bit   |        23 Bit         |
```

- **bias** = 127
- C/Java: `float`
- $E = 0$ und $E = 255$ sind Sonderfälle

**Doppelte Genauigkeit (Double Precision, 64 Bit):**

```
|  s  |      E      |              f              |
| 1 Bit | 11 Bit    |           52 Bit            |
```

- **bias** = 1023
- C/Java: `double`

### Beispiel 1: $-0{,}75_D$ (Single Precision)

**Schritt 1:** Vorzeichen
- $s = 1$ (negativ)

**Schritt 2:** Dezimal → Binär
- $0{,}75_D = 0{,}11_B$

**Schritt 3:** Normalisieren
- $0{,}11_B = 1{,}1 \times 2^{-1}$
- Führende 1 ist implizit → Bruch: $f = 1000\ldots0$ (23 Bit)

**Schritt 4:** Transformierter Exponent
- $E = e + \text{bias} = -1 + 127 = 126 = 01111110_B$

**Ergebnis:**

```
| 1 | 0111 1110 | 100 0000 0000 0000 0000 0000 |
```

### Beispiel 2: $0{,}075_D$ (Single Precision)

**Schritt 1:** $s = 0$ (positiv)

**Schritt 2:** Konvertierung

```
0,075 × 2 = 0,150 + 0
0,150 × 2 = 0,300 + 0
0,300 × 2 = 0,600 + 0
0,600 × 2 = 0,200 + 1
0,200 × 2 = 0,400 + 0
0,400 × 2 = 0,800 + 0
0,800 × 2 = 0,600 + 1
0,600 × 2 = 0,200 + 1  (Periode!)
```

$$0{,}075_D = 0{,}0001\,0011\,0011\,0011\ldots_B$$

**Schritt 3:** Normalisieren
- $0{,}00010011_B = 1{,}0011 \times 2^{-4}$
- Bruch: $f = 0011\,0011\,0011\,0011\,0011\,001$

**Schritt 4:** Exponent
- $E = -4 + 127 = 123 = 01111011_B$

**Ergebnis:**

```
| 0 | 0111 1011 | 0011 0011 0011 0011 0011 001 |
```

---

## 9. IEEE 754 Sonderfälle

### Übersicht

| Wert               | $E$                | $f$      | Bedeutung                                  |
| ------------------ | ------------------ | -------- | ------------------------------------------ |
| **Null**           | 0                  | 0        | $(-1)^s \times 0$                          |
| **Unnormalisiert** | 0                  | $\neq 0$ | $(-1)^s \times 0.f \times 2^{-126/-1022}$  |
| **Normalisiert**   | $1 < E < 254/2046$ | beliebig | $(-1)^s \times 1.f \times 2^{E-127/-1023}$ |
| **Unendlich**      | 255/2047           | 0        | $(-1)^s \times \infty$                     |
| **NaN**            | 255/2047           | $\neq 0$ | Not a Number                               |

**Sonderfälle:**
- **Null:** Positiv/Negativ Null möglich
- **Unendlich:** z.B. Division durch Null
- **Unnormalisierte Zahlen:** Winzige (tiny) Zahlen nahe Null
- **NaN (Not a Number):** Ungültige Operationen wie $0/0$ oder $\sqrt{-1}$

---

## 10. Addition von Gleitkommazahlen

### Algorithmus

**Beispiel:** $X = 2{,}35_D$, $Y = 10{,}17_D$ (16-Bit Minifloat Format)

**Schritt 1: Normalisieren**

```
X = 2,35  = 10.0101 1001 1001... → 1.0010 1100 11 × 2¹
Y = 10,17 = 1010.0010 1011...    → 1.0100 0101 01 × 2³
```

→ Verlust von signifikanten Stellen durch Formatbegrenzung!

**Schritt 2: Exponentenanpassung**

Kleineren Exponent an größeren anpassen:

```
X = 0.0100 1011 00|11 × 2³
                  └─→ gehen verloren!
```

**Schritt 3: Mantissen addieren**

```
  0.0100 1011 00  (X)
+ 1.0100 0101 01  (Y)
------------------
  1.1001 0000 01  (Z)
```

**Schritt 4: Normalisieren (falls nötig)**

Hier bereits normalisiert.

**Ergebnis:**

$$Z = 1{,}1001\,0000\,01 \times 2^3 = 12{,}5078125$$

(Korrekter Wert wäre: $12{,}52$)

---

## 11. Der Pentium Bug (1994)

### Historischer Kontext

**Fehler im Divisionsalgorithmus für Gleitkommazahlen**

**Beispiel:**

$$\frac{4195835{,}0}{3145727{,}0} = 1{,}333\,820\,449\,136\,241\,002 \quad \text{(korrekt)}$$

$$\frac{4195835{,}0}{3145727{,}0} = 1{,}333\,739\,068\,902\,037\,589 \quad \text{(Pentium Fehler)}$$

### Chronologie

| Datum | Ereignis | Kosten |
|-------|----------|--------|
| **Juli 1994** | Intel entdeckt Fehler | ~100K\$ (Behebung) |
| **Sept. 1994** | Prof. Thomas Nicely entdeckt Fehler, keine Reaktion von Intel, veröffentlicht im Internet | — |
| **7. Nov. 1994** | EE Times bringt Story auf Titelseite | — |
| **22. Nov. 1994** | Intel: "Fehler an 9. Stelle, nur wenige Nutzer betroffen" | — |
| **5. Dez. 1994** | Intel: "Fehler nur einmal in 27000 Jahren bei typischer Anwendung" | — |
| **21. Dez. 1994** | Intel gibt nach: Jeder darf Pentium austauschen | **500 M\$!** |

**Lektion:** Transparenz und schnelle Reaktion bei Fehlern sind wichtig!

---

## 📌 Zusammenfassung

### Zahlensysteme

**Konvertierung:**

| Von → Nach | Methode |
|-----------|---------|
| Dezimal → Binär | Wiederholte Division durch 2, Reste von unten lesen |
| Binär → Oktal | Gruppierung in 3er-Blöcken |
| Binär → Hexadezimal | Gruppierung in 4er-Blöcken |
| Dezimal-Bruch → Binär | Wiederholte Multiplikation mit 2 |

### 2-Komplement

$$\boxed{b_{n-1}b_{n-2} \ldots b_0 = -b_{n-1} \cdot 2^{n-1} + \sum_{i=0}^{n-2} b_i \cdot 2^i}$$

**Negation:** Alle Bits invertieren + 1

**Wertebereich (n-Bit):** $-2^{n-1}$ bis $2^{n-1} - 1$

### Arithmetik

**Overflow tritt auf wenn:**
- Carry-in(MSB) ≠ Carry-out(MSB)
- Addition zweier positiver Zahlen → negatives Ergebnis
- Addition zweier negativer Zahlen → positives Ergebnis

**Subtraktion:** $A - B = A + (-B)$

**Multiplikation:** $n$-Bit × $n$-Bit = $2n$-Bit Produkt

### IEEE 754 Gleitkommazahlen

$$\boxed{(-1)^s \times 1.f \times 2^e \quad \text{wobei } E = e + \text{bias}}$$

**Single Precision (32 Bit):** 1 Bit Sign, 8 Bit Exponent, 23 Bit Fraction, bias = 127

**Double Precision (64 Bit):** 1 Bit Sign, 11 Bit Exponent, 52 Bit Fraction, bias = 1023

### Wichtige Erkenntnisse

✅ Bitmuster haben keine inhärente Bedeutung – Standards definieren Interpretation

✅ Computer-Arithmetik ist durch limitierte Genauigkeit beschränkt

✅ Overflow und Rundungsfehler müssen berücksichtigt werden

✅ Hardware-Implementierung muss Effizienz und Genauigkeit balancieren

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.01 Grundlegenden Ideen]]: Hardware-Grundlagen
- [[VL.03 Grundlagen Digitalerentwurf]]: Verwendung von Binärdarstellung in Befehlen
- [[VL.04 Befehle]]: Implementierung arithmetischer Operationen
- [[VL.05 Single Cycle]]: Verarbeitung von Zahlen im Prozessor