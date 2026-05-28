**Class:** [[SysProg - Systemprogrammierung]]
**Date:** 08-05-2026
**Topics:** #Scheduling #FCFS #LCFS #RoundRobin #Prioritäten #Echtzeit #RMS #EDF #Linux #Windows

---

## 🎯 Lernziele der Vorlesung

VL.03 behandelt **Scheduling** (Ablaufplanung) — die räumliche und zeitliche Zuordnung von Aktivitäten zu Prozessoren. Die Reihenfolge von Prozessen beeinflusst die wahrgenommene Rechnerleistung massiv.

**Gliederung:**
- 3.1 Einführung
- 3.2 Schedulingstrategien
- 3.3 Multilevel-Scheduling
- 3.4 Scheduling mit Sollzeitpunkten (Echtzeit)
- 3.5 Fallbeispiele: Linux und Windows

---

## 3.1 Einführung

### Definition

**Scheduling** (Ablaufplanung) = räumliche und zeitliche Zuordnung von Aktivitäten zu Instanzen, welche diese Aktivitäten durchführen können.

Scheduling beeinflusst die **subjektive Wahrnehmung** der Rechnerleistung stark:

| Reihenfolge | Wirkung |
|------------|---------|
| P2 (E-Mail) → P1 (Fenster schließen) | Verzögerung sofort wahrnehmbar → Rechner wirkt langsam |
| P1 (Fenster schließen) → P2 (E-Mail) | E-Mail-Verzögerung um 2 s bleibt wahrscheinlich unbemerkt |

### Zeitskalen des Schedulings

| Ebene | Zuständigkeit |
|-------|-------------|
| **LTS** (Long-Term Scheduling) | Erzeugung und Zerstörung von Prozessen (ausreichend Ressourcen?) |
| **MTS** (Medium-Term Scheduling) | Ein- und Auslagern von Prozessen (Swap in/out) |
| **STS** (Short-Term Scheduling) | Zuweisung der CPU(s) zu bereiten Prozessen → **Fokus dieser VL** |
| **Dispatching** | Durchführen der CPU-Zuweisung |

„Scheduling" meint gewöhnlich **CPU Scheduling = STS**.

### Klassisches Scheduling-Problem

Zuordnung von Prozessen zu Prozessoren so, dass die **Ausführungszeit (Makespan) minimiert** wird. Darstellung im **Gantt-Diagramm**: Jeder Prozessor auf einer Zeitachse, Prozesse als Blöcke.

![[Screenshot 2026-05-07 at 13.42.31.png|center|581x403]]
### Mehrere Warteschlangen

![[VL.03 Scheduling-1778154373566.webp|800x374]]
### Gestaltungsparameter

**Prozessmenge:**
- **Statisch**: keine neuen Prozesse kommen hinzu
- **Dynamisch**: neue Prozesse kommen während der Ausführung hinzu

**Scheduling-Zeitpunkt:**
- **Off-line**: alle Prozesse bekannt → vollständige Information
- **On-line** (zur Laufzeit): nur aktuelle Prozesse bekannt → unvollständige Information

**Verdrängung (Preemption):**
- Scheduling-Entscheidung bei Änderung der Bereit-Liste
- Mit Verdrängung können Ziele besser erreicht werden

**Weitere Parameter:**
- Abhängigkeiten zwischen Prozessen (Reihenfolgebeziehungen, Kommunikationszeiten)
- Prioritäten (statisch oder dynamisch)
- Sollzeitpunkte / Deadlines (Echtzeitsysteme)
- Periodische Prozesse

### Zielfunktionen

| Ziel | Optimierung |
|------|------------|
| Länge des Ablaufplans | min |
| Maximale Antwortzeit | min |
| Mittlere (gewichtete) Antwortzeit | min |
| Anzahl Prozessoren | min |
| Durchsatz | max |
| Prozessorauslastung | max |
| Maximale Verspätung | min |

**Universelle Ziele (alle Systemarten):**
- **Fairness**: gerechte Verteilung der Rechenzeiten
- **Policy Enforcement**: transparente Entscheidungskriterien
- **Balance**: alle Teile des Systems sind ausgelastet

---

## 3.2 Schedulingstrategien

### Definitionen

$$\text{Antwortzeit} = \text{Wartezeit} + \text{Bedienzeit}$$

