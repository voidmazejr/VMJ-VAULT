**Class:** [[InfoProp]]  
**Date:** 26-12-2026  
**Topics:** #Abstraktion #Graphentheorie #Suchalgorithmen #Eulerkreis #Königsberg #Heuristik #Validität #SurvivorshipBias

---

## 🎯 Lernziele der Vorlesung

Abstraktion als zentrale Problemlösungstechnik verstehen und Graphentheorie als Anwendungsbeispiel kennenlernen.

- **Abstraktion** - Definition und Bedeutung in der Informatik
- **Suchalgorithmen** - Planbasiert vs. Heuristisch (A*)
- **Graphentheorie** - Grundbegriffe und Terminologie
- **Königsberger Brückenproblem** - Historisches Abstraktionsbeispiel
- **Eulerkreis und Eulerpfad** - Bedingungen und Algorithmen
- **Hierholzer-Algorithmus** - Finden von Eulerkreisen
- **Validität** - Wissenschaftskriterium
- **Survivorship Bias** - Kognitive Verzerrung

---

## 1. Abstraktion - Definition

### Etymologie

**Lateinisch:** *abstractus* - "abgezogen" von *abs-trahere* - "abziehen, entfernen, trennen"

### Definition

$$\boxed{\text{Abstraktion} = \text{Induktiver Denkprozess, bei dem Spezifika weggelassen werden}}$$

**Abstraktion:**
- Man **lässt Spezifika** eines Problems weg
- Überführt es auf etwas **Allgemeineres** oder **Einfacheres**
- **Trennung** der äußeren Eigenschaften eines Gegenstandes von seiner **Funktion**

### Induktion vs. Deduktion

| Induktion | Deduktion |
|-----------|-----------|
| **Herbeführen** | **Ableiten** |
| Abstrahierender Schluss aus **beobachteten Phänomenen** | Schluss folgt **zwingend/logisch** |
| Auf **allgemeinere Erkenntnis** | Aus bestimmten **Annahmen** |
| Beispiel: Aus vielen Einzelfällen → Regel | Beispiel: Aus Regel → Einzelfall |

### Vorteile und Nachteile

**Vorteile:**

✅ **Vereinfachung** - Fokus auf das Wesentliche

✅ **Generalisierung** - Ein Ansatz für viele Probleme

**Nachteile:**

❌ **Entfremdung** - Verlust wichtiger Details

❌ **Fehlschluss** - Falsche Abstraktion führt zu falschen Lösungen

---

## 2. Beispiele für Abstraktion

### Picasso - "The Head of a Woman"

Abstraktion in der Kunst:
- Reduktion auf wesentliche Formen
- Weglassen unwichtiger Details
- Verstärkung der Essenz

### U-Bahn-Karten (Henry C. Beck, 1933)

**Vergleich:**

| Fred Stingemore (1928) | Henry C. Beck (1933) |
|------------------------|----------------------|
| Realistische Lagebeziehungen | 45° Winkel der Linien |
| Geografisch genau | Topologisch vereinfacht |
| Unübersichtlich | Übersichtlich |

**Prinzip:**
- Realistische Lagebeziehungen **unnötig**
- 45° Winkel erhöhen **Übersichtlichkeit**
- **Kunst des Weglassens** und Vereinfachens basiert auf **Erfahrung**

### Neuronenmodell

**Von komplex zu abstrakt:**

```
Biologisches Neuron (links)         Künstliches Neuron (rechts)
┌─────────────────────┐            ┌──────────────┐
│ Dendriten           │            │   Inputs     │
│ Soma                │     →      │   Weights    │
│ Axon                │            │   Activation │
│ Synapsen            │            │   Output     │
└─────────────────────┘            └──────────────┘
```

**Abstraktion:** Komplexe biologische Strukturen → Einfaches mathematisches Modell

---

## 3. Abstraktion und Problemlösen

### Kernidee

$$\boxed{\text{Algorithmen lösen Probleme, die ähnliche Grundstruktur haben}}$$

**Probleme lösen erfordert Abstraktion!**

### Phasen der Problemlösung (nach Polya, 1945)

```
1. Das Problem verstehen
        ↓
2. Einen Plan zum Lösen entwerfen
        ↓
3. Den Plan umsetzen
        ↓
4. Die Lösung bewerten
   (Generalisierbarkeit: abstrakt → konkret)
```

**Wichtig:** Manchmal versteht man ein Problem **erst**, wenn man es **gelöst** hat!

### Beispiel: Das Alter der drei Kinder

**Problem:**

