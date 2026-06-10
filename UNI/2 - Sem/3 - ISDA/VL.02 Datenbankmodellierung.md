**Class:** [[ISDA - Informationsysteme und Datenanalyse]]
**Date:** 21-04-2026
**Topics:** #Datenbankmodellierung #ER-Diagramm #EntityRelationship #Kardinalität #Totalität #Schlüssel #SchwacherEntityTyp #Integritätsbedingungen #Mengenlehre #Prädikatenlogik
**Link:** [[VL.02 ISDA.pdf]]

---

## 🎯 Lernziele der Vorlesung

VL.02 behandelt **Datenbankmodellierung I** — die Erstellung eines konzeptionellen Schemas mit ER-Diagrammen, unabhängig von einem konkreten DBMS.

- **Methodik**: von der Miniwelt zum konzeptionellen Schema
- **ER-Diagramm**: Entity-Typ, Relationship-Typ, Attribut, Integritätsbedingungen
- **Syntaktisch korrektes ER-Diagramm**: 6 Schritte
- **Integritätsbedingungen**: Kardinalität, Totalität, referentielle Integrität
- **Schwacher Entity-Typ**: partieller Schlüssel, Existenzabhängigkeit
- **Semantik**: mathematische Formalisierung via Mengenlehre und Prädikatenlogik

---

## Wiederholung: Was sollten wir bereits wissen

Eine **Datenbank** ist eine Sammlung von Daten, die einen Ausschnitt der realen Welt beschreiben. Drei Abstraktionsebenen im DBMS:

```
Externe Ebene   → Sichten (Teilmengen der Information)
Logische Ebene  → Datenbankschema (welche Daten?)
Physische Ebene → Speicherstruktur (wie gespeichert?)
```

- **Physische Datenunabhängigkeit**: Änderungen der Speicherstruktur beeinflussen die logische Ebene nicht
- **Logische Datenunabhängigkeit**: Änderungen am Schema beeinflussen die Sichten nicht
- DBMS basieren auf einem **Datenmodell**, das die Infrastruktur für die Modellierung bereitstellt

---

## 1. Phasen des Datenbankentwurfs

```
Realwelt / Miniwelt
       ↓ Anforderungsanalyse
Anforderungsspezifikation
       ↓ Konzeptioneller Entwurf
ER-Schema (konzeptionell, DBMS-unabhängig)
       ↓ Implementationsentwurf
DB-Schema (z.B. relational)
       ↓ Physischer Entwurf
Physische Datenbankstruktur (Effizienz)
```

| Phase | Eingabe | Ausgabe |
|-------|---------|---------|
| **Anforderungsanalyse** | Miniwelt präzise beschreiben | Anforderungsspezifikation |
| **Konzeptioneller Entwurf** | Informationsstruktur festlegen | ER-Schema |
| **Implementationsentwurf** | Datenmodell des DBMS | DB-Schema |
| **Physischer Entwurf** | Effizienzsteigerung | Physische DB-Struktur |

### Miniwelt (Universe of Discourse, UoD)

- Abgrenzung eines Teils der „realen Welt" → Aufgabe der Anforderungsanalyse
- **Konzentration auf das Wesentliche**, Abstraktion überflüssiger Details
- Der Erfolg der Datenbank hängt von der richtigen Abgrenzung der Miniwelt ab

### Von der Miniwelt zum Schema

```
Miniwelt → [Manuelle/intellektuelle Modellierung] → Konzeptionelles Schema (ER)
         → [Halbautomatische Transformation] → Relationales / XML / OO Schema
```

Das **ER-Diagramm** ist das mit Abstand am häufigsten verwendete Beschreibungsmittel für konzeptionelle Modelle. Konzeptionelle Modelle haben **keine Datenmanipulationssprache** — sie beschreiben nur Struktur.

---

## 2. Entity-Relationship-Modell (nach Peter P. Chen, 1976)

