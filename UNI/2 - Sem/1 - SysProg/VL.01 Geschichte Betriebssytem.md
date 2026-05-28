**Class:** [[SysProg - Systemprogrammierung]]
**Date:** 17-04-2026
**Topics:** #Organisation #Betriebssysteme #Geschichte #UNIX #Linux #Virtualisierung #Cloud #FogComputing

---

## 🎯 Lernziele der Vorlesung

VL.01 führt in den Kurs ein und behandelt als Selbststudium eine **kurze Geschichte der Betriebssysteme** — von Vakuumröhren bis Cloud und Fog Computing.

- **Kursorganisation**: Team, Kommunikationswege, Prüfungsmodalitäten
- **BS als Kategorie**: älteste und ausgereifteste Software; Grundlage vieler Domains
- **Generationen**: 1. bis 4. Generation + Mobilgeräte
- **CTSS → MULTICS → UNIX → Linux**: Entstehung der modernen BS-Linie
- **Virtualisierung**: Hypervisor, Virtualisierungsformen
- **Cloud und Fog Computing**: Definitionen, Schichten, Anwendungsfälle

---

## 1. Organisatorisches

### Das Team

| Rolle | Name | E-Mail | Raum | Sprechzeiten |
|-------|------|--------|------|-------------|
| **Dozent** | Prof. Odej Kao | odej.kao@tu-berlin.de | EN 729 | n.V. |
| **Sekretariat** | Jana Bechstein | jana.bechstein@tu-berlin.de | EN 727 | Mo–Do 12–16 Uhr |
| **Koordination** | Jonathan Rau | j.rau.1@tu-berlin.de | EN 725 | n.V. |
| **Koordination** | Justus Flerlage | j.flerlage@tu-berlin.de | EN 726 | n.V. |

⚠️ E-Mails bitte mit **`[SysProg]`** im Betreff kennzeichnen.

### Kommunikationswege

- **Fachgebiets-Homepage**: https://www.tu.berlin/dos/studium-lehre/lehrveranstaltungen
- **ISIS** (Lernplattform): https://isis.tu-berlin.de/course/view.php?id=47805 — Folien, Videos, Übungsblätter, Diskussionsforum
- **E-Mail**: dringende Ankündigungen, individuelle Fragen
- **Persönlich**: Sprechstunden

### Vorlesungsstil

- Vorlesung: **Freitags 10–12 Uhr** — Beispiele und Fragen
- PDFs werden **freitags nach der VL** auf ISIS hochgeladen, zusammen mit Multiple-Choice-Tests (nicht bewertet, zum Selbsttest)

### Vorlesungsplan

| Datum | Thema | Übung |
|-------|-------|-------|
| 17-Apr | Organisatorisches + Prozesse 1 | — |
| 24-Apr | Prozesse 2 + Shell | C Basics |
| 1-May | 🔴 Feiertag | — |
| 8-May | Scheduling | Scheduling |
| 15-May | Semaphore 1 | Prozesssynchronisation |
| 22-May | Semaphore 2 | Prozesssynchronisation |
| 29-May | BM-Verwaltung | BM-Verwaltung |
| 5-Jun | Speicher 1 | Speicherverwaltung |
| 12-Jun | Speicher 2 + Dateisysteme | Speicherverwaltung |
| 19-Jun | Sicherheit | Dateisysteme |
| 26-Jun | Betriebssysteme und Fallbeispiele | Wiederholung + Klausurvorbereitung |
| 3-Jul | Virtualisierung | ← |
| 10-Jul | Microservices | ← |

### Übungsbetrieb

- Beginn: **ab 20.04.2026**
- Tutorien: Mo–Fr 08–18 Uhr (außer Fr 10–12 Uhr = Vorlesung)
- Inhalte: Übungsblätter + Präsenztutorien + selbstständige Aufgaben + Tutorensprechstunden

### Prüfung

- **Pflichtveranstaltung** im Bachelor Informatik und Technische Informatik
- Schriftliche Prüfung = **100% der Note**
- **Ersttermin**: 30.07.2026 08:00 Uhr (Anmeldung bis 22.07.2026 23:59 Uhr)
- **Zweittermin**: 01.10.2026 13:00 Uhr (Anmeldung bis 23.09.2026 23:59 Uhr)

