**Class:** [[ROrg]]  
**Date:** 2025  
**Topics:** #Cache #Speicherhierarchie #Assoziativität #Hauptspeicher #CacheLeistung

---

## 🎯 Lernziele der Vorlesung

Nach dieser Vorlesung können Sie:

- Verschiedene Cache-Organisationen erklären: **satzassoziativer Cache**, **vollassoziativer Cache**, **Cache-Hierarchie**
- Den **Einfluss des Caches auf die CPU-Zeit** bestimmen
- **Fehlzugriffsrate** und **Fehlzugriffsaufwand** eines Caches reduzieren
- **Speicherbandbreite** von Systemen berechnen und optimieren

---

## 1. Hauptspeicher und Bandbreite

### Eigenschaften von DRAM

**DRAM-Bausteine:**

- Hauptspeicher aus DRAM aufgebaut
- Optimiert auf **Dichte**, nicht auf **Zugriffszeit**
- **Latenz** schwer zu reduzieren
- **Bandbreite** zwischen Cache und Speicher kann erhöht werden

### Bus-Verbindung

Cache und Speicher über **Bus** verbunden:

- Bus-Takt **10× langsamer** als CPU-Takt

**Beispiel: Anzahl Bus-Takte**

- 1 Bus-Takt: Senden der Adresse
- 15 Bus-Takte: Jeder DRAM-Zugriff
- 1 Bus-Takt: Senden eines Datenworts

### Berechnung Speicherbandbreite

**Beispiel:** Blöcke von 4 Wörtern mit 1-Wort breitem DRAM

$$\text{Fehlzugriffsaufwand} = 1 + 4 \times 15 + 4 \times 1 = 65 \text{ Bus-Takte}$$

$$\boxed{\text{Bandbreite} = \frac{16 \text{ Byte}}{65 \text{ Bus-Zyklen}} = 0.25 \text{ Byte/Takt}}$$

### Speicherbandbreite erhöhen

**Methoden zur Erhöhung:**

|Methode|Fehlzugriffsaufwand|Verbesserung|
|---|---|---|
|1-Wort-breit (Basis)|65 Bus-Takte|-|
|2-Wort-breit|$1 + 2 \times 15 + 2 \times 1 = 33$|~2× schneller|
|4-Wort-breit|$1 + 15 + 1 = 17$|~4× schneller|
|Verschachtelt (4 Banken)|$1 + 15 + 4 \times 1 = 20$|~3× schneller|

---

## 2. Einfluss der Cache-Leistung auf CPU-Zeit

### CPU-Zeit Modell

$$\boxed{\text{CPU-Zeit} = (\text{CPU-Ausführungszyklen} + \text{Speicherstillstands-Zyklen}) \times \text{Taktzeit}}$$

**Speicherstillstands-Zyklen:**

$$\text{Speicherstillstands-Zyklen} = \text{Lesestillstands-Zyklen} + \text{Schreibestillstands-Zyklen}$$

**Vereinfachtes Modell (unter Annahmen):**

$$\boxed{\text{Speicherstillstands-Zyklen} = N_{\text{Befehle}} \times \frac{\text{Fehlzugriffe}}{\text{Befehl}} \times \text{Fehlaufwand}}$$

### Beispiel: Cache-Leistung Einfluss

**Gegeben:**

- Fehlzugriffsrate Befehlscache: 2%
- Fehlzugriffsrate Datencache: 4%
- CPI ohne Speicherstillstände (perfekter Cache): 2
- Fehleraufwand: 100 Zyklen
- 36% Lade/Speicher-Befehle

**Berechnung:**

$$\text{Befehlsfehlzugriffs-Zyklen} = N_{\text{instr}} \times 0.02 \times 100 = 2 \times N_{\text{instr}}$$

$$\text{Datenfehlzugriffs-Zyklen} = N_{\text{instr}} \times 0.36 \times 0.04 \times 100 = 1.44 \times N_{\text{instr}}$$

$$\boxed{\text{CPI}_{\text{real}} = 2 + 2 + 1.44 = 5.44}$$

