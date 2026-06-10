**Class:** [[ISDA - Informationsysteme und Datenanalyse]]  
**Date:** 18-05-2026  
**Topics:** #ISDA #Datenbanken #RelationaleEntwurfstheorie #FunktionaleAbhaengigkeiten #Normalisierung #BCNF
**Link:** [[VL.05 ISDA.pdf]]

---

## 🎯 Lernziele der Vorlesung

Diese Vorlesung verfeinert den relationalen Entwurf mithilfe funktionaler Abhängigkeiten. Ziel ist es, Redundanzen und Anomalien systematisch zu erkennen und Relationen so zu dekomponieren, dass Semantik, Rekonstruierbarkeit und möglichst auch Abhängigkeitserhalt erhalten bleiben.

- **Funktionale Abhängigkeiten (FDs)**: Semantik von Attributen formal ausdrücken und ausnutzen.
- **Hülle und Ableitungsregeln**: Aus gegebenen FDs weitere FDs bzw. ableitbare Attribute bestimmen.
- **Schlüsselanalyse**: Superschlüssel, Schlüssel und Schlüsselkandidaten aus FDs ableiten.
- **Anomalien erkennen**: Redundanz-, Insert-, Delete- und Update-Anomalien erklären.
- **Normalisierung**: Relationen in 1NF, 2NF, 3NF und BCNF überführen.
- **Entwurfskriterien**: Verlustfreie Wiederherstellung, Abhängigkeitserhalt und Redundanzfreiheit gegeneinander abwägen.

---

## 1. Abschnitt: Definitionen & Grundlagen

### Motivation des relationalen Feinentwurfs

Bisher wurden E/R-Schemata direkt in relationale Schemata übersetzt. Die relationale Entwurfstheorie geht einen Schritt weiter: Sie verbessert den logischen Entwurf anhand semantischer Nebenbedingungen, insbesondere anhand funktionaler Abhängigkeiten.

**Rolle:** Funktionale Abhängigkeiten beschreiben nicht die aktuelle Tabelleninstanz, sondern die inhaltliche Bedeutung der Attribute. Genau diese Semantik erlaubt es, Redundanzen gezielt zu entfernen.

⚠️ **Achtung:** FDs lassen sich nicht zuverlässig aus einer einzelnen Instanz „ablesen“. Sie müssen von Personen angegeben werden, die die Domäne und die Bedeutung der Attribute kennen.

### Definition: Funktionale Abhängigkeit

Eine funktionale Abhängigkeit $X \to Y$ sagt aus: Stimmen zwei Tupel in allen Attributen aus $X$ überein, dann stimmen sie auch in allen Attributen aus $Y$ überein.

$$\boxed{X \to Y \iff \forall r,s \in R: r.X = s.X \Rightarrow r.Y = s.Y}$$

**Wichtige Begriffe:**

- **$X, Y, Z$**: Attributmengen.
- **$A, B, C, \dots$**: Einzelne Attribute.
- **Kurzschreibweise**: Statt ${A,B,C}$ schreibt man oft einfach $ABC$.
- **Mehrere rechte Attribute**: Aus $X \to A$, $X \to B$, $X \to C$ wird kompakt $X \to ABC$.

### Beispiel: FD auf einer Relation

Für ein Schema $R(A,B,C,D)$ kann z. B. gelten:

- $A \to B$
- $CD \to B$
- **nicht** zwingend: $B \to C$

**Intuition:** Wenn $A$ einen Wert eindeutig festlegt, dann darf es keine zwei Tupel mit gleichem $A$ und verschiedenem $B$ geben.

### Beispiel: Stammbaum

In einer Stammbaum-Relation sind typische FDs:

- $Kind \to Vater, Mutter$
- $Kind, Opa \to Oma$
- $Kind, Oma \to Opa$

**Merkhilfe:** Eine FD sagt immer: „Wenn ich diese Information kenne, dann ist jene Information bereits festgelegt.“  
Beispiel: Kennt man das Kind, dann sind Vater und Mutter fest bestimmt.

### Schlüssel als Spezialfall von FDs

$$\boxed{\text{Schlüssel } K \text{ ist eine minimale Attributmenge mit } K \to R}$$

**Wichtige Begriffe:**

