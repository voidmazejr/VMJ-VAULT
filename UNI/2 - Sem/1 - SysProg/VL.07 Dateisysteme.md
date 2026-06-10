**Class:** [[SysProg - Systemprogrammierung]]  
**Date:** 01-06-2026  
**Topics:** #Dateisysteme #Inodes #Journaling #SSD #Backup  
**Link:** [[VL.07 SysProg.pdf]]

***

## 🎯 Lernziele der Vorlesung

Diese Vorlesung behandelt **Dateisysteme**: ihre Struktur, Implementierung und Zuverlässigkeitsmechanismen auf modernen Speichermedien.

- **Dateisystem-Grundlagen**: Datei, Verzeichnis, Partition, Mounting, Links
- **Blockzuordnung**: Zusammenhängende Belegung, verkettete Listen (intern/extern), Indexblöcke, Inodes, Extents
- **SSD-Verwaltung**: FTL, Garbage Collection, TRIM, Wear Leveling
- **Konsistenz & Journaling**: Inkonsistenzarten, fsck, Log-basierte Dateisysteme
- **Backup**: Vollständige vs. inkrementelle Sicherung, physische vs. logische Datensicherung

***

## 1. Einführung: Grundbegriffe

### Definitionen

$$\boxed{\text{Datei} = \text{Sammlung von Daten auf stabilem Speicher unter einem gewählten Namen}}$$

$$\boxed{\text{Dateisystem} = \text{enthält einen Verzeichnisbaum; definiert max. Dateinamenlänge, max. Dateigröße, Abstraktions-Algorithmus}}$$

**Wichtige Begriffe:**
- **Datei (file)**: Sammlung von Daten auf persistentem Speicher
- **Verzeichnis (directory/folder)**: Enthält Dateien und andere Verzeichnisse → Baumstruktur
- **Dateisystem (filesystem)**: Enthält einen Verzeichnisbaum; Typ definiert allgemeine Charakteristika
- **Partition**: Zusammenhängende Menge von Blöcken einer Festplatte, die ein Dateisystem enthalten kann
- **Festplatte**: Persistentes Speichermedium – heute meist SSD (Flash) oder HDD (Magnet)

### Dateiattribute

| Attribut | Beschreibung |
|---|---|
| **Name** | Benutzervergebener Name + Dateierweiterung (Typ/Format-Hinweis) |
| **Bezeichner** | Eindeutige numerische Kennung im Dateisystem |
| **Typ** | UNIX: reguläre Datei, Link, Gerätedatei, Pipe, Socket, … |
| **Position** | Blockadresse(n) in der Partition |
| **Größe** | Aktuelle Dateigröße |
| **Zugriffsrechte** | Lesen / Schreiben / Ausführen pro Benutzer |
| **Zeitpunkte** | Erstellung, letzter Zugriff, letzte Modifikation |

### Ausführbare Programmdateitypen

- **Stapelverarbeitungsdatei (Shell-Script)**:
  - Erste Zeile: **Shebang** (`#!`), gefolgt vom Interpreter-Pfad
  - Beispiel: `#!/bin/sh`

```bash
#!/bin/sh
set -e
cd /tmp
wget https://www.stw.berlin/assets/speiseplaene/321/aktuelle_woche_de.pdf
evince aktuelle_woche_de.pdf
rm aktuelle_woche_de.pdf
exit 0
```

- **Kompiliertes Programm (ELF Binary unter Linux)**:
  - Erste 4 Bytes: **Magic Number** zur Typ-Identifikation
  - Header = "Inhaltsverzeichnis": Beginn/Größe von Code ("Text"), Daten, Einstiegspunkt (virtuelle Adresse der ersten Instruktion)
  - Inhalte: Code, Daten, Symboltabelle, Bibliotheksabhängigkeiten

> [!info] **Merkhilfe:** Shebang = „Zeig dem Kernel, wer dieses Skript ausführen soll." Magic Number = „Zeig dem Kernel, dass dies ein ELF-Binary ist."

***

## 2. Verzeichnisbaum, Pfade & Mounting