> Person B sagt: Das Produkt der Alter meiner drei Kinder ist 36.  
> Person A: "Ich brauche einen weiteren Hinweis."  
> Person B: Die Summe der Alter ist X.  
> Person A: "Ich brauche noch einen Hinweis."  
> Person B: "Das älteste Kind spielt Klavier."  
> Person A kann jetzt das Alter sagen. Wie alt sind die Kinder?

**Lösung:**

```
Dreier-Produkte = 36:

(1,1,36) → Summe: 38     (1,6,6) → Summe: 13
(1,2,18) → Summe: 21     (2,2,9) → Summe: 13 ← 
(1,3,12) → Summe: 16     (2,3,6) → Summe: 11
(1,4,9)  → Summe: 14     (3,3,4) → Summe: 10
```

**Schlüssel:** A braucht weiteren Hinweis nach Summe → **Zwei Tripel haben gleiche Summe!**

Die beiden mit Summe 13: (1,6,6) und (2,2,9)

"Ältestes Kind" → **Ein** ältestes, nicht zwei gleich alte älteste

→ **Lösung: 2, 2, 9**

**Erkenntnis:** Erst beim **Versuch**, das Problem zu lösen, kommt das **Verständnis**!

**Inkubationszeit:** Manchmal muss man ein Problem "reifen" lassen

---

## 4. Suchalgorithmen

### Das Suchproblem

**Routenplanung:** Von **Alderaan** nach **Endor**

**Shuttleplan:**
```
3 Alderaan - Bespin
2 Alderaan - Felucia
2 Bespin - Corellia
1 Bespin - Geonosis (Sackgasse)
1 Felucia - Corellia
1 Corellia - Bespin
1 Corellia - Dagobah
1 Dagobah - Endor
```

### Planbasierter Algorithmus (Uninformierte Suche)

**Prinzip:** Wähle Zeile mit bislang **kürzester Reisezeit** und notiere alle möglichen Weiterreisen

**Ablauf:**

```
Start:
3 Alderaan - Bespin
2 Alderaan - Felucia

Nach Felucia (kürzeste Route):
3 Alderaan - Bespin
3 Alderaan - Felucia - Corellia

Von Bespin weiter:
5 Alderaan - Bespin - Corellia
4 Alderaan - Bespin - Geonosis (Sackgasse)
3 Alderaan - Felucia - Corellia

Von Corellia weiter:
5 Alderaan - Bespin - Corellia
5 Alderaan - Felucia - Corellia - Bespin
4 Alderaan - Felucia - Corellia - Dagobah

Endlich Endor:
5 Alderaan - Felucia - Corellia - Dagobah - Endor ✓
```

**Ergebnis:** Route in **5 Monaten**

**Problem:** Nicht besonders "intelligent" - untersucht viele Routen

### Heuristischer Algorithmus (A*)

**Zusatzinformation:** Koordinaten der Planeten → **Distanzschätzung im Euklidischen Raum**

**Wie Menschen das machen:** Abschätzen, ob Route zum Ziel führt!

**Prinzip:**

$$\boxed{f(n) = g(n) + h(n)}$$

Wo:
- $g(n)$ = bisherige Reisezeit
- $h(n)$ = geschätzte Restzeit (Heuristik)
- $f(n)$ = geschätzte Gesamtzeit

**Ablauf:**

```
3+2,1  Alderaan - Bespin           (3 gereist + 2,1 Luftlinie)
2+0,6  Alderaan - Felucia         (2 gereist + 0,6 Luftlinie) ← vielversprechender!

3+1,1  Alderaan - Felucia - Corellia

5+2,1  Alderaan - Felucia - Corellia - Bespin
5+0,0  Alderaan - Felucia - Corellia - Dagobah - Endor ✓
```

**Vorteil:** Findet **schneller** die beste Route durch Nutzung der Zusatzinformation

### Heuristik - Definition

$$\boxed{\text{Heuristik} = \text{Mentale Abkürzung (Shortcut)}}$$

**Eigenschaften:**

- Hilft, Probleme zu lösen
- Hilft, Wahrscheinlichkeiten abzuwägen
- "Daumenregel" (rule of thumb)
- **Nicht garantiert optimal**, aber **meist gut genug** und **schnell**

---

## 5. Graphentheorie - Grundbegriffe

### Definition: Graph

$$\boxed{G = (V, E)}$$

**Graph repräsentiert paarweise Beziehungen zwischen Objekten**

**Komponenten:**

- $V$ = **Vertices** (Knoten, Ecken) - Objekte, z.B. Orte
- $E$ = **Edges** (Kanten) - Beziehungen zwischen Objekten, z.B. Brücken

**Beispiel:**

