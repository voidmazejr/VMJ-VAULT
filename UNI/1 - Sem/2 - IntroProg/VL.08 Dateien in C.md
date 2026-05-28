**Class:** [[IntroProg]]  
**Date:** VL.8  
**Topics:** #DateienInC #Dateisysteme #CStreams #fopen #fprintf #fscanf #fgets #sscanf #Fehlerbehandlung #perror

---
## 🎯 Lernziele der Vorlesung

Diese Vorlesung behandelt den **Umgang mit Dateien in C** für dauerhafte Datenspeicherung und -verarbeitung.

- Verständnis von **Dateien und Dateisystemen**
- **Dateiattribute** und **Operationen**
- **Verzeichnisse** und **Pfadnamen**
- **C-Streams** (`stdin`, `stdout`, `stderr`)
- **Datei-I/O**: `fopen`, `fclose`, `fprintf`, `fscanf`
- **Sichere Eingabe** mit `fgets` und `sscanf`
- **Fehlerbehandlung** mit `perror`

---

## 1. Dateien und Dateisysteme

### Was ist eine Datei?

Eine **Datei** ist eine **Sammlung logischer Dateneinheiten**, die dauerhaft auf einem Speichermedium gespeichert sind.

**Dateisysteme** ermöglichen:
- **Abstraktion** von Hintergrundspeichern (Platten, USB, CD-ROM, etc.)
- **Einheitliche Schnittstelle** für Programme
- Dauerhafte Speicherung von Daten, Code, Programmen

### Dateiattribute

Jede Datei hat **Metadaten**:

| Attribut | Bedeutung |
|----------|-----------|
| **Name** | Symbolischer Name (vom Benutzer lesbar) |
| **Größe** | Länge in Bytes oder Blöcken |
| **Zeitstempel** | Erstellung, letzte Änderung |
| **Rechte** | Zugriffsrechte (rwx) |
| **Eigentümer** | Benutzer-ID |

**Beispiel** (`ls -l`):
```bash
-rw-r--r-- 1 manfred user 1047 2021-09-16 15:56 hello.c
drwxr-xr-x 10 manfred user 2048 2021-08-21 12:41 progintro
```

**Erklärung:**
- `-rw-r--r--`: Datei, Owner: read+write, Gruppe: read, Andere: read
- `drwxr-xr-x`: Verzeichnis (d), Owner: rwx, Gruppe: rx, Andere: rx
- `1047`: Größe in Bytes
- `2021-09-16 15:56`: Letzter Änderungszeitpunkt

---

## 2. Operationen auf Dateien

### Grundlegende Operationen

- **create**: Datei erzeugen
- **open**: Datei öffnen
- **read**: Aus Datei lesen
- **write**: In Datei schreiben
- **close**: Datei schließen
- **delete**: Datei löschen

⚠️ **Wichtig:** In C arbeitet man **nie direkt mit Dateien**, sondern über **Streams** (`FILE*`).

---

## 3. Verzeichnisse

### Was ist ein Verzeichnis?

Ein **Verzeichnis** (Directory/Folder) ist eine **Sammlung von Dateien und Verzeichnissen**.

**Attribute:** Ähnlich wie Dateien (Name, Größe, Datum, Eigentümer, Rechte)

### Operationen auf Verzeichnissen

- **Suchen** einer Datei/eines Verzeichnisses
- **Erzeugen** (`mkdir`)
- **Löschen** (`rmdir`, `rm`)
- **Umbenennen** (`mv`)
- **Durchlaufen** des Dateisystems
- **Auslesen** der Einträge (`ls`)

### Wichtige Unix-Befehle

| Befehl | Funktion |
|--------|----------|
| `ls` | Verzeichnisinhalt anzeigen |
| `cp` | Datei kopieren |
| `mv` | Datei verschieben/umbenennen |
| `rm` | Datei löschen |
| `mkdir` | Verzeichnis erstellen |
| `find` | Dateien suchen |

---

## 4. Verzeichnisstruktur und Pfadnamen

### Baumstruktur