### Verzeichnisbaum

- **Hierarchische Organisation** → Sicherheit (Zugriffsrechte) + Komfort (eindeutige Namen pro Benutzer)
- **Absoluter Pfad**: Weg vom Wurzel-Verzeichnis `/` → z.B. `/home/alice/foo.txt`
- **Relativer Pfad**: Weg vom aktuellen Arbeitsverzeichnis → z.B. `../bob/foo.txt`

| Symbol | Bedeutung |
|---|---|
| `.` | Aktuelles Verzeichnis |
| `..` | Übergeordnetes Verzeichnis |
| `~` | Heimat-Verzeichnis des Nutzers |

### Mounting (Linux)

$$\boxed{\text{mount } P_2 \text{ /home} \Rightarrow \text{Partition } P_2 \text{ wird unter /home in den globalen Verzeichnisbaum eingehängt}}$$

- Systempartition bildet die **globale Wurzel**
- Weitere Partitionen werden an einen leeren **Mount Point** angedockt

![[Mounting Linux.excalidraw|800]]

### UNIX-Verweise (Links)

| Typ | Beschreibung | Besonderheit |
|---|---|---|
| **Hard Link** | Beide Einträge verweisen auf denselben Inode-Bezeichner | Nur innerhalb eines Dateisystems möglich; Datei bleibt nach Löschen eines Links erhalten |
| **Soft Link** (Symbolic Link) | Enthält den symbolischen Dateinamen des Ziels | Über Dateisysteme hinweg möglich; wird „dangling" wenn Originaldatei gelöscht wird |

> [!warning] **Achtung:** Ein Soft Link auf eine gelöschte Datei ist **dangling** – der Link existiert noch, zeigt aber ins Leere.

***

## 3. Partitionsstruktur (MBR-Schema)

### Aufbau

$$\boxed{\text{MBR (Sektor 0)} = 446\,\text{B Boot-Code} + 4 \times 16\,\text{B Partitionstabelle} + 2\,\text{B Magic}}$$

![[MBR-Schema.excalidraw|800]]

**Bestandteile jeder Partition:**
- **Bootblock**: Code zum Laden des installierten Betriebssystems
- **Superblock**: Schlüsselparameter (Magic, Anzahl Blöcke, Admin-Infos)
- **Liste der freien Blöcke**
- **I-Nodes**: Verwaltungsstrukturen für Dateien und Verzeichnisse
- **Eigentliche Daten**

***

## 4. Zuordnung Dateien → Datenblöcke

### 4.1 Zusammenhängende Belegung

$$\boxed{\text{Dateiblöcke gleicher Größe werden direkt hintereinander auf dem Datenträger abgelegt}}$$

| | Details |
|---|---|
| **Vorteile** | Maximale Effizienz, direkter Zugriff, einfache Verwaltung (nur Startblock + Länge nötig) |
| **Nachteile** | Fragmentierung beim Löschen/Anlegen; Probleme mit mehreren gleichzeitig offenen Dateien |
| **Einsatz** | CD-ROM, DVD, Blu-Ray |

### 4.2 Interne Verkettung (Linked List)

- Startblock im Verzeichniseintrag, jeder Block verweist auf Nachfolger
- Ausschließlich **sequentieller Zugriff** möglich

| | Details |
|---|---|
| **Vorteile** | Keine externe Fragmentierung, keine Größenvorgabe, einfaches Anlegen |
| **Nachteile** | Interne Fragmentierung (Zeiger verbraucht Platz im Block), ineffizienter Zugriff, Zuverlässigkeitsproblem |

> [!tip] **Abhilfe:** Gruppierung mehrerer Blöcke in **Cluster** reduziert den Overhead durch Zeiger.

### 4.3 Externe Verkettung: FAT (File Allocation Table)

$$\boxed{\text{FAT: Je eine Zeile pro Block } \rightarrow \text{ Adresse des nächsten Blocks; Dateiende} = \text{NULL-Zeiger}}$$

- Eingesetzt bei **MS-DOS/Windows**
- FAT an **fest reservierter Stelle** der Partition, wird laufend aktualisiert
- Startblock steht im Verzeichniseintrag

