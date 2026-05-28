**Class:** [[ISDA - Informationsysteme und Datenanalyse]]  
**Date:** 04-05-2026  
**Topics:** #RelationalesModell #RelationalerEntwurf #ERModell #Schlüssel #Informationskapazität #Generalisierung #SchwacherEntityTyp #ISDA #TU-Berlin
**Link:** [[VL.04 ISDA.pdf]]

---

## 🎯 Lernziele der Vorlesung

In dieser Vorlesung geht es um den **relationalen Entwurf**, also die Abbildung eines konzeptionellen ER-/EER-Schemas auf das relationale Datenmodell.

- **Relationales Modell verstehen**: Relation, Tupel, Attribut, Attributwert, Domäne, Schema und Instanz sicher unterscheiden.
- **Schlüsselkonzepte anwenden**: Primärschlüssel, Fremdschlüssel und minimale Schlüssel korrekt bestimmen.
- **ER-Modelle in Relationen überführen**: Grundalgorithmus für Entity-Typen und Relationship-Typen beherrschen.
- **Informationskapazität beurteilen**: kapazitätserhaltende, kapazitätserhöhende und kapazitätsvermindernde Abbildungen erkennen.
- **Kardinalitäten berücksichtigen**: Schlüsselwahl für $m:n$-, $1:n$- und $1:1$-Beziehungen korrekt vornehmen.
- **Relationen sinnvoll zusammenlegen**: Verstehen, wann Zusammenlegung erlaubt ist und wann nicht.
- **Sonderfälle behandeln**: Schwache Entity-Typen sowie Generalisierung/Spezialisierung relational abbilden.
- **Beispielschema nachvollziehen**: Den relationalen Entwurf der Universitätsdatenbank schrittweise herleiten.

---

## 1. Grundlagen des relationalen Modells

### Historischer Kontext

Das relationale Modell geht auf **Edgar F. Codd** zurück und wurde 1970 in dem grundlegenden Artikel _A Relational Model of Data for Large Shared Data Banks_ vorgestellt.

### Definitionen

Eine Relation ist eine Teilmenge eines Kreuzprodukts von Domänen.

$$\boxed{R \subseteq D_1 \times D_2 \times \dots \times D_n}$$

**Wichtige Begriffe:**

- **Domäne**: Wertebereich eines Attributs, z. B. `string` oder `integer`.
- **Relation**: Menge von Tupeln über gegebenen Domänen.
- **Tupel**: Ein einzelner Datensatz, also eine Zeile der Tabelle.
- **Relationenschema**: Name der Relation plus Attributliste.
- **Datenbankschema (Intension)**: Menge aller Relationenschemata einer Datenbank.
- **Ausprägung / Instanz / Extension**: Aktueller Zustand der gespeicherten Daten.

### Beispiel: Telefonbuch

Als Beispiel wird ein Telefonbuch als Relation über drei Domänen modelliert.

$$\boxed{\text{Telefonbuch} \subseteq \text{string} \times \text{string} \times \text{integer}}$$

Ein Tupel könnte dann etwa `("Mickey Mouse", "Main Street", 4711)` sein.

```text
Telefonbuch
┌─────────────────┬──────────────┬──────────┐
│ Name            │ Straße       │ Telefon# │
├─────────────────┼──────────────┼──────────┤
│ Mickey Mouse    │ Main Street  │ 4711     │
│ Minnie Mouse    │ Broadway     │ 94725    │
│ Donald Duck     │ Broadway     │ 95672    │
└─────────────────┴──────────────┴──────────┘
```

### Eigenschaften relationaler Daten

Relationen kann man als Tabellen interpretieren, aber mathematisch sind sie Mengen von Tupeln.

⚠️ **Achtung:** Tupel bilden eine **Menge** und keine Liste, daher sind doppelte Tupel konzeptionell nicht vorgesehen.

⚠️ **Achtung:** Attribute werden als **geordnete** Liste betrachtet, während Tupel als Menge aufgefasst werden.

> 💡 **Merkhilfe:** Im relationalen Modell ist die **Relation** das einzige zentrale Konstrukt; genau diese Einfachheit macht das Modell so mächtig.

---

## 2. Schlüssel und relationale Schemata

### Definition: Relationenschema

Ein Relationenschema besteht aus dem Relationsnamen und einer Liste von Attributen.

$$\boxed{R(A_1, A_2, \dots, A_n)}$$