```
/ (root)
├── etc/
│   └── passwd
├── home/
│   ├── manfred/
│   │   └── test/
│   │       ├── file1
│   │       └── file2
│   └── qdoctor/
├── usr/
│   ├── bin/
│   │   ├── ls
│   │   └── mkdir
│   └── sbin/
└── tmp/
```

### Unix-Pfadnamen

**Besondere Verweise:**
- `.` → Aktuelles Verzeichnis
- `..` → Elternverzeichnis

**Mehrere Pfade für dieselbe Datei möglich:**
```
/home/manfred/test
/home/manfred/test/.
/home/manfred/test/../test
```

Alle drei Pfade zeigen auf **dasselbe Verzeichnis**.

---

## 5. C-Streams

### Standard-Streams

Jedes laufende C-Programm hat **drei vordefinierte Streams**:

| Stream   | Beschreibung    | Standardziel |
| -------- | --------------- | ------------ |
| `stdin`  | Standardeingabe | Tastatur     |
| `stdout` | Standardausgabe | Bildschirm   |
| `stderr` | Fehlerausgabe   | Bildschirm   |

```
┌─────────┐
│ myProg  │
│         │
│  stdin  │ ← Tastatur
│  stdout │ → Bildschirm
│  stderr │ → Bildschirm
└─────────┘
```

### Stream-Umleitung

Streams können **umgeleitet** werden:

```bash
./prog < input.txt      # stdin von Datei lesen
./prog > output.txt     # stdout in Datei schreiben
./prog 2> error.txt     # stderr in Datei schreiben
./prog &> all.txt       # stdout UND stderr in Datei
```

### Pipes

Ausgabe eines Programms als Eingabe für ein anderes:

```bash
./prog1 | sort > output.txt
```

**Unix-Tools für Pipes:**
`cat`, `sort`, `grep`, `wc`, `tail`, `cut`, `sed`, `uniq`, `more`, `less`

---

## 6. Formatierte Ausgabe: fprintf

### Syntax

```c
int fprintf(FILE *stream, const char *format, ...);
```

**Wie `printf`, aber Ausgabe erfolgt auf einen Stream.**

### Äquivalenz

```c
fprintf(stdout, ...) ≙ printf(...)
```

### Beispiele

```c
fprintf(stdout, "Hello world\n");
fprintf(stdout, "Wert von i: %d\n", i);
fprintf(stdout, "a(%d) + b(%d) = %d\n", a, b, a+b);
```

---

## 7. Formatierte Eingabe: fscanf

### Syntax

```c
int fscanf(FILE *stream, const char *format, ...);
```

**Liest von Stream** und versucht, Eingabe gemäß Format zu parsen.

**Rückgabewert:** Anzahl erfolgreich gelesener Werte oder `EOF`.

### Äquivalenz

```c
fscanf(stdin, ...) ≙ scanf(...)
```

### Beispiele

```c
int a, b;
fscanf(stdin, "%d %d", &a, &b);

float x;
fscanf(stdin, "%f", &x);

char c;
fscanf(stdin, "%c", &c);
```

⚠️ **Problem:** `fscanf` ist **fehleranfällig** bei ungültigen Eingaben!

---

## 8. Dateien öffnen und schließen

### Öffnen: fopen

```c
FILE *fopen(const char *path, const char *mode);
```

**Modi:**

| Modus | Bedeutung |
|-------|-----------|
| `"r"` | Lesen (read) |
| `"w"` | Schreiben (write) – **überschreibt** existierende Datei! |
| `"a"` | Anhängen (append) – schreibt am Ende |

### Beispiele

```c
FILE *fp_in, *fp_out;

// Datei zum Lesen öffnen
fp_in = fopen("./datei.txt", "r");

// Datei zum Schreiben öffnen (überschreibt!)
fp_out = fopen("./output.txt", "w");

// Am Ende anhängen
fp_out = fopen("./output.txt", "a");
```

### Schließen: fclose

```c
int fclose(FILE *stream);
```

**Wichtig:**
- Beendet Operationen **fehlerfrei**
- Gibt **Ressourcen frei** (im Betriebssystem)
- **Muss immer aufgerufen werden!**