> *„The entity-relationship model – towards a unified view of data."* ACM TODS — Standardmodell für das konzeptionelle Schema.

### Grundbegriffe und Notation

| Begriff                       | Definition                                                                                   | Notation                |
| ----------------------------- | -------------------------------------------------------------------------------------------- | ----------------------- |
| **Entity / Entität**          | Ding / Objekt der realen oder Vorstellungswelt; nur über Eigenschaften beobachtbar           | —                       |
| **Entity-Typ** (*entity set*) | Menge gleichartiger Objekte                                                                  | Rechteck                |
| **Relationship**              | Beschreibt Beziehungen zwischen Entities (meist binär)                                       | —                       |
| **Relationship-Typ**          | Menge gleichartiger Beziehungen                                                              | Raute                   |
| **Attribut**                  | Eigenschaft von Entities oder Relationships; primitive Datenwerte                            | Ellipse                 |
| **Schlüsselattribut**         | Minimale Menge von Attributen, die ein Entity eindeutig innerhalb seines Typs identifizieren | Ellipse mit Unterstrich |
| **Integritätsbedingung**      | Kardinalität, Totalität, Nebenbedingungen — aus Eigenschaften der Miniwelt abgeleitet        | Kantenmarkierung        |

⚠️ Integritätsbedingungen sind **keine Eigenschaften von Daten** — sie werden von Personen festgelegt, die die Semantik der Miniwelt kennen!

---

## 3. Syntaktisch korrektes ER-Diagramm

### 6 Schritte der Erstellung

1. Alle **Entity-Typen** definieren
2. **Relationship-Typen** zwischen Entity-Typen festlegen
3. **Attribute** für Entity-Typen definieren
4. Attribute für **Relationship-Typen** definieren (falls nötig)
5. **Schlüsselattribut** für jeden Entity-Typ notieren
6. **Kardinalität** festlegen

### Merkmale eines syntaktisch-korrekten ER-Diagramms

- Alle Entity-Typen müssen über mindestens einen Relationship-Typ **verbunden** sein
- Jeder Entity-Typ muss **ein oder mehrere Attribute** besitzen
- Jeder Relationship-Typ **kann** ein oder mehrere Attribute besitzen
- Für jeden Entity-Typ muss ein **Schlüsselattribut** definiert werden
- Für jeden Relationship-Typ muss die **Kardinalität** festgelegt werden

### Beispiel: Universität (Kern-ER)

![[Screenshot 2026-04-21 at 15.17.17.png|600]]

---

## 4. Integritätsbedingungen

### Kardinalität

![[Screenshot 2026-04-21 at 15.17.49.png|600]]

Relationship-Typ $RT \subseteq ET_1 \times ET_2$:

| Kardinalität | Bedeutung |
|------------|----------|
| **1:1** | Einem Entity aus $ET_1$ ist höchstens ein Entity aus $ET_2$ zugeordnet und umgekehrt |
| **1:n** | Einem Entity aus $ET_1$ können beliebig viele Entities aus $ET_2$ zugeordnet sein |
| **n:1** | Analog zu 1:n (symmetrisch) |
| **n:m** | Keinerlei Restriktionen — max $n$ zu max $m$ |

**Mathematische Formalisierung n:1:**

$$\forall e_1, e_2 \in E_1, e \in E_2 : (e_1, e) \in R \land (e_2, e) \in R \Rightarrow e_1 = e_2$$

$$\forall e_2 \in E_2 : |\{(e, e_2) \in R \mid e \in E_1\}| \leq n$$

### Totalität (Teilnahmeeinschränkung)

![[Screenshot 2026-04-21 at 15.19.31.png|425]]

Totalität verlangt, dass **alle Entities eines Entity-Typs** an einer Beziehung teilnehmen müssen.

**Notation:** schwarzer Punkt (●) an der Muss-Seite

**Mathematische Formalisierung (links-total):**