### Literatur

| Buch | Verlag |
|------|--------|
| Stallings — *Operating Systems: Internals and Design Principles* | Pearson |
| Silberschatz et al. — *Operating System Concepts* | John Wiley |
| Tanenbaum & Bos — *Modern Operating Systems* | Pearson |

E-Books über TU-Campusnetz (ggf. VPN):
- [Operating Systems (Campuslizenz)](https://www.pearson-studium.de/drm/reader/nu/code/qz8qb0436ui6wyos6hbnas4xs2cso4ai)
- [Internals and Design Principles](https://ebookcentral.proquest.com/lib/tuberlin/detail.action?docID=5833157)
- [Modern Operating Systems](https://ebookcentral.proquest.com/lib/tuberlin/detail.action?docID=5833738)

---

## 2. Betriebssysteme — Einführung

Betriebssysteme sind die **älteste und am weitesten entwickelte Software** bzgl. Funktionalität, Effizienz, Ausfallsicherheit, Sicherheit und Portabilität. Die grundlegenden Mechanismen wurden für viele andere Domains adaptiert: Datenbanken, Grafik, Compiler, verteilte Systeme.

---

## 3. Geschichte der Betriebssysteme (Selbststudium)

Die Entwicklung der BS ist eng mit der Entwicklung der **Rechnerarchitekturen** verbunden. Die Generationen sind nicht exakt abgegrenzt und teilweise überlappend. Die Erzählung ist USA- (insbesondere MIT-)zentriert — vergleichbare Systeme entstanden auch andernorts.

### Erste Generation (1945–1955)

- Vakuumröhren und Trommelspeicher
- BS und Programmiersprachen unbekannt; Assembler entsteht erst im Laufe dieser Epoche
- Programmierung in **Maschinensprache**; Portierung als Konzept unbekannt
- Folklore: „Story of Mel" → http://catb.org/jargon/html/story-of-mel.html

### Zweite Generation (1955–1965)

- Transistoren → erhöhte Zuverlässigkeit; Magnetbänder als schnellerer Massenspeicher; Lochkarten
- **Stapelverarbeitung** als Hauptbetriebsart:
  - Manuell: Operateur lädt neuen Job nach Abschluss des alten
  - Automatisch: kleiner Rechner kopiert Jobs auf Band → Mainframe führt aus → kleiner Rechner druckt Ergebnisse
- **Job Control Language (JCL)**: Automatisierung von Operateursaufgaben → erste Form von BS-Funktionalität
- 📌 *Randnotiz*: Der Begriff „patchen" kommt vom buchstäblichen Kleben von Lochstreifen

### Dritte Generation (1965–1980)

- Einführung von **integrierten Schaltungen**
- Zwei inkompatible Produktlinien:
  - 36-bit-**wortorientiert** (Wissenschaft/Industrie): IBM 7094
  - 6-bit-**zeichenorientiert** (Banken/Versicherungen): IBM 1401
- **IBM System/360**: Serie softwarekompatibler Rechner mit identischem Instruktionssatz → löst Portabilitätsproblem
- Widersprüchliche Anforderungen → großes, komplexes, fehlerbehaftetes BS
  → Einsatz höherer Programmiersprachen für BS-Entwicklung
  → **Geburtsstunde des Software-Engineering**

**CTSS und Time-Sharing:**

MIT-Forscher frustriert vom Batch-Betrieb → Idee: mehrere Nutzer interagieren gleichzeitig (Time-Sharing statt Batch)

- **CTSS** (Compatible Time Sharing System, 1961/62):
  - Minimierung der **Antwortzeit** statt CPU-Auslastung
  - HW-Änderungen an IBM 7094: Intervallzeitgeber, zweite Speicherbank, Speicherschutzregister
  - Prozessor wechselt ständig zwischen Jobs; E/A-wartende Jobs blockiert; kein interaktiver Job → Batch-Job im Hintergrund (daher *Compatible*)
  - Schlüsseltechnik: **Prozessor wird virtualisiert** → der Job wird zum **Prozess**

**MULTICS:**

- MULTIplexed Information and Computing System (Bell Labs + MIT + General Electric)
- Idee: Rechenleistung wie Strom aus der Steckdose — für alle Einwohner Bostons
- Bahnbrechende Features: baumartiges Dateisystem, Datenteilung, Multiprocessing, **Paging**, umfangreiche Bibliotheken
- Projekt scheiterte am Zeitplan; Bell Labs verließ es 1969, GE verkaufte Computer-Sparte 1970

**UNIX:**

- Ken Thompson (Bell Labs) schrieb **UNICS** (→ UNIX) für DEC PDP-7
- Problem: Portierung in Assembler aufwendig → neue Sprache nötig; B (BCPL) unzureichend
- Dennis Ritchie entwickelt **C**; Thompson + Ritchie schreiben UNIX in C neu
  → **C als Standard für Systemprogrammierung** entsteht
- AT&T durfte nicht ins Computergeschäft → UNIX an Universitäten mit Quellcode (8200 Zeilen C + 900 Zeilen Assembler)
- Unternehmen lizenzierten Quellcode → z.B. **XENIX** (Microsoft-Startup)
- **BSD** (Berkeley Software Distribution): SUN, DEC bauten darauf auf, nicht auf UNIX V

**Linus Torvalds' historische Nachricht (25. Aug 1991):**

```
Newsgroup: comp.os.minix
"I'm doing a (free) operating system (just a hobby, won't be big
and professional like gnu) for 386(486) AT clones."
— Linus Torvalds, torvalds@kruuna.helsinki.fi
```

**POSIX, MINIX und Linux:**

- **POSIX** (1988): Standardisierung der Schnittmenge von System V und BSD (IEEE 1003.1); UNIX-Landschaft bleibt dennoch gespalten (→ „Unix Wars", SCO vs. IBM)
- **MINIX** (Tanenbaum, 1987): Mikrokern, 1600 Zeilen C + 800 Zeilen Assembler; „UNIX für Ausbildungszwecke"
- **Linux** (Torvalds, ab 1991): monolithisch, POSIX-kompatibel, GNU Public License

| Version | Jahr | Codezeilen |
|---------|------|-----------|
| 0.0.1 | 1991 | — |
| 1.0 | 1994 | 150.000 |
| 2.0 | 1996 | 630.000 |
| 3.0 | 2011 | 11.900.000 |

**Unix-Stammbaum (vereinfacht):**

```
Bell Labs → Research UNIX
         → Commercial UNIX (AT&T) → UnixWare, Solaris, HP-UX, AIX
         → BSD → FreeBSD
                → NextStep → Darwin → OS X (Apple)
                → GNU + Minix → Linux (Torvalds)
```

### Vierte Generation (1980–1990)

- Mikrocomputer → **Massenverbreitung von BS**:
  - **CP/M**: plattenbasiert für Intel 8080; dominierte ~5 Jahre den Markt
  - **MS-DOS**: basiert auf DOS von Seattle Computer Products; mit IBM PC gebündelt → **Vermarktung** entscheidend (CP/M separat verkauft)
  - **Mac OS**: Einführung von GUI und benutzerfreundlichen Interfaces
  - **UNIX + X-Windows**: grafische Oberfläche für UNIX (MIT)
- Leistungsfähige Netzwerke → **Verteilte Systeme**; BS überwinden Rechnergrenzen
- Neue Herausforderungen:
  - Einführung von **Lightweight Processes (Threads)**
  - Massivparallele Verarbeitung, Lastverteilung
  - Multimedia (Bilder, Audio, Video)
  - **Eingebettete Systeme** mit Echtzeitanforderungen
  - Interoperabilität in heterogenen Umgebungen

### Mobilgeräte (1995–…)

- Vorläufer: PDAs (PalmOS, Symbian); erste Geräte: HP OmniGo 700LX, Nokia 9000 Communicator
- Neue Anforderung: **sparsame Ressourcenverwendung** (Akku!) ohne Leistungseinbußen
- Seit 2008: Smartphones lösen Feature Phones ab
  - **iOS**: Nachfahre von BSD UNIX + Mach Mikrokern
  - **Android**: modifiziertes Linux + spezielle Systembibliotheken

---

## 4. Virtualisierung

**Grundidee:** Virtualisierung der Prozessorteile, die das BS für Schutzmechanismen nutzt → neue, höhere Kontrollinstanz: **Hypervisor**

- Hypervisor funktioniert wie ein BS, aber auf anderer Abstraktionsebene
- Erlaubt Ausführung **mehrerer BS** gleichzeitig

**Anwendungsfälle:**
- BS entwickeln und debuggen
- Verschiedene Software-Ökosysteme gleichzeitig nutzen
- Kompatibilitätsprobleme umgehen
- Optimale Ressourcennutzung in Rechenzentren

### Virtualisierungsformen

| Form | Beschreibung | Beispiele |
|------|-------------|---------|
| **Emulation** | Simulation sämtlicher HW inkl. CPU | Bochs, QEMU, PearPC |
| **Full Virtualization** | Simulation bestimmter HW (keine CPU-Sim.) | VMware, VirtualBox |
| **Hardware Enabled Virt.** | HW-Unterstützung der Virtualisierung | VMware Fusion, QEMU/KVM |
| **Partial Virtualization** | Nur Teile der HW virtualisiert | IBM M44 (historisch) |
| **Paravirtualization** | Keine HW-Sim., API für Zugriff | Xen |
| **Containerization** | Starke Prozesskisolation im BS | OpenVZ, BSD Jail, Linux cgroups |
| **Application Virt.** | Anwendungen in kleiner virtueller Umgebung | Java VM |

---

## 5. Cloud Computing

**NIST-Definition:**
> „Cloud computing is a model for enabling convenient, on-demand network access to a shared pool of configurable computing resources [...] that can be rapidly provisioned and released with minimal management effort."

| Begriff | Bedeutung |
|--------|----------|
| **Convenient** | Einfache Schnittstelle |
| **On demand / rapidly provisioned** | Kurzfristige Bereitstellung |
| **Shared Pool** | Keine dedizierten Ressourcen; Multi-Tenant |
| **Minimal management effort** | Standard-Service des Providers |

### Schichten des Cloud Computing

```
SaaS  → Software as a Service     (Anwendungen für Endnutzer)
PaaS  → Platform as a Service     (Laufzeitumgebungen: Java, C++, Python)
IaaS  → Infrastructure as a Ser.  (Server, Storage, Netzwerk)
```

### Fog Computing

Zwischenschicht zwischen Cloud und IoT-Geräten — Verarbeitung näher am Gerät reduziert Latenz:

```
Cloud (Data Center)
       │
  Fog Nodes (verteilte Mini-Cloud-Knoten)
       │
IoT Devices / Sensors (Connected Cars, Smart Traffic Lights, ...)
```

---

## ✅ Kernaussagen

- BS sind die älteste und ausgereifteste Software; ihre Mechanismen prägen alle anderen Domains
- CTSS (MIT, 1961) führte Time-Sharing ein → der Job wurde zum **Prozess**
- MULTICS scheiterte → Ken Thompson schrieb UNIX → Dennis Ritchie entwickelte **C**
- Linux begann 1991 als Hobby-Projekt und hat heute ~12 Mio. Codezeilen
- Virtualisierung ermöglicht mehrere BS auf einer Maschine (Hypervisor als neue Kontrollinstanz)
- Cloud = geteilte Ressourcen on-demand; Fog = dezentrale Vorverarbeitung nahe IoT-Geräten

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Betriebssyteme und Prozesse]]: Betriebssysteme und Prozesse — direkte Fortsetzung
- [[VL.03 Scheduling]]: Scheduling — Verwaltung von Prozessen (aus VL.01: Job → Prozess)
- [[SysProg VL.10 Virtualisierung]]: vertieft Hypervisor und Virtualisierungsformen
- [[SysProg VL.10 Microservices]]: Cloud-native Architektur als Weiterentwicklung von Cloud
- [[FoG - Formal-Mathematische]]: Formale Modelle für BS-Zustände und -Übergänge