- **Wartezeit** (*waiting time*): Zeit vom Programmstart bis Beginn der Bedienung
- **Bedienzeit** (*service time*): tatsächliche Rechenzeit
- **Antwortzeit** (*response time*): Gesamtzeit vom Start bis Ende

### FCFS — First Come First Served (= FIFO)

- Bearbeitung in Reihenfolge der Ankunft in der Bereitliste
- Prozessorbesitz bis zum **Ende** oder zur freiwilligen Aufgabe
- **Keine Verdrängung**
- Entspricht der Alltagserfahrung

### LCFS — Last Come First Served

- Bearbeitung in **umgekehrter** Ankunftsreihenfolge
- Prozessorbesitz bis zum Ende oder zur freiwilligen Aufgabe
- In dieser reinen Form selten benutzt

### LCFS-PR — Last Come First Served Preemptive Resume

- Neuankömmling **verdrängt** den rechnenden Prozess; verdrängter Prozess kommt hinten in die Warteschlange
- Ziel: **Bevorzugung kurzer Prozesse** — kurzer Prozess hat die Chance, schnell (vor nächster Ankunft) fertig zu werden
- Langer Prozess kann mehrfach verdrängt werden
- Nach Eintreffen aller Prozesse: Warteschlange wird nach **FIFO** abgearbeitet

### Zeitscheibenbetrieb (Time Sharing, Round Robin)

- Jeder Prozess erhält im festen Takt ein **Zeitfenster** zugeteilt
- Am Ende des Zeitfensters: Prozess wird unterbrochen und hinten angestellt
- Voraussetzung: Prozesse unterbrechbar, Prozessumschaltung möglich
- Abfolge: $P_{11} \to P_{21} \to P_{31} \to P_{12} \to P_{22} \to P_{32} \to \ldots$

**Round Robin — Wahl der Zeitscheibenlänge $t$:**

| $t$ | Effekt |
|-----|--------|
| Groß | RR nähert sich FCFS |
| Klein | Hoher Overhead durch häufiges Umschalten |
| Typisch | **Millisekunden-Bereich** |

Tradeoff: **Reaktionsgeschwindigkeit vs. Overhead**

### PRIO-NP — Priorities Non-preemptive

- Neuankömmlinge werden nach **Priorität** in die Bereitliste eingeordnet
- Prozessorbesitz bis zum Ende oder zur freiwilligen Aufgabe
- **Keine Verdrängung** des laufenden Prozesses

### PRIO-P — Priorities Preemptive

- Wie PRIO-NP, aber: Neuankömmling mit **höherer Priorität verdrängt** rechnenden Prozess

### Prioritätsinvertierung

**Problem:** Prozess C (Prio 12) „verhungert":
- A (Prio 4) besitzt ein Betriebsmittel, das C braucht
- B (Prio 8) belegt dauerhaft die CPU → A kann Betriebsmittel nicht freigeben → C blockiert

![[VL.03 Scheduling-1778160258738.webp|662x259]]

**Lösung: Prioritätsvererbung** (*priority inheritance*): A bekommt temporär die Priorität von C, solange A das Betriebsmittel besitzt, auf das C wartet.

### SJN — Shortest Job Next

- Prozess mit **kürzester Bedienzeit** wird zuerst bearbeitet
- Wie PRIO-NP mit Bedienzeit als umgekehrtem Prioritätskriterium
- **Keine Verdrängung**; bevorzugt kurze Prozesse

### SRTN — Shortest Remaining Time Next

- Prozess mit **kürzester Restbedienzeit** wird zuerst bearbeitet
- **Mit Verdrängung**
- Nachteil: Schätzung der Bedienzeit stammt vom Benutzer
- Längere Prozesse können „verhungern" (starvation)

### HRRN — Highest Response Ratio Next

Response Ratio dynamisch berechnet als:

$$rr := \frac{\text{Wartezeit} + \text{Bedienzeit}}{\text{Bedienzeit}}$$

- Prozess mit **größtem $rr$-Wert** wird als nächster ausgewählt
- **Keine Verdrängung**
- Bevorzugt kurze Prozesse; lange Prozesse können durch Warten „Punkte sammeln"
- Verhindert damit das Verhungern langer Prozesse

---

## 3.3 Multilevel-Scheduling