```
    v1 -------- v2
    |  \      / |
    |    \  /   |
    |     ×     |
    |   /  \    |
    | /      \  |
    v3 -------- v4
```

### Wichtige Begriffe

**Multigraph:**

Mehr als 1 Verbindung zwischen 2 Punkten möglich

**Weg (Kantenzug):**

Folge von Knoten $v_1, ..., v_n$, in der je 2 aufeinanderfolgende Knoten durch eine Kante verbunden sind.

$$\{v_i, v_{i+1}\} \in E \text{ für alle } i < n$$

**Beispiel:** $\{v_1, v_5\}, \{v_5, v_3\}, \{v_3, v_1\}, \{v_1, v_4\}$

**Pfad:**

Ein Weg, bei dem **alle Knoten verschieden** sind (außer eventuell Anfang und Ende)

**Zyklus:**

Ein Weg, bei dem $v_1 = v_n$ (Anfang = Ende)

**Kreis:**

Ein Zyklus, bei dem außer $v_1$ und $v_n$ **alle Knoten verschieden** sind

**Grad eines Knotens:**

Anzahl der Kanten, die an einem Knoten beginnen oder enden

```
Beispiel:
    v1 ---- v2
    |  \    |
    |    \  |
    v3 --- v4

Grad(v1) = 3
Grad(v2) = 2
Grad(v3) = 2
Grad(v4) = 3
```

**Gerader/Ungerader Grad:**

- **Gerade:** Grad ist durch 2 teilbar
- **Ungerade:** Grad ist nicht durch 2 teilbar

---

## 6. Das Königsberger Brückenproblem

### Das historische Problem (Leonhard Euler, 1736)

**Königsberg (Preußen):**

- Flussinsel "Kneiphof"
- Umgeben von zwei Flussarmen
- **7 Brücken** über die Flussarme

**Frage:**

> Gibt es einen Rundweg, der erlaubt, dass man:
> 1. Jede Brücke **einmal** überquert, und
> 2. Am Ende wieder am **Ausgangspunkt** zurückkommt?

### Euler's Abstraktion

**Beobachtungen:**

✅ **Absolute Entfernungen** und **Positionen** sind **unwichtig**!

✅ **Lagen** und **relative Beziehungen** sind wichtig!

**Euler lässt irrelevante Informationen weg und vereinfacht:**

```
Landmassen → Knoten (Punkte)
Brücken    → Kanten (Linien)
```

**Abstraktion:**

```
Original:                  Graph:
┌──Brücke──┐              A ─── B
│  Insel   │               │ \ /│
│          │               │  X │
└──Brücke──┘               │ / \│
                           C ─── D
```

**Bedeutung:** **1736** - Erste Fragestellung der **Graphentheorie**!

Euler begründet damit die Graphentheorie.

---

## 7. Eulerweg und Eulerkreis

### Definitionen

**Eulerpfad (Eulerweg):**

$$\boxed{\text{Ein Weg, der jede Kante genau einmal durchläuft}}$$

- Knoten können **mehrmals** vorkommen
- Ausgangs- $\neq$ Endpunkt

**Eulerkreis:**

$$\boxed{\text{Ein Eulerpfad, der gleichzeitig ein Zyklus ist}}$$

- Jede Kante genau einmal
- $v_1 = v_n$ (Anfang = Ende)
- **Rundweg!**

### Notwendige und hinreichende Bedingungen

**Für einen Eulerkreis:**

$$\boxed{\begin{aligned}
&1. \text{ Graph muss } \textbf{zusammenhängend} \text{ sein}\\
&2. \text{ Jeder Knoten muss } \textbf{geraden Grad} \text{ haben}
\end{aligned}}$$

**Für einen Eulerpfad (kein Kreis):**

$$\boxed{\begin{aligned}
&1. \text{ Graph muss } \textbf{zusammenhängend} \text{ sein}\\
&2. \text{ Genau } \textbf{2 Knoten ungeraden Grad}\\
&\quad \text{(alle anderen geraden Grad)}
\end{aligned}}$$

### Lösung des Königsberger Brückenproblems

**Grade der Knoten:**

```
    A(3) ─── B(5)
       \ /│\
         X │
        /│\│
    C(3) ─ D(3)
```

Alle Knoten haben **ungeraden Grad**!

**Antwort:** **NEIN** - Es gibt **keinen Eulerkreis** und auch **keinen Eulerpfad** durch Königsberg!

(Ein Eulerpfad bräuchte genau 2 Knoten ungeraden Grads, aber hier haben alle 4 Knoten ungeraden Grad)

---

## 8. Haus vom Nikolaus

### Das Problem

```
      2
     /│\
    / │ \
   1──┼──3
   │\ │ /│
   │ \│/ │
   4─────5
```

