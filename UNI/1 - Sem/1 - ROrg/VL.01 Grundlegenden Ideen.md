**Class:** [[ROrg]]  
**Date:** 2025  
**Topics:** #Computerrevolution #Klassen #Hardware #Software #Abstraktion #ISA #Prozessor

---

## 🎯 Lernziele der Vorlesung

Grundlegende Konzepte der Rechnerorganisation verstehen: von der Hardware-Ebene bis zur Software-Abstraktion.

- **Klassen von Computersystemen** und deren Anwendungsbereiche
- **Hardware- und Software-Ebenen** verstehen
- Von **Hochsprache zu Maschinensprache**
- **Klassische Computerkomponenten** kennen
- Konzept der **Abstraktion** in der Rechnerorganisation
- **Instruction Set Architecture (ISA)** als zentrale Schnittstelle

---

## 1. Die Computerrevolution

### Entwicklung der letzten 35 Jahre

Technologien, die vor 35 Jahren Science-Fiction waren:
- Laptops (z.B. Toshiba T1100 von 1985)
- World Wide Web (WWW)
- Handys/Smartphones
- Digitales Fernsehen/Kameras
- Forschung am menschlichen Genom
- Bilderkennung durch Künstliche Intelligenz

**Wichtig:** Alle diese Anwendungen sind nur durch die Entwicklung der Rechnertechnologie möglich geworden!

---

## 2. Klassen von Computersystemen

### Übersicht der drei Hauptklassen

| Klasse | Verkaufszahlen/Jahr | Eigenschaften |
|--------|---------------------|---------------|
| **Arbeitsplatzrechner** (Desktop) | ~100 M | Gute Leistung zu akzeptablen Preisen, Software von Drittanbietern |
| **Server** | ~5 M | Große Rechenleistung, höheres Maß an Erweiterbarkeit, Cloud-Infrastrukturen |
| **Eingebettete Rechner** (Embedded) | ~1000 M | Größte Bandbreite, in Waschmaschinen, KFZ, Handys, TVs |

### Verkaufszahlen von Prozessoren (1998-2002)

**Eingebettete Computer:**
- 1998: 290 M → 2002: 1122 M
- **Größte Anzahl** an verkauften Prozessoren

**Desktop-PCs:**
- 1998: 93 M → 2002: 131 M

**Server:**
- 1998: 3 M → 2002: 5 M

**Wichtig:** Bei Desktop und Server werden komplette Systeme gezählt (können mehrere Prozessorkerne haben), bei Embedded die tatsächliche Anzahl der Prozessoren.

---

## 3. Hardware- und Software-Ebenen

### Hierarchische Darstellung

```
┌─────────────────────────┐
│  Anwendungssoftware     │
│  ┌───────────────────┐  │
│  │ Systemsoftware    │  │
│  │  ┌─────────────┐  │  │
│  │  │  Hardware   │  │  │
│  │  └─────────────┘  │  │
│  └───────────────────┘  │
└─────────────────────────┘
```

**Definitionen:**

**Systemsoftware:** Software, die allgemein nützliche Dienste bereitstellt
- Betriebssysteme
- Compiler
- Assembler

**Anwendungssoftware:** Besteht häufig aus mehreren Software-Ebenen

---

## 4. Von Hochsprache zu Maschinensprache

### Übersetzungshierarchie

**Beispiel: swap-Funktion**

**1. Hochsprachenprogramm (C):**
```c
void swap(int v[], int k)
{
    int temp;
    temp = v[k];
    v[k] = v[k+1];
    v[k+1] = temp;
}
```

↓ **C Compiler**

**2. Assemblerprogramm (MIPS):**
```assembly
swap:
    sll $2,$5,4
    add $2,$4,$2
    lw $15,0($2)
    lw $16,4($2)
    sw $16,0($2)
    sw $15,4($2)
    jr $31
```

↓ **Assembler**

**3. Binärer Maschinencode (MIPS):**
```
00000000101000010000000000011000
00000000100011100001100000100001
10001100011000100000000000000000
10001100111100100000000000000100
101011001111001000000000000000...
```

