**Class:** [[SysProg - Systemprogrammierung]]
**Date:** 24-04-2026
**Topics:** #Prozesse #Threads #Adressraum #Interrupts #Systemaufrufe #Scheduling #Fork #Shell #Bash #Leistung

---
 
## 🎯 Lernziele der Vorlesung

VL.02 behandelt das Kernkapitel **„Betriebssysteme und Prozesse"** — den Weg von Programmen über das BS zur Hardware und wie das BS Prozesse, Threads und die Shell verwaltet.

- **Motivation**: Leistung abhängig von Algorithmus, Sprache, HW — Cache-Lokalität entscheidend
- **BS-Definition**: Mittler zwischen Programmen und Hardware; Mechanismus vs. Policy
- **Modi**: Benutzermodus vs. Systemmodus; Systemaufrufe und Interrupts
- **Prozesse**: Adressraum, Zustände, PCB, Kontextwechsel, Scheduling-Vorschau
- **Threads**: UL/KL/Hybrid; Multithreading-Modelle; Webserver-Beispiel
- **Prozesshierarchien**: fork(), exec(), UNIX-Startsequenz, Zombies/Orphans
- **Shell**: Bash, Pipes, Variablen, Skripte

---

## 1. Motivation und Leistung

Jedes Programm wird auf 0 und 1 abgebildet, im Speicher abgelegt und durch CPU/GPU ausgeführt. Hardware und BS beeinflussen die Leistung — es lohnt sich, beide zu verstehen.

### Drei Ebenen der Programmierung

| Ebene | Beschreibung |
|-------|-------------|
| **Höhere Programmiersprachen** | Python, Java, C, Rust, … — leicht erlernbar, hohe Produktivität |
| **Assembler** | Textuelle Darstellung der CPU-Befehle; Ergebnis der Kompilierung |
| **Hardwaredarstellung** | Binäre Ziffern 0/1 — einzige Sprache, die CPUs ausführen |

### Leistungsfaktoren

| Komponente | Einfluss |
|-----------|---------|
| **Algorithmus** | Anzahl und Art der Lösungsschritte |
| **Sprache, Compiler, Architektur** | Anzahl Befehle; Häufigkeit von Datenzugriffen |
| **CPU, Speicher, Cache** | Ausführungsgeschwindigkeit |
| **Bus, Festplatte, Netzwerk** | Datentransfergeschwindigkeit |

### Beispiel: MacBook Pro 17,2 (Apple M5)

$$\text{Peak} = 4{,}6 \times 10^9 \times 1 \times 10 \times 4 = 184\,000 \text{ MFLOPS}$$

### Matrixmultiplikation ($n = 1024, FLOPS$ $= 2n^3 = 2^{31}$)

| Sprache / Variante | Laufzeit | Leistung      |
| ------------------ | -------- | ------------- |
| Python             | 165 s    | ~13 MFLOPS    |
| C (i,j,k)          | 6,6 s    | ~325 MFLOPS   |
| C (i,k,j) ✅        | 1,85 s   | ~1161 MFLOPS  |
| C (j,k,i)          | 8,5 s    | ~253 MFLOPS   |
| C mit `-O3`        | 0,23 s   | ~10737 MFLOPS |
| Java               | 1,74 s   | ~1234 MFLOPS  |

⚠️ **Schleifenreihenfolge bestimmt Cache-Lokalität** → massiver Leistungsunterschied!

**Vibe-Coding:** Claude und ChatGPT liefern korrekte, aber **nicht die beste** Lösung (i,j,k statt i,k,j).

---

## 2. Betriebssystem

### Definition

Das BS ist **Mittler** zwischen Programmen und Hardware:

- Bereitstellung von Hilfsmitteln für Benutzerprogramme
- Abstraktion von HW-Eigenschaften (z.B. Gerätetreiber)
- Koordination und Vergabe von Ressourcen an mehrere Benutzer

