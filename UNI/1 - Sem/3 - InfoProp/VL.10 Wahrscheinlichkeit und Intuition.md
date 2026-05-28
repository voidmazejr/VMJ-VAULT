**Class:** [[Wissenschaftliches Arbeiten]]  
**Date:** 27-01-2026 
**Topics:** #Wahrscheinlichkeit #Kombinatorik #Mengen #LaplaceExperiment #BedingteWahrscheinlichkeit #Bayes #Geburtstagsproblem #BaseRateFallacy

---

## 🎯 Lernziele der Vorlesung

Wahrscheinlichkeitstheorie und Kombinatorik sind fundamentale Werkzeuge zur Formalisierung von Zufall und zur Berechnung von Möglichkeiten.

- **Mengen** und Mengenoperationen verstehen
- **Kombinatorik**: Permutationen und Variationen berechnen
- **Wahrscheinlichkeitsraum** formal definieren
- **Laplace-Experimente** und Wahrscheinlichkeitsberechnung
- **Geburtstagsproblem** verstehen
- **Bedingte Wahrscheinlichkeit** und **Satz von Bayes**
- **Base Rate Fallacy** erkennen

---

## 1. Mengen - Grundlagen

### Definition nach Cantor

$$\boxed{\text{Menge: Zusammenfassung von bestimmten, wohlunterschiedenen Objekten unseres Denkens zu einem Ganzen}}$$

**Georg Cantor (1845-1918):** Begründer der Mengenlehre

### Notation und Eigenschaften

**Beispiel:** $A = \{1, 2, 3, 42\}$

**Elementbeziehung:**
- $3 \in A$ → "3 ist Element von A"
- $7 \notin A$ → "7 ist nicht Element von A"

**Wichtige Eigenschaften:**

✅ **Reihenfolge spielt keine Rolle:** $\{1, 2, 3, 42\} = \{3, 42, 2, 1\}$

✅ **Wiederholungen spielen keine Rolle:** $\{1, 2, 3, 3, 42\} = \{1, 2, 3, 42\}$

✅ **Identität durch Elemente:** Eine Menge ist eindeutig durch ihre Elemente bestimmt

---

## 2. Beziehungen zwischen Mengen

### Teilmenge (Subset)

$$\boxed{X \subseteq Y \iff \text{Jedes Element von } X \text{ ist auch Element von } Y}$$

**Beispiel:** $X = \{3, 5, 10\}$, $Y = \{3, 5, 6, 10, 11\}$ → $X \subseteq Y$

**Wichtig:**
- $X \subseteq Y$ bedeutet NICHT unbedingt $|X| < |Y|$
- $A \subseteq B$ bedeutet NICHT $B \subseteq A$
- Wenn $A \subseteq B$ UND $B \subseteq A$, dann $A = B$

### Spezielle Mengen

**Leere Menge:** $\emptyset = \{\}$

$$\boxed{\text{Für jedes Objekt } a \text{ gilt: } a \notin \emptyset}$$

**Wichtige Eigenschaft:** $\emptyset \subseteq A$ für jede Menge $A$

---

## 3. Mengenoperationen

### Vereinigung (Union)

$$\boxed{A \cup B = \{x \mid x \in A \text{ ODER } x \in B\}}$$

**Beispiel:** $A = \{1, 2, 3, 4\}$, $B = \{3, 4, 5\}$
$$A \cup B = \{1, 2, 3, 4, 5\}$$

### Schnitt (Intersection)

$$\boxed{A \cap B = \{x \mid x \in A \text{ UND } x \in B\}}$$

**Beispiel:** $A = \{1, 2, 3, 4\}$, $B = \{3, 4, 5\}$
$$A \cap B = \{3, 4\}$$

**Disjunkte Mengen:** $A \cap B = \emptyset$ (keine gemeinsamen Elemente)

### Mengentheoretische Differenz

$$\boxed{A \setminus B = \{x \mid x \in A \text{ UND } x \notin B\}}$$

**Beispiel:** $A = \{1, 2, 3, 4\}$, $B = \{3, 4, 5\}$
$$A \setminus B = \{1, 2\}$$

### Komplement

$$\boxed{A^C = \Omega \setminus A}$$

