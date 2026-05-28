**Class:** [[InfoProp]]  
**Date:** 24-12-2026
**Topics:** #GeschichteInformatik #Mechanisierung #Rechenmaschinen #FrüheComputer #Babbage #Zuse #Turing

---

## 🎯 Lernziele der Vorlesung

Geschichte der Informatik und Entwicklung des Computers verstehen.

- **Mensch als Inspiration** für Maschinen
- **Automatisierung** von Tätigkeiten (körperlich und geistig)
- **Entwicklung von Computern** - wichtige Personen und Meilensteine
- **Wissenschaftliches Arbeiten** - fragengeleitetes Lesen und Wissensaufbau

---

## 1. Philosophische Grundlagen: Descartes' Gedankenexperiment

### René Descartes (1596-1650)

**Gedankenexperiment:** Wie unterscheidet man zwischen Mensch und Maschine?

**Zwei Mittel zur Unterscheidung:**

1. **Sprachliche Flexibilität:** Maschinen können Worte und Zeichen nicht flexibel zusammensetzen, um auf sprachliche Äußerungen anderer sinnvoll zu antworten
2. **Universalität der Vernunft:**
    - Menschliche Vernunft ist ein **Universalinstrument**, das in allen möglichen Situationen/Tätigkeiten benutzt werden kann
    - Organe von Maschinen benötigen eine ganz bestimmte Anordnung für jede mögliche Tätigkeit

### Warum war Descartes' Vorstellung "naiv"?

✅ Descartes lebte 1596-1650 und kannte nur **mechanische Maschinen**

✅ Er konnte das Wissen um heutige Computer nicht vorwegnehmen - Computer sind das Resultat einer Reihe von Entwicklungsschritten

✅ In Computern sind **Hardware** ('Organe') und **Software** ('Denken') voneinander getrennt - das macht sie zu einem 'Universalinstrument'

❌ Seine Intuition war teilweise richtig, aber er kannte das Konzept der **Trennung von Hard- und Software** nicht

---

## 2. Antike Rechengeräte

### Frühe Hilfsmittel

|Zeit|Gerät|Funktion|
|---|---|---|
|~2500 v.Chr.|**Abakus** (Mesopotamien)|Erste 'Maschine' zum Zählen und Rechnen|
|~500 v.Chr.|**Kerbholz/Knotenschnur** (Herodot)|Schuldurkunde (Gedächtnis)|
|~70 v.Chr.|**Mechanismus von Antikythera**|Komplizierte Modelle zur Berechnung von Sonne und Mond|

---

## 3. 17. Jahrhundert: Mechanische Rechenmaschinen

### Wilhelm Schickard (1592-1635)

**1623:** Rechenmaschine zur Erleichterung astronomischer Rechnungen

- Addition & Subtraktion von bis zu sechsstelligen Zahlen
- Bei "Speicherüberlauf" klingelte Glocke
- Kepler nannte ihn "beidhändiger Philosoph"

### Blaise Pascal (1632-1662)

**1642:** **Pascaline** für seinen Vater, einen hohen Steuerbeamten

- Addition & Subtraktion
- Ca. 50 Exemplare wurden tatsächlich gebaut
- Namensgeber für die Programmiersprache Pascal (entwickelt von Niklaus Wirth, ETH Zürich)

### Gottfried Wilhelm Leibniz (1646-1716)

**1673:** Dezimale Rechenmaschine für 4 Grundrechenarten

> _"...unwürdig, die Zeit von hervorragenden Leuten mit knechtischen Rechenarbeiten zu verschwenden, weil bei Einsatz einer Maschine auch der Einfältigste die Ergebnisse sicher hinschreiben kann."_

**Idee:** Einzelne Lösungsschritte des schriftlichen Rechnens systematisch auf mechanischen Vorgang übertragen

---

## 4. 18. Jahrhundert: Grenzen mechanischer Rechenmaschinen

### Weitere Erfinder

Giovanni Poleni, Anton Braun, Jacob Leupold, ...

### Limitierungen der frühen Rechenmaschinen

❌ Jede Maschine tut nur das, wofür sie bei der Erbauung festgelegt war

❌ Keine Trennung von "Hard-" (Organen) und "Software" (Vernunft)

❌ Konzept des **'Programms'** gab es nicht - um eine Berechnung zu wiederholen, mussten alle Schritte und alle Eingaben wieder per Hand ausgeführt werden

❌ "Rechner" hatten keinen **Speicher (Memory)** - Teilergebnisse mussten aufgeschrieben und wieder eingegeben werden

❌ Einzelne Berechnungsschritte erforderten menschliche Bedienung

❌ Mechanisch, nicht elektronisch

**Vision:** Eine programmierbare und damit universelle Rechenmaschine

---

## 5. 19. Jahrhundert: Programmierbarkeit

### Joseph-Marie Jacquard (1752-1834)

**1801:** Programmierbarer Webstuhl

