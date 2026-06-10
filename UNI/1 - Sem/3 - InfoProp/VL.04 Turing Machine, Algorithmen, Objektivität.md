**Class:** [[InfoProp]]  
**Date:** 24-12-2026
**Topics:** #Algorithmen #Objektivität #TuringMaschine #Berechenbarkeit #CognitiveBias #EuklidischerAlgorithmus

---

## 🎯 Lernziele der Vorlesung

Algorithmen verstehen als fundamentales Konzept der Informatik und ihre Verbindung zu Objektivität.

- **Algorithmen** - Definition und historische Entwicklung
- **Repräsentation von Algorithmen** - verschiedene Darstellungsformen
- **Turing-Maschinen** - theoretisches Modell der Berechenbarkeit
- **Objektivität** als wissenschaftliches Kriterium
- **Cognitive Biases** - Hindernisse für Objektivität

---

## 1. Geschichte der Informatik - Zwei Säulen

### Enge Verbindung zweier Entwicklungen

```
┌─────────────────────────────────┐  ┌─────────────────────────────────┐
│        AUTOMATIK                │  │       INFORMATION               │
│                                 │  │                                 │
│  automatos (altgriech.)         │  │  informare (lat.)               │
│  selbst (autos) + denken (men)  │  │  durch Unterweisung bilden      │
└─────────────────────────────────┘  └─────────────────────────────────┘
            ↓                                      ↓
┌─────────────────────────────────┐  ┌─────────────────────────────────┐
│  Rechengeräte                   │  │  Erkenntnisse                   │
│  Praktische Fragen              │  │  Theoretische, philosophische   │
│  Arbeitserleichterung           │  │  Fragen                         │
└─────────────────────────────────┘  └─────────────────────────────────┘
            ↓                                      ↓
┌─────────────────────────────────┐  ┌─────────────────────────────────┐
│  Ingenieurdisziplin             │  │  Mathematik                     │
│  Rechnen mechanisieren          │  │  Denken formalisieren           │
└─────────────────────────────────┘  └─────────────────────────────────┘
            ↓                                      ↓
┌─────────────────────────────────┐  ┌─────────────────────────────────┐
│  Entwicklung des Computers      │  │  Entwicklung von Algorithmen    │
│  (HARDWARE)                     │  │  (SOFTWARE)                     │
└─────────────────────────────────┘  └─────────────────────────────────┘
```

---

## 2. Was ist ein Algorithmus?

### Definition

$$\boxed{\text{Algorithmus} = \text{Klar definierte Folge von Schritten}}$$

**Ein Algorithmus:**
- Beschreibt **eindeutig**, wie alle Probleme eines bestimmten Typs gelöst werden können
- Kann von jedem ausgeführt werden (unabhängig vom Ausführenden)
- Liefert bei gleicher Eingabe immer dasselbe Ergebnis

### Bedeutung von Algorithmen

> *"The intelligence required to solve the problem at hand is encoded in the algorithm."*

**Kernaussagen:**

1. Die **Intelligenz**, die zur Lösung des Problems erforderlich ist, **steckt im Algorithmus**

2. Das **Intelligenzniveau von Maschinen** hängt davon ab, wie viel Intelligenz durch Algorithmen abgebildet werden kann

3. Maschinen können **nur solche Aufgaben ausführen**, für die es einen Algorithmus gibt

4. Wenn für eine Problemlösung **kein Algorithmus existiert**, liegt die Lösung des Problems **außerhalb der Fähigkeit von Maschinen**

### Historische Bedeutung

> *"Once an algorithm for performing a task has been found, the performance of that task no longer requires an understanding of the principles on which the algorithm is based."*

**Konsequenz:**
- Wir können dem Euklidischen Algorithmus folgen, um einen größten gemeinsamen Teiler zu finden, **ohne zu verstehen, warum der Algorithmus funktioniert**
- Die Ausführung der Aufgabe wird reduziert auf das **bloße Befolgen von Anweisungen**

---

## 3. Historische Algorithmen

### Euklidischer Algorithmus (300 v. Chr.)

**Problem:** Finde den **größten gemeinsamen Teiler (ggT)** zweier Zahlen

**Eigenschaften:**
- **Ältester Algorithmus**, der den Namen verdient
- Wird **noch heute benutzt**, weil es keinen besseren gibt
- Entdeckt von Euklid, griechischer Mathematiker

#### Geometrische Darstellung

**Beispiel:** $\text{ggT}(75, 27)$