- **Superschlüssel**: Attributmenge, die alle Attribute der Relation funktional bestimmt.
- **Schlüssel**: Minimaler Superschlüssel.
- **Schlüsselkandidat**: Jeder minimale Schlüssel, falls es mehrere gibt.
- **Primärschlüssel**: Ausgewählter Schlüsselkandidat.
- **Sekundärschlüssel**: Weitere Schlüsselkandidaten.

✅ **Korrekt:** Jeder Schlüssel ist ein Spezialfall einer FD, denn er bestimmt alle anderen Attribute.  
❌ **Falsch:** Jeder Determinant einer FD ist automatisch ein Schlüssel.

### Beispiel: Schlüsselkandidaten

Für die Relation `Städte(Name, BLand, Vorwahl, EW)` sind mögliche Schlüsselkandidaten:

- $(Name, BLand)$
- $(Name, Vorwahl)$

⚠️ **Achtung:** Eine Vorwahl ist nicht immer allein eindeutig, da mehrere kleinere Städte dieselbe Vorwahl haben können.

### Bestimmung von Schlüsselkandidaten aus FDs

Gegeben sei $R(A,B,C,D)$ mit:

- $AB \to C$
- $AB \to D$
- $C \to B$

Einteilung der Attribute:

- **nur links**: $A$
- **beide Seiten**: $B, C$
- **nur rechts**: $D$

Daraus folgt:

- Attribute, die **nur links** vorkommen, müssen in jedem Schlüsselkandidaten enthalten sein.
- Attribute, die **nur rechts** vorkommen, dürfen nicht Teil eines minimalen Schlüsselkandidaten sein.
- Attribute auf **beiden Seiten** können vorkommen.

Daher sind hier die Schlüsselkandidaten:

- $AB$
- $AC$

---

## 2. Abschnitt: Algorithmus / Verfahren

### Algorithmus: Attributshülle berechnen

Die Hülle $X^+$ ist die Menge aller Attribute, die aus $X$ mithilfe einer FD-Menge $S$ funktional ableitbar sind.

$$\boxed{X^+ = {A \mid X \to A \text{ aus } S \text{ ableitbar ist}}}$$

**Rolle:** Die Attributshülle ist das zentrale Werkzeug für drei Aufgaben: Schlüsselsuche, Test von Ableitbarkeit und Vorbereitung der Normalisierung.

### Schritt-für-Schritt Beispiel

Gegeben seien die FDs:

- $AB \to C$
- $BC \to A$
- $BC \to D$
- $D \to E$
- $CF \to B$

Gesucht ist $(AB)^+$.

```
Ausgangszustand:
H = {A, B}

Schritt 1: Nutze AB -> C
          H -> {A, B, C}

Schritt 2: Nutze BC -> D
          B und C sind in H
          H -> {A, B, C, D}

Schritt 3: Nutze D -> E
          H -> {A, B, C, D, E}

Schritt 4: Keine weitere FD erweitert H

✅ Ergebnis:
(AB)^+ = {A, B, C, D, E}
```

### Membership-Problem

Die Frage lautet: Ist eine bestimmte FD $X \to Y$ aus $F$ ableitbar?

**Idee:** Berechne $X^+$ und prüfe, ob $Y \subseteq X^+$ gilt.

Mit denselben FDs wie oben:

```
Frage 1: Gilt AB -> D?
Berechne (AB)^+ = {A, B, C, D, E}
D ist enthalten
✅ Also ist AB -> D ableitbar.

Frage 2: Gilt D -> A?
Berechne D^+ = {D, E}
A ist nicht enthalten
❌ Also ist D -> A nicht ableitbar.
```

---

## 3. Abschnitt: Mathematische Herleitung

### FD-Mengen, Äquivalenz und Hülle

$$\boxed{S \equiv T \iff \text{S und T dieselbe Menge gueltiger Instanzen beschreiben}}$$

Eine FD-Menge $S$ folgt aus einer FD-Menge $T$, wenn jede unter $T$ gültige Instanz auch $S$ erfüllt. Die Hüllenbildung bedeutet, alle aus einer gegebenen FD-Menge ableitbaren FDs bzw. alle aus einer Attributmenge ableitbaren Attribute zu bestimmen.

### Dekompositions- und Vereinigungsregel

