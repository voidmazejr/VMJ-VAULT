**Class:** [[ROrg]]  
**Date:** 2025  
**Topics:** #Speicherhierarchie #Cache #Lokalität #DirectMapped #AMAT #WriteThrough #WriteBack #MissPenalty #SpatialLocality

---

## 🎯 Lernziele der Vorlesung

Cache-Systeme verstehen, analysieren und optimieren können.

- **Cache-Begriffe** erklären: Block, Zeile, Lokalität, Hit, Miss, Tag, etc.
- **Cache-Parameter** berechnen: Größe, Index, Tag
- **Hit/Miss-Sequenzen** bestimmen für Speicherzugriffe
- **CPU-Zeit** berechnen bei gegebener Miss-Rate und Miss-Penalty
- **AMAT** (Average Memory Access Time) und optimale Blockgröße berechnen
- **Implementierungskosten** berechnen (Anzahl benötigter Bits)

---

## 1. Warum Speicherhierarchie?

### Das Problem

**Nutzer wollen:**
- Unbegrenzt großen Speicher
- Unendlich schnelle Zugriffe

**Realität:**

$$\boxed{\text{Schneller Speicher} = \text{Teuer + Wenig Platz}}$$

### Speichertechnologien

| Technologie | Zugriffszeit | Kosten/Bit | Kapazität |
|-------------|--------------|------------|-----------|
| **SRAM** (Static RAM) | ~1 ns (1 cc) | Hoch | Klein |
| **DRAM** (Dynamic RAM) | ~50 ns (50 cc) | Mittel | Groß |
| **Festplatte** | ~10 ms | Niedrig | Sehr groß |

**cc = Clock Cycle** (bei 1 GHz)

---

## 2. Speicherhierarchie-Aufbau

### Pyramide

```
           ┌─────────────┐
           │  Register   │ ← Schnell, teuer, klein
           ├─────────────┤
           │ L1 Cache    │
           ├─────────────┤
           │ L2 Cache    │
           ├─────────────┤
           │ L3 Cache    │ (optional)
           ├─────────────┤
           │Hauptspeicher│
           │   (DRAM)    │
           ├─────────────┤
           │ Festplatte  │ ← Langsam, billig, groß
           └─────────────┘
```

**Eigenschaften:**

| Ebene | Größe ↑ | Geschwindigkeit ↓ | Kosten/Bit ↓ |
|-------|---------|-------------------|--------------|
| Register | ~KB | ~1 cc | Sehr hoch |
| L1 Cache | ~32 KB | ~2-4 cc | Hoch |
| L2 Cache | ~256 KB | ~10-20 cc | Mittel |
| L3 Cache | ~8 MB | ~40-50 cc | Niedrig |
| DRAM | ~8 GB | ~100-200 cc | Sehr niedrig |
| Disk | ~1 TB | ~10⁷ cc | Minimal |

---

## 3. Cache-Grundlagen

### Definition

$$\boxed{\text{Cache} = \text{Hochgeschwindigkeitsspeicher zwischen CPU und Hauptspeicher}}$$

**Eigenschaften:**
- Hardware-kontrolliert (transparent für Software)
- On-demand: Daten werden bei Bedarf geladen
- Nutzt Lokalitätsprinzip

**Abgrenzung:**
- **Scratchpad Memory:** Software-kontrolliert
- Beispiele: IBM Cell Local Store, OpenCL Local Memory

### Hit und Miss

**Cache Hit:**

```
CPU → Cache → [Daten gefunden] → CPU
      ↑
      Schnell (1-2 Zyklen)
```

**Cache Miss:**

```
CPU → Cache → [Daten NICHT gefunden] → Hauptspeicher
                                             ↓
                    Cache ← [Block laden] ←──┘
                      ↓
                    CPU
      ↑
      Langsam (50-200 Zyklen)
```

### Hit Rate und Miss Rate