```
┌───────────────────────────────────────────────────────────────────────┐
│  75                                                                   │
│  ┌──────────────────────────────┐  ┌──────────────────────────────┐  │
│  │        27                    │  │        27                    │  │
│  │  ┌──────────────────────┐    │  │  ┌──────────────────────┐    │  │
│  │  │                      │    │  │  │                      │    │  │
│  │  └──────────────────────┘    │  │  └──────────────────────┘    │  │
│  └──────────────────────────────┘  └──────────────────────────────┘  │
│                 Rest: 21                                              │
└───────────────────────────────────────────────────────────────────────┘

Schritt 1: 75 = 2 × 27 + 21
Schritt 2: 27 = 1 × 21 + 6
Schritt 3: 21 = 3 × 6 + 3
Schritt 4: 6 = 2 × 3 + 0  ← Rest = 0, fertig!

ggT(75, 27) = 3
```

#### Algorithmus in Worten

1. Stelle die **größere Zahl** als **Vielfaches der kleineren Zahl** plus **Rest** dar
2. Wenn der Rest **null** ist, dann ist die **kleinere Zahl** der ggT
3. Sonst: Ersetze die größere Zahl durch die kleinere, und die kleinere durch den Rest
4. Wiederhole ab Schritt 1

#### Übung: ggT(8, 5)

```
8 = 1 × 5 + 3
5 = 1 × 3 + 2
3 = 1 × 2 + 1
2 = 2 × 1 + 0

ggT(8, 5) = 1
```

### Das Sieb des Eratosthenes (276-194 v.Chr.)

**Problem:** Finde alle **Primzahlen** in einer Liste von Zahlen der Länge $n$

**Definition Primzahl:**
Eine ganze Zahl $x \in \mathbb{N}$, $x > 1$, die ausschließlich durch sich selbst und durch $1$ teilbar ist.

#### Algorithmus

```
Schritt 1: Liste aller Zahlen von 2 bis n

2  3  4  5  6  7  8  9  10 11 12 13 14 15 16 17 18 19 20
```

```
Schritt 2: Beginne mit 2 (erste Primzahl)
          Streiche alle Vielfachen von 2 (außer 2 selbst)

2  3  ✗  5  ✗  7  ✗  9  ✗  11 ✗  13 ✗  15 ✗  17 ✗  19 ✗
```

```
Schritt 3: Nächste nicht gestrichene Zahl ist 3
          Streiche alle Vielfachen von 3 (außer 3 selbst)

2  3  ✗  5  ✗  7  ✗  ✗  ✗  11 ✗  13 ✗  ✗  ✗  17 ✗  19 ✗
```

```
Schritt 4: Wiederhole bis zur größten Siebzahl √n

Primzahlen bis 20: 2, 3, 5, 7, 11, 13, 17, 19
```

**Wichtig:** Größte Siebzahl einer Liste mit $n$ Zahlen ist $\sqrt{n}$

---

## 4. Herkunft des Begriffs "Algorithmus"

### Abu Dscha'far Muhammad ibn Musa al-Chwarizmi (∼780-850)

**Etymologie:**

- **"Dixit Algorizmi"** = "also sprach al-Chwarizmi"
- Als **Gütezeichen einer Rechnung** (ab ca. 1200)
- Autor von **"Hisab al-ğabr wa-'l-muqabala"** (Algebra)

### Moderne Definition

$$\boxed{\begin{aligned}
\text{Algorithmus} &= \text{Eindeutige Handlungsanweisung zur Lösung eines Problems}\\
&\text{Eingabe} \rightarrow \text{Ausgabe}\\
&\text{Intelligenz steckt in der Anweisung}\\
&\text{Ausführender muss nicht verstehen, was er tut}
\end{aligned}}$$

---

## 5. Repräsentation von Algorithmen

### Verschiedene Darstellungsformen

**Beispiel: Euklidischer Algorithmus**

#### 1. Natürliche Sprache

```
1. Stelle die größere Zahl als Vielfaches der kleineren Zahl plus Rest dar
2. Wenn der Rest null ist → kleinere Zahl ist der ggT
3. Sonst wiederhole mit kleinerer Zahl und Rest
```

#### 2. Mathematisch-Geometrisch

Visuelle Darstellung durch Rechtecke (siehe oben)

#### 3. Pseudocode

```python
ggt_mod(a, b):
    while a % b != 0:           # solange der Rest nicht null ist
        if b > a:
            a, b = b, a          # tausche a und b
        a = a % b                # größere Zahl als Vielfaches der kleineren
    return b                     # kleinere Zahl ist ggT
```

