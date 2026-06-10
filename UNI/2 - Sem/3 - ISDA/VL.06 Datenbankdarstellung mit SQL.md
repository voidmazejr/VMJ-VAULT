**Class:** [[ISDA - Informationsysteme und Datenanalyse]]  
**Date:** 18-05-2026  
**Topics:** #ISDA #Datenbanken #DDL #DML #SQL #Schema #Constraints #Trigger
**Link:** [[VL.06 ISDA.pdf]]

---

## 🎯 Lernziele der Vorlesung

In dieser Vorlesung geht es darum, wie relationale Datenbanken in SQL **definiert**, **strukturiert**, **abgesichert** und **mit Daten befüllt bzw. verändert** werden. Der Schwerpunkt liegt auf den Grundbausteinen der Datendefinitionssprache (DDL), der Datenmanipulationssprache (DML) und auf Integritätsmechanismen wie Constraints und Triggern.

- **Datenbankobjekte verstehen**: Datenbank, Schema, Tabelle, Schlüssel, Constraints, Trigger.
- **DDL-Befehle anwenden**: `CREATE SCHEMA`, `CREATE TABLE`, `DROP TABLE`, `ALTER TABLE`.
- **Datentypen und Default-Werte modellieren**: passende SQL-Typen auswählen und Standardwerte definieren.
- **Integrität absichern**: `PRIMARY KEY`, `FOREIGN KEY`, `NOT NULL`, `CHECK`, `ASSERTION`.
- **DML-Befehle anwenden**: `INSERT`, `DELETE`, `UPDATE`.
- **Trigger verstehen**: automatische Reaktionen auf Änderungen formulieren.
- **Unterschied DDL vs. DML sauber trennen**: Strukturdefinition vs. Datenänderung.
- **SQL-Konstrukte auf ein Universitätsbeispiel übertragen**: Tabellen und Beziehungen konkret modellieren.

---

## 1. Abschnitt: Datenbankobjekte & Grundlagen

### Definition: Datenbankobjekt

Ein Datenbankobjekt ist eine dauerhafte Struktur innerhalb einer Datenbank zur Speicherung, Verwaltung, Absicherung oder Präsentation von Daten.

$$\boxed{\text{Datenbankobjekt} = \text{permanentes Strukturelement einer Datenbank}}$$

**Wichtige Begriffe:**

- **Datenbank**: Enthält alle Datenbankobjekte und organisiert den effizienten Zugriff auf Daten.
- **Schema**: Logische Gruppierung von Datenbankobjekten innerhalb einer Datenbank.
- **Tabelle**: Speicherort für Daten in Form von Tupeln und Attributen.
- **View**: Logische Sicht auf Daten.
- **Index**: Hilfsstruktur für effizienten Zugriff.
- **Constraint**: Integritätsbedingung auf Daten.
- **Trigger**: Automatisch ausgeführte Prozedur bei Datenänderungen.

### Rolle von Datenbank, Schema und Tabelle

Eine **Datenbank** speichert Daten für eine oder mehrere Anwendungen und enthält Objekte wie Tabellen, Sichten, Trigger, Assertions, Procedures und Mechanismen zur Rechteverwaltung.

Ein **Schema** trennt Objekte logisch voneinander. Typisch ist, dass Benutzer standardmäßig ein eigenes Schema besitzen und Objekte zunächst dort erzeugen.

Eine **Tabelle** ist die relationale Grundstruktur zur Speicherung von Daten. Sie besitzt:

- ein festes Schema,
- Attribute mit Datentypen,
- Schlüsselattribute,
- optionale Nebenbedingungen wie Referenzen, Default-Werte oder Einzigartigkeit.

### Tabelle als Relation

$$\boxed{\text{Tabelle} = \text{Relation mit Attributen, Tupeln und Integritätsbedingungen}}$$

**Wichtige Begriffe:**

- **Attribut / Feld**: Spalte einer Tabelle.
- **Tupel / Datensatz**: Zeile einer Tabelle.
- **Primärschlüssel**: Eindeutige Identifikation eines Tupels.
- **Fremdschlüssel**: Verweis auf Tupel einer anderen Tabelle.

### Beispiel: Primär- und Fremdschlüssel

Angenommen, es gibt zwei Tabellen:

- `Person(Name, Geburtsdatum, Geburtsort)`
- `Ort(Ortname, Land)`

Dann kann gelten:

$$\boxed{\text{PK(Person)} = (Name, Geburtsdatum)}$$