Eine oft verwendete Kurzschreibweise ist daher etwa `Hört(MatrNr, VorlNr)`.

### Definition: Schlüssel

Ein Schlüssel ist eine minimale Attributmenge, deren Werte ein Tupel eindeutig identifizieren.

$$\boxed{\text{Schlüssel} = \text{minimale identifizierende Attributmenge}}$$

**Begriffe im Überblick:**

|Begriff|Bedeutung|
|---|---|
|**Schlüsselkandidat**|Jede minimale Attributmenge, die Tupel eindeutig identifiziert.|
|**Primärschlüssel**|Ein ausgewählter Schlüsselkandidat mit besonderer Bedeutung für Referenzen.|
|**Fremdschlüssel**|Attribut(e), die auf den Schlüssel einer anderen Relation verweisen.|

### Beispiel-Schema aus der Vorlesung

Das Vorlesungsbeispiel verwendet die drei Relationen `Student`, `Vorlesung` und `Hört`.

```text
Student(MatrNr, Name, Semester)
Vorlesung(VorlNr, Titel, SWS)
Hört(MatrNr, VorlNr)
```

Die Relation `Hört` repräsentiert die Beziehung zwischen Studenten und Vorlesungen.

```text
Student ──m:n── Hört ── Vorlesung
```

### Schritt-für-Schritt-Beispiel

```text
Ausgang:
Student:    MatrNr = 26120
Vorlesung:  VorlNr = 5001

Schritt 1: Student 26120 existiert
Schritt 2: Vorlesung 5001 existiert
Schritt 3: Eintrag in Hört erzeugen → (26120, 5001)

✅ Ergebnis:
Hört enthält das Tupel (26120, 5001)
```

---

## 3. Ziel der Abbildung: Informationskapazität

### Zentrales Ziel

Bei der Abbildung vom ER-Modell auf Relationen soll die **Informationskapazität** erhalten bleiben.

$$\boxed{\text{ER-Modell} \Longrightarrow \text{Relationales Schema mit gleicher Informationskapazität}}$$

Das relationale Schema soll also **genau** die Instanzen darstellen können, die auch das ursprüngliche ER-Diagramm erlaubt.

### Drei Fälle

|Fall|Bedeutung|
|---|---|
|**Kapazitätserhaltend**|Das relationale Schema kann genau so viele Instanzen darstellen wie das ER-Diagramm.|
|**Kapazitätsvermindernd**|Es sind weniger Instanzen darstellbar, also geht Information verloren.|
|**Kapazitätserhöhend**|Es sind mehr Instanzen darstellbar, also werden unerlaubte Zustände möglich.|

✅ **Richtig:** Ziel ist eine **kapazitätserhaltende** Abbildung.

❌ **Falsch:** Eine Abbildung ist nicht gut, wenn sie zwar technisch funktioniert, aber zusätzliche oder zu wenige Datenbankzustände zulässt.

### Rolle der Kardinalität

Bei Entity-Typen ist die Abbildung unproblematisch, aber bei Relationship-Typen hängt die korrekte Schlüsselwahl von der Kardinalität ab.

> 💡 **Merkhilfe:** Die Kardinalität entscheidet, **welche Attribute Schlüssel der Beziehungsrelation werden dürfen**.

---

## 4. Grundalgorithmus: ER-Diagramm $\rightarrow$ Relationenschemata

### Algorithmus

Die Vorlesung gibt einen dreistufigen Grundalgorithmus für die Überführung von ER-Diagrammen in relationale Schemata an.

```pseudocode
RelationalerEntwurf(ER-Diagramm):
1. Für jeden Entity-Typ E:
2.     Erzeuge eine Relation mit denselben Attributen wie E.
3. Für jeden Relationship-Typ R:
4.     Erzeuge eine Relation mit
5.         - den Attributen von R
6.         - den Schlüsselattributen aller beteiligten Entity-Typen.
7. Verfeinere den Entwurf:
8.     - Relationen zusammenlegen, falls erlaubt
9.     - später Normalisierung anwenden
10. Behandle Sonderfälle:
11.     - schwache Entity-Typen
12.     - Generalisierung/Spezialisierung
13. return relationales Schema
```

### Schritt-für-Schritt-Erklärung

- **Schritt 1** bildet alle Entity-Typen direkt auf Relationen ab.
- **Schritt 2** erzeugt für jede Beziehung eine zusätzliche Relation mit den beteiligten Schlüsseln.
- **Schritt 3** verbessert den Entwurf durch Zusammenlegung und später durch Normalisierung.