#### 4. Ablaufdiagramme (Flowcharts)

```
         ┌─────────┐
         │  Start  │
         └────┬────┘
              │
         ┌────▼────┐
         │ Eingabe │
         │  a, b   │
         └────┬────┘
              │
         ┌────▼────┐
      ┌─►│ a % b?  │
      │  └────┬────┘
      │       │
      │  ┌────▼────┐
      │  │ = 0?    │──Ja──► b ist ggT
      │  └────┬────┘
      │       │Nein
      │  ┌────▼────┐
      │  │ a = a%b │
      │  └────┬────┘
      │       │
      └───────┘
```

#### 5. Programmcode

Konkrete Implementierung in einer Programmiersprache (Python, Java, C++, etc.)

---

## 6. Formalisieren des Denkens

### Zeichensysteme

**Gottfried Wilhelm Leibniz (1646-1716):**

> *Träumte von einer Maschine, die Symbole manipulieren kann, um den Wahrheitswert mathematischer Aussagen zu bestimmen.*

**Voraussetzung:** Klare, formale Sprache

#### Das Binärsystem

**3. Jahrhundert v.Chr.:** Indischer Mathematiker **Pingala** beschreibt Zahlensystem bestehend aus **2 Zeichen**

**Ende 17. Jahrhundert:** Leibniz entwirft das **binäre Zahlensystem**

**Bedeutung für Computer:**
- Zahlen werden durch **elektrische Zustände** dargestellt (Strom an/aus)
- Kritisch bei der Entwicklung elektronischer Rechenmaschinen

### Boolesche Logik

**George Boole (1815-1864), 1847:**

Entwickelt das nach ihm benannte **Logikkalkül**

**Grundlage für die Zweiwertige Boolesche Algebra:**

| Operation | Symbol | Bedeutung |
|-----------|--------|-----------|
| **UND** | $\land$ | Konjunktion |
| **ODER** | $\lor$ | Disjunktion |
| **NICHT** | $\neg$ | Negation |

**Verallgemeinert:**
- Logische Operatoren
- Mengentheoretische Verknüpfungen (Durchschnitt, Vereinigung, Komplement)

**Venn-Diagramme** visualisieren diese Operationen

→ Siehe Modul **FORSA** (Formale Sprachen und Automaten)

---

## 7. Programmierbare Maschinen

### Ada Lovelace (1815-1852)

**1842:**

> *"Die Grenzen der Arithmetik wurden in dem Augenblick überschritten, in dem die Idee zur Verwendung der [Programmier]Karten entstand ... die Analytical Engine hat keine Gemeinsamkeit mit schlichten Rechenmaschinen."*

### Lady Lovelace's Objection

> *"Die Analytical Engine hat keine Ambitionen etwas (Neues) hervorzubringen. Sie kann [nur] das tun, was wir ihr befehlen; sie hat jedoch keine Fähigkeit zur Erkenntnis analytischer Verhältnisse oder Wahrheiten."*

**Dieser Einwand wird von Turing (1950) diskutiert** - siehe [[VL.03 Can Machines Think?]]

---

## 8. Das Entscheidungsproblem (Entscheidbarkeit)

### Das Problem (Hilbert & Ackermann, 1928)

**Frage:**

$$\boxed{\text{Kann es einen Algorithmus geben, der für eine Aussage entscheidet, ob sie universell wahr oder falsch ist?}}$$

### Die Antwort: NEIN

**Church (1935) und Turing (1936):**

Haben **bewiesen**, dass es so einen Algorithmus **nicht geben kann**.

**Bedeutung:**
- Nicht alle Probleme sind algorithmisch lösbar
- Es gibt Grenzen der Berechenbarkeit
- Dies ist eine fundamentale Erkenntnis der theoretischen Informatik

---

## 9. Konzept der Berechenbarkeit - Turing-Maschinen

### Alan Turing (1912-1954)

**Zentrale Fragen:**

1. Wenn man schon nicht alles beweisen kann, **was kann man dann berechnen**? (Und was nicht?)
2. Was heißt das überhaupt, **Dinge zu berechnen**?

**Ansatz:** Versucht zu formalisieren, wie ein **Mensch rechnet**

**Wichtig:** Die Turing-Maschine war **nicht** als Modell für Computer gedacht, sondern als **theoretisches Modell** zur Formalisierung der Berechenbarkeit!

