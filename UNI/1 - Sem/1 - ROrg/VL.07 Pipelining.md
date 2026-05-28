**Class:** [[ROrg]]  
**Date:** 2025  
**Topics:** #Pipelining #Hazards #Forwarding #BranchPrediction #Datenkonflikte #Steuerkonflikte #CPI #Durchsatz

---

## 🎯 Lernziele der Vorlesung

Pipelining verstehen und optimieren können.

- **Grundlagen von Pipelining** erklären
- **Pipeline-Konflikte** und Lösungen erläutern (Daten-, Steuerkonflikte)
- **Forwarding** verstehen und anwenden
- **MIPS-Code optimieren** für Pipeline-Prozessoren
- **Befehle hinzufügen** zum Pipeline-Prozessor
- **Steuerung** des Pipeline-Prozessors beschreiben
- **Branch Prediction** und **Superskalar-Prozessoren** erklären

---

## 1. Pipelining-Grundkonzept

### Wäsche-Analogie

**Problem:** 4 Personen (A, B, C, D) waschen Wäsche
- Waschen: 30 min
- Trocknen: 40 min
- Falten: 20 min

**Sequentiell:**

```
A: |─W─|──T──|─F─|
B:                |─W─|──T──|─F─|
C:                               |─W─|──T──|─F─|
D:                                              |─W─|──T──|─F─|
   ├──────────────────────────────────────────────────────┤
                    6 Stunden
```

**Mit Pipelining:**

```
A: |─W─|──T──|─F─|
B:      |─W─|──T──|─F─|
C:           |─W─|──T──|─F─|
D:                |─W─|──T──|─F─|
   ├───────────────────────────┤
         3,5 Stunden
```

$$\boxed{\text{Speedup} = \frac{6}{3{,}5} = 1{,}71}$$

**Taktzeit bestimmt durch längste Stufe:** 40 min (Trocknen)

---

## 2. Computer-Pipeline

### 5 Pipeline-Stufen in MIPS

$$\boxed{\text{IF} → \text{ID} → \text{EX} → \text{MEM} → \text{WB}}$$

**1. IF (Instruction Fetch):**
- Befehl aus Speicher holen
- PC inkrementieren

**2. ID (Instruction Decode):**
- Befehl dekodieren
- Register lesen

**3. EX (Execute):**
- ALU-Operation ausführen
- Adresse berechnen

**4. MEM (Memory Access):**
- Speicherzugriff (lw, sw)
- Branch-Entscheidung

**5. WB (Write Back):**
- Ergebnis in Register schreiben

### Pipeline-Ablauf

**Traditionelle Darstellung:**

| Befehl | TZ 1 | TZ 2 | TZ 3 | TZ 4 | TZ 5 | TZ 6 | TZ 7 | TZ 8 | TZ 9 |
|--------|------|------|------|------|------|------|------|------|------|
| Instr 1 | IF | ID | EX | MEM | WB | | | | |
| Instr 2 | | IF | ID | EX | MEM | WB | | | |
| Instr 3 | | | IF | ID | EX | MEM | WB | | |
| Instr 4 | | | | IF | ID | EX | MEM | WB | |
| Instr 5 | | | | | IF | ID | EX | MEM | WB |

**Wichtig:**

$$\boxed{\text{Pipelining erhöht Durchsatz, nicht Latenz einzelner Befehle}}$$

---

## 3. Leistungsanalyse

### Ohne Pipelining (Single-Cycle)

**Annahmen:**
- Instruction Memory: 200 ps
- Register File: 100 ps
- ALU: 200 ps
- Data Memory: 200 ps
- Register Write: 100 ps

$$T_{\text{cycle}} = 200 + 100 + 200 + 200 + 100 = 800\text{ ps}$$

### Mit Pipelining

**Taktzeit = Längste Stufe:**

$$\boxed{T_{\text{cycle}} = \max(\text{IF, ID, EX, MEM, WB}) = 200\text{ ps}}$$

### Speedup-Berechnung

**Idealer Speedup:**

$$\boxed{\text{Speedup}_{\text{ideal}} = \text{Anzahl Stufen} = 5}$$

**Realer Speedup (für 10 Befehle):**

- Ohne Pipeline: $10 \times 800 = 8000$ ps
- Mit Pipeline: $5 \times 200 + 5 \times 200 = 2000$ ps

$$\text{Speedup}_{\text{real}} = \frac{8000}{2000} = 4$$

**Warum nicht 5?**
- Pipeline-Füllzeit (fill time)
- Erste 4 Zyklen: Pipeline wird gefüllt
- Nur ab Zyklus 5: Voller Durchsatz

