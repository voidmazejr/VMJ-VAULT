**Class:** [[SysProg - Systemprogrammierung]]  
**Date:** 15-05-2026  
**Topics:** #Nebenläufigkeit #Synchronisation #Semaphore #Monitore #KritischeAbschnitte #Betriebssysteme

***

## 🎯 Lernziele der Vorlesung

Diese Vorlesung behandelt die Koordination nebenläufiger Prozesse – ein zentrales Problem der Systemprogrammierung, bei dem Prozesse um gemeinsame Ressourcen konkurrieren oder kooperieren müssen.

- **Prozessinteraktion**: Unterschied zwischen impliziter und expliziter Interaktion, Konkurrenz vs. Kooperation
- **Signalisierung**: Aktives und blockierendes Warten mit `signal(s)` / `wait(s)`
- **Kritische Abschnitte**: Definition, Anforderungen, Mutex-Konzept
- **Semaphore**: P/V-Operationen, Zählsemaphore, Anwendungsmuster (Mutex, Erzeuger-Verbraucher, Reader-Writer)
- **Monitore**: Automatischer Mutex durch Sprachkonstrukte, Bedingungssynchronisation, Java-Monitor

***

## 1. Elementare Koordinationsoperationen

### Warum Koordination notwendig ist

Prozesse, die isoliert und unabhängig ablaufen, brauchen keine Koordination. In der Praxis ist dies selten, weil:

- Betriebsmittel (z. B. Drucker) nur **exklusiv** belegt werden können
- Mehrere Prozesse gemeinsam an einer Aufgabe arbeiten
- Prozesse Daten aus unterschiedlichen Quellen austauschen

> 💡 **Rolle:** Systemsoftware muss Prozess- und Threadinteraktion unterstützen – das ist eine ihrer Kernaufgaben.

### Klassifikation der Prozessinteraktion

$$\boxed{\text{Prozessinteraktion} = \begin{cases} \text{Implizit} & \to \text{Blockierende Aufrufe} \\ \text{Explizit} & \to \begin{cases} \text{Konkurrenz} & \to \text{Synchronisation} \\ \text{Kooperation} & \to \text{Kommunikation} \end{cases} \end{cases}}$$
![[VL.04 Koordination nebenläufiger Prozesse-1778781424370.webp]]

| Dimension       | Implizit                         | Explizit                              |
|-----------------|----------------------------------|---------------------------------------|
| **Sichtbarkeit**| Prozess merkt nichts             | Prozess verwaltet Interaktion selbst  |
| **Muster**      | –                                | Konkurrenz / Kooperation              |
| **Mittel**      | Blockierende Systemaufrufe       | Synchronisation / Kommunikation       |
| **Beispiel**    | Unix Pipe (`ls \| grep`)         | Semaphor, Monitor, Message Queue      |

### Beispiel: Implizite Interaktion – Unix Pipe

```
user@machine:~$ ls -l | grep foo
```

```
┌──────────────────────┐       Pipe        ┌──────────────────────────┐
│  ls-Prozess          │ ────────────────▶ │  grep-Prozess            │
│  write(stdout, Zeile)│                   │  read(stdin, Zeile)      │
│  (Erzeuger)          │                   │  (Verbraucher)           │
└──────────────────────┘                   └──────────────────────────┘
                         ↑ Implizite Interaktion:
                           read() blockiert, wenn ls zu langsam ist
```

> 💡 **Merkhilfe:** Bei der Pipe passiert die Synchronisation „hinter den Kulissen" – der `grep`-Prozess weiß nicht, dass er auf `ls` wartet. Er ruft einfach `read()` auf und das Betriebssystem blockiert ihn automatisch.

### Konkurrenz vs. Kooperation

$$\boxed{\text{Prozesssynchronisation} = \text{zeitliche Abstimmung konkurrierender Prozesse}}$$

**Konkurrenz:**
- Zwei oder mehr Prozesse bewerben sich um ein **exklusiv nutzbares** Betriebsmittel
- Durch Koordination muss eine **Serialisierung** der Zugriffsversuche erreicht werden
- Bei $n$ konkurrierenden Prozessen werden $n-1$ Prozesse **zeitlich verzögert**

