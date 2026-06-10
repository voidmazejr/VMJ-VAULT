**Class:** [[InfoProp]]  
**Date:** 25-12-2026 
**Topics:** #Kryptographie #RSA #Verschlüsselung #Primzahlen #ModulareArithmetik #Relevanz #SituatedKnowledge

---

## 🎯 Lernziele der Vorlesung

Kryptographie verstehen als Anwendungsbeispiel informatischer Entwicklung und Relevanz wissenschaftlicher Arbeit reflektieren.

- **Geschichte der Verschlüsselung** - von Caesar bis Enigma
- **Symmetrische vs. Asymmetrische Verschlüsselung**
- **RSA-Kryptosystem** - mathematische Grundlagen
- **Erweiterter Euklidischer Algorithmus** - Berechnung modularer Inverse
- **Relevanz** wissenschaftlicher Forschung
- **Situated Knowledge** - Objektivität im historischen Kontext

---

## 1. Objektivität im historischen Kontext

### Klassische Wissenschaftstheorie

**Forderung:**

Objektivität verlangt, dass individuelle **Biases** durch methodische Verfahren so weit wie möglich **kontrolliert** werden, sodass Ergebnisse **intersubjektiv prüfbar** bleiben.

### Situated Knowledge (Haraway, 1988)

**Kritik der klassischen Sicht:**

❌ **Falsche Annahme:** Objektivität garantiert, dass wissenschaftliche Erkenntnisse universell gültig sind, **unabhängig** von historischen oder kulturellen Kontexten.

✅ **Realität:** Wissen(schaft) ist **situiert** - findet immer im **historischen Kontext** statt

### Der Fall Alan Turing

**Historischer Kontext:**

- 1940er Jahre: Zweiter Weltkrieg
- Turing arbeitet in **Bletchley Park**, England
- Aufgabe: Entschlüsselung deutscher **Enigma**-Nachrichten
- **1952:** Turing wird wegen Homosexualität verurteilt
- **1954:** Tod durch Zyanidvergiftung (vermutlich Suizid)

**Bedeutung:**

Wissenschaftliche Arbeit ist **nie** losgelöst von gesellschaftlichen, politischen und persönlichen Umständen.

---

## 2. Die Enigma-Maschine

### Funktionsweise

**Prinzip:** Polyalphabetisches Substitutionsverfahren

**Komponenten:**

```
┌──────────────────────────────────────┐
│  1. Walzen (Rotoren)                 │
│     - 3 aus 5 auswählbar             │
│     - Je 26 Positionen (A-Z)         │
│                                      │
│  2. Ringstellungen                   │
│     - 26 Positionen pro Walze        │
│                                      │
│  3. Steckerbrett (Plugboard)         │
│     - Vertauschung von Buchstaben    │
└──────────────────────────────────────┘
```

**Tägliche Änderung der Konfiguration:**

- Walzenlage
- Walzenstellung
- Ringstellung
- Steckerverbindungen

→ **Kombinatorik:** Riesiger Schlüsselraum!

### Besondere Eigenschaft: Involutorische Verschlüsselung

$$\boxed{\text{Wenn } U \rightarrow X \text{, dann auch } X \rightarrow U}$$

**Bedeutung:** Die Enigma ist ihre eigene Inverse - dieselbe Einstellung ver- und entschlüsselt

### Turing's Lösung

**Turing-Bombe:**

- Reduziert den effektiven **Schlüsselraum**
- Nutzt die **Methode des wahrscheinlichen Wortes** (crib)
- Nutzt die **involutorische Verschlüsselung**

**Wichtig:** Lösung durch **Algorithmen** - Formalisierung des Denkens!

---

## 3. Geschichte der Kryptographie

### Grundbegriffe

**Kryptographie:** (kryptos = verborgen, geheim; graphein = schreiben)

Wissenschaft der **Verschlüsselung** von Informationen

**Kryptologie:** (logos = Wort, richtige Einsicht)

Wissenschaft eines bestimmten Fachgebietes

### Chiffre vs. Code

| Chiffre | Code |
|---------|------|
| **Austausch von Buchstaben** | **Zuordnung bedeutungsvoller Einheiten** |
| Einzelne Zeichen werden ersetzt | Ganze Wörter/Phrasen werden ersetzt |
| Beispiel: Caesar-Chiffre | Beispiel: "RED ALERT" → "Situation A" |