**Basisfunktionen jedes BS:**
- Unterbrechungsverarbeitung (*interrupt handling*)
- Prozessumschaltung
- Betriebsmittelverwaltung (*resource management*)
- Programmallokation (*program allocation*)
- Dateiverwaltung (*file management*)
- Auftragsteuerung (*scheduling*)
- Zuverlässigkeit (*reliability*)

### Mechanismus vs. Policy

| Begriff | Frage | Beispiel (Wecker) |
|--------|-------|-------------------|
| **Mechanismus** | *Wie* wird eine Aufgabe gelöst? | Zeitgeber + Vergleich + Ton auslösen |
| **Policy** | *Welche Parameter* werden eingesetzt? | Wann und mit welchem Ton alarmieren |

Trennung wichtig für Flexibilität: Policies ändern sich häufig — ohne Trennung müsste auch der Mechanismus geändert werden.

### Benutzermodus vs. Systemmodus

| Modus | Zugriff | Verwendung |
|-------|--------|-----------|
| **Benutzermodus** (user mode) | Einige Instruktionen/Register gesperrt | Benutzerprogramme |
| **Systemmodus** (supervisor mode) | Alle Instruktionen und Register erlaubt | Betriebssystem |

**Wechsel unprivilegiert → privilegiert:**
- Auftreten einer Unterbrechung
- Fehler (Division durch 0, verbotene Instruktion, …)
- Explizite Instruktion: x86 `sysenter`, ARM `svc`
- Ausführung springt zu BS-definierten Einsprungpunkten; Registerzustand wird gesichert

**Wechsel privilegiert → unprivilegiert:** jederzeit erlaubt (BS setzt Programm fort).

---

## 2.1 Systemaufrufe und Interrupts

### Ablauf eines Systemaufrufs

1. Anwendung nutzt Bibliothek, um gewünschte Funktion anzufragen
2. Bibliothek übernimmt Parameter und bereitet Systemaufruf vor (Register belegen)
3. Bibliothek wechselt in privilegierten Modus
4. Ausführung springt zur BS-Behandlungsroutine
5. BS prüft Berechtigung und Ressourcen, führt Funktion durch
6. BS setzt Anwendung fort (Rückkehr in unprivilegierten Modus)

### Wichtige UNIX-Signale

| Signal | Bedeutung |
|--------|----------|
| `SIGHUP` | Hangup / Tod des steuernden Prozesses |
| `SIGINT` | Interrupt von Tastatur (Strg+C) |
| `SIGQUIT` | Quit von Tastatur |
| `SIGILL` | Illegale Instruktion |
| `SIGKILL` | Prozess beenden (nicht blockierbar) |
| `SIGTERM` | Beendigungsanfrage |
| `SIGCHLD` | Kindprozess hat Status geändert |
| `SIGSTOP` | Prozess anhalten (nicht blockierbar) |
| `SIGXCPU` | CPU-Zeitlimit überschritten |
| `SIGSYS` | Ungültiger Systemaufruf |
| `SIGPIPE` | Schreiben in Pipe ohne Leser |
| `SIGBUS` | Bus-Fehler (ungültiger Speicherzugriff) |

### Interrupts

Ein **Interrupt** ist ein Signal, das die CPU über das Ende einer Aktivität informiert.

- Systembus hat mindestens eine Unterbrechungsleitung
- Nach **jedem CPU-Befehl** wird geprüft, ob ein Signal anliegt
- Falls ja: sofortiger Sprung zur Interrupt-Behandlungsroutine
- Interrupts können **jederzeit** auftreten

**Zwei Abarbeitungsstrategien:**

| Strategie | Beschreibung |
|-----------|-------------|
| **Sequentiell** | Weitere Interrupts während Behandlung gesperrt (`disable interrupt`); Maskierung auf bestimmte Typen möglich |
| **Geschachtelt** | Interrupts höherer Priorität dürfen laufende Behandlung unterbrechen (statische Prioritätsklassen) |

