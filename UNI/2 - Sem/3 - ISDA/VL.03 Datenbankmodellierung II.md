**Class:** [[ISDA - Informationsysteme und Datenanalyse]]  
**Date:** 28-04-2026  
**Topics:** #EER #Generalisierung #Spezialisierung #Aggregation #Sichtenintegration #Designprinzipien #Entwurfsmethodik #ISDA #TU-Berlin
**Link:** [[VL.03 ISDA.pdf]]

---

## 🎯 Lernziele der Vorlesung

Diese Vorlesung erweitert das klassische ER-Modell zum **EER-Modell** und führt methodisch in den strukturierten konzeptionellen Datenbankentwurf ein.

- **Erweiterte ER-Diagramme (EER)** verstehen: Generalisierung/Spezialisierung und Aggregation als zusätzliche Abstraktionskonzepte.
- **Generalisierung/Spezialisierung modellieren**: Notation, Semantik und Integritätsbedingungen sicher anwenden.
- **Aggregation modellieren**: Notation, Kardinalität und Totalität korrekt interpretieren.
- **Komplexe EER-Diagramme lesen und konstruieren**: Universitätsbeispiel nachvollziehen.
- **Designprinzipien anwenden**: Treue zur Anwendung, Redundanzvermeidung und Einfachheit im Entwurf umsetzen.
- **Drei Entwurfsphasen unterscheiden**: frühe, mittlere und späte Entwurfsphase mit ihren Aufgaben kennen.
- **Sichtenintegration verstehen**: mehrere Teilsichten zu einem globalen Schema konsolidieren.
- **Integrationskonflikte erkennen**: Namens-, Typ-, Wertebereichs- und Bedingungskonflikte systematisch behandeln.

---

## 1. Einordnung: Vom ER zum EER-Modell

### Ausgangspunkt

Aus der Anforderungsanalyse wird zunächst die **Miniwelt** abgegrenzt und daraus ein konzeptionelles Schema in Form eines syntaktisch korrekten ER-Diagramms entwickelt.

Bereits bekannt sein sollten dabei die Grundkonzepte **Entity-Typ**, **Relationship-Typ**, **Attribut** sowie die Integritätsbedingungen **Kardinalität** und **Totalität**.

$$\boxed{\text{Miniwelt} \xrightarrow{\text{Anforderungsanalyse}} \text{ER-Diagramm} \xrightarrow{\text{Erweiterung}} \text{EER-Diagramm}}$$

### Warum EER?

Das klassische ER-Modell reicht für einfache Datenstrukturen aus, stößt aber bei komplexeren fachlichen Zusammenhängen an Grenzen.

Das EER-Modell ergänzt deshalb das ER-Modell um zusätzliche **Abstraktionskonzepte**, mit denen gemeinsame Eigenschaften und Teil-Ganzes-Strukturen natürlicher modelliert werden können.

> 💡 **Merkhilfe:** ER beschreibt „was es gibt und wie es zusammenhängt“, EER beschreibt zusätzlich „was spezieller ist als etwas anderes“ und „was aus Teilen besteht“.

---

## 2. Generalisierung und Spezialisierung

### Definition

Die Vorlesung führt Generalisierung und Spezialisierung als zwei Blickrichtungen auf dasselbe Strukturprinzip ein.

$$\boxed{\text{Generalisierung: Spezielle Entity-Typen werden aufgrund gemeinsamer Eigenschaften zu einer Superklasse zusammengefasst.}}$$

$$\boxed{\text{Spezialisierung: Aus einem allgemeinen Entity-Typ werden speziellere Subklassen definiert.}}$$

### Intuition

Bei der **Generalisierung** werden Unterschiede einzelner Entity-Typen unterdrückt und die gemeinsamen Attribute in einer allgemeineren Superklasse gebündelt.

Bei der **Spezialisierung** wird umgekehrt ein allgemeiner Entity-Typ in speziellere Unterklassen aufgeteilt, die zusätzliche Eigenschaften besitzen.

```text
Generalisierung (bottom-up):
  Bachelor      Master
     \            /
      \          /
       Student:In

Spezialisierung (top-down):
       Student:In
       /        \
  Bachelor      Master
```

