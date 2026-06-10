**Class:** [[SysProg - Systemprogrammierung]]  
**Date:** 28-05-2026  
**Topics:** #Speicherverwaltung #Paging #Verdrängung  
**Link:** [[VL.06 SysProg.pdf]]

***

## 🎯 Lernziele der Vorlesung

Diese Vorlesung erklärt, wie Betriebssysteme Speicher und Adressräume verwalten, wie virtuelle Adressen in physische Adressen übersetzt werden und wie Seiten bei Speichermangel ausgelagert und ersetzt werden. Der Fokus liegt auf Paging, Seitentabellen, Page Faults und Verdrängungsstrategien.

- **Speicherverwaltung im Betriebssystem**: Warum Speicher das zentrale Betriebsmittel ist und welche Bereiche ein Prozess benötigt.
- **Virtuelle Adressierung**: Wie logische Adressen unabhängig vom physischen Speicher funktionieren.
- **Seitentabellen und Paging**: Wie Adressen effizient abgebildet werden.
- **Seitenfehler und Auslagerung**: Was bei fehlenden Seiten passiert.
- **Verdrängungsstrategien**: Welche Seite bei Speicherknappheit entfernt wird und warum einige Strategien besser sind als andere.

***

## 1. Speicherverwaltung im Betriebssystem

### Definitionen & Grundidee

Speicher ist das am häufigsten genutzte Betriebsmittel eines Systems. Ein Betriebssystem verwaltet nicht nur den Arbeitsspeicher für Prozesse, sondern auch eigene Datenstrukturen wie PCBs oder Kernel-Daten.

$$\boxed{\text{Speicherallokation} = \text{Zuordnung von Speicher an Prozesse und das Betriebssystem}}$$

**Benötigte Speicherbereiche:**
- **Prozesse**: Stack, Heap, Programm-Code, Daten.
- **Betriebssystem**: BS-Code, BS-Daten, Verwaltungsstrukturen.

> [!info] **Rolle**
> Speicherverwaltung sorgt dafür, dass mehrere Programme gleichzeitig laufen können, ohne sich gegenseitig zu überschreiben.

### Statische und dynamische Speicherallokation

Frühe Systeme arbeiteten mit **statischer Speicherallokation**. Dabei wird der Speicher fest in Bereiche eingeteilt, und ein Prozess belegt einen ganzen Bereich vollständig. Das ist einfach, aber unflexibel.

**Nachteile der statischen Allokation:**
- Nur ganze Prozesse werden verdrängt.
- Viel Speicher kann ungenutzt bleiben.
- Wechsel zwischen Prozessen ist ineffizient.

$$\boxed{\text{Dynamische Speicherallokation} = \text{Speicher wird bedarfsgerecht zur Laufzeit zugewiesen und ausgelagert}}$$

Bei dynamischer Allokation werden Prozessteile transparent ein- und ausgelagert. Das ist die Grundlage für **virtuelle Adressierung** und **realokierbare Prozesse**.

> [!warning] **Achtung**
> Wenn eine benötigte Seite nicht im Speicher ist, löst der Zugriff einen **Page Fault** aus.

### Intuition

Die statische Variante ist wie ein fester Parkplatz pro Auto. Die dynamische Variante ist wie ein intelligentes Parkhaus, in dem Autos je nach Bedarf umgeparkt werden.

***

## 2. Virtuelle Adressierung und Seiten

### Virtueller und physischer Adressraum

In modernen Systemen gibt es viel mehr virtuelle als physische Adressen. Eine virtuelle Adresse muss zur Laufzeit auf eine physische Adresse abgebildet werden.

**Entscheidungen des Betriebssystems:**
- Welche virtuellen Adressen sollen im Hauptspeicher sein?
- Wie wird die Übersetzung effizient ausgeführt?
- Welche Daten werden bei Speicherknappheit ausgelagert?
- Was passiert mit ausgelagerten Daten?