**Frage:** Kann man das Haus in einem Zug zeichnen, ohne abzusetzen?

### Analyse

**Grade der Knoten:**

- Knoten 1: Grad 3 (ungerade)
- Knoten 2: Grad 2 (gerade)
- Knoten 3: Grad 3 (ungerade)
- Knoten 4: Grad 2 (gerade)
- Knoten 5: Grad 2 (gerade)

**Genau 2 Knoten ungeraden Grads** (1 und 3)

→ Es gibt einen **Eulerpfad** (von 1 nach 3 oder umgekehrt)

→ Es gibt **keinen Eulerkreis** (weil nicht alle Knoten geraden Grad haben)

**Wichtig:** Das Problem ist **schwieriger** als es auf den ersten Blick aussieht!

**Kombinatorik:** Viele verschiedene Möglichkeiten durchzuprobieren

→ **Graphentheorie**: Analytische Lösung - leichter zu überprüfen als alle Möglichkeiten zu testen

---

## 9. Der Algorithmus von Hierholzer (1871)

### Zweck

**Findet einen Eulerkreis** in einem Graphen (falls einer existiert)

### Vorüberlegung

**Wenn ein Graph 2 Zyklen hat:**

```
Zyklus 1: (1,2,3,6,5,1)
Zyklus 2: (3,4,8,7,5,3)

Gemeinsamer Knoten: 3 und 5
```

**Dann kann man beide zu einem neuen Zyklus vereinigen:**

```
Vereinigt: (1,2,3,4,8,7,5,3,6,5,1)
```

### Der Algorithmus

**Voraussetzung:**

- $G = (V, E)$ ist **zusammenhängend**
- Alle Knoten haben **geraden Grad**

**Schritte:**

```
1. Wähle beliebigen Knoten v₀ in G
   
2. Konstruiere von v₀ ausgehend einen Unterkreis K,
   der keine Kante zweimal durchläuft
   
3. Wenn K ein Eulerkreis in G ist → FERTIG!
   Sonst: Lösche alle Kanten des Unterkreises K
   
4. Am ersten Knoten von K, dessen Grad > 0 ist,
   starte weiteren Unterkreis K'
   (der keine Kante zweimal durchläuft)
   
5. Füge K' in K ein:
   Ersetze den Startknoten von K' durch
   alle Knoten von K' in richtiger Reihenfolge
   Nenne den so erhaltenen Kreis K
   
6. Fahre bei Schritt 3 fort
```

### Beispiel

**Gegeben:**

```
    A ─── C ─── E
    │   /   \   │
    │  /     \  │
    B ─────── D │
     \       /  │
      \─────────/
```

**Durchführung:**

```
Schritt 1: Starte bei A
Kreis K: A → C → E → A

Schritt 2: Lösche Kanten, suche Knoten mit Grad > 0
           Finde C

Schritt 3: Von C starten
Kreis K': C → D → C → B → C

Schritt 4: Füge K' in K ein
Neuer K: A → C → D → C → B → C → E → A

Schritt 5: Weiter bei E? Nein, alle Kanten benutzt
           Bei D? ...

Schritt 6: Alle Kanten durchlaufen
Eulerkreis: A → C → D → C → B → C → E → A → B → E → D → A
```

---

## 10. Binärbäume vs. Graphen

### Binärbaum - Definition

$$\boxed{\text{Binärbaum} = \text{Spezielle Form eines Graphen}}$$

**Eigenschaften:**

- **Gerichteter** Graph
- **Azyklisch** (keine Zyklen!)
- **Zusammenhängend**
- Jeder Knoten hat **höchstens 2 Kinder**
- Hat eine **Wurzel** (root)
- Hat **Hierarchie** (Eltern/Kinder)

```
        Root
       /    \
      v1     v2
     /  \   /  \
    v3  v4 v5  v6
```

### Allgemeiner Graph

**Eigenschaften:**

- Kann **Zyklen** haben
- **Beliebig viele** Kanten pro Knoten
- **Keine Hierarchie**
- Keine Wurzel
- Keine Eltern/Kinder-Beziehung

```
    v1 ─── v2
    │ \   / │
    │   X   │
    │ /   \ │
    v3 ─── v4
     \     /
       v5
```

### Graphalgorithmen

**Traversierungsalgorithmen** (Durchlaufen):

- Hierholzer
- Fleury
- ...

**Suchalgorithmen:**

- **Tiefensuche** (Depth-First Search, DFS)
- **Breitensuche** (Breadth-First Search, BFS)
- **A*** (Heuristisch)
- Dijkstra
- ...

---

## 11. Anwendungen der Graphentheorie

