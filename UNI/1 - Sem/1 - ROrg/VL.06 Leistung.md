**Class:** [[ROrg]]  
**Date:** 2025  
**Topics:** #Performance #Rechenleistung #CPUZeit #CPI #Benchmarks #SPEC #AmdahlsGesetz #Durchsatz #Latenz

---

## 🎯 Lernziele der Vorlesung

Rechenleistung messen, vergleichen und optimieren können.

- **Rechenleistung messen**, protokollieren und zusammenfassen
- **Intelligente Entscheidungen** über Hardware treffen
- **Marketing-Hype durchblicken**
- **Ausführungszeit** bei gegebener Befehlsanzahl, CPI und Taktfrequenz berechnen
- **Gesetz von Amdahl** anwenden
- **Benchmark-Suites** kennen (SPEC)

---

## 1. Rechenleistung definieren

### Grundfragen

**Zentrale Fragen:**
1. Warum ist manche Hardware für bestimmte Programme besser geeignet?
2. Welche Faktoren der Systemleistung sind hardwarebezogen?
3. Wie beeinflusst der Befehlssatz die Rechenleistung?

### Flugzeug-Analogie

**Beispiel:** Welches Flugzeug hat die beste Leistung?

| Flugzeug | Passagiere | Reichweite (Meilen) | Geschwindigkeit (mph) |
|----------|------------|---------------------|----------------------|
| Boeing 737-100 | 101 | 630 | 598 |
| Boeing 747 | 470 | 4150 | 610 |
| Concorde | 132 | 4000 | 1350 |
| Douglas DC-8-50 | 146 | 8720 | 544 |

**Abhängig von der Bewertung:**
- **Schnellster Flug nach New York?** → Concorde (Latenz)
- **300 Menschen am schnellsten nach New York?** → Boeing 747 (Durchsatz)

---

## 2. Latenz vs. Durchsatz

### Definitionen

**Antwortzeit (Response Time, Latency):**

$$\boxed{\text{Latenz} = \text{Zeit bis Job ausgeführt ist}}$$

**Fragen:**
- Wie lange dauert es, bis mein Job ausgeführt wird?
- Wie lange dauert eine Datenbankabfrage?

**Durchsatz (Throughput):**

$$\boxed{\text{Durchsatz} = \text{Anzahl Jobs pro Zeiteinheit}}$$

**Fragen:**
- Wie viele Jobs können gleichzeitig ausgeführt werden?
- Wie viele Rechenoperationen werden erledigt?

### Auswirkung von Prozessor-Upgrade

**Wenn Maschine schnelleren Prozessor bekommt:**

| Metrik | Änderung |
|--------|----------|
| **Latenz** | ✅ Verringert sich |
| **Durchsatz** | ✅ Erhöht sich |

---

## 3. CPU-Zeit

### Zeitarten

**Verstrichene Zeit (Elapsed Time):**
- Zählt **alles**: Platten-/Speicherzugriffe, I/O, andere Programme
- Brauchbar, aber selten gut zum Vergleichen

**CPU-Zeit:**
- Zählt **weder** I/O **noch** Ausführungszeit anderer Programme
- Kann zerlegt werden in:
  - **System-CPU-Zeit:** Zeit im Betriebssystem
  - **Benutzer-CPU-Zeit:** Zeit im Benutzerprogramm

### Unix time-Kommando

```
90.7u  12.9s  2:39
  ↑      ↑      ↑
  │      │      └─ Verstrichene Zeit
  │      └──────── System-CPU-Zeit
  └───────────── Benutzer-CPU-Zeit
```

**Unser Fokus:** Benutzer-CPU-Zeit

---

## 4. CPU-Leistungsgleichung

### Die zentrale Gleichung

$$\boxed{T = N_{\text{instr}} \times \text{CPI} \times t_{\text{cycle}}}$$

**Alternativ:**

$$\boxed{T = \frac{N_{\text{instr}} \times \text{CPI}}{f}}$$

**Variablen:**
- $T$: CPU-Zeit (Ausführungszeit)
- $N_{\text{instr}}$: Anzahl der Maschinenbefehle
- $\text{CPI}$: Durchschnittliche Taktzyklen pro Befehl (Cycles Per Instruction)
- $t_{\text{cycle}}$: Taktzykluszeit
- $f$: Taktfrequenz = $1/t_{\text{cycle}}$

### Beispiel: Taktzykluszeit berechnen

**4-GHz-Takt:**

$$t_{\text{cycle}} = \frac{1}{f} = \frac{1}{4 \times 10^9\text{ Hz}} = 0{,}25 \times 10^{-9}\text{ s} = 250\text{ ps}$$

