**Class:** [[ROrg]]  
**Date:** 2025  
**Topics:** #Datenpfad #Steuerung #SingleCycle #ALU #MIPS #Prozessor #Taktzeit #Steuersignale

---

## 🎯 Lernziele der Vorlesung

Einen vollständigen MIPS-Prozessor in Hardware implementieren.

- **Datenpfad** entwerfen für Teilmenge des MIPS-Befehlssatzes
- **Steuersignale** für Befehlsausführung angeben
- **Befehle hinzufügen** zum unterstützten Befehlssatz
- **Steuerlogik** entwerfen zur Berechnung der Steuersignale
- **Ineffizienz** der Eintakt-Implementierung erklären
- **Mehrzyklen-Implementierungen** als bessere Alternative verstehen

---

## 1. Datenpfad und Steuerung

### Definitionen

**Datenpfad (Datapath):**

$$\boxed{\text{Datenpfad} = \text{Hardware-Komponenten + Verbindungen}}$$

**Komponenten:**
- ALU
- Counter (z.B. Program Counter)
- Register
- Speicher
- Multiplexer
- Busse

**Rolle:** "Muskeln" des Prozessors

**Steuerung (Control):**

$$\boxed{\text{Steuerung} = \text{Steuert Ablauf der Befehlsverarbeitung}}$$

**Realisierung:**
- FSM (Finite State Machine)
- Mikroprogrammierung

**Rolle:** "Gehirn" des Prozessors

### Zusammenspiel

```
┌─────────────────────────────────┐
│         Steuerung               │
│   (FSM/Mikroprogrammierung)     │
└──────────┬──────────────────────┘
           │ Steuersignale
           ↓
┌─────────────────────────────────┐
│         Datenpfad               │
│  Register | Speicher | ALU      │
│  Multiplexer | Busse            │
└─────────────────────────────────┘
```

---

## 2. Eintaktprozessor-Konzept

### Definition

$$\boxed{\text{Eintaktprozessor} = \text{Jeder Befehl in einem Taktzyklus}}$$

**Unterstützte Befehle (vereinfacht):**
- **Speicherreferenz:** `lw`, `sw`
- **Arithmetisch-logisch:** `add`, `sub`, `and`, `or`, `slt`
- **Kontrollfluss:** `beq`, `j`

### Fetch-Decode-Execute

**Genereller Ablauf:**

1. Sende PC an Befehlsspeicher
2. Hole Befehl aus Speicher
3. Lese Register
4. Dekodiere Befehl
5. Führe Operation aus
6. Schreibe Ergebnis

---

## 3. ALU-Erweiterung

### Erweiterung um `slt` (Set Less Than)

**Befehl:** `slt $rd, $rs, $rt`

$$\boxed{\text{rd} = \begin{cases} 1 & \text{falls rs} < \text{rt} \\ 0 & \text{sonst} \end{cases}}$$

**Implementierung:**
- Verwende Subtraktion: $(a - b) < 0 \Rightarrow a < b$
- Extra Input: **Less** (für alle 1-Bit ALUs)
- Extra Output: **Set** (nur für ALU31)

**Verbindung:**
- `Less₀ = Set` (von ALU31)
- `Less₁₋₃₁ = 0`
- Set = Vorzeichenbit des Subtraktionsergebnisses (Bit 31)

**ALU-Steuersignale für slt:**
- Ainvert: 0
- Binvert: 1
- CarryIn: 1 (für Subtraktion)
- Operation: 11 (wählt Less-Input)

### Erweiterung um `beq` (Branch on Equal)

**Befehl:** `beq $rs, $rt, offset`

$$\boxed{\text{Falls rs} = \text{rt:  PC} = \text{PC} + 4 + 4 \times \text{offset}}$$

**Test auf Gleichheit:**

$$\text{rs} = \text{rt} \Leftrightarrow \text{rs} - \text{rt} = 0$$

**Implementierung:**
- Neues Ausgangssignal: **Zero**
- Zero = 1, falls alle Result-Bits = 0
- Realisierung: NOR aller Result-Bits