**MIPS:** Microprocessor without interlocked pipeline stages („Mikroprozessor ohne verschränkte Pipeline-Stufen")

---

## 5. Klassische Computerkomponenten

### Die 5 Hauptkomponenten

$$\boxed{\text{Computer} = \text{Eingabe} + \text{Ausgabe} + \text{Speicher} + \text{Datenpfad} + \text{Steuerwerk}}$$

**1. Eingabegeräte (Input Devices)**
- Maus, Tastatur, Scanner, etc.

**2. Ausgabegeräte (Output Devices)**
- Bildschirm (Display), Drucker, etc.

**3. Speicher**
- **Intern (flüchtig):**
  - DRAM (Dynamic RAM)
  - SRAM (Static RAM)
- **Extern (nicht flüchtig):**
  - Festplatte (Hard Disk)
  - CD/DVD
  - Diskettenlaufwerk

**4. Datenpfad (Datapath)**
- Führt Operationen aus
- Die **"Muskeln"** eines Prozessors

**5. Leitwerk/Steuerung (Control)**
- Sendet Signale, welche die Operationen bestimmen
- Das **"Gehirn"** eines Prozessors

### Der Prozessor (CPU)

$$\boxed{\text{CPU} = \text{Datenpfad} + \text{Steuerwerk}}$$

**CPU = Central Processing Unit**

**Beispiel:** Intel Core 2 Extreme Quadcore (2006)
- 2 × 291 Millionen Transistoren
- Unmöglich zu verstehen, wenn man Transistoren einzeln betrachtet
- **Benötigt Abstraktion auf vielen Ebenen!**

---

## 6. Abstraktion

### Definition

$$\boxed{\begin{align}
\text{Abstraktion} &= \text{Modell, bei dem Details der unteren Ebenen} \\
&\phantom{=} \text{vorübergehend ausgeblendet werden}
\end{align}}$$

**Zweck:** Entwicklung komplexer Systeme erleichtern

### Abstraktionsebenen in der Rechnerorganisation

**1. Schaltkreisebene**
- Beispiel: MUX (Multiplexer) statt einzelner Transistoren/Gatter

**2. Befehlssatzarchitektur (ISA)**
- Digitaler Rechner = Satz von Befehlen, den er ausführen kann

**3. Programmabstraktion**
- Funktionen, Klassen, Objekte

**4. Datenabstraktion**
- Datenstrukturen: Sets, Queues, Listen

---

## 7. Instruction Set Architecture (ISA)

### Definition und Bedeutung

$$\boxed{\text{ISA} = \text{Schnittstelle zwischen Hardware und Software}}$$

**ISA (Befehlssatzarchitektur):** Eine sehr wichtige Abstraktion!

**Standardisiert:**
- Befehle
- Bitfolgen
- Register
- Speicherzugriffe

### Vor- und Nachteile

✅ **Vorteil:**
- Verschiedene Implementierungen einer Architektur möglich
- Hardware kann verbessert werden, ohne Software zu ändern
- Rückwärtskompatibilität

❌ **Nachteil:**
- Verhindert manchmal neue Innovationen
- Legacy-Support kann Entwicklung bremsen

---

## 📌 Zusammenfassung

### Hauptpunkte

**Computer haben die Welt verändert**
- Von Science-Fiction zu Alltag in 35 Jahren

**3 Klassen von Computersystemen:**

| Klasse | Anzahl | Bedeutung |
|--------|--------|-----------|
| Eingebettete Rechner | Größte Anzahl | ~1000 M/Jahr |
| Arbeitsplatzrechner | Größter Umsatz ($$$) | ~100 M/Jahr |
| Server | Kleinste Anzahl | ~5 M/Jahr |

**5 klassische Komponenten:**
1. Eingabegeräte
2. Ausgabegeräte
3. Speicher (intern/extern)
4. Datenpfad
5. Steuerwerk

**Prozessor (CPU):**
$$\text{CPU} = \text{Datenpfad} + \text{Steuerwerk}$$

**Abstraktion ist notwendig:**
- Komplexität beherrschbar machen
- Von Transistoren zu ISA zu Hochsprachen
- ISA als zentrale Schnittstelle zwischen HW und SW

### Übersetzungskette

$$\text{Hochsprache} \xrightarrow{\text{Compiler}} \text{Assembly} \xrightarrow{\text{Assembler}} \text{Maschinencode}$$

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Zahlensysteme]]: Details zur MIPS-ISA
- [[VL.03 Grundlagen Digitalerentwurf]]: Implementierung des Datenpfads
- [[VL.04 Befehle]]: Implementierung des Steuerwerks
- [[VL.08 Speicherhierarchie]]: DRAM, SRAM, Cache