**Class:** [[Wissenschaftliches Arbeiten]]  
**Date:** 26-12-2026  
**Topics:** #KünstlicheIntelligenz #MaschinellesLernen #Anthropomorphismus #Intelligenz #DeepLearning #NeuronaleNetze #Superintelligenz

---

## 🎯 Lernziele der Vorlesung

Künstliche Intelligenz (KI) ist ein aktuelles und wichtiges Forschungsfeld. Diese Vorlesung behandelt grundlegende Konzepte von KI, maschinellem Lernen und die kritische Auseinandersetzung mit Intelligenz.

- Definition und Abgrenzung von **Intelligenz** und **Künstlicher Intelligenz**
- Grundlagen des **maschinellen Lernens** und **tiefer neuronaler Netze**
- **Anthropomorphismus** als menschliche Eigenschaft
- Unterschiede zwischen **menschlicher** und **maschineller** Intelligenz
- **Kritisches Denken** über KI-Systeme und deren Grenzen
- **Dual Use** und Technikfolgenabschätzung

---

## 1. Was ist Intelligenz?

### Definition von Intelligenz

**Psychologische Definition:** Intelligenz ist das, was ein Intelligenztest misst

**Problematik der Definition:**

- Intuitiv: "We know it when I see it"
- **Stichprobenabhängig**: Teststichprobe und Validierungsstichprobe
- **Aufgabenabhängig**: Welche Aufgaben werden gewählt?

### Intelligenztest-Methodik

**Vorgehen:**

1. Große Menge von Aufgaben, die vermeintlich Intelligenz erfordern
2. Aufgaben, die von wenigen Personen gelöst werden können, sind schwerer als Aufgaben, die von vielen gelöst werden können
3. Personen, die mehr schwere Aufgaben lösen können, sind per Definition intelligenter

**Typische Testaufgaben:**

- **Wortanalogien** (verbal/semantisch/konzeptuell): Lehrer : Kreide = Soldat : ?
- **Zahlenfolgen** (mathematisch/numerisch): 1, 1, 2, 3, 5, 8, ?
- **Geometrische Analogien**: Mustererkennung
- **Räumliches Schlussfolgern**: 3D-Aufgaben

### Allgemeine Intelligenz

**Definition:** Fähigkeit, viele verschiedene (mehr oder weniger sinnvolle) Testaufgaben erfolgreich zu bearbeiten

**Psychologische Befunde:**

- Verschiedene Faktoren bestimmen die Testleistung (sprachliche, numerische, visuelle Fähigkeiten)
- Es gibt einen **allgemeinen Faktor** für Intelligenz über alle Aufgaben hinweg
- Personen mit höherer allgemeiner Intelligenz sind tendenziell in allen Testaufgaben besser
- Korrelation mit Schulerfolg und beruflichem Erfolg

---

## 2. Definition von Künstlicher Intelligenz

### Verschiedene Definitionen

**Pragmatische Definition:**

$$\boxed{\text{KI wird attestiert, wenn Computerprogramme Aufgaben übernehmen, für die Menschen Intelligenz benötigen}}$$

**Paradoxon der KI-Definition:**

- Eine Fähigkeit gilt so lange als Ausdruck von Intelligenz, bis ein Computer sie ausführen kann
- Gerade jene Fähigkeiten gelten als Ausdruck spezifisch menschlicher Intelligenz, die ein Computer **nicht** beherrscht

**Konsequenz:** Echte KI kann es nach dieser Definition nicht geben (bewegliches Ziel)

### KI als Alltagsbegriff

**Früher:** "Computer" war eine Berufsbezeichnung (meist Frauen), die physikalische Berechnungen durchführten

**Heute:** Selbst einfache Taschenrechner sind technisch gesehen eine Form von KI

**Problem:** Der Begriff "KI" weckt große Erwartungen, führt aber auch zu Enttäuschungen

---

## 3. Maschinelles Lernen und Deep Learning

### Hierarchie der Begriffe

```
Künstliche Intelligenz (KI)
    ↓
Maschinelles Lernen
    ↓
Künstliche Neuronale Netzwerke
    ↓
Deep Neural Networks (DNN)
    ↓
Transformermodelle (z.B. LLMs)
    ↓
ChatGPT (Large Language Model)
```

**Maschinelles Lernen:** Oberbegriff für Verfahren, bei denen Computer aus Daten Muster lernen

**Deep Neural Networks:** Künstliche neuronale Netzwerke mit vielen Schichten

**Large Language Models (LLM):** Transformermodelle, die auf Sprachverarbeitung trainiert wurden

---