### Beispiel: Entity-Typen und Relationship-Typen

Aus dem Beispiel mit `Modul`, `Dozent` und `Lehrt` entstehen zunächst drei Relationen.

```text
Dozent(PersNr, Vorname, Name, Titel)
Modul(ModNr, Titel_des_Moduls, {Studiengang}, Leistungspunkte)
Lehrt(ModNr, PersNr, Semester)
```

Für Relationship-Typen müssen neben eigenen Attributen auch die Schlüssel der beteiligten Entity-Typen übernommen werden.

⚠️ **Achtung:** Dabei können doppelte Attributnamen entstehen; dann sind Umbenennungen zur Klarheit nötig.

---

## 5. Schlüsselwahl bei Beziehungsrelationen

### Allgemeine Regel

Die Schlüsselwahl für eine Beziehungsrelation hängt von der Kardinalität ab.

$$\boxed{ \text{Schlüssel(RT)} = \begin{cases} P_1 \cup P_2 & \text{bei } m:n \ P_2 & \text{bei } 1:n \text{, falls } E_2 \text{ die } n\text{-Seite ist} \ P_1 \text{ oder } P_2 & \text{bei } 1:1 \end{cases} }$$

### Fall 1: $m:n$

Bei einer $m:n$-Beziehung müssen **beide** Schlüssel zusammen den Primärschlüssel der Beziehungsrelation bilden.

**Beispiel:** `Hört(MatrNr, VorlNr, Sem)` bei `Student` und `Vorlesung`.

```text
Kapazitätserhaltend:
Hört(MatrNr, VorlNr, Sem)
PK = (MatrNr, VorlNr)
```

✅ So bleiben mehrere Vorlesungen pro Student und mehrere Studenten pro Vorlesung möglich.

❌ Nimmt man nur `MatrNr` als Schlüssel, wäre ein Student nur einmal in `Hört` speicherbar, also wäre die Abbildung kapazitätsvermindernd.

### Fall 2: $1:n$

Bei einer $1:n$-Beziehung wird der Schlüssel der **n-Seite** zum Schlüssel der Beziehungsrelation.

**Beispiel:** `Liest(VorlNr, PersNr, Sem)` mit `Vorlesung` auf der $n$-Seite.

```text
Kapazitätserhaltend:
Liest(VorlNr, PersNr, Sem)
PK = VorlNr
```

❌ Wählt man stattdessen `PersNr` als Schlüssel, könnte ein Dozent nur einmal in `Liest` vorkommen; das wäre kapazitätsvermindernd.

⚠️ Wählt man fälschlich `VorlNr` und `PersNr` gemeinsam als Schlüssel, würde aus einer $1:n$-Beziehung faktisch eine $m:n$-artige Speichermöglichkeit; das wäre kapazitätserhöhend.

### Fall 3: $1:1$

Bei einer $1:1$-Beziehung kann grundsätzlich **einer** der beiden beteiligten Schlüssel als Primärschlüssel gewählt werden.

$$\boxed{\text{Bei } 1:1 \text{ ist } P_1 \text{ oder } P_2 \text{ als Schlüssel möglich.}}$$

> 💡 **Rolle:** Beide Varianten sind inhaltlich möglich; die Entscheidung ist eher eine Design- und Effizienzfrage.

---

## 6. Verfeinerung durch Zusammenlegen von Relationen

### Regel

Die Vorlesung formuliert eine klare Kurzregel für das Zusammenlegen.

$$\boxed{\text{Relationen mit gleichem Schlüssel kann man zusammenfassen – aber nur diese und keine anderen.}}$$

### Wann ist das erlaubt?

Man kann die Relation eines Entity-Typs mit der Relation eines $1:n$-Relationship-Typs zusammenlegen, wenn der Entity-Typ auf der **n-Seite** liegt.

**Begründung:**

- Die Entity-Relation enthält den Schlüssel von $E$ und seine Nicht-Schlüssel-Attribute.
- Die Beziehungsrelation enthält denselben Schlüssel von $E$, weitere Beziehungsattribute und den Schlüssel des anderen Entity-Typs.
- Damit sind alle Werte eindeutig durch denselben Schlüssel bestimmt.

### Beispiel

Aus

```text
Vorlesung(VorlNr, Titel, SWS)
Professor(PersNr, Name, Rang, Raum)
Liest(VorlNr, PersNr)
```