**Idee:** Kombination verschiedener Scheduling-Verfahren durch Unterteilung der bereiten Prozesse in **mehrere priorisierte Listen**.

**Einfachste Realisierung:**
- Prozesse werden bei Erzeugung einer Liste zugeordnet
- Jede Liste hat eigene Strategie
- Scheduler: suche höchst-priorisierte nicht-leere Liste → Strategie dieser Liste bestimmt nächsten Prozess

**Beispiel: Multilevel mit wachsenden Zeitscheiben:**

![[VL.03 Scheduling-1778162429266.webp|723x370]]

### Multilevel-Feedback-Scheduling

*(Ursprung: Corbató, MULTICS)*

**Schlüsselidee:** Zugehörigkeit zur Ebene ist **nicht fest** — Prozesse können hoch- oder heruntergestuft werden.

**Regeln:**
- Neue Prozesse starten mit **hoher Priorität** (Annahme: kurz → SJN-Idee)
- Prozess verbraucht gesamte Zeitscheibe → wird in **nächste Liste** (längere Zeitscheibe, geringere Priorität) verschoben
- Prozess gibt CPU freiwillig ab oder blockiert → **verbleibt** in aktueller Liste (bevorzugt E/A-intensive und interaktive Prozesse)
- Optionaler **Aging**: Erhöhung der Priorität bei langer Wartezeit (verhindert starvation)
- 
![[VL.03 Scheduling-1778162488685.webp|694x345]]

Freiwillige CPU-Abgabe / Blockierung → Prozess **verbleibt** in aktueller Warteschlange oder wird hochgestuft.

---

## 3.4 Scheduling mit Sollzeitpunkten (Echtzeit)

### Grundlagen

**Sollzeitpunkte** (Deadlines) = Prozesse müssen zu bestimmten Zeitpunkten abgeschlossen sein.

| Typ | Verletzung | Beispiele |
|-----|-----------|----------|
| **Hard real-time** | Untolerierbar → Systemausfall | Airbag, ABS, Ventilsteuerung |
| **Soft real-time** | Tolerierbar → Qualitätsverlust | Audio-/Videostreaming |

### Wichtige Zeitpunkte für Prozess $P_i$

$$a_i \leq s_i \leq e_i \leq d_i$$

| Symbol | Bedeutung |
|--------|----------|
| $a_i$ | Frühester Startzeitpunkt |
| $s_i$ | Tatsächlicher Startzeitpunkt |
| $e_i$ | Tatsächlicher Endzeitpunkt |
| $d_i$ | Spätester Endzeitpunkt (Deadline) |
| $b_i = e_i - s_i$ | Bedienzeit (*service time*) |
| $sl_i = d_i - e_i$ | Spielraum (*slack time / laxity*) |

### Verspätungen

Verspätung: $L_i = e_i - d_i$ (positiv wenn Deadline überschritten)

**Zwei Zielfunktionen bei Soft-RTS:**

1. **Minimierung von $L_{max}$**: alle Deadlines werden gleichmäßig knapp verpasst
2. **Einhaltung möglichst vieler Deadlines**: kürzere Prozesse zuerst → mehr Deadlines eingehalten (aber $L_{max}$ steigt)

### EDD — Earliest Due Date (Jacksons Regel)

- Voraussetzung: 1-CPU, keine Verdrängung, keine Abhängigkeiten, alle Prozesse gleichzeitig startbereit
- **Theorem**: Ablaufplan mit Prozessen nach **nicht fallenden Sollzeitpunkten** sortiert ist optimal bzgl. $L_{max}$
- Aufwand: nur $\mathcal{O}(n \log n)$
- **Problem in der Praxis**: Unterschiedliche Startzeitpunkte machen das Problem **NP-schwer**

### EDF — Earliest Deadline First

- Voraussetzung: vorgegebene Startzeitpunkte, **Verdrängung möglich**
- **Theorem**: Ablaufplan, bei dem zu jedem Zeitpunkt der Prozess mit **frühestem Sollzeitpunkt** unter allen ablaufbereiten Prozessen zugeordnet wird, ist optimal bzgl. $L_{max}$

### Periodische Prozesse

Periodische Aufgaben kommen in regelmäßigen Abständen wieder.

**Schedulability Test (Feasibility Test):**