---

## 2.2 Prozesse

### Definition

Ein **Prozess** ist eine Instanz eines laufenden Programms, definiert durch:

1. **Adressraum** und ggf. weitere Ressourcen
2. **Auszuführendes Programm**
3. **Ein oder mehrere Threads** (Aktivitätsträger)

$$\text{Prozess} = \text{Programm} + \text{Daten} + \text{Adressraum} + \text{Ressourcen}$$

### Adressräume

| Typ | Beschreibung |
|-----|-------------|
| **Physischer Adressraum** | Einmal pro Maschine; RAM, ROM, E/A-Geräte |
| **Virtueller Adressraum** | Einmal pro Prozess; vom BS erzeugt; i.d.R. größer als physischer Speicher |

**Aufbau des virtuellen Adressraums:**

```
0x00000000  [Lücke für NULL-Zeiger]
            Programmtext        (Instruktionen)
            Statische Daten     (globale Variablen, static)
            Heap                (dynamisch, wächst aufwärts)
            Stack               (dynamisch, wächst abwärts)
0xFFFFFFFF  BS-Text und -Daten  (nur privilegierter Modus)
            E/A-Geräte
```

**Code-Sharing:** Mehrere Prozesse können denselben Programmcode teilen, haben aber jeweils private Datenbereiche.

### Prozessausführung

**Stapelbetrieb:** Prozesse sequentiell abgearbeitet → CPU-Leerlauf bei E/A.

**Multiprogrammierung:** Bei E/A-Warten wird nächster bereiter Prozess gestartet.

CPU-Auslastung bei Grad $n$ und E/A-Warteanteil $p$:

$$A = 1 - p^n$$

### Prozesszustände

```
             Add
  ─────────────────► Bereit
                      │  ▲
               Assign │  │ Resign
                      ▼  │
                    Laufend ──── Retire ──► Beendet
                      │
                Block │  Ready
                      ▼  ▲
                    Blockiert

  Swap out: Bereit/Blockiert → Ausgelagert
  Swap in:  Ausgelagert → Bereit/Blockiert
```

| Zustand | Beschreibung |
|---------|-------------|
| **Bereit** (Ready) | Hat alle Ressourcen, wartet auf CPU |
| **Laufend** (Running) | Wird aktuell auf CPU ausgeführt |
| **Blockiert** (Waiting) | Wartet auf Bedingung (z.B. E/A-Ende) |
| **Beendet** (Terminated) | Fertig, alle Ressourcen freigegeben |
| **Ausgelagert** | Adressraum bei Speichermangel auf Festplatte |

**Zustandsübergänge:**

| Übergang | Auslöser |
|---------|---------|
| **Add** | Neu erzeugter Prozess → Bereit |
| **Assign** | Kontextwechsel → Prozessor zugeteilt |
| **Block** | Blockierende E/A oder Synchronisation |
| **Ready** | Blockierende Operation beendet |
| **Resign** | Zeitscheibe abgelaufen oder freiwillige Abgabe |
| **Retire** | Prozess terminiert, Ressourcen freigegeben |

### Prozesskontrollblock (PCB)

Der PCB ist die BS-Datenstruktur zur Prozessverwaltung:

- **PID** (Prozessidentifikation)
- **Besitzer** (Nutzerkennung)
- **Gesicherte Registerwerte** (wenn nicht Laufend, inkl. Befehlszähler)
- **Zustandsvariable**
- **Zugeteilte Betriebsmittel**
- **Konfiguration des virtuellen Adressraums**
- **Verweise auf Eltern- und Kindprozesse**

### Prozessumschaltung (Context Switch)

**Prozess A → Prozess B:**

1. Registerinhalte in $\text{PCB}_A$ sichern (inkl. Befehlszähler)
2. Zustand von $A$ aktualisieren (→ Blockiert/Bereit)
3. Zustand von $B$ aktualisieren (→ Laufend)
4. Virtuellen Adressraum auf $\text{PCB}_B$ umschalten
5. Registerinhalte aus $\text{PCB}_B$ laden
6. $B$ an gespeichertem Befehlszähler fortsetzen