```c
fclose(fp_in);
```

---

## 9. Fehlerbehandlung mit perror

### Problem

`fopen` kann **fehlschlagen** (Datei existiert nicht, keine Rechte, etc.).

### Lösung: Immer prüfen!

```c
#include <errno.h>

FILE *fp = fopen("datei.txt", "r");

if (fp == NULL) {
    perror("Fehler beim Öffnen der Datei");
    return 1;
}

// ... Datei verwenden ...

fclose(fp);
```

### perror

```c
void perror(const char *msg);
```

- Gibt die **letzte Systemfehlermeldung** auf `stderr` aus
- Nutzt die globale Variable `errno`

**Ausgabe-Format:**
```
Fehler beim Öffnen der Datei: No such file or directory
```

⚠️ **Ohne Fehlerbehandlung ist dein Programm unbrauchbar!**

---

## 10. Datei lesen und ausgeben

### Beispiel: Lesen und auf stdout ausgeben

```c
FILE *fp = fopen("datei.txt", "r");
int a, b;

if (fp == NULL) {
    perror("Fehler beim Öffnen");
    return 1;
}

while (fscanf(fp, "%d %d\n", &a, &b) != EOF) {
    printf("%d %d\n", a, b);
}

fclose(fp);
```

**`EOF` (End Of File):**
- Wird zurückgegeben, wenn nichts mehr gelesen werden kann
- Signalisiert Dateiende oder Fehler

---

## 11. Datei lesen und in andere Datei schreiben

```c
FILE *fpin = fopen("datei_in.txt", "r");
FILE *fpout = fopen("datei_out.txt", "a");
int a, b;

if (fpin == NULL || fpout == NULL) {
    perror("Fehler beim Öffnen");
    return 1;
}

while (fscanf(fpin, "%d %d\n", &a, &b) != EOF) {
    fprintf(fpout, "%d + %d = %d\n", a, b, a + b);
}

fclose(fpin);
fclose(fpout);
```

---

## 12. Problem: Fehlerhafte Eingabedaten

### Probleme mit scanf/fscanf

- Eingabedaten entsprechen **nicht dem erwarteten Format**
- Z.B. String statt Zahl
- `scanf`/`fscanf` können **hängen bleiben** oder falsche Werte liefern

### Lösung: fgets + sscanf

**Strategie:**
1. **Ganze Zeile lesen** mit `fgets`
2. **String parsen** mit `sscanf`

---

## 13. Sichere Eingabe: fgets

### Syntax

```c
char *fgets(char *buf, int n, FILE *stream);
```

**Funktionsweise:**
- Liest **bis zum ersten Newline** `\n` (inklusive!)
- **Maximal `n-1` Zeichen**
- Fügt **`\0`** am Ende hinzu
- Oder bis **EOF**

**Rückgabewert:**
- Pointer auf `buf` bei Erfolg
- `NULL` bei Fehler oder EOF

### Beispiel

```c
char buf[200];
char *h = fgets(buf, 200, stdin);

if (h == NULL) {
    fprintf(stderr, "Error in fgets\n");
    exit(1);
}
```

🚫 **Finger weg von `gets()`!**
- Liest **unbegrenzt** → **Buffer Overflow**!
- Extrem unsicher, **nie verwenden**!

---

## 14. Sichere Eingabe: fgets + sscanf

### Vollständiges Beispiel

```c
char buf[200];
int a, b;

// Schritt 1: Ganze Zeile lesen
char *h = fgets(buf, 200, stdin);
if (h == NULL) {
    fprintf(stderr, "Input error\n");
    exit(1);
}

// Schritt 2: String parsen
int ret = sscanf(buf, "%d %d", &a, &b);
if (ret == 2) {
    printf("Read 2 integers: %d %d\n", a, b);
} else {
    fprintf(stderr, "Error reading 2 integers\n");
}
```

### Vorteile