$$\boxed{X \to Y_1 Y_2 \dots Y_m \Rightarrow X \to Y_i \text{ fuer alle } i}$$

$$\boxed{(X \to Y_1) \land (X \to Y_2) \land \dots \land (X \to Y_m) \Rightarrow X \to Y_1 Y_2 \dots Y_m}$$

**Wichtige Beobachtung:** Die Dekomposition funktioniert nur auf der rechten Seite. Aus $OB \to EW$ folgt **nicht** $O \to EW$ und auch **nicht** $B \to EW$.

### Triviale und nicht-triviale FDs

$$\text{Typ}(X \to Y) = \begin{cases} \text{trivial}, & \text{falls } Y \subseteq X \ \text{nicht-trivial}, & \text{falls } Y \nsubseteq X \ \text{voellig nicht-trivial}, & \text{falls } X \cap Y = \emptyset \end{cases}$$

Beispiele:

- trivial: $(BLand, Ort, Straße) \to BLand$
- nicht-trivial: $(BLand, Ort, Straße) \to (BLand, PLZ)$
- völlig nicht-trivial: $(BLand, Ort, Straße) \to PLZ$

✅ **Korrekt:** Jede triviale FD gilt immer.  
⚠️ **Achtung:** Für den Entwurf sind vor allem nicht-triviale und insbesondere völlig nicht-triviale FDs interessant.

### Armstrong-Axiome

$$\boxed{\text{Armstrong-Axiome: Reflexivitaet, Augmentation, Transitivitaet}}$$

Für Attributmengen $X,Y,Z,W$ gelten:

- **R1 Reflexivität:** $X \supseteq Y \Rightarrow X \to Y$
- **R2 Augmentation / Akkumulation:** $X \to Y \Rightarrow XZ \to YZ$
- **R3 Transitivität:** $X \to Y \land Y \to Z \Rightarrow X \to Z$

Weitere nützliche Ableitungsregeln:

- **R4 Dekomposition:** $X \to YZ \Rightarrow X \to Y$
- **R5 Vereinigung:** $X \to Y \land X \to Z \Rightarrow X \to YZ$
- **R6 Pseudotransitivität:** $X \to Y \land WY \to Z \Rightarrow WX \to Z$

### Satz

$$\boxed{\text{Die Armstrong-Axiome sind korrekt, vollstaendig und minimal.}}$$

**Beweisidee:**

- **Korrekt (sound):** Jede Regel erzeugt nur FDs, die in allen Relationen gelten, in denen die Voraussetzungen gelten.
- **Vollständig (complete):** Jede semantisch gültige ableitbare FD lässt sich mit diesen Regeln herleiten.
- **Minimal:** Keine der drei Grundregeln kann entfernt werden, ohne Ausdrucksstärke zu verlieren.

### Korrektheitsbeweis des Hüllenalgorithmus

$$\boxed{\text{Am Ende liefert der Algorithmus genau } X^+}$$

**Beweis (Schleifeninvariante):**

**Anfang:**

- Zu Beginn ist $H := X$.
- Damit enthält $H$ nur Attribute, die trivial aus $X$ folgen.

**Voraussetzung / Schleifeninvariante:**

- Vor jeder Iteration gilt: Jedes Attribut in $H$ ist aus $X$ mittels der gegebenen FDs ableitbar.

**Schritt:**

- Falls eine FD $Y \to Z$ gefunden wird mit $Y \subseteq H$, dann sind alle Attribute aus $Y$ bereits aus $X$ ableitbar.
- Wegen der Gültigkeit von $Y \to Z$ ist dann auch jedes Attribut in $Z$ aus $X$ ableitbar.
- Das Hinzufügen von $Z$ verletzt die Invariante also nicht.

**Terminierung:**

- $H$ wächst monoton.
- Es gibt nur endlich viele Attribute.
- Also kann die Schleife nur endlich oft neue Attribute hinzufügen.

**Abschluss:**

- Wenn die Schleife endet, ist keine FD mehr anwendbar, die $H$ erweitert.
- Wegen der Invariante enthält $H$ nur ableitbare Attribute.
- Wegen der Sättigung fehlt aber auch kein weiter ableitbares Attribut.
- Also gilt $H = X^+$.

### Beispiel: Dozenten-Schema