### Wann wird Graphentheorie eingesetzt?

**Graphentheorie** ist ein Werkzeug **NACHDEM** die Abstraktion stattgefunden hat!

**Schnittfeld:** Mathematik ↔ Informatik

**Graphen** sind mathematische Modelle für **netzartige Strukturen** in der Welt

### Konkrete Anwendungen

**1. Soziale Netzwerke:**

- V = Personen
- E = Freundschaften/Beziehungen

**2. Spielpläne:**

- V = Teams
- E = Begegnungen

**3. Molekülstrukturen:**

- V = Atome
- E = Bindungen

**4. Verkehrsnetze:**

- V = Orte/Stationen
- E = Straßen/Verbindungen

**5. Weitere:**

- Personalplanung
- Kommunikationsnetze
- Zuordnungen
- Abhängigkeiten in Software
- ...

---

## 12. Wissenschaftskriterium: Validität

### Definition nach Balzert et al. (2022)

$$\boxed{\text{Validität} = \text{Grad der Genauigkeit, mit dem das zu Prüfende tatsächlich geprüft wird}}$$

**Kernfrage:**

> **Wird gemessen, was gemessen werden sollte?**

### Beispiel: Klausur

**Problem:**

```
Lernzielkatalog:      Themen A, B, C
Vorlesung:            Themen A, B, C
Klausur:              Themen A, D, E  ← 

✗ Klausur ist nicht valide!
```

**Ein Drittel der Klausurfragen** bezieht sich auf Wissensgebiete, die weder im Skript noch in den Vorlesungen behandelt wurden.

**Frage:** Was wird hier eigentlich geprüft?

### Fehlerquellen für mangelnde Validität

**1. Zu große Antwortspielräume:**

❌ "Was halten Sie von der Software?"

✅ "In welchem Ausmaß können Sie Ihre Aufgaben mit der Software erledigen?"

**2. Zu kleine Stichprobe:**

Die Auswahl ist nicht **repräsentativ**

**Beispiel:** Ein Psychiater sagt, die ganze Menschheit sei verrückt, weil er nur seine Patienten sieht!

**3. Falsche Stichprobenauswahl:**

**Historisches Beispiel (1936, USA):**

- 10 Millionen Menschen per **Briefwahl** befragt
- 2 Millionen Antworten: **Landon** wird gewinnen
- Tatsächlich gewann **Roosevelt**

**Problem:** Adressen aus **Telefonbüchern** und **Kfz-Zulassungen**

→ Nur **vermögende Klasse** befragt!

→ **Nicht repräsentativ** für Gesamtbevölkerung

→ **Keine Validität**

---

## 13. Survivorship Bias

### Definition

$$\boxed{\text{Survivorship Bias} = \text{Kognitive Verzerrung durch Überbewertung sichtbarer Informationen}}$$

**Weniger sichtbare Informationen** werden vernachlässigt oder übersehen

### Das Flugzeug-Beispiel (Zweiter Weltkrieg)

**Situation:**

US-Fliegerstaffel wurde analysiert, um Flugzeuge zu optimieren.

**Naiver Ansatz:**

1. Untersuche Flugzeuge, die **zurückgekehrt** sind
2. Zähle, wo die meisten **Einschusslöcher** sind
3. **Verstärke** diese Stellen mit Panzerung

**Problem:**

```
Zurückgekehrte Flugzeuge:
  Viele Löcher an: Flügel, Rumpf  ← Sichtbar!
  
Abgeschossene Flugzeuge:
  Viele Löcher an: Motor, Cockpit ← NICHT sichtbar!
```

**Richtige Lösung:**

Die Stellen **OHNE** Einschusslöcher bei zurückgekehrten Flugzeugen müssen gepanzert werden!

**Warum?**

- Flugzeuge mit Treffern an **Flügeln/Rumpf** kommen zurück
- Flugzeuge mit Treffern an **Motor/Cockpit** stürzen ab!

→ **Motor/Cockpit** sind die kritischen Stellen!

### Allgemeines Prinzip

**Survivorship Bias tritt auf, wenn:**

- Man nur **"Überlebende"** betrachtet
- Man **"Nicht-Überlebende"** ignoriert
- Man daraus falsche Schlüsse zieht

**Weitere Beispiele:**

- **Erfolgreiche Unternehmer:** Wir sehen nur die Erfolgreichen, nicht die 90%, die scheitern
- **Börsenerfolg:** Wir hören von Gewinnern, nicht von Verlierern
- **Alte Gebäude:** Wir bewundern robuste alte Architektur, aber die schlechten Gebäude sind längst zerfallen

---

## 14. Abstraktion in der Informatik