---

## 4. MIPS-ISA für Pipelining optimiert

### Design-Entscheidungen

**1. Alle Befehle 32 Bit lang**

✅ **Vorteil:** Einfaches Fetchen in einem Takt

❌ **Vergleich x86:** 1-17 Byte Instruktionen → komplex

**2. Wenige, regelmäßige Befehlsformate (R, I, J)**

✅ **Vorteil:** Dekodierung und Registerlesen **gleichzeitig** möglich

**3. Load/Store-Architektur**

✅ **Vorteil:**
- Adressberechnung in EX (Stufe 3)
- Speicherzugriff in MEM (Stufe 4)
- Klare Trennung

---

## 5. Pipeline-Datenpfad

### Pipeline-Register

**Zwischen jeder Stufe:** Speicherregister für Zwischenwerte

```
IF → [IF/ID] → ID → [ID/EX] → EX → [EX/MEM] → MEM → [MEM/WB] → WB
```

**Pipeline-Register:**
- **IF/ID:** Instruktion (IR), PC+4 (NPC)
- **ID/EX:** Register A, B, Immediate, NPC
- **EX/MEM:** ALU-Ergebnis, Condition, NPC
- **MEM/WB:** ALU-Ergebnis oder Speicherdaten (LMD)

**Wichtig:** Zielregister-Adresse muss durch Pipeline propagiert werden!

### Fehler im ersten Design

**Problem:** Welche Stufe schreibt in Registersatz? → WB

**Lösung:** Zielregisteradresse durch alle Stufen weiterleiten

---

## 6. Steuerung der Pipeline

### Steuersignale

**Identisch zu Single-Cycle, aber:**
- Steuersignale werden durch Pipeline-Stufen **propagiert**
- Jede Stufe nutzt ihre Steuersignale

**Steuerung pro Stufe:**

| Stufe | Steuersignale |
|-------|---------------|
| **ID** | RegDst, ALUOp, ALUSrc |
| **EX** | ALUOp, ALUSrc |
| **MEM** | Branch, MemRead, MemWrite |
| **WB** | RegWrite, MemToReg |

**Durchschalten:** Steuersignale wandern mit Daten durch Pipeline

---

## 7. Pipeline-Konflikte (Hazards)

### Definition

$$\boxed{\text{Hazard} = \text{Situation, die nächsten Befehl im nächsten Takt verhindert}}$$

### Drei Arten von Hazards

**1. Strukturkonflikte (Structural Hazards):**
- Benötigte Ressource ist belegt
- **Lösung:** Ressourcen replizieren (z.B. separate Instruction/Data Memory)

**2. Datenkonflikte (Data Hazards):**
- Ergebnis eines vorherigen Befehls wird benötigt
- **Lösung:** Forwarding, Stalling

**3. Steuerkonflikte (Control Hazards):**
- Branch-Entscheidung verzögert
- **Lösung:** Branch Prediction, Delay Slots

---

## 8. Datenkonflikte

### Beispiel

```assembly
sub  $2, $1, $3    # $2 wird in WB geschrieben
and  $12, $2, $5   # Benötigt $2 in EX
or   $13, $6, $2   # Benötigt $2 in EX
add  $14, $2, $2   # Benötigt $2 in EX
```

**Problem:**

| Befehl | TZ 1 | TZ 2 | TZ 3              | TZ 4              | TZ 5   |
| ------ | ---- | ---- | ----------------- | ----------------- | ------ |
| sub    | IF   | ID   | EX                | MEM               | **WB** |
| and    |      | IF   | **ID (needs $2)** | EX                | MEM    |
| or     |      |      | IF                | **ID (needs $2)** | EX     |

$2 wird in TZ 5 geschrieben, aber in TZ 3 und 4 benötigt!

### Software-Lösung: NOPs einfügen

```assembly
sub  $2, $1, $3
nop                 # Warte-Zyklus
nop                 # Warte-Zyklus
and  $12, $2, $5    # Jetzt ist $2 verfügbar
or   $13, $6, $2
```

❌ **Problem:** Extrem langsam! 2 verschwendete Zyklen pro Konflikt

### Hardware-Lösung: Forwarding (Bypassing)

$$\boxed{\text{Forwarding} = \text{Ergebnisse sofort weiterleiten, ohne auf WB zu warten}}$$

**Prinzip:**
- ALU-Ergebnis aus EX/MEM direkt zur ALU zurückleiten
- ALU-Ergebnis aus MEM/WB direkt zur ALU zurückleiten

**Forwarding-Pfade:**