$$\forall e_1 \in E_1 \; \exists e_2 \in E_2 : (e_1, e_2) \in R$$

**Beispiel:** Jedes Modul *muss* von einem Dozenten gelehrt werden (Modul ist existenzabhängig von Dozent).

### Referentielle Integrität

Ein Entity, auf das sich ein anderes bezieht, **muss existieren**:
- Bei Einfügen/Ändern eines Moduls muss der entsprechende Dozent vorhanden sein
- Ein Dozent darf nicht gelöscht werden, solange er noch Module lehrt — oder: Löschen kaskadiert
- Wird im ER-Diagramm durch **Totalität + Kardinalität n:1** ausgedrückt

### Allgemeine Nebenbedingungen (Constraints)

Nicht alle Constraints haben graphische Notation. Sie werden in den **Entwurfsentscheidungen dokumentiert** und erst bei der DB-Programmierung implementiert:

- **Datentyp**: Integer, String, …
- **Wertebereich / Domäne**: z.B. Alter $\in [16, 70]$; Geschlecht $\in \{m, w, d\}$
- **Länge**: z.B. Stringlänge Name $< 25$
- **Kardinalität**: z.B. mindestens 3 Studierende pro Kurs

---

## 5. Weitere Konzepte

### Kardinalität bei n-stelligen Relationship-Typen

$$RT \subseteq ET_1 \times \ldots \times ET_{k-1} \times ET_{k+1} \times \ldots \times ET_n \to ET_k$$

Eine „1" bei $ET_k$ bedeutet: für feste Werte aller anderen Entity-Typen ist der $ET_k$-Wert eindeutig bestimmt.

**Beispiel: „Betreut" (Dozent, Student, Seminarthema)**

$$\text{Betreut} : \text{Dozent} \times \text{Student} \to \text{Seminarthema}$$
$$\text{Betreut} : \text{Seminarthema} \times \text{Student} \to \text{Dozent}$$

- Student darf dasselbe Thema nur einmal bearbeiten
- Student darf bei einem Dozenten nur ein Thema belegen
- Dozenten dürfen dasselbe Thema mehrfach vergeben (an verschiedene Studenten)

Illegale Ausprägungen: gleicher Student + gleicher Dozent mit zwei Seminaren; gleicher Student + gleiches Thema bei zwei Dozenten.

### Konvertierung n-ärer in binäre Relationship-Typen

**Methode:** Neuen verbindenden **Entity-Typ** einführen, n-ären RT ersetzen durch mehrere binäre n:1-RTs.

```
VORHER: Prüft (Dozent, Student, Modul) mit Attribut Note
NACHHER:
  Dozent ──(1)── RT1 ──(n)── Prüfung ──(n)── RT2 ──(1)── Modul
                               [Note]
                                 │
                                (n)── RT3 ──(1)── Student
```

- Attribute des n-ären RT werden an den **neuen Entity-Typ** angehängt
- Falls ein Entity-Typ mehrere Rollen spielt: pro Rolle ein eigener Relationship-Typ

### Rollen von Relationship-Typen

**Rekursiver Relationship-Typ**: Entity-Typ taucht mehr als einmal auf → jede Kante entspricht einer anderen Rolle.

**Beispiel: Setzt_voraus (Modul)**

```
Modul ──(m)── Setzt_voraus ──(n)── Modul
          Vorgänger           Nachfolger
```

Beispiele: Statistik I → II; Filmfortsetzungen.

### Weitere Attributarten

| Attributart | Definition | Notation |
|------------|-----------|---------|
| **Optionales Attribut** | Attributwert nicht für jedes Entity vorhanden (z.B. Telefonnummer) | Ellipse mit gestricheltem Rand |
| **Abgeleitetes Attribut** | Berechnung aus gespeicherten Attributen (z.B. Bruttopreis = Netto + MwSt) | Ellipse mit gestricheltem Rand + Pfeil |
| **Mengenwertiges Attribut** | Enthält Menge von Werten (z.B. Studiengänge) | `{Attributname}` |
| **Strukturiertes Attribut** | Wird durch Unterattribute beschrieben (z.B. Adresse: Straße, PLZ, Ort) | Ellipse mit Ästen |