wobei $\Omega$ die Grundmenge ist.

---

## 4. Mächtigkeit von Mengen

### Definition

$$\boxed{|A| = \text{Anzahl der Elemente von } A}$$

**Beispiele:**
- $|\{42, 43, 100\}| = 3$
- $|\emptyset| = 0$
- $|\{1, 2, 3, 3, 42, 43, 100\}| = 6$ (Wiederholungen zählen nicht!)

### Inklusions-Exklusions-Prinzip

**Für disjunkte Mengen:**

$$\boxed{\text{Wenn } A \cap B = \emptyset: \quad |A \cup B| = |A| + |B|}$$

**Für beliebige Mengen:**

$$\boxed{|A \cup B| = |A| + |B| - |A \cap B|}$$

**Für drei Mengen:**

$$|A \cup B \cup C| = |A| + |B| + |C| - |A \cap B| - |A \cap C| - |B \cap C| + |A \cap B \cap C|$$

---

## 5. Kombinatorik - Permutationen

### Permutationen ohne Wiederholungen

$$\boxed{n! = n \cdot (n-1) \cdot (n-2) \cdot \ldots \cdot 2 \cdot 1}$$

**Bedeutung:** Anzahl der Möglichkeiten, $n$ verschiedene Objekte anzuordnen

**Beispiele:**
- $3! = 3 \cdot 2 \cdot 1 = 6$
- $4! = 4 \cdot 3 \cdot 2 \cdot 1 = 24$

**Visualisierung für 3 Objekte:**
```
1 Element:  1              → 1 Möglichkeit
2 Elemente: 12, 21         → 2 · 1 = 2 Möglichkeiten
3 Elemente: 123, 132, ...  → 3 · 2 · 1 = 6 Möglichkeiten
```

### Permutationen mit Wiederholungen

$$\boxed{\frac{n!}{k_1! \cdot k_2! \cdot \ldots \cdot k_r!}}$$

wobei:
- $n$ = Gesamtzahl der Objekte
- $k_i$ = Anzahl der ununterscheidbaren Objekte vom Typ $i$

**Multinomialkoeffizient**

**Beispiel 1:** 1 grünes und 3 gelbe Gummibärchen
$$\frac{4!}{1! \cdot 3!} = \frac{24}{6} = 4$$

**Beispiel 2:** 2 grüne und 2 gelbe Gummibärchen
$$\frac{4!}{2! \cdot 2!} = \frac{24}{4} = 6$$

**"Probe":** Summe der Fakultäten im Nenner = Fakultät im Zähler
- $2! + 2! = 4$, aber $4! = 24$ ✓ (Korrekt: $2 + 2 = 4$)

---

## 6. Variationen

### Variationen ohne Wiederholungen

$$\boxed{\frac{n!}{(n-k)!} = n \cdot (n-1) \cdot \ldots \cdot (n-k+1)}$$

**Bedeutung:** Anzahl der Möglichkeiten, $k$ aus $n$ Objekten auszuwählen, wobei die **Reihenfolge wichtig** ist

**Beispiel:** 3 aus 7 Personen auf Plätze 1, 2, 3 verteilen
$$\frac{7!}{(7-3)!} = \frac{7!}{4!} = 7 \cdot 6 \cdot 5 = 210$$

**Visualisierung:**
```
Platz 1: 7 Möglichkeiten
Platz 2: 6 Möglichkeiten (eine Person ist schon gewählt)
Platz 3: 5 Möglichkeiten (zwei sind schon gewählt)
Total: 7 · 6 · 5 = 210
```

### Variationen mit Wiederholungen

$$\boxed{n^k}$$

**Bedeutung:** $k$ Objekte aus $n$ auswählen, Reihenfolge wichtig, **Wiederholungen erlaubt**

**Beispiel:** 4-stellige PIN
$$10^4 = 10000 \text{ Möglichkeiten}$$

Jede Stelle: 10 Möglichkeiten (0-9)

---

## 7. Anwendungsbeispiel: Wege in Graphen

**Problem:** Wie viele Wege von A nach Z, die jeden Knoten höchstens einmal besuchen?

**Formel:** $\frac{n!}{(n-k)!}$ wobei $k$ = Anzahl der Zwischenknoten + 1