***

## 2. Signalisierung

### Grundkonzept

$$\boxed{\text{Signalisierung: } P_2 \text{ wird fortgesetzt, nachdem } P_1 \text{ Abschnitt A beendet hat}}$$

**Operationen:** `signal(s)` und `wait(s)` mit Sperrvariable $s$

![[VL.04 Koordination nebenläufiger Prozesse-1778781570625.webp|801]]

> 💡 **Merkhilfe:** Staffelstabübergabe – P1 läuft zuerst, gibt den Stab (Signal) an P2 weiter.

### Version 1: Aktives Warten (Busy Waiting)

```c
// Signalisierung mit Busy-Waiting
struct Signal { // Version 1
    boolean s;
} so = { false }; // Initialisierung

void signal(struct Signal *so) {
    so->s = true;
}

void wait(struct Signal *so) {
    while (so->s == false) { ; } // Warten, bis gesetzt
    so->s = false;
}
```

```
signal(s):          wait(s):
   │                   │
  set s             s set?  ←──┐
   │                   │  no   │
   ▼               reset s ────┘
                       │
                       ▼
```

⚠️ **Achtung:** Busy Waiting **verschwendet CPU-Kapazität** – der wartende Prozess läuft in einer Schleife und verbraucht 100% einer CPU-Kern-Zeit, ohne nützliche Arbeit zu leisten.

### Version 2: Blockierendes Warten

**Lösung:** Wenn gewartet werden muss, CPU freigeben und Prozess in Zustand `BLOCKED` versetzen.

```c
// Signalisierung mit blockierendem Warten
struct Signal { // Version 2
    boolean s;
    process *wp;
} so = { false, NULL }; // Initialisierung

void signal(struct Signal *so) {
    so->s = true;
    if (so->wp != NULL) {      // Wartet ein Prozess?
        deblock(so->wp);       // Blockierung aufheben
        so->wp = NULL;         // Struktur zurücksetzen
    }
}

void wait(struct Signal *so) {
    if (so->s == false) {      // noch kein Signal?
        so->wp = MYSELF;
        block();
    }
    so->s = false;
}
```

```
signal(s):                  wait(s):
   │                           │
  set s                     s set? ──yes──▶ (direkt weiter)
   │                           │ no
process waiting?             block()
   │ no ──▶ (fertig)            │
   │                         (wird durch signal deblockiert)
deblock(process)               │
   │                        reset(s)
   ▼                           ▼
```

✅ **Vorteil:** Wartender Prozess gibt CPU frei → andere Prozesse können arbeiten.

### Wechselseitige Synchronisierung (Rendezvous)

Symmetrischer Einsatz: Beide Prozesse synchronisieren sich gegenseitig – weder P1 noch P2 kann mit B beginnen, bevor beide A abgeschlossen haben.

```
P1:  A → signal(s1) + wait(s2) → B1
P2:  A → signal(s2) + wait(s1) → B2
```

$$\boxed{\text{sync}(s) = \text{signal}(s_\text{selbst}) + \text{wait}(s_\text{anderer}) \quad \text{(Rendezvous)}}$$

```
P1              P2
 │ A1            │ A2
 │               │
sync(s) ◄───────▶ sync(s)
 │               │
 │ B1            │ B2
 ▼               ▼
```

> 💡 **Merkhilfe:** Rendezvous = beide warten aufeinander, bevor sie weitermachen – wie zwei Züge, die am selben Bahnhof aufeinander warten.

***

## 3. Kritische Abschnitte

### Definition

$$\boxed{\text{Kritischer Abschnitt} = \text{Operationsfolge, bei der nebenläufige Ausführung zu Fehlern führt}}$$

**Beispiele:**
- Zugriff auf exklusiv nutzbare Betriebsmittel (Drucker, Datei)
- Modifikation gemeinsamer Datenstrukturen (z. B. verkettete Liste)

**Strukturprinzip:**
```
...
Sperren(Sperrvariable)    ┐
  [kritischer Bereich]    │  Kritischer Abschnitt
Freigeben(Sperrvariable)  ┘
...
```

### Anforderungen an kritische Abschnitte