---

## 4. Monoalphabetische Verfahren

### Definition

$$\boxed{\text{Monoalphabetisch} = \text{Verwendet 1 Zuordnung von Klartext- zu Chiffretextbuchstaben}}$$

### Beispiel: Leibniz' Verschlüsselung mit Schlüsselwort

**Schlüsselwort:** BOXKAMPFJURY

**Aufbau der Substitutionstabelle:**

```
Schlüsselwort (ohne Wiederholungen): B O X K A M P F J U R Y
Rest des Alphabets:                   C D E G H I L N Q S T V W Z

Klartext:  A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
Chiffre:   B O X K A M P F J U R Y C D E G I L N S T V W Z
```

**Beispiel:**

```
Klartext:  GUTEN MORGEN
Chiffre:   XYUOP CKFXOP
```

### Schwächen monoalphabetischer Verfahren

❌ **Häufigkeitsanalyse möglich:**

Buchstabenhäufigkeiten bleiben erhalten!

**Deutsch:**
- E: ~17%
- N: ~10%
- I, R, S, T: ~6-7%

**Englisch:**
- E: ~12%
- T: ~9%
- A, O, I, N: ~7-8%

**Polnisch:**
- A: ~9%
- I: ~8%
- O, E: ~7-8%

❌ **Fehleranfällig** bei manueller Ausführung

❌ **Leicht zu dechiffrieren** mit genügend Chiffretext

---

## 5. Caesar-Chiffre - Substitutionschiffre

### Prinzip

**Modulare Arithmetik** mit kleiner Anzahl an Schlüsseln

### Algorithmus

**1. Buchstaben → Zahlen:**

A=0, B=1, C=2, ..., Z=25

**2. Verschlüsseln:**

$$\boxed{c = (m + k) \mod 26}$$

Wo:
- $m$ = Klartextbuchstabe (als Zahl)
- $k$ = Schlüssel (Verschiebung)
- $c$ = Chiffretextbuchstabe (als Zahl)

**3. Entschlüsseln:**

$$\boxed{m = (c - k) \mod 26}$$

### Beispiel: Schlüssel k = 7

```
Klartext:  HILFE KOMMT ZU SPAET RUECKZUG
Chiffre:   ABEYX DHFFM SN LITXM KNXVDSNZ
```

**Visualisierung:**

```
Scheibe um 7 Schritte drehen:

Außen (Klar): A B C D E F G H I J K  L  M  N  O  P  Q  R  S  T  U  V  W  X  Y  Z
Innen (Chif): T U V W X Y Z A B C D  E  F  G  H  I  J  K  L  M  N  O  P  Q  R  S
```

### Schwäche

❌ Nur **26 mögliche Schlüssel** - alle durchprobierbar!

---

## 6. Polyalphabetische Verfahren

### Definition

$$\boxed{\text{Polyalphabetisch} = \text{Substitutionsverfahren mit mehr als einem Alphabet}}$$

### Zwei Ansätze

**1. Enigma:**

Änderung des Alphabets in **vorhersagbarer** Art und Weise (mechanisch durch Walzendrehung)

**2. Machina Deciphratoria (Leibniz):**

Änderung des Alphabets in **irregulärer** Art und Weise durch mechanische Staffelwalze

---

## 7. One-Time-Pad (OTP)

### Prinzip

**Vergrößerung der Schlüsselmenge** durch Schlüssel"wörter"

### Beispiel

```
Klartext:   B B B B B
Schlüssel:  C H I F F R E
           ─────────────
Chiffrat:   D I ...

Alphabet 1: A→C, B→D
Alphabet 2: A→H, B→I
```

### Sicherheitsbedingungen

✅ **Schlüssel** muss **mindestens gleich lang** sein wie Klarnachricht

✅ **Schlüssel** ist **zufällig** gewählte Buchstabenfolge

✅ Pro Nachricht ein **anderer Schlüssel** → **One-Time-Pad**

**Wenn diese Bedingungen erfüllt sind:** **Perfekt sicher!** (informationstheoretisch beweisbar)

---

## 8. Symmetrische Verschlüsselung

### Definition

$$\boxed{\text{Symmetrisch} = \text{Sender und Empfänger benutzen denselben Schlüssel}}$$

### Probleme

**1. Viele Partner = Viele Schlüssel:**

Für $n$ Personen, die untereinander kommunizieren:

