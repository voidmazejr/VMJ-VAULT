**Class:** [[DS - Diskrete Strukturen]]  
**Date:** 17-04-2026  
**Topics:** #Einführung #Kombinatorik #Graphen #Induktion #Abstraktion

---

## 🎯 Lernziele der Vorlesung

Diskrete Strukturen behandelt **endliche und abzählbare** mathematische Objekte und deren Anwendung in der Informatik. Im Mittelpunkt stehen Modellierung, Zählen und Beweisen.

- **Modellierung und Abstraktion**: Reale Probleme als mathematische Modelle beschreiben
- **Kombinatorik**: Zählen von Möglichkeiten, Grundlage für Laufzeitanalyse
- **Graphen**: Wichtigstes Modell für Netzwerke und Zuordnungen
- **Induktion**: Grundlegendes Beweisverfahren für Aussagen über $\mathbb{N}$
- **Zahlentheorie & Kryptographie**: Grundlage für RSA und Public-Key-Verschlüsselung

---

## 1. Was sind Diskrete Strukturen?

### Definition (Diskret)

**Diskret** bedeutet hier im Sinne von *trennbar*: Der Fokus liegt auf **endlichen oder abzählbaren** Objekten, z.B. endliche Graphen, algebraische Strukturen oder ganze Zahlen.

Im Gegensatz dazu stehen Analysis und Lineare Algebra, die sich mit überabzählbaren, kontinuierlichen Objekten wie $\mathbb{R}$ oder $\mathbb{C}$ befassen.

### Warum DS für die Informatik?

Diskrete Mathematik liefert:

- Mathematische Modelle als Basis für **Datenstrukturen**
- Methoden für die **Laufzeitanalyse** von Algorithmen
- Grundlagen für **Kryptographie** (Zahlentheorie)
- Werkzeuge zur **Modellierung** von Netzwerken, Zuordnungen, etc.

---

## 2. Modellierung und Abstraktion

### Prinzip der Abstraktion

Ein reales Problem wird in ein abstraktes mathematisches Modell überführt. Dabei:

- bleiben alle für die Aufgabe **relevanten Informationen** erhalten
- fällt alles Irrelevante weg
- lassen sich entwickelte Algorithmen auf **andere Anwendungsfälle** übertragen

> **Aber:** Mathematische Modellierung ist nur sinnvoll, wenn die Lösungen **allgemeine Gültigkeit** haben. Daher: mathematische Beweise statt ausführliches Testen.

### Beispiel 1: Routenfinden als Graph

Eine Straßenkarte wird als Graph modelliert:

$$G := (V, E)$$

- $V = \{v_0, \ldots, v_k\}$: Knoten $\hat{=}$ Kreuzungen
- $E = \{\{v_0, v_{17}\}, \ldots\}$: Kanten $\hat{=}$ Straßen

Mit diesem Modell lassen sich Algorithmen zum Finden **kürzester Wege** entwickeln.

### Beispiel 2: Tutorienzuordnung als bipartiter Graph

Studierende sollen Tutorien zugeordnet werden. Modellierung als **bipartiter Graph**:

$$G := (V, E), \quad V := S \cup T$$

- $S$: Menge der Studierenden
- $T$: Menge der Tutorien
- Kante $\{s_i, t_j\} \in E$: Studierende $i$ kann in Tutorium $j$

Eine **Zuordnung** ist ein **Matching**: jeder Studierende bekommt genau einen Platz.

### Beispiel 3: Public-Key-Kryptographie

$$\text{Text} = \text{priv}(\text{pub}(\text{Text}))$$

- Absender verschlüsselt mit dem **öffentlichen Schlüssel** (pub)
- Empfänger entschlüsselt mit dem **privaten Schlüssel** (priv)
- Schlüssel sind invers, aber **nicht auseinander berechenbar**

Die mathematische Grundlage dafür ist die **Zahlentheorie** (RSA-System).

---

## 3. Kombinatorik

### Was ist Kombinatorik?

Kombinatorik behandelt das **Zählen** von Möglichkeiten: Auf wie viele Arten lassen sich Objekte anordnen, auswählen oder kombinieren?

**Wichtig für die Informatik:** Laufzeitabschätzungen von Algorithmen hängen oft direkt von solchen Zählproblemen ab.

### Definition (Unabhängige Menge)

Sei $G = (V, E)$ ein Graph. Eine Menge $X \subseteq V$ heißt **unabhängige Menge** (*independent set*), wenn gilt:

$$\boxed{\forall\, u, v \in X : \{u, v\} \notin E}$$

D.h. keine zwei Knoten in $X$ sind durch eine Kante verbunden.

### Algorithmus TM (Naiver Ansatz)

**Gegeben:** $G = (V,E)$ mit $n$ Knoten, $k \geq 1$  
**Problem:** Finde unabhängige Menge der Größe $k$
1. Für jede Teilmenge X ⊆ V teste:
    
2. Hat X die Größe k und gibt es kein u,v ∈ X mit {u,v} ∈ E?
    
3. Wenn ja: Gib X aus.
    
4. Wenn kein geeignetes X gefunden: Gib "nein" aus.


⚠️ **Laufzeit:** Die Schleife durchläuft **alle $2^n$ Teilmengen** → **Exponentialzeitalgorithmus**.

### Algorithmus kTM (Verbesserung)

Statt aller Teilmengen wird nur über **$k$-elementige Teilmengen** iteriert. Die Laufzeit ist im Wesentlichen die **Anzahl der $k$-elementigen Teilmengen** von $V$.

### Algorithmus rec-IS (Rekursiv)
rec-ind(G, k, i, X):

1. Falls (n-1)-i < k oder i ≥ n: gib "nein" zurück.
    