**ALU-Steuersignale:**
- Gleich wie Subtraktion
- Ainvert: 0
- Binvert (=Bnegate): 1
- CarryIn: 1
- Operation: 10 (Adder-Output)

### Zusammenfassung ALU-Steuersignale

| Gewünschte Operation | Ainvert | Bnegate | Operation |
|---------------------|---------|---------|-----------|
| AND | 0 | 0 | 00 |
| OR | 0 | 0 | 01 |
| ADD | 0 | 0 | 10 |
| SUB | 0 | 1 | 10 |
| SLT | 0 | 1 | 11 |
| NOR | 1 | 1 | 00 |
| NAND | 1 | 1 | 01 |

**4-Bit ALU-Operation:**

| ALU-Operation | Funktion |
|---------------|----------|
| 0000 | AND |
| 0001 | OR |
| 0010 | ADD |
| 0110 | SUB |
| 0111 | SLT |
| 1100 | NOR |

---

## 4. Registersatz (Register File)

### Funktionsweise

**Ports:**
- 2 Leseports (immer aktiv)
- 1 Schreibport (nur bei RegWrite = 1)

**Verhalten:**

```
LeseDaten1 = Register[LeseRegister1]    (immer)
LeseDaten2 = Register[LeseRegister2]    (immer)

Register[SchreibeRegister] = SchreibeDaten
    (nur wenn RegWrite = 1 und bei Taktflanke!)
```

### Flankengesteuertes Taktverfahren

$$\boxed{\text{Edge-Triggered: Zustandsänderungen NUR bei Taktflanke}}$$

**Vorteil:** Schaltwerk kann in einem Zyklus gelesen UND geschrieben werden

```
Register → Kombinatorische Logik → Register
   ↑                                    ↑
   └──────── Clock (Taktflanke) ────────┘
```

**Varianten:**
- Steigende Taktflanke (0 → 1)
- Fallende Taktflanke (1 → 0)

---

## 5. Datenpfad-Aufbau

### Schritt 1: Befehl laden

**Benötigte Komponenten:**
- **PC (Program Counter):** Speichert aktuelle Befehlsadresse
- **Instruction Memory:** Speichert Programm
- **Addierer:** Berechnet PC + 4

```
┌────┐     ┌──────────────────┐
│ PC │────→│ Instruction      │
└─┬──┘     │ Memory           │
  │        └──────────────────┘
  │             │
  │             ↓ Instruction[31:0]
  │        
  └───→ [+4] ──→ PC' (nächster PC)
```

### Schritt 2: R-Type Befehle

**Format:**

```
| op (6) | rs (5) | rt (5) | rd (5) | shamt (5) | func (6) |
```

**Zusätzliche Komponenten:**
- Registersatz (Register File)
- ALU

**Verbindungen:**
- `Instruction[25:21]` → LeseRegister1 (rs)
- `Instruction[20:16]` → LeseRegister2 (rt)
- `Instruction[15:11]` → SchreibeRegister (rd)
- ALU-Ergebnis → SchreibeDaten

### Schritt 3: Load/Store-Befehle

**Format:**

```
| op (6) | rs (5) | rt (5) | 16-Bit Offset |
```

**Zusätzliche Komponenten:**
- **Vorzeichenerweiterung:** 16 Bit → 32 Bit
- **Data Memory:** Datenspeicher
- **Multiplexer:** Für ALU-Operand und Zielregister

**lw-Befehl:** `lw $rt, offset($rs)`

1. Adresse = Register[rs] + offset
2. Daten = Memory[Adresse]
3. Register[rt] = Daten

**sw-Befehl:** `sw $rt, offset($rs)`

1. Adresse = Register[rs] + offset
2. Memory[Adresse] = Register[rt]

### Schritt 4: Branch-Befehle

**beq-Befehl:** `beq $rs, $rt, offset`

$$\boxed{\text{Zieladresse} = \text{PC} + 4 + 4 \times \text{offset}}$$

**Zusätzliche Komponenten:**
- Addierer für Verzweigungsadresse
- Shift-left-2 für Offset
- Multiplexer für PC

**Ablauf:**