### Schlüsselattribute

- Minimale Menge von Attributen: keine zwei Entities haben gleiche Werte in allen Schlüsselattributen
- Jeder Entity-Typ muss einen Schlüssel haben; es kann mehrere geben
- Üblich: **Primärschlüssel** auswählen, weitere sind Sekundärschlüssel

**Mathematische Formalisierung (injektive Abbildung):**

$$\forall e_1, e_2 \in E : e_1 \neq e_2 \Rightarrow a(e_1) \neq a(e_2)$$

### Schwacher Entity-Typ

Entity-Typ ohne eigene Schlüsselattribute — nur mit **partiellem Schlüssel**.

**Notation:** Doppelrechteck (Entity-Typ), Doppelraute (Relationship-Typ)

**Eigenschaften:**
- Immer **existenzabhängig** (total auf der schwachen Seite)
- Beziehung zum starken Typ ist immer **1:n** (oder selten 1:1)
- Schlüssel = Schlüssel des starken Typs + partieller Schlüssel

**Beispiel:** Tutorium hat nur eine Nummer — verschiedene Module können Tutorien mit gleicher Nummer haben → Schlüssel = (ModNr, Nummer)

```
Modul ──(1)── Gehört_zu ──(n)── Tutorium
[ModNr, …]                      [Nummer (partiell)]
```

---

## 6. Komplexes ER-Diagramm: Universität_DB

### Anforderungsanalyse

- 32.000 Bachelor- und Master-Studenten
- Studenten: MatrNr, Vorname, Name, BenutzerId, Studiengang, besuchte/abgeschlossene Module (Semester, Versuch, Note)
- Jedes Modul: genau eine Vorlesung + eine Übung
- 3. Versuch: mündliche Prüfung nur durch den LV-Dozenten
- Tutor:innen-Pool auf Tutorien verteilen
- Module von Fachgebieten angeboten; Dozenten forschen in Fachgebieten
- Fachgebiete: Name (eindeutig), Gebäude (Kürzel, Straße)

**Regel:** Das Wesentliche zuerst! → 3 wichtigste Entity-Typen (Student, Modul, Dozent) bilden den Kern.

### Vollständiges ER-Diagramm

Entity-Typen und Attribute:

| Entity-Typ | Schlüssel | Weitere Attribute |
|-----------|---------|------------------|
| **Student:In** | MatrNr | Vorname, Name, BenutzerId, {Studiengang} |
| **Modul** | ModNr | Titel, {Studiengang}, Leistungspunkte |
| **Dozent** | PersNr | Titel, Name, Vorname |
| **Fachgebiet** | FName | Straße, GebKür |
| **Tutorium** | (ModNr, Nummer) | Nummer (partiell) |

Relationship-Typen:

| RT | Kardinalität | Attribute |
|----|------------|---------|
| **Besucht** (Student:In, Modul) | n:m | Semester |
| **Lehrt** (Dozent, Modul) | n:1 ● | Semester |
| **Prüft** (Dozent, Student:In, Modul) | n:m:n | Note, Versuch |
| **Forscht** (Dozent, Fachgebiet) | n:m | — |
| **Bietet_an** (Fachgebiet, Modul) | 1:n | — |
| **Gehört_zu** (Modul, Tutorium) | 1:n ● | — |

### Konsistenzprüfung mit Glossar

$$\text{Konsistenz}: ET + \text{Attr}[\text{Glossar}] = ET + \text{Attr}[\text{Modell}]$$

