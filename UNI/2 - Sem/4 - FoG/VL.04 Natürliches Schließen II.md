**Class:** [[FoG - Formal-mathematische Grundlagen]]  
**Date:** 05-05-2026 -> 12-05-2026
**Topics:** #NatürlichesSchließen #Prädikatenlogik #Quantoren #Substitution #FoG
**Link:** [[VL.04 FoG Skript-28-30.pdf]]

---

## 🎯 Lernziele der Vorlesung

Dieser Abschnitt erweitert das Natürliche Schließen auf die **Prädikatenlogik** und führt die Beweisregeln für Universal- und Existenzquantoren ein.

- **Substitution**: Freie Variablen in Formeln durch konkrete Terme ersetzen
- **OK-Bedingung**: Sicherstellen, dass Substitutionen keine ungewollten Variablenbindungen erzeugen
- **∀-Einführung / -Elimination**: Regeln für den Allquantor
- **∃-Einführung / -Elimination**: Regeln für den Existenzquantor
- **Vorwärts- vs. Rückwärtsbeweise**: Richtung der Regelanwendung im Sequenzkontext

---

## 1. Erweiterungen für die Prädikatenlogik (§5.1)

### 1.1 Motivation

Die Regeln des Natürlichen Schließens für die Prädikatenlogik erfordern im Umgang mit Quantoren eine präzise Klärung, wie man **gebundene Termvariablen** nach Auflösung der Quantoren durch konkrete Terme ersetzen kann – ohne versehentlich neue Bindungen einzuführen.

> 💡 **Merkhilfe:** „Auflösen eines Quantors" = Quantor entfernen und Variable durch einen Term ersetzen. Das Werkzeug dafür heißt **Substitution**.

---

### 1.2 Definition: Substitution (§5.1.1)

Sei $\sigma$ eine Signatur, $X$ eine Menge von Termvariablen.  
Seien $x \in X$, $\varphi \in \mathbf{P}_\sigma(X)$ und $t \in T_\sigma$.

$$\boxed{\varphi\!\left[\tfrac{t}{x}\right] \text{ bezeichnet die Formel, die durch Ersetzen aller \textit{freien} Vorkommen von } x \text{ in } \varphi \text{ durch } t \text{ entsteht.}}$$

**Kurzschreibweise:** $\varphi(t)$ für das Ergebnis der Substitution $\varphi(x)\!\left[\tfrac{t}{x}\right]$.

⚠️ **Achtung:** Enthält der Term $t$ eine Variable $z$, zu der es in $\varphi$ eine Teilformel $(Qz.\psi)$ gibt, so muss $\varphi$ **vor** der Substitution durch eine $\alpha$-gleiche Variante ersetzt werden, um versehentliche neue Bindungen zu vermeiden.

---

### 1.3 Definition: OK-Bedingung (§5.1.2)

Sei $\sigma$ eine Signatur, $X$ eine Menge von Termvariablen.  
Seien $x \in X$, $\varphi \in \mathbf{P}_\sigma(X)$, $t \in T_\sigma$, $Q \in \{\forall, \exists\}$.  
Sei $\text{var}(t)$ die Menge der in $t$ vorkommenden Variablen.

$$\boxed{\text{OK}(t, x, \varphi) \iff \text{es gibt kein freies Vorkommen von } x \text{ in } \varphi, \text{ das im Scope eines } Qy \text{ für } y \in \text{var}(t) \text{ liegt.}}$$

**Bedeutung:** Wenn $\text{OK}(t, x, \varphi)$ gilt, ist keine $\alpha$-Konversion nötig — die Substitution $\varphi\!\left[\tfrac{t}{x}\right]$ ist direkt „sicher" durchführbar.

**Beispiel:**

| Formel $\varphi$ | Term $t$ | Variable $x$ | OK? | Grund |
|---|---|---|---|---|
| $\forall y.\, x = y$ | $y$ | $x$ | ❌ | $y \in \text{var}(t)$, aber $x$ liegt im Scope von $\forall y$ |
| $\forall z.\, x = 0$ | $y$ | $x$ | ✅ | $y \notin \text{var}(\forall z.\ldots)$ als Problem |
| $P(x) \land Q(x)$ | $f(a)$ | $x$ | ✅ | Kein Quantor über Variablen aus $t$ |