Gegeben sei:

`Dozent(PersNr, Name, Rang, Raum, Ort, Straße, PLZ, Vorwahl, BLand, EW, Landesregierung)`

Spezifizierte FDs:

- $PersNr \to$ alle Attribute
- $(Ort, BLand) \to (EW, Vorwahl)$
- $PLZ \to (BLand, Ort, EW)$
- $(BLand, Ort, Straße) \to PLZ$
- $BLand \to Landesregierung$
- $Raum \to PersNr$

Ableitbare FDs:

- $Raum \to$ alle Attribute
- $PLZ \to Landesregierung$

**Intuition:** Weil $Raum \to PersNr$ und $PersNr \to$ alle Attribute gilt, bestimmt auch $Raum$ transitiv die gesamte Tupelbeschreibung.

---

## 4. Abschnitt: Diagramme & Strukturen

### ASCII-Diagramm: Ablauf der FD-Analyse

```
┌──────────────────────────────┐
│ Gegebene Relation + FDs      │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Attributshüllen berechnen    │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Schlüssel bestimmen          │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Anomalien / Redundanzen      │
│ erkennen                     │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ Dekomposition wählen         │
└──────────────┬───────────────┘
               │
               ▼
┌──────────────────────────────┐
│ 1NF -> 2NF -> 3NF -> BCNF    │
└──────────────────────────────┘
```

### ASCII-Diagramm: Verlustfreie Dekomposition der Filmrelation

Ausgangsrelation:

```
Film(Titel, Jahr, Laenge, Typ, StudioName, SchauspName, SchauspAdresse)
```

Dekomposition:

```
                 Film
                  |
        ┌─────────┴─────────┐
        |                   |
        ▼                   ▼
Film1(Titel, Jahr,      Film2(Titel, Jahr,
      Laenge, Typ,            SchauspName)
      StudioName)
```

**Idee:** Die Filmdaten werden von den Schauspielzuordnungen getrennt. Dadurch verschwinden Wiederholungen derselben Filminformationen.

### Anomalien

**Redundanz:** Länge und Typ eines Films werden mehrfach gespeichert.  
**Delete-Anomalie:** Wird der letzte Schauspieler eines Films gelöscht, können auch die Filmdaten verloren gehen.  
**Insert-Anomalie:** Ein neuer Film lässt sich eventuell nicht eintragen, solange kein Schauspieler zugeordnet ist.  
**Update-Anomalie:** Eine Änderung, z. B. der Filmlänge, muss an mehreren Stellen konsistent durchgeführt werden.

⚠️ **Achtung:** Genau diese Anomalien sind das zentrale Signal dafür, dass eine Relation weiter normalisiert werden sollte.

### Piecewise-Formel: Normalform-Prüfung

$$NF(R) = \begin{cases} \text{nicht einmal 1NF}, & \text{falls nicht alle Attribute atomar sind} \ \text{1NF}, & \text{falls atomar, aber partielle Abhaengigkeiten existieren} \ \text{2NF}, & \text{falls keine partiellen, aber transitive Abhaengigkeiten existieren} \ \text{3NF}, & \text{falls keine transitiven, aber BCNF-Verletzungen existieren} \ \text{BCNF}, & \text{falls jede nicht-triviale FD einen Superschluessel links hat} \end{cases}$$

---

## 5. Abschnitt: Vergleich / Übersicht

### Normalformen

$$\boxed{\text{Normalisierung = Umformung gegebener FDs in Schluesselabhaengigkeiten durch Dekomposition}}$$

|Normalform|Bedingung|Typische Verletzung|Typische Reparatur|
|---|---|---|---|
|**1NF**|Nur atomare Attribute|Mengenwertige oder strukturierte Attribute|Zerlegung in Grundrelation + Zuordnungsrelation|
|**2NF**|1NF und jedes Nicht-Schlüssel-Attribut hängt voll vom ganzen Schlüssel ab|Partielle Abhängigkeit vom Teilschlüssel|Abspaltung der partiellen FD in eigene Relation|
|**3NF**|2NF und keine transitive Abhängigkeit von Schlüsseln zu Nicht-Schlüssel-Attributen|Nicht-Schlüssel bestimmt anderes Nicht-Schlüssel-Attribut|Aufspaltung entlang transitiver FD|
|**BCNF**|3NF und bei jeder nicht-trivialen FD ist links ein Superschlüssel|Nicht-Superschlüssel bestimmt Attribute|Strengere Dekomposition entlang verletzender FD|