$$\boxed{\text{PK(Ort)} = (Ortname)}$$

$$\boxed{\text{FK(Person.Geburtsort)} \rightarrow \text{Ort.Ortname}}$$


⚠️ **Achtung:** Ein Fremdschlüssel beschreibt keine bloße Namensähnlichkeit, sondern eine **referenzielle Bindung** an einen Schlüssel einer anderen Relation.

> 💡 **Merkhilfe:**  
> Der Primärschlüssel sagt: „**Wer bin ich?**“  
> Der Fremdschlüssel sagt: „**Zu wem gehöre ich?**“

---

## 2. Abschnitt: DDL – Schema, Datentypen und Tabellen

### Definition: DDL

Die Datendefinitionssprache beschreibt die **Struktur** der Datenbank, nicht die einzelnen Dateninhalte.

$$\boxed{\text{DDL} = \text{SQL-Befehle zur Definition und Änderung von Schemata und Relationen}}$$

**Typische DDL-Befehle:**

- `CREATE SCHEMA`
- `CREATE TABLE`
- `DROP SCHEMA`
- `DROP TABLE`
- `ALTER TABLE`

### CREATE SCHEMA

Mit `CREATE SCHEMA` wird ein SQL-Schema angelegt, das zusammengehörige Datenbankobjekte bündelt.

```sql
CREATE SCHEMA UNIVERSITÄT_DB
AUTHORIZATION JMUELLER;
```

**Bedeutung:**

- Das Schema hat einen **Namen**.
- Es besitzt einen **Autorisationsbezeichner**.
- Es enthält Deskriptoren für seine Objekte, z. B. Tabellen, Wertebereiche, Views und Constraints.

### Datentypen

Jedes Attribut muss in SQL einen Datentyp besitzen.

$$\boxed{\text{Attribut} \rightarrow \text{genau ein Datentyp}}$$

|Datentyp|Bedeutung|Beispiel|
|---|---|---|
|`CHAR(n)`|Zeichenkette fester Länge|Matrikelnummer fester Länge|
|`VARCHAR(n)`|Zeichenkette variabler Länge|Name, Titel|
|`BIT(n)` / `BIT VARYING(n)`|Bitfolge|Binärflags|
|`BOOLEAN`|`TRUE`, `FALSE`, `UNKNOWN`|Statuswerte|
|`INT`, `INTEGER`, `SMALLINT`|Ganzzahlen|Punkte, IDs|
|`FLOAT`, `REAL`, `DOUBLE PRECISION`|Fließkommazahlen|Messwerte|
|`DECIMAL(i,j)`|feste Präzision und Skala|Noten, Geld|
|`DATE`, `TIME`|Datum bzw. Uhrzeit|Prüfungsdatum|

⚠️ **Achtung:** Die Wahl des Datentyps ist Teil des Schemas und beeinflusst zulässige Werte, Speicherbedarf und Integrität.

### CREATE TABLE

Mit `CREATE TABLE` wird ein Relationenschema definiert. Die so erzeugten Relationen heißen **Basisrelationen**, da ihre Tupel tatsächlich vom DBMS verwaltet werden.

```sql
CREATE TABLE MODUL (
    MODNR CHAR(9) NOT NULL,
    TITEL_DES_MODULS VARCHAR(15),
    LEISTUNGSPUNKTE INT,
    PERSNR INT NOT NULL,
    SEMESTER CHAR(6),
    PRIMARY KEY (MODNR),
    FOREIGN KEY (PERSNR) REFERENCES DOZENT(PERSNR)
);
```

### Definition: Relationenschema

$$\boxed{R(A_1{:}T_1,\dots,A_n{:}T_n,\text{Constraints})}$$

Dabei ist:

- (R) der Tabellenname,
- (A_i) ein Attribut,
- (T_i) sein Datentyp.

### Beispiel: Universitätsdatenbank

Ein mögliches Schema der Anwendung `UNIVERSITÄT_DB` enthält u. a.:

- `Student(MatrNr, BenutzerID, Name, Vorname, BcSt, MsSt)`
- `Dozent(PersNr, Name, Vorname, Titel, FName)`
- `Modul(ModNr, Titel_des_Moduls, Leistungspunkte, PersNr, Semester)`
- `Prüft(PersNr, MatrNr, Note)`
- `Besucht(MatrNr, ModNr, Note, Semester, Versuch)`
- `Tutorium(ModNr, Nummer)`