| | Details |
|---|---|
| **Vorteile** | Kein Platz im Datenblock verschwendet |
| **Nachteile** | Jeder Zugriff erfordert FAT-Lesevorgang (Sprung an Partitionsanfang); massiver Datenverlust bei FAT-Korruption → daher redundant gespeichert |

### 4.4 Indexblöcke & Inodes

$$\boxed{\text{Inode (Index Node)} = \text{dezentralisierte Tabelle pro Datei mit Blockliste als Array}}$$

- **Verzeichniseintrag** verweist nicht auf Datenblock, sondern auf **Inode**
- Inode enthält Blockliste → schneller direkter Zugriff an beliebige Position
- Zerstörung eines Inodes → Verlust **nur dieser einen Datei** (kein Single Point of Failure wie FAT)

> [!info] **Merkhilfe:** Inodes sind **namenlos** – der Name steht im Verzeichnis, nicht im Inode!

#### Ext2/Ext3: Kombiniertes Schema

| Ebene | Beschreibung | Max. Kapazität (bei 4 KiB Blöcken, 32-bit) |
|---|---|---|
| **Direct Blocks** | 12 direkte Zeiger auf Datenblöcke | $12 \times 4\,\text{KiB} = 48\,\text{KiB}$ |
| **Single Indirect** | Zeiger → Block mit Datenblock-Indizes | $1024 \times 4\,\text{KiB} = 4\,\text{MiB}$ |
| **Double Indirect** | Zeiger → Block mit Indizes auf Indexblöcke | $1024^2 \times 4\,\text{KiB} = 4\,\text{GiB}$ |
| **Triple Indirect** | Drei Zwischenstufen | $1024^3 \times 4\,\text{KiB} = 4\,\text{TiB}$ |

> [!warning] **Achtung:** Für **kleine Dateien** ist die Allokation eines ganzen Indexblocks (typisch 4 KiB) massive Platzverschwendung!

#### Beispielaufgabe: Verwaltungsaufwand für 300 KiB Datei

**Gegeben:** 10 direkte Referenzen, 1× Single-Indirect, 1× Double-Indirect, Blockgröße = 1024 B, Adresslänge = 32 Bit

$$\text{Einträge pro Block} = \frac{1024\,\text{B}}{4\,\text{B}} = 256$$

| Ebene | Datenblöcke referenziert | Verwaltungsblöcke |
|---|---|---|
| Direct (10) | 10 | 1 (Inode selbst) |
| Single-Indirect | 256 | 1 |
| Double-Indirect | 34 (Rest) | 2 (1 für DI-Block + 1 für eigentliche Daten) |
| **Gesamt** | **300** | **4 Verwaltungsblöcke** |

$$\boxed{\text{Verwaltungsaufwand} = 4\,\text{Blöcke}}$$

### 4.5 Ext4: Extents

$$\boxed{\text{Extent} = (\text{Startblock im Dateisystem},\, \text{Länge in Blöcken})}$$

- Statt 15 Blockindizes: **4 Extents** pro Inode → kompakte Adressierung vieler zusammenhängender Blöcke
- Bei mehr als 4 Extents: Verweis auf separaten Block mit weiteren Extent-Einträgen

> [!example] **Beispiel:**  
> `Dateiblöcke 0–55 → ab DS-Block 1200`  
> `Dateiblöcke 56–1400 → ab DS-Block 9950`  
> `Dateiblöcke 1401–1410 → ab DS-Block 10`  
> `Dateiblock 1411 → DS-Block 9`

***

## 5. Verzeichnisrealisierung

### Zwei Organisationsformen

| | MS-DOS-Stil | UNIX (Inode-basiert) |
|---|---|---|
| **Verzeichniseintrag enthält** | Alle Metadaten (Name, Typ, Größe, Rechte, …) | Nur Dateiname + Inode-Nummer |
| **Eintraglänge** | Groß | Klein |
| **Flexibilität** | Geringer | Höher (Inode kann über mehrere Verzeichnisse referenziert werden) |