$$\text{Anzahl Schlüssel} = \frac{n(n-1)}{2}$$

**Beispiel:** 12 Personen = $\frac{12 \times 11}{2} = 66$ Schlüssel!

**2. Große Menge an Schlüsselmaterial:**

Bei One-Time-Pad: Schlüssel so lang wie alle Nachrichten zusammen!

**3. Schlüsselübertragung:**

Der Schlüssel muss **sicher übertragen** werden - wie?

```
┌─────┐    Schlüssel?     ┌─────┐
│Alice├──────────────────>│ Bob │
└─────┘                   └─────┘
   │                         │
   │   Verschlüsselte        │
   │      Nachricht          │
   └────────────────────────>│
```

---

## 9. Das RSA-Kryptosystem (1977)

### Die Entwickler

**Rivest, Shamir, Adleman**

- 1977: Veröffentlichung
- 2002: **Turing Award**
- Erstes veröffentlichtes **asymmetrisches** Verschlüsselungsverfahren

### Grundidee: Asymmetrische Verschlüsselung

$$\boxed{\text{Asymmetrisch} = \text{Verschiedene Schlüssel zum Ver- und Entschlüsseln}}$$

**Schlüsselpaar:**

```
┌────────────────────────────────────┐
│  1. Öffentlicher Schlüssel         │
│     (public key)                   │
│     → Zum Verschlüsseln            │
│     → Jeder kann ihn kennen        │
└────────────────────────────────────┘

┌────────────────────────────────────┐
│  2. Privater Schlüssel             │
│     (private key)                  │
│     → Zum Entschlüsseln            │
│     → Nur Empfänger kennt ihn      │
└────────────────────────────────────┘
```

**Vorteile:**

✅ **Verschlüsseln** kann jede mit dem public key

✅ **Entschlüsseln** kann nur Inhaber des private key

✅ **Kein Schlüsselaustausch** notwendig!

✅ Für $n$ Personen: nur $n$ Schlüsselpaare (statt $\frac{n(n-1)}{2}$ Schlüssel)

---

## 10. Mathematische Grundlage: Einwegfunktionen

### One-Way Function

$$\boxed{\text{Einwegfunktion} = \text{In einer Richtung einfach, Umkehrfunktion schwer}}$$

**Beispiel für RSA:**

```
Einfach:       2 große Primzahlen multiplizieren
               p × q = n
                 ↓
               Ergebnis n (z.B. 600 Dezimalstellen)

Schwierig:     Große Zahl n in Primfaktoren zerlegen
               n = ? × ?
                 ↓
               Primfaktorzerlegung praktisch unmöglich
```

### Trapdoor One-Way Function (Falltürfunktion)

$$\boxed{\text{Mit Zusatzinformation (trapdoor) ist Umkehrung leicht}}$$

**Bei RSA:**

- **Öffentlich:** $n = p \times q$
- **Geheim (trapdoor):** $p$ und $q$ selbst
- **Mit trapdoor:** Entschlüsselung einfach
- **Ohne trapdoor:** Entschlüsselung praktisch unmöglich

---

## 11. Mathematische Werkzeuge für RSA

### Primfaktorzerlegung

**Jede natürliche Zahl** $n$ lässt sich als Produkt aus Primzahlen darstellen.

**Beispiel:**

$$4200 = 2 \times 2 \times 2 \times 3 \times 5 \times 5 \times 7 = 2^3 \times 3 \times 5^2 \times 7$$

**Problem:** Für **große Zahlen** ist bisher **kein effizientes** Faktorisierungsverfahren bekannt!

### Teilerfremdheit

**Definition:**

Zwei Zahlen $a$ und $b$ sind **teilerfremd**, wenn $\text{ggT}(a, b) = 1$

**Beispiel:**

$$\text{ggT}(5, 48) = 1 \quad \Rightarrow \quad 5 \text{ und } 48 \text{ sind teilerfremd}$$

### Modularer Kehrwert (Inverse)

**Definition:**

Der **Kehrwert von** $a$ **modulo** $m$ ist eine positive Zahl $b < m$, die folgende Gleichung erfüllt:

$$\boxed{b \cdot a \equiv 1 \pmod{m}}$$

**Beispiel:** Kehrwert von 5 modulo 48?

$$b \cdot 5 \equiv 1 \pmod{48}$$