### Beispiel aus der Vorlesung

Im Universitätsbeispiel werden `Bachelor` und `Master` zu `Student:In` generalisiert, weil beide gemeinsame Attribute wie `MatrNr`, `BenutzerID`, `Name` und `Vorname` besitzen.

Die spezifischen Attribute `BcSt` und `MsSt` bleiben in den jeweiligen Subklassen.

```text
                Student:In
      (MatrNr, BenutzerID, Name, Vorname)
                 {t, d}
                /      \
         Bachelor      Master
          (BcSt)       (MsSt)
```

✅ So wird gemeinsame Information nicht doppelt modelliert.

---

## 3. Integritätsbedingungen der Generalisierung

### Zwei unabhängige Dimensionen

Die Integritätsbedingungen der Generalisierung bestehen aus zwei voneinander unabhängigen Einschränkungen: **Vollständigkeit** und **Disjunktheit**.

$$\boxed{{x, y} \text{ mit } x \in {t, p}, ; y \in {d, o}}$$

### Vollständigkeit

|Symbol|Bedeutung|
|---|---|
|**t**|**total**: Jede Entität der Superklasse gehört zu mindestens einer Subklasse.|
|**p**|**partiell**: Es gibt Entitäten der Superklasse, die keiner modellierten Subklasse angehören.|

### Disjunktheit

|Symbol|Bedeutung|
|---|---|
|**d**|**disjunkt**: Die Subklassen schließen sich gegenseitig aus.|
|**o**|**überlappend**: Eine Entität darf gleichzeitig in mehreren Subklassen liegen.|

### Alle vier Fälle

$$\boxed{ \begin{cases} {t,d} & \text{total, disjunkt} \ {t,o} & \text{total, überlappend} \ {p,d} & \text{partiell, disjunkt} \ {p,o} & \text{partiell, überlappend} \end{cases} }$$

### Beispiele aus der Vorlesung

**{t, d}:** Jede Prüfung an der TU Berlin ist entweder mündlich, schriftlich oder Portfolio, also total und disjunkt modelliert.

**{t, o}:** Jede Studierende ist immatrikuliert, und manche Studierende sind zusätzlich Tutor:innen, also total und überlappend.

**{p, d}:** Statusgruppen von Universitätsangehörigen sind disjunkt, aber nicht vollständig modelliert, also partiell und disjunkt.

**{p, o}:** Räume können zugleich Computerräume und Seminarräume sein, und zusätzlich gibt es weitere nicht modellierte Raumarten, also partiell und überlappend.

```text
{t,d}  Prüfung
       /   |    \
 mündl. schr. portfolio

{t,o}  Studierende
        /       \
 Student:In    Tutor

{p,d}  Uni-Angehöriger
        /         \
  Student:In      Professor

{p,o}  Raum
       /   \
Seminar  Computer
```

⚠️ **Achtung:** Totalität und Disjunktheit sind **nicht dasselbe**; beide Eigenschaften müssen getrennt beurteilt werden.

---

## 4. Aggregation

### Definition

Aggregation ist das zweite neue Abstraktionskonzept der Vorlesung und beschreibt den Aufbau eines zusammengesetzten Objekts aus seinen Komponenten.

$$\boxed{\text{Aggregation} = \text{Modellierung eines Ganzen aus mehreren Teilen}}$$

Die vertikale Beziehung dazu heißt **„Ist-Teil-Von“**.

### Intuition

Während Generalisierung die Frage beantwortet „Welche spezielleren Arten gibt es?“, beantwortet Aggregation die Frage „Aus welchen Bausteinen besteht etwas?“.

Damit beschreibt Aggregation keine Klassifikation, sondern **Komposition** bzw. Struktur.

```text
      Modul
     /  |  \
Vorl. Übung Projekt
```

### Integritätsbedingungen der Aggregation

Wie bei normalen Relationship-Typen müssen auch bei Aggregationen die **Kardinalitäten** angegeben werden.

Die Vorlesung betont zusätzlich die **Totalität**: Ein schwarzer Punkt an einer Komponente bedeutet, dass jede Ausprägung des Aggregats mit mindestens einer Entität dieser Komponente verbunden sein muss.