wird durch Zusammenlegung

```text
Vorlesung(VorlNr, Titel, SWS, gelesenVon)
Professor(PersNr, Name, Rang, Raum)
```

Die Umbenennung von `PersNr` zu `gelesenVon` dient hier der besseren Verständlichkeit.

### Schritt-für-Schritt-Beispiel

```text
Ausgang:
Liest(VorlNr, PersNr)

Schritt 1: Vorlesung liegt auf der n-Seite
Schritt 2: Schlüssel von Liest = VorlNr
Schritt 3: Vorlesung hat ebenfalls VorlNr als Schlüssel
Schritt 4: PersNr wird als Fremdschlüssel in Vorlesung integriert

✅ Ergebnis:
Vorlesung(VorlNr, Titel, SWS, gelesenVon)
```

---

## 7. Schwacher Entity-Typ

### Definition und Besonderheit

Ein schwacher Entity-Typ benötigt zur Identifikation zusätzlich den Schlüssel eines starken Entity-Typs.

$$\boxed{\text{Schlüssel(schwacher ET)} = P_{\text{eigene Teilidentifikation}} \cup P_{\text{starker ET}}}$$

### Regeln aus der Vorlesung

- Die Relation des schwachen Entity-Typs enthält nicht nur eigene Attribute, sondern auch die Schlüsselattribute der unterstützenden starken Entity-Typen.
- Relationen für weitere Beziehungen dieses schwachen Entity-Typs müssen diese Attribute ebenfalls mitführen.
- Der unterstützende Relationship-Typ selbst braucht oft **keine** eigene Relation, weil der Fall wie eine $1:n$-Beziehung behandelt wird.

### Beispiel: Modul und Tutorium

```text
Modul(ModNr, Titel_des_Moduls, {Studiengang}, Leistungspunkte)
Tutorium(ModNr, Nummer)
```

Hier ist `Tutorium` der schwache Entity-Typ, und sein Schlüssel ist zusammengesetzt aus `ModNr` und `Nummer`.

```text
Modul ──1:n── Tutorium

Tutorium
┌────────┬────────┐
│ ModNr  │ Nummer │
├────────┼────────┤
│ ...    │ ...    │
└────────┴────────┘
PK = (ModNr, Nummer)
```

⚠️ **Achtung:** Wenn der unterstützende Relationship-Typ eigene Attribute hätte, müssten diese in die Relation des schwachen Entity-Typs übernommen werden.

---

## 8. Generalisierung/Spezialisierung im Relationalen

### Überblick

Für die Überführung von Generalisierung/Spezialisierung nennt die Vorlesung drei Stile.

1. **ER-Stil**
2. **Objektorientierter Stil**
3. **Mit Null-Werten**

### Ausgangsbeispiel Film

Das Beispiel verwendet eine Hierarchie mit `Film`, `Zeichentrickfilm` und `Krimi` sowie Beziehungen wie `Stimme` und `Schauspieler`.

```text
            Film
     (Titel, Länge, Jahr, Typ)
          /              \
Zeichentrickfilm        Krimi
   (Farbe)             (Waffe)
```

### ER-Stil

Beim ER-Stil wird für **jeden Entity-Typ der Hierarchie** eine eigene Relation erzeugt, jeweils mit den Schlüsselattributen des Wurzel-Entity-Typs und den eigenen Attributen.

```text
Film(Titel, Jahr, Länge, Typ)
Krimi(Titel, Jahr, Waffe)
Zeichentrickfilm(Titel, Jahr, Farbe)
Stimme(Titel, Jahr, Name)
Schauspieler(Name)
```

**Wichtige Punkte:**

- Die IST-Beziehung erhält keine eigene Relation.
- Geerbte Schlüsselattribute werden für weitere Beziehungen verwendet.
- Ein konkreter Film kann Tupel in mehreren Relationen besitzen.

### Objektorientierter Stil

Beim objektorientierten Stil wird für jeden möglichen Teilbaum eine Relation mit allen relevanten Attributen erzeugt.

```text
Film(Titel, Jahr, Länge, Typ)
FilmZ(Titel, Jahr, Länge, Typ, Farbe)
FilmK(Titel, Jahr, Länge, Typ, Waffe)
FilmZK(Titel, Jahr, Länge, Typ, Farbe, Waffe)
```