### Zentrale Rolle

**1. Funktionen** sind wichtige Abstraktionstechnik in Programmen

**2. Modellierung** ist zentrale Abstraktionstechnik - unabdingbar für Abbildung der realen Welt auf Computer/Software

**3. Computing** = Konstruieren, Manipulieren und Folgern auf Basis von Abstraktionen

**4. Beherrschung komplexer Systeme** durch Abstraktion (z.B. komplexe Softwaresysteme)

**5. Verallgemeinerung** von Lösungsansätzen - Softwarelösungen mehrfach verwenden

**6. Schärfung des Blicks** aufs Wesentliche → Lösungsstrategien werden sichtbar

### Beispiel: Vom Speziellen zum Allgemeinen

**Spezielle Funktionen:**

```python
def billig_strom(verbrauch):
    return 4.9 + 0.19 * verbrauch

def watt_fuer_wenig(verbrauch):
    return 8.2 + 0.16 * verbrauch
```

**Abstraktion → Allgemeine Funktion:**

```python
def alle_tarife(grundgebuehr, pro_einheit, verbrauch):
    return grundgebuehr + pro_einheit * verbrauch
```

**Vorteil:** **Eine** Funktion für **viele** Tarife!

---

## 15. Problemlösestrategien

### Allgemeine Strategien

**Ein Problem lösen erfordert:**

- **Erfahrung/Übung**
- **Geduld**
- **Vertrauen** in die eigenen Fähigkeiten
- → **Kreativität**

### Drei Hauptstrategien

**1. Von hinten anfangen:**

Gegeben: Input → Output

Strategie: Beim **Output** anfangen und sich zum **Input** zurückarbeiten

**2. Verwandtes Problem finden:**

Ein **einfacheres** verwandtes Problem lösen und Lösung auf Kontext anwenden

**3. Zerlegen in Teilprobleme:**

Komplexes Problem in kleinere, lösbare Teilprobleme zerlegen

**Wichtig:** Entscheiden, **welche Strategie** passt!

### Beispiel: Perspektivwechsel

**Das Hut-Problem:**

> Fluss fließt mit 24 km/h. Rudermannschaft rudert flussaufwärts mit 10 km/h relativ zum Ufer. Nach einer Weile fällt ein Hut ins Wasser. Nach 15 Minuten bemerken sie es, kehren um und rudern mit gleicher Kraft zurück. Wie lange brauchen sie, um den Hut einzuholen?

**Falsche Perspektive:** Vom Ufer aus (komplex)

**Richtige Perspektive:** **Vom Wasser aus** betrachten!

Im Bezugssystem des Wassers:
- Boot rudert mit konstanter Geschwindigkeit weg
- Boot rudert mit konstanter Geschwindigkeit zurück
- Hut bewegt sich **nicht** (schwimmt mit Strömung)

→ Zeit hin = Zeit zurück = **15 Minuten**!

### Beispiel: "Einen Fuß in die Tür kriegen"

**Das Rennproblem:**

> A, B, C und D laufen ein Rennen. Vorhersagen:
> - A: "B gewinnt"
> - B: "D wird Letzte"
> - C: "A wird Dritte"
> - D: "A's Vorhersage ist richtig"
> 
> Nur **eine** Vorhersage ist richtig - die der **Gewinnerin**.
> In welcher Reihenfolge beenden sie das Rennen?

**Lösung - Schritt für Schritt:**

```
Beobachtung 1: A und D machen dieselbe Vorhersage
              → Nur eine kann richtig sein
              → Weder A noch D haben gewonnen
              → Beide Vorhersagen sind falsch

Beobachtung 2: A's Vorhersage "B gewinnt" ist falsch
              → B hat nicht gewonnen
              → C ist Gewinnerin! ✓

Beobachtung 3: C's Vorhersage "A wird Dritte" ist richtig
              → A ist Dritte

Beobachtung 4: B hat nicht gewonnen, A ist Dritte
              → Reihenfolge: C _ A _
              → Entweder C B A D oder C D A B?

Beobachtung 5: B's Vorhersage "D Letzte" muss falsch sein
              → D ist NICHT Letzte
              → D ist Zweite

Ergebnis: C D A B ✓
```

**Strategie:** "Einen Fuß in die Tür kriegen" - mit dem arbeiten, was man weiß, und Schritt für Schritt weitergehen!

---

## 📌 Zusammenfassung

### Abstraktion - Kernkonzepte

| Aspekt | Beschreibung |
|--------|--------------|
| **Definition** | Weglassen von Spezifika, Überführung auf Allgemeineres |
| **Vorteile** | Vereinfachung, Generalisierung |
| **Nachteile** | Entfremdung, mögliche Fehlschlüsse |
| **Anwendung** | Problemlösen, Modellierung, Algorithmenentwicklung |