- **Vollständigkeit**: alle Anforderungen abgebildet
- **Nachverfolgbarkeit**: jede Anforderung im Modell auffindbar
- Werkzeug: **draw.io** für graphische Erstellung

---

## 7. Semantik der Grundkonzepte (Anhang)

### Mathematische Formalisierung

| Konzept | Mathematische Interpretation |
|--------|----------------------------|
| **Entity-Typ** $E$ | Menge $E = \{e_1, e_2, \ldots\}$ |
| **Relationship-Typ** $R(E_1, \ldots, E_n)$ | $n$-stellige Relation $R \subseteq E_1 \times \ldots \times E_n$ |
| **Entity-Attribut** $a$ zu $E$ | Abbildung $a : E \to \text{dom}(a)$ |
| **Relationship-Attribut** $a$ zu $R$ | Abbildung $a : E_1 \times \ldots \times E_n \to \text{dom}(a)$ |
| **Schlüsselattribut** | Injektive Abbildung: $e_1 \neq e_2 \Rightarrow a(e_1) \neq a(e_2)$ |

**Kartesisches Produkt:**

$$E_1 \times E_2 := \{(e_1, e_2) \mid (e_1 \in E_1) \land (e_2 \in E_2)\}$$

**Typische Wertebereiche:** $\mathbb{N}$, $\mathbb{Z}$, $\mathbb{Q}$, $\mathbb{R}$, Zeichenketten $\Sigma^*$ oder $\Sigma^+$

---

## 📌 Zusammenfassung der Schlüsselkonzepte

| Konzept | Erläuterung |
|--------|------------|
| **Konzeptionelles Modell** | Beschreibt Struktur der Daten aus Anwendersicht |
| **Entity-Typ** | Menge gleichartiger Objekte der realen oder Vorstellungswelt |
| **Relationship-Typ** | Menge gleichartiger Beziehungen zwischen Entity-Typen |
| **Attribut** | Modelliert Daten: atomar, abgeleitet, mengenwertig, strukturiert |
| **Lokale Integrität** | Schlüsseleinschränkung, Entitätsintegrität (Schlüssel ≠ null), Domänen |
| **Strukturelle Integrität** | Kardinalität (1:1, 1:n, n:1, n:m), Totalität, referentielle Integrität |
| **Integritätsbedingung** | Eigenschaft der Miniwelt — keine Eigenschaft von Daten! |
| **Schwacher Entity-Typ** | Kein eigener Schlüssel; nur partieller Schlüssel; existenzabhängig |

---

## ✅ Kernaussagen

- Das ER-Diagramm ist das **Standardmodell** für das konzeptionelle Schema (Chen 1976)
- Konzeptionelle Schemas sind **DBMS-unabhängig** — kein SQL, keine physische Struktur
- Integritätsbedingungen sind **keine Dateneigenschaften** — sie kommen aus der Semantik der Miniwelt
- Schwache Entity-Typen identifizieren sich **nur zusammen** mit dem starken Entity-Typ
- Mathematisch: Entity-Typ = Menge; Relationship-Typ = Relation; Attribut = Abbildung
- n-äre Relationship-Typen können stets in binäre umgewandelt werden (neuer Entity-Typ)

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.01 Einführung]]: DBMS-Architektur und Drei-Ebenen-Schema (Grundlage dieser VL)
- [[VL.03 Datenbankmodellierung II]]: Datenbankmodellierung II — EER-Modellierung, Abstraktionskonzepte
- [[VL.01 Mengen]]: Mengenlehre (Entity-Typen als Mengen, kartesisches Produkt)
- [[VL.02 Inferenz und Regelschemata]]: Prädikatenlogik (Formalisierung von Integritätsbedingungen mit $\forall$, $\exists$)
- [[VL.06 Relationen]]: Relationen als mathematische Grundlage für Relationship-Typen
- [[VL.07 Abbildunge Funktionen & Kardinalität]]: Funktionen als Grundlage für Attribut-Interpretationen