- Gesteuert durch **Lochstreifen**, mit Nadeln abgetastet
- Loch → Fadenhebung
- Kein Loch → Fadensenkung
- **Binäre Kodierung** von Daten und Steuerungsinfo - austauschbar

**Bedeutung:** Dieselbe Maschine kann verschiedene Dinge tun!

### Herman Hollerith (1860-1929)

**1890:** Lochkarten-Maschine für Datenverarbeitung bei Volkszählung

- **Idee:** Eisenbahnschaffner - Locher zur Kodierung von Merkmalen der Passagiere
- **Effizienz:** 1 Zehntel Helfer, 4 Wochen statt 7 Jahre
- **Legacy:** Übliche maximale Zeilenlänge von knapp 80 Zeichen in E-Mails und Textdateien geht auf das Lochkartenformat zurück

**Vorlaufer der elektronischen Datenverarbeitung**

### Charles Babbage (1791-1871)

**Problem:** Berechnung mathematischer Tabellen von Hand (z.B. Trigonometrische Funktionen, Logarithmen) - Fehler! → Schiffsunglücke

**Beobachtung:** (Teil-)Rechnungen wiederholen sich → Mechanisieren

**1837:** **Analytical Engine** - universelle Maschine

✅ Idee des **Mehrzweck-Rechners** - programmierbar mit Punch Cards

✅ Konzepte wie **bedingte Verzweigungen** und **Schleifen** eingeführt

✅ Zusammenarbeit mit **Ada Lovelace**, 1. Programm für die Analytical Engine

❌ **Scheiterte** aufgrund mangelnder Feinmechanik - Feinmechanik war nicht präzise und robust genug

**= Vorläufer des Computers**

---

## 6. 20. Jahrhundert: Der erste Computer

### Alan Turing (1912-1954)

**1936:** Bahnbrechender Aufsatz über **Berechenbarkeit**

**Turing-Maschine (fiktiv):**

- Besteht aus einem **unendlichen Speicher** und einem **kleinen Prozessor**
- Vollführt nur einfachste Umwandlungen von Nullen und Einsen
- Kann als **Universalrechner** arbeiten
- **Speicher** enthält: Daten des Problems + das **Programm**

**Bedeutung:** 1936 ist nicht der Computer im heutigen Sinne entstanden, wohl aber **dessen Konzept**

### Konrad Zuse (1910-1995)

**Motivation:**

> _"Allerdings war ich von dem Studium ... etwas enttäuscht, weil sehr viel nüchterne Arbeit dazu gehörte, insbesondere Rechenarbeit. ... es behagte mir an sich nicht, dass ein junger Mensch seine Arbeitskraft dafür hergeben sollte."_

**Anforderungen an ideale Rechenmaschine (1936):**

1. Ingenieur arbeitet mit festen Formeln, die immer wiederkehren - immer gleiche Aufeinanderfolge von Grundrechenarten
2. Rechenmaschine soll diese Rechenoperationen **automatisch ausführen** - Rechenplan auf einem **Lochstreifen** festgehalten, der die Befehle selbsttätig nacheinander an die Maschine gibt

### Die Z1 (1938)

- Praktisch vollständig **mechanisches Gerät**
- Vier arithmetische Operationen (Addition, Subtraktion, Multiplikation, Division) in **beliebiger Reihenfolge** mit gespeicherten Zahlen
- ❌ Mechanische Bauteile (bewegliche Bleche) waren nicht zuverlässig genug → Umstieg auf Relaistechnik

### Die Z3 (1941) - Oranienstraße 37, Berlin

**Erster funktionsfähiger, programmgesteuerter Digitalrechner**

**Architektur:**

- **Rechenwerk**, **Steuerwerk**, **Speicher**, **Ein- und Ausgabe** → Von-Neumann-Architektur
- Elektromechanische **Relais** (5.3 Takte pro Sekunde)
    - 600 Relais für das Rechenwerk
    - 1400 Relais für den Speicher
- **Binäre Gleitkommaarithmetik**

**Wichtige Designentscheidungen:**

1. **Binärsystem (Basis 2):**
    - ✅ Bauteile, die 2 Zustände darstellen, waren **robuster**
    - ❌ Für uns Menschen **unintuitiv**
    - Jedes Bauteil, das zwei wohl unterscheidbare Zustände annehmen kann, ist geeignet, eine Binärziffer darzustellen
    - Zuse: In der Maschine sind die Zahlen "unter sich", der Mensch braucht den einzelnen Berechnungsschritten nicht folgen zu können
2. **Trennung von Prozessor und Speicher:**
    - Bei Mark I und ENIAC war diese Trennung noch nicht vollzogen
    - Speicherzellen dienten zugleich als arithmetische Elemente
3. **Gleitkomma-Darstellung (floating point notation)**

---

## 7. Vergleich früher Computer

### Zeitgleiche Entwicklungen (USA)