$$\boxed{\text{Virtuelle Adresse} \xrightarrow{\text{Abbildung}} \text{Physische Adresse}}$$

### Seitenadressierung / Paging

Beim **Paging** werden virtueller und physischer Speicher in gleich große Blöcke fester Länge geteilt.

| Begriff                | Bedeutung                      |
| ---------------------- | ------------------------------ |
| **Seite (page)**       | Block im virtuellen Adressraum |
| **Kachel / Pageframe** | Block im physischen Speicher   |
| **Seitentabelle**      | Abbildung von Seite auf Kachel |

$$\boxed{\text{Paging} = \text{virtuelle und physikalische Speicher in Stücke fester Länge eingeteilt}}$$

Die Größe ist meist $4\,\text{KiB}$, weil dies ein guter Kompromiss zwischen Verwaltungsaufwand und Effizienz ist.

> [!tip] **Merkhilfe**
> Virtuell heißt **Seite**, physisch heißt **Kachel**.

### Warum die Granularität wichtig ist

Die Verwaltungseinheit darf nicht zu klein sein, sonst wird die Verwaltungsstruktur selbst riesig. Sie darf aber auch nicht zu groß sein, sonst wird Speicher unflexibel verschwendet.

| Granularität | Vorteil | Nachteil |
|---|---|---|
| sehr klein | präzise Nutzung | große Verwaltungsstruktur |
| sehr groß | kleine Verwaltungsstruktur | viel Speicherverlust |

***

## 3. Seitentabellen und Adressübersetzung

### Aufbau der Seitentabelle

Für jede virtuelle Seite braucht man Informationen darüber, ob sie gültig ist, wo sie physisch liegt und welche Zugriffsrechte gelten.

$$\boxed{\text{Seitentabelleneintrag} = (\text{Kachelnummer}, \text{Metadaten})}$$

**Wichtige Metadaten:**
- **Präsenzbit, presence bit P:** Seite im Hauptspeicher vorhanden?
- **Referenzbit, reference bit R oder access bit A:** Wurde auf die Seite bereits zugegriffen?
- **Modifikationsbit, dirty bit D oder modification bit M:** Wurde die seite modifiziert?

> [!note] **Wichtig**
> Die Bits **R** und **D** werden von der CPU gesetzt und helfen dem Betriebssystem bei Ersetzungsstrategien.


![[Seitentabelle.excalidraw|700]]

### Adressübersetzung mit Seitentabelle

Eine virtuelle Adresse besteht aus:
- **Seitennummer**
- **Offset** innerhalb der Seite

Der Prozessor besitzt ein privilegiertes Register mit der Basisadresse der Seitentabelle.

#### Ablauf der Übersetzung

1. Zerlege die virtuelle Adresse in **Seitennummer** und **Offset**.
2. Nutze die Seitennummer als Index in der Seitentabelle.
3. Prüfe Gültigkeit und Zugriffsrechte.
4. Erzeuge aus **Kachelnummer** und **Offset** die physische Adresse.

$$\boxed{\text{Physische Adresse} = \text{Kachelnummer} \,\Vert\, \text{Offset}}$$

### Beispiel für eine Übersetzung

Gegeben:
- virtueller Adressraum: 18 Bits
- Seitengröße: $4\,\text{KiB} = 2^{12}$

Dann gilt:
- **Offset**: 12 Bits
- **Seitennummer**: 6 Bits

Die Seitennummer wird in der Tabelle nachgeschlagen, die Kachelnummer ersetzt und der Offset unverändert übernommen.

> [!example] **Intuition**
> Die Seite sagt: „Wo ungefähr?“ Der Offset sagt: „Genau welches Byte innerhalb der Seite?“

### Mehrstufige Seitentabellen

Bei großen Adressräumen wäre eine einfache Tabelle viel zu groß. Deshalb werden oft **mehrstufige Tabellen** verwendet.

$$\boxed{\text{Mehrstufige Seitentabelle} = \text{hierarchische Aufteilung der Adressübersetzung}}$$