**Beispiele:**

| Knoten | Formel | Berechnung | Ergebnis |
|--------|--------|------------|----------|
| 1 (A→Z) | $\frac{1!}{0!}$ | $\frac{1}{1}$ | 1 |
| 2 (A→B→Z) | $\frac{2!}{1!}$ | $\frac{2}{1}$ | 2 |
| 3 (A→B,C→Z) | $\frac{3!}{2!}$ | $\frac{6}{2}$ | 3 |
| 4 | $\frac{4!}{3!}$ | $\frac{24}{6}$ | 4 |

**Für 5 Knoten gesamt:**
$$n_v = \frac{3!}{2!} + \frac{3!}{1!} + \frac{3!}{0!} + 1 = 3 + 6 + 6 + 1 = 16$$

---

## 8. Formalisierung von Zufall

### Historischer Kontext

**Geburtsstunde der Wahrscheinlichkeitstheorie:**
- **1654:** Briefwechsel zwischen Blaise Pascal und Pierre de Fermat
- **Teilungsproblem:** Glücksspiel wird bei Punktestand 3:2 abgebrochen - wie teilt man den Einsatz gerecht?

### Ergebnismenge

$$\boxed{\Omega = \text{Menge aller möglichen Ergebnisse}}$$

**Beispiel - Würfelwurf:**
$$\Omega = \{1, 2, 3, 4, 5, 6\}$$

**Beispiel - Münzwurf:**
$$\Omega = \{\text{Kopf}, \text{Zahl}\} = \{0, 1\}$$

**Beispiel - 2 Münzwürfe:**
$$\Omega = \{00, 01, 10, 11\} = \{0, 1\}^2$$

Anzahl: $n^k$ (Variationen mit Wiederholungen), hier $2^2 = 4$

---

## 9. Ereignisse als Mengen

### Definition

$$\boxed{\text{Ereignis: Teilmenge von } \Omega}$$

**Beispiel - Würfelwurf:**

| Menge | Ereignis |
|-------|----------|
| $\{3\}$ | Eine Drei wurde gewürfelt |
| $\{2, 4, 6\}$ | Gerade Zahl wurde gewürfelt |
| $\{1, 2, 3, 4, 5\}$ | Keine Sechs wurde gewürfelt |
| $\{1, 2, 3\}$ | Zahl kleiner als 4 |

### Spezielle Ereignisse

**Sicheres Ereignis:** $\Omega$ (tritt immer ein)

**Unmögliches Ereignis:** $\emptyset$ (tritt nie ein)

### Mengenoperationen für Ereignisse

| Mengenoperation | Ereignis-Bedeutung | Beispiel |
|-----------------|-------------------|----------|
| $B \subseteq A$ | Wenn $B$ eintritt, dann auch $A$ | $\{2\} \subseteq \{2,4,6\}$ |
| $A \cap B$ | $A$ UND $B$ | $\{1,2,3\} \cap \{2,4,6\} = \{2\}$ |
| $A \cup B$ | $A$ ODER $B$ | $\{1,2\} \cup \{3,1,5\} = \{1,2,3,5\}$ |
| $A \cap B = \emptyset$ | $A$ und $B$ schließen sich aus | $\{1,3,5\} \cap \{2,4,6\} = \emptyset$ |
| $\Omega \setminus A = A^C$ | Komplement | $\{1,2\}^C = \{3,4,5,6\}$ |

---

## 10. Wahrscheinlichkeitsraum

### Definition

$$\boxed{\text{Wahrscheinlichkeitsraum: } (\Omega, \mathcal{P}(\Omega), P)}$$

wobei:
- $\Omega$ = Ergebnismenge ("Was kann passieren?")
- $\mathcal{P}(\Omega)$ = Potenzmenge, alle möglichen Ereignisse ("Welche Ereignisse betrachten wir?")
- $P: \mathcal{P}(\Omega) \to [0,1]$ = Wahrscheinlichkeitsfunktion ("Wie wahrscheinlich?")

### Kolmogorov-Axiome

