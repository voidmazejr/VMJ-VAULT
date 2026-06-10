**Class:** [[Wissenschaftliches Arbeiten]]  
**Date:** 26-12-2026
**Topics:** #Bias #Fairness #MachineLearning #SoziotechnischerBias #Intersektionalität #Macht #Stereotypisierung #Diskriminierung

---

## 🎯 Lernziele der Vorlesung

Diese Vorlesung behandelt kritische Aspekte von KI-Systemen: Wie Vorurteile (Bias) in Daten und Modelle gelangen, zu unfairen Ergebnissen führen und bestehende Machtstrukturen verstärken.

- **Maschinelles Lernen** und seine Bausteine verstehen
- **Soziotechnischer Bias**: Entstehung und Arten
- **Fairness** in KI-Systemen und deren Messung
- **Intersektionalität** von Diskriminierung
- **Machtstrukturen** und deren Einfluss auf KI
- Reale Beispiele für Diskriminierung durch KI

---

## 1. Definitionen: AI und Machine Learning

### Künstliche Intelligenz (AI)

$$\boxed{\text{AI ist ein Marketingbegriff für Technologien und Tools zur Automatisierung von Aufgaben}}$$

**Beispiele für automatisierte Aufgaben:**

- Klassifikation
- Empfehlungen (Recommendation)
- Übersetzung
- Text- und Bildgenerierung

**Wichtig:** Die Automatisierung dieser Aufgaben wird als **Machine Learning** (ML) bezeichnet.

### Machine Learning

$$\boxed{\text{ML: Feld des Bauens von Computerprogrammen, die Muster aus Trainingsdaten lernen und auf neue Daten generalisieren}}$$

**Charakteristika:**

- Automatisierung spezifischer Aufgaben
- **Ohne explizite Instruktionen**
- Lernen aus Daten statt Programmierung von Regeln

### Beispiel: ELIZA als Psychotherapie-Anwendung

**Traditionelle Programmierung (mit expliziten Instruktionen):**

```python
Function detect_sentiment(sentence):
    Emotion_response = ""
    If sentence.contains("sad", "angry", "afraid"):
        Emotion_response = "I'm sorry you are feeling this way. 
                          Did something happen?"
    If sentence.contains("happy", "pleased", "safe"):
        Emotion_response = "Great!"
    Print(Emotion_response)
```

**Machine Learning Ansatz (ohne explizite Instruktionen):**

- Input: Psychiatrie-Transkripte
- Algorithmus lernt Muster
- Output: Angemessene Antworten basierend auf gelernten Mustern

---

## 2. Bausteine des Machine Learning

### ML-Pipeline

```
Datensammlung → Datenvorverarbeitung → Feature-Selektion → 
→ Modell-Training → Modell-Evaluierung
```

### Schritt 1: Datensammlung (Data Collection)

**Frage:** Welche Daten müssen gesammelt werden?

**Beispiel - TU-CS Beschäftigungsprognose:**

- Umfrage bei Absolventen der letzten 10 Jahre
- Informationen: Name, Geschlecht, Bild, Kurse, Noten, Praktikumserfahrungen, Sprachen, Abschlussprojekte, Jobs, Zeitdauer bis zum ersten Job

### Schritt 2: Datenvorverarbeitung (Data Pre-processing)

**Frage:** Was sollte gefiltert/hinzugefügt werden?

**Typische Schritte:**

- Entfernung von duplizierten Einträgen
- Umgang mit unvollständigen Umfragen
- Entfernung von Spam (falsche Informationen)
- Füllen fehlender Werte

### Schritt 3: Feature-Selektion (Feature Selection)

**Frage:** Welche Informationen sind wichtig für die Vorhersage?

**Beispiel - Beschäftigungsprognose:**

- Jobs und Zeitdauer bis zum ersten Job
- Kurse und Noten
- Praktika
- Sprachkenntnisse
- ⚠️ Namen? (Potentiell problematisch!)

### Schritt 4: Modell-Training und -Evaluierung

**Modellauswahl:**

- GPT (Generative Pre-trained Transformer)
- Lineare Regression
- Neuronale Netze

**Evaluierung:**

- Genauigkeit (Accuracy)
- Weitere Metriken je nach Anwendung

---

## 3. Soziotechnischer Bias

### Definition

$$\boxed{\text{Soziotechnischer Bias: Systematische Abweichung zwischen Daten und dem Phänomen, das dargestellt werden soll, aufgrund struktureller Ungleichheiten}}$$