**Wichtig:** Ein modularer Kehrwert existiert **nur**, wenn $a$ und $m$ **teilerfremd** sind!

---

## 12. Erweiterter Euklidischer Algorithmus

### Problem

Finde den Kehrwert von $a = 5$ modulo $m = 48$

### Schritt 1: Standard Euklidischer Algorithmus

```
ggT(5, 48) = 1

48 = 9 × 5 + 3
5  = 1 × 3 + 2
3  = 1 × 2 + 1
2  = 2 × 1 + 0
```

**Ergebnis:** $\text{ggT}(5, 48) = 1$ ✓ (teilerfremd!)

### Schritt 2: Rückwärts arbeiten

**Ziel:** 1 darstellen als $k_1 \times 5 + k_2 \times 48$

```
1 = 3 - 1 × 2                          (aus Zeile 3)
  = 3 - 1 × (5 - 1 × 3)                (2 ersetzen aus Zeile 2)
  = 2 × 3 - 1 × 5                      (ausmultiplizieren)
  = 2 × (48 - 9 × 5) - 1 × 5           (3 ersetzen aus Zeile 1)
  = 2 × 48 - 19 × 5                    (ausmultiplizieren)
```

**Ergebnis:**

$$\boxed{-19 \times 5 + 2 \times 48 = 1}$$

### Schritt 3: Umformen

$$-19 \times 5 + 2 \times 48 = 1$$

Modulo 48 rechnen:

$$-19 \times 5 \equiv 1 \pmod{48}$$

Positiven Wert finden ($b < 48$):

$$-19 + 48 = 29$$

$$\boxed{29 \times 5 \equiv 1 \pmod{48}}$$

**Probe:** $29 \times 5 = 145 = 3 \times 48 + 1$ ✓

---

## 13. Übung: Modulare Inverse berechnen

### Aufgabe

Bestimme die modulare Inverse von $5$ modulo $24$!

### Lösung

**1. Testen auf Teilerfremdheit:**

```
ggT(5, 24):

24 = 4 × 5 + 4
5  = 1 × 4 + 1
4  = 4 × 1 + 0

ggT(5, 24) = 1 ✓
```

**2. Rückwärts arbeiten:**

```
1 = 5 - 1 × 4
  = 5 - 1 × (24 - 4 × 5)
  = 5 × 5 - 1 × 24

5 × 5 - 1 × 24 = 1
```

**3. Umformen:**

$$5 \times 5 \equiv 1 \pmod{24}$$

**Ergebnis:** Die modulare Inverse von $5$ modulo $24$ ist $\boxed{5}$

**Probe:** $5 \times 5 = 25 = 1 \times 24 + 1$ ✓

---

## 14. RSA - Schlüsselerzeugung

### Schritt-für-Schritt Anleitung

**Erzeuge Schlüsselpaar:** $(e, n)$ public, $(d, n)$ private

**1. Wähle 2 Primzahlen** $p$ und $q$

Beispiel: $p = 11$, $q = 17$

**2. Berechne den RSA-Modul:**

$$n = p \times q$$

Beispiel: $n = 11 \times 17 = 187$

**3. Berechne die Eulersche** $\varphi$**-Funktion:**

$$\varphi(n) = (p-1) \times (q-1)$$

Beispiel: $\varphi(187) = 10 \times 16 = 160$

**4. Wähle** $e$ **teilerfremd zu** $\varphi(n)$ **und** $< \varphi(n)$:

$$\text{ggT}(e, \varphi(n)) = 1$$

Beispiel: $e = 7$ (da $\text{ggT}(7, 160) = 1$)

**5. Berechne** $d$ **als Kehrwert von** $e$ **modulo** $\varphi(n)$:

$$d \cdot e \equiv 1 \pmod{\varphi(n)}$$

Beispiel: $d = 23$ (da $23 \times 7 = 161 = 1 \times 160 + 1$)

### Ergebnis

```
Public Key:  (n = 187, e = 7)
Private Key: (n = 187, d = 23)
```

---

## 15. RSA - Ver- und Entschlüsselung

### Verschlüsselung (Alice → Bob)

**Alice** verschlüsselt Nachricht $N$ mit **Bob's public key** $(e, n)$:

$$\boxed{C = N^e \mod n}$$

**Beispiel:**

```
Bob's public key: (187, 7)
Alice's Nachricht: N = 76

Verschlüsseln:
C = 76^7 mod 187 = 32
```