```
EX/MEM.ALUOut ──→ [MUX] ──→ ALU-Eingang
MEM/WB.ALUOut ──→ [MUX] ──→ ALU-Eingang
```

**Forwarding-Einheit:**

```c
// EX-Hazard (frischestes Ergebnis)
if (EX/MEM.RegWrite && EX/MEM.Rd != 0) {
    if (EX/MEM.Rd == ID/EX.Rs) ForwardA = 10;
    if (EX/MEM.Rd == ID/EX.Rt) ForwardB = 10;
}

// MEM-Hazard (älteres Ergebnis, niedrigere Priorität)
if (MEM/WB.RegWrite && MEM/WB.Rd != 0) {
    if (EX/MEM.Rd != ID/EX.Rs && MEM/WB.Rd == ID/EX.Rs)
        ForwardA = 01;
    if (EX/MEM.Rd != ID/EX.Rt && MEM/WB.Rd == ID/EX.Rt)
        ForwardB = 01;
}
```

**Multiplexer-Steuerung:**

| ForwardA/B | Quelle |
|------------|--------|
| 00 | ID/EX (normaler Registerinhalt) |
| 01 | MEM/WB (von WB-Stufe) |
| 10 | EX/MEM (von MEM-Stufe) |

---

## 9. Load-Use Hazard

### Problem: Forwarding reicht nicht immer

```assembly
lw   $2, 20($1)    # Daten erst in MEM verfügbar
and  $4, $2, $5    # Benötigt $2 in EX
```

**Timing:**

| Befehl | TZ 1 | TZ 2 | TZ 3 | TZ 4 | TZ 5 |
|--------|------|------|------|------|------|
| lw | IF | ID | EX | **MEM (Daten)** | WB |
| and | | IF | ID | **EX (needs $2)** | MEM |

**Problem:** Daten aus MEM (TZ 4) werden in EX (TZ 4) benötigt → **Gleichzeitig!**

### Lösung: Pipeline Stall (Bubble)

**Hazard Detection Unit erkennt:**

```c
if (ID/EX.MemRead && 
    (ID/EX.Rt == IF/ID.Rs || ID/EX.Rt == IF/ID.Rt)) {
    // Stall!
}
```

**Aktion beim Stall:**
1. **PC einfrieren** (PC.Write = 0)
2. **IF/ID einfrieren** (IF/ID.Write = 0)
3. **NOP in ID/EX** einfügen (alle Steuersignale = 0)

**Ergebnis:**

| Befehl | TZ 1 | TZ 2 | TZ 3 | TZ 4 | TZ 5 | TZ 6 |
|--------|------|------|------|------|------|------|
| lw | IF | ID | EX | MEM | WB | |
| and | | IF | ID | **bubble** | EX | MEM |

**1 Zyklus Verzögerung, dann Forwarding möglich**

---

## 10. Steuerkonflikte (Control Hazards)

### Problem: Branch-Entscheidung verzögert

```assembly
40: beq  $1, $3, 72    # Branch-Entscheidung in MEM (TZ 4)
44: and  $12, $2, $5   # Bereits in Pipeline
48: or   $13, $6, $2   # Bereits in Pipeline
52: add  $14, $2, $2   # Bereits in Pipeline
```

**Problem:** Entscheidung erst in MEM bekannt → 3 Befehle falsch geladen!

### Lösung 1: Pipeline anhalten

**Warten bis Branch-Entscheidung:**
- 3 Warte-Zyklen bei **jeder** Verzweigung
- Sehr ineffizient!

### Lösung 2: Branch in frühere Stufe verlegen

**Optimierung:** Branch-Entscheidung in ID-Stufe

**Benötigt:**
- Extra-Comparator in ID: XOR-Gatter zum Vergleich
- Adressberechnung in ID

**Ergebnis:** Nur **1** Warte-Zyklus statt 3

**Implementierung:**

```
Register A ──→ [XOR] ──→ Equal (zu PC-MUX)
Register B ──→ [XOR]
```

### Lösung 3: Annehmen + Flush

**Branch Prediction (einfach):**

$$\boxed{\text{Annahme: Branch NOT taken}}$$

**Ablauf:**
1. Lade nächsten Befehl (PC+4)
2. Falls Branch **nicht genommen:** Kein Verlust
3. Falls Branch **genommen:** Flush (lösche nächsten Befehl)

**Flush-Mechanismus:**
- NOP in IF/ID einfügen
- Alle Steuersignale = 0

### Lösung 4: Branch Delay Slot

**MIPS-Lösung:**

$$\boxed{\text{Befehl NACH Branch wird IMMER ausgeführt}}$$

**Compiler muss Delay Slot füllen:**