$$\boxed{\text{Hit Rate } h = \frac{\# \text{ Hits}}{\# \text{ Zugriffe}}}$$

$$\boxed{\text{Miss Rate } = 1 - h = \frac{\# \text{ Misses}}{\# \text{ Zugriffe}}}$$

**Typische Werte:**
- L1 Cache: Hit Rate ~95-99%
- L2 Cache: Hit Rate ~80-95%

---

## 4. Lokalitätsprinzip

### Temporale Lokalität (Temporal Locality)

$$\boxed{\text{Wenn auf X zugegriffen wird} \Rightarrow \text{bald wieder Zugriff auf X}}$$

**Beispiele:**
- Schleifenvariablen
- Funktionen, die oft aufgerufen werden
- Stack-Frames

**Code-Beispiel:**

```c
for (i = 0; i < n; i++)  // i: temporale Lokalität
    sum += a[i];         // sum: temporale Lokalität
```

### Räumliche Lokalität (Spatial Locality)

$$\boxed{\text{Wenn auf X zugegriffen wird} \Rightarrow \text{bald Zugriff auf Nachbarn von X}}$$

**Beispiele:**
- Array-Durchläufe
- Sequentielle Befehle
- Datenstrukturen im Speicher

**Code-Beispiel:**

```c
for (i = 0; i < n; i++)
    sum += a[i];         // a[i], a[i+1], a[i+2], ...
```

### Ausnutzung räumlicher Lokalität

**Problem:** Einzelne Wörter laden ineffizient

**Lösung:** **Ganze Blöcke laden**

```
Miss auf A[0]:
  ┌──────────────────────────────┐
  │ Lade A[0], A[1], A[2], A[3]  │ Block = 4 Wörter
  └──────────────────────────────┘
                ↓
        Alle im Cache

Zugriff auf A[1], A[2], A[3]: Hits!
```

**Vorteil:** 1 Miss + 3 Hits statt 4 Misses

---

## 5. Cache-Terminologie

### Wichtige Begriffe

**Block / Cache Line:**
- Informationseinheit zwischen Speicherebenen
- Typisch: 32-64 Bytes

**Hit:** Daten in höherer Ebene gefunden

**Miss:** Daten NICHT in höherer Ebene gefunden

**Tag:** Adressinformation zur Identifikation des Blocks

**Index:** Position im Cache

**Valid Bit:** Gibt an, ob Block gültige Daten enthält

**Dirty Bit:** Gibt an, ob Block verändert wurde (nur bei write-back)

---

## 6. Cache-Leistung (Performance)

### Average Memory Access Time (AMAT)

$$\boxed{\text{AMAT} = \text{Hit Time} + \text{Miss Rate} \times \text{Miss Penalty}}$$

**Komponenten:**

**Hit Time:**
- Zeit für Cache-Zugriff bei Hit
- Inklusive Tag-Vergleich
- Typisch: 1-2 Zyklen

**Miss Penalty:**
- Zeit zum Laden eines Blocks aus nächster Ebene
- Typisch: 50-200 Zyklen (für L1 → DRAM)

**Beispiel:**

```
Hit Time = 1 Zyklus
Miss Rate = 2%
Miss Penalty = 100 Zyklen

AMAT = 1 + 0,02 × 100 = 1 + 2 = 3 Zyklen
```

**Wichtig:**

$$\boxed{\text{Hit Rate allein ist KEIN gutes Leistungsmaß!}}$$

Warum? Cache mit höherer Hit Rate kann schlechtere AMAT haben!

---

## 7. Direct-Mapped Cache

### Grundprinzip

$$\boxed{\text{Jede Speicheradresse} \Rightarrow \text{Genau EINE Cache-Position}}$$

**Abbildung:**

$$\text{Cache-Index} = \text{Blockadresse} \mod \# \text{Cache-Blöcke}$$

### Blockadresse berechnen

$$\boxed{\text{Blockadresse} = \frac{\text{Byteadresse}}{\text{Bytes pro Block}}}$$

**Beispiel:** 4-Byte-Blöcke

```
Byteadresse 0:  Block 0
Byteadresse 4:  Block 1
Byteadresse 8:  Block 2
Byteadresse 12: Block 3
...
```

**Allgemein:**

```
Byteadresse: 01000₂ (8₁₀)
Block-Größe: 4 Bytes

Blockadresse = 8 / 4 = 2 = 010₂
```

### Cache-Index berechnen

**Wenn $\# \text{Blöcke} = 2^k$:**

$$\boxed{\text{Cache-Index} = \text{Untere } k \text{ Bits der Blockadresse}}$$

**Beispiel:**

```
Blockadresse = 34₁₀ = 100010₂
# Blöcke = 8 = 2³

Cache-Index = 34 mod 8 = 2 = 010₂
```

---

## 8. Adressaufteilung

### Komponenten einer Adresse

**32-Bit-Adresse:**

```
| Tag | Index | Block-Offset | Byte-Offset |
```

**Aufteilung:**

**1. Byte-Offset (2 Bit bei 4-Byte-Wörtern):**
- Adressiert Byte innerhalb eines Worts
- Letzte 2 Bits

**2. Wort-Offset:**
- Adressiert Wort innerhalb eines Blocks
- $\log_2(\text{Blockgröße in Wörtern})$ Bits

**3. Block-Offset:**
- Wort-Offset + Byte-Offset zusammen
- $\log_2(\text{Blockgröße in Bytes})$ Bits

**4. Index:**
- Cache-Position
- $\log_2(\# \text{Cache-Blöcke})$ Bits

**5. Tag:**
- Übrige Bits
- Zur Identifikation des Blocks

### Beispiel: 4 KB Cache

**Gegeben:**
- Cache-Größe: 4 KB = 4096 Bytes
- Blockgröße: 4 Bytes (1 Wort)
- Adresslänge: 32 Bit

**Berechnung:**

$$\# \text{Blöcke} = \frac{4096}{4} = 1024 = 2^{10}$$

$$\text{Index} = 10 \text{ Bit}$$

$$\text{Block-Offset} = \log_2(4) = 2 \text{ Bit}$$

$$\text{Tag} = 32 - 10 - 2 = 20 \text{ Bit}$$

**Adressaufteilung:**

```
|←─── 20 Bit ───→|←─ 10 Bit ─→|← 2 Bit →|
     Tag            Index      Block-Off
```

---

## 9. Daten im Cache finden

### Tag-Vergleich

**Problem:** Mehrere Speicherblöcke können auf gleichen Index abgebildet werden

**Lösung:** Tag speichern und vergleichen

**Ablauf:**

1. **Index extrahieren** aus Adresse
2. **Cache-Zeile lesen** an Index-Position
3. **Tag vergleichen:** Cache-Tag == Adress-Tag?
4. **Valid Bit prüfen:** Ist Block gültig?
5. **Hit/Miss:**
   - Tag gleich UND Valid = 1 → **Hit**
   - Sonst → **Miss**

### Cache-Block-Struktur

```
┌───────┬──────────┬─────────────────────┐
│ Valid │   Tag    │       Data          │
├───────┼──────────┼─────────────────────┤
│  1    │ 20 Bit   │    4 Bytes          │
└───────┴──────────┴─────────────────────┘
```

**Valid Bit = 1:** Block enthält gültige Daten

**Valid Bit = 0:** Block leer (z.B. nach Programmstart)

---

## 10. Cache-Gleichungen (Direct-Mapped)

### Grundlegende Formeln

$$\boxed{\text{BlockAddress} = \frac{\text{ByteAddress}}{\text{BytesPerBlock}}}$$

$$\boxed{\text{Cache-Index} = \text{BlockAddress} \mod \# \text{CacheBlocks}}$$

$$\boxed{\text{Tag} = \frac{\text{BlockAddress}}{\# \text{CacheBlocks}}}$$

$$\boxed{\text{Block-Offset} = \log_2(\text{BytesPerBlock}) \text{ Bits}}$$

### Beispiel-Berechnung

**Gegeben:**
- Cache: 64 Blöcke
- Blockgröße: 16 Bytes
- Byteadresse: 1204₁₀

**Gesucht:** Cache-Index

**Lösung:**

$$\text{BlockAddress} = \frac{1204}{16} = 75{,}25 \approx 75$$

$$\text{Cache-Index} = 75 \mod 64 = 11$$

---

## 11. Beispiel: Hit/Miss-Sequenz

### Setup

**Direct-Mapped Cache:**
- Größe: 8 Wörter = 8 Blöcke
- Blockgröße: 1 Wort (4 Bytes)
- Anfangs leer (alle Valid = 0)

**Zugriffe:**

| Zugriff | Adresse | Block | Index | Tag | Hit/Miss | Grund |
|---------|---------|-------|-------|-----|----------|-------|
| 1 | 0x00 | 0 | 0 | 0 | **Miss** | Valid = 0 |
| 2 | 0x04 | 1 | 1 | 0 | **Miss** | Valid = 0 |
| 3 | 0x00 | 0 | 0 | 0 | **Hit** | Im Cache |
| 4 | 0x20 | 8 | 0 | 1 | **Miss** | Tag ≠ |
| 5 | 0x00 | 0 | 0 | 0 | **Miss** | Verdrängt |

**Erklärung:**
- Zugriff 4: Block 8 wird auf Index 0 abgebildet → verdrängt Block 0
- Zugriff 5: Block 0 nicht mehr im Cache → Miss

---

## 12. Größere Blöcke

### Motivation

**Problem:** Blöcke von 1 Wort nutzen räumliche Lokalität nicht

**Lösung:** Größere Blöcke (32-64 Bytes typisch)

### Vorteile

✅ **Niedrigere Miss-Rate** durch räumliche Lokalität

✅ **Weniger Overhead:** Ein Block laden kostet weniger als n × 1 Wort laden

### Gleichungen bleiben gleich

$$\text{BlockAddress} = \frac{\text{ByteAddress}}{\text{BytesPerBlock}}$$

$$\text{Cache-Index} = \text{BlockAddress} \mod \# \text{CacheBlocks}$$

**Beispiel: 64 Blöcke, 16 Bytes/Block**

```
Byteadresse 1204:
  BlockAddress = 1204 / 16 = 75
  Cache-Index = 75 mod 64 = 11
```

---

## 13. Optimale Blockgröße

### Trade-offs

**Größere Blöcke:**

✅ **Pro:**
- Niedrigere Miss-Rate (räumliche Lokalität)
- Weniger Tag-Overhead

❌ **Contra:**
- Höherer Miss-Penalty (mehr Daten laden)
- Weniger Blöcke → mehr Konflikte
- Bei sehr großen Blöcken: Miss-Rate steigt wieder!

### Miss-Rate vs. Blockgröße

```
Miss Rate
    ↑
 25%│     Optimum
    │        ↓
 20%│      ╱╲
    │     ╱  ╲
 15%│    ╱    ╲___
    │   ╱         ╲___
 10%│  ╱              ╲___
    │ ╱                   ╲___
  5%│╱                        ╲
  0%└─────────────────────────────→
    16  32  64  128  256  512    Blockgröße (Bytes)
```

### AMAT-Optimierung

**Gegeben:**
- Hit Time = 1 Zyklus
- Miss Penalty = 10 + Wörter pro Block

**Miss Rates:**

| Blockgröße | Miss Rate |
|------------|-----------|
| 1 Wort | 25% |
| 2 Wörter | 15% |
| 4 Wörter | 5% |
| 8 Wörter | 7% |

**AMAT berechnen:**

**1 Wort:**

$$\text{AMAT} = 1 + 0{,}25 \times (10 + 1) = 1 + 2{,}75 = 3{,}75$$

**2 Wörter:**

$$\text{AMAT} = 1 + 0{,}15 \times (10 + 2) = 1 + 1{,}8 = 2{,}8$$

**4 Wörter:**

$$\text{AMAT} = 1 + 0{,}05 \times (10 + 4) = 1 + 0{,}7 = 1{,}7$$

**8 Wörter:**

$$\text{AMAT} = 1 + 0{,}07 \times (10 + 8) = 1 + 1{,}26 = 2{,}26$$

$$\boxed{\text{Optimal: 4 Wörter (AMAT = 1,7 Zyklen)}}$$

---

## 14. Verarbeitung von Misses

### Instruction Cache Miss

**Ablauf:**

1. **Pipeline stallen**
2. **PC sichern** (aktueller PC - 4)
3. **IF/ID Register löschen**
4. **Warten** bis Speicher Block geladen hat
5. **Cache-Block füllen**
6. **Tag und Valid Bit setzen**
7. **Befehl erneut holen**
8. **Pipeline fortsetzen**

### Data Cache Miss

**Ablauf:**

1. **Pipeline stallen** (ab MEM-Stufe)
2. **Warten** bis Block geladen
3. **Cache aktualisieren**
4. **Pipeline fortsetzen**

**Wichtig:** Frühere Stufen können weiterlaufen!

---

## 15. Schreiboperationen

### Write-Through (Durchschreibetechnik)

$$\boxed{\text{Schreibe in Cache UND Hauptspeicher}}$$

✅ **Vorteil:** Cache und Speicher immer konsistent

❌ **Nachteil:** Schlechte Leistung (CPU wartet auf Speicher)

**Beispiel:**

```
CPI ohne Misses: 1,0
Schreiboperation: 100 Zyklen
10% Schreibbefehle

CPI = 1,0 + 0,1 × 100 = 11
→ 10× langsamer!
```

### Verbesserung: Write Buffer

**Idee:** Zwischenspeicher für Schreiboperationen

```
CPU → Write Buffer → Hauptspeicher
        ↓
   CPU läuft weiter!
```

**CPU stopt nur wenn:** Write Buffer voll

### Write-Back (Rückschreibetechnik)

$$\boxed{\text{Schreibe NUR in Cache}}$$

**Dirty Bit:** Markiert veränderte Blöcke

✅ **Vorteil:** Bessere Leistung (mehrere Schreibvorgänge kombiniert)

❌ **Nachteil:** 
- Cache und Speicher inkonsistent
- Komplexere Implementierung
- Beim Verdrängen: Dirty Block muss zurückgeschrieben werden

### Write-Back Buffer

**Auch Write-Back Caches haben Buffer:**
- Für verdrängte Dirty Blocks
- Verhindert Stalling bei Verdrängung

### Vergleich

| Eigenschaft | Write-Through | Write-Back |
|-------------|---------------|------------|
| **Konsistenz** | ✅ Immer | ❌ Verzögert |
| **Leistung** | ❌ Langsam | ✅ Schnell |
| **Komplexität** | ✅ Einfach | ❌ Komplex |
| **Buffer** | Write Buffer | Write-Back Buffer |
| **Dirty Bit** | Nicht nötig | ✅ Benötigt |

---

## 16. Beispiel: Intrinsity FastMATH

### Spezifikationen

**Prozessor:**
- Embedded MIPS mit 12-Stufen-Pipeline
- Split Cache (getrennt I-Cache und D-Cache)

**Beide Caches:**
- Größe: 16 KB
- Direct-Mapped
- Blockgröße: 64 Bytes (16 Wörter)
- Adresslänge: 32 Bit

### Parameter berechnen

**# Blöcke:**

$$\# \text{Blöcke} = \frac{\text{Cache-Größe}}{\text{Blockgröße}} = \frac{16 \times 1024}{64} = 256 = 2^8$$

**Index:**

$$\text{Index} = \log_2(256) = 8 \text{ Bit}$$

**Block-Offset:**

$$\text{Block-Offset} = \log_2(64) = 6 \text{ Bit}$$

**Tag:**

$$\text{Tag} = 32 - 8 - 6 = 18 \text{ Bit}$$

### Adressaufteilung

```
|←──── 18 Bit ────→|← 8 Bit →|←── 6 Bit ──→|
       Tag           Index    Block-Offset
```

**Block-Offset weiter aufgeteilt:**

```
Block-Offset (6 Bit) = Wort-Offset (4 Bit) + Byte-Offset (2 Bit)
                         └─→ 16 Wörter       └─→ 4 Bytes/Wort
```

### Cache-Struktur

```
┌───────┬──────────┬──────────────────────────────┐
│ Valid │ Tag (18) │  Data (64 Bytes = 16 Wörter)│
├───────┼──────────┼──────────────────────────────┤
│   1   │  18 Bit  │  Wort 0 | Wort 1 | ... | 15 │
└───────┴──────────┴──────────────────────────────┘
  ↑                             ↑
  1 Bit                   512 Bit (64 × 8)
```

**Pro Cache-Zeile:** 1 + 18 + 512 = 531 Bit

**Gesamter Cache:** 256 × 531 = 135.936 Bit ≈ 17 KB

**Overhead:** (17 KB - 16 KB) / 16 KB = 6,25%

---

## 17. Implementierungskosten

### Allgemeine Berechnung

**Gegeben:**
- Cache-Größe: 16 KB Daten
- Blockgröße: 4 Wörter (16 Bytes)
- Adresslänge: 32 Bit

**Berechnung:**

**# Blöcke:**

$$\# \text{Blöcke} = \frac{16 \times 1024}{4 \times 4} = \frac{16384}{16} = 1024 = 2^{10}$$

**Pro Block:**
- **Daten:** 4 Wörter × 32 Bit = 128 Bit
- **Tag:** 32 - 10 (Index) - 2 (Wort-Offset) - 2 (Byte-Offset) = 18 Bit
- **Valid:** 1 Bit
- **Gesamt:** 128 + 18 + 1 = 147 Bit

**Gesamter Cache:**

$$1024 \times 147 = 150{,}528 \text{ Bit} = 18{,}816 \text{ Bytes} = 18{,}4 \text{ KB}$$

**Overhead:**

$$\text{Overhead} = \frac{18{,}4 - 16}{16} = 15\%$$

### Formel für Implementierungskosten

$$\boxed{\text{Bits}_{\text{gesamt}} = \# \text{Blöcke} \times (1 + \text{Tag-Bits} + \text{Data-Bits})}$$

---

## 📌 Zusammenfassung

### Speicherhierarchie-Prinzipien

**1. Lokalitätsprinzip:**

$$\boxed{\text{Temporal: kürzlich genutzt} \Rightarrow \text{bald wieder genutzt}}$$

$$\boxed{\text{Spatial: X genutzt} \Rightarrow \text{Nachbarn von X bald genutzt}}$$

**2. Cache-Hierarchie:**

```
Register < L1 < L2 < L3 < DRAM < Disk
  ↑                                ↑
Schnell, klein, teuer     Langsam, groß, billig
```

### Cache-Performance

**AMAT (Average Memory Access Time):**

$$\boxed{\text{AMAT} = \text{Hit Time} + \text{Miss Rate} \times \text{Miss Penalty}}$$

**Ziel:** AMAT minimieren (nicht nur Hit Rate maximieren!)

### Direct-Mapped Cache

**Abbildung:**

$$\text{Cache-Index} = \text{BlockAddress} \mod \# \text{CacheBlocks}$$

**Adressaufteilung:**

```
| Tag | Index | Block-Offset | Byte-Offset |
```

**Cache-Zeile:**

```
| Valid (1) | Tag | Data |
```

### Wichtige Gleichungen

**Blockadresse:**

$$\text{BlockAddress} = \frac{\text{ByteAddress}}{\text{BytesPerBlock}}$$

**Index-Bits:**

$$\text{Index-Bits} = \log_2(\# \text{CacheBlocks})$$

**Block-Offset-Bits:**

$$\text{Block-Offset-Bits} = \log_2(\text{BytesPerBlock})$$

**Tag-Bits:**

$$\text{Tag-Bits} = \text{Adresslänge} - \text{Index-Bits} - \text{Block-Offset-Bits}$$

### Schreibstrategien

**Write-Through:**
- ✅ Einfach, konsistent
- ❌ Langsam
- Lösung: Write Buffer

**Write-Back:**
- ✅ Schnell
- ❌ Komplex, inkonsistent
- Benötigt: Dirty Bit

### Blockgröße-Trade-offs

**Klein:**
- ❌ Höhere Miss-Rate
- ✅ Niedriger Miss-Penalty

**Groß:**
- ✅ Niedrigere Miss-Rate (bis Optimum)
- ❌ Höherer Miss-Penalty
- ❌ Weniger Blöcke → mehr Konflikte

**Optimal:** Balance finden via AMAT-Berechnung

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.05 Single Cycle]]: Speicherzugriff im Datenpfad
- [[VL.06 Leistung]]: CPI wird durch Cache-Misses erhöht
- [[VL.07 Pipelining]]: Cache-Misses verursachen Pipeline-Stalls
- [[VL.09 Cache]]: TLB als Cache für Seitentabellen