### Scheduling (Vorschau → Kapitel 3)

Strategien zur Auswahl Bereit → Laufend:
- Prozessnummer (zyklisch)
- Ankunftsreihenfolge (FIFO)
- Fairness und Priorität (konstant / dynamisch)
- Einhaltung von Fertigstellungspunkten (Deadlines)

### Nebenläufigkeit vs. Parallelität

| Begriff | Bedeutung |
|--------|----------|
| **Nebenläufigkeit** | Logisch simultan; verzahnt auf einer CPU |
| **Parallelität** | Physisch simultan; braucht mind. 2 CPUs/Kerne |

Parallelität $\subset$ Nebenläufigkeit. Beide setzen kontrollierten Zugang zu gemeinsamen Ressourcen voraus.

---

## 2.3 Threads (Leichtgewichtsprozesse)

### Definition

Ein **Thread** ist ein Kontrollfluss innerhalb eines Prozesses:

- Operiert im **selben virtuellen Adressraum** wie alle anderen Threads des Prozesses
- Ausnahme: **eigener Stack**
- Eigener Zustand, Befehlszähler, Registerwerte → gespeichert in **Threadtabelle** (nicht PCB)
- Erzeugung eines Prozesses impliziert immer mind. einen Thread

### Single-Threaded vs. Multi-Threaded

| Modell | Beispiele |
|--------|----------|
| 1 Prozess, 1 Thread | MS-DOS |
| Mehrere Prozesse, 1 Thread/Prozess | Ältere UNIX-Versionen, Mac OS |
| Mehrere Prozesse, mehrere Threads/Prozess | Windows, Solaris, Linux |
| 1 Prozess, mehrere Threads | Java Runtime Engine |

### Beispiel: Webserver

**Single-threaded:** Anfragen sequenziell → bei Cache-Miss blockiert gesamter Prozess.

**Multi-threaded:**

```c
// Dispatcher-Thread
while (TRUE) {
    get_next_request(&buf);
    handoff_work(&buf);
}

// Worker-Thread
while (TRUE) {
    wait_for_work(&buf);
    look_in_cache(&buf, &page);
    if (page_not_in_cache(&page))
        read_page_from_disk(&buf, &page);
    return_page(&page);
}
```

→ Hohes Maß an Parallelität zwischen Lese- und Rechenzugriffen.

### Threadtypen

| Typ | Realisierung | Vorteile | Nachteile |
|-----|-------------|---------|----------|
| **UL-Threads** | Im Benutzeradressraum; BS-unbekannt | Sehr schnell; freies Scheduling | Blockierender Syscall blockiert alle; kein Multicore |
| **KL-Threads** | Im BS-Kernadressraum | Kein Einfluss blockierender Syscalls; Multicore | Verwaltung teuer (Systemaufruf nötig) |
| **Hybrid** | Mehrere UL auf mehrere KL | Kompromiss aus beiden | Komplexe Randfälle |

### Multithreading-Modelle

| Modell | Zuordnung | Beispiele |
|--------|----------|----------|
| **Many-to-One** | Alle UL auf 1 KL | Historisch |
| **One-to-One** | 1 UL = 1 KL | Windows, Linux |
| **Many-to-Many** | Mehrere UL auf mehrere KL | Hybrid-Systeme |

---

## 2.4 Prozesshierarchien

### fork() und exec()

**`fork()`** erzeugt eine perfekte Kopie (Child) des aufrufenden Prozesses (Parent):

- Gleiches Programm, gleiche Daten, gleicher Programmzähler, gleicher Eigentümer, gleiche offenen Dateien
- **Unterschiedliche PID**

**Rückgabewert von `fork()`:**