---

## 5. CPI-Berechnung

### Beispiel: Mehrzyklenprozessor

**Gegeben:**
- Prozessor: 2 GHz
- Programm: 5 Millionen Befehle
- Befehlsmix:
  - 52% arithmetisch: 4 Zyklen/Befehl
  - 25% Load: 5 Zyklen/Befehl
  - 10% Store: 4 Zyklen/Befehl
  - 11% Branch: 3 Zyklen/Befehl
  - 2% Jump: 3 Zyklen/Befehl

**CPI-Berechnung:**

$$\text{CPI} = \sum (\text{Anteil}_i \times \text{CPI}_i)$$

$$\text{CPI} = 0{,}52 \times 4 + 0{,}25 \times 5 + 0{,}10 \times 4 + 0{,}11 \times 3 + 0{,}02 \times 3$$

$$\text{CPI} = 2{,}08 + 1{,}25 + 0{,}40 + 0{,}33 + 0{,}06 = 4{,}12$$

**Ausführungszeit:**

$$T = \frac{N_{\text{instr}} \times \text{CPI}}{f} = \frac{5 \times 10^6 \times 4{,}12}{2 \times 10^9}$$

$$T = \frac{20{,}6 \times 10^6}{2 \times 10^9} = 10{,}3\text{ ms}$$

---

## 6. Leistungsfähigkeit verbessern

### Optimierungsansätze

$$\boxed{T = N_{\text{instr}} \times \text{CPI} \times t_{\text{cycle}}}$$

**Um Leistung zu erhöhen (T verringern):**

1. **Befehlsanzahl verringern** ($N_{\text{instr}} ↓$)
2. **CPI verringern**
3. **Taktzykluszeit verringern** ($t_{\text{cycle}} ↓$)
4. **Taktfrequenz erhöhen** ($f ↑$)

### Einflussfaktoren

| Faktor | $N_{\text{instr}}$ | CPI | $t_{\text{cycle}}$ |
|--------|---------------------|-----|---------------------|
| **Programm** | ✅ | (✅) | — |
| **Compiler** | ✅ | (✅) | — |
| **Befehlssatz (ISA)** | ✅ | ✅ | (✅) |
| **Mikroarchitektur** | — | ✅ | ✅ |
| **Technologie** | — | — | ✅ |

**Beachte:** Optimierungen können Trade-offs haben!
- Beispiel: Weniger Befehle → höherer CPI?

---

## 7. Rechenleistung vergleichen

### Einzelnes Programm

**Eindeutig:** Computer mit kürzerer Ausführungszeit ist schneller

### Mehrere Programme

**Problem:** Verschiedene Programme haben unterschiedliche Laufzeiten

**Beispiel:**

| Computer | P1 (s) | P2 (s) | Summe (s) |
|----------|--------|--------|-----------|
| A | 1 | 1000 | 1001 |
| B | 10 | 100 | 110 |
| C | 20 | 20 | 40 |

**Auswertung:**
- **B ist 9,1× schneller als A** (1001/110 ≈ 9,1)
- **C ist 25× schneller als A** (1001/40 = 25,025)

**Konsistentes Maß:** Summe der Ausführungszeiten

---

## 8. Mittelwertbildung

### Arithmetisches Mittel

**Definition:**

$$\boxed{\text{Arithmetisches Mittel} = \frac{1}{n} \sum_{i=1}^{n} \text{Time}_i}$$

**Anwendung:** Wenn alle Programme gleich häufig ausgeführt werden

**Beispiel:**

| Computer | P1 | P2 | Arithm. Mittel |
|----------|----|----|----------------|
| A | 1 s | 1000 s | 500,5 s |
| B | 10 s | 100 s | 55 s |
| C | 20 s | 20 s | 20 s |

### Gewichtetes arithmetisches Mittel

**Definition:**

$$\boxed{\text{Gewichtetes Mittel} = \sum_{i=1}^{n} \text{Weight}_i \times \text{Time}_i}$$

**Bedingung:** $\sum_{i=1}^{n} \text{Weight}_i = 1$

**Beispiel:** $\text{Weight}_1(\text{P1}) = 0{,}8$, $\text{Weight}_2(\text{P2}) = 0{,}2$

| Computer | Gewichtetes Mittel |
|----------|-------------------|
| A | $0{,}8 \times 1 + 0{,}2 \times 1000 = 200{,}8$ s |
| B | $0{,}8 \times 10 + 0{,}2 \times 100 = 28$ s |
| C | $0{,}8 \times 20 + 0{,}2 \times 20 = 20$ s |