### Suchalgorithmen

| Algorithmus | Typ | Eigenschaft |
|-------------|-----|-------------|
| **Planbasiert** | Uninformiert | Untersucht systematisch alle Routen |
| **A*** | Heuristisch | Nutzt Schätzung (Heuristik) für effizientere Suche |

**Heuristik:** Mentale Abkürzung, "Daumenregel" - meist gut und schnell, aber nicht garantiert optimal

### Graphentheorie - Grundbegriffe

**Graph:** $G = (V, E)$

| Begriff | Definition |
|---------|------------|
| **Knoten (V)** | Objekte (Vertices) |
| **Kanten (E)** | Beziehungen zwischen Objekten (Edges) |
| **Weg** | Folge verbundener Knoten |
| **Pfad** | Weg mit verschiedenen Knoten |
| **Zyklus** | Weg, der zum Startknoten zurückkehrt |
| **Kreis** | Zyklus mit verschiedenen Knoten (außer Start=Ende) |
| **Grad** | Anzahl Kanten an einem Knoten |

### Königsberger Brückenproblem

**Historische Bedeutung:**

- **1736** - Euler begründet Graphentheorie
- Erste graphentheoretische Fragestellung
- Beispiel für erfolgreiche **Abstraktion**

**Abstraktion:**

```
Landmassen → Knoten
Brücken    → Kanten
```

### Eulerkreis und Eulerpfad

**Bedingungen:**

| Typ | Bedingungen |
|-----|-------------|
| **Eulerkreis** | 1. Zusammenhängend<br>2. **Alle** Knoten geraden Grad |
| **Eulerpfad** | 1. Zusammenhängend<br>2. **Genau 2** Knoten ungeraden Grad |

**Königsberg:** Alle 4 Knoten haben ungeraden Grad → **Kein** Eulerkreis, **kein** Eulerpfad!

**Haus vom Nikolaus:** 2 Knoten ungeraden Grad → **Eulerpfad existiert!**

### Hierholzer-Algorithmus

**Prinzip:**

1. Finde Unterkreis
2. Lösche Kanten
3. Finde weiteren Unterkreis
4. Vereinige Kreise
5. Wiederhole bis alle Kanten durchlaufen

**Voraussetzung:**

- Graph zusammenhängend
- Alle Knoten geraden Grad

### Validität

**Definition:**

$\text{Validität} = \frac{\text{Was tatsächlich gemessen wird}}{\text{Was gemessen werden sollte}}$

**Fehlerquellen:**

- Zu kleine/falsche Stichprobe
- Unklare Fragen
- Nicht-repräsentative Auswahl

### Survivorship Bias

**Problem:** Überbewertung **sichtbarer** Informationen

**Flugzeug-Beispiel:**

- ✗ Verstärke Stellen mit vielen Löchern (bei zurückgekehrten Flugzeugen)
- ✓ Verstärke Stellen **ohne** Löcher (das sind die kritischen Stellen!)

**Grund:** Flugzeuge mit Treffern an kritischen Stellen kommen **nicht zurück**!

---

## 🔗 Verbindungen zu anderen Vorlesungen

### Mathematische Grundlagen

- **Zahlentheorie:** Euler (auch Primzahlen, modulare Arithmetik)
- **Kombinatorik:** Königsberger Brückenproblem, Anzahl möglicher Wege
- **Graphentheorie:** Eigenständiges mathematisches Gebiet

### Informatik-Konzepte

- [[VL.04 Algorithmen & Objektivität]]: Euklidischer Algorithmus, Sieb des Eratosthenes
- **Datenstrukturen:** Binärbäume als spezielle Graphen
- **Algorithmen:** Suchalgorithmen (BFS, DFS, A*), Traversierung
- **KI:** Heuristische Suche, Problemlösen

### Wissenschaftstheorie

- [[VL.03 Can Machines Think?]]: Euler's origineller Beitrag
- [[VL.04 Turing Machine, Algorithmen, Objektivität]]: Cognitive Biases, Survivorship Bias
- **Validität:** Neues Qualitätskriterium
- **Abstraktion:** Kernkonzept wissenschaftlichen Denkens

---

## 🎓 Wichtige Konzepte für die Prüfung

### Definitionen

**Abstraktion:** Weglassen von Spezifika, Überführung auf Allgemeineres

**Graph:** $G = (V, E)$ - Knoten und Kanten

**Weg:** Folge verbundener Knoten

**Pfad:** Weg mit verschiedenen Knoten