**Option 1:** Sinnvoller Befehl

```assembly
    add  $4, $5, $6    # Unabhängig von Branch
    beq  $1, $2, target
    # $4 wird immer berechnet!
target:
    ...
```

**Option 2:** NOP (falls kein passender Befehl)

```assembly
    beq  $1, $2, target
    nop                # Delay Slot
target:
    ...
```

---

## 11. Dynamische Sprungvorhersage

### Motivation

**Moderne Prozessoren:**
- Intel Core i7: **16 Stufen**
- Branch Penalty: Bis zu 15 Zyklen!
- Unmöglich alle Delay Slots zu füllen

### Branch History Table (BHT)

**Konzept:** Lerne aus der Vergangenheit

**Aufbau:**
- Tabelle indiziert durch PC (untere Bits)
- Speichert: Taken (T) / Not Taken (NT)

**Vorhersage:**
1. Nachschlagen in BHT mit PC
2. Hole Befehl aus vorhergesagter Richtung
3. Bei Fehlvorhersage: Flush + Invertiere Bit

### 1-Bit Predictor

**Problem:** 100% Fehlvorhersage bei alternierenden Branches!

**Beispiel: Schleife**

```assembly
loop:
    ...
    bne $1, $0, loop    # 9× taken, 1× not taken
```

**Fehlvorhersagen:**
1. Letzte Iteration: **Fehlvorhersage** (war T, jetzt NT)
2. Nächster Schleifeneintritt: **Fehlvorhersage** (war NT, jetzt T)

**2 Fehlvorhersagen pro Durchlauf!**

### 2-Bit (Bimodal) Predictor

$$\boxed{\text{Ändere Vorhersage erst nach 2 Fehlvorhersagen}}$$

**Zustände:**

```
       ┌─────────────────────────┐
       │ Strongly Taken (ST)     │ Vorhersage: T
       └───┬─────────────────┬───┘
     NT    │                 │ T
       ┌───▼─────────────────▼───┐
       │ Weakly Taken (WT)       │ Vorhersage: T
       └───┬─────────────────┬───┘
     NT    │                 │ T
       ┌───▼─────────────────▼───┐
       │ Weakly Not Taken (WNT)  │ Vorhersage: NT
       └───┬─────────────────┬───┘
     NT    │                 │ T
       ┌───▼─────────────────▼───┐
       │ Strongly Not Taken (SNT)│ Vorhersage: NT
       └─────────────────────────┘
```

**Vorteil:** Optimiert für Schleifen
- Letzte Iteration: ST → WT (noch Vorhersage T)
- Schleifenaustritt: WT → WNT (jetzt Vorhersage NT)
- Nur **1 Fehlvorhersage** statt 2!

---

## 12. Branch Target Buffer (BTB)

### Problem mit BHT allein

**BHT sagt nur Richtung voraus, nicht Zieladresse!**

**In 5-Stufen-MIPS:**
- Branch-Richtung UND Zieladresse in ID berechnet
- Vorhersage kommt zu spät

### Lösung: BTB

$$\boxed{\text{BTB} = \text{Sprungvorhersage} + \text{Zieladresse}}$$

**BTB-Einträge:**

| Tag (PC) | Target Address | Prediction Bits |
|----------|----------------|-----------------|
| PC obere Bits | Zieladresse | 2-Bit Predictor |

**Funktionsweise:**

1. **IF-Stufe:** Lookup mit PC in BTB
2. **Tag-Vergleich:** PC[31:n] == BTB-Tag?
3. **Falls Hit:**
   - Prediction Bits → Taken/Not Taken?
   - Falls Taken → PC = Target Address
4. **Falls Miss:**
   - PC = PC + 4 (oder Stall)
   - Branch später in BTB eintragen

**BTB als Cache:**
- Verdrängungs-Strategie (z.B. LRU)
- Enthält bedingte UND unbedingte Sprünge

### BTB in MIPS-Pipeline integriert

**Änderungen:**
- BTB-Lookup in **IF-Stufe**
- PC-MUX direkt von BTB gesteuert
- Frühe Vorhersage → weniger Penalty

---

## 13. Moderne Hochleistungsprozessoren

### Intel Core i7 (Beispiel)

**Pipeline:**
- **16 Stufen** (vs. 5 bei MIPS)

**Superskalar:**
- **4-6 Befehle gleichzeitig** verarbeiten
- Mehrere Fetch-, Decode-, Execute-Einheiten

**Out-of-Order Execution:**
- CPU bestimmt Ausführungsreihenfolge
- Dynamisches Scheduling

