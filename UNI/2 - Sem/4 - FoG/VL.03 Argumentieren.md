**Class:** [[FoG - Formal-mathematische Grundlagen]]
**Date:** 28-04-2026
**Topics:** #Formalisierung #Beweistechniken #Kontraposition #Widerspruchsbeweis #NatürlichesSchließen #Sequenzen #Konjunktion #Implikation #Disjunktion #TU-Berlin #FoG
**Link:** [[VL.03 Skript-20-27.pdf]]

---

## 🎯 Lernziele der Vorlesung

VL.03 (Teil II) überführt natürlichsprachliche Aussagen in formale PL-Formeln und führt die drei klassischen Beweistechniken ein – zunächst informell, dann als Sequenzenkalkül.

- **Formalisierung**: Natürlichsprachliche Aussagen in AL/PL-Formeln übersetzen
- **Kontraposition**: $(A \to B) \equiv (\neg B \to \neg A)$ als Beweistechnik verstehen und anwenden
- **Widerspruchsbeweis**: $\neg B \equiv (B \to \bot)$ – Negation annehmen, Widerspruch herleiten
- **Grade der Formalität**: Unterschied zwischen meta-erklärender und formal hingeschriebener Beweisebene
- **Sequenzen**: Formale Beweisverpflichtungen $\Phi \Longrightarrow \psi$ als Grundstruktur des Natürlichen Schließens
- **Beweisregeln §4**: Einführungs- (I) und Eliminationsregeln (E) für $\wedge$, $\to$, $\vee$

---

## 1. Formalisierung natürlichsprachlicher Aussagen (§3.1)

### Beispiele: Aussagen → PL-Formeln

| Natürliche Sprache | Formalisierung |
|---|---|
| „Wenn es regnet und die Sonne scheint nicht, gehe ich nicht aus dem Haus." | $r \wedge \neg s \to \neg a$ |
| „Für alle $n \in \mathbb{N}$: $n^2$ gerade $\Rightarrow$ $n$ gerade." | $\forall n \in \mathbb{N}.\;(\exists k \in \mathbb{N}.\;n^2=2k) \to (\exists m \in \mathbb{N}.\;n=2m)$ |
| „$\sqrt{2}$ ist irrational." | $\neg\!\left(\exists m \in \mathbb{Z},\, n \in \mathbb{Z}\setminus\{0\}.\;\sqrt{2}=\tfrac{m}{n}\right)$ |
| „Für alle Primzahlen $p > 4$: $p^2-1$ durch $24$ teilbar." | $\forall p \in \mathbb{N}.\;\mathrm{Prim}(p) \to (p>4) \to (\exists k \in \mathbb{N}.\;p^2-1=24k)$ |

> 💡 **Merkhilfe:** „Für alle …" → $\forall$ mit $\to$ | „Es gibt …" → $\exists$ mit $\wedge$
> ❌ **Falsch:** $\forall x \in A.\,\varphi$ mit $\forall x.\, x \in A \wedge \varphi$ – beim $\forall$ steht $\to$, nicht $\wedge$!

---

## 2. Beweistechniken (§3.2)

### Überblick

| Technik | Logische Basis | Vorgehen |
|---|---|---|
| **Direkter Beweis** | $A,\; A \to B \;\vdash\; B$ | Modus Ponens – direkt folgern |
| **Kontraposition** | $(A \to B) \equiv (\neg B \to \neg A)$ | $\neg B$ annehmen, $\neg A$ beweisen |
| **Widerspruch** | $\neg B \equiv (B \to \bot)$ | $B$ annehmen, $\bot$ herleiten |

---

### Technik 1: Direkter Beweis

$$\boxed{\frac{A \quad A \to B}{B} \quad \text{(Modus Ponens)}}$$

> 💡 **Rolle:** Wenn $A$ wahr ist und $A \Rightarrow B$ gilt, folgt direkt $B$.

---

### Technik 2: Kontraposition – Vollständiger Beweis

$$\boxed{(A \to B) \;\equiv\; (\neg B \to \neg A)}$$

**Satz:** $\forall n \in \mathbb{N}.\; n^2 \text{ gerade} \Rightarrow n \text{ gerade}$

Zeige äquivalent: $n \text{ ungerade} \Rightarrow n^2 \text{ ungerade}$

$$\forall n \in \mathbb{N}.\;(\exists m \in \mathbb{N}.\;n=2m+1) \to (\exists k \in \mathbb{N}.\;n^2=2k+1)$$

**Beweis:**