> [!note] **Merke:** Der **Name einer Datei ist nicht Teil des Inodes** – er steht ausschließlich im Verzeichnis!

***

## 6. Plattenplatzverwaltung

### Blockgröße

- Kompromiss zwischen **Zugriffsgeschwindigkeit** (große Blöcke gut) und **interner Fragmentierung** (kleine Blöcke gut)
- Typische Wahl: **4 KiB**

### Disk Quotas (Plattenkontingente)

$$\boxed{\text{Quota} = \text{Max. erlaubte Anzahl Dateien und Blöcke pro Nutzer}}$$

| Typ | Verhalten |
|---|---|
| **Soft Limit** | Überschreitung x-mal möglich (Warnzähler), beim Login geprüft; bei $x=0$ → keine Anmeldung |
| **Hard Limit** | Keine Überschreitung möglich; Speicherung endet mit Fehlermeldung |

**Realisierung mit zwei Tabellen:**
1. Details der geöffneten Datei (Benutzer, Zeiger auf Quotatabelle)
2. Gesamtbelegung, Soft/Hard-Limits, verbleibende Warnanzahl

***

## 7. SSD-Verwaltung

### Flash-Hierarchie

```mermaid
graph LR
    Zelle --> Page
    Page --> Block
    Block --> Plane
    Plane --> Chip
    Chip --> SSD
```

$$\boxed{\text{Page} = \text{kleinste Lese/Schreib-Einheit} \quad \text{Block} = \text{kleinste Lösch-Einheit}}$$

> [!danger] **Erase-before-Write** 
> Eine Seite mit Daten **kann nicht direkt überschrieben** werden. Erst muss der gesamte Block gelöscht werden!

### Flash Translation Layer (FTL)

$$\boxed{\text{FTL: } \text{LBA} \rightarrow \text{physische Seitenadresse (Zuordnungstabelle)}}$$

- BS sendet Befehle an logische Blockadressen (LBAs) – ohne Kenntnis interner SSD-Struktur
- **Out-of-Place-Updates**: Statt Überschreiben wird alte Seite als ungültig markiert → neue Seite an freier Stelle geschrieben

### Garbage Collection (GC)

$$\boxed{\text{WAF} = \frac{\text{physische Schreibvorgänge}}{\text{logische Schreibvorgänge}}}$$

**Ablauf:**
1. GC wählt Block mit hohem Anteil veralteter Seiten
2. Gültige Seiten → in anderen Block kopieren
3. FTL-Mapping aktualisieren
4. Leergeräumten Block vollständig löschen
5. Freigabe für neue Schreibvorgänge

> [!warning] **Write Amplification:** Reale WAFs liegen zwischen **3 und 10** → Leistungseinbuße und verkürzte Flash-Lebensdauer!

| WAF-Wert | Bedeutung |
|---|---|
| **1,0** | Ideal: jeder logische Schreibvorgang = genau ein physischer |
| **3–10** | Realistisch: erheblicher Overhead |

### TRIM

$$\boxed{\text{TRIM (Linux: DISCARD/SCSI UNMAP)}: \text{Dateisystem informiert SSD über nicht mehr genutzte LBAs}}$$

| Modus | Beschreibung |
|---|---|
| **Echtzeit-TRIM** | Anwendung bei jedem Löschvorgang |
| **Gebündeltes TRIM** | Periodisches Ausführen → weniger Overhead/Latenz |

### Overprovisioning & Wear Leveling

- **Overprovisioning**: SSDs reservieren 10–20% als unsichtbaren Systemplatz → Spielraum für GC
- **Wear Leveling**: Gleichmäßige Verteilung von Löschvorgängen (NAND: 1.000–100.000 Schreib/Lösch-Zyklen je nach Zelltyp)

| Typ | Strategie |
|---|---|
| **Dynamisches Wear Leveling** | Heiße Daten → weniger abgenutzte Blöcke verschieben |
| **Statisches Wear Leveling** | Kalte Daten periodisch von wenig auf stärker abgenutzte Blöcke verschieben |

***