$$\boxed{\text{Totalität bei Aggregation} \Rightarrow \text{jede Aggregat-Entität besitzt den betreffenden Teil zwingend}}$$

### Beispiele aus der Vorlesung

**Schule:** Eine Schule besteht aus mehreren Klassenräumen, höchstens einer Aula und höchstens einer Sporthalle.

**Modul:** Ein Modul besteht aus genau einer Vorlesung und genau einer Übung; ein Projekt kann optional hinzukommen.

```text
Schule
 ├── Klassenraum   n
 ├── Aula          1
 └── Sporthalle    1

Modul
 ├── Vorlesung     1   (total)
 ├── Übung         1   (total)
 └── Projekt       n   (optional)
```

✅ Aggregation eignet sich besonders, wenn das fachliche Objekt tatsächlich als zusammengesetztes Ganzes verstanden wird.

---

## 5. Komplexes EER-Diagramm: Universitätsbeispiel

### Überblick

Die Vorlesung zeigt ein komplexes EER-Diagramm für eine Universitätsdatenbank, in dem klassische ER-Konzepte mit Generalisierung und Aggregation kombiniert werden.

Enthalten sind u. a. `Student:In`, `Modul`, `Dozent`, `Tutorium`, `Fachgebiet` sowie Beziehungen wie `Besucht`, `Lehrt`, `Prüft`, `Forscht`, `Bietet_an` und `Gehört_zu`.

### Verwendete Erweiterungen

Die Spezialisierung `Student:In → Bachelor/Master` wird mit `{t,d}` modelliert, also total und disjunkt.

Außerdem wird `Modul` als Aggregat aus `Vorlesung` und `Übung` modelliert, jeweils mit Kardinalität `1:1`, sodass jedes Modul genau eine Vorlesung und genau eine Übung besitzt.

```text
Student:In {t,d}
   /        \
Bachelor   Master

Modul
 ├── Vorlesung (1)
 └── Übung     (1)
```

### Auflösung in ein gewöhnliches ERD

Die Folien zeigen auch, wie man die Abstraktionskonzepte in ein gewöhnliches ER-Diagramm übersetzen kann.

Generalisierung wird dann über `Ist_Ein`-Beziehungen modelliert, und Aggregation wird über `Teil_Von`-Beziehungen zwischen dem Aggregat und seinen Komponenten ausgedrückt.

```text
Student:In --Ist_Ein1--> Bachelor
Student:In --Ist_Ein2--> Master

Modul --Teil_Von1--> Vorlesung
Modul --Teil_Von2--> Übung
Modul --Teil_Von3--> Projekt
```

> 💡 **Rolle:** Diese Auflösung ist wichtig, weil sie zeigt, dass EER eine konzeptionelle Erweiterung ist, die sich auf ER-artige Strukturen zurückführen lässt.

---

## 6. Designprinzipien des konzeptionellen Entwurfs

### Leitlinien

Die Vorlesung nennt mehrere konkrete Prinzipien, die beim ER- bzw. EER-Entwurf beachtet werden sollen.

$$\boxed{\text{Guter Entwurf} = \text{treu zur Anwendung} + \text{einfach} + \text{redundanzarm}}$$

### Prinzipien im Überblick

|Prinzip|Bedeutung|
|---|---|
|**Treue zur Anwendung**|Das Modell soll die reale Miniwelt fachlich korrekt abbilden.|
|**Vermeidung von Redundanz**|Informationen sollen nicht unnötig mehrfach modelliert werden.|
|**Einfachheit**|Das Modell soll so klar und einfach wie möglich bleiben.|
|**Überlegte Entscheidung zwischen Entity-Typen und Attributen**|Nicht jedes Merkmal ist gleich ein eigener Entity-Typ.|
|**Sparsamer Einsatz von Relationship-Typen**|Beziehungen nur dort einsetzen, wo sie wirklich fachlich nötig sind.|
|**Sparsamer Einsatz schwacher Entity-Typen**|Schwache Entity-Typen nur bei echter Existenzabhängigkeit nutzen.|

### Praktische Konsequenz