### Entschlüsselung (Bob)

**Bob** entschlüsselt $C$ mit seinem **private key** $(d, n)$:

$$\boxed{N = C^d \mod n = (N^e)^d \mod n}$$

**Beispiel:**

```
Bob's private key: (187, 23)
Empfangene Nachricht: C = 32

Entschlüsseln:
N = 32^23 mod 187 = 76 ✓
```

### Warum funktioniert das?

**Mathematischer Beweis** (vereinfacht):

Da $d \cdot e \equiv 1 \pmod{\varphi(n)}$, gibt es ein $k$ mit:

$$d \cdot e = 1 + k \cdot \varphi(n)$$

Nach dem **kleinen Satz von Fermat**:

$$(N^e)^d = N^{ed} = N^{1 + k \cdot \varphi(n)} = N \cdot (N^{\varphi(n)})^k \equiv N \cdot 1^k = N \pmod{n}$$

---

## 16. Sicherheit des RSA-Verfahrens

### Kann man den Code "knacken"?

**Wenn ein Angreifer** $p$ **und** $q$ **kennt:**

1. Kann sofort $n = p \times q$ berechnen
2. Kann sofort $\varphi(n) = (p-1) \times (q-1)$ berechnen
3. Da $e$ öffentlich ist, kann $d$ als Kehrwert von $e$ berechnet werden
4. **→ Code geknackt!**

### Sicherheit beruht auf "Erfahrung"

⚠️ **Wichtig:** Die Sicherheit beruht **NICHT** auf einem mathematischen Beweis!

**Annahme:**

Ist $n$ **groß genug** (z.B. 2048 Bit = ca. 600 Dezimalstellen), so ist es **praktisch unmöglich**, $n$ in Primfaktoren zu zerlegen.

**Problem:**

- Niemand hat **bewiesen**, dass Primfaktorzerlegung schwer ist
- Es ist nur **bisher kein effizienter Algorithmus bekannt**
- **Könnte** eines Tages ein effizienter Algorithmus gefunden werden

### Bedrohung durch Quantencomputer

⚠️ **Shor's Algorithmus** (1994):

Mit einem **leistungsfähigen Quantencomputer** kann RSA **leicht** geknackt werden!

- Der Algorithmus existiert bereits
- Nur die **Hardware fehlt noch** (Stand 2025)
- **Post-Quantum-Kryptographie** wird bereits entwickelt

---

## 17. Weitere Anwendung: Digitale Signaturen

### Prinzip

RSA ist **symmetrisch** bezüglich Ver- und Entschlüsselung:

$$(N^e)^d \equiv N \pmod{n} \quad \text{und} \quad (N^d)^e \equiv N \pmod{n}$$

### Anwendung

```
┌─────────────────────────────────────┐
│  Bob signiert Nachricht N:          │
│                                     │
│  1. Berechne S = N^d mod n          │
│     (mit seinem PRIVATE key!)       │
│                                     │
│  2. Sende (N, S) an Alice           │
└─────────────────────────────────────┘

┌─────────────────────────────────────┐
│  Alice verifiziert Signatur:        │
│                                     │
│  1. Berechne N' = S^e mod n         │
│     (mit Bob's PUBLIC key)          │
│                                     │
│  2. Prüfe: N' = N ?                 │
│     ✓ Ja → Signatur gültig          │
│     ✗ Nein → Signatur ungültig      │
└─────────────────────────────────────┘
```

**Bedeutung:**

- Nur **Bob** kann mit seinem private key signieren
- **Jeder** kann mit Bob's public key die Signatur **verifizieren**
- Garantiert **Authentizität** und **Integrität** der Nachricht

---

## 18. Praxis: Hybride Verschlüsselung

### Problem

**Asymmetrische Verfahren** (wie RSA) sind **langsam!**

**Symmetrische Verfahren** (wie AES) sind **schnell**, aber Schlüsselaustausch ist schwierig.

### Lösung: Kombination

```
Schritt 1: Asymmetrische Verschlüsselung für Schlüsselaustausch
────────────────────────────────────────────────────────────────
Alice:
  1. Erzeugt zufälligen symmetrischen Schlüssel K
  2. Verschlüsselt K mit Bob's public key: C_K = K^e mod n
  3. Sendet C_K an Bob

Bob:
  4. Entschlüsselt: K = C_K^d mod n
  
  → Beide kennen jetzt K!

Schritt 2: Symmetrische Verschlüsselung für Daten
────────────────────────────────────────────────────────────────
Alice & Bob:
  - Verwenden K für schnelle symmetrische Verschlüsselung
  - Z.B. mit AES (Advanced Encryption Standard)
  - Erzeugen für jede Session einen neuen K
```