✅ Jedes Objekt gehört hier genau **einer** Klasse an.

### Null-Werte-Stil

Beim Null-Werte-Stil wird eine einzige Relation für die gesamte Hierarchie erzeugt.

```text
Film(Titel, Jahr, Länge, Typ, Waffe, Farbe, ZFlag, KFlag)
```

Nicht-Krimis haben dann `NULL` in `Waffe`, und Nicht-Zeichentrickfilme haben `NULL` in `Farbe`.

⚠️ **Achtung:** Bei disjunkten Subklassen kann ein Typattribut genügen, bei überlappenden Subklassen sind boolesche Flags sinnvoll.

### Vergleich der drei Stile

|Kriterium|ER-Stil|OO-Stil|Null-Werte-Stil|
|---|---|---|---|
|**Anzahl Relationen**|$n$ Relationen bei $n$ Entity-Typen.|Maximal $2^n$ Teilbäume bei $n$ Kindern im überlappenden Fall.|Genau eine Relation.|
|**Speicherbedarf**|Mehrere Tupel pro Entity, aber nur Schlüsselattribute werden wiederholt.|Minimaler Speicherbedarf, da nur ein Tupel pro Entity mit genau den nötigen Attributen gespeichert wird.|Ebenfalls nur ein Tupel pro Entity, aber eventuell viele `NULL`-Werte.|
|**Einfache Anfragen**|Oft direkt möglich.|Können mehrere Relationen erfordern.|Oft günstig, weil nur eine Relation abgefragt werden muss.|
|**Komplexe spezialisierte Anfragen**|Erfordern Joins über mehrere Relationen.|Können sehr effizient sein, wenn genau eine spezialisierte Relation genügt.|Erfordern oft `NULL`-Prüfungen.|

> 💡 **Merkhilfe:** ER-Stil ist „nah am Modell“, OO-Stil ist „nah an Klassen“, Null-Stil ist „nah an einer einzigen Tabelle“.

---

## 9. Relationaler Entwurf: Universitätsdatenbank

### Maximale Zahl an Relationen

Im vollständigen Ausgangsentwurf der Universitätsdatenbank ergeben sich zunächst 15 Relationen als Summe aus Entity-Typen und Relationship-Typen.

```text
Student(MatrNr, BenutzerID, Name, Vorname)
BcStudent(MatrNr, BsSt)
MsStudent(MatrNr, MsSt)
Dozent(PersNr, Name, Vorname, Titel)
Modul(ModNr, Titel_des_Moduls, {Studiengang}, Leistungspunkte)
Vorlesung(ModNr, VorlNr)
Übung(ModNr, ÜbNr)
Prüft(PersNr, MatrNr, Note)
Lehrt(PersNr, ModNr, Sem)
Besucht(MatrNr, ModNr, Note, Semester, Versuch)
Fachgebiet(FName, GebKür, Strasse)
Forscht(PersNr, FName)
Bietet_an(ModNr, FName)
Tutorium(Nummer)
Gehört_zu(ModNr, Nummer)
```

### Minimale sinnvolle Zahl nach Verfeinerung

Nach Generalisierungsabbildung mit Null-Werten, Zusammenlegung von $1:n$-Beziehungen und Einbau des schwachen Entity-Typs reduziert sich das Beispiel auf 10 Relationen.

```text
Student(MatrNr, BenutzerID, Name, Vorname, BcSt, MsSt)
Dozent(PersNr, Name, Vorname, Titel, FName)
Modul(ModNr, Titel_des_Moduls, {Studiengang}, Leistungspunkte, PersNr, Semester)
Vorlesung(ModNr, VorlNr)
Übung(ModNr, ÜbNr)
Prüft(PersNr, MatrNr, Note)
Besucht(MatrNr, ModNr, Note, Semester, Versuch)
Fachgebiet(FName, GebKür, Strasse)
Bietet_an(ModNr, FName)
Tutorium(ModNr, Nummer)
```

### Schritt-für-Schritt-Idee der Verfeinerung

```text
Schritt 1: Student, BcStudent, MsStudent werden zusammengeführt
          → Student(MatrNr, BenutzerID, Name, Vorname, BcSt, MsSt)

Schritt 2: Forscht wird in Dozent integriert
          → Dozent(..., FName)

Schritt 3: Lehrt wird in Modul integriert
          → Modul(..., PersNr, Semester)

Schritt 4: Gehört_zu wird in Tutorium integriert
          → Tutorium(ModNr, Nummer)

✅ Ergebnis:
15 Relationen → 10 Relationen
```