---

### 1.4 Erweiterung des Sequenzbegriffs

Der Sequenzbegriff aus §4.1 wird erweitert: Neben Formel-Annahmen erlauben wir nun die **explizite Nennung von Termvariablen** in $\Phi$.

Die bisherige Kontextregel:

$$\frac{\Phi \Rightarrow \psi \;\leadsto\; \Phi' \Rightarrow \psi'}{\Gamma,\, \Phi \Rightarrow \psi \;\leadsto\; \Gamma,\, \Phi' \Rightarrow \psi'}$$

gilt jetzt **nur noch** unter der Einschränkung, dass eine in $\Phi$ gelistete Variable **nicht** in den Formeln von $\Gamma$ frei vorkommen darf.

> 💡 **Rolle:** Dies verhindert, dass eine „frische" Variable $x_0$ aus einem lokalen Beweis mit dem globalen Kontext kollidiert.

---

## 2. Universelle Quantifikation ($\forall$) (§5.2)

### 2.1 Eliminationsregel (∀E)

**Idee:** Gilt $\forall x.\,\varphi$, dann gilt $\varphi$ insbesondere für jeden konkreten Term $t$.

$$\boxed{(\forall\text{E})\;\frac{\forall x.\,\varphi}{\varphi\!\left[\tfrac{t}{x}\right]} \quad t \in T_\sigma,\; \text{OK}(t, x, \varphi)}$$

**Rolle der Nebenbedingung:** $\text{OK}(t, x, \varphi)$ stellt sicher, dass keine versehentlichen neuen Bindungen entstehen.

**Vorwärtsbeweisschritt** (aus der Annahme $\forall x.\,\varphi$ gewinnt man $\varphi\!\left[\tfrac{t}{x}\right]$):

```

{{ ∀x.φ }} ⟹ ψ ~~> {{ ∀x.φ, φ[t/x] }} ⟹ ψ

```

> 💡 **Merkhilfe:** $\forall$E ist wie das Projizieren bei $\land$E — man „entnimmt" eine Instanz aus der Allaussage.

---

### 2.2 Einführungsregel (∀I)

**Idee:** Um $\forall x.\,\varphi$ zu zeigen, nimmt man eine **beliebige, frische** Variable $x_0$ an und beweist $\varphi\!\left[\tfrac{x_0}{x}\right]$ für diese stellvertretende Variable.

$$\boxed{(\forall\text{I})\;\frac{\{\!\{x_0\}\!\} \;\overset{!}{\Rightarrow}\; \varphi\!\left[\tfrac{x_0}{x}\right]}{\forall x.\,\varphi} \quad x_0 \in X}$$

**Bedingung:** $x_0$ muss **frisch** sein — es darf nicht in den Formeln weiterer Annahmen außerhalb dieses lokalen Beweises frei vorkommen.

**Rückwärtsbeweisschritt:**

```

{{}} ⟹ ∀x.φ ~~> {{x₀}} ⟹ φ[x₀/x]

```

**Schritt-für-Schritt Beispiel** (Beweis von $\forall n \in \mathbb{N}.\; n + 0 = n$):

```

Beweisziel: {{}} ⟹ ∀n. n + 0 = n

Schritt 1 (∀I anwenden): {{n₀}} ⟹ n₀ + 0 = n₀

Schritt 2: Zeige n₀ + 0 = n₀ durch Rechenregeln/Induktion.

✅ Da n₀ beliebig (frisch) war, gilt ∀n. n + 0 = n.

```

> 💡 **Natürlichsprachliche Formulierung:** „Sei $x_0$ (beliebig, aber fest)." — man weiß von $x_0$ **nichts** außer seiner Existenz als Variable.

⚠️ **Häufiger Fehler:** $x_0$ nicht frisch wählen, sodass es in Γ vorkommt → Beweis ungültig!

---

## 3. Existentielle Quantifikation ($\exists$) (§5.3)