$$\boxed{
\begin{align}
1. & \quad P(A) \geq 0 \text{ für alle } A \in \mathcal{P}(\Omega) \quad \text{(Nicht-Negativität)} \\
2. & \quad P(\Omega) = 1 \quad \text{(Normierung)} \\
3. & \quad P(A \cup B) = P(A) + P(B) \text{ wenn } A \cap B = \emptyset \quad \text{(}\sigma\text{-Additivität)}
\end{align}
}$$

**Konsequenzen:**
- $P(\emptyset) = 0$
- $P(A^C) = 1 - P(A)$
- $0 \leq P(A) \leq 1$ für alle Ereignisse $A$

---

## 11. Laplace-Experiment

### Definition

$$\boxed{\text{Laplace-Experiment: Zufallsexperiment mit endlich vielen, gleich wahrscheinlichen Ergebnissen}}$$

### Wahrscheinlichkeit im Laplace-Experiment

$$\boxed{P(A) = \frac{|A|}{|\Omega|} = \frac{\text{Anzahl günstiger Fälle}}{\text{Anzahl möglicher Fälle}}}$$

**Beispiel - Würfelwurf:**
$$P(\{5, 6\}) = \frac{|\{5,6\}|}{|\Omega|} = \frac{2}{6} = \frac{1}{3}$$

**Wichtig:** Jedes Elementarereignis hat Wahrscheinlichkeit $\frac{1}{|\Omega|}$

$$P(\{1\}) = P(\{2\}) = \ldots = P(\{6\}) = \frac{1}{6}$$

### Urnenbeispiel: Nicht-Laplace-Experiment

**Gegeben:** 3 rote, 2 blaue Kugeln; ziehe 2 ohne Zurücklegen

**Ergebnismenge:** $\Omega = \{RR, RB, BR, BB\}$

**Wahrscheinlichkeiten:**
- $P(R,R) = \frac{3}{5} \cdot \frac{2}{4} = \frac{3}{10}$
- $P(B,B) = \frac{2}{5} \cdot \frac{1}{4} = \frac{1}{10}$

⇒ **KEIN Laplace-Experiment**, da nicht alle Ergebnisse gleich wahrscheinlich!

---

## 12. Das Geburtstagsproblem

### Die Wette

**Behauptung:** In einer Gruppe von $k$ Personen haben mindestens zwei am selben Tag Geburtstag.

**Frage:** Ab wie vielen Personen lohnt sich die Wette? (d.h. $P(\text{Treffer}) > 0.5$)

### Modellierung als Laplace-Experiment

**Annahmen:**
1. Endlich viele Elementarereignisse: $n = 365$ Tage
2. Alle Geburtstage gleich wahrscheinlich (Gleichverteilung)

**Ergebnismenge für $k$ Personen:**
$$|\Omega| = 365^k \quad \text{(Variationen mit Wiederholungen)}$$

### Berechnung über das Gegenereignis

**Problem:** Günstige Fälle (mind. 2 gleiche) schwer zu zählen

**Lösung:** Berechne ungünstige Fälle (alle verschieden)

$$P(A) = 1 - P(\neg A) = 1 - \frac{|\neg A|}{|\Omega|}$$

**Ungünstige Fälle (alle verschieden):**
$$|\neg A| = \frac{365!}{(365-k)!} \quad \text{(Variationen ohne Wiederholungen)}$$

**Wahrscheinlichkeit:**

$$\boxed{P(\text{mind. 2 gleiche}) = 1 - \frac{365!}{(365-k)! \cdot 365^k}}$$

### Ergebnisse

| Personen $k$ | Wahrscheinlichkeit | Kommentar |
|--------------|-------------------|-----------|
| 4 | 1,6% | Sehr unwahrscheinlich |
| 10 | 12% | Noch unwahrscheinlich |
| 20 | 41% | Fast 50/50 |
| 22 | 47% | Knapp unter 50% |
| **23** | **51%** | **Wette lohnt sich!** |
| 30 | 70% | Deutlich über 50% |
| 50 | 97% | Fast sicher |

### Warum ein Paradoxon?

**Subjektive Schätzung:** Menschen denken oft an ein anderes Modell

**Falsches Modell im Kopf:**
- "Ich greife mich selbst heraus"
- "Wie wahrscheinlich ist es, dass jemand anderes an MEINEM Geburtstag Geburtstag hat?"
- Antwort: $\frac{k-1}{365}$ für $k$ Personen