1. *[∀-Beweis]* Sei $n \in \mathbb{N}$ beliebig, aber fest.
2. *[→-Beweis]* Nehme an: $\exists m \in \mathbb{N}.\; n = 2m+1$. Arbeite abstrakt mit $m$ weiter.
3. *[∃-Beweis]* Wähle $k \triangleq 2m^2 + 2m$. *(kreative Wahl!)*
4. Rechnung:

$$n^2 \overset{(2)}{=} (2m+1)^2 \overset{\text{Sch.}}{=} 4m^2+4m+1 \overset{\text{Sch.}}{=} 2(2m^2+2m)+1 \overset{(3)}{=} 2k+1 \quad \blacksquare$$

---

### Technik 3: Widerspruch – Vollständiger Beweis

$$\boxed{A \;\equiv\; (\neg A \to \bot)} \qquad \boxed{\neg B \;\equiv\; (B \to \bot)}$$

**Satz:** $\sqrt{2}$ ist irrational.

**Beweis:**

1. Zeige: $\left(\exists m \in \mathbb{Z},\, n \in \mathbb{Z}\setminus\{0\}.\;\sqrt{2}=\tfrac{m}{n}\right) \to \bot$
2. **Annahme:** Es gibt $m, n$ mit $\sqrt{2} = \tfrac{m}{n}$. *(nur Existenz bekannt!)*
3. **O.B.d.A.:** $\tfrac{m}{n}$ vollständig gekürzt.
4. $m = \sqrt{2}\cdot n$ → Quadrieren: $m^2 = 2n^2$ → $m^2$ gerade → $m$ gerade → $m = 2k$.
5. *(Abstrakt mit $k$ weiter – nur Existenz bekannt!)*
6. $2n^2 = (2k)^2 = 4k^2 = 2(2k^2)$ → $n^2 = 2k^2$ → $n$ gerade.
7. **Widerspruch:** $m$ und $n$ gerade → $\tfrac{m}{n}$ nicht gekürzt. Widerspricht (3). $\bot \quad \blacksquare$

```

Flussdiagramm: Annahme: √2 = m/n (vollständig gekürzt, O.B.d.A.) ↓ m² = 2n² → m gerade → m = 2k ↓ n² = 2k² → n gerade ↓ m, n gerade → m/n nicht gekürzt → ⊥ ✅

```

> ⚠️ **O.B.d.A.** ist keine freie Annahme – jeder Bruch lässt sich kürzen, daher darf man zum gekürzten Vertreter übergehen.

---

## 3. Grade der Formalität (§3.3)

| Ebene | Schreibweise | Inhalt |
|---|---|---|
| **Meta-Erklärung** | *kursiv* | Was logisch passiert: ∀ auflösen, → annehmen, ∃ konstruieren |
| **Formaler Beweis** | Normalschrift | Was tatsächlich hingeschrieben wird |

> 💡 In der Praxis schreibt man nur die Normalschrift – die kursiven Schritte entsprechen exakt den Beweisregeln des Natürlichen Schließens (§4).

---

## 4. Sequenzen (§4.1)

$$\boxed{\Phi \Longrightarrow \psi}$$

- $\Phi = \{\!\{\varphi_1, \ldots, \varphi_n\}\!\}$: endliche Multimenge → **Beweisannahmen**
- $\psi$: einzelne Formel → **Beweisziel**

| Symbol | Zustand | Bedeutung |
|---|---|---|
| $\Phi \overset{?}{\Longrightarrow} \psi$ | Offen | Beweisverpflichtung ungelöst |
| $\Phi \overset{\checkmark}{\Longrightarrow} \psi$ | Erfüllt | $\psi \in \Phi$ |
| $\Phi \overset{!}{\Longrightarrow} \psi$ | Beweisbar | Durch Regeln auf Erfülltes reduzierbar |

> 💡 **Beweiszustand** = Menge aller noch offenen Verpflichtungen. Beweis fertig ↔ keine offenen Verpflichtungen mehr.

---

## 5. Beweisregeln ∧, →, ∨ (§4.2–4.5)

### Notation & Monotonie

Beweisschritt: $\Phi \Longrightarrow \psi \;\leadsto\; \Phi' \Longrightarrow \psi'$

Für Wolke $\Gamma$:

$$\frac{\Phi \Longrightarrow \psi \;\leadsto\; \Phi' \Longrightarrow \psi'}{\Gamma,\,\Phi \Longrightarrow \psi \;\leadsto\; \Gamma,\,\Phi' \Longrightarrow \psi'}$$

> 💡 **Dual-Prinzip:** I-Regeln erzeugen Operator im Ziel (Rückwärts) | E-Regeln zerlegen Operator aus Annahme (Vorwärts)