$$\text{fork()} = \begin{cases} \text{PID des Child} > 0 & \text{im Parent} \\ 0 & \text{im Child} \\ < 0 & \text{Fehlerfall} \end{cases}$$

```c
pid_t p = fork();
if (p == 0) {
    /* child */
} else if (p > 0) {
    /* parent */
}
```

**`execl()`** lädt und startet ein neues Programm im aktuellen Prozess:

```c
execl("/usr/bin/cp", "cp", "a.txt", "b.txt", NULL);
```

- `path`: Pfad zur ausführbaren Datei
- `arg0`: Programmname; `arg1, ...`: Argumente (mit `NULL` terminiert)
- Rückgabewert $-1$ im Fehlerfall

**Typisches Muster:**

```c
if (fork() == 0) {
    execl("/usr/bin/cp", "cp", "a.txt", "b.txt", NULL);
    abort();  // nur falls execl() scheitert
}
wait(NULL);
printf("copy completed\n");
```

**Mehrfaches fork():**

```c
void fork2() {
    printf("L0\n");
    fork();
    printf("L1\n");
    fork();
    printf("Bye\n");
}
// Ausgabe: L0, L1, L1, Bye, Bye, Bye, Bye
```

### Prozessbeziehungen

- **Eltern-Kind**: Ein Prozess erzeugt einen weiteren
- **Vorgänger-Nachfolger**: Prozess B startet erst nach Ende von A
- **Kommunikation**: Zwei Prozesse kommunizieren miteinander
- **Warten**: Prozess wartet auf Ergebnis eines anderen
- **Dringlichkeit**: Ein Prozess hat höhere Priorität

### Prozesshierarchie UNIX

```
init
├── Daemons (z.B. sshd)
└── getty → login → bash
    ├── Child
    │   └── Grandchild
    └── Child
```

- **Zombies**: Kind terminiert vor Eltern → Tabelleneintrag bleibt bis Eltern enden
- **Orphans**: Eltern terminiert vor Kind → Kind nicht mehr erreichbar
- **Windows**: kein Konzept einer Prozesshierarchie (Handle statt Baum; weitergabe an andere Prozesse möglich)

### UNIX-Startsequenz

```
Reset
→ Bootstrapprogramm (ROM)
→ Bootblock (Plattenblock 0)
→ Kernel (/boot/vmlinux)
→ Prozess 0 (manuell erzeugt durch Kernel)
→ fork() → Prozess 1
→ execl(/sbin/init) → init
→ fork() + Daemons (/etc/inittab) + getty
→ execl() → login
→ execl() → Shell (bash / zsh / …)
```

---

## 2.5 Shell

### Grundlagen

Die Shell ist ein Programm zum Starten und Steuern von Prozessen ohne BS-GUI.

| Shell | Herkunft | Besonderheit |
|-------|---------|-------------|
| `sh` (Bourne Shell) | Unix V7, 1977 | Grundlage moderner Shells |
| `csh` | BSD, 1979 | C-Syntax |
| `bash` | GNU, Ende 80er | Standard Linux |
| `zsh` | BSD | Standard macOS |
| PowerShell | Windows | KornShell-basiert, erweitert |

### Basisfunktionen

- Scripts erstellen und starten
- Bedingungen (`if`, `case`) und Schleifen (`while`, `for`)
- Interne Befehle (`cd`, `read`) und Variablen (`$HOME`)
- Umgebungsvariablen manipulieren
- E/A-Umlenkung und Pipes
- Job control (Hintergrund, Stoppen, Fortsetzen)
- Command history und Tab-Completion
- Testen von Dateieigenschaften (`test`)

### Wichtige Bash-Befehle

| Befehl | Bedeutung |
|--------|----------|
| `ls` | Verzeichnisinhalt anzeigen |
| `pwd` | Aktuelles Verzeichnis anzeigen |
| `cd` | Verzeichnis wechseln (`~`, `.`, `..`) |
| `mkdir` / `rmdir` | Verzeichnis erstellen / löschen |
| `cp` / `mv` / `rm` | Kopieren / Verschieben / Löschen |
| `man <cmd>` | Hilfe zu einem Befehl |