### Was brauchen Menschen, um etwas zu berechnen?

✅ Liste von **Anweisungen** (Algorithmus/Programm)

✅ **Lesen**, **Schreiben** (radieren/überschreiben)

✅ **Schmierpapier** für Zwischenergebnisse

✅ **Gedächtnis**

✅ **"Eingabe"** & **"Ausgabe"**

✅ **Speichermedium**

---

## 10. Turing's Formalisierung - Die Turing-Maschine

### Komponenten einer Turing-Maschine

#### 1. Alphabet

Endliche Menge von Zeichen: $\Sigma = \{0, 1\}$

#### 2. Speicherband ("Tickertape")

```
┌───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┬───┐
│ * │   │ 1 │ 0 │ 1 │ 0 │   │   │   │   │   │   │ ...
└───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┴───┘
  ↑
  Anfang
```

- In **Felder unterteilt**
- **1 Zeichen pro Feld**
- **Beliebig lang** (theoretisch unendlich)

#### 3. Leerzeichen

Symbol: $\square$ oder "B" (blank)

$\square \notin \Sigma$

#### 4. Sonderzeichen für Anfang

Symbol: `*` 

`*` $\notin \Sigma$

#### 5. Schreib-/Lesekopf

```
┌───┬───┬───┬───┬───┬───┐
│ * │   │ 1 │ 0 │ 1 │   │
└───┴───┴─▲─┴───┴───┴───┘
          │
      Kopf hier
```

**Fähigkeiten:**
- Kann jeweils **ein Feld lesen**
- Kann jeweils **ein Feld überschreiben**
- Darf `*` **nicht überschreiben**
- Darf **nicht weiter nach links** als `*` gehen

#### 6. "Programm" (Berechnungsvorschrift)

Steuert den Kopf

---

## 11. Das Turing-Maschinen-Programm

### Struktur einer Instruktion

| read | write | move | go to |
|------|-------|------|-------|
| 1 | 1 | R | 0 |

**Bedeutung der Spalten:**

1. **read:** Lies aktuelles Feld
2. **write:** Schreibe etwas auf das Feld
3. **move:** Gehe 1 Schritt nach links (L), rechts (R) oder halte an (H)
4. **go to:** Wähle den nächsten Programmschritt aus

**(2, 3 und 4 hängen von 1 ab)**

### Beispiel-Programm

| read | write | move | go to | = **Zustand** |
| ---- | ----- | ---- | ----- | ------------- |
| 1    | 1     | R    | 0     | Zustand 0     |
| 0    | 1     | R    | 2     | Zustand 0     |
| *    | *     | R    | 0     | Zustand 0     |
| B    | 0     | L    | -1    | Zustand 0     |

**Zustand -1:** HALT (Programm endet)

---

## 12. Beispiel: Subtraktion von 1 (Binärzahl)

### Problem

Subtrahiere 1 von einer Binärzahl

**Beispiele:**

```
10 - 1 = 9        1010
                  -  1
                  ----
                  1001

17 - 1 = 16      10001
                  -   1
                  -----
                 10000
```

**Spezialfall:** Wenn Input 0, dann Ergebnis 0

### Turing-Maschinen-Programm

| Zustand | read | write | move | go to |
|---------|------|-------|------|-------|
| 0 | 1 | 0 | L | -1 |
| 0 | 0 | 1 | L | 0 |
| 0 | * | * | R | 1 |
| 0 | B | B | R | 0 |
| 1 | ... | ... | ... | ... |

**Logik:**
- Gehe nach links bis zur letzten 1
- Ändere diese 1 zu 0
- Alle 0en davor werden zu 1en

---

## 13. Übung: Addition von 1 (Binärzahl)

### Problem

Addiere 1 zu einer Binärzahl

**Beispiele:**

```
4 + 1 = 5        100
                 + 1
                 ---
                 101

5 + 1 = 6        101
                 + 1
                 ---
                 110

7 + 1 = 8        111
                 + 1
                 ----
                1000
```

**Aufgabe:**
1. Überlegen Sie sich eine Turing-Maschine für diese Operation
2. Testen Sie Ihre Maschine mit den Beispielen
3. Achten Sie besonders auf den Fall 111 + 1 = 1000 (Übertrag!)

---

## 14. Die Turing-Maschine - Zusammenfassung

### Was ist eine Turing-Maschine?

$$\boxed{\text{Turing-Maschine} = \text{Theoretisches Modell einer Rechenmaschine}}$$