Notwendige Bedingung für jeden Prozess:

$$0 < b_i \leq d_i \leq p_i$$

Notwendige Bedingung für alle Prozesse:

$$\sum_i \frac{b_i}{p_i} \leq 1$$

### Rate Monotonic Scheduling (RMS)

**Annahmen:**
- $T_i$ periodisch mit Periodenlänge $p_i$; Deadline $d_i = p_i$
- $T_i$ unmittelbar nach $p_i$ erneut bereit; konstante Bedienzeit $b_i \leq p_i$
- **Je kleiner die Periode, desto höher die Priorität** (statisch)

**Hinreichende Bedingung (RMS-Kriterium):**

$$\sum_{i=1}^{n} \frac{b_i}{p_i} \leq n \left(2^{\frac{1}{n}} - 1\right)$$

Bei großem $n$: CPU-Auslastung höchstens $\ln 2 \approx 69{,}3\%$

**Beispiel:** $T = \{T_1, T_2, T_3\}$, $p = \{4, 6, 8\}$, $b = \{1, 2, 1\}$

Notwendige Bedingung:

$$\frac{1}{4} + \frac{2}{6} + \frac{1}{8} = \frac{17}{24} \approx 71\% \leq 1 \quad \checkmark$$

Hinreichendes RMS-Kriterium:

$$\frac{17}{24} \approx 71\% \leq 3\left(2^{\frac{1}{3}} - 1\right) \approx 78\% \quad \checkmark$$

**Hyperperiode** = $\text{kgV}(4, 6, 8) = 24$ — danach wiederholt sich der Plan.

---

## 3.5 Fallbeispiele

### Linux-Scheduling

**Grundlage:** Multilevel-Feedback-Scheduling; lauffähige Prozesse in einer Liste (`runqueue`).

**Scheduling-Policies:**

| Policy | Verfahren | Zielgruppe | Priorität |
|--------|----------|-----------|----------|
| `SCHED_OTHER` | PRIO-P | normale Prozesse | statisch = 20; dynamisch (nice): $[-20, 19]$ |
| `SCHED_FIFO` | FCFS | Echtzeitprozesse | statisch: 1–99 |
| `SCHED_RR` | Round Robin | Echtzeitprozesse | statisch: 1–99 |

- `SCHED_OTHER`: Verdrängung durch höhere statische Priorität; Rest-Zeitscheibe bleibt als „Guthaben"
- `SCHED_FIFO`: bei gleicher Priorität → erster Prozess; Verdrängung durch höhere Priorität
- `SCHED_RR`: bei gleicher Priorität → RR; nach Ablauf der Zeitscheibe → Ende der `runqueue`

**Linux Scheduler-Ablauf:**
1. Entferne Prozesse ohne `TASK_RUNNING` aus runqueue
2. Bewerte alle lauffähigen Prozesse mit `goodness()`
3. Wähle Prozess mit höchster Bewertung
4. Wenn alle Quanten abgelaufen → neu berechnen

**Quanten:** üblicherweise 20 Uhrticks à 10 ms = 200 ms

**CPU wird entzogen wenn:**
- Quantum vollständig verbraucht ($\text{Quantum} = 0$)
- Thread blockiert wegen E/A
- Thread höherer Priorität ist ablaufbereit

**Funktion `goodness()`:**

| Rückgabewert | Bedeutung |
|-------------|----------|
| $-1$ | freiwillige Abgabe der CPU |
| $0$ | Quantum aufgebraucht |
| $[1, 1000]$ | normaler Prozess |
| $> 1000$ | Echtzeitprozess |

Berechnung bei normalen Prozessen:

$$\text{Güte} = \text{quantum} + \text{priorität} \quad (+1 \text{ wenn gleicher Prozess oder Adressraum})$$

$$\text{Neuberechnung: } \text{Quantum}_{neu} = \frac{\text{Quantum}_{alt}}{2} + \text{Basispriorität}$$

**Multilevel-Scheduling UNIX (Zusammenfassung):**

```
Statische Priorität (hoch → niedrig):
99–98  → SCHED_RR oder SCHED_FIFO  → RR / FIFO
...
22–21  →                            → PRIO
20     → SCHED_OTHER                → PRIO
...
```

### Windows-Scheduling

**Grundlage:** Kombination aus Prozess- und Threadpriorität → 32 Prioritätsstufen $[0, 31]$