### ALTER TABLE

Mit `ALTER TABLE` werden bestehende Tabellen geändert.

```sql
ALTER TABLE MODUL ADD MAX_PERSONEN INT;
```

```sql
ALTER TABLE MODUL DROP SEMESTER CASCADE;
```

```sql
ALTER TABLE MODUL ALTER LEISTUNGSPUNKTE DROP DEFAULT;
```

**Typische Operationen:**

- Spalte hinzufügen,
- Spalte entfernen,
- Default-Wert ändern oder entfernen.

### DROP TABLE und DROP SCHEMA

```sql
DROP TABLE MODUL CASCADE;
```

```sql
DROP SCHEMA UNIVERSITÄT_DB CASCADE;
```

### CASCADE vs. RESTRICT

|Option|Wirkung|
|---|---|
|`CASCADE`|Löscht abhängige Objekte oder referenzierende Definitionen mit.|
|`RESTRICT`|Löscht nur, wenn keine Abhängigkeiten bestehen.|

⚠️ **Achtung:** Beim Entfernen von Tabellen oder Spalten muss geprüft werden, ob Constraints, Views oder Referenzen betroffen sind.


---

## 3. Abschnitt: Integritätssicherung mit Constraints

### Definition: Integritätsbedingung

Integritätsbedingungen legen fest, welche Zustände einer Datenbank **zulässig** sind.

$$\boxed{\text{Integrität} = \text{Menge aller Bedingungen, die Daten erfüllen müssen}}$$

**Wichtige SQL-Konstrukte:**

- `PRIMARY KEY`
- `FOREIGN KEY ... REFERENCES ...`
- `NOT NULL`
- `CHECK`
- `CREATE ASSERTION`

### PRIMARY KEY

Ein Primärschlüssel besteht aus einem oder mehreren Attributen, die ein Tupel eindeutig identifizieren.

$$\boxed{\text{PRIMARY KEY} = \text{eindeutige Identifikation eines Tupels}}$$

```sql
CREATE TABLE Prüft (
    PersNr INT NOT NULL,
    MatrNr INT NOT NULL,
    Note DECIMAL(2,1) DEFAULT '0,0',
    PRIMARY KEY (PersNr, MatrNr)
);
```

**Eigenschaften:**

- eindeutig,
- keine `NULL`-Werte,
- kann aus mehreren Attributen bestehen.

⚠️ **Achtung:** Für Primärschlüsselattribute muss `NOT NULL` gelten.

### FOREIGN KEY ... REFERENCES ...

Ein Fremdschlüssel stellt referenzielle Integrität her.

$$\boxed{\text{FK}(A) \rightarrow \text{PK}(B)}$$

```sql
CREATE TABLE Prüft (
    PersNr INT NOT NULL,
    MatrNr INT NOT NULL,
    Note DECIMAL(2,1) DEFAULT '0,0',
    PRIMARY KEY (PersNr, MatrNr),
    FOREIGN KEY (PersNr) REFERENCES DOZENT(PERSNR),
    FOREIGN KEY (MatrNr) REFERENCES STUDENT(MATRNR)
);
```

**Bedeutung:**

- Ein Wert im Fremdschlüssel muss auf einen existierenden Wert der referenzierten Tabelle zeigen.
- Dadurch werden „verwaiste“ Referenzen verhindert.

### Referenz-Trigger-Aktionen

Beim Fremdschlüssel können automatische Reaktionen auf Änderungen definiert werden:

```sql
CREATE TABLE MODUL (
    MODNR CHAR(9) NOT NULL,
    TITEL_DES_MODULS VARCHAR(15),
    LEISTUNGSPUNKTE INT,
    PERSNR INT NOT NULL,
    SEMESTER CHAR(6),
    PRIMARY KEY (MODNR),
    FOREIGN KEY (PERSNR)
        REFERENCES DOZENT(PERSNR)
        ON DELETE CASCADE
        ON UPDATE CASCADE
);
```

**Bedeutung:**

- `ON DELETE CASCADE`: beim Löschen des referenzierten Tupels werden abhängige Tupel mitgelöscht.
- `ON UPDATE CASCADE`: Schlüsseländerungen propagieren auf referenzierende Tupel.

### NOT NULL

`NULL` ist in SQL grundsätzlich erlaubt, außer es wird explizit verboten.

$$\boxed{\text{NOT NULL} \Rightarrow \text{Attributwert darf nicht leer/unbekannt sein}}$$