**Eigenschaften:**

✅ **Theoretisches Modell** - nicht für praktische Implementierung gedacht

✅ **Formalisiert den Begriff der Berechenbarkeit**

✅ **Berechnung** = schrittweise Manipulation von Zeichen/Symbolen

✅ Zeichen können u.a. als **Zahlen** interpretiert werden

### Bedeutung

> *"The Turing machine is a mathematical model of computation that defines an abstract machine which manipulates symbols on a strip of tape according to a table of rules."*

**Fundamentale Erkenntnis:**

Alles, was algorithmisch berechenbar ist, kann von einer Turing-Maschine berechnet werden (**Church-Turing-These**)

---

## 15. Grace Hopper und die 1940er/50er Jahre

### Grace Hopper (1906-1992)

**1952:** "The education of a computer"

> *"I was lazy and hoped that the programmer may return to being a mathematician."*

**Bedeutung:**
- Pionierarbeit in der Programmierung
- Entwicklung höherer Programmiersprachen
- Idee: Programmierung sollte einfacher und mathematischer werden

---

## 16. Algorithmen und Objektivität

### Verbindung zu Objektivität

**Warum gelten Algorithmen als objektiv?**

```
┌─────────────────────────────────────────────┐
│  Bei gleicher Eingabe (Frage)               │
│          ↓                                  │
│  Immer dasselbe Ergebnis                    │
└─────────────────────────────────────────────┘
         ↓
┌─────────────────────────────────────────────┐
│  Jede/r kann sie ausführen                  │
└─────────────────────────────────────────────┘
         ↓
┌─────────────────────────────────────────────┐
│  Unabhängig von Nutzerin                    │
└─────────────────────────────────────────────┘
         ↓
┌─────────────────────────────────────────────┐
│  → OBJEKTIVITÄT                             │
└─────────────────────────────────────────────┘
```

**Aber:** Diese Objektivität ist trügerisch - siehe unten!

---

## 17. Wissenschaftskriterium: Objektivität

### Definition nach Balzert et al. (2022)

$$\boxed{\text{Objektivität} = \text{Ergebnisse sind unabhängig vom Beobachter}}$$

**Bedeutet:**

✅ Frei von **persönlichen Urteilen** und **Einstellungen**

✅ **Nicht frei** von fachlichem Vorwissen

✅ Sachlich und **vorurteilsfrei**

✅ **Neutrale Haltung**

### Zwei Dimensionen der Objektivität

**1. Unabhängigkeit vom Ersteller:**

Ein hohes Maß an Objektivität liegt vor, wenn Erkenntnisse und Ergebnisse auch **unabhängig von Ihrer Person** zustande kommen.

→ Andere Menschen an anderen Orten können auf dem gleichen Wege zu den **gleichen Resultaten** kommen

**2. Unabhängigkeit vom Auswerter/Gutachter:**

Ein hohes Maß an Objektivität liegt vor, wenn die Beurteilung der Qualität **unabhängig** von der Person des Auswerters/Gutachters ist.

→ Mehrere Gutachter kommen zu der **gleichen Beurteilung**

---

## 18. Was steht Objektivität im Wege?

### Hindernisse für Objektivität

**Persönliche Faktoren:**

❌ **Vorlieben** und **Vorurteile**

❌ **Ressentiments**

❌ Übergroßer **Ehrgeiz**

❌ **Hoffnungen** und **Wünsche**

❌ Eingeschränkter **Blickwinkel**

### Warnsignale

⚠️ Sie wollen andere Menschen **unbedingt von Ihren guten Vorstellungen überzeugen**

⚠️ Sie glauben **schon vor der Erstellung**, das Endergebnis **detailgenau zu kennen**

> *"Hat der menschliche Verstand einmal eine Meinung angenommen (sei es, dass es die herrschende ist, sei es, dass sie ihm sonstwie angenehm ist), dann interpretiert er alle anderen Dinge so, dass sie diese Meinung stützen und mit ihr übereinstimmen"* (Bacon)

---

## 19. Mögliche Fehlerquellen

### Bei der Durchführung

❌ Der Autor bringt sich immer wieder selbst ins Spiel

❌ **Emotionale Formulierungen** und unklare, vorurteilsbeladene Darstellung

❌ Eine bestimmte **Denkrichtung** ist nötig, damit man die Inhalte nachvollziehen kann

❌ **Auslassen**, was nicht ins Konzept passt