### Schlüsselaspekte

- `Student` hat `MatrNr` als Primärschlüssel.
- `Dozent` hat `PersNr` als Primärschlüssel.
- `Modul` hat `ModNr` als Primärschlüssel.
- `Prüft(PersNr, MatrNr, Note)` benötigt einen zusammengesetzten Schlüssel.
- `Besucht(MatrNr, ModNr, Note, Semester, Versuch)` ist ebenfalls eine Beziehungsrelation mit zusammengesetztem Schlüssel.
- `Tutorium(ModNr, Nummer)` hat wegen des schwachen Entity-Typs den Schlüssel $(ModNr, Nummer)$.

---

## 10. Ausblick: Nächster Schritt im Entwurf

### Was kommt als Nächstes?

Die Vorlesung schließt mit dem Hinweis, dass in der nächsten Veranstaltung die **relationale Entwurfstheorie** behandelt wird.

Insbesondere folgen funktionale Abhängigkeiten, Regeln über funktionale Abhängigkeiten, Entwurf relationaler Schemata, Dekomposition sowie die dritte Normalform.

### Rolle der Normalisierung

Normalisierung gehört im Grundalgorithmus zur Verfeinerung des Entwurfs, wird aber erst in der nächsten Woche im Detail behandelt.

$$\boxed{\text{Relationaler Entwurf} = \text{Abbildung aus ER} + \text{Verfeinerung durch Entwurfstheorie}}$$

---

## 📌 Zusammenfassung

### Wichtige Konzepte

|Konzept|Bedeutung|
|---|---|
|**Relation**|Teilmenge eines Kreuzprodukts von Domänen.|
|**Relationenschema**|Name plus Attributliste einer Relation.|
|**Datenbankschema**|Menge aller Relationenschemata.|
|**Datenbankzustand**|Aktuelle Instanzen aller Relationen.|
|**Schlüssel**|Minimale Attributmenge zur eindeutigen Identifikation eines Tupels.|
|**Informationskapazität**|Menge aller darstellbaren Datenbankzustände.|
|**Zusammenlegen von Relationen**|Nur bei gleichem Schlüssel erlaubt.|

### Kernaussagen

✅ **Entity-Typen** werden direkt und kapazitätserhaltend in Relationen überführt. ✅ **Relationship-Typen** benötigen die Schlüssel der beteiligten Entity-Typen; die Kardinalität bestimmt den Primärschlüssel. ✅ **Bei $m:n$** muss der Schlüssel aus beiden beteiligten Schlüsseln bestehen. ✅ **Bei $1:n$** ist der Schlüssel der $n$-Seite entscheidend. ⚠️ **Zusammenlegen** ist nur dann korrekt, wenn beide Relationen denselben Schlüssel haben. ⚠️ **Generalisierungen** können auf verschiedene Arten abgebildet werden; keine Variante ist in jeder Hinsicht optimal. ❌ **Falsch:** Alle Schlüssel einfach immer gemeinsam zu übernehmen; das kann die Informationskapazität verfälschen.

### Wichtige Formeln und Regeln

|Regel / Formel|Bedeutung|
|---|---|
|$R \subseteq D_1 \times \dots \times D_n$|Definition einer Relation.|
|$R(A_1, \dots, A_n)$|Schreibweise eines Relationenschemas.|
|$P_1 \cup P_2$ bei $m:n$|Beide Schlüssel bilden gemeinsam den Primärschlüssel.|
|$P_2$ bei $1:n$|Schlüssel der $n$-Seite wird Primärschlüssel.|
|$P_1$ oder $P_2$ bei $1:1$|Einer der beiden Schlüssel genügt.|
|$P_{\text{schwach}} \cup P_{\text{stark}}$|Schlüsselregel für schwache Entity-Typen.|

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Datenbankmodellierung]]: Grundlage für diese Vorlesung; dort werden Entity-Typen, Relationship-Typen, Generalisierung und Aggregation konzeptionell entwickelt.
- [[VL.05-ISDA – Relationale Entwurfstheorie]]: Dort folgen funktionale Abhängigkeiten, Dekomposition und Normalformen.
- [[VL.06-ISDA – SQL]]: Die hier entworfenen Relationen werden später als Tabellen mit `PRIMARY KEY` und `FOREIGN KEY` in SQL implementiert.