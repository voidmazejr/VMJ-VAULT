**Class:** [[AlgoDat - Algorithmen und Datenstrukturen]]  
**Date:** 20-04-2026  
**Topics:** #Java #OO #Klassen #Objekte #UML #Vererbung #Polymorphismus
**Link:** [[VL.02 AlgoDat.pdf]]

---

## 🎯 Lernziele der Vorlesung

Algorithmen und Datenstrukturen lösen Probleme durch **Erkennen und Nutzen von Struktur**. Java und Objektorientierung (OO) sind das zentrale Werkzeug.

- **Programmparadigmen**: Imperativ, OO, funktional, ...
- **Klassen und Objekte**: Grundlage der OO-Modellierung
- **Access Modifiers**: `public`, `private`, `protected`, package-private
- **Vererbung und Polymorphismus**: Beziehungen zwischen Klassen
- **UML**: Visualisierung von OO-Strukturen
- **Java Setup**: IntelliJ IDEA, main-Methode, Javadoc, Debugging
- **Beispiele**: Sieb des Eratosthenes, Suchmaschinen, Spreadsheets

---

## 1. Programmparadigmen

### Übersicht

Java ist **objektorientiert** (OO), gehört zur Familie der **imperativen** Programmiersprachen:

| Paradigma | Beschreibung | Beispiele |
|-----------|-------------|----------|
| **Imperativ** | Explizite Steuerung des Ablaufs | C, Java, Pascal |
| **Prozedural** | Funktionen/Verfahren | C |
| **Objektorientiert** | Klassen, Objekte, Vererbung | Java, C++ |
| **Deklarativ** | Was soll erreicht werden? | SQL, HTML |
| **Funktional** | Funktionen als Bürger 1. Klasse | Haskell, Scala |
| **Logisch** | Regeln und Inferenz | Prolog |
| **Constraint** | Einschränkungen definieren | MiniZinc |

⚠️ **Phlogiston-Fehler vermeiden:** OO ist kein Allheilmittel, sondern ein Werkzeug für bestimmte Probleme.

### Warum OO?

OO ermöglicht **Modellierung realer Strukturen**:
- **Suchmaschinen**: Datenstrukturen (Graphen, Indizes) + Algorithmen (Ranking, Crawling)
- **Spreadsheets**: Zellen, Formeln, Referenzen

---

## 2. Klassen und Objekte

### Definitionen

- **Klasse**: Bauplan für Objekte (Struktur + Verhalten)
- **Objekt**: Instanz einer Klasse mit konkreten Werten

**Access Modifiers** (für Klassen, Attribute, Methoden, Konstruktoren):

| Modifier | Sichtbarkeit |
|----------|-------------|
| `public` | Weltweit sichtbar |
| `protected` | Innerhalb Package + Vererbung |
| `private` | Nur innerhalb der Klasse |
| *(kein Modifier)* | Package-private (Standard) |

### Struktur einer Klasse

```java
public class Beispiel {
    // Attribute (Felder)
    private int attribut;
    
    // Konstruktor
    public Beispiel(int wert) {
        this.attribut = wert;
    }
    
    // Methoden
    public int getAttribut() {
        return attribut;
    }
}
```

### Java main-Methode

**Einstiegspunkt** jedes Java-Programms:

```java
public static void main(String[] args) {
    // Programmcode hier
}
```

### Beispiel: Sieb des Eratosthenes

**Aufgabe:** Alle Primzahlen bis $n$ finden.  
**Zeitkomplexität:** $O(n \log \log n)$

**Pseudocode:**
```
1. Erstelle Array isPrime[0..n] = true
2. isPrime = isPrime = false
3. for p = 2 to √n:
     if isPrime[p]:
         mark multiples of p as false
4. Gib alle i mit isPrime[i] = true aus
```

**Java-Implementierung (selbst programmieren!)**

⚠️ **Notizen machen:** Nicht alles steht auf Folien – Lernpyramide beachten!

---

## 3. Beziehungen zwischen Klassen

### Vererbung

**"Ist-ein"-Beziehung** (is-a):

```
Tier
├── Säugetier
│   └── Hund
└── Vogel
    └── Pinguin
```

```java
public class Hund extends Säugetier {
    // Erbt alle Attribute/Methoden von Säugetier
}
```

### Polymorphismus

**"Kann-als"-Beziehung** (behaves-like):  
Methodenaufruf hängt von **tatsächlichem Objekttyp** ab, nicht Referenztyp.

```java
Säugetier tier = new Hund();
tier.machenGeräusch();  // Ruft Hund.machenGeräusch()
```

### Assoziationen

**"Hat-ein"-Beziehung** (has-a):

```
Auto
└── Motor
```

---

## 4. UML (Unified Modeling Language)

### Klassen-Diagramm

```
+----------------+     +----------------+
|   Fahrzeug     |     |     Motor      |
+----------------+     +----------------+
| - geschwindigkeit |◄──| - leistung    |
| + beschleunigen()  |  | + starten()   |
+----------------+     +----------------+
```

### Use Case Diagramm

```
[Benutzer] ──► (Anmelden) ──► [System]
         ──► (Daten eingeben)
         ──► (Ergebnis anzeigen)
```

---

## 5. Setup und Best Practices

### Java-Entwicklung

1. **IntelliJ IDEA** installieren: https://www.jetbrains.com/idea/
2. **Java Crash-Kurs** anschauen
3. **Debugger** nutzen:
   - Breakpoint setzen
   - Variablen inspizieren/ändern
   - Bedingte Breakpoints

### Coding Conventions

**Google nach "Java coding conventions"** – IDE hat eingebaute Präferenzen.

### Javadoc Standards

**Block-Kommentare** mit @-Tags:

```java
/**
 * Berechnet die Summe zweier Zahlen.
 * @param a Erste Zahl
 * @param b Zweite Zahl
 * @return Summe von a und b
 * @throws IllegalArgumentException falls a oder b negativ
 */
public int summe(int a, int b) { ... }
```

---

## 📌 Zusammenfassung

### OO-Grundlagen

| Konzept | Bedeutung |
|---------|----------|
| **Klasse** | Blaupause für Objekte |
| **Objekt** | Instanz einer Klasse |
| **Access Modifiers** | `public`, `private`, `protected`, package-private |
| **Vererbung** | "Ist-ein"-Beziehung (`extends`) |
| **Polymorphismus** | Verhalten hängt vom Objekttyp ab |
| **UML** | Visualisierung von Klassenbeziehungen |

### Wichtige Java-Elemente

| Element | Verwendung |
|---------|-----------|
| `main(String[] args)` | Programm-Einstiegspunkt |
| `this` | Referenz auf aktuelles Objekt |
| `@param`, `@return`, `@throws` | Javadoc-Tags |
| Breakpoint | Debugging in IDE |

### Zeitkomplexitäten (Beispiele)

| Algorithmus | Komplexität |
|-------------|-------------|
| **Sieb des Eratosthenes** | $O(n \log \log n)$ |

### Kernaussagen

✅ **OO löst Probleme durch Strukturerkennung** – Klassen modellieren reale Hierarchien

✅ **Access Modifiers schützen** und kapseln Implementierungen

✅ **Polymorphismus** ermöglicht flexible Code-Wiederverwendung

⚠️ **Nicht alles auf Folien** – Notizen machen, Lernpyramide beachten!

✅ **IntelliJ + Debugger** = essenziell für effektive Entwicklung

✅ **Javadoc** dokumentiert für Team und Zukunft

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.03 Komplexität]]: Zeitkomplexitäten, Sieb des Eratosthenes
