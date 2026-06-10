**Class:** [[ISDA - Informationsysteme und Datenanalyse]]
**Date:** 14-04-2026
**Topics:** #Einführung #Daten #Informationen #Datenbank #Informationssystem #Datenmodell #DreiSchichtenArchitektur #DBMS #Datenanalyse #DataScience
**Link:** [[VL.01 ISDA.pdf]]
 
---

## 🎯 Lernziele der Vorlesung

VL.01 führt in **Informationssysteme und Datenanalyse** ein und erklärt, wie reale Probleme in Daten, Modelle und Analysen überführt werden.

- Unterschied zwischen **Daten**, **Informationen**, **Wissen** und **Handeln**
- Einordnung von **Datenbank**, **DBMS**, **Datenbanksystem** und **Informationssystem**
- **Problem-Lösung-Zyklus** als Leitmodell der Vorlesung
- Überblick über die **Drei-Schichten-Architektur**
- Rolle von **Datenanalyse**, **Data Warehousing**, **Data Streams** und **Data Science**
- Aufbau der Vorlesung und empfohlene Literatur

---

## 1. Warum ISDA?

Die Vorlesung betont, dass Zahlen nicht „für sich selbst sprechen" — erst durch Interpretation werden sie zu Information. Ein typisches Motiv ist die Frage: *Wie viele Bäume gibt es auf dem Planeten?* Daraus wird klar, dass man zuerst Begriffe definieren muss, bevor man Daten sinnvoll erheben kann.

Der zentrale Gedanke ist der **Problem-Lösung-Zyklus**:

```
Problem → Verständnis/Definition → Plan → Datenerfassung → Analyse → Interpretation → neue Ideen
```

Die Vorlesung betrachtet Datenbanken und Informationssysteme aus Anwendersicht und ordnet die Themen entlang dieses Zyklus.

---

## 2. Daten und Informationen

### Definitionen

| Begriff | Bedeutung |
|--------|----------|
| **Daten** | Sammlungen von Zeichen oder Zeichenketten, deren Aufbau syntaktischen Regeln folgt |
| **Informationen** | Daten, die mit einer Bedeutung verknüpft und in einem Kontext interpretiert werden |
| **Wissen** | interpretierte Information, die als Entscheidungsgrundlage dient |
| **Handeln** | zielgerichtete Aktion auf Basis von Wissen |

### Kernaussage

Daten allein sind noch nicht nützlich. Erst durch einen **Bedeutungskontext** werden sie zu Information. Das Beispiel „Informationssystem" zeigt: Dieselbe Zeichenkette kann je nach Kontext völlig verschiedene Bedeutung haben.

### DIKW-Pyramide

```
Daten → Informationen → Wissen → Handeln
```

- **Datenanalyse** extrahiert Informationen aus Daten.
- **Wissen** entsteht durch Interpretation.
- **Data Science** zielt darauf, diese Wissensgenerierung datengetrieben zu optimieren.

---

## 3. Datenbank und Informationssystem

### Datenbank

Eine Datenbank ist eine organisierte Sammlung strukturierter Daten, die elektronisch gespeichert sind und einen Ausschnitt der realen Welt beschreiben.

### Informationssystem

Ein Informationssystem ist ein **soziotechnisches System**, das die Informationsnachfrage von Menschen oder anderen Systemen deckt. Es ist ein Mensch/Aufgabe/Technik-System, das Daten verarbeitet und dadurch Informationen bereitstellt.

### Unterschiede

| Begriff | Fokus |
|--------|-------|
| **DB** | Daten als Sammlung |
| **DBMS** | Software zur Verwaltung und Pflege der Datenbank |
| **DBS** | Datenbank plus DBMS |
| **IS** | Gesamt-System aus Technik, Menschen und Aufgaben |

### Datenbankmerkmale

- Datenbank beschreibt eine **Miniwelt** oder ein **Universe of Discourse (UoD)**
- Die Daten sind logisch zusammenhängend und haben eine bestimmte Bedeutung
- Datenbanken werden für einen bestimmten Zweck entworfen und von einer bestimmten Benutzergruppe genutzt
- Änderungen in der Miniwelt spiegeln sich in der Datenbank wider

---

## 4. Was ist ein Datenmodell?

Ein Datenmodell ist eine visuelle Darstellung der Datenelemente einer Anwendung und ihrer Verbindungen. Es hilft, Struktur und Zusammenhang von Daten explizit festzulegen.

ISDA betrachtet hier vor allem das **relationale Datenmodell**. Andere Modelle wie hierarchische oder objektorientierte Modelle werden nur kurz erwähnt.

### Bedeutung von Datenmodellen

- unterstützen die Datenbankmodellierung
- machen Struktur und Beziehungen sichtbar
- bilden die Grundlage für spätere Schema-Entwürfe

---

## 5. Architektur von DBMS

### Architekturübersicht

Ein DBMS besteht aus mehreren Komponenten:

- **Anfragebearbeitung**
- **Schemaverwaltung** 
- **Dateiverwaltung**
- **Datenbankmanager**
- **Mehrbenutzersynchronisation**
- **Fehlerbehandlung**
- **Datenbasis**, **Indexe**, **Logdateien**, **Datenwörterbuch**

### Einbettung