**Richtiges Modell:**
- "Wie wahrscheinlich ist es, dass IRGENDWELCHE zwei Personen den gleichen Geburtstag haben?"
- Viel mehr Paarvergleiche möglich: $\binom{k}{2} = \frac{k(k-1)}{2}$

**Bei 23 Personen:**
- Falsche Rechnung: $\frac{22}{365} \approx 6\%$
- Richtige Rechnung: 51% (253 Paarvergleiche!)

---

## 13. Bedingte Wahrscheinlichkeit

### Das Taxi-Problem

**Szenario:**
1. Stadt mit 2 Taxi-Unternehmen: 15% blau, 85% grün
2. Unfall mit Fahrerflucht in der Nacht
3. Zeuge sagt: "Das Auto war blau"
4. Test zeigt: Zeuge erinnert Farben in 80% der Fälle korrekt

**Frage:** Wie wahrscheinlich ist es, dass das Auto tatsächlich blau war?

**Intuitive (falsche) Antwort:** ≈ 80%

**Richtige Antwort:** 41%

### Formalisierung

**Gegeben:**
- $P(\text{blau}) = 0.15$ (Prior / Basisrate)
- $P(\text{grün}) = 0.85$
- $P(\text{"blau"} | \text{blau}) = 0.8$ (Sensitivität)
- $P(\text{"grün"} | \text{grün}) = 0.8$ (Spezifität)
- $P(\text{"blau"} | \text{grün}) = 0.2$ (Falsch-Positiv-Rate)

**Gesucht:** $P(\text{blau} | \text{"blau"})$

### Visualisierung mit Häufigkeitstabelle

**Annahme:** 100 Taxis

|  | Tatsächlich blau | Tatsächlich grün | Summe |
|--|------------------|------------------|-------|
| Zeuge sagt "blau" | 12 | 17 | 29 |
| Zeuge sagt "grün" | 3 | 68 | 71 |
| Summe | 15 | 85 | 100 |

**Berechnung:**

$$P(\text{blau} | \text{"blau"}) = \frac{\text{Treffer}}{\text{Treffer} + \text{Falscher Alarm}} = \frac{12}{12 + 17} = \frac{12}{29} \approx 0.41$$

### Signal Detection Theory

| Realität \ Aussage | "blau" | "grün" |
|-------------------|--------|--------|
| **blau** | Treffer (Hit) | Miss |
|  | Korrekt positiv | Falsch negativ |
| **grün** | Falscher Alarm | Korrekte Ablehnung |
|  | Falsch positiv | Korrekt negativ |

---

## 14. Satz von Bayes

### Allgemeine Form

$$\boxed{P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B|A) \cdot P(A) + P(B|\neg A) \cdot P(\neg A)}}$$

**Komponenten:**
- $P(A)$ = **Prior** (A-priori-Wahrscheinlichkeit, Basisrate)
- $P(B|A)$ = **Likelihood** (Wahrscheinlichkeit der Beobachtung unter $A$)
- $P(A|B)$ = **Posterior** (A-posteriori-Wahrscheinlichkeit nach Beobachtung)

### Anwendung auf Taxi-Problem

$$P(\text{blau}|\text{"blau"}) = \frac{0.8 \cdot 0.15}{0.8 \cdot 0.15 + 0.2 \cdot 0.85} = \frac{0.12}{0.12 + 0.17} = \frac{0.12}{0.29} \approx 0.41$$

---

## 15. Base Rate Fallacy (Prävalenzfehler)

### Definition

$$\boxed{\text{Base Rate Fallacy: Fehler, die Basisrate (Prävalenz) von } A \text{ bei der Berechnung von } P(A|B) \text{ zu ignorieren}}$$

**Alternative Namen:** Prävalenzfehler, Basisratenfehler

### Warum passiert der Fehler?

**Psychologische Ursachen:**
1. **Repräsentativitätsheuristik:** Menschen fokussieren auf $P(B|A)$ und ignorieren $P(A)$
2. **Verfügbarkeitsheuristik:** Lebhafte Beispiele übergewichten die Basisrate
3. **Fehlende Intuition für bedingte Wahrscheinlichkeiten**