**Vorteil:**
- Nur die tatsächlich genutzten Teile des Adressraums brauchen Tabellen.
- Besonders gut für **spröde besetzte** Adressräume.

| Variante | Vorteil | Nachteil |
|---|---|---|
| einfache Tabelle | direkter Lookup | riesig bei großem Adressraum |
| invertierte Tabelle | Größe abhängig vom physischen Speicher | Suche schwieriger |
| mehrstufige Tabelle | effizient bei sparsamer Belegung | mehrere Zugriffe nötig |

> [!warning] **Achtung**
> Eine 1-stufige Tabelle für einen 64-Bit-Adressraum ist praktisch nicht handhabbar.

***

## 4. Auslagerung und Demand Paging

### Nachschubstrategien

Das Betriebssystem muss entscheiden, wann Seiten in den Speicher geladen werden.

**Zwei Grundideen:**
- **Demand Paging**: Seite wird erst bei Bedarf geladen.
- **Pre-Paging**: Seite wird vorsorglich vorab geladen.

$$\boxed{\text{Demand Paging} = \text{Nachladen erst bei Zugriff auf eine nicht vorhandene Seite}}$$

Pre-Paging ist nur sinnvoll, wenn das zukünftige Zugriffsverhalten gut bekannt ist. Das ist in der Praxis oft nicht der Fall.

### Verdrängung

Wenn Speicher knapp wird, müssen Seiten ausgelagert werden. Seiten werden auf andere Medien geschrieben, meist auf die Festplatte oder in eine Swap-Datei.

**Wichtige Idee:**
- Nicht der ganze Prozess wird ausgelagert.
- Stattdessen werden nur einzelne Seiten verdrängt.
- Das Betriebssystem merkt sich, wo die Seite abgelegt wurde.

$$\boxed{\text{Verdrängung} = \text{Auslagerung einzelner Seiten bei Speicherknappheit}}$$

### Seitenfehler und Ablauf

Wenn eine ausgelagerte oder noch nicht geladene Seite angesprochen wird, entsteht ein **Page Fault**.

### Ablauf bei Page Fault

1. Zugriff auf eine ungültige Seite.
2. Page Fault wird ausgelöst.
3. Betriebssystem prüft, ob eine freie Kachel vorhanden ist.
4. Falls nein, wird eine Kachel nach einer Verdrängungsstrategie gewählt.
5. Falls die Seite modifiziert war, wird sie zurück auf den Ersatzspeicher geschrieben.
6. Neue Seite wird eingelagert.
7. Seitentabelle wird aktualisiert.


![[Detaillierter-Ablauf.excalidraw|700]]

> [!info] **Rolle des Dirty-Bits**
> Ist eine Seite nicht verändert worden, muss sie vor dem Verdrängen oft nicht gespeichert werden.

### Wo liegen ausgelagerte Daten?

Das Betriebssystem führt eine zusätzliche Struktur, um zu wissen, wo die ausgelagerten Inhalte liegen.

**Mögliche Orte:**
- Swap-Datei.
- Ausführbare Datei.
- Gemeinsame Bibliothek.
- Noch nicht initialisierte Daten, die erst erzeugt werden.

***

## 5. Verdrängungsstrategien

### Ziel der Ersetzung

Die Leistung von Demand Paging hängt stark davon ab, wie gut die verdrängte Seite gewählt wird. Ziel ist es, die Zahl der Seitenfehler zu minimieren.

$$\boxed{\text{Replacement Policy} = \text{Strategie zur Auswahl der zu verdrängenden Seite}}$$

### Lokale und globale Auswahl

| Strategie | Bedeutung |
|---|---|
| **lokal** | Nur Seiten des verursachenden Prozesses werden ersetzt |
| **global** | Jede beliebige Kachel darf ersetzt werden |

### Optimale Strategie

Die optimale Strategie verdrängt die Seite, die am längsten nicht mehr benötigt wird.