1. Subtrahiere rs - rt
2. Falls Zero = 1: PC = PC + 4 + (offset << 2)
3. Sonst: PC = PC + 4

### Schritt 5: Jump-Befehl

**Format:**

```
| op (6) | 26-Bit Wortadresse |
```

$$\boxed{\text{Zieladresse} = \text{PC}[31:28] \# (\text{Adresse} \times 4)}$$

**Implementierung:**
- Shift-left-2: Adresse × 4
- Konkatenation mit PC[31:28]
- Multiplexer für PC-Auswahl

---

## 6. Steuersignale

### Multiplexer-Steuersignale

**RegDst:** Wählt Zielregister

$$\text{RegDst} = \begin{cases} 0 & \text{rt (I-Format)} \\ 1 & \text{rd (R-Format)} \end{cases}$$

**ALUSrc:** Wählt zweiten ALU-Operand

$$\text{ALUSrc} = \begin{cases} 0 & \text{Register[rt]} \\ 1 & \text{Sign-Extended Immediate} \end{cases}$$

**MemToReg:** Wählt Daten für Registersatz

$$\text{MemToReg} = \begin{cases} 0 & \text{ALU-Ergebnis} \\ 1 & \text{Memory-Daten} \end{cases}$$

**PCSrc:** Wählt nächsten PC

$$\text{PCSrc} = \text{Branch} \land \text{Zero}$$

**Jump:** Wählt Jump-Adresse (0 oder 1)

### Speicher-Steuersignale

**MemRead:** Lesen aus Data Memory aktivieren

**MemWrite:** Schreiben in Data Memory aktivieren

**RegWrite:** Schreiben in Registersatz aktivieren

---

## 7. ALU-Steuerung

### Zweistufige Steuerung

**ALUOp (2 Bit):** Von Hauptsteuereinheit

| ALUOp | Bedeutung |
|-------|-----------|
| 00 | Addition (lw, sw) |
| 01 | Subtraktion (beq) |
| 10 | Durch Funktionscode bestimmt (R-Type) |

**Funktionscode (6 Bit):** Aus Instruction[5:0]

### ALU-Steuereinheit-Wahrheitstabelle

| ALUOp | Funct | ALU-Operation | Funktion |
|-------|-------|---------------|----------|
| 00 | X | 0010 | ADD |
| 01 | X | 0110 | SUB |
| 10 | 100000 | 0010 | ADD |
| 10 | 100010 | 0110 | SUB |
| 10 | 100100 | 0000 | AND |
| 10 | 100101 | 0001 | OR |
| 10 | 101010 | 0111 | SLT |

**Blockdiagramm:**

```
Opcode[31:26] → ┌──────────────┐
                │ Haupt-       │
                │ steuereinheit│ → ALUOp (2)
                └──────────────┘
                
Funct[5:0]   → ┌──────────────┐
ALUOp (2)    → │ ALU-         │
                │ Steuereinheit│ → ALU-Operation (4)
                └──────────────┘
```

---

## 8. Hauptsteuereinheit

### Steuersignale für R-Format

**Beispiel:** `add $rd, $rs, $rt`

```
Opcode = 000000
```

| Signal | Wert | Begründung |
|--------|------|------------|
| RegDst | 1 | Schreibe nach rd |
| ALUSrc | 0 | Zweiter Operand aus Register |
| MemToReg | 0 | ALU-Ergebnis in Register |
| RegWrite | 1 | Schreibe in Register |
| MemRead | 0 | Kein Speicherlesen |
| MemWrite | 0 | Kein Speicherschreiben |
| Branch | 0 | Keine Verzweigung |
| ALUOp | 10 | R-Type |
| Jump | 0 | Kein Sprung |

### Steuersignale für lw

**Beispiel:** `lw $rt, offset($rs)`

```
Opcode = 100011 (35)
```

| Signal | Wert | Begründung |
|--------|------|------------|
| RegDst | 0 | Schreibe nach rt |
| ALUSrc | 1 | Immediate als Offset |
| MemToReg | 1 | Memory-Daten in Register |
| RegWrite | 1 | Schreibe in Register |
| MemRead | 1 | Lese aus Speicher |
| MemWrite | 0 | Kein Speicherschreiben |
| Branch | 0 | Keine Verzweigung |
| ALUOp | 00 | Addition |
| Jump | 0 | Kein Sprung |

### Steuersignale für sw

**Beispiel:** `sw $rt, offset($rs)`

```
Opcode = 101011 (43)
```

| Signal | Wert | Begründung |
|--------|------|------------|
| RegDst | X | Kein Registerschreiben |
| ALUSrc | 1 | Immediate als Offset |
| MemToReg | X | Kein Registerschreiben |
| RegWrite | 0 | Kein Registerschreiben |
| MemRead | 0 | Kein Speicherlesen |
| MemWrite | 1 | Schreibe in Speicher |
| Branch | 0 | Keine Verzweigung |
| ALUOp | 00 | Addition |
| Jump | 0 | Kein Sprung |

### Steuersignale für beq

**Beispiel:** `beq $rs, $rt, offset`

```
Opcode = 000100 (4)
```

| Signal | Wert | Begründung |
|--------|------|------------|
| RegDst | X | Kein Registerschreiben |
| ALUSrc | 0 | Zweiter Operand aus Register |
| MemToReg | X | Kein Registerschreiben |
| RegWrite | 0 | Kein Registerschreiben |
| MemRead | 0 | Kein Speicherlesen |
| MemWrite | 0 | Kein Speicherschreiben |
| Branch | 1 | Verzweige bei Zero=1 |
| ALUOp | 01 | Subtraktion |
| Jump | 0 | Kein Sprung |

### Steuersignale für j

**Beispiel:** `j target`

```
Opcode = 000010 (2)
```

| Signal | Wert | Begründung |
|--------|------|------------|
| RegDst | X | Kein Registerschreiben |
| ALUSrc | X | ALU nicht relevant |
| MemToReg | X | Kein Registerschreiben |
| RegWrite | 0 | Kein Registerschreiben |
| MemRead | 0 | Kein Speicherlesen |
| MemWrite | 0 | Kein Speicherschreiben |
| Branch | X | Jump steuert PC |
| ALUOp | XX | ALU nicht relevant |
| Jump | 1 | Springe zu Adresse |

### Hauptsteuereinheit-Wahrheitstabelle

| Befehl | Opcode | RegDst | ALUSrc | MemToReg | RegWrite | MemRead | MemWrite | Branch | ALUOp | Jump |
|--------|--------|--------|--------|----------|----------|---------|----------|--------|-------|------|
| R-Format | 000000 | 1 | 0 | 0 | 1 | 0 | 0 | 0 | 10 | 0 |
| lw | 100011 | 0 | 1 | 1 | 1 | 1 | 0 | 0 | 00 | 0 |
| sw | 101011 | X | 1 | X | 0 | 0 | 1 | 0 | 00 | 0 |
| beq | 000100 | X | 0 | X | 0 | 0 | 0 | 1 | 01 | 0 |
| j | 000010 | X | X | X | 0 | 0 | 0 | X | XX | 1 |

---

## 9. Vollständiger Datenpfad

### Komponenten

```
┌──────────────────────────────────────────────────────────┐
│                  Hauptsteuereinheit                       │
│                  (Opcode[31:26])                         │
└───────────┬──────────────────────────────────────────────┘
            │ Steuersignale
            ↓
┌───────────────────────────────────────────────────────────┐
│  ┌────┐   ┌────────────┐   ┌──────────┐   ┌───────────┐ │
│  │ PC │→  │Instruction │→  │Register  │→  │   ALU     │ │
│  └────┘   │  Memory    │   │   File   │   └───────────┘ │
│     ↑     └────────────┘   └──────────┘          ↓       │
│     │                            ↓                ↓       │
│     │                       ┌────────────┐  ┌──────────┐ │
│     └───────────────────────│   MUX      │  │   Data   │ │
│                             └────────────┘  │  Memory  │ │
│                                             └──────────┘ │
└───────────────────────────────────────────────────────────┘
```

### Kritische Pfade

**R-Type:**
- Instruction Memory → Register File → ALU → Register File

**lw:**
- Instruction Memory → Register File → ALU → Data Memory → Register File

**sw:**
- Instruction Memory → Register File → ALU → Data Memory

**beq:**
- Instruction Memory → Register File → ALU (+ Verzweigungsadresse)

**j:**
- Instruction Memory (kürzester Pfad)

---

## 10. Leistungsanalyse

### Taktzeit-Bestimmung

**Annahmen (Verzögerungen):**
- Instruction/Data Memory: 200 ps
- ALU & Addierer: 100 ps
- Register File: 50 ps (Lesen + Schreiben)

**Befehlszeiten:**

| Befehl | Pfad | Zeit |
|--------|------|------|
| **lw** | IM → RF → ALU → DM → RF | 200 + 50 + 100 + 200 + 50 = **600 ps** |
| **sw** | IM → RF → ALU → DM | 200 + 50 + 100 + 200 = **550 ps** |
| **R-Type** | IM → RF → ALU → RF | 200 + 50 + 100 + 50 = **400 ps** |
| **beq** | IM → RF → ALU | 200 + 50 + 100 = **350 ps** |
| **j** | IM | **200 ps** |

$$\boxed{\text{Taktzeit} = \max(\text{alle Befehlszeiten}) = 600\text{ ps}}$$

**Maximale Taktfrequenz:**

$$f_{\max} = \frac{1}{600\text{ ps}} = 1{,}67\text{ GHz}$$

### Performance-Berechnung

**Instruktionsmix:**
- 25% lw
- 10% sw
- 45% R-Type
- 15% beq
- 5% j

**Durchschnittliche Befehlszeit (theoretisch mit variabler Taktzeit):**

$$\text{DB} = 0{,}25 \times 600 + 0{,}1 \times 550 + 0{,}45 \times 400 + 0{,}15 \times 350 + 0{,}05 \times 200$$

$$\text{DB} = 150 + 55 + 180 + 52{,}5 + 10 = 447{,}5\text{ ps}$$

**Speedup bei variabler Taktzeit:**

$$\text{Speedup} = \frac{600}{447{,}5} = 1{,}34$$

---

## 11. Probleme des Eintaktprozessors

### Hauptprobleme

**1. Ineffiziente Ressourcennutzung:**

$$\boxed{\text{Alle Befehle brauchen Taktzeit des langsamsten Befehls}}$$

- lw benötigt 600 ps
- j benötigt nur 200 ps
- Aber j muss auch 600 ps warten!

**2. Verschwendung von Chipfläche:**
- Hardware-Ressourcen müssen repliziert werden
- Beispiel: Mehrere Addierer (PC+4, ALU, Verzweigung)
- Können nicht wiederverwendet werden im selben Zyklus

**3. Skalierungsprobleme:**
- Komplexere Befehle (z.B. Gleitkomma) würden Taktzeit stark erhöhen
- Gesamte Prozessorgeschwindigkeit sinkt

### Visualisierung der Ineffizienz

```
lw:    |████████████████████████| 600 ps (100% genutzt)
sw:    |████████████████████░░░░| 550 ps (92% genutzt)
R-Type:|█████████████░░░░░░░░░░░| 400 ps (67% genutzt)
beq:   |█████████░░░░░░░░░░░░░░░| 350 ps (58% genutzt)
j:     |████░░░░░░░░░░░░░░░░░░░░| 200 ps (33% genutzt!)
```

---

## 12. Lösung: Mehrzyklenprozessor

### Grundidee

$$\boxed{\text{Unterschiedliche Befehle} \Rightarrow \text{Unterschiedliche Anzahl Zyklen}}$$

**Vorteile:**
- Kürzere Taktzeit möglich
- Ressourcen können wiederverwendet werden
- Effizienter für verschiedene Befehlstypen

**Beispiel-Architektur:**

```
┌────┐   ┌──────────┐   ┌──────────┐
│ PC │→  │ Memory   │→  │Instr. Reg│
└────┘   │(Instr+   │   └──────────┘
         │ Data)    │         ↓
         └──────────┘   ┌──────────┐
              ↑         │Register  │
              │         └──────────┘
         ┌────┴────┐         ↓
         │  ALU    │←────────┘
         └─────────┘
```

**Unterschiede:**
- Ein gemeinsamer Speicher (Instruction + Data)
- Register zwischen Phasen
- Befehle in mehreren Schritten

---

## 13. Beispiel: seq-Befehl hinzufügen

### Aufgabenstellung

**Neuer Befehl:** `seq $rd, $rs, $rt`

$$\boxed{\text{rd} = \begin{cases} 1 & \text{falls rs} = \text{rt} \\ 0 & \text{sonst} \end{cases}}$$

### Lösung

**1. Befehlsformat:** R-Type

```
| 0 | rs | rt | rd | 0 | funct |
```

**2. Datenpfad-Änderungen:**
- Zero-Ausgang der ALU nutzen
- ALU subtrahieren lassen (rs - rt)
- Zero-Signal zum Registersatz leiten
- Multiplexer für Schreibdaten:
  - 0: ALU-Ergebnis
  - 1: Zero-Signal (erweitert zu 32 Bit)

**3. Steuersignale:**

| Signal | Wert | Begründung |
|--------|------|------------|
| RegDst | 1 | Schreibe nach rd |
| ALUSrc | 0 | Register-Operanden |
| MemToReg | X | Über seq-MUX gesteuert |
| RegWrite | 1 | Schreibe in Register |
| MemRead | 0 | Kein Speicherlesen |
| MemWrite | 0 | Kein Speicherschreiben |
| Branch | 0 | Keine Verzweigung |
| ALUOp | 10 | R-Type → Subtraktion |
| **SetEq** | **1** | **Wähle Zero-Signal** |

**4. ALU-Steuerung:**
- Funktionscode von seq muss 0110 (Subtraktion) erzeugen

---

## 📌 Zusammenfassung

### Datenpfad-Komponenten

**Speicherelemente:**
- Program Counter (PC)
- Instruction Memory
- Register File
- Data Memory

**Kombinatorische Logik:**
- ALU
- Addierer (PC+4, Verzweigung)
- Multiplexer
- Vorzeichenerweiterung
- Steuereinheiten

### Steuersignale-Übersicht

**Multiplexer:**
- RegDst, ALUSrc, MemToReg, PCSrc, Jump

**Speicher:**
- MemRead, MemWrite, RegWrite

**ALU:**
- ALUOp (2 Bit) → ALU-Operation (4 Bit)

### Entwurfsprinzipien

**1. Flankengesteuertes Taktverfahren:**
- Alle Zustandsänderungen bei Taktflanke
- Ermöglicht Lesen + Schreiben im selben Zyklus

**2. Zweistufige Steuerung:**
- Hauptsteuereinheit (Opcode → ALUOp)
- ALU-Steuereinheit (ALUOp + Funct → ALU-Operation)

**3. Multiplexer für Flexibilität:**
- Verschiedene Datenpfade für verschiedene Befehle

### Leistungsmetriken

**Taktzeit:**

$$\text{Taktzeit} = \text{Längster Pfad} = 600\text{ ps (für lw)}$$

**CPI (Cycles Per Instruction):**

$$\text{CPI}_{\text{Single-Cycle}} = 1$$

**Problem:** Verschwendung bei kurzen Befehlen

### Warum Eintakt nicht mehr verwendet wird

❌ **Ineffizient:** Alle Befehle gleich langsam wie der langsamste

❌ **Ressourcenverschwendung:** Hardware repliziert statt wiederverwendet

❌ **Nicht skalierbar:** Komplexe Befehle würden Taktzeit drastisch erhöhen

✅ **Lösung:** Mehrzyklenprozessor (nächstes Kapitel)

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.03 Grundlagen Digitalerentwurf]]: ALU, Register, Multiplexer
- [[VL.04 Befehle]]: MIPS-Befehlsformate, Semantik
- [[VL.06 Leistung]]: Effizienzsteigerung durch Parallelität
- [[VL.07 Pipelining]]: Cache-Integration