### Beispiel: Medizinischer Test

**Gegeben:**
- Krankheit kommt bei 1% der Bevölkerung vor (Basisrate)
- Test erkennt Krankheit in 90% der Fälle (Sensitivität)
- Test gibt bei 10% der Gesunden falschen Alarm (Falsch-Positiv-Rate)

**Frage:** Test ist positiv - wie wahrscheinlich ist die Krankheit?

**Intuitive (falsche) Antwort:** ≈ 90%

**Richtige Rechnung:**

$$P(\text{krank}|\text{positiv}) = \frac{0.9 \cdot 0.01}{0.9 \cdot 0.01 + 0.1 \cdot 0.99} = \frac{0.009}{0.009 + 0.099} = \frac{0.009}{0.108} \approx 0.083$$

**Richtige Antwort:** Nur etwa 8%!

**Häufigkeitstabelle (1000 Personen):**

|  | Krank | Gesund | Summe |
|--|-------|--------|-------|
| Test positiv | 9 | 99 | 108 |
| Test negativ | 1 | 891 | 892 |
| Summe | 10 | 990 | 1000 |

$$P(\text{krank}|\text{positiv}) = \frac{9}{108} \approx 8.3\%$$

---

## 📌 Zusammenfassung

### Kombinatorik-Formeln

| Situation | Formel | Name |
|-----------|--------|------|
| $n$ Objekte anordnen (alle verschieden) | $n!$ | Permutationen |
| $n$ Objekte mit Wiederholungen | $\frac{n!}{k_1! \cdot k_2! \cdot \ldots \cdot k_r!}$ | Perm. mit Wdh. |
| $k$ aus $n$ wählen, Reihenfolge wichtig | $\frac{n!}{(n-k)!}$ | Variationen |
| $k$ aus $n$, Reihenfolge wichtig, Wdh. | $n^k$ | Var. mit Wdh. |

### Wahrscheinlichkeit

**Laplace-Experiment:**

$$\boxed{P(A) = \frac{|A|}{|\Omega|} = \frac{\text{günstig}}{\text{möglich}}}$$

**Satz von Bayes:**

$$\boxed{P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B)}}$$

**Geburtstagsproblem:**

$$\boxed{P(\text{mind. 2 gleiche bei } k \text{ Personen}) = 1 - \frac{365!}{(365-k)! \cdot 365^k}}$$

Ab $k = 23$: $P > 50\%$

### Kernpunkte

✅ **Mengen:** Reihenfolge und Wiederholungen irrelevant, Identität durch Elemente

✅ **Inklusions-Exklusions:** $|A \cup B| = |A| + |B| - |A \cap B|$

✅ **Kombinatorik:** Unterscheide Reihenfolge wichtig/unwichtig, Wiederholungen ja/nein

✅ **Wahrscheinlichkeitsraum:** $(\Omega, \mathcal{P}(\Omega), P)$ mit Kolmogorov-Axiomen

✅ **Laplace:** Alle Ergebnisse gleich wahrscheinlich → $P(A) = \frac{|A|}{|\Omega|}$

✅ **Geburtstagsproblem:** Zeigt Grenzen der Intuition, rechne über Gegenereignis

✅ **Base Rate Fallacy:** Basisrate NICHT ignorieren! Nutze Bayes oder Häufigkeitstabellen

### Wichtige Fehlerquellen

❌ **Falsches Modell beim Geburtstagsproblem:** "Mein Geburtstag" vs. "irgendwelche zwei"

❌ **Base Rate ignorieren:** $P(A|B) \neq P(B|A)$

❌ **Nicht-Laplace als Laplace behandeln:** Nicht alle Experimente haben gleiche Wahrscheinlichkeiten

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.XX Statistik]]: Bedingte Wahrscheinlichkeit und Bayes in der Datenanalyse
- [[VL.07 Künstliche Intelligenz]]: Wahrscheinlichkeiten in ML-Modellen
- [[VL.08 Bias, Fairness und Power in AI]]: Base Rate Fallacy bei False Positives
- [[VL.XX Algorithmische Komplexität]]: Kombinatorik zur Abschätzung von Laufzeiten