**Wichtige Regel:**

- Ohne `DEFAULT` gilt als Standardwert meist `NULL`.
- Für Primärschlüsselattribute ist `NOT NULL` zwingend.

⚠️ **Achtung:** `NULL` bedeutet nicht 0, nicht leerer String und nicht „falsch“, sondern **unbekannt / nicht vorhanden**.

### CHECK – einfache Integritätsbedingungen

Mit `CHECK` werden zulässige Wertebereiche oder Prädikate formuliert.

```sql
CREATE TABLE Student (
    MatrNr INTEGER PRIMARY KEY,
    Name VARCHAR(30) NOT NULL,
    Semester INTEGER CHECK (Semester BETWEEN 1 AND 13)
);
```

```sql
CREATE TABLE Professor (
    PersNr INTEGER PRIMARY KEY,
    Name VARCHAR(30) NOT NULL,
    Rang CHARACTER(2) CHECK (Rang IN ('W1','W2','W3')),
    Raum INTEGER UNIQUE
);
```

### CHECK – komplexe Integritätsbedingungen

Auch komplexere Bedingungen über mehrere Tabellen sind konzeptionell möglich.

```sql
CREATE TABLE Prüfung (
    PersNr INT NOT NULL,
    ModNr CHAR(9),
    MatrNr INT NOT NULL,
    Note DECIMAL(2,1) CHECK (Note BETWEEN 0.0 AND 5.0) DEFAULT '0,0',
    PRIMARY KEY (PersNr, MatrNr),
    FOREIGN KEY (PersNr) REFERENCES DOZENT(PERSNR),
    FOREIGN KEY (MatrNr) REFERENCES STUDENT(MATRNR),
    CONSTRAINT VORHER_HÖREN
    CHECK (
        EXISTS (
            SELECT *
            FROM Besucht b
            WHERE b.ModNr = Prüfung.ModNr
              AND b.MatrNr = Prüfung.MatrNr
        )
    )
);
```

**Idee:** Studierende dürfen nur über Module geprüft werden, die sie zuvor besucht haben.

⚠️ **Achtung:** Solche komplexen `CHECK`-Constraints werden in vielen DBMS nur eingeschränkt oder gar nicht unterstützt.

### ASSERTION

Assertions sind eigenständige Datenbankobjekte, nicht bloß Bestandteile einer Tabelle.

$$\boxed{\text{Assertion} = \text{globale benannte Integritätsbedingung}}$$

```sql
CREATE ASSERTION assertion_name
CHECK (condition);
```

```sql
DROP ASSERTION assertion_name;
```

**Beispiel:**

```sql
CREATE ASSERTION age_assertion
CHECK (age >= 18);
```

### Vergleich der Integritätsmechanismen

|Mechanismus|Geltungsbereich|Typischer Einsatz|Bemerkung|
|---|---|---|---|
|`NOT NULL`|einzelne Spalte|Pflichtfeld|sehr einfach|
|`PRIMARY KEY`|Tabelle|eindeutige Identifikation|impliziert Eindeutigkeit|
|`FOREIGN KEY`|zwischen Tabellen|referenzielle Integrität|wichtig für Joins|
|`CHECK`|Tabelle / Zeile|Wertebereich, Prädikate|teils eingeschränkte Unterstützung|
|`ASSERTION`|datenbankweit|globale Bedingungen|in vielen DBMS nicht implementiert|

---

## 4. Abschnitt: DML – Einfügen, Löschen und Ändern

### Definition: DML

Die Datenmanipulationssprache verändert die **Inhalte** der Tabellen.

$$\boxed{\text{DML} = \text{SQL-Befehle zur Änderung von Tupeln}}$$

**Grundoperationen:**

- `INSERT`
- `DELETE`
- `UPDATE`

### INSERT

```sql
INSERT INTO R(A1, ..., An) VALUES (v1, ..., vn);
```

**Regeln:**

- Werden alle Attribute gesetzt, muss die Reihenfolge der Schemaspezifikation entsprechen.
- Werden Attribute ausgelassen, erhalten sie ihren `DEFAULT`-Wert oder `NULL`.

### Beispiele für INSERT

```sql
INSERT INTO Dozent
VALUES ('33344455', 'Schmidt', 'Johann', 'Professor', 'DBS');
```

```sql
INSERT INTO Dozent (Name, Vorname)
VALUES ('Weber', 'Sophia');
```