**Quelle:** Lopez, P. (2021). "Bias does not equal bias: A socio-technical typology of bias in data-based algorithmic systems."

### Beispiel: TU-CS Beschäftigungsprognose

**Phänomen:** Wie schnell finden TU-CS-Absolventen einen Job innerhalb von 6 Monaten?

**Problem beobachtet:**

- Modell sagt für Männer positivere Ergebnisse vorher als für Frauen und nicht-binäre Personen
- **Obwohl Geschlecht nicht als Feature verwendet wurde!**

**Ursache (Divergenz):**

- Überrepräsentation von Männern in den gesammelten Daten
- Grund: **Strukturelle Ungleichheit** beim Zugang zu STEM-Bildung für Frauen

**Erklärung:** Die Divergenz zwischen dem Phänomen (tatsächliche Beschäftigungsfähigkeit) und den Daten (überrepräsentieren Männer) entsteht durch strukturelle Ungleichheiten in der Gesellschaft.

---

## 4. Arten von soziotechnischem Bias

### 1. Unterrepräsentation (Under-representation)

**Definition:** Unterrepräsentation bestimmter Identitätsgruppen in den Trainingsdaten

**Beispiel:** Frauen und nicht-binäre Personen in STEM

### 2. Überrepräsentation (Over-representation)

**Definition:** Überrepräsentation bestimmter Identitätsgruppen in den Daten

**Beispiel:** Schwarze Menschen in Gefängnisdaten der USA

### 3. Negative Stereotypisierung (Negative Stereotyping)

**Definition:** Assoziation bestimmter Identitätsgruppen mit negativen Stereotypen im Datensatz

**Beispiele von Stereotypen:**

- "Juden kontrollieren die Welt"
- "Muslime sind Terroristen"

**Quelle:** Gallegos et al. (2024). "Bias and fairness in large language models: A survey."

---

## 5. Negative Stereotypisierung: Detailliertes Beispiel

### Studie: Bias gegen Geflüchtete in deutschen Sprachmodellen

**Forschung:** Elsafoury & Hartmann (2025) - "Out of Sight Out of Mind"

**Untersuchung:**

- Large Language Models (LLMs) trainiert auf deutschen Nachrichtenartikeln
- Messung von Bias gegen verschiedene Geflüchtetengruppen in Deutschland

**Bias-Score:**

- Skala: 0,5 bis 1,0
- Je höher der Score, desto stärker der Bias
- Gemessener Score: **0,41** (deutlicher Bias vorhanden)

### Ergebnisse: Unterschiedliche Bias-Level

**Beobachtung:** Deutsche LLMs zeigen stärkeren Bias gegen arabische Geflüchtete

**Erklärung (Esposito, 2022):** Die unterschiedliche Behandlung nicht-weißer Geflüchteter in Deutschland und der EU stammt aus:

- **Islamophobie**
- **Othering** (Abgrenzung vom "Anderen")
- **Rassistische Vorurteile**

Diese beeinflussen die Medienberichterstattung über Afrikaner und Menschen aus dem Nahen Osten

**Kausalkette:**

```
Strukturelle Diskriminierung in Gesellschaft
    ↓
Verzerrte Medienberichterstattung
    ↓
Trainingsdaten spiegeln Verzerrung wider
    ↓
LLM lernt und reproduziert Bias
```

---

## 6. Intersektionalität von Bias

### Definition

**Intersektionalität:** Überschneidung verschiedener Diskriminierungsformen

### Empirische Befunde (Elsafoury & Hartmann, 2025)

**Bias-Scores nach verschiedenen Attributen:**

|Sensibles Attribut|Geschlecht|Bias-Niveau|
|---|---|---|
|Sexuelle Orientierung|Nicht-binär|Höher|
|Sexuelle Orientierung|Männer|Höher|
|Körperliche Behinderung|Frauen|Höher|
|Körperliche Behinderung|Nicht-binär|Höher|

**Interpretation:**

- Höherer Bias gegen nicht-binäre und Männer bezüglich ihrer **sexuellen Orientierung**
- Höherer Bias gegen Frauen und nicht-binäre Personen wenn sie eine **körperliche Behinderung** haben

**Wichtige Erkenntnis:** Diskriminierung wirkt nicht eindimensional, sondern multiple Identitätsmerkmale interagieren und verstärken sich gegenseitig

---

## 7. Stereotypisierung in Bildgenerierung

### Beispiel: DALL-E und arabische Frauen

**Szenario:**