**Vorteile:**

✅ **Sicherheit** der asymmetrischen Verschlüsselung für Schlüsselaustausch

✅ **Geschwindigkeit** der symmetrischen Verschlüsselung für Daten

✅ Kein Problem mit Schlüsselübertragung

---

## 19. Wissenschaftskriterium: Relevanz

### Definition nach Balzert et al. (2022)

$$\boxed{\text{Relevant} = \text{Was Wissen schafft und Probleme löst}}$$

**Relevant ist:**

✅ Was zum **wissenschaftlichen Fortschritt** beiträgt

✅ Was in der eigenen Wissenschaftsdisziplin **neues Wissen** schafft

✅ Was hilft, **Praxisprobleme** zu lösen

✅ Was einen **hohen Informationswert** hat

### Relevanz im Spannungsfeld

**Forschung findet statt im Spannungsfeld von:**

```
┌────────────────────────────────┐  ┌────────────────────────────────┐
│  WISSENSCHAFTLICHE QUALITÄT    │  │  GESELLSCHAFTLICHE FRAGEN      │
│                                │  │                                │
│  • Hoher Informationswert      │  │  • Technikfolgenabschätzung    │
│  • Präzise Dokumentation       │  │  • Dual Use                    │
│  • Überprüfbar                 │  │  • Verteilungsgerechtigkeit    │
│  • Nachvollziehbar             │  │  • Sicherheit                  │
│  • Erkenntniserweiterung       │  │  • Privatsphäre & Anonymität   │
│  • Praktischer Nutzen          │  │  • Kontext & Objektivität      │
└────────────────────────────────┘  └────────────────────────────────┘
```

### Computerethik

**Definition:**

Teilgebiet der **Technikethik**, das sich mit ethischen Fragen im Zusammenhang mit Computern und Informationstechnologie beschäftigt.

**Zentrale Fragen:**

- Wer profitiert von technischer Entwicklung?
- Wer trägt die Risiken?
- Wie werden Daten verwendet?
- Welche Folgen hat Technologie für Gesellschaft?

---

## 20. Beispiel Relevanz: RSA in der Praxis

### Wo wird RSA verwendet?

✅ **HTTPS** - Sichere Webseiten

✅ **E-Mail-Verschlüsselung** (PGP, S/MIME)

✅ **Digitale Signaturen** für Software

✅ **SSH** - Sichere Remote-Verbindungen

✅ **VPN** - Virtuelle private Netzwerke

✅ **Online-Banking**

✅ **Blockchain** und Kryptowährungen

### Relevanz von RSA

**Wissenschaftlich:**

- Verbindet **Zahlentheorie** mit **praktischer Anwendung**
- Motiviert Forschung in **Algorithmischer Zahlentheorie**
- Antrieb für **Primzahltests** und **Faktorisierungsalgorithmen**

**Gesellschaftlich:**

- Ermöglicht **sichere Kommunikation** für Milliarden Menschen
- Grundlage für **E-Commerce** und **digitale Wirtschaft**
- Schützt **Privatsphäre** und **vertrauliche Daten**
- Ermöglicht **digitale Identitäten** und **Authentifizierung**

**Kritisch:**

- Dual Use: Schutz für Aktivisten vs. Schutz für Kriminelle
- Macht staatliche Überwachung schwieriger
- Frage: Sollten Hintertüren (backdoors) für Behörden existieren?

---

## 📌 Zusammenfassung

### Geschichte der Verschlüsselung

| Verfahren | Typ | Sicherheit | Beispiel |
|-----------|-----|------------|----------|
| **Caesar-Chiffre** | Monoalphabetisch | ❌ Sehr schwach (26 Schlüssel) | Verschiebung um k |
| **Leibniz mit Schlüsselwort** | Monoalphabetisch | ❌ Schwach (Häufigkeitsanalyse) | BOXKAMPFJURY |
| **Enigma** | Polyalphabetisch | ⚠️ Mittel (mit Schwächen) | Walzen + Stecker |
| **One-Time-Pad** | Polyalphabetisch | ✅ Perfekt sicher | Zufälliger Schlüssel, einmalig |
| **RSA** | Asymmetrisch | ✅ Praktisch sicher (2048+ bit) | Public/Private Key |