### 1NF

$$\boxed{\text{1NF: Alle Attribute sind atomar.}}$$

Beispiel:

`Modul(ModNr, Titel_des_Moduls, {Studiengang}, Leistungspunkte)`

ist **nicht** in 1NF wegen des mengenwertigen Attributs `{Studiengang}`.

Dekomposition:

- `Modul(ModNr, Titel_des_Moduls, Leistungspunkte)`
- `StudiengangZuordnung(ModNr, Studiengang)`

### 2NF

$$\boxed{\text{2NF: Kein Nicht-Schluessel-Attribut darf nur von einem Teilschluessel abhaengen.}}$$

Beispiel:

- Relation $S(A,B,C,D)$
- FD: $AC \to D$
- FD: $A \to B$
- Schlüsselkandidat: $AC$

Dann ist die Relation **nicht** in 2NF, weil $B$ nur von $A$ und damit von einem echten Teil des Schlüssels abhängt.

Dekomposition:

- $S_1(A,C,D)$
- $S_2(A,B)$

✅ **Regel:** Jede Relation mit nur einem Schlüsselattribut ist, sofern sie in 1NF ist, automatisch in 2NF.

### 3NF

$$\boxed{\text{3NF: Kein Nicht-Schluessel-Attribut darf transitiv von einem Schluessel abhaengen.}}$$

Beispiel:

- Relation $R(A,B,C,D)$
- Schlüssel: $AB$
- zusätzliche FD: $C \to D$

Dann folgt aus $AB \to C$ und $C \to D$, dass $D$ transitiv vom Schlüssel abhängt. Also ist die Relation **nicht** in 3NF.

Dekomposition:

- $R(A,B,C)$
- $S(C,D)$

✅ **Eigenschaft:** 3NF-Dekompositionen sind typischerweise verlustfrei wiederherstellbar und abhängigkeitserhaltend.  
⚠️ **Achtung:** 3NF ist nicht immer absolut redundantfrei.

### BCNF

$$\boxed{\text{BCNF: Fuer jede nicht-triviale FD } X \to Y \text{ muss } X \text{ ein Superschluessel sein.}}$$

**Merkspruch:** Der Schlüssel, der ganze Schlüssel und nichts als der Schlüssel.

Beispiel:

- Relation $R(A,B,C,D)$
- FDs: $AB \to C$, $AB \to D$, $C \to B$

Die Relation ist **nicht** in BCNF, weil $C \to B$ gilt, aber $C$ kein Superschlüssel ist.

Dekomposition:

- $R(A,C,D)$
- $S(C,B)$

✅ **Regel:** Jede Relation mit genau zwei Attributen ist immer in BCNF.  
⚠️ **Achtung:** BCNF ist verlustfrei und redundantfrei, aber nicht immer abhängigkeitserhaltend.

### Warum BCNF strenger ist als 3NF

Betrachte `Stadt(Name, Straße, PLZ)` mit:

- $PLZ \to Name$
- $(Name, Straße) \to PLZ$

Schlüsselkandidaten sind:

- $(Name, Straße)$
- $(PLZ, Straße)$

Hier kann 3NF noch erfüllt sein, obwohl eine Überlappung von zusammengesetzten Schlüsselkandidaten zu Redundanz führt. BCNF verhindert genau solche Fälle, in denen Teile verschiedener Schlüsselkandidaten voneinander abhängen.

### Basisrelationen der Universitätsdatenbank

Als Basisrelationen werden die Relationen bezeichnet, deren Tupel tatsächlich vom DBMS gespeichert werden. Im Idealfall liegen sie in 3NF oder BCNF.

Gegeben sind:

- `Student(MatrNr, BenutzerID, Name, Vorname, BcSt, MsSt)`
- `Dozent(PersNr, Name, Vorname, Titel, FName)`
- `Modul(ModNr, Titel_des_Moduls, {Studiengang}, Leistungspunkte, PersNr, Semester)`
- `Vorlesung(ModNr, VorlNr)`
- `Übung(ModNr, ÜbNr)`
- `Prüft(PersNr, MatrNr, Note)`
- `Besucht(MatrNr, ModNr, Note, Semester, Versuch)`
- `Fachgebiet(FName, GebKür, Straße)`
- `Bietet_an(ModNr, FName)`
- `Tutorium(ModNr, Nummer)`