**Register Renaming:**
- Mehr physische als logische Register
- Erhöht Instruction-Level Parallelism (ILP)

**Hardware Multithreading:**
- 1 Kern bearbeitet 2 Threads gleichzeitig
- Hyper-Threading

**Fortgeschrittene Branch Prediction:**
- Mehrstufige Prädiktoren
- Pattern-basierte Vorhersage
- Sehr hohe Genauigkeit (>95%)

### Vertiefung

**Modul:** Advanced Computer Architecture (AES)
- Detaillierte Behandlung moderner Prozessoren
- Superscalar, Out-of-Order, Speculation
- Multi-Core, Multi-Threading

---

## 14. Vergleich: Single-Cycle vs. Multi-Cycle vs. Pipelined

### Übersicht

| Eigenschaft | Single-Cycle | Multi-Cycle | Pipelined |
|-------------|--------------|-------------|-----------|
| **CPI** | 1 | 3-5 | ≈1 (ideal) |
| **Taktzeit** | Lang (800 ps) | Kurz (200 ps) | Kurz (200 ps) |
| **Durchsatz** | Niedrig | Niedrig | **Hoch** |
| **Latenz** | Mittel | Mittel | Mittel |
| **Hardware** | Repliziert | Wiederverwendet | Repliziert |
| **Komplexität** | Einfach | Mittel | **Komplex** |

### Leistungsvergleich (10 Befehle)

**Single-Cycle:**

$$T = 10 \times 800\text{ ps} = 8000\text{ ps}$$

**Multi-Cycle (Ø 4 Zyklen):**

$$T = 10 \times 4 \times 200\text{ ps} = 8000\text{ ps}$$

**Pipelined:**

$$T = (5 + 9) \times 200\text{ ps} = 2800\text{ ps}$$

$$\boxed{\text{Speedup} \approx 2{,}86}$$

---

## 📌 Zusammenfassung

### Grundprinzipien

**1. Pipelining:**

$$\boxed{\text{Erhöht Durchsatz, nicht Latenz einzelner Befehle}}$$

**2. Idealer Speedup:**

$$\text{Speedup}_{\text{ideal}} = \text{Anzahl Stufen}$$

**3. Taktzeit:**

$$T_{\text{cycle}} = \max(\text{Stufenzeiten}) + \text{Overhead}$$

### Pipeline-Stufen (MIPS)

$$\boxed{\text{IF} → \text{ID} → \text{EX} → \text{MEM} → \text{WB}}$$

### Hazards und Lösungen

**Strukturkonflikte:**
- ✅ Ressourcen replizieren

**Datenkonflikte:**
- ✅ **Forwarding** (sofortige Weiterleitung)
- ✅ **Stalling** (bei Load-Use Hazard)
- ✅ Compiler-Optimierung (Befehlsumordnung)

**Steuerkonflikte:**
- ✅ Branch in ID verlegen (1 Stall statt 3)
- ✅ **Branch Delay Slot**
- ✅ **Branch Prediction** (1-Bit, 2-Bit)
- ✅ **Branch Target Buffer** (BTB)

### Forwarding-Bedingungen

```c
// EX-Hazard
if (EX/MEM.RegWrite && EX/MEM.Rd != 0 &&
    EX/MEM.Rd == ID/EX.Rs)
    ForwardA = 10;

// MEM-Hazard (nur wenn kein EX-Hazard)
if (MEM/WB.RegWrite && MEM/WB.Rd != 0 &&
    EX/MEM.Rd != ID/EX.Rs &&
    MEM/WB.Rd == ID/EX.Rs)
    ForwardA = 01;
```

### Branch Prediction

**1-Bit Predictor:**
- Einfach, aber 2 Fehlvorhersagen pro Schleife

**2-Bit Predictor:**
- Besser für Schleifen
- Nur 1 Fehlvorhersage pro Schleife

**Branch Target Buffer:**
- Vorhersage + Zieladresse
- Ermöglicht Vorhersage in IF-Stufe

### MIPS-Design für Pipelining

✅ **Alle Befehle 32 Bit** → einfaches IF

✅ **Regelmäßige Formate** → ID und Register-Lesen gleichzeitig

✅ **Load/Store-Architektur** → klare Trennung EX/MEM

✅ **Einfache Branches** → frühe Entscheidung möglich

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.04 Befehle]]: MIPS-Befehlsformate für Pipelining
- [[VL.05 Single Cycle]]: Datenpfad-Grundlagen
- [[VL.06 Leistung]]: CPI-Verbesserung durch Pipelining
- [[VL.08 Speicherhierarchie]]: Cache-Misses beeinflussen Pipeline