**Ergebnis:** Prozessor mit perfektem Cache ist Faktor $\frac{5.44}{2} = 2.72$ schneller

### Einfluss Hauptspeichergeschwindigkeit

**Szenario:** Taktgeschwindigkeit verdoppelt, Hauptspeicher unverändert

- Fehleraufwand: 200 Zyklen (statt 100)

**Neue Berechnung:**

$$\text{Befehlsfehlzugriffs-Zyklen} = N_{\text{instr}} \times 0.02 \times 200 = 4 \times N_{\text{instr}}$$

$$\text{Datenfehlzugriffs-Zyklen} = N_{\text{instr}} \times 0.36 \times 0.04 \times 200 = 2.88 \times N_{\text{instr}}$$

$$\text{CPI}_{\text{schnell}} = 2 + 4 + 2.88 = 8.88$$

$$\boxed{\text{Leistungssteigerung} = \frac{5.44}{8.88/2} = 1.23}$$

**Wichtig:** Nur 1.23× schneller statt erwartete 2× durch Memory-Bottleneck!

---

## 3. Cache-Leistung verbessern

### AMAT-Formel

$$\boxed{\text{AMAT} = \text{hit time} + \text{miss rate} \times \text{miss penalty}}$$

**Drei Ansätze:**

1. ✅ **Trefferzeit** (hit time) verbessern
2. ✅ **Fehlzugriffsrate** (miss rate) reduzieren → **Assoziative Caches**
3. ✅ **Fehlzugriffsaufwand** (miss penalty) reduzieren → **Cache-Hierarchie**

---

## 4. Assoziative Caches

### Motivation

**Problem:** Konflikt-Fehlzugriffe

**Beispiel:**

```c
for (i=0; i<n; i++)
    dotprod += a[i] * b[i];
```

Wenn `a[i]` und `b[i]` auf **gleichen Cache-Block** abgebildet werden:

- Jeder Zugriff generiert Fehlzugriff!
- Tritt auf, wenn Arrays hintereinander allokiert und Größe Vielfaches der Cache-Größe

**Lösung:** Flexiblere Platzierung → **Assoziative Caches**

### Cache-Organisationen

#### 1. Direkt abgebildeter Cache (Direct Mapped)

- Ein Block hat **genau eine** mögliche Position im Cache
- $\text{Cache-Index} = \text{Blockadresse} \mod (\text{Anzahl Blöcke})$
- ✅ Einfach, schnell
- ❌ Viele Konflikt-Fehlzugriffe

#### 2. Vollassoziativer Cache (Fully Associative)

- Block kann an **jeder Stelle** im Cache platziert werden
- Auch **Content Addressable Memory (CAM)** genannt
- **Alle Einträge** müssen parallel durchsucht werden
- Benötigt **1 Vergleicher pro Cache-Eintrag**
- ✅ Minimale Fehlzugriffsrate
- ❌ Teuer, nur für kleine Caches praktikabel

#### 3. n-fach satzassoziativer Cache (n-way Set Associative)

- Cache besteht aus **Sätzen** (Sets) mit je **n Ways**
- Blockadresse bestimmt **Satz**: $\text{Satz-Index} = \text{Blockadresse} \mod (\text{Anzahl Sätze})$
- Innerhalb eines Satzes: flexible Platzierung
- Benötigt **n Vergleicher**
- ✅ Guter Kompromiss zwischen Leistung und Kosten

### Vergleich der Organisationen

**Cache mit 8 Blöcken:**

|Organisation|Anzahl Sätze|Ways pro Satz|Vergleicher|
|---|---|---|---|
|Direct Mapped|8|1|1|
|2-way Set Associative|4|2|2|
|4-way Set Associative|2|4|4|
|Fully Associative|1|8|8|

### Beispiel: Zugriffsmuster

**Blockadressen-Sequenz:** 0, 8, 0, 6, 8

**4-Block-Cache, Direct Mapped:**

- Cache-Index = Blockadresse mod 4
- 0 → Index 0: Miss
- 8 → Index 0: Miss (verdrängt Block 0)
- 0 → Index 0: Miss (verdrängt Block 8)
- 6 → Index 2: Miss
- 8 → Index 0: Miss
- **Ergebnis:** 0 Treffer, 5 Fehlzugriffe