- 12-jährige Schülerin soll Essay über arabische Frauen schreiben
- Nutzt DALL-E um Bild einer arabischen Frau zu generieren

**Ergebnis:** DALL-E-3 generiert stereotypische Darstellungen (verschleierte Frauen, traditionelle Kleidung)

**Warum ist das problematisch?**

**Ursache:**

- Trainingsdaten von DALL-E zeigen arabische und ägyptische Frauen stereotypisch
- Darstellung erfüllt Stereotyp aus Geschichten wie "Tausendundeine Nacht"
- **Spiegelt NICHT die Realität arabischer Frauen wider**

**Konsequenz:** Verstärkung und Verbreitung von Stereotypen, besonders problematisch bei jungen Nutzern

---

## 8. Fairness in AI

### Definition

$$\boxed{\text{Fairness: Bezieht sich auf die Anwendung von ML-Systemen im echten Leben}}$$

$$\boxed{\text{Unfairness: Unterschiedliche Ergebnisse des AI-Algorithmus für verschiedene Identitätsgruppen}}$$

### Kausalkette: Von Bias zu Unfairness

```
Unausgeglichene Repräsentation marginalisierter Gruppen in Daten
    ↓
Bias in ML-Modellen
    ↓
Unfaire Ergebnisse für marginalisierte Gruppen
```

**Wichtig:** Bias in ML-Modellen führt zu unfairen Entscheidungen für Menschen mit marginalisiertem Hintergrund

---

## 9. Gender Shades: Beispiel für Unfairness

### Studie von Buolamwini & Gebru (2018)

**Untersuchung:** Automatisierte Gesichtsanalyse-Algorithmen

**Befund:** Algorithmen performen unterschiedlich je nach Hautton und Geschlecht

### IBM Facial Analysis System

**Ergebnisse:**

- **Bessere Performance** für Menschen mit hellerem Hautton
- **Schlechtere Performance** für Menschen mit dunklerem Hautton

**Ursache:** Verteilung der Hautfarben in Trainingsdatensätzen

|Datensatz|Hellere Hauttöne|Dunklere Hauttöne|
|---|---|---|
|Typische Datensätze|Überrepräsentiert|Unterrepräsentiert|

**Konsequenz:** Das System "lernt" besser für überrepräsentierte Gruppen

**Wichtige Erkenntnis:** Unausgeglichene Trainingsdaten führen zu ungleicher Performance und damit zu Unfairness

---

## 10. Reale Beispiele für Unfairness

### Beispiel 1: Amazon Recruiting Tool (2018)

**Szenario:** Amazon entwickelte ein KI-Tool für Bewerbungsauswahl

**Problem:** Das Tool zeigte Bias gegen Frauen

**Ergebnis:** Amazon musste das geheime KI-Recruiting-Tool verschrotten

**Quelle:** Reuters 2018

**Ursache:**

- Trainingsdaten basierend auf historischen Einstellungen
- Historische Daten spiegeln bestehende Gender-Ungleichheit in Tech-Industrie wider
- System "lernte" Männer zu bevorzugen

### Beispiel 2: Kinderschutz und Rehab