Zusätzliche FD:

- $GebKür \to Straße$

### Schritt-für-Schritt Normalisierung des Uni-Beispiels

#### 1NF-Test

`Modul(ModNr, Titel_des_Moduls, {Studiengang}, Leistungspunkte, PersNr, Semester)` ist nicht in 1NF.

Dekomposition:

- `Modul(ModNr, Titel_des_Moduls, Leistungspunkte, PersNr, Semester)`
- `StudiengangZuordnung(ModNr, Studiengang)`

#### 2NF-Test

Nach der 1NF-Dekomposition liegen alle gezeigten Relationen in 2NF, weil keine spezifizierte partielle Abhängigkeit vom Teilschlüssel angegeben ist.

#### 3NF-Test

`Fachgebiet(FName, GebKür, Straße)` ist nicht in 3NF, da wegen $GebKür \to Straße$ eine transitive Abhängigkeit vorliegt.

Dekomposition:

- `Fachgebiet(FName, GebKür)`
- `Uni_Gebäude(GebKür, Straße)`

#### BCNF-Test

Die resultierenden Relationen sind in BCNF, weil keine weiteren verletzenden FDs spezifiziert sind. Insbesondere gilt wieder die Regel: Eine Relation mit nur zwei Attributen ist immer in BCNF.

### Entwurfskriterien im Überblick

|Kriterium|Bedeutung|Warum wichtig?|
|---|---|---|
|**Verlustfreie Wiederherstellung**|Die ursprüngliche Relation kann durch Join rekonstruiert werden|Sonst geht Information verloren|
|**Abhängigkeitserhalt**|Wichtige FDs bleiben in den Teilrelationen prüfbar|Integritätsbedingungen bleiben lokal formulierbar|
|**Redundanzfreiheit**|Fakten werden möglichst nur einmal gespeichert|Verhindert Update-, Insert- und Delete-Anomalien|

---

## 6. Abschnitt: Anwendungsbeispiel

### Beispiel: Vollständige Analyse einer Relation

**Aufgabe:** Untersuche die Film-Relation auf Redundanz und schlage eine sinnvolle Dekomposition vor.  
**Zeitkomplexität:** Hängt im Kern von Schlüsselsuche und Hüllenberechnung ab; zentrale Teilschritte liegen typischerweise in polynomialer Zeit in der Größe von Attribut- und FD-Menge.

Gegeben:

`Film(Titel, Jahr, Laenge, Typ, StudioName, SchauspName, SchauspAdresse)`

Beobachtung:

- Filmdaten wie `Laenge`, `Typ`, `StudioName` wiederholen sich für jeden Schauspieler desselben Films.
- Damit entstehen Redundanzen und alle klassischen Änderungsanomalien.

**Pseudocode:**

```pseudocode
1. Identifiziere wiederholte Fakten pro Film.
2. Trenne Filmstammdaten von Schauspielzuordnungen.
3. Erzeuge Film1(Titel, Jahr, Laenge, Typ, StudioName).
4. Erzeuge Film2(Titel, Jahr, SchauspName).
5. Rekonstruiere bei Bedarf durch Join ueber (Titel, Jahr).
```

### Schritt-für-Schritt Beispiel

```
Ausgangszustand:
(Total Recall, 1990, 113, Farbe, Fox, Sharon Stone, Hollywood)
(Total Recall, 1990, 113, Farbe, Fox, Arnold, Sacramento)

Schritt 1: Wiederholung erkennen
          Die Filmdaten sind identisch, nur Schauspieler variiert.

Schritt 2: Filmstammdaten auslagern
          Film1(Total Recall, 1990, 113, Farbe, Fox)

Schritt 3: Zuordnungstabelle bilden
          Film2(Total Recall, 1990, Sharon Stone)
          Film2(Total Recall, 1990, Arnold)

✅ Ergebnis:
Keine mehrfache Speicherung von Laenge, Typ und StudioName pro Schauspieler.
```