## 8. Konsistenz & Log-basierte Dateisysteme

### Schreibstrategien bei gecachten Daten

| Strategie | Beschreibung | Risiko |
|---|---|---|
| **Write Through** | Sofortiges Schreiben, kein Cache | Langsam, aber sicher |
| **Careful Write** | Verzögertes Schreiben (max. Verzögerung) | Inkonsistenz bei Systemausfall möglich |
| **Lazy Write** | Nur im Cache, periodische Synchronisation (z.B. alle 30 s) | Gravierende Inkonsistenzen nach Crash |

### Inkonsistenzbeispiel: Datei löschen
1. Dateieintrag aus dem Verzeichnis entfernen
2. Inode der Datei freigeben
3. Von der Inode belegte Datenblöcke freigeben

> [!failure] 
> **Crash zwischen Schritt 1 und 2** → **Orphaned Inode** (Inode verwaist, nicht mehr erreichbar)  
> **Crash zwischen Schritt 2 und 3** → **Missing Blocks** (Blöcke nicht in Freiliste, aber auch keiner Datei zugeordnet)

### Konsistenzüberprüfung (fsck/scandisk)

- Zwei Zählertabellen: „In wie vielen Dateien kommt Block X vor?" + „In wie vielen Freilisten-Einträgen?"
- **Konsistenter Zustand**: Jeder Block in genau einer der beiden Tabellen

| Problem | Lösung |
|---|---|
| **Vermisster Block** | In Freiliste aufnehmen |
| **Block doppelt als frei** | Freiliste bereinigen |
| **Block in zwei Dateien** | Block kopieren, Benutzer informieren |

### Log-basierte (Journaling) Dateisysteme

$$\boxed{\text{Journal} = \text{Ringpuffer mit geplanten Operationen + Prüfsummen (Ganz-oder-gar-nicht-Prinzip)}}$$

**Ablauf einer Operation:**
1. Beschreibung ins Logbuch schreiben
2. Prüfsumme ans Logbuch anhängen
3. Cache der Festplatte leeren
4. Operation durchführen
5. Operation im Logbuch als abgeschlossen markieren

**Nach Systemcrash:** Replay aller nicht abgeschlossenen Operationen → Konsistenz wiederhergestellt

#### Journaling-Stufen

| Stufe | Journal enthält | Vorteil | Nachteil |
|---|---|---|---|
| **Vollständig** | Daten + Metadaten | Volle Konsistenzgarantie | Alle Daten 2× geschrieben → Leistungseinbuße |
| **Metadata-Only** | Nur Metadaten | Deutlich bessere Performance | Datenverlust möglich (Metadaten konsistent, Inhalte ggf. verloren) |

> [!tip] **Flexibilität:** Das Journal muss nicht Teil des Dateisystems sein – es kann auf einer anderen Festplatte (z.B. SSD) oder in Batterie-gestütztem RAM liegen.

***

## 9. Backup

### Backup-Arten

$$\boxed{\text{Vollständig: alle Daten} \quad \text{Inkrementell: nur Änderungen seit letztem Backup}}$$

**Typische Strategie:**
- Wöchentliche vollständige Sicherung (z.B. Wochenende)
- Tägliches inkrementelles Backup
- Sicherung über 3–4 Wochen auf unterschiedlichen Medien
- Periodisch: dauerhaftes Vollbackup (nicht überschrieben)

> [!warning] **Achtung:** Backup-Medien müssen vor Feuer, Wasser, Erdbeben, Diebstahl geschützt werden → **Offsite-Lagerung**!

### Physische vs. Logische Datensicherung

| | Physische Sicherung (dump) | Logische Sicherung |
|---|---|---|
| **Vorgehen** | Block 0 bis Ende sequenziell auf Band schreiben | Rekursives Durchlaufen ab vorgegebenen Verzeichnissen |
| **Vorteil** | Einfach und schnell | Einzelne Dateien einfach restaurierbar |
| **Nachteil** | Keine inkrementelle Sicherung möglich | Aufwändiger |
| **Standard** | Nein | Ja (bei den meisten Betriebssystemen) |