Ein gutes Modell ist nicht das mit den meisten Details, sondern das mit der **besten Balance zwischen Genauigkeit und Verständlichkeit**.

⚠️ **Achtung:** Zu viele Relationship-Typen oder unnötige schwache Entity-Typen machen ein Schema schnell unübersichtlich und schwer wartbar.

---

## 7. Drei Phasen des konzeptionellen Entwurfs

### Überblick

Die Vorlesung beschreibt den konzeptionellen Datenbankentwurf als **dreiphasigen, iterativen Prozess** innerhalb der Drei-Schichten-Architektur.

```text
Frühe Phase  →  Mittlere Phase  →  Späte Phase
  ↖──────── iterative Rückkopplung ───────↗
```

### Frühe Entwurfsphase

In der frühen Phase geht es um die grundlegende Analyse der Miniwelt und die Identifikation der relevanten Begriffe.

Wichtige Ergebnisse sind ein **Glossar**, eine erste Einteilung in Entity-Typen, Attribute und Relationship-Typen sowie ein erster Entwurf des ER-Diagramms.

**Typische Schritte:**

- Zielsetzung der Datenbankentwicklung klären.
- Relevante Begriffe und Objekte identifizieren.
- Synonyme, Homonyme und Unklarheiten bereinigen.
- Irrelevante Begriffe bewusst ausschließen.

### Mittlere Entwurfsphase

Die mittlere Phase vertieft und präzisiert den bisherigen Entwurf.

Hier werden zusätzliche Eigenschaften und Beziehungen ergänzt, Integritätsbedingungen analysiert und mögliche Abstraktionen durch Generalisierung/Spezialisierung und Aggregation erkannt.

### Späte Entwurfsphase

Die späte Phase liefert den vollständigen konzeptionellen Datenbankentwurf.

Am Ende liegen das verfeinerte **ER-/EER-Diagramm**, ein erweitertes **Begriffsglossar** und ein **Protokoll der Entwurfsentscheidungen** vor.

```text
Ergebnis der späten Phase:
- EER-Diagramm
- Glossar
- Entwurfsentscheidungen
- Instanzbeispiele / Erläuterungen
```

✅ Die Vorlesung betont, dass die Dokumentation der Entwurfsentscheidungen **über alle Phasen hinweg** wichtig ist.

---

## 8. Sichtenintegration

### Grundidee

Bei größeren Anwendungen entstehen oft mehrere **Teilschemata** oder **Sichten**, die anschließend zu einem globalen Schema konsolidiert werden müssen.

$$\boxed{\text{Sichtenintegration} = \text{Konsolidierung mehrerer Teilschemata zu einem globalen, widerspruchsfreien Schema}}$$

### Ziel eines globalen Schemas

Das globale Schema soll **redundanzfrei**, **widerspruchsfrei** und semantisch konsistent sein.

Dabei müssen Synonyme, Homonyme und strukturelle Konflikte bereinigt werden.

```text
Sicht 1   Sicht 2   Sicht 3   Sicht 4
   \         |         |        /
    \        |         |       /
         Konsolidierung
               ↓
         Globales Schema
```

### Integrationskonflikte

|Konflikttyp|Beschreibung|Beispiel|
|---|---|---|
|**Namenskonflikte**|Unterschiedliche Namen für dasselbe oder gleicher Name für Unterschiedliches.|Synonyme: Auto, KFZ, Fahrzeug; Homonyme: Schloss, Hahn, Kunde.|
|**Typkonflikte**|Unterschiedliche Modellierung desselben Sachverhalts.|Etwas ist in einer Sicht Attribut, in einer anderen Entity-Typ.|
|**Wertebereichskonflikte**|Unterschiedliche Domänen für dasselbe Element.|Unterschiedliche Wertebereiche für dieselbe ID.|
|**Bedingungskonflikte**|Unterschiedliche Integritätsbedingungen.|Verschiedene Schlüssel für dasselbe Element.|

⚠️ **Achtung:** Integrationskonflikte sind normal und kein Zeichen eines schlechten Zwischenstands; sie müssen bewusst analysiert und aufgelöst werden.

### Konsolidierungsbäume