### Schritt-für-Schritt Beispiel: INSERT

```text
Ausgangszustand:
Dozent = ∅

Schritt 1: Füge vollständiges Tupel ein
          Dozent → ('33344455', 'Schmidt', 'Johann', 'Professor', 'DBS')

Schritt 2: Füge partielles Tupel ein
          Angegeben: (Name, Vorname) = ('Weber', 'Sophia')
          Nicht gesetzte Attribute → DEFAULT oder NULL

✅ Ergebnis:
Die Tabelle enthält beide Tupel; fehlende Werte werden automatisch ergänzt.
```

⚠️ **Achtung:** Ein `INSERT` schlägt fehl, wenn Primärschlüssel verletzt oder Fremdschlüsselreferenzen nicht erfüllt werden.

### DELETE

```sql
DELETE FROM R WHERE Bedingung;
```

**Bedeutung:**

- Es werden alle Tupel gelöscht, für die die Bedingung wahr ist.
- Ohne `WHERE` werden **alle** Tupel der Tabelle gelöscht.

**Beispiele:**

```sql
DELETE FROM Dozent
WHERE NAME = 'Brown';
```

```sql
DELETE FROM Dozent
WHERE PersNr = '33344455';
```

```sql
DELETE FROM Dozent;
```

### Schritt-für-Schritt Beispiel: DELETE

```text
Ausgangszustand:
Dozent = {d1, d2, d3}

Schritt 1: DELETE ... WHERE NAME = 'Brown'
          Falls Brown nicht existiert → keine Änderung

Schritt 2: DELETE ... WHERE PersNr = '33344455'
          Genau ein Tupel mit dieser Schlüssel-ID wird gelöscht

Schritt 3: DELETE FROM Dozent
          Alle verbleibenden Tupel werden entfernt

✅ Ergebnis:
Tabelle ist leer.
```

### UPDATE

```sql
UPDATE R
SET A1 = Ausdruck1, A2 = Ausdruck2
WHERE Bedingung;
```

**Beispiel:**

```sql
UPDATE Dozent
SET Gehalt = '6000',
    Name = 'Dr. ' || Name
WHERE PersNr = '33344455';
```

**Bedeutung:**

- Mit einem `UPDATE` können mehrere Attribute gleichzeitig geändert werden.
- Auch mehrere Tupel können betroffen sein, wenn die `WHERE`-Bedingung mehrere Zeilen trifft.

### Schritt-für-Schritt Beispiel: UPDATE

```text
Ausgangszustand:
Dozent(PersNr='33344455', Name='Schmidt', Gehalt='5000')

Schritt 1: Suche Tupel mit PersNr = '33344455'
          Treffer → genau ein Tupel

Schritt 2: Setze Gehalt auf '6000'
          Zustand → Gehalt='6000'

Schritt 3: Ergänze Präfix 'Dr. ' vor Name
          Zustand → Name='Dr. Schmidt'

✅ Ergebnis:
Dozent(PersNr='33344455', Name='Dr. Schmidt', Gehalt='6000')
```

### LIKE und Wildcards

`LIKE` wird in `WHERE`-Klauseln für Mustersuche verwendet.

$$\boxed{\text{LIKE} = \text{Mustervergleich auf Zeichenketten}}$$

**Wildcards:**

- `%` : beliebig viele Zeichen, auch 0
- `_` : genau ein Zeichen

**Beispiele:**

```sql
SELECT Name
FROM Dozent
WHERE Name LIKE 'Alex%';
```

```sql
SELECT Name
FROM Dozent
WHERE Name LIKE '_im';
```

### Piecewise-Darstellung der Wildcards

$$ \text{Match}(p,s)= \begin{cases} \text{wahr} & \text{falls } s \text{ zum Muster } p \text{ passt} \ \text{falsch} & \text{sonst} \end{cases} $$

|Muster|Bedeutung|Beispieltreffer|
|---|---|---|
|`Alex%`|beginnt mit `Alex`|Alex, Alexis, Alexa|
|`_im`|genau 3 Zeichen, endet auf `im`|Kim, Tim, Jim|

---

## 5. Abschnitt: Trigger, Beispiele und Überblick

### Definition: Trigger

Ein Trigger ist eine in der Datenbank gespeicherte Prozedur, die automatisch durch ein bestimmtes Änderungsereignis ausgelöst wird.