$$\boxed{\text{Optimal} = \text{verdränge die Seite mit dem spätesten nächsten Zugriff}}$$

Diese Strategie minimiert die Seitenfehlerzahl, ist aber nicht realisierbar, weil sie zukünftige Zugriffe kennen müsste.

> [!failure] **Nicht realisierbar**
> Die optimale Strategie ist nur ein theoretischer Maßstab für andere Algorithmen.

### Lokalität

Reale Programme zeigen typischerweise **Lokalität**.

**Arten von Lokalität:**
- **Zeitliche Lokalität**: Was gerade benutzt wurde, wird bald wieder benutzt.
- **Räumliche Lokalität**: Adressen in der Nähe einer benutzten Adresse werden bald gebraucht.

$$\boxed{\text{Lokalität} = \text{Vergangenheit ist eine gute Prognose für die nahe Zukunft}}$$

> [!example] **Intuition**
> Ein Programm arbeitet oft in Schleifen oder in zusammenhängenden Codeabschnitten.

### Reale Verdrängungsstrategien

| Strategie | Idee | Nachteil |
|---|---|---|
| **FIFO** | älteste Seite zuerst | kann Anomalie zeigen |
| **LRU** | am längsten nicht benutzt | aufwendig umzusetzen |
| **LFU** | am seltensten benutzt | Zählerverwaltung nötig |
| **RNU** | innerhalb eines Fensters nicht referenziert | nur Näherung |

#### FIFO

FIFO verdrängt die Seite, die am längsten im Speicher ist.

> [!warning] **Achtung**
> FIFO kann eine **Anomalie** zeigen: Mehr Speicher kann mehr Seitenfehler verursachen.

#### LFU

LFU verdrängt die am wenigsten häufig benutzte Seite. Dafür zählt man Zugriffe pro Seite.

#### LRU

LRU verdrängt die Seite, die am längsten nicht mehr referenziert wurde. Das nähert oft das optimale Verhalten gut an.

$$\boxed{\text{LRU} = \text{verdränge die zuletzt am längsten nicht benutzte Seite}}$$

### Angenäherte LRU-Verfahren

Da exaktes LRU zu teuer ist, nutzt man Hardwareunterstützung.

**Grundidee:**
- Jede Seite hat ein **Accessed-Bit**.
- Die CPU setzt es beim Zugriff.
- Periodisches Zurücksetzen erzeugt eine grobe Zeitinformation.

#### Second-Chance / Clock

Der Clock-Algorithmus ist eine FIFO-Variante mit Referenzbit:

1. Gehe zyklisch über die Seiten.
2. Hat die aktuelle Seite ein Referenzbit 1, setze es auf 0 und gib ihr eine zweite Chance.
3. Hat sie Referenzbit 0, verdränge sie.

$$\boxed{\text{Clock} = \text{FIFO mit Zweitchance über Referenzbits}}$$

#### Solaris 2 / Two-Handed Clock

Hier arbeiten zwei Zeiger:
- Der erste setzt Referenzbits zurück.
- Der zweite gibt später Seiten mit weiterhin 0 frei.

**Wichtige Parameter:**
- **scanrate**: Geschwindigkeit des Scans.
- **handspread**: Abstand zwischen den Zeigern.

### Page-Fault-Frequency

Ein alternatives Konzept passt die Anzahl der Kacheln pro Prozess an dessen Seitenfehlerrate an.

**Regel:**
- Ist die Fehlerrate zu hoch, bekommt der Prozess mehr Kacheln.
- Ist die Fehlerrate zu niedrig, kann man Kacheln entziehen.

$$\boxed{\text{Page-Fault-Frequency} = \text{Steuerung der Kacheln über die Fehlerrate}}$$

***

## 6. Zentrale Formeln und Tabellen

### Wichtige Formeln