| Anforderung | Beschreibung |
|---|---|
| **Mutual Exclusion** | Nur 1 Prozess gleichzeitig im kritischen Bereich |
| **Keine Annahmen** | Unabhängig von Prozessorgeschwindigkeit & Anzahl der Prozesse |
| **Keine unnötige Verzögerung** | Prozesse in unkritischen Bereichen dürfen nicht verzögert werden |
| **Keine Verklemmung** | Prozesse dürfen sich nicht gegenseitig blockieren (Deadlock-Freiheit) |
| **Fortschritt** | Ein Prozess muss nach endlicher Zeit eintreten können |
| **Endliche Aufenthaltsdauer** | Prozess verlässt kritischen Bereich nach endlicher Zeit |

### Das Race-Condition-Problem

⚠️ **Kernproblem:** Bei verzahnter Ausführung kann zwischen **Prüfen** und **Ändern** der Sperrvariable ein Kontextwechsel stattfinden.

**Szenario cnt++:** (Assembly: lw → addiu → sw)

```
Thread A                        Thread B
lw v0, 40(gp)   // liest 10
                ← Umschaltung
                                lw v0, 40(gp)   // liest 10
                                addiu v0,v0,1   // v0 = 11
                                sw v0, 40(gp)   // schreibt 11
                ← Umschaltung
addiu v0,v0,1   // v0 = 11 (veralteter Wert!)
sw v0, 40(gp)   // schreibt 11 → B's Inkrement verloren!
```

❌ **Fehler:** Iterationen von Thread B gehen verloren, weil Thread A einen veralteten Wert zurückschreibt.

**Gleiches Problem bei Sperrflags:**

```
Thread A                    Thread B
lw v0, 0(a0)  // FREI
← Umschaltung →
                            lw v0, 0(a0)  // auch FREI!
                            sw zero,0(a0) // Bereich betreten
← Umschaltung →
sw zero, 0(a0) // Bereich betreten ← KATASTROPHE: beide drin!
```

❌ **Fazit:** Einfache Sperrflags ohne atomare Operationen sind **nicht thread-sicher**.

### Thread-Safety: Lösungsstrategien

$$\boxed{\text{Thread-Safe} = \text{alle Threads verhalten sich gemäß Designspezifikation ohne unbeabsichtigte Interaktion}}$$

| Ansatz | Technik | Beschreibung |
|---|---|---|
| **Ansatz 1: Zustand vermeiden** | Wiedereintritt | Statusinformationen in **lokalen** Variablen speichern |
| | Thread-lokaler Speicher | Jeder Thread hat eigene **private Kopie** aller Variablen |
| | Unveränderliche Objekte | Nur **schreibgeschützte** Daten werden geteilt |
| **Ansatz 2: Synchronisation** | Gegenseitiger Ausschluss | Serialisierung der Zugriffe |
| | Atomare Operationen | Spezielle CPU-Befehle: **Compare-and-Swap**, **Load-Linked/Store-Conditional** |

***

## 4. Betriebssystemgestützte Prozessinteraktion

### Motivation

Aktives Warten verschwendet Ressourcen → Betriebssystem übernimmt Kontrolle:

- **Blockierung** wartender Prozesse bis kritischer Bereich frei
- **Scheduling** des nächsten Prozesses aus der Warteschlange (FCFS, Prioritäten, ...)
- **Voraussetzung:** Atomare Instruktionssequenz für Prüfen/Setzen (heute überall verfügbar)

**Betriebssystemkonstrukte:**
- **Semaphore** (Dijkstra, 1965)
- **Monitore**

***

## 5. Semaphore

### Definition

$$\boxed{\text{Semaphor} = (\underbrace{s \in \mathbb{Z}_{\geq 0}}_{\text{Zähler}},\ \underbrace{Q}_{\text{Warteschlange}})}$$

Ein Semaphor besteht aus:
- Einem **nicht-negativ initialisierten Zähler** $s$
- Einer **Warteschlange** mit Verweisen auf blockierte Prozesse

> 💡 **Merkhilfe:** Stell dir eine Ampel vor: Das Signal zeigt an, wer fahren darf (Zähler), die Fahrzeuge dahinter warten in der Schlange (Queue).

### P-Operation (Passieren / „Proberen")