### Pipes und E/A-Umleitung

```bash
ls | wc -l                           # Anzahl Dateien
cat beispiel.txt | grep okao         # Zeilen filtern

wc < beispiel.txt                    # stdin aus Datei
wc < beispiel.txt > ergebnis.txt     # stdout in Datei (überschreiben)
wc < beispiel.txt >> ergebnis.txt    # stdout anhängen
./myCode < beispiel.txt 2> fehler.txt # stderr in Datei
```

| Symbol | Bedeutung |
|--------|----------|
| `<` | stdin aus Datei |
| `>` | stdout in Datei (überschreiben) |
| `>>` | stdout anhängen |
| `2>` | stderr in Datei |

### Variablen

```bash
NAME="Linux"
echo $NAME
export PATH="$PATH:/home/sysprog/bin/"
echo Anzahl Dateien: "$(ls -l | wc -l)"
```

| Variable | Bedeutung |
|---------|----------|
| `$0`–`$9` | Skriptname und Argumente |
| `$@` | Alle Argumente |
| `$PATH` | Suchpfade für ausführbare Dateien |
| `$HOME` | Heimverzeichnis |
| `$PWD` | Aktuelles Verzeichnis |
| `$PPID` | PID des Elternprozesses |

### Shell-Skripte

```bash
#!/usr/bin/bash

if [ "${1}" = "${2}" ]; then
    echo "Parameter identisch"
else
    echo "Parameter nicht identisch"
fi

for j in $(seq 3 6); do
    sum=$(($j + $j))
    echo $sum
done

while [ Bedingung ]; do
    Befehle
done
```

```bash
chmod +x myscript    # ausführbar machen
./myscript arg1 arg2
```

**Vergleiche:**

| Typ | Gleich | Ungleich | Größer | Kleiner |
|-----|--------|---------|--------|---------|
| **String** | `=` | `!=` | — | — |
| **Integer** | `-eq` | `-ne` | `-gt` / `-ge` | `-lt` / `-le` |

---

## 📌 Wichtige Formeln

| Formel | Bedeutung |
|--------|----------|
| $\text{Peak MFLOPS} = f \times \text{CPUs} \times \text{Kerne} \times \text{FP/Cycle}$ | Theoretische CPU-Leistung |
| $A = 1 - p^n$ | CPU-Auslastung bei Multiprogrammierung |

---

## ✅ Kernaussagen

- BS = Mittler zwischen Anwendungen und Hardware; trennt Benutzermodus von Systemmodus
- Interrupts können jederzeit auftreten → BS sichert Prozessorzustand und springt zur Behandlungsroutine
- Prozesse haben eigene Adressräume; Threads teilen Adressraum, haben jedoch eigenen Stack
- `fork()` kopiert Prozess vollständig; `execl()` ersetzt Programm im aktuellen Prozess
- Schleifenreihenfolge bei Matrixoperationen ist massiv performance-relevant (Cache-Lokalität!)
- Blockierender Syscall bei UL-Threads blockiert **alle** Threads des Prozesses
- Zombies und Orphans entstehen bei falscher Prozesssynchronisation

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.01 Geschichte Betriebssytem]]: Geschichte der BS; der Job wurde zum Prozess (CTSS)
- [[VL.03 Scheduling]]: Scheduling-Strategien (Bereit → Laufend)
- [[VL.04 Koordination nebenläufiger Prozesse]]: Synchronisation (Semaphore) — Prioritätsinvertierung in der Praxis
- [[VL.06 Speicher- und Adressraumverwaltung]]: Speicherverwaltung — virtueller Adressraum, Paging, Swapping
- [[VL.02 Inferenz und Regelschemata]]: Inferenzregeln für induktive Definitionen von Zustandsmaschinen