### Symmetrisch vs. Asymmetrisch

| Aspekt | Symmetrisch | Asymmetrisch (RSA) |
|--------|-------------|-------------------|
| **Schlüssel** | 1 gemeinsamer | 2 verschiedene (Paar) |
| **Anzahl Schlüssel** (n Personen) | $\frac{n(n-1)}{2}$ | $n$ Paare |
| **Geschwindigkeit** | ✅ Schnell | ❌ Langsam |
| **Schlüsselaustausch** | ❌ Problematisch | ✅ Kein Problem |
| **Beispiele** | AES, DES | RSA, ECC |
| **Verwendung** | Daten verschlüsseln | Schlüssel austauschen, Signieren |

### RSA - Mathematische Grundlagen

**Schlüsselerzeugung:**

```
1. Wähle Primzahlen: p, q
2. Berechne: n = p × q
3. Berechne: φ(n) = (p-1) × (q-1)
4. Wähle e: ggT(e, φ(n)) = 1
5. Berechne d: d × e ≡ 1 (mod φ(n))

→ Public Key: (n, e)
→ Private Key: (n, d)
```

**Ver- und Entschlüsselung:**

$\boxed{\begin{aligned}
\text{Verschlüsseln:} & \quad C = N^e \mod n\\
\text{Entschlüsseln:} & \quad N = C^d \mod n\\
\text{Signieren:} & \quad S = N^d \mod n\\
\text{Verifizieren:} & \quad N = S^e \mod n
\end{aligned}}$

### Erweiterter Euklidischer Algorithmus

**Zweck:** Berechnung der modularen Inversen

**Algorithmus:**

```
1. Standardalgorithmus vorwärts:
   ggT(a, m) berechnen
   
2. Rückwärts:
   1 = k₁ × a + k₂ × m darstellen
   
3. Umformen:
   k₁ × a ≡ 1 (mod m)
   
4. Positiven Wert finden:
   b = k₁ mod m
```

**Beispiel:**

```
ggT(5, 48) = 1
→ -19 × 5 + 2 × 48 = 1
→ -19 × 5 ≡ 1 (mod 48)
→ 29 × 5 ≡ 1 (mod 48)
→ Inverse von 5 mod 48 ist 29
```

### Sicherheit von RSA

**Beruht auf:**

- **Primfaktorzerlegung** ist praktisch unmöglich für große Zahlen
- Bisher **kein effizienter Algorithmus** bekannt
- **NICHT bewiesen**, dass es keinen gibt!

**Empfehlungen (2025):**

- Minimum: **2048 Bit** (ca. 617 Dezimalstellen)
- Empfohlen: **3072 Bit** oder **4096 Bit**
- Vorbereitung auf Post-Quantum: Alternative Verfahren

**Bedrohungen:**

⚠️ **Quantencomputer:** Shor's Algorithmus kann RSA knacken

⚠️ **Seitenkanalangriffe:** Timing, Stromverbrauch, elektromagnetische Strahlung

⚠️ **Implementierungsfehler:** Schwache Zufallszahlen, Padding-Fehler

### Wissenschaftliche Relevanz

**Kriterien nach Balzert:**

| Kriterium | RSA-Beispiel |
|-----------|--------------|
| **Neues Wissen** | Erste praktische asymmetrische Verschlüsselung |
| **Wissenschaftlicher Fortschritt** | Verbindung Zahlentheorie ↔ Praxis |
| **Hoher Informationswert** | Mathematisch fundiert, überprüfbar |
| **Praxisrelevanz** | Grundlage für sichere digitale Kommunikation |
| **Überprüfbarkeit** | Algorithmus öffentlich, mathematisch beweisbar |

### Situated Knowledge - Kontextuelle Einbettung

**Turing und Enigma:**

- Wissenschaft findet im **historischen Kontext** statt
- Turings Arbeit: Kriegskontext, aber auch gesellschaftliche Verfolgung
- **Objektivität** ist nicht "kontextfrei", sondern situiert

**RSA heute:**

- Entwickelt 1977 (Kalter Krieg)
- Heute: Spannungsfeld zwischen Sicherheit und Überwachung
- Dual Use: Schutz für Dissidenten vs. Schutz für Terroristen