$$\boxed{P(s): \quad s \leftarrow s - 1; \quad \text{falls } s < 0 \Rightarrow \text{blockiere aktuellen Prozess}}$$

```pseudocode
P(Semaphor s):
1. s.zaehler--
2. if s.zaehler < 0 then
3.     currentProcess.state = BLOCKED
4.     enqueue(s.queue, currentProcess)
5.     scheduler()   // anderen Prozess auswählen
```

### V-Operation (Verlassen / „Verhogen")

$$\boxed{V(s): \quad \text{falls } s < 0 \Rightarrow \text{deblockiere Prozess}; \quad s \leftarrow s + 1}$$

```pseudocode
V(Semaphor s):
1. if s.zaehler < 0 then
2.     p = dequeue(s.queue)   // FCFS oder Priorität
3.     p.state = READY
4.     // ggf. scheduler() für Verdrängung
5. s.zaehler++
```

### Bedeutung des Zählerwertes

$$\text{Zählerwert} = \begin{cases} s > 0 & \text{Anzahl Prozesse, die noch passieren dürfen} \\ s = 0 & \text{Semaphor genau erschöpft} \\ s < 0 & |s| = \text{Anzahl wartender Prozesse in der Queue} \end{cases}$$

### Vollständige Implementierung

```c
void P(Semaphor s) {
    s.zaehler--;                         // Zähler dekrementieren
    if (s.zaehler < 0) {                 // kleiner 0: Semaphor sperrt
        currentProcess.state = BLOCKED;
        enqueue(s.queue, currentProcess);
        scheduler();                     // anderen Prozess auswählen
    }
}

void V(Semaphor s) {
    if (s.zaehler < 0) {                 // es gibt wartende Prozesse
        Process p = dequeue(s.queue);   // einen auswählen (FCFS?)
        p.state = READY;                // aufwecken
        /* ggf. auch hier: scheduler() (Verdrängung prüfen!) */
    }
    s.zaehler++;                        // Zähler inkrementieren
}
```

### Initialisierungswert und Semantik

| Initialisierung | Bedeutung |
|---|---|
| $s = 1$ | **Binärer Semaphor / Mutex** – gegenseitiger Ausschluss, max. 1 Prozess im krit. Bereich |
| $s = k > 1$ | **Zählsemaphor** – bis zu $k$ Prozesse gleichzeitig (z. B. max. $k$ Download-Verbindungen) |
| $s = 0$ | **Signalisierung** – Verbraucher wartet, bis Erzeuger signalisiert |

⚠️ **Achtung:** FIFO-Reihenfolge der Warteschlange gilt für Standard-Betriebssysteme. Im **Echtzeitbetrieb** müssen Prioritäten berücksichtigt werden (FIFO-Abweichung notwendig).

***

## 6. Anwendungsmuster der Semaphore

### Muster 1: Einfacher kritischer Abschnitt (Mutex)

```
Semaphor mutex = 1

Prozess P1:              Prozess P2:
P(mutex)                 P(mutex)
  [krit. Abschnitt]        [krit. Abschnitt]
V(mutex)                 V(mutex)
```

**Schritt-für-Schritt Beispiel:**

```
Ausgangszustand: mutex.zaehler = 1

Schritt 1: P1 ruft P(mutex) auf
          mutex.zaehler = 1-1 = 0  → P1 darf eintreten ✅

Schritt 2: P2 ruft P(mutex) auf
          mutex.zaehler = 0-1 = -1 → P2 wird BLOCKIERT ⚠️

Schritt 3: P1 ruft V(mutex) auf
          zaehler < 0 → P2 wird deblockiert (READY)
          mutex.zaehler = -1+1 = 0

Schritt 4: P2 tritt in krit. Bereich ein ✅
```

### Muster 2: Erzeuger-Verbraucher-System

**Problem:** Gemeinsamer Puffer mit beschränkter Kapazität. Erzeuger darf nicht schreiben wenn voll, Verbraucher nicht lesen wenn leer.

$$\boxed{\text{Semaphor } leer = 1,\quad voll = 0 \quad \text{(für Puffer der Größe 1)}}$$