|Maschine|Jahr|Ort|Besonderheiten|
|---|---|---|---|
|**ABC**|1938-1942|Iowa State College (John Atanasoff)|Binärmaschine|
|**Mark I**|1939-1944|Harvard (Howard Aiken)|Dezimalcodierung|
|**ENIAC**|1943-1945|Pennsylvania (Eckert & Mauchly)|Vollelektronisch, Dezimalcodierung|
|**Z3**|1941|Berlin (Konrad Zuse)|Binärmaschine, Trennung Prozessor/Speicher|

### Wichtige Unterschiede

**Z3 und ABC:**

- ✅ Binärmaschinen
- ✅ Z3: Trennung von Prozessor und Speicher

**Mark I und ENIAC:**

- ❌ Dezimalcodierung (10 Vakuumröhren für eine Dezimalziffer)
- ❌ Keine Trennung von Prozessor und Speicher
- ❌ Gemessen an ihrer Rechenleistung viel zu komplex

**Gemeinsame Limitierung:**

- ❌ Keine der Maschinen bot einen **bedingten Sprungbefehl** - wesentliches Merkmal eines Universalrechners
- ENIAC konnte immerhin Schleifen abbrechen, aber nur eine Kontrolleinheit
- Zuse führte Sprungbefehle erst in späteren Rechnern ein

---

## 8. Historische Einbettung - Zweiter Weltkrieg

Realisierung der ersten Computer im II. Weltkrieg:

**Z3 (1941):**

- 25.000 Dt. Reichsmark der Deutschen Versuchsanstalt für Luftfahrt
- Zuse war nicht Mitglied der NSDAP
- Kurz beim Militär, dann fördern ihn Henschel-Flugzeug-Werke als Statiker zurück
- Flugzeug-Werke waren Rüstungskonzern der NS

**Colossus (1943):**

- Röhrencomputer - Bletchley Park, England (Alan Turing)
- Dechiffrierung von geheimen Nachrichten des dt. Militärs im II. WK

**Mark I (1944):**

- Harvard, USA
- 1. Programm: John von Neumann - Manhattan Project - Rechnungen am Implosionskonzept der Plutonium-Bombe

---

## 📌 Zusammenfassung

### Wichtigste Entwicklungsschritte

1. **Antike:** Abakus - erste mechanische Rechenhilfe (~2500 v.Chr.)
2. **17. Jh.:** Mechanische Rechenmaschinen (Schickard, Pascal, Leibniz) - nur 4 Grundrechenarten
3. **19. Jh.:**
    - Jacquard-Webstuhl (1801) - **Programmierbarkeit** durch Lochkarten
    - Babbage's Analytical Engine (1837) - **Konzept** des Mehrzweck-Rechners (scheiterte)
    - Hollerith (1890) - Lochkarten für Datenverarbeitung
4. **1936:** Turing's theoretischer Aufsatz + Zuse beginnt mit Z1
5. **1941:** Z3 - **erster funktionsfähiger programmgesteuerter Digitalrechner**

### Schlüsselkonzepte moderner Computer

|Konzept|Bedeutung|Erstmals realisiert|
|---|---|---|
|**Programmierbarkeit**|Trennung Hardware/Software|Jacquard (1801), Babbage (Konzept 1837)|
|**Binärsystem**|Robuste 2-Zustands-Darstellung|Zuse Z1/Z3 (1936-1941)|
|**Trennung Prozessor/Speicher**|Moderne Rechnerarchitektur|Zuse Z3 (1941)|
|**Universalrechner (Konzept)**|Theoretische Grundlage|Turing (1936)|
|**Gleitkommaarithmetik**|Effiziente Zahlendarstellung|Zuse Z1/Z3 (1936-1941)|

### Wichtige Unterschiede: Mittelalter vs. Moderne

**Rechengeräte des Mittelalters:**

- Bei ihrer Erbauung auf **eine Funktion** festgelegt
- Keine Trennung von Hardware und Software
- Kein Speicher, kein Programm

**Zuse's Computer:**

- **Programmierbar** - dieselbe Maschine für verschiedene Aufgaben
- **Speicher** für Daten und Zwischenergebnisse
- Automatische Ausführung von Rechenoperationen

### Konzeptuelle Analogie: Buchdruck

**Buchdruck mit beweglichen Lettern:**

- Dieselben Teile (Letter) erzeugen in verschiedener Anordnung unterschiedliche Dinge
- Arbeitserleichterung durch **Flexibilität**, kostengünstig, wiederholbar

**Vergleichbar mit programmierbaren Maschinen:**

- Dieselbe Hardware führt verschiedene Programme aus
- Flexibilität durch Software statt durch mechanische Umbauten

---

## 🔗 Verbindungen zu anderen Vorlesungen

- **Wissenschaftliches Arbeiten:** Fragengeleitetes Lesen, Aufbau auf vorhandenem Wissen
- **Von-Neumann-Architektur:** Moderne Computer-Grundstruktur
- **Binärsystem:** Basis digitaler Informationsverarbeitung