$$\boxed{\text{Trigger} = \text{automatische Reaktion auf INSERT, UPDATE oder DELETE}}$$

**Rolle:**

- Integrität sichern,
- Folgeaktionen ausführen,
- abgeleitete Werte automatisch berechnen,
- referenzielle Konsistenz ergänzend absichern.

### Allgemeiner Aufbau

```sql
CREATE TRIGGER Trigger_Name
(BEFORE | AFTER) [INSERT | UPDATE | DELETE]
ON [Table_Name]
[FOR EACH ROW | FOR EACH COLUMN]
[trigger_body]
```

### Bestandteile

|Bestandteil|Bedeutung|
|---|---|
|`Trigger_Name`|eindeutiger Name im Schema|
|`BEFORE` / `AFTER`|Zeitpunkt vor bzw. nach dem auslösenden Ereignis|
|`INSERT` / `UPDATE` / `DELETE`|auslösendes Ereignis|
|`ON Table_Name`|Basistabelle, auf der der Trigger definiert ist|
|`FOR EACH ROW`|zeilenorientierte Ausführung|
|`trigger_body`|auszuführende Logik|

⚠️ **Achtung:** Trigger werden auf **Basistabellen** definiert, nicht auf Views oder temporären Tabellen.

### Beispiel I: Automatisches Löschen zugehöriger Tutorien

Wenn ein Modul gelöscht wird, sollen seine Tutorien ebenfalls gelöscht werden.

```sql
CREATE TRIGGER delete_tutorium
AFTER DELETE
ON Modul
FOR EACH ROW
BEGIN
    DELETE FROM Tutorium
    WHERE ModNr.Modul = ModNr.Tutorium;
END;
```

### Pseudocode: Trigger-Idee

```pseudocode
Trigger delete_tutorium(nach Löschung eines Moduls):
1. Für jede gelöschte Modul-Zeile:
2.     Suche alle Tutorium-Zeilen mit derselben ModNr
3.     Lösche diese Tutorium-Zeilen
4. Ende
```

### Schritt-für-Schritt Beispiel

```text
Ausgangszustand:
Modul enthält ModNr = M123
Tutorium enthält (M123, 1), (M123, 2), (M777, 1)

Schritt 1: DELETE FROM Modul WHERE ModNr = 'M123'
          Modul M123 wird gelöscht

Schritt 2: AFTER DELETE Trigger feuert
          Suche Tutorium-Zeilen mit ModNr = M123

Schritt 3: Lösche passende Tutorien
          Entfernt: (M123, 1), (M123, 2)

✅ Ergebnis:
Nur Tutorium (M777, 1) bleibt erhalten.
```

### Beispiel II: Automatische Berechnung einer Gesamtpunktzahl

Die Tabelle `BESUCHT` wird um Portfolio-Spalten erweitert:

```sql
ALTER TABLE BESUCHT
ADD DATENBANKERSTELLUNG DEC(4,2),
ADD DATENBANKABFRAGE DEC(4,2),
ADD PROGRAMMIERAUFGABE DEC(4,2),
ADD SCHRIFTLICHER_TEST DEC(4,2),
ADD GESAMT DEC(5,2);
```

Dann wird die Gesamtsumme vor dem Einfügen berechnet:

```sql
CREATE TRIGGER TOTAL
BEFORE INSERT
ON BESUCHT
FOR EACH ROW
SET new.GESAMT =
    new.DATENBANKERSTELLUNG +
    new.DATENBANKABFRAGE +
    new.PROGRAMMIERAUFGABE +
    new.SCHRIFTLICHER_TEST;
```

### Pseudocode: Summenberechnung

```pseudocode
Trigger TOTAL(vor Einfügen in BESUCHT):
1. Lese neue Teilpunktzahlen
2. Berechne Summe:
3.     GESAMT := DBERSTELLUNG + DBABFRAGE + PROGRAMMIERAUFGABE + TEST
4. Schreibe GESAMT in das neue Tupel
5. Füge Tupel ein
```

### Schritt-für-Schritt Beispiel

```text
Ausgangszustand:
Neues Tupel soll eingefügt werden mit:
DATENBANKERSTELLUNG = 20.00
DATENBANKABFRAGE    = 18.50
PROGRAMMIERAUFGABE  = 22.00
SCHRIFTLICHER_TEST  = 15.00

Schritt 1: BEFORE INSERT Trigger wird aktiviert

Schritt 2: Berechnung
          GESAMT = 20.00 + 18.50 + 22.00 + 15.00
                 = 75.50

Schritt 3: Tupel wird mit GESAMT = 75.50 eingefügt

✅ Ergebnis:
Die Gesamtpunktzahl ist automatisch konsistent berechnet.
```