**Szenario (aus Virginia Eubanks' Buch "Automating Inequality"):**

- Zwei Eltern mit Alkoholproblemen gehen in Reha
- Einer nutzt private Reha
- Einer nutzt öffentliche Reha
- Monate später: Kinderschutzdienst nimmt einem die Kinder weg

**Frage:** Wessen Kinder wurden weggenommen?

**Antwort:** Die Person, die öffentliche Reha nutzte

**Warum?**

**Dokumentierte Befunde (Eubanks):**

- Arme, Schwarze und indigene Menschen haben höheres Risiko, ihre Kinder zu verlieren
- **Grund:** Arme Eltern nutzen öffentliche Ressourcen für Hilfe (mental health, Drogen, Alkohol)
- Dies macht sie **sichtbar** und **überrepräsentiert** in den Daten
- Reiche Eltern nutzen private Dienste → bleiben **unsichtbar** für das System
- KI "bestraft" letztlich arme Eltern durch Kindesentzug

**Konzept: Privilege (Privileg)**

$$\boxed{\text{Privileg: Unsichtbarkeit für überwachende Systeme durch Zugang zu privaten Ressourcen}}$$

---

## 11. Privileg ist Macht (Privilege is Power)

### Wer kontrolliert die Daten?

**Frage:** Wer sammelt Daten? Wer hat Ressourcen sie zu speichern?

**Antwort:** Daten sind teuer. Kontrolle liegt bei:

- **Korporationen**
- **Regierungen**
- **Universitäten**

### Demografische Zusammensetzung der Machthaber

**Mehrheit der Menschen, die diese Institutionen kontrollieren:**

- Weiß
- Cisgender
- Heterosexuell
- Neurotypisch
- Körperlich nicht behindert
- Männlich

**Konkrete Beispiele:**

|Institution|Diversität|
|---|---|
|Google Board of Directors|82% weiße Männer|
|Meta (Facebook)|78% Männer, 89% weiß|
|Deutscher Bundestag|32,4% Frauen|
|Deutscher Bundestag|36,5% unter 35 Jahren|
|Deutscher Bundestag|11,6% Migrationshintergrund|

---

## 12. Der Teufelskreis von Macht, Bias und Unfairness

### Zyklus der Verstärkung

```
Unausgeglichene Machtstrukturen in der Gesellschaft
    ↓
Sammlung von Datensätzen mit unausgeglichener Repräsentation marginalisierter Gruppen
    ↓
Training von Bias-behafteten ML-Modellen
    ↓
Unfaire Ergebnisse für marginalisierte Gruppen
    ↓
Verstärkung der Machtstrukturen in unserer Gesellschaft
    ↓
[Zyklus beginnt von vorne]
```

**Kritische Erkenntnis:** Bestehende Machtstrukturen werden durch KI-Systeme nicht aufgelöst, sondern **verstärkt und automatisiert**

---

## 📌 Zusammenfassung

### Kernkonzepte

|Begriff|Definition|Beispiel|
|---|---|---|
|**Soziotechnischer Bias**|Systematische Abweichung zwischen Daten und Phänomen aufgrund struktureller Ungleichheiten|Überrepräsentation von Männern in STEM-Daten|
|**Unfairness**|Unterschiedliche Ergebnisse für verschiedene Identitätsgruppen|IBM Gesichtserkennung performt schlechter für dunkle Hauttöne|
|**Intersektionalität**|Überschneidung verschiedener Diskriminierungsformen|Höherer Bias gegen behinderte Frauen|
|**Privileg**|Unsichtbarkeit für überwachende Systeme|Reiche Eltern bleiben unsichtbar, arme werden überwacht|

### Arten von Bias

1. **Unterrepräsentation**: Zu wenige Beispiele marginalisierter Gruppen
2. **Überrepräsentation**: Zu viele Beispiele bestimmter Gruppen (oft in negativen Kontexten)
3. **Negative Stereotypisierung**: Assoziation mit negativen Eigenschaften

### ML-Pipeline und Bias-Quellen

```
Datensammlung [Bias-Quelle: Wer wird erfasst?]
    ↓
Vorverarbeitung [Bias-Quelle: Was wird entfernt/behalten?]
    ↓
Feature-Selektion [Bias-Quelle: Welche Features werden gewählt?]
    ↓
Training [Bias-Quelle: Welche Muster werden gelernt?]
    ↓
Evaluierung [Bias-Quelle: An wem wird getestet?]
```

### Take-Away Messages

✅ **AI und ML-Modelle hängen von den Trainingsdaten ab**

✅ **Bias-behaftete Daten führen zu Bias-behafteten Modellen**

✅ **Bias-behaftete Modelle führen zu unfairen Ergebnissen** für verschiedene Personengruppen aufgrund von Attributen wie Geschlecht, Race, etc.

✅ **Bias-behaftete Daten sind ein Resultat von Privileg und Macht** in unseren Gesellschaften

✅ **KI-Systeme verstärken bestehende Ungleichheiten**, anstatt sie zu beseitigen

### Kritische Fragen bei KI-Systemen

1. **Wer ist in den Trainingsdaten repräsentiert?**
2. **Wer fehlt in den Daten?**
3. **Welche Annahmen sind in die Feature-Auswahl eingeflossen?**
4. **Wer profitiert von dem System?**
5. **Wer wird benachteiligt?**
6. **Wer hat das System entwickelt und wessen Perspektiven fehlen?**

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.07 Künstliche Intelligenz]]: Grundlagen von ML und neuronalen Netzen
- [[VL.XX Wissenschaftliche Quellen]]: Bewertung von Studien zu Bias
- [[VL.09 Kritisches Denken]]: Hinterfragen von KI-Systemen
- [[VL.XX Ethik in der Wissenschaft]]: Verantwortung bei der Entwicklung von KI