## 4. Architektur tiefer neuronaler Netze

### Grundstruktur

**Neuronale Netze sind mathematische Modelle:**

- Gerichtete Graphen bestehend aus Knoten (Neuronen) und Kanten (gewichteten Verbindungen)
- **Abstraktion** von biologischen Nervenzellen
- In verschiedenen **Schichten** organisiert
- Schichten haben unterschiedliche Funktionen

### Funktion eines Neurons

**Verarbeitungsschritte:**

1. Jedes Neuron bekommt **Zahlen als Eingabe**
2. Multipliziert sie mit **Gewichten** $w_i$
3. Addiert einen **Bias** $b$
4. Schickt das Ergebnis durch eine **Aktivierungsfunktion**

$$\text{Output} = f\left(\sum_i w_i \cdot x_i + b\right)$$

---

## 5. Lernen in tiefen neuronalen Netzen

### Lernprozess (Training)

**1. Vorwärtsdurchlauf (Forward Pass):**

- Input wird Schicht für Schicht verarbeitet
- Ergebnis: Vorhersage (Output)

**2. Fehlerberechnung:**

- Vorhersage wird mit Zielwert verglichen
- Berechnung des Fehlers (loss)

**3. Rückwärtsdurchlauf (Backpropagation):**

- Netz berechnet, wie stark jedes Gewicht und Bias zum Fehler beiträgt
- Verwendet **Ableitungen (Gradienten)** der Aktivierungsfunktion und des Fehlers
- **Gewichte und Bias werden angepasst**, um Fehler zu minimieren

**Iterativer Prozess:** Wiederholung bis der Fehler nicht mehr kleiner wird

---

## 6. Lineare Regression als Beispiel

### Modell 1: Mittelwert

**Vorhersage:** $\bar{y} = \frac{1}{n}\sum_{i=1}^n y_i$

**Fehler (Standardabweichung):**

$$s_y = \sqrt{\frac{1}{n}\sum_{i=1}^n (y_i - \bar{y})^2}$$

### Modell 2: Lineare Regression

**Vorhersage:** $\hat{y} = b \cdot x + a$

**Fehler (Residuen):**

$$s_{\hat{y}y} = \sqrt{\frac{1}{n}\sum_{i=1}^n (y_i - \hat{y}_i)^2}$$

Typischerweise gilt: $s_{\hat{y}y} < s_y$ (bessere Vorhersage)

### Verbindung zum Maschinellen Lernen

**Ziel:** Minimiere die Abstände zwischen Vorhersage und Daten

**Vorgehen:** $y = w \cdot x + \text{bias}$

1. Wähle Startwerte für $w$ und bias (z.B. $w = 0$, $\text{bias} = \bar{y}$)
2. Berechne Vorhersage und Differenz zu tatsächlichen Werten
3. Backpropagation des Fehlers und Anpassung der Parameter
4. Wiederhole bis Konvergenz

**Wichtig:** Das **Modell steckt in den Gewichten und der Architektur**

### Einfache vs. Multiple Lineare Regression

|Einfache Regression|Multiple Regression|
|---|---|
|$y = \beta \cdot x + \alpha$|$Y = \beta_1 \cdot X_1 + \ldots + \beta_n \cdot X_n + \alpha$|
|$x, y$ - Abszisse, Ordinate|$X_i, Y$ - Dimensionen im Vektorraum|
|$\beta, \alpha$ - Anstieg, Achsenabschnitt|$\beta_i, \alpha$ - Gewichte, Fehler|
|Modell ist Linie|Modell ist Hyperebene|

---

## 7. Unterschied: Menschliche vs. Maschinelle Intelligenz

### Inselbegabungen von KI-Systemen

**Charakteristik aktueller KI:**

- Schachprogramme spielen nur Schach
- Taschenrechner rechnen nur
- Programme zur Analyse von Röntgenbildern analysieren nur Röntgenbilder
- In allem **teils besser als Menschen**, aber **Inselbegabungen**

**Fehlende Transferfähigkeit:**

- "Erfahrungen" im Schach nicht übertragbar auf Poker oder Dame
- Jede Aufgabe braucht ein eigenes, neues KI-Programm

### Menschliche Flexibilität

**Menschen:**

- Setzen flexibel unterschiedliche Strategien bei verschiedenen Problemen ein
- Übertragen eine Strategie auf verschiedene Probleme
- Können Erfahrungen nutzen, um neue Aufgaben schneller zu lernen
- Besitzen **allgemeine Intelligenz**, nicht auf bestimmte Aufgaben beschränkt

### Historische Entwicklung