---

### Konjunktion ∧ (§4.3)

$$\boxed{(\wedge E_1)\;\frac{A \wedge B}{A}} \qquad \boxed{(\wedge E_2)\;\frac{A \wedge B}{B}} \qquad \boxed{(\wedge I)\;\frac{A \quad B}{A \wedge B}}$$

```

E (Vorwärts): {A ∧ B} ⟹ C ~~> {A ∧ B, A} ⟹ C (∧E₁) I (Rückwärts): {} ⟹ A ∧ B ~~> {} ⟹ A und {} ⟹ B

```

---

### Implikation → (§4.4)

$$\boxed{(\to E)\;\frac{A \quad A \to B}{B}} \qquad \boxed{(\to I)\;\frac{A \overset{!}{\Longrightarrow} B}{A \to B}}$$

```

E (Vorwärts): {A, A→B} ⟹ C ~~> {A, A→B, B} ⟹ C I (Rückwärts): {} ⟹ A→B ~~> {A} ⟹ B

```

> 💡 $(\to I)$ = „Nehme $A$ an, zeige $B$."

---

### Disjunktion ∨ (§4.5)

$$\boxed{(\vee I_1)\;\frac{A}{A \vee B}} \qquad \boxed{(\vee I_2)\;\frac{B}{A \vee B}} \qquad \boxed{(\vee E)\;\frac{A \vee B \quad A \overset{!}{\Longrightarrow} C \quad B \overset{!}{\Longrightarrow} C}{C}}$$

```

I (Rückwärts): {} ⟹ A∨B ~~> {} ⟹ A oder {} ⟹ B E (Vorwärts): {A∨B} ⟹ C ~~> {A∨B,A} ⟹ C und {A∨B,B} ⟹ C

```

> ⚠️ $(\vee E)$ ist **zielabhängig** – $C$ muss vor der Fallunterscheidung feststehen!

---

## 📌 Zusammenfassung

### Wichtige Konzepte

| Konzept | Bedeutung |
|---|---|
| **Kontraposition** | $(A \to B) \equiv (\neg B \to \neg A)$ |
| **Widerspruch** | $\neg B \equiv (B \to \bot)$ |
| **O.B.d.A.** | Zulässige Vereinfachung; muss begründet sein |
| **Sequenz** | $\Phi \Longrightarrow \psi$: Annahmen + Ziel |
| **E-Regeln** | Operator aus Annahme zerlegen → Vorwärts |
| **I-Regeln** | Operator im Ziel erzeugen → Rückwärts |

### Alle Beweisregeln

| Regel | Schema | Richtung |
|---|---|---|
| $(\wedge E_1)$ | $A \wedge B \vdash A$ | Vorwärts |
| $(\wedge E_2)$ | $A \wedge B \vdash B$ | Vorwärts |
| $(\wedge I)$ | $A,\;B \vdash A \wedge B$ | Rückwärts |
| $(\to E)$ | $A,\;A \to B \vdash B$ | Vorwärts |
| $(\to I)$ | $\{A\} \overset{!}{\Longrightarrow} B \;\vdash\; A \to B$ | Rückwärts |
| $(\vee I_1)$ | $A \vdash A \vee B$ | Rückwärts |
| $(\vee I_2)$ | $B \vdash A \vee B$ | Rückwärts |
| $(\vee E)$ | $A \vee B,\;A{\overset{!}{\Longrightarrow}}C,\;B{\overset{!}{\Longrightarrow}}C \;\vdash\; C$ | Vorwärts + zielabh. |

### Kernaussagen

✅ **E-Regeln** gewinnen neue Annahmen (Vorwärts)  
✅ **I-Regeln** zerlegen Beweisziele (Rückwärts)  
✅ Kontraposition ↔ direkter Beweis logisch äquivalent  
✅ ∀-Beweis: fixiere beliebiges Element | ∃-Beweis: konstruiere konkreten Zeugen  
⚠️ $(\vee E)$ zielabhängig – $C$ muss feststehen  
⚠️ O.B.d.A. muss begründet werden  
❌ **Falsch:** E erzeugt Operator; I zerlegt Annahmen – genau umgekehrt!

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.02 Inferenz und Regelschemata]]: Regelnotation, Ableitungsbäume – Basis für §4
- [[VL.04 Natürliches Schließen II]]: Regeln für $=$, $\forall$, $\exists$
- [[VL.06-FoG – Natürliches Schließen III]]: Negation, AL-Semantik, logische Äquivalenz