**Ethische Fragen:**

- Wer sollte Zugang zu sicherer Verschlüsselung haben?
- Sollten Regierungen "Hintertüren" verlangen können?
- Wie balanciert man Privatsphäre und Sicherheit?

---

## 🔗 Verbindungen zu anderen Vorlesungen

### Mathematische Grundlagen

- [[VL.04 Turing Machine, Algorithmen, Objektivität]]: Euklidischer Algorithmus
- **Zahlentheorie:** Primzahlen, Modulare Arithmetik
- **Algebra:** Gruppentheorie, Eulersche φ-Funktion
- **Komplexitätstheorie:** P vs. NP, Einwegfunktionen

### Informatik-Konzepte

- [[VL.02 History Computing]]: Enigma, Turing
- [[VL.04 Turing Machine, Algorithmen, Objektivität]]: Primzahltests, Sieb des Eratosthenes
- **Kryptographie:** Symmetrische Verfahren (AES), Hash-Funktionen
- **Netzwerksicherheit:** TLS/SSL, HTTPS
- **Blockchain:** Digitale Signaturen, Public-Key-Infrastruktur

### Wissenschaftstheorie

- [[VL.03 Can Machines Think?]]: RSA als origineller Durchbruch
- [[VL.04 Turing Machine, Algorithmen, Objektivität]]: Objektivität, Situated Knowledge
- **Ethik:** Dual Use, Technikfolgenabschätzung
- **Relevanz:** Wissenschaftlicher vs. gesellschaftlicher Nutzen

---

## 🎓 Wichtige Konzepte für die Prüfung

### Definitionen

**Kryptographie:** Wissenschaft der Verschlüsselung von Informationen

**Monoalphabetisch:** Verwendet 1 Zuordnung Klar- → Chiffretext

**Polyalphabetisch:** Verwendet mehrere Alphabete

**Symmetrisch:** Sender und Empfänger nutzen denselben Schlüssel

**Asymmetrisch:** Verschiedene Schlüssel zum Ver- und Entschlüsseln

**Einwegfunktion:** In einer Richtung einfach, Umkehrung schwer

**Modulare Inverse:** $b \cdot a \equiv 1 \pmod{m}$

### Algorithmen können Sie

✅ **Caesar-Chiffre:** Ver- und entschlüsseln mit Schlüssel k

✅ **Euklidischer Algorithmus:** ggT zweier Zahlen berechnen

✅ **Erweiterter Euklidischer Algorithmus:** Modulare Inverse berechnen

✅ **RSA-Schlüsselerzeugung:** Aus p, q → (e,n), (d,n)

✅ **RSA Ver-/Entschlüsselung:** Mit kleinen Zahlen durchführen

### Konzepte verstehen Sie

✅ Warum ist **Häufigkeitsanalyse** bei monoalphabetischen Verfahren möglich?

✅ Warum braucht man bei **symmetrischer** Verschlüsselung so viele Schlüssel?

✅ Was ist der Vorteil **asymmetrischer** Verschlüsselung?

✅ Warum ist **Primfaktorzerlegung** schwer?

✅ Warum funktioniert RSA mathematisch? (Kleiner Satz von Fermat)

✅ Was bedroht RSA-Sicherheit? (Quantencomputer)

✅ Was bedeutet **Situated Knowledge**?

✅ Was macht Forschung **relevant**?

---

## 💡 Vertiefende Fragen

### Mathematik

1. Warum muss $e$ teilerfremd zu $\varphi(n)$ sein?
2. Wie groß sollte $n$ mindestens sein für praktische Sicherheit?
3. Was ist die Verbindung zum Kleinen Satz von Fermat?

### Informatik

1. Warum kombiniert man in der Praxis RSA mit symmetrischer Verschlüsselung?
2. Was sind Seitenkanalangriffe?
3. Wie funktionieren digitale Zertifikate?

### Wissenschaftstheorie

1. Inwiefern ist Turings Arbeit ein Beispiel für "Situated Knowledge"?
2. Was macht RSA wissenschaftlich relevant?
3. Welche ethischen Dilemmata entstehen durch Verschlüsselung?

### Gesellschaft

1. Sollte es Hintertüren in Verschlüsselung geben?
2. Wer profitiert von starker Verschlüsselung?
3. Was ist das "Dual Use"-Problem bei Kryptographie?