**Frühe KI-Forschung (1950er-1960er):**

- Ziel: Allgemeine Prinzipien intelligenten menschlichen Verhaltens in Computerprogramme gießen
- Beispiel: "General Problem Solver" - sollte beliebige Probleme eigenständig lösen
- Problem: Menschen nutzen unterschiedliche Strategien bei verschiedenen Problemen

**Moderne KI:**

- Fokus auf spezielle Lösungen für spezielle Probleme (sehr erfolgreich)
- Wiederbelebung des Traums der allgemeinen Intelligenz
- Neues Schlagwort: **Allgemeine Künstliche Intelligenz (AKI)** / Artificial General Intelligence (AGI)

---

## 8. Anthropomorphismus

### Definition

$$\boxed{\text{Anthropomorphismus: Zuschreiben menschlicher Eigenschaften zu nicht-menschlichen Wesen oder Objekten}}$$

Altgriechisch: _anthropos_ = "Mensch", _morphē_ = "Form, Gestalt"

### Anthropomorphismus als fundamentale menschliche Eigenart

**Begriff der Kognitionspsychologie:**

- **Attribution**: Zuschreibung von Ursachen zu verschiedenen Handlungen und Verhaltensweisen
- **Fundamentaler menschlicher Bias**: Wir neigen dazu, allem Intentionen zuzuschreiben

**Klassisches Experiment: Heider & Simmel (1944):**

- Versuchspersonen sehen geometrische Formen (Dreiecke, Kreise), die sich bewegen
- Menschen schreiben den Formen automatisch Absichten, Emotionen und soziale Beziehungen zu
- Zeigt: Anthropomorphismus ist eine automatische kognitive Reaktion

### ELIZA - Früher Chatbot (1966)

**Entwickler:** Joseph Weizenbaum

**Funktionsweise:**

- "Großmutter" heutiger Chatbots
- Unterhaltung in natürlicher Sprache
- Ein- und Ausgabe in Form von Sätzen in der Konsole
- Festgelegte Themen, die vorher programmiert wurden
- **Cover Story:** ELIZA ist eine Psychiaterin

**Techniken:**

- Gezielte Fragen stellen
- Schlüsselwörter erkennen (z.B. "unglücklich", "Mutter")
- Einfache Musterersetzung

**Wichtige Erkenntnis:** Menschen neigen dazu, dem System mehr Verständnis zuzuschreiben, als tatsächlich vorhanden ist

---

## 9. Was wird tatsächlich gelernt?

### Problem der Übertragbarkeit

**Objekterkennung (Geirhos et al., 2019):**

- Ziel: Computer soll Objekte in Bildern erkennen
- Problem: Was lernt das System wirklich?

**Wichtigkeit von Transfertests:**

- Ohne Transfertests ist nicht klar, was gelernt wird
- System könnte oberflächliche Merkmale statt konzeptuellem Verständnis lernen

### Erkennen vs. Erklären

**Zwei verschiedene Fähigkeiten:**

- **Erkennen von Zusammenhängen**: Korrelationen in Daten finden
- **Erklären von Zusammenhängen**: Kausale Mechanismen verstehen

**Aktuelle KI:** Meist sehr gut im Erkennen, schwach im Erklären

---

## 10. Zutaten für Allgemeine Künstliche Intelligenz

### Drei essenzielle Komponenten

**1. Suchalgorithmen**

- Systematisches Durchsuchen von Lösungsräumen
- Finden optimaler oder guter Lösungen

**2. Lernalgorithmen**

- Selbständiges Lernen aus Daten
- Anpassung ohne explizite Programmierung für jedes Problem
- Vom Gehirn inspiriert

**3. Sprachmodelle**

- Integration von Sprachverständnis
- Zugang zu Alltagswissen
- Viele Aufgaben haben einen Sprachanteil

**Aktueller Stand (2025):** Sprachmodelle scheinen ein wichtiger Schritt hin zu AKI-Systemen zu sein, können als Grundlage für viele verschiedene Aufgaben dienen

**Noch fehlend:** Integration mit Wahrnehmung und einem Körper, der sich bewegen kann

---

## 11. Dual Use und Technikfolgenabschätzung

### Definition Dual Use

$$\boxed{\text{Dual Use: Mehrfachnutzung von Waren, Gütern, Algorithmen, Ergebnissen}}$$

**Problem:** Folgen und "Nutzen" sind zu Zeiten der Entwicklung nicht abzuschätzen

### Beispiele und Risiken

**Statement (Center for AI Safety):**

> "Mitigating the risk of extinction from AI should be a global priority alongside other societal-scale risks such as pandemics and nuclear war."