2. Falls k = 0:  
    2.1 Wenn X unabhängige Menge → gib X aus  
    2.2 Sonst → gib "nein" zurück
    
3. Rufe rekursiv rec-ind(G, k-1, i+1, X ∪ {vᵢ}) auf.  
    Wenn Rückgabe X' → gib X' aus.  
    Sonst → gib Ergebnis von rec-ind(G, k, i+1, X) zurück


Die Rekursionsgleichung für die Laufzeit lautet:

$$L(n, k) = L(n-1, k-1) + L(n-1, k)$$

---

## 4. Anzahl von Teilmengen

### Lemma (Potenzmenge)

Sei $n \in \mathbb{N}$. Jede Menge $M$ mit $n$ Elementen hat genau $2^n$ verschiedene Teilmengen.

$$\boxed{|\mathcal{P}(M)| = 2^n}$$

**Informelle Begründung:** Für jedes Element $a_i \in M$ gibt es zwei unabhängige Möglichkeiten: $a_i \in U$ oder $a_i \notin U$. Da alle Entscheidungen unabhängig sind, multiplizieren sie sich.

### Beweis (per vollständiger Induktion)

**Induktionsverankerung** $n = 0$:  
Sei $M = \emptyset$. Es gibt genau $2^0 = 1$ Teilmenge: $U = \emptyset$. ✓

**Induktionsannahme:**  
Die Behauptung gilt für alle Mengen der Größe $n$.

**Induktionsschritt** $n \to n+1$:  
Sei $M = \{a_1, \ldots, a_{n+1}\}$. Definiere $M^- := M \setminus \{a_{n+1}\}$.

Jede Teilmenge $U \subseteq M$ ist entweder:
- $U \subseteq M^-$ (enthält $a_{n+1}$ **nicht**), oder
- $U = U' \cup \{a_{n+1}\}$ mit $U' \subseteq M^-$ (enthält $a_{n+1}$)

Es gibt also **doppelt so viele** Teilmengen von $M$ wie von $M^-$.  
Nach IA gibt es $2^n$ Teilmengen von $M^-$, also $2^{n+1}$ Teilmengen von $M$. $\square$

### Definition (Potenzmenge)

$$\boxed{\mathcal{P}(M) := \{U : U \subseteq M\}}$$

Auch geschrieben als $2^M$.

---

## 5. Vollständige Induktion

### Aufbau eines Induktionsbeweises

Mit vollständiger Induktion beweist man Aussagen der Form $A(n)$ für alle $n \in \mathbb{N}$.

1. **Induktionsverankerung:** Zeige $A(0)$ (oder $A(n_0)$ für ein $n_0$).
2. **Induktionsannahme:** Nehme an, $A(n)$ gilt bereits.
3. **Induktionsschritt:** Zeige $A(n+1)$ unter Verwendung von $A(n)$.

### Varianten

- Verankerung bei $n_0 \neq 0$ möglich, wenn die Aussage erst ab $n_0$ gilt.
- **Starke Induktion:** Statt nur $A(n)$ kann man annehmen, dass $A(j)$ für **alle $j \leq n$** gilt.

### Häufige Fehler

⚠️ Die Induktion wird **nicht verankert**.  
⚠️ Die Induktionsannahme ist **falsch formuliert**.  
⚠️ Die Induktionsannahme wird im Schritt **nicht benutzt**.

---

## 📌 Zusammenfassung

### Wichtige Definitionen

| Begriff               | Definition                                                                                         |                |        |
| --------------------- | -------------------------------------------------------------------------------------------------- | -------------- | ------ |
| **Graph**             | $G = (V, E)$ mit Knotenmenge $V$ und Kantenmenge $E \subseteq \{\{a,b\} : a \neq b,\, a,b \in V\}$ |                |        |
| **Bipartiter Graph**  | $V = S \cup T$, Kanten nur zwischen $S$ und $T$                                                    |                |        |
| **Matching**          | Zuordnung, die jedem Knoten eindeutig einen Partner zuordnet                                       |                |        |
| **Unabhängige Menge** | $X \subseteq V$ mit $\forall u,v \in X: \{u,v\} \notin E$                                          |                |        |
| **Potenzmenge**       | $\mathcal{P}(M) = \{U : U \subseteq M\}$, es gilt $                                                | \mathcal{P}(M) | = 2^n$ |

### Kernaussagen

✅ Diskrete Strukturen = endliche/abzählbare Objekte als Basis der Informatik

✅ Graphen modellieren Routing, Zuordnung, Netzwerke — abstrakt und übertragbar

✅ Laufzeit von Algorithmen hängt direkt von kombinatorischen Zählproblemen ab

⚠️ Algorithmus TM ist korrekt, aber **exponentiell langsam** ($2^n$ Teilmengen)

✅ Vollständige Induktion: immer Verankerung + Annahme + Schritt

### Vorlesungsinhalt (Überblick)

| Thema | Inhalte |
|-------|---------|
| **Kombinatorik** | Urnenmodelle, Permutationen, Binomialsatz, Catalan-/Stirling-Zahlen |
| **Beweismethoden** | Vollständige Induktion (Varianten) |
| **Graphentheorie** | Bäume, Kreise, Euler-Touren, Flüsse, Menger, Matchings, Färbungen |
| **Zahlentheorie** | Modulare Arithmetik, Primzahlen, Euklidischer Algorithmus, RSA |
| **Algebraische Strukturen** | Äquivalenzrelationen, Ordnungen, Monoide |

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Kombinatorik - Bionmialkoeffizient]]: Urnenmodelle, Binomialkoeffizient
- [[VL.05 Graphentheorie]]: Formale Definition von Graphen, Bäume
- [[DS VL.X Zahlentheorie]]: Primzahlen, Euklidischer Algorithmus, RSA