❌ **Unerwünschte Beobachtungen** oder Expertisen ignorieren

❌ **Unvollständige Darstellung** unliebsamer Beobachtungen

### Bei der Dokumentation

❌ **Unvollständiges Zitieren**

❌ **Unrichtige Wiedergaben**

❌ Nur Freunde dürfen mitmachen

### Bei der Auswertung

❌ **Manipulierte Ergebnisse**

❌ Ungenau messende Instrumente

❌ **Unbegründete**, den eigenen Wünschen entsprechende Schlussfolgerungen

❌ In eine gewünschte Zielrichtung **interpretieren**

❌ Persönliche und **vorschnelle Wertungen** ohne Belege

---

## 20. Das Affenexperiment - Confirmation Bias

### Das Experiment (Marc Hauser, Harvard)

**Forschungsfrage:**

Besitzen Rhesusaffen einen **Sprachsinn**?

**Experiment:**

1. Affen wird eine **regelmäßige Abfolge von Tönen** vorgespielt
2. Dann wird die **Tonfolge geändert**
3. **Beobachtung:** Richten die Affen ihre Augen auf den Lautsprecher?

**Wenn ja:** Hinweis darauf, dass Affen eine wesentliche Voraussetzung zur Entwicklung von Sprache besitzen

### Das Problem

**Schwierigkeit:**

Auswertung ist **kritisch**, da es schwierig ist, die **Richtung und Dauer eines Affenblicks** richtig einzuschätzen

**Was geschah:**

- **Hauser** kam zu dem Ergebnis: Affen schauen bei veränderten Tonfolgen auf den Lautsprecher (wie angenommen!)
- **Laborassistent** konnte auf den Videobändern **nichts Auffälliges** erkennen
- Hauser **missbrauchte seine Autorität**, um den Auswerter in seiner Analyse zu **beeinflussen**

### Cognitive Bias: Confirmation Bias

$$\boxed{\text{Confirmation Bias} = \text{Bestätigungsfehler}}$$

**Definition:**

Die Tendenz, Informationen so zu **suchen**, zu **interpretieren** und sich an sie zu **erinnern**, dass sie die eigenen Vorannahmen **bestätigen**

**Auch genannt:**
- **Selektive Wahrnehmung**
- **Wunschdenken**

### Standards zur Sicherung der Objektivität

✅ Videobänder sollen von **mindestens zwei Personen** unabhängig ausgewertet werden

✅ Sie dürfen das **Ziel des Experiments nicht kennen**, um Befangenheit auszuschließen

✅ Wenn sich die Ergebnisse beider Auswerter um **mehr als 20 Prozent** unterscheiden, ist das Experiment zu **verwerfen**

---

## 21. Wie kann man Objektivität sichern?

### Maßnahmen für objektiveres Arbeiten

**Bei der Darstellung:**

✅ Inhalte **neutral** und **vorurteilsfrei** darstellen

✅ Problemsituation **sachlich** und **klar** beschreiben

✅ Formulieren Sie **unabhängig von Ihrer Person** und auf Grundlage von **Belegen** und **logischen Schlussfolgerungen**

**Beispiele:**

| ❌ Nicht objektiv | ✅ Objektiv |
|-------------------|------------|
| "Ich habe mit viel Mühe festgestellt, ..." | "Wie das Beispiel zeigt, ..." |
| "Ich meine aber schon lange, ..." | "Hier kann man beobachten, dass ..." |
| | "Daraus ergibt sich, ..." |

**Bei der Quellenauswahl:**

✅ Möglichst **unvoreingenommen** die Quellen auswählen

✅ **Einwände berücksichtigen**

✅ Auch **gegenteilige Meinungen** einbeziehen

✅ **Richtig** und **vollständig** zitieren

**Bei der Durchführung:**

✅ Für **unabhängige Interviewer** oder Beobachter sorgen

✅ **Repräsentative Auswahl** an Testpersonen oder Untersuchungsobjekten treffen

✅ **Ausreichend große Stichprobe** vornehmen

✅ **Geeignete Methoden** und Instrumente einsetzen

**Bei der Auswertung:**

✅ **Korrekte Datenauswertungen**

✅ Begründete **Interpretationen** und **Schlussfolgerungen**

✅ **Ehrliche Ergebnisbeschreibung**

### Ist Objektivität überhaupt möglich?

**Kritischer Einwand:**

Kann man als Ersteller einer wissenschaftlichen Arbeit tatsächlich **neutral** und **wertfrei** denken und argumentieren?