### Normalisierte Ausführungszeit

**Problem:** Arithmetisches Mittel normalisierter Zeiten führt zu **unterschiedlichen Aussagen** je nach Referenzmaschine!

**Beispiel: Normalisiert auf A**

| Computer | P1 | P2 | Arithm. Mittel |
|----------|----|----|----------------|
| A | 1,0 | 1,0 | 1,0 |
| B | 10,0 | 0,1 | 5,05 |
| C | 20,0 | 0,02 | 10,01 |

**Beispiel: Normalisiert auf B**

| Computer | P1 | P2 | Arithm. Mittel |
|----------|----|----|----------------|
| A | 0,1 | 10,0 | 5,05 |
| B | 1,0 | 1,0 | 1,0 |
| C | 2,0 | 0,2 | 1,1 |

⚠️ **Widerspruch:** A scheint mal schneller, mal langsamer als C!

### Geometrisches Mittel

**Lösung:** Geometrisches Mittel verwenden!

$$\boxed{\text{Geometrisches Mittel} = \sqrt[n]{\prod_{i=1}^{n} \text{Ratio}_i}}$$

**Ratio:** Ausführungszeit normalisiert auf Referenzmaschine

**Beispiel:**

| Norm. auf | A | B | C |
|-----------|---|---|---|
| A | 1,0 | 1,0 | 0,63 |
| B | 1,0 | 1,0 | 0,63 |
| C | 1,58 | 1,58 | 1,0 |

✅ **Konsistent:** Relative Verhältnisse bleiben gleich!

⚠️ **Achtung:** Geometrisches Mittel hat **keine physikalische Bedeutung**!

---

## 9. Benchmarks

### Definition

$$\boxed{\text{Benchmark} = \text{Standardisierte Testprogramme zur Leistungsmessung}}$$

### Arten von Benchmarks

**Kleine Benchmarks:**
- ✅ Gut für Architekten und Designer
- ✅ Leicht zu standardisieren
- ❌ Können missbraucht werden

**Echte Applikationen:**
- ✅ Beste Leistungsmessung
- ✅ Typische Programme für erwarteten Workload
- ❌ Aufwändig zu standardisieren

### SPEC (Standard Performance Evaluation Corporation)

**Website:** www.spec.org

**Mitglieder:** AMD, Apple, Dell, HP, IBM, Intel, Microsoft, NVIDIA, Oracle, etc.

**Aktuelle Suite:** SPEC CPU2017

**Prinzip:**
- Unternehmen einigen sich auf **Set realer Programme und Eingaben**
- Wertvoller Indikator für Rechenleistung
- Zeigt auch Compilertechnologie

### SPEC CPU Benchmarks

**Integer Benchmarks (C/C++):**

| Name | Beschreibung |
|------|--------------|
| gzip | Komprimierung |
| vpr | FPGA Schaltkreis-/Leiterbahnanordnung |
| gcc | GNU C-Compiler |
| mcf | Kombinatorische Optimierung |
| crafty | Schachprogramm |
| parser | Textverarbeitung |
| eon | Computervisualisierung |
| perlbmk | Perl-Anwendung |
| gap | Gruppentheorie, Interpreter |
| vortex | Objektorientierte Datenbank |
| bzip2 | Komprimierung |
| twolf | Ort-/Routensimulation |

**Gleitkomma-Benchmarks (Fortran/C):**

| Name | Beschreibung |
|------|--------------|
| wupwise | Quanten-Chromodynamik |
| swim | Flachwassersimulation |
| mgrid | 3D-Mehrgitterverfahren |
| applu | Partielle Differentialgleichungen |
| mesa | 3D-Grafikbibliothek |
| galgel | Strömungsmechanik |
| art | Bilderkennung (neuronale Netze) |
| equake | Seismische Wellensimulation |
| facerec | Gesichtserkennung |
| ammp | Chemische Simulationen |
| lucas | Primzahlentests |
| fma3d | Crash-Simulation (FEM) |
| sixtrack | Beschleunigerkonstruktion |
| apsi | Meteorologie: Schadstoffausbreitung |

### Benchmark-Missbrauch

**Intel Pentium Compiler-Bug (1996):**

> "An embarrassed Intel Corp. acknowledged Friday that a bug in a 
> software program known as a compiler had led the company to 
> overstate the speed of its microprocessor chips on an industry 
> benchmark by 10 percent..."

**Problem:** "Tuning" des Compilers
- Compiler erkennt spezifische Testprobleme
- Ersetzt Code durch handgeschriebene Optimierungen
- Nicht repräsentativ für echte Anwendungen