Die Vorlesung zeigt verschiedene Konsolidierungsbäume, etwa einen **links-tiefen** und einen **balancierten** Baum.

```text
Links-tief:
(((S1 + S2) + S3) + S4)

Balanciert:
((S1 + S2) + (S3 + S4))
```

Beide Vorgehensweisen haben Vor- und Nachteile; die Wahl hängt vom Projekt und den vorhandenen Sichten ab.

---

## 9. Formale Semantik von Generalisierung und Aggregation

### Semantik der Generalisierung

Die Vorlesung ergänzt die Modellierung um eine mengentheoretische Interpretation.

Für einen generalisierten Entity-Typ $G$ und seine Subklassen $E_1, \dots, E_n$ gilt:

$$\boxed{E_1 \subseteq G,; E_2 \subseteq G,; \dots,; E_n \subseteq G}$$

Sind $A_i$ die Attribute von $E_i$ und $A$ die Attribute von $G$, dann gilt außerdem:

$$\boxed{A_i \supset A}$$

### Semantik der Aggregation

Aggregation wird formal als kartesische Produktbildung beschrieben; bei mengenwertigen Komponenten kommt zusätzlich die Potenzmenge ins Spiel.

$$\boxed{A := E_1 \times \dots \times E_k \times \mathcal{P}(E_{k+1}) \times \dots \times \mathcal{P}(E_n)}$$

Dabei bezeichnet $\mathcal{P}(E)$ die Potenzmenge von $E$, also die Menge aller Teilmengen von $E$.

> 💡 **Rolle:** Diese formale Sicht macht deutlich, dass EER-Konzepte nicht nur zeichnerische Notation sind, sondern eine saubere mathematische Grundlage besitzen.

---

## 📌 Zusammenfassung

### Wichtige Konzepte

|Konzept|Bedeutung|
|---|---|
|**Generalisierung**|Spezielle Entity-Typen werden zu einer gemeinsamen Superklasse abstrahiert.|
|**Spezialisierung**|Ein allgemeiner Entity-Typ wird in speziellere Subklassen zerlegt.|
|**Aggregation**|Ein zusammengesetztes Objekt wird aus seinen Komponenten modelliert.|
|**{t,d}**|Total und disjunkt.|
|**{t,o}**|Total und überlappend.|
|**{p,d}**|Partiell und disjunkt.|
|**{p,o}**|Partiell und überlappend.|
|**Sichtenintegration**|Mehrere Teilsichten werden zu einem globalen Schema zusammengeführt.|

### Kernaussagen

✅ **EER** erweitert das klassische ER-Modell um mächtige Abstraktionskonzepte. ✅ **Generalisierung/Spezialisierung** modelliert gemeinsame und spezielle Eigenschaften vertikal. ✅ **Aggregation** modelliert Teil-Ganzes-Strukturen und ist nicht mit Generalisierung zu verwechseln. ✅ **Konzeptioneller Entwurf** ist ein iterativer Prozess in drei Phasen. ⚠️ **Integrationskonflikte** entstehen fast immer bei der Sichtenintegration und müssen systematisch gelöst werden. ❌ **Falsch:** Ein EER-Diagramm sei nur „ein größeres ER-Diagramm“; tatsächlich führt es neue semantische Konzepte ein.

### Wichtige Formeln

|Formel|Bedeutung|
|---|---|
|$E_i \subseteq G$|Subklassen sind Teilmengen der Superklasse.|
|$A_i \supset A$|Subklassen besitzen die Attribute der Superklasse plus eigene.|
|$A := E_1 \times \dots \times E_k \times \mathcal{P}(E_{k+1}) \times \dots \times \mathcal{P}(E_n)$|Formale Semantik der Aggregation.|

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Datenbankmodellierung]]: Grundbegriffe des ER-Modells, auf denen VL.03 direkt aufbaut.
- [[VL.04 Relationaler Entwurf]]: Überführt die hier entwickelten ER-/EER-Schemata in relationale Schemata.
- [[VL.05 Relationale Entwurfstheorie]]: Baut auf dem konzeptionellen und logischen Entwurf auf und behandelt funktionale Abhängigkeiten sowie Normalformen.