### Sicherungsalgorithmus (4 Phasen)

- [>] **Phase 1**: Rekursives Durchlaufen aller Verzeichnisse → Bitmap mit I-Node-Nummern; **alle modifizierten Dateien** markieren; **alle Verzeichnisse** markieren
- [>] **Phase 2**: Erneuter Durchlauf → Aufhebung der Markierung aller Verzeichnisse **ohne modifizierte Dateien**
- [>] **Phase 3**: Markierte Verzeichnisse mit Attributen sichern
- [>] **Phase 4**: Markierte Dateien mit Attributen sichern

> [!note] Alle Verzeichnisse auf dem **Pfad zu einer modifizierten Datei** werden gesichert (auch wenn unverändert) → vollständige Pfadstruktur für Restauration vorhanden.

***

## 📌 Zusammenfassung

### Wichtige Konzepte

| Konzept | Bedeutung |
|---|---|
| **Inode** | Dezentrale Indexstruktur pro Datei (namenlos, enthält Blockzeiger + Metadaten) |
| **FAT** | Externe verkettete Liste; zentrale Tabelle mit nächsten Blockzeigern |
| **FTL** | SSD-Treiberschicht: übersetzt LBAs in physische Seitenadressen |
| **WAF** | Write Amplification Factor: physische/logische Schreibvorgänge |
| **Journaling** | Transaktionsbasiertes Dateisystem: Ganz-oder-gar-nicht-Prinzip |
| **TRIM** | Befehl zur Benachrichtigung der SSD über freigegebene LBAs |
| **Extent** | Kompakte Blockadressierung: (Startblock, Länge) statt einzelner Zeiger |
| **Hard Link** | Direktverweis auf Inode; Datei bleibt nach Löschen eines Links erhalten |
| **Soft Link** | Symbolischer Verweis auf Dateinamen; wird dangling bei Löschung des Ziels |

### Kernaussagen

- [p] **Inodes dezentralisieren die Blockverwaltung** – kein Single Point of Failure wie bei FAT  
- [p] **Journaling garantiert Konsistenz** durch das Ganz-oder-gar-nicht-Prinzip  
- [p] **Extents reduzieren Metadaten-Overhead** bei großen zusammenhängenden Dateien  
- [!] **Achtung:** Metadata-Only-Journaling kann Datenverlust verursachen, auch wenn Metadaten konsistent sind  
- [c] **Falsch:** Soft Links funktionieren immer – sie werden dangling wenn das Ziel gelöscht wird  
- [c] **Falsch:** SSDs können Seiten direkt überschreiben – Erase-before-Write ist zwingend  

### Blockzuordnungsverfahren im Vergleich

| Verfahren | Zugriff | Fragmentierung | Einsatz |
|---|---|---|---|
| **Zusammenhängend** | $O(1)$ | Extern (hoch) | CD/DVD/Blu-Ray |
| **Interne Verkettung** | $O(n)$ sequenziell | Intern (Zeiger) | Historisch |
| **FAT (extern)** | $O(n)$ | Keine externe | MS-DOS/Windows |
| **Indexblöcke (Inodes)** | $O(1)$ direkt | Minimal | UNIX/Linux (ext2/3) |
| **Extents** | $O(1)$ | Minimal | Linux ext4 |

***

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.06 Speicher- und Adressraumverwaltung]]: Speicherverwaltung & virtuelle Adressräume – Seitentabellen-Konzept direkt wiederverwendet bei verschachtelten Indexblöcken
- [[VL.05 Betriebsmittelverwaltung]]: Prozesse & Scheduling – `exec`-Systemaufruf lädt ELF-Binaries über das Dateisystem
- [[VL.04 Koordination nebenläufiger Prozesse]]: Synchronisation – Journaling nutzt Transaktionskonzepte (Atomarität wie bei Mutex-geschützten kritischen Abschnitten)
- [[VL.08 Sicherheit und Architektur von BS]]: I/O-Subsystem – Gerätedateien und Blockgeräteabstraktion bauen direkt auf Dateisystem-Konzepten auf