**Eulerkreis:** Weg, der jede Kante genau einmal durchläuft und zum Start zurückkehrt

**Eulerpfad:** Weg, der jede Kante genau einmal durchläuft (ohne Rückkehr)

**Heuristik:** Mentale Abkürzung, Daumenregel

**Validität:** Wird gemessen, was gemessen werden sollte?

**Survivorship Bias:** Überbewertung sichtbarer Informationen

### Algorithmen können Sie

✅ **Planbasierte Suche:** Systematisch kürzeste Routen finden

✅ **A*-Suche:** Mit Heuristik effizient suchen

✅ **Hierholzer-Algorithmus:** Eulerkreis finden durch Vereinigung von Unterkreisen

✅ **Gradberechnung:** Grad eines Knotens bestimmen

✅ **Eulerkreis-Test:** Bedingungen prüfen (zusammenhängend + alle Knoten geraden Grad)

### Konzepte verstehen Sie

✅ Warum ist **Abstraktion** wichtig für Problemlösen?

✅ Was ist der **Unterschied** zwischen Weg, Pfad, Zyklus, Kreis?

✅ Warum hat das **Königsberger Brückenproblem** keinen Eulerkreis?

✅ Wann existiert ein **Eulerkreis**, wann ein **Eulerpfad**?

✅ Was macht **A*** besser als planbasierte Suche?

✅ Was ist **Survivorship Bias** und wie vermeidet man ihn?

✅ Was bedeutet **Validität** in wissenschaftlichem Kontext?

### Anwendungen erkennen Sie

✅ Welche realen Probleme lassen sich als **Graphen** modellieren?

✅ Wann ist welcher **Suchalgorithmus** geeignet?

✅ Wie erkennt man **Survivorship Bias** in Studien?

✅ Wie prüft man **Validität** einer Messung?

---

## 💡 Vertiefende Fragen

### Abstraktion

1. Welche Informationen sollte man bei Abstraktion **weglassen**?
2. Welche Informationen sind **essentiell**?
3. Wie findet man die richtige **Abstraktionsebene**?

### Graphentheorie

1. Warum ist der **Grad** der Knoten wichtig für Eulerkreise?
2. Wie viele **Brücken** müsste man in Königsberg **bauen**, um einen Eulerkreis zu ermöglichen?
3. Welche anderen **historischen Probleme** führten zur Entwicklung von Graphentheorie?

### Algorithmen

1. Wann ist **heuristische** Suche besser als **systematische**?
2. Kann **A*** garantiert den **optimalen** Weg finden?
3. Wie würde man **Hierholzer** implementieren?

### Wissenschaftstheorie

1. Wie unterscheidet sich **Validität** von **Objektivität**?
2. Welche anderen **kognitiven Verzerrungen** gibt es neben Survivorship Bias?
3. Wie kann man **Validität** in eigenen Studien sicherstellen?

---

## 📝 Übungsaufgaben

### Aufgabe 1: Eulerkreis finden

Gegeben ist dieser Graph:

```
    A ─── B
    │ \ / │
    │  X  │
    │ / \ │
    C ─── D
```

a) Bestimmen Sie den Grad jedes Knotens
b) Gibt es einen Eulerkreis? Begründen Sie.
c) Wenn ja, geben Sie einen an (mit Hierholzer)

**Lösung:**

a) A: Grad 3, B: Grad 3, C: Grad 3, D: Grad 3
b) Nein, alle Knoten haben ungeraden Grad
c) Kein Eulerkreis möglich, aber ein Eulerpfad von einem beliebigen Knoten zu einem anderen

### Aufgabe 2: Stadt mit Brücken

```
    A ─── B
    │     │
    │     │
    C ─── D
    │     │
    E ─── F
```

a) Zeichnen Sie den Graphen
b) Kann man alle Brücken genau einmal überqueren?
c) Bauen Sie eine Brücke, sodass ein Eulerkreis möglich ist

**Lösung:**

a) A:2, B:2, C:3, D:3, E:2, F:2
b) Ja! Eulerpfad von C nach D (genau 2 Knoten ungeraden Grad)
c) Brücke zwischen C und D → alle Knoten Grad 4 (gerade) → Eulerkreis möglich

### Aufgabe 3: A*-Suche

Wenden Sie A* an, um den kürzesten Weg von A nach Z zu finden:

```
Verbindungen:
A → B: 4, A → C: 2
B → D: 5
C → D: 1, C → E: 4
D → Z: 3
E → Z: 2

Luftlinie zu Z:
A: 8, B: 5, C: 6, D: 3, E: 2
```

**Lösung:** A → C → E → Z (Gesamtkosten: 8)