✅ **Kontrollierte Eingabe** (keine Buffer Overflows)  
✅ **Fehlerhafte Eingaben** bleiben nicht im Buffer hängen  
✅ **Rückgabewert** von `sscanf` zeigt Anzahl erfolgreich geparster Werte

---

## 15. Kombination: Datei lesen mit fgets/sscanf

```c
FILE *fp = fopen("numbers.txt", "r");
char buf[200];
int a, b;

if (fp == NULL) {
    perror("Fehler beim Öffnen");
    return 1;
}

while (fgets(buf, 200, fp) != NULL) {
    int ret = sscanf(buf, "%d %d", &a, &b);
    if (ret == 2) {
        printf("%d + %d = %d\n", a, b, a + b);
    } else {
        fprintf(stderr, "Ungültige Zeile: %s", buf);
    }
}

fclose(fp);
```

---

## 16. Stream-Umleitung und Pipes

### Umleitung

```bash
# Eingabe von Datei
./prog < input.txt

# Ausgabe in Datei
./prog > output.txt

# Beide kombinieren
./prog < input.txt > output.txt

# Fehlerausgabe separat
./prog 2> errors.txt

# Alles in eine Datei (bash)
./prog &> all.txt
```

### Pipes

```bash
# Ausgabe von prog1 an sort weiterleiten
./prog1 | sort > sorted.txt

# Mehrere Pipes kombinieren
cat file.txt | grep "error" | wc -l
```

---

## 📌 Zusammenfassung

### Dateisystem-Konzepte

- **Datei:** Dauerhafte Speicherung von Daten
- **Verzeichnis:** Sammlung von Dateien und Verzeichnissen
- **Pfade:** Absolute (`/home/user/file`) oder relativ (`./file`)

### C-Streams

| Stream | Beschreibung | Umleitung |
|--------|--------------|-----------|
| `stdin` | Standardeingabe | `< file` |
| `stdout` | Standardausgabe | `> file` |
| `stderr` | Fehlerausgabe | `2> file` |

### Wichtige Funktionen

| Funktion | Verwendung |
|----------|------------|
| `fopen(path, mode)` | Datei öffnen |
| `fclose(fp)` | Datei schließen |
| `fprintf(fp, fmt, ...)` | Formatierte Ausgabe |
| `fscanf(fp, fmt, ...)` | Formatierte Eingabe (unsicher!) |
| `fgets(buf, n, fp)` | Zeile lesen (sicher) |
| `sscanf(buf, fmt, ...)` | String parsen |
| `perror(msg)` | Fehlermeldung ausgeben |

### Sichere vs. Unsichere Methoden

| Unsicher ❌ | Sicher ✅ |
|------------|---------|
| `scanf` | `fgets` + `sscanf` |
| `gets` | `fgets` |
| Keine Fehlerprüfung | Immer `if (fp == NULL)` prüfen |

### Best Practices

1. **Immer Fehlerbehandlung** (`if (fp == NULL)`)
2. **Immer `fclose()` aufrufen**
3. **`fgets` + `sscanf`** statt `fscanf` für robuste Eingabe
4. **Nie `gets()` verwenden** (Buffer Overflow!)
5. **Rückgabewerte prüfen** (`EOF`, `NULL`)

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.01 Algorithmen-pseudocode]] – Datenverarbeitung aus Dateien
- [[VL.04 Einfache Datenstrukturen]] – Structs für komplexe Dateninhalte


---

## Cheat Sheet: Datei-I/O in C

```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    FILE *fp;
    char buf[200];
    int a, b;
    
    // Datei öffnen mit Fehlerbehandlung
    fp = fopen("data.txt", "r");
    if (fp == NULL) {
        perror("Fehler beim Öffnen");
        return 1;
    }
    
    // Sichere Zeilen-Eingabe
    while (fgets(buf, 200, fp) != NULL) {
        int ret = sscanf(buf, "%d %d", &a, &b);
        if (ret == 2) {
            printf("%d + %d = %d\n", a, b, a + b);
        } else {
            fprintf(stderr, "Ungültige Zeile: %s", buf);
        }
    }
    
    // Datei schließen
    fclose(fp);
    return 0;
}
```