### Laufzeitanalyse

Da in der Vorlesung keine formale Komplexitätsanalyse von SQL-Operationen entwickelt wird, ist hier vor allem die **operationelle** Sicht wichtig:

|Operation|Typische logische Kosten|Bemerkung|
|---|---|---|
|`INSERT` eines Tupels|(O(1)) bis Zugriff auf Indizes/Constraints|Integritätsprüfung kann Zusatzkosten verursachen|
|`DELETE` mit `WHERE`|abhängig von Suchbedingung|ohne Index oft linear|
|`UPDATE` mit `WHERE`|Suche + Änderung|kann mehrere Tupel betreffen|
|Trigger pro Zeile|Zusatzkosten pro betroffenem Tupel|bei `FOR EACH ROW` mehrfach|
|Fremdschlüsselprüfung|zusätzlicher Lookup|referenzielle Integrität kostet Prüfaufwand|

⚠️ **Achtung:** Die reale Laufzeit hängt stark von Indizes, Tabellenumfang, Optimizer und Implementierung des DBMS ab.

### Schleifeninvariante / Korrektheitsidee bei Trigger-Summenbildung

Obwohl SQL-Trigger keine klassische Schleife enthalten, kann man die Korrektheit des zweiten Triggers durch eine Invariante der Berechnungsidee beschreiben:

$$\boxed{\text{Nach der Triggerausführung gilt: } \text{GESAMT} = \sum \text{aller Teilpunkte}}$$

**Korrektheitsargument:**

- **Anfang:** Vor dem Einfügen liegt ein neues Tupel mit vier Teilwerten vor.
- **Voraussetzung:** Diese vier Werte sind die vollständigen Komponenten der Gesamtpunktzahl.
- **Schritt:** Der Trigger setzt `new.GESAMT` exakt auf deren Summe.
- **Ergebnis:** Das eingefügte Tupel erfüllt die gewünschte Konsistenzbedingung.

✅ **Korrekt:** `GESAMT` wird aus allen Teilwerten neu berechnet.  
❌ **Falsch:** `GESAMT` manuell pflegen und hoffen, dass es später zu den Teilpunkten passt.

---

## 6. Abschnitt: Gesamtüberblick, Einordnung und Verbindungen

### DDL vs. DML

$$\boxed{\text{DDL beschreibt die Struktur, DML verändert die Inhalte}}$$

|Bereich|Zweck|Typische Befehle|
|---|---|---|
|**DDL**|Schema und Relationen definieren/ändern|`CREATE`, `DROP`, `ALTER`|
|**DML**|Tupel einfügen, löschen, ändern|`INSERT`, `DELETE`, `UPDATE`|

### Zentrale Unterscheidung

- **DDL** beantwortet die Frage: _Wie ist die Datenbank aufgebaut?_
- **DML** beantwortet die Frage: _Welche Daten stehen aktuell in ihr?_

### ASCII-Diagramm: Einordnung der Vorlesung

```text
                 SQL
                  │
      ┌───────────┴───────────┐
      │                       │
      ▼                       ▼
     DDL                     DML
      │                       │
      ├─ CREATE SCHEMA        ├─ INSERT
      ├─ CREATE TABLE         ├─ DELETE
      ├─ ALTER TABLE          └─ UPDATE
      └─ DROP TABLE
                  │
                  ▼
        Integrität & Automatisierung
                  │
          ├─ PRIMARY KEY
          ├─ FOREIGN KEY
          ├─ NOT NULL
          ├─ CHECK / ASSERTION
          └─ TRIGGER
```

### Beispielhafter Gesamtablauf

```pseudocode
Datenbank_entwerfen_und_nutzen():
1. Erzeuge Schema
2. Definiere Tabellen mit Datentypen
3. Ergänze Schlüssel und Constraints
4. Füge Daten ein
5. Ändere oder lösche Daten bei Bedarf
6. Verwende Trigger für automatische Reaktionen
7. Prüfe Integrität fortlaufend
```

### Anwendungsbeispiel aus der Praxis

**Aufgabe:** Ein Universitätsverwaltungssystem soll Studierende, Dozierende, Module, Prüfungen und Tutorien korrekt verwalten.  
**Zeitkomplexität:** abhängig von Anfrage, Indizes und Constraints; logisch besteht der Ablauf aus Schemaentwurf + Integritätssicherung + DML-Operationen.