**Zentrale Fragen:**

- Führen KI-Systeme lediglich Befehle aus?
- Verstehen sie, was sie tun?
- Ist es angemessen, deren Verhalten nur als Ausführen von Befehlsfolgen zu betrachten?

**Wichtig:** Risiken, die von solchen Systemen ausgehen können, sind **unabhängig** davon, ob man diesen Systemen Eigenschaften wie Verstehen oder Bewusstsein zuordnet oder nicht

### Begriffe

**Singularität:**

- Hypothetischer zukünftiger Zeitpunkt, an dem KI die menschliche Intelligenz übertrifft
- Ray Kurzweil prognostiziert Jahr 2045
- Vorstellung einer "Intelligenzexplosion": KI entwickelt bessere KI

**Superintelligenz:**

- KI, die menschliche Intelligenz in allen Bereichen übertrifft
- Derzeit Science-Fiction

**AGI (Artificial General Intelligence):**

- KI mit menschenähnlicher allgemeiner Intelligenz
- Kann verschiedenste Aufgaben lösen wie ein Mensch
- Derzeit noch nicht erreicht

---

## 12. Vertrauenswürdigkeit von Quellen

### Hierarchie der Vertrauenswürdigkeit

**1. Wissenschaftliche Fachzeitschriften (höchste Vertrauenswürdigkeit):**

- Peer-Review-Prozess
- Autorinnen ohne direkte finanzielle Anreize
- Systematische Qualitätskontrolle

**2. Fachzeitschriften (z.B. c't, Computerwoche):**

- Kostenpflichtig
- Freiberufliche Reporterinnen (finanzielle Anreize)
- Redaktionelle Begutachtung

**3. Tages-/Wochenzeitungen (z.B. Die Zeit):**

- Festangestellte Mitarbeitende
- Kostenpflichtig
- Breites Themenspektrum
- Informations- und Nachrichtenorientierung

**4. Online-Magazine (z.B. Telepolis):**

- Breites Themenspektrum
- Freiwilliges Unterstützermodell
- Kostenfrei
- Freie Autorinnen

**5. Boulevardzeitung (z.B. BILD):**

- Mischform von Sensations- und Nachrichtenorientierung
- Geringere Vertrauenswürdigkeit

---

## 📌 Zusammenfassung

### Definitionen

|Begriff|Definition|Bemerkung|
|---|---|---|
|**Intelligenz**|Das, was ein Intelligenztest misst|Stichproben- und aufgabenabhängig|
|**KI**|Computerprogramme, die Aufgaben übernehmen, für die Menschen Intelligenz benötigen|Bewegliches Ziel|
|**Maschinelles Lernen**|Verfahren, bei denen Computer aus Daten Muster lernen|Oberbegriff|
|**Deep Learning**|Neuronale Netze mit vielen Schichten|Teil des ML|
|**Anthropomorphismus**|Zuschreiben menschlicher Eigenschaften zu nicht-menschlichen Objekten|Fundamentaler menschlicher Bias|

### Kernaussagen

✅ **Intelligenz** ist schlecht definiert - sowohl bei Menschen als auch Maschinen

✅ **Aktuelle KI** hat Inselbegabungen, keine allgemeine Intelligenz

✅ **Menschen** nutzen flexibel verschiedene Strategien und können Transfer leisten

✅ **Lernen in Neuronalen Netzen:** Vorwärtsdurchlauf → Fehler → Backpropagation → Anpassung

✅ **Anthropomorphismus** führt dazu, dass wir KI mehr zuschreiben als gerechtfertigt

✅ **Dual Use:** Technologien können unvorhersehbare Folgen haben

### Drei Zutaten für AKI (Allgemeine Künstliche Intelligenz)

1. **Suchalgorithmen** - Systematisches Finden von Lösungen
2. **Lernalgorithmen** - Selbständiges Lernen aus Daten
3. **Sprachmodelle** - Integration von Sprache und Alltagswissen

### Kritisches Denken über KI

❌ KI "versteht" nicht im menschlichen Sinne

❌ Aktuelle KI ist keine allgemeine Intelligenz

❌ Korrelation ≠ Kausalität (Erkennen ≠ Erklären)

✅ Transfertests sind notwendig, um zu verstehen, was gelernt wird

✅ Risiken sollten unabhängig von philosophischen Fragen (Bewusstsein, Verstehen) bewertet werden

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.08 AI Bias und Data Ethics]]: Bewertung von Aussagen über KI
- [[VL.10 Wahrscheinlichkeit und Intuition]]: Korrelation und Kausalität