### 3.1 Einführungsregel (∃I)

**Idee:** Um $\exists x.\,\varphi$ zu zeigen, genügt es, **einen konkreten Zeugen** $t$ zu finden, für den $\varphi\!\left[\tfrac{t}{x}\right]$ gilt.

$$\boxed{(\exists\text{I})\;\frac{\varphi\!\left[\tfrac{t}{x}\right]}{\exists x.\,\varphi} \quad t \in T_\sigma,\; \text{OK}(t, x, \varphi)}$$

**Rückwärtsbeweisschritt:**

```

{{}} ⟹ ∃x.φ ~~> {{}} ⟹ φ[t/x]

```

> 💡 **Natürlichsprachliche Formulierung:** „Wähle $x = t$." – dann reicht es, $\varphi(t)$ nachzuweisen.

**Schritt-für-Schritt Beispiel** (Beweis von $\exists k \in \mathbb{N}.\; 4 = 2k$):

```

Beweisziel: {{}} ⟹ ∃k. 4 = 2k

Schritt 1 (∃I, Zeuge t = 2): {{}} ⟹ 4 = 2·2

Schritt 2: 4 = 4 ✅ (durch Rechnen)

✅ Mit Zeuge k = 2 gilt ∃k. 4 = 2k.

```

> 💡 **Merkhilfe:** $\exists$I ist wie $\lor$I — es reicht eine Alternative (ein Zeuge) zu finden.

---

### 3.2 Eliminationsregel (∃E)

**Idee:** Hat man $\exists x.\,\varphi$, weiß man nur, dass **irgendein** $x$ mit der Eigenschaft $\varphi$ existiert — aber nicht welches. Man führt daher einen **abstrakten Stellvertreterbeweis**: Annahme eines frischen $x_0$ mit $\varphi\!\left[\tfrac{x_0}{x}\right]$, um das Ziel $\psi$ zu zeigen.

$$\boxed{(\exists\text{E})\;\frac{\exists x.\,\varphi \qquad \{\!\{x_0,\, \varphi\!\left[\tfrac{x_0}{x}\right]\}\!\} \;\overset{!}{\Rightarrow}\; \psi}{\psi}}$$