```
Semaphor leer = 1, voll = 0

Erzeuger:              Verbraucher:
P(leer)                P(voll)
  [schreibe Daten]       [lese Daten]
V(voll)                V(leer)
```

**Schritt-für-Schritt:**

```
Ausgangszustand: leer=1, voll=0, Puffer leer

Schritt 1: Erzeuger: P(leer) → leer=0, tritt ein, schreibt Daten
Schritt 2: Erzeuger: V(voll) → voll=1
          (Verbraucher war bei P(voll) blockiert → wird geweckt)
Schritt 3: Verbraucher: P(voll) → voll=0, liest Daten
Schritt 4: Verbraucher: V(leer) → leer=1 (Erzeuger kann wieder schreiben)

✅ Kein Überlauf, kein Unterlauf möglich
```

> 💡 **Merkhilfe:** Die Semaphore `leer` und `voll` sind wie kommunizierende Gefäße – wenn eines steigt, sinkt das andere. Das „Über-Kreuz"-Muster (Erzeuger P(leer)/V(voll), Verbraucher P(voll)/V(leer)) erzwingt die Abwechslung.

### Muster 3: Reader-Writer-Problem

**Definition:**
- **Writer:** Schreiben gemeinsam genutzte Daten → exklusiver Zugriff erforderlich
- **Reader:** Lesen die Daten → paralleler Zugriff unkritisch

$$\boxed{\text{Im krit. Bereich: entweder } 1 \text{ Writer } \textbf{oder} \text{ beliebig viele Reader}}$$

#### Lösung mit Leservorrang (Reader Priority)

```c
int Readernr = 0;
Semaphor w = 1, mutex = 1;

// Writer-Prozess:
P(w);
  Modifiziere Daten;
V(w);

// Reader-Prozess:
P(mutex);              // Readernr schützen
  Readernr++;
  if (Readernr == 1) P(w);  // Erster Reader sperrt Writer aus
V(mutex);
  Lese Daten;          // Mehrere Reader gleichzeitig möglich!
P(mutex);
  Readernr--;
  if (Readernr == 0) V(w);  // Letzter Reader gibt Writer frei
V(mutex);
```

**Schleifeninvariante / Korrektheit:**
- `mutex` schützt die Variable `Readernr` vor Race Conditions
- `w` schützt den Datenzugriff gegen Writers
- Erster Reader sperrt Writer aus; letzter Reader gibt frei → Writer kann erst dann ran

⚠️ **Problem Leservorrang:** Bei konstantem Leserstrom kann ein Writer **verhungern** (Starvation), weil immer mindestens ein Reader im kritischen Bereich ist.

#### Lösung mit Schreibervorrang (Writer Priority)

```c
int Readernr, Writernr = 0;
Semaphor mutex1, mutex2, mutex3, w, r = 1;

// Writer-Prozess:
P(mutex2);
  Writernr++;
  if (Writernr == 1) P(r);  // Erster Writer sperrt Leser-Eingang
V(mutex2);
P(w);                        // Exklusiver Schreibzugriff
  Modifiziere Daten;
V(w);
P(mutex2);
  Writernr--;
  if (Writernr == 0) V(r);  // Letzter Writer gibt Leser-Eingang frei
V(mutex2);

// Reader-Prozess:
P(mutex3);           // Seriell eintreten (damit Writers blockieren können)
  P(r);              // Prüft ob Writer vorrangig
    P(mutex1);
      Readernr++;
      if (Readernr == 1) P(w);
    V(mutex1);
  V(r);
V(mutex3);
  Lese Daten;
P(mutex1);
  Readernr--;
  if (Readernr == 0) V(w);
V(mutex1);
```

| Strategie | Vorrang | Nachteil |
|---|---|---|
| **Leservorrang** | Reader können jederzeit eintreten | Writer können verhungern |
| **Schreibervorrang** | Writer werden bevorzugt | Reader können verhungern |

***

## 7. Monitore

### Motivation

$$\boxed{\text{Monitor} = \text{Objekt mit Methoden + Daten, automatisch unter gegenseitigem Ausschluss}}$$

**Problem mit Semaphoren:** Programmierer müssen P/V-Operationen **manuell** und **korrekt** platzieren. Fehler (vergessenes V, falsche Reihenfolge) führen zu Deadlocks oder Race Conditions.