Schließlich arbeitet man mit **Leidenschaft** und hegt **Wünsche** und **Ziele** im eigenen Fachgebiet.

**Realistische Antwort:**

Man kann sich um einen **möglichst hohen Grad an Objektivität** bemühen und auf diese Weise seiner wissenschaftlichen Arbeit **Qualität** und **Glaubwürdigkeit** verleihen.

---

## 22. Algorithmen und das Problem der Objektivität

### Die trügerische Objektivität von Algorithmen

**Versprechen:**

```
Algorithmus
    ↓
Eindeutige Schritte
    ↓
Gleiche Eingabe → Gleiche Ausgabe
    ↓
Unabhängig vom Ausführenden
    ↓
OBJEKTIV?
```

**Aber:** Algorithmen werden von **Menschen entwickelt**!

### Wo kann Subjektivität eindringen?

**1. Bei der Problemdefinition:**

- Welches Problem wird überhaupt als lösungswürdig angesehen?
- Wer definiert, was das "richtige" Ergebnis ist?

**2. Bei der Datenselektion:**

- Welche Daten werden gesammelt?
- Welche Daten werden als relevant betrachtet?
- Welche Daten werden ignoriert?

**3. Bei der Algorithmenentwicklung:**

- Welche Merkmale werden berücksichtigt?
- Welche Gewichtungen werden vorgenommen?
- Welche Annahmen werden gemacht?

**4. Bei der Interpretation:**

- Wie werden die Ergebnisse interpretiert?
- Welche Schlussfolgerungen werden gezogen?

### Beispiel: Gesichtserkennung

Ein Algorithmus zur Gesichtserkennung:

❌ Trainiert hauptsächlich mit Bildern weißer männlicher Gesichter

→ **Ergebnis:** Funktioniert schlechter bei Frauen und People of Color

**Problem:** Der **Bias** der Entwickler und der Trainingsdaten wird im Algorithmus **reproduziert**

---

## 23. Cognitive Biases - Systematische Denkfehler

### Was sind Cognitive Biases?

$\boxed{\text{Cognitive Bias} = \text{Systematische Abweichung vom rationalen Denken}}$

**Definition:**

Menschliche **Wahrnehmungs- und Urteilstendenzen**, die die **Unvoreingenommenheit** beeinträchtigen können

### Wichtige Cognitive Biases

**1. Confirmation Bias (Bestätigungsfehler):**

Tendenz, Informationen zu suchen und zu interpretieren, die die eigenen Vorannahmen bestätigen

**2. Availability Bias (Verfügbarkeitsheuristik):**

Überschätzung der Wahrscheinlichkeit von Ereignissen, die leicht aus dem Gedächtnis abgerufen werden können

**3. Anchoring Bias (Ankereffekt):**

Zu starke Orientierung an der ersten Information, die man erhält

**4. Selection Bias (Auswahlverzerrung):**

Systematische Fehler bei der Auswahl von Daten oder Teilnehmern

**5. Observer Bias (Beobachterverzerrung):**

Erwartungen des Beobachters beeinflussen, was er wahrnimmt

### Visualisierung: 50 Cognitive Biases

Siehe: https://www.visualcapitalist.com/50-cognitive-biases-in-the-modern-world/

**Kategorien:**

- **Too Much Information:** Wie wir mit Informationsüberflutung umgehen
- **Not Enough Meaning:** Wie wir Mustern Bedeutung zuschreiben
- **Need to Act Fast:** Wie wir unter Zeitdruck entscheiden
- **What Should We Remember:** Wie wir auswählen, was wir behalten

---

## 24. Algorithmen als Forschungsgegenstand

### Zentrale Forschungsfragen

**1. Grenzen der Berechenbarkeit:**

Welche Probleme lassen sich algorithmisch lösen?

**2. Algorithmenentwicklung:**

Wie kann man Algorithmenentwicklung vereinfachen?

**3. Repräsentation:**

Wie repräsentiert man Algorithmen?
- Natürliche Sprache
- Pseudocode
- Flowcharts
- Programmiersprachen

**4. Analyse:**

Wie kann man Algorithmen analysieren?
- Korrektheit
- Laufzeit
- Speicherbedarf
- Effizienz

**5. Künstliche Intelligenz:**

Können Algorithmen intelligentes Verhalten erzeugen?

**6. Optimierung:**

Wie steigert man ihre Effizienz?

---

## 25. Intelligente Maschinen - Wo stehen wir?