| Konzept | Formel |
|---|---|
| Seitengröße | $2^n$ Bytes |
| Offset-Bits | $\log_2(\text{Seitengröße})$ |
| Adresszerlegung | $V = (\text{Seitennummer}, \text{Offset})$ |
| Physische Adresse | $P = (\text{Kachelnummer}, \text{Offset})$ |

### Vergleich der Strategien

| Strategie | Gut | Schlecht |
|---|---|---|
| **Optimal** | theoretisch beste Fehlerrate | nicht realisierbar |
| **FIFO** | einfach | Anomalie möglich |
| **LRU** | meist sehr gut | teuer in Hardware/Software |
| **LFU** | berücksichtigt Nutzungshäufigkeit | langsame Reaktion auf Wandel |
| **RNU** | praktikable Näherung | abhängig von Fensterwahl |

> [!success] **Kernaussage**
> Gute Speicherverwaltung kombiniert Paging, Metadaten, Page Fault Handling und eine möglichst intelligente Verdrängungsstrategie.

***

## 📌 Zusammenfassung

### Wichtige Konzepte

| Konzept | Bedeutung | Zentrale Idee |
|---|---|---|
| **Paging** | Aufteilung in Seiten und Kacheln | gleiche Blockgröße |
| **Seitentabelle** | Abbildung virtuell auf physisch | Lookup pro Seite |
| **Page Fault** | Zugriff auf fehlende Seite | Nachladen durch BS |
| **Demand Paging** | Laden bei Bedarf | spart Speicher |
| **Verdrängung** | Entfernen einer Seite | bei Speichermangel |
| **LRU** | zuletzt unbenutzte Seite verdrängen | gute Näherung |

### Kernaussagen

- [p] **Virtuelle Adressierung** trennt Programmierung vom physikalischen Speicher.
- [p] **Paging** macht Speicherverwaltung flexibel und effizient.
- [p] **Seitentabellen** speichern nicht nur Adressen, sondern auch Schutz- und Zustandsbits.
- [p] **Demand Paging** reduziert Speicherverbrauch, weil Seiten erst bei Bedarf geladen werden.
- [p] **LRU-nahe Verfahren** funktionieren in der Praxis meist am besten, weil Programme Lokalität zeigen.
- [!] **Achtung:** Eine große einfache Tabelle skaliert schlecht mit riesigen Adressräumen.
- [c] **Falsch:** Nicht der ganze Prozess muss bei Speicherknappheit verdrängt werden; oft reichen einzelne Seiten.

### Wichtige Algorithmen / Formeln

| Algorithmus | Laufzeit / Aufwand | Anwendung |
|---|---|---|
| **Einfaches Paging** | schneller Lookup, aber große Tabelle | kleine bis mittlere Adressräume |
| **Mehrstufige Seitentabelle** | mehrere Lookups | große, sparse Adressräume |
| **FIFO** | sehr einfach | Baseline |
| **LRU** | höherer Aufwand | gute Praxisnähe |
| **Clock** | effizienter LRU-Ersatz | reale Systeme |
| **Page-Fault-Frequency** | dynamische Anpassung | Laststeuerung |

***

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.05 Betriebsmittelverwaltung]]: Grundlage für virtuelle Adressierung und Speicherabbildung.
- [[VL.07 Dateisysteme]]: Einordnung in Kernel-Aufgaben und Ressourcenverwaltung.
- [[VL.08 Sicherheit und Architektur von BS]]: Zusammenspiel von Speicherverwaltung und Prozesswechseln.
- [[VL.07 Dateisysteme]]: Swap-Datei und Auslagerung als Verbindung zum Massenspeicher.

### Fußnoten

1. Die Begriffe **Seite** und **Kachel** sind die zentrale Analogie zwischen virtuellem und physischem Speicher.  
2. In der Praxis werden viele Strategien nur angenähert umgesetzt, weil exakte Information über zukünftige Zugriffe fehlt.  
3. Das Dirty-Bit spart Arbeit, wenn eine Seite seit dem Laden nicht verändert wurde.