**4-Block-Cache, 2-way Set Associative:**

- Satz-Index = Blockadresse mod 2
- Besseres Ergebnis durch flexible Platzierung

**4-Block-Cache, Fully Associative:**

- Beste Fehlzugriffsrate

---

## 5. Ersetzungsstrategien

Bei mehreren möglichen Positionen: Welcher Block wird ersetzt?

### Ersetzungsverfahren

|Verfahren|Beschreibung|Aufwand|
|---|---|---|
|**Random**|Zufälliger Block im Satz|Gering|
|**FIFO**|First-In-First-Out: Ältester Block|Mittel|
|**LRU**|Least Recently Used: Am längsten nicht verwendet|Hoch|
|**OPT/MIN**|Optimal: Block, der am spätesten wieder benötigt wird|Nicht implementierbar|

**LRU:**

- Meist beste praktische Strategie
- Für > 4-way: Approximationen notwendig
- Komplexe Hardware

### Einfluss der Assoziativität

**Simulation:** 64KB Datencache, 64-Byte Blöcke, SPEC2000

|Assoziativität|Fehlrate|
|---|---|
|1-fach (Direct Mapped)|10.3%|
|2-fach|8.6%|
|4-fach|8.3%|
|8-fach|8.1%|

**Beobachtung:** Abnehmende Rendite (diminishing returns) bei höherer Assoziativität

---

## 6. Organisation satzassoziativer Cache

### Adressaufteilung

Für **n-way set associative cache:**

$$\text{Adresse} = [\text{Tag}][\text{Index}][\text{Block Offset}]$$

**Block Offset:** $\log_2(\text{Blockgröße in Bytes})$ Bits

**Index:** $\log_2(\text{Anzahl Sätze})$ Bits

**Tag:** Restliche Bits

### Beispiel: Cache-Dimensionierung

**Gegeben:**

- Cache-Größe: 4 KB
- 4-fach satzassoziativ
- Blockgröße: 4 Wörter à 4 Bytes = 16 Bytes
- Adresslänge: 32 Bit

**Berechnung:**

$$\boxed{\text{Cache-Größe} = \text{Anzahl Sätze} \times \text{Assoziativität} \times \text{Blockgröße}}$$

$$\text{Anzahl Sätze} = \frac{4096}{4 \times 16} = 64 = 2^6$$

**Adressaufteilung:**

- Block Offset: $\log_2(16) = 4$ Bits
- Index: $\log_2(64) = 6$ Bits
- Tag: $32 - 6 - 4 = 22$ Bits

---

## 7. Cache-Speicherhierarchie (Multi-Level Cache)

### Motivation

**Fehlzugriffsaufwand** durch mehrere Cache-Ebenen reduzieren

### Typische Hierarchie

```
CPU
 ↓
L1-Cache (klein, schnell)
 ↓
L2-Cache (größer, langsamer)
 ↓
L3-Cache (optional, noch größer)
 ↓
Hauptspeicher (groß, langsam)
```

### Eigenschaften der Cache-Ebenen

|Ebene|Größe|Trefferzeit|Eigenschaften|
|---|---|---|---|
|**L1**|32-64 KB|1-3 Zyklen|Pro Core, getrennt I/D möglich|
|**L2**|256 KB - 1 MB|10-50 Zyklen|Pro Core, unified|
|**L3**|1.5-30 MB|~50 Zyklen|Shared zwischen Cores|
|**RAM**|GB-Bereich|100-500 Zyklen|DRAM|

### Beispiel: Intel Haswell

**L1I Cache:**

- 32 KB, 8-way set associative
- 64 B Blockgröße, Write-back
- Pro Core, shared von 2 Threads

**L1D Cache:**

- 32 KB, 8-way set associative
- 64 B Blockgröße
- 4 Zyklen schnellstes load-to-use
- Bandbreite: 64 Bytes/Zyklus (load), 32 Bytes/Zyklus (store)

**L2 Cache:**

- 256 KB, 8-way set associative, unified
- 11 Zyklen schnellstes load-to-use
- 64 B/Zyklus Bandbreite zu L1