### Typische Denkfehler

- ❌ **Falsch:** „Mehr Tabellen sind immer schlechter.“ — Nein, gut gewählte Dekomposition reduziert Redundanz und erhöht Datenqualität.
- ❌ **Falsch:** „3NF und BCNF sind dasselbe.“ — BCNF ist strenger.
- ❌ **Falsch:** „Eine FD beschreibt nur beobachtete Daten.“ — Eine FD beschreibt semantische Gültigkeit auf Schemaebene.
- ✅ **Korrekt:** Gute Normalisierung balanciert Redundanzfreiheit, Verlustfreiheit und Abhängigkeitserhalt.

> 💡 **Merkhilfe:** Eine gute Relation speichert jeden Fakt genau dort, wo er „hingehört“ und möglichst nur einmal.

---

## 📌 Zusammenfassung

### Wichtige Konzepte

|Konzept|Bedeutung|
|---|---|
|**Funktionale Abhängigkeit**|$X \to Y$ bedeutet: Gleiche Werte in $X$ erzwingen gleiche Werte in $Y$.|
|**Attributshülle $X^+$**|Alle Attribute, die aus $X$ mit den gegebenen FDs ableitbar sind.|
|**Superschlüssel**|Attributmenge, die alle Attribute einer Relation bestimmt.|
|**Schlüssel**|Minimaler Superschlüssel.|
|**Minimale Basis**|FD-Menge, aus der alle anderen ableitbar sind und aus der nichts Überflüssiges entfernt werden kann.|
|**Normalisierung**|Dekomposition einer Relation zur Vermeidung von Redundanz und Anomalien.|
|**BCNF**|Strengere Form der 3NF; jede nicht-triviale FD muss links einen Superschlüssel haben.|

### Kernaussagen

✅ **FDs sind Semantik auf Schemaebene** – Sie werden nicht sicher aus einzelnen Datenzuständen abgelesen.  
✅ **Die Hülle ist das Standardwerkzeug** – Mit $X^+$ testet man Ableitbarkeit und Schlüssel.  
✅ **Dekomposition beseitigt Anomalien** – Voraussetzung ist, dass sie sinnvoll und möglichst verlustfrei erfolgt.  
✅ **3NF und BCNF verfolgen unterschiedliche Ziele** – 3NF betont oft Abhängigkeitserhalt, BCNF maximale Redundanzfreiheit.  
⚠️ **Achtung:** Dekomposition kann Abhängigkeitserhalt kosten, auch wenn sie verlustfrei ist.  
❌ **Falsch:** Triviale FDs liefern bereits interessante Entwurfsinformation.

### Wichtige Algorithmen / Formeln

|Algorithmus / Formel|Laufzeit / Charakter|Anwendung|
|---|---|---|
|**Attributshülle $X^+$**|typischerweise polynomial|Ableitbare Attribute und Schlüssel testen|
|**Membership-Test**|reduziert sich auf Hüllenberechnung|Prüfen, ob $X \to Y$ aus $F$ folgt|
|**2NF-/3NF-/BCNF-Test**|analytisches Prüfverfahren|Verletzende FDs finden und dekomponieren|
|**$X \to Y \iff \forall r,s: r.X=s.X \Rightarrow r.Y=s.Y$**|Definition|Formale Semantik von FDs|
|**$X^+ = {A \mid X \to A}$**|Definition|Alle aus $X$ ableitbaren Attribute|
|**BCNF-Bedingung**|strukturelle Eigenschaft|Test auf absolute Redundanzfreiheit bezüglich FDs|

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.04 Relationaler Entwurf]]: Die heutige Vorlesung baut direkt auf Relation, Tupel, Attribut, Relationsschema und der Übersetzung von E/R-Modellen auf.
- [[VL.06 Datenbankdarstellung mit SQL]]: Normalisierte Schemata werden in späteren Vorlesungen in SQL als Tabellen, Schlüssel und Constraints umgesetzt.
- [[VL.02 Datenbankmodellierung]]: Gute konzeptionelle Modellierung reduziert bereits viele spätere Normalisierungsprobleme.
- [[VL.06 Datenbankdarstellung mit SQL]]: Funktionale Abhängigkeiten motivieren Schlüssel- und Konsistenzbedingungen im relationalen Modell.