Die Datenbank ist die **primäre Ressource**, das DBMS die **sekundäre Ressource**. Zusammen bilden sie das **Datenbanksystem (DBS)**.

### Drei-Schichten-Architektur

Die Architektur trennt Anwendungen von Speicherdetails und unterstützt die Datenunabhängigkeit.

| Schicht | Aufgabe |
|--------|--------|
| **Externe Schicht** | Benutzersichten auf die Daten |
| **Konzeptionelle Schicht** | stabiles, anwendungsbezogenes Schema |
| **Interne Schicht** | Speicherung, Zugriffswege, physische Organisation |

### Datenunabhängigkeit

- **Physische Datenunabhängigkeit**: Speicheränderungen beeinflussen Anwendungen nicht
- **Logische Datenunabhängigkeit**: Schemaänderungen beeinflussen Sichten nicht

---

## 6. Zielgruppen der Vorlesung

Die Vorlesung unterscheidet mehrere Rollen im Umfeld von ISDA:

| Rolle | Aufgabe |
|------|--------|
| **Datenbank-Administrator** | Betrieb und Pflege |
| **Datenbank-Architekt** | Modellierung und Entwurf |
| **Systemanalytiker** | Anforderungen und Problemverständnis |
| **Data Analyst / Data Scientist** | Analyse und Auswertung |
| **Anwendungsprogrammierer** | Umsetzung von Anwendungen |
| **Endbenutzer** | Nutzung des Systems |
| **DBMS-Designer** | Entwurf von DBMS-Software |
| **Werkzeug-Entwickler** | Entwicklung von Tools |

---

## 7. Das Semester

### Thematischer Verlauf

Die Vorlesung folgt einem typischen Weg von der Modellierung bis zur Analyse:

- Datenbankmodellierung
- Relationaler Entwurf
- SQL
- Data Warehousing
- Relationale Algebra
- Data Streams
- Data Science

### Beispielanwendungen

- Firmendatenbanken
- Filmdatenbanken
- Universitätsdatenbanken
- Reiseverwaltungssysteme
- Projektmanagementsysteme

### Projektmanagement als Beispiel

Projektmanagement dient als konkrete Anwendung, um Datenmanagement- und Datenanalyseprobleme zu verstehen:
- Miniwelt festlegen
- konzeptionelles Schema entwickeln
- Datenbankschema ableiten
- Qualität prüfen
- Anfragen formulieren

---

## 8. Datenanalyse und Data Science

### Datenanalyse

Datenanalyse extrahiert Informationen aus Daten mit mathematischen bzw. statistischen Verfahren.

| Art | Ziel |
|----|------|
| **deskriptiv** | Daten beschreiben |
| **explorativ** | Muster und Zusammenhänge entdecken |
| **inferenziell / prädiktiv** | von Stichprobe auf Nichtbeobachtetes schließen |

### Data Warehousing

Ein Data Warehouse ist eine themenorientierte, integrierte, nichtflüchtige und zeitvariable Datensammlung zur Unterstützung von Managemententscheidungen.

- basiert auf historischen Daten
- nutzt oft **OLAP**
- dient analytischen Fragestellungen

### Data Streams

Datenströme sind unbeschränkte, fortlaufende Datenmengen. Die Herausforderung ist, sie mit diskretisierenden und zusammenfassenden Verfahren effizient auszuwerten.

### Data Science

Data Science beschäftigt sich mit der exakten digitalen Erfassung, Analyse und Visualisierung vergangener, aktueller und zukünftiger Phänomene, um Wissensgenerierung datengetrieben zu optimieren.

---

## 📌 Zusammenfassung

### Schlüsselkonzepte

| Konzept | Erläuterung |
|--------|------------|
| **Daten** | syntaktisch strukturierte Zeichenketten |
| **Informationen** | Daten mit Bedeutung |
| **Datenbank** | strukturierte, gespeicherte Daten über einen Ausschnitt der Welt |
| **DBMS** | Software zur Verwaltung einer Datenbank |
| **DBS** | Datenbank + DBMS |
| **Informationssystem** | soziotechnisches System zur Informationsbereitstellung |
| **Datenanalyse** | Extraktion von Informationen aus Daten |
| **Datenmodell** | Struktur und Beziehungen von Daten |
| **Drei-Schichten-Architektur** | externe, konzeptionelle, interne Ebene |

### Kernaussagen

✅ Daten werden erst durch Interpretation zu Information.

✅ Der Problem-Lösung-Zyklus ist das Grundmuster der Vorlesung.

✅ Datenbank, DBMS und Informationssystem sind nicht dasselbe, sondern unterschiedliche Ebenen.

✅ Die Drei-Schichten-Architektur erklärt und unterstützt Datenunabhängigkeit.

✅ Data Science und Data Warehousing bauen auf den Grundlagen der Datenmodellierung auf.

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Datenbankmodellierung]]: Datenbankmodellierung I — ER-Diagramme und Miniwelt
- [[VL.03 Datenbankmodellierung II]]: Datenbankmodellierung II — EER und komplexe Modelle
- [[FoG - Formal-mathematische Grundlagen]]: Mengen, Relationen und Prädikatenlogik als mathematische Grundlage
- [[SysProg - Systemprogrammierung]]: Datenhaltung, Speicherhierarchien und Betriebssystem-Grundlagen