**Vorwärtsbeweisschritt** (mit Ziel $\psi$ als „Richtschnur"):

```

{{ ∃x.φ }} ⟹ ψ ~~> {{ ∃x.φ, x₀, φ[x₀/x] }} ⟹ ψ

```

> 💡 **Natürlichsprachliche Formulierung:** „Sei nun $x_0$ dieses $x$, von dem wir annehmen dürfen, dass $\varphi\!\left[\tfrac{x_0}{x}\right]$ gilt."

⚠️ **Achtung:** $x_0$ muss **frisch** sein. Man darf $x_0$ **nicht** mit einem bereits bekannten konkreten Wert identifizieren — wir wissen nur, dass es existiert, nicht wer es ist.

❌ **Falsch:** $\exists$E anwenden und $x_0$ dabei mit einer konkreten Konstanten aus dem Kontext gleichsetzen.

**Schritt-für-Schritt Beispiel** (Aus $\exists k.\, n = 2k$ folgt $\exists k.\, n^2 = 2k$, für gerades $n$):

```

Annahme: ∃k. n = 2k

Schritt 1 (∃E anwenden, x₀ = k₀): Annahme: k₀ frisch, n = 2k₀

Schritt 2: n² = (2k₀)² = 4k₀² = 2·(2k₀²)

Schritt 3 (∃I mit Zeuge 2k₀²): ∃k. n² = 2k ✅

```

---

## 4. Vergleich aller Quantoren-Regeln

| Regel | Form | Richtung | Analogie |
|---|---|---|---|
| $(\forall\text{E})$ | $\forall x.\varphi \;\vdash\; \varphi[t/x]$ | Vorwärts | $\land$E (Projektion) |
| $(\forall\text{I})$ | $\{x_0\} \vdash \varphi[x_0/x] \;\Rightarrow\; \forall x.\varphi$ | Rückwärts | $\land$I (beide zeigen) |
| $(\exists\text{I})$ | $\varphi[t/x] \;\vdash\; \exists x.\varphi$ | Rückwärts | $\lor$I (eine Alternative) |
| $(\exists\text{E})$ | $\exists x.\varphi,\; \{x_0, \varphi[x_0/x]\} \vdash \psi \;\Rightarrow\; \psi$ | Vorwärts (+Ziel) | $\lor$E (Fallunterscheidung) |

---

## 5. Gesamtstruktur: Natürliches Schließen — Regelübersicht

```

KONJUNKTION IMPLIKATION DISJUNKTION ∧E₁, ∧E₂, ∧I →E (Modus Ponens) ∨I₁, ∨I₂, ∨E →I

PRÄDIKATENLOGIK ∀E (Elimination) ∃I (Einführung) ∀I (Einführung) ∃E (Elimination)

NEGATION (§6) ¬E, ¬I

```

> 💡 **Merkhilfe Symmetrie:**  
> - $\forall$ verhält sich wie $\land$ (viele Fälle → nimm einen heraus / zeige alle)  
> - $\exists$ verhält sich wie $\lor$ (einer reicht → finde einen / analysiere alle Fälle)

---

## 📌 Zusammenfassung

### Wichtige Konzepte

| Konzept | Bedeutung |
|---|---|
| **Substitution** $\varphi[t/x]$ | Ersetze alle freien Vorkommen von $x$ in $\varphi$ durch $t$ |
| **OK$(t, x, \varphi)$** | Keine versehentliche neue Bindung bei Substitution |
| **$\alpha$-Konversion** | Umbenennung gebundener Variablen, um OK herzustellen |
| **Zeuge** | Der konkrete Term $t$ bei $\exists$I |
| **Frische Variable $x_0$** | Beliebige, unbekannte Variable bei $\forall$I und $\exists$E |
| **Vorwärtsbeweis** | Neue Annahmen aus bestehenden gewinnen |
| **Rückwärtsbeweis** | Beweisziel in einfachere Teilziele zerlegen |

### Kernaussagen

✅ **∀E** – Aus $\forall x.\varphi$ darf man $\varphi[t/x]$ für jeden erlaubten Term $t$ ableiten (Vorwärts)  
✅ **∀I** – $\forall x.\varphi$ zeigt man mit einer frischen Variablen $x_0$ stellvertretend (Rückwärts)  
✅ **∃I** – $\exists x.\varphi$ zeigt man durch Angabe eines konkreten Zeugen $t$ (Rückwärts)  
✅ **∃E** – Aus $\exists x.\varphi$ gewinnt man eine abstrakte Annahme mit frischem $x_0$ (Vorwärts+Ziel)  
⚠️ **Achtung:** $x_0$ bei $\forall$I und $\exists$E muss immer **frisch** sein — keine Kollision mit dem Kontext $\Gamma$  
❌ **Falsch:** OK-Bedingung ignorieren → führt zu falschen Substitutionen mit ungewollten Bindungen

### Wichtige Formeln

| Regel | Formel |
|---|---|
| **∀E** | $\dfrac{\forall x.\,\varphi}{\varphi[t/x]}$ mit $\text{OK}(t,x,\varphi)$ |
| **∀I** | $\dfrac{\{x_0\} \overset{!}{\Rightarrow} \varphi[x_0/x]}{\forall x.\,\varphi}$ mit $x_0 \in X$ frisch |
| **∃I** | $\dfrac{\varphi[t/x]}{\exists x.\,\varphi}$ mit $\text{OK}(t,x,\varphi)$ |
| **∃E** | $\dfrac{\exists x.\,\varphi \quad \{x_0,\,\varphi[x_0/x]\} \overset{!}{\Rightarrow} \psi}{\psi}$ |

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Inferenz und Regelschemata]]: Regelschemas, Pattern Matching, Ableitungsbäume Definition von $T_\sigma(X)$, $\mathbf{P}_\sigma(X)$, Substitution, $\alpha$-Konversion
- [[VL.03 Argumentieren]]: ∧, →, ∨ — Grundregeln, auf denen §5 aufbaut