### Offene Fragen

**1. Das Messproblem:**

```
Denken zu definieren ist subjektiv
        ↓
Oder: von außen beobachtbar machen
        ↓
Messbar machen
        ↓
Wie gut ist die Messung?
```

**2. Das Definitionsproblem:**

**Intelligenz** haben wir noch nicht definiert!

**3. Das Spezialisierungsproblem:**

Klassische Maschinen und Algorithmen sind **bereichsspezifisch**

```
┌────────────────────────────────┐
│  Schach-Algorithmus            │
│  ✓ Spielt Schach perfekt       │
│  ✗ Kann nicht Auto fahren      │
└────────────────────────────────┘

┌────────────────────────────────┐
│  Gesichtserkennung             │
│  ✓ Erkennt Gesichter           │
│  ✗ Kann nicht Schach spielen   │
└────────────────────────────────┘
```

**Frage:** Wie kommen wir zu **universeller** künstlicher Intelligenz?

---

## 📌 Zusammenfassung

### Algorithmen - Kernkonzepte

| Aspekt | Beschreibung |
|--------|--------------|
| **Definition** | Klar definierte Folge von Schritten zur Lösung eines Problems |
| **Intelligenz** | Steckt im Algorithmus, nicht im Ausführenden |
| **Grenzen** | Maschinen können nur Aufgaben ausführen, für die Algorithmen existieren |
| **Berechenbarkeit** | Church & Turing: Nicht alle Probleme sind algorithmisch lösbar |

### Historische Algorithmen

**Euklidischer Algorithmus (300 v. Chr.):**
- Findet ggT zweier Zahlen
- Ältester Algorithmus
- Wird heute noch verwendet

**Sieb des Eratosthenes (276-194 v. Chr.):**
- Findet alle Primzahlen bis $n$
- Streicht Vielfache ("sieben")
- Größte Siebzahl: $\sqrt{n}$

### Repräsentationsformen

1. **Natürliche Sprache** - für Menschen lesbar
2. **Mathematisch-Geometrisch** - visuell
3. **Pseudocode** - strukturiert, aber nicht ausführbar
4. **Ablaufdiagramme** - grafische Darstellung
5. **Programmcode** - maschinenausführbar

### Turing-Maschine

**Komponenten:**

```
┌──────────────────────────────────────┐
│ Alphabet: Σ = {0, 1}                │
│ Band: unendlich, Felder              │
│ Leerzeichen: □                       │
│ Anfang: *                            │
│ Kopf: liest/schreibt                 │
│ Programm: Zustandsübergänge          │
└──────────────────────────────────────┘
```

**Bedeutung:**
- Theoretisches Modell der Berechenbarkeit
- Formalisiert, was "berechnen" bedeutet
- Alles Berechenbare kann von einer Turing-Maschine berechnet werden (Church-Turing-These)

### Objektivität

**Definition:**
- Ergebnisse unabhängig vom Beobachter
- Frei von persönlichen Urteilen
- Nicht frei von fachlichem Vorwissen

**Hindernisse:**
- Vorlieben, Vorurteile, Ressentiments
- Cognitive Biases (Confirmation Bias, Selection Bias, ...)
- Emotionale Formulierungen

**Maßnahmen:**
- Neutrale Darstellung
- Gegenteilige Meinungen einbeziehen
- Unabhängige Beobachter
- Repräsentative Stichproben
- Korrekte Datenauswertung

### Das Problem: Algorithmen und Objektivität

**Versprechen:**
```
Algorithmus = Objektiv?
  ↓
Gleiche Eingabe → Gleiche Ausgabe
```

**Realität:**
```
Algorithmus entwickelt von Menschen
  ↓
Problemdefinition (subjektiv)
Datenselektion (subjektiv)
Gewichtungen (subjektiv)
  ↓
Bias wird reproduziert
```

**Wichtige Erkenntnis:**

Algorithmen sind **nicht automatisch objektiv**, nur weil sie deterministisch sind!

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 History Computing]]: Entwicklung von Rechenmaschinen, Babbage, Hollerith
- [[VL.03 Can Machines Think?]]: Turing's Konzept der Berechenbarkeit, Lady Lovelace's Objection
- **FORSA**: Formale Sprachen und Automaten - Boolesche Algebra
- **Wissenschaftliches Arbeiten**: Objektivität, Überprüfbarkeit, Cognitive Biases
- **KI und Ethik**: Bias in Algorithmen (kommende Vorlesungen)