- Systemprioritäten $16..31$ → Zuweisung durch Administrator
- Benutzerprioritäten $0..15$ → Änderung via `SetThreadPriority`

**Win32-Prioritätsmatrix (Prozessklasse × Thread-Priorität):**

| Thread-Priorität | Echtzeit | Hoch | Über normal | Normal | Unter normal | Idle |
|-----------------|---------|------|------------|--------|-------------|------|
| Zeitkritisch | 31 | 15 | 15 | 15 | 15 | 15 |
| Höchste | 26 | 15 | 12 | 10 | 8 | 6 |
| Über normal | 25 | 14 | 11 | 9 | 7 | 5 |
| Normal | 24 | 13 | 10 | 8 | 6 | 4 |
| Unter normal | 23 | 12 | 9 | 7 | 5 | 3 |
| Niedrigste | 22 | 11 | 8 | 6 | 4 | 2 |
| Idle | 16 | 1 | 1 | 1 | 1 | 1 |

**Arbeitsweise:**
- 32 Prioritätslisten; Durchlauf von Priorität 31 → 0; bei nicht-leerem Eintrag → Round-Robin
- **Null Thread**: überschreibt Speicherseiten mit Nullen (Hintergrund)
- **Idle Thread**: läuft wenn keine anderen Threads aktiv

**Zeitscheibenlängen:**
- Standard: 20 ms; Einzelprozessor-Server: 120 ms
- Einstellbar um Faktor 2, 4 oder 6
- Kürzere Zeitscheiben → bessere Interaktivität; längere → weniger Kontextwechsel

**Prioritätsverringerung:** Verbraucht ein Thread seine gesamte Zeitscheibe → Priorität um 1 verringert (solange aktuell > Basispriorität) → vgl. Multilevel Feedback Queue

---

## 📌 Strategienvergleich

| Strategie | Verdrängung | Vorteil | Nachteil |
|-----------|------------|---------|---------|
| **FCFS** | nein | einfach, fair | schlechte Antwortzeit bei kurzen Prozessen |
| **LCFS** | nein | — | unfair, selten eingesetzt |
| **LCFS-PR** | ja | kurze Prozesse bevorzugt | langer Prozess kann mehrfach verdrängt werden |
| **RR** | ja | faire Verteilung | Overhead bei kleinem $t$ |
| **PRIO-NP** | nein | Prioritäten berücksichtigt | hohe Prio blockiert niedrige |
| **PRIO-P** | ja | dringende Prozesse schnell | Prioritätsinvertierung möglich |
| **SJN** | nein | minimale mittlere Antwortzeit | lange Prozesse benachteiligt |
| **SRTN** | ja | optimal bei bekannter Restzeit | starvation möglich |
| **HRRN** | nein | verhindert starvation | dynamische Berechnung nötig |
| **Multilevel-Feedback** | ja | adaptiv; bevorzugt interaktive Prozesse | komplexe Konfiguration |

---

## ✅ Kernaussagen

- Scheduling beeinflusst **subjektive Rechnerleistung** — Reihenfolge ist entscheidend
- „Scheduling" = meistens **CPU Scheduling (STS)**
- Verdrängung (Preemption) ermöglicht bessere Zielerreichung, erhöht aber Komplexität
- **Multilevel-Feedback** ist die Grundlage moderner Scheduler (Linux, Windows)
- **EDD** (ohne Verdrängung) und **EDF** (mit Verdrängung) sind optimal bzgl. $L_{max}$
- **RMS**: hinreichende Bedingung $\sum b_i/p_i \leq n(2^{1/n}-1)$; bei großem $n$ max. $\ln 2 \approx 69{,}3\%$ Auslastung
- Prioritätsinvertierung → gelöst durch **Prioritätsvererbung**

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Betriebssyteme und Prozesse]]: Prozesszustände, Bereit → Laufend (Grundlage für Scheduling)
- [[VL.04 Koordination nebenläufiger Prozesse]]: Synchronisation (Semaphore) — Prioritätsinvertierung in der Praxis
- [[AlgoDat]]: $\mathcal{O}(n \log n)$ Sortieralgorithmen für EDD
- [[FoG §7]]: Partielle Ordnungen, Abhängigkeiten zwischen Prozessen