**Lektion:** Benchmarks können manipuliert werden!

---

## 10. Leistung vs. Taktfrequenz

### Wichtige Erkenntnis

$$\boxed{\text{Höhere Taktfrequenz} \neq \text{Doppelte Leistung}}$$

**Warum?**

$$T = N_{\text{instr}} \times \text{CPI} \times t_{\text{cycle}}$$

- Höhere Frequenz → kleineres $t_{\text{cycle}}$
- Aber: CPI kann sich ändern!
- Komplexere Designs benötigen mehr Zyklen

**Beispiel: Pentium III vs. Pentium 4**
- Pentium 4 hat höhere Taktfrequenz
- Aber: Nicht proportional höhere SPEC-Scores
- Grund: Unterschiedliche Mikroarchitekturen, unterschiedliche CPIs

### Stromverbrauch als Limitierung

**Moderne Realität:**

$$\boxed{\text{Stromverbrauch} = \text{Entscheidende Begrenzung der Leistung}}$$

**Besonders wichtig bei:**
- Eingebetteten Systemen
- Mobilen Geräten
- Rechenzentren

**Trade-off:** Leistung vs. Energieeffizienz

---

## 11. Amdahls Gesetz

### Formulierung

**Angenommen:**
- Anteil $f$ der Ausführungszeit kann um Faktor $x$ verbessert werden
- Restliche Zeit $(1-f)$ bleibt gleich

**Gesamter Speedup:**

$$\boxed{S = \frac{T_{\text{old}}}{T_{\text{new}}} = \frac{1}{(1-f) + \frac{f}{x}}}$$

**Herleitung:**

$$T_{\text{new}} = (1-f) \cdot T_{\text{old}} + \frac{f \cdot T_{\text{old}}}{x}$$

$$T_{\text{new}} = T_{\text{old}} \left[(1-f) + \frac{f}{x}\right]$$

$$S = \frac{T_{\text{old}}}{T_{\text{new}}} = \frac{1}{(1-f) + \frac{f}{x}}$$

### Visualisierung

**Vorher:**

```
|←────── 1-f ──────→|←────── f ──────→|
```

**Nachher:**

```
|←────── 1-f ──────→|←── f/x ──→|
```

### Beispiel 1: Multiplikation beschleunigen

**Gegeben:**
- Programm: 100 s Gesamtzeit
- Multiplikationen: 80 s (= 80% = 0,8)
- Ziel: 4× Speedup

**Gesucht:** Wie schnell müssen Multiplikationen werden?

$$4 = \frac{1}{(1-0{,}8) + \frac{0{,}8}{x}}$$

$$4 = \frac{1}{0{,}2 + \frac{0{,}8}{x}}$$

$$0{,}2 + \frac{0{,}8}{x} = 0{,}25$$

$$\frac{0{,}8}{x} = 0{,}05$$

$$x = \frac{0{,}8}{0{,}05} = 16$$

**Antwort:** Multiplikationen müssen **16× schneller** werden!

**Für 5× Speedup:**

$$5 = \frac{1}{0{,}2 + \frac{0{,}8}{x}}$$

$$0{,}2 + \frac{0{,}8}{x} = 0{,}2$$

$$\frac{0{,}8}{x} = 0$$

$$x = \infty$$

**Antwort:** **Unmöglich!** 5× Speedup nicht erreichbar, da 20% nicht verbessert werden können.

### Beispiel 2: Gleitkomma-Einheit

**Gegeben:**
- Benchmark: 10 s Gesamtzeit
- Gleitkomma-Befehle: 5 s
- Gleitkomma-Verbesserung: 5×

**Speedup:**

$$S = \frac{1}{(1-0{,}5) + \frac{0{,}5}{5}} = \frac{1}{0{,}5 + 0{,}1} = \frac{1}{0{,}6} = 1{,}67$$

### Beispiel 3: Benchmark-Auswahl

**Gegeben:**
- Gewünschter Speedup: 3×
- Gleitkomma-Verbesserung: 5×
- Benchmark: 100 s Gesamtzeit

**Gesucht:** Wie viel % Gleitkomma-Zeit nötig?

$$3 = \frac{1}{(1-f) + \frac{f}{5}}$$

$$3(1-f) + \frac{3f}{5} = 1$$

$$3 - 3f + 0{,}6f = 1$$

$$3 - 2{,}4f = 1$$

$$2{,}4f = 2$$

$$f = \frac{2}{2{,}4} = 0{,}833 = 83{,}3\%$$

**Antwort:** Mindestens **83,3%** der Zeit müssen Gleitkomma-Befehle sein.