**Pseudocode:**

```text
1. Definiere Relationen Student, Dozent, Modul, Prüft, Besucht, Tutorium
2. Lege Primär- und Fremdschlüssel fest
3. Ergänze CHECK- und NOT-NULL-Bedingungen
4. Füge Personen, Module und Belegungen ein
5. Nutze Trigger für automatische Folgeaktionen
```

> 💡 **Merkhilfe:**  
> Erst **Form bauen** (DDL), dann **Inhalt einfüllen** (DML), dann **Regeln automatisch überwachen** (Constraints + Trigger).

---

## 📌 Zusammenfassung

### Wichtige Konzepte

|Konzept|Bedeutung|
|---|---|
|**Datenbankobjekt**|Permanentes Element der Datenbank, z. B. Tabelle, Schema, View, Trigger|
|**Schema**|Logische Gruppierung zusammengehöriger Datenbankobjekte|
|**Tabelle**|Relation zur Speicherung von Tupeln und Attributen|
|**DDL**|Sprache zur Definition und Änderung der Datenbankstruktur|
|**DML**|Sprache zur Manipulation von Dateninhalten|
|**Primärschlüssel**|Eindeutige Identifikation eines Tupels|
|**Fremdschlüssel**|Referenz auf Schlüssel einer anderen Tabelle|
|**Constraint**|Bedingung, die gültige Daten beschreibt|
|**Assertion**|Globale, benannte Integritätsbedingung|
|**Trigger**|Automatische Reaktion auf Datenänderungen|

### Kernaussagen

✅ **DDL und DML haben verschiedene Rollen** – DDL formt die Struktur, DML verändert Tupel.  
✅ **Integrität ist zentral** – Schlüssel, `NOT NULL`, `CHECK`, Assertions und Trigger schützen die Konsistenz.  
✅ **Tabellen sind Relationen mit Datentypen und Nebenbedingungen** – nicht nur einfache Datensammlungen.  
✅ **Fremdschlüssel modellieren Beziehungen zwischen Tabellen** – sie sichern referenzielle Integrität.  
✅ **Trigger automatisieren Folgeaktionen** – etwa Kaskadenlöschungen oder Summenberechnungen.  
⚠️ **Achtung:** Komplexe `CHECK`-Constraints und Assertions sind in realen DBMS oft nur eingeschränkt implementiert.  
❌ **Falsch:** DDL und DML gleichsetzen oder annehmen, dass fehlende Werte ohne `DEFAULT` automatisch sinnvoll belegt sind.

### Wichtige Algorithmen / Formeln

|Algorithmus / Konstrukt|Laufzeit|Anwendung|
|---|---|---|
|**CREATE TABLE**|abhängig vom DBMS, logisch einmalig|Strukturdefinition|
|**INSERT**|typ. klein pro Tupel, plus Constraint-Prüfungen|Dateneinfügen|
|**DELETE**|abhängig von Suchbedingung und Indizes|Tupel entfernen|
|**UPDATE**|Suche + Änderung|bestehende Tupel verändern|
|**Trigger TOTAL**|proportional zur Anzahl berechneter Felder|automatische Summenbildung|

### Zentrale Formeln und Definitionen

$$\boxed{\text{DDL} = \text{Definition und Änderung von Schemata/Relationen}}$$

$$\boxed{\text{DML} = \text{Manipulation von Dateninhalten}}$$

$$\boxed{\text{PRIMARY KEY} = \text{eindeutige Identifikation eines Tupels}}$$

$$\boxed{\text{FOREIGN KEY} \Rightarrow \text{referenzielle Integrität zwischen Tabellen}}$$

$$\boxed{\text{Trigger} = \text{automatische Aktion bei INSERT, UPDATE oder DELETE}}$$

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.05 Relationale Entwurfstheorie]]: Die heutige Vorlesung setzt auf gut entworfenen Relationen, Schlüsseln und funktionalen Abhängigkeiten auf.
- [[VL.06 Datenbankdarstellung mit SQL]]: Constraints konkretisieren die inhaltlichen Integritätsregeln nun direkt in SQL.
- [[VL.07 Relationale Algebra]]: Nach dem Erzeugen und Befüllen der Datenbank folgt als nächster Schritt die formale Anfrage auf Relationen.