**L3 Cache:**

- 1.5-3 MB pro Core
- Write-back

---

## 8. Leistung Cache-Hierarchie

### Beispielrechnung

**Gegeben:**

- Grund-CPI: 1.0 (alle Zugriffe im L1)
- Taktgeschwindigkeit: 4 GHz (0.25 ns/Zyklus)
- Hauptspeicher: 100 ns (400 Zyklen)
- Fehlrate L1: 2%

**Nur L1-Cache:**

$$\text{CPI} = 1.0 + 0.02 \times 400 = 9.0$$

**Mit L2-Cache:**

- L2 Zugriffszeit: 5 ns (20 Zyklen)
- L2 lokale Fehlrate: 25%

$$\text{Fehlaufwand}_{\text{L1}} = \text{Trefferzeit}_{\text{L2}} + \text{Fehlrate}_{\text{L2}} \times \text{Fehlaufwand}_{\text{L2}}$$

$$\text{Fehlaufwand}_{\text{L1}} = 20 + 0.25 \times 400 = 120 \text{ Zyklen}$$

$$\boxed{\text{CPI} = 1.0 + 0.02 \times 120 = 3.4}$$

**Beschleunigung:** $\frac{9.0}{3.4} = 2.6\times$ schneller mit L2-Cache!

### Überlegungen zum Multi-Level Cache

**L1-Cache:**

- Ziel: Minimale **Trefferzeit**
- Klein, einfache Organisation
- Kleinere Blockgrößen

**L2-Cache:**

- Ziel: Geringe **Fehlzugriffsrate**
- Trefferzeit weniger kritisch
- Größer, höhere Assoziativität
- Größere Blockgrößen

---

## 📌 Zusammenfassung

### Wichtige Formeln

$$\boxed{\text{Bandbreite} = \frac{\text{Datenmenge}}{\text{Anzahl Zyklen}}}$$

$$\boxed{\text{CPI}_{\text{real}} = \text{CPI}_{\text{ideal}} + \text{Speicherstillstands-Zyklen pro Befehl}}$$

$$\boxed{\text{AMAT} = \text{hit time} + \text{miss rate} \times \text{miss penalty}}$$

$$\boxed{\text{Cache-Größe} = \text{Anzahl Sätze} \times \text{Assoziativität} \times \text{Blockgröße}}$$

$$\boxed{\text{Satz-Index} = \text{Blockadresse} \mod (\text{Anzahl Sätze})}$$

$$\boxed{\text{Blockadresse} = \frac{\text{Byteadresse}}{\text{Blockgröße in Bytes}}}$$

### Cache-Organisationen im Vergleich

|Eigenschaft|Direct Mapped|n-way Set Assoc.|Fully Associative|
|---|---|---|---|
|Flexibilität|❌ Gering|⚠️ Mittel|✅ Maximal|
|Fehlrate|❌ Hoch|⚠️ Mittel|✅ Niedrig|
|Hardware-Aufwand|✅ Gering|⚠️ Mittel|❌ Hoch|
|Vergleicher|1|n|Alle Einträge|

### Methoden zur Leistungsverbesserung

1. **Assoziative Caches:** Reduzieren Fehlzugriffsrate durch flexible Platzierung
2. **Cache-Hierarchie:** Reduziert Fehlzugriffsaufwand durch schnelle Zwischenspeicher
3. **Speicherbandbreite erhöhen:** Breitere Speicher oder Verschachtelung

### Kernaussagen

✅ Cache-Hierarchie schließt Prozessor/DRAM-Leistungslücke

✅ Temporale und räumliche Lokalität ermöglichen hohe Trefferquoten

✅ Höhere Assoziativität verbessert Fehlrate, aber mit abnehmender Rendite

✅ L1 optimiert auf Trefferzeit, L2+ auf Fehlrate

✅ Memory-Bandbreite kann zum Bottleneck werden

---

## 🔗 Verbindungen zu anderen Vorlesungen

- Speicherhierarchie: Grundlage für parallele Architekturen
- Performance-Modelle: CPI-Berechnungen