### Wichtige Erkenntnisse aus Amdahls Gesetz

**Entwurfsprinzip 3 (Wiederholung):**

$$\boxed{\text{Make the common case fast (Optimiere den häufigen Fall)}}$$

**Konsequenzen:**
1. Kleine Verbesserungen an seltenen Teilen bringen wenig
2. Große Verbesserungen an häufigen Teilen bringen viel
3. Es gibt eine **Obergrenze** für den Speedup:

$$\boxed{S_{\max} = \frac{1}{1-f} \quad \text{(für } x \to \infty \text{)}}$$

Beispiel: Wenn 20% nicht verbessert werden können → Max. 5× Speedup!

---

## 12. MIPS und MFLOPS

### MIPS (Million Instructions Per Second)

**Definition:**

$$\boxed{\text{MIPS} = \frac{N_{\text{instr}}}{\text{Ausführungszeit} \times 10^6}}$$

### Probleme mit MIPS

❌ **Problem 1: Befehlssätze nicht vergleichbar**
- Leistungsfähigkeit der Befehle wird nicht berücksichtigt
- RISC vs. CISC: Unterschiedliche Befehle pro Operation

❌ **Problem 2: Programmabhängig**
- MIPS variiert für verschiedene Programme
- Kein einzelner MIPS-Wert für Computer

❌ **Problem 3: Kann invers zur Leistung sein**
- Beispiel:
  - Programm A: 1M Befehle, CPI = 1,0 → hoher MIPS
  - Programm B: 0,4M Befehle, CPI = 2,0 → niedriger MIPS
  - Aber: B kann trotzdem schneller sein!

**Berechnung:**

$$\text{MIPS} = \frac{N_{\text{instr}}}{T \times 10^6} = \frac{f}{\text{CPI} \times 10^6}$$

### MFLOPS (Million Floating Point Operations Per Second)

**Definition:**

$$\boxed{\text{MFLOPS} = \frac{\text{Anzahl Gleitkomma-Operationen}}{\text{Ausführungszeit} \times 10^6}}$$

**Ähnliche Probleme wie MIPS:**
- Was zählt als "Operation"?
- Programmabhängig
- Architekturen nicht vergleichbar

---

## 📌 Zusammenfassung

### Zentrale Erkenntnisse

**1. Einziges gültiges Leistungsmaß:**

$$\boxed{\text{Ausführungszeit} = \text{Einziges gültiges Maß}}$$

**2. CPU-Leistungsgleichung:**

$$\boxed{T = N_{\text{instr}} \times \text{CPI} \times t_{\text{cycle}} = \frac{N_{\text{instr}} \times \text{CPI}}{f}}$$

**3. Mittelwertbildung:**
- Gleiche Häufigkeit → Arithmetisches Mittel
- Unterschiedliche Häufigkeit → Gewichtetes arithmetisches Mittel
- Normalisierte Zeiten → **Geometrisches Mittel** (nicht arithmetisch!)

**4. Amdahls Gesetz:**

$$\boxed{S = \frac{1}{(1-f) + \frac{f}{x}}}$$

- Optimiere den häufigen Fall
- Maximaler Speedup: $S_{\max} = \frac{1}{1-f}$

### Einflussfaktoren auf Leistung

| Komponente | Beeinflusst |
|------------|-------------|
| **Algorithmus** | $N_{\text{instr}}$, CPI |
| **Programmiersprache** | $N_{\text{instr}}$, CPI |
| **Compiler** | $N_{\text{instr}}$, CPI |
| **ISA** | $N_{\text{instr}}$, CPI, $t_{\text{cycle}}$ |
| **Mikroarchitektur** | CPI, $t_{\text{cycle}}$ |
| **Technologie** | $t_{\text{cycle}}$ |

### Benchmarks

**SPEC (Standard Performance Evaluation Corporation):**
- Set realer Programme und Eingaben
- Integer- und Gleitkomma-Benchmarks
- Website: www.spec.org
- Aktuell: SPEC CPU2017

**Vorsicht:** Benchmarks können manipuliert werden!

### Was NICHT verwenden

❌ **MIPS/MFLOPS:**
- Nicht architektur-übergreifend vergleichbar
- Programmabhängig
- Kann irreführend sein

✅ **Stattdessen:** Ausführungszeit realer Programme

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.04 Befehle]]: $N_{\text{instr}}$ und CPI verschiedener Befehle
- [[VL.05 Single Cycle]]: CPI = 1 beim Single-Cycle
- [[VL.06 Leistung]]: CPI-Verbesserung durch Pipelining
- [[VL.07 Pipelining]]: Cache-Misses beeinflussen CPI