**Lösung:** Monitor kapselt Sperrmechanismus – der Programmierer deklariert nur, **was** kritisch ist, nicht **wie** gesperrt wird.

```
┌─────────────────────────────────────┐
│           MONITOR                   │
│                                     │
│  Warteschlange → [Lock] → Methode 1 │
│                           Methode 2 │
│                           Methode 3 │  ──▶ Daten
│                           Methode n │
└─────────────────────────────────────┘
```

### Monitor-Äquivalenz

```java
// Monitor-Syntax (abstrakt):
monitor shared_counter {
    int c = 0;
    public void increment() { c = c + 1; }
    public void decrement() { c = c - 1; }
}
```

**Äquivalent zu (expliziter Mutex):**

```java
class shared_counter {
    private mutex m;
    int c = 0;
    public void increment() {
        mutex_lock(m);
        c = c + 1;
        mutex_unlock(m);
    }
    public void decrement() {
        mutex_lock(m);
        c = c - 1;
        mutex_unlock(m);
    }
}
```

✅ Der Monitor übernimmt das Setzen und Freigeben der Sperren **automatisch und implizit**.

### Bedingungssynchronisation

**Problem:** Was, wenn ein Prozess innerhalb des Monitors auf eine Bedingung warten muss (z. B. Puffer ist voll)? Er darf den Monitor nicht blockiert halten, sonst Deadlock!

$$\boxed{\text{cwait}(c): \text{Monitor freigeben, blockieren, auf csignal}(c) \text{ warten, dann Monitor wieder belegen}}$$

$$\boxed{\text{csignal}(c): \text{einen wartenden Prozess aufwecken (kein Effekt wenn keiner wartet)}}$$

```
┌──────────────────────────────────────────────────────────┐
│  Monitor                                                 │
│                                                          │
│  Prozess P ruft cwait(c):                                │
│    1. Monitor-Lock wird freigegeben                      │
│    2. P wird in Bedingungswarteschlange eingereiht       │
│    3. Anderer Prozess Q betritt Monitor                  │
│    4. Q ruft csignal(c) → P wird aufgeweckt              │
│    5. P belegt Monitor wieder und fährt fort             │
└──────────────────────────────────────────────────────────┘
```

### Monitore in Java

Java implementiert Monitore über das `synchronized`-Schlüsselwort:

| Java-Konstrukt | Monitor-Äquivalent | Bedeutung |
|---|---|---|
| `synchronized void methode()` | Monitor-Methode | Automatischer gegenseitiger Ausschluss |
| `wait()` | `cwait(c)` | Monitor freigeben und blockieren |
| `notify()` | `csignal(c)` | Einen wartenden Thread aufwecken |
| `notifyAll()` | csignal für alle | Alle wartenden Threads aufwecken |

⚠️ **Achtung:** `notifyAll()` gibt temporär **alle** durch `synchronized` belegten Sperren frei. Nach dem Aufwecken konkurrieren alle Threads erneut um den Monitor.

### Monitor-Beispiel: Bounded Buffer (Java)

```java
public class BoundedBuffer {
    Object buffer[n];
    int head, tail, count;

    public BoundedBuffer() { /* initialize */ }

    public synchronized void deposit(Object data) {
        while (count == n) wait();       // Puffer voll → warten
        buffer[tail] = data;
        tail = (tail + 1) % n;
        count++;
        notifyAll();                     // Verbraucher aufwecken
    }

    public synchronized Object fetch() {
        Object result;
        while (count == 0) wait();       // Puffer leer → warten
        result = buffer[head];
        head = (head + 1) % n;
        count--;
        notifyAll();                     // Erzeuger aufwecken
        return result;
    }
}
```

**Schritt-für-Schritt Ablauf:**

```
Ausgangszustand: Puffer leer, count = 0

Schritt 1: fetch() aufgerufen → count==0 → wait() → Monitor freigegeben
Schritt 2: deposit(x) aufgerufen → count < n → schreibt x, count=1
Schritt 3: notifyAll() → fetch()-Thread wird aufgeweckt
Schritt 4: fetch() belegt Monitor wieder → count > 0 → liest x ✅
```

> 💡 **Merkhilfe:** `while`-Schleife statt `if` beim Warten ist kritisch! Nach dem Aufwecken durch `notifyAll()` muss die Bedingung **erneut geprüft** werden, da ein anderer Thread die Ressource inzwischen wieder belegt haben könnte (Spurious Wakeups).

***

## 📌 Zusammenfassung

### Wichtige Konzepte

| Konzept | Bedeutung |
|---|---|
| **Prozessinteraktion** | Implizit (verborgen) oder Explizit (Konkurrenz/Kooperation) |
| **Signalisierung** | `signal(s)` / `wait(s)` – einseitige Abhängigkeit; Rendezvous = gegenseitig |
| **Busy Waiting** | Aktives Warten in Schleife – einfach, aber CPU-verschwendend |
| **Blockierendes Warten** | Prozess wird `BLOCKED`, gibt CPU frei, wird durch Signal geweckt |
| **Kritischer Abschnitt** | Codebereich, der nur von einem Prozess gleichzeitig ausgeführt werden darf |
| **Mutex** | Binärer Semaphor ($s=1$) für gegenseitigen Ausschluss |
| **Semaphor** | Zählsperre mit P/V-Operationen; Zähler > 0: frei, < 0: Anzahl wartender Prozesse |
| **Monitor** | Objekt mit automatischem Mutex; `cwait`/`csignal` für Bedingungen |
| **Race Condition** | Fehler durch nicht-atomares Lesen-Modifizieren-Schreiben bei Nebenläufigkeit |
| **Thread-Safety** | Garantie: korrekt auch bei beliebiger nebenläufiger Ausführung |

### Kernaussagen

✅ **Blockierendes Warten** ist Busy Waiting immer vorzuziehen – CPU wird sinnvoll genutzt  
✅ **Atomare Operationen** (Compare-and-Swap, LL/SC) sind die Hardware-Grundlage aller Synchronisation  
✅ **Semaphor P(s) vor, V(s) nach** dem kritischen Bereich – diese Reihenfolge darf nie vertauscht werden  
✅ **Monitor kapselt** Synchronisation – weniger fehleranfällig als manuelle Semaphore  
⚠️ **Leservorrang** kann Writer verhungern lassen; **Schreibervorrang** kann Reader verhungern lassen  
⚠️ **`while` statt `if`** bei `wait()` in Java-Monitoren – Bedingung nach Aufwecken neu prüfen!  
❌ **Vergessenes V(s)** führt zu Deadlock – alle wartenden Prozesse blockieren dauerhaft  
❌ **Vertauschte P-Operationen** beim Erzeuger-Verbraucher führen zu Deadlock (z.B. P(mutex) vor P(leer))  

### Wichtige Operationen im Vergleich

| Mechanismus | Operation | Effekt bei Sperre frei | Effekt bei Sperre belegt |
|---|---|---|---|
| **Busy Waiting** | `wait(s)` | Passiert sofort | Schleife (CPU-Last) |
| **Block. Warten** | `wait(s)` | Passiert sofort | Prozess → BLOCKED |
| **Semaphor** | `P(s)` | $s \geq 0$: passiert | $s < 0$: BLOCKED, in Queue |
| **Semaphor** | `V(s)` | $s$ inkrementieren | Prozess aus Queue aufwecken |
| **Monitor Java** | `synchronized` | Lock belegen | Thread → Warteschlange |
| **Monitor Java** | `wait()` | Monitor freigeben + blockieren | – |
| **Monitor Java** | `notify()` | Einen Thread aufwecken | – |

***

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.03 Scheduling]]: Prozesszustände (Bereit, Laufend, Blockiert) – Basis für Semaphor-Blockierung
- [[VL.05 Betriebsmittelverwaltung]]: Verklemmungen entstehen bei falschem Semaphor-Einsatz (zyklische Warteabhängigkeiten)
- [[VL.03 Scheduling]]: Warteschlangen-Strategien (FCFS, Prioritäten) bei Semaphoren und Betriebsmittelverwaltung
- [[VL.06 Speicher- und Adressraumverwaltung]]: Shared Memory als Voraussetzung für Semaphor-basierte Synchronisation
