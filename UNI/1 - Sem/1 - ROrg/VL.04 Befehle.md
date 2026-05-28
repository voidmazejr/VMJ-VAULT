**Class:** [[ROrg]]  
**Date:** 2025  
**Topics:** #MIPS #Assemblersprache #Befehle #Register #Speicheroperanden #Maschinencode #Prozeduren #Stack #Adressierung

---

## 🎯 Lernziele der Vorlesung

MIPS-Assemblersprache verstehen und Programme in Maschinencode übersetzen können.

- **C-Anweisungen** in MIPS-Assembler umsetzen
- **Programmierkonstrukte** implementieren: if, while, for, switch, Funktionen
- **MIPS-Registerkonventionen** befolgen
- **Stack (Stapel)** verstehen und nutzen
- **Assemblerprogramme** in Maschinensprache übersetzen und umgekehrt
- **Rekursive Funktionen** implementieren

---

## 1. Einführung in MIPS

### MIPS (Microprocessor without Interlocked Pipeline Stages)

**Definition:** Befehlssatzarchitektur entwickelt in den 1980er Jahren

**Verwendung:**
- NEC, Nintendo, Silicon Graphics, Sony
- Embedded Systems
- Akademische Lehre

### Befehle (Instructions)

$$\boxed{\text{Befehle} = \text{"Sprache" des Rechners}}$$

**Eigenschaften:**
- Viel primitiver als höhere Programmiersprachen
- Keine while-Schleifen oder if-Anweisungen direkt
- Sehr restriktiv: Viele MIPS-Befehle haben **genau 3 Operanden**

**Ziel der Architekten:**
- Hardware und Compiler einfach konstruierbar
- Leistung maximieren
- Kosten/Aufwand minimieren

---

## 2. Befehlskategorien

### Übersicht

**1. Arithmetische Befehle**
- Integer-Operationen
- Gleitpunkt-Operationen (Floating Point)

**2. Datentransfer-Befehle**
- Laden (Load)
- Speichern (Store)

**3. Kontrollbefehle**
- Sprung (Jump)
- Bedingte Verzweigungen (Conditional Branch)
- Prozedurunterstützung (Call & Return)

---

## 3. Arithmetische Befehle

### Grundprinzip

$$\boxed{\text{Die meisten Befehle haben genau 3 Operanden}}$$

**Operandenreihenfolge:** Zielregister zuerst

**Beispiel:**

```c
// C/Java:
A = B + C;

// MIPS:
add $s0, $s1, $s2    # $s0 = $s1 + $s2
```

### Entwurfsprinzip 1

$$\boxed{\text{Simplicity favors regularity (Einfachheit begünstigt Regelmäßigkeit)}}$$

**Begründung:**
- Hardware für feste Operandenzahl ist einfacher
- Variable Operandenzahl erhöht Komplexität

### Komplexere Ausdrücke

**C/Java:**

```c
a = b + c + d + e;
```

**MIPS:**

```assembly
add $t0, $t1, $t2    # a = b + c
add $t0, $t0, $t3    # a = a + d  
add $t0, $t0, $t4    # a = a + e
```

**Beispiel 2:**

```c
f = (g + h) - (i + j);
```

**MIPS:**

```assembly
add $t0, $s1, $s2    # $t0 = g + h
add $t1, $s3, $s4    # $t1 = i + j
sub $s0, $t0, $t1    # f = $t0 - $t1
```

---

## 4. MIPS-Register

### 32 Register (32 Bit breit)

**Entwurfsprinzip 2:**

$$\boxed{\text{Smaller is faster (Kleiner ist schneller)}}$$

**Begründung:**
- Mehr Register passen nicht ins Befehlsformat
- Große Anzahl von Registern → längere Taktzykluszeit

### Register-Übersicht

| Register | Nummer | Verwendung | Bei Aufruf beibehalten? |
|----------|--------|------------|-------------------------|
| `$zero` | 0 | Konstante 0 | — |
| `$at` | 1 | Assembler Temporary | Nein |
| `$v0-$v1` | 2-3 | Rückgabewerte | Nein |
| `$a0-$a3` | 4-7 | Argumente | Nein |
| `$t0-$t7` | 8-15 | Temporäre Variablen | Nein |
| `$s0-$s7` | 16-23 | Gesicherte Variablen | **Ja** |
| `$t8-$t9` | 24-25 | Weitere temporäre Var. | Nein |
| `$k0-$k1` | 26-27 | OS-reserviert | — |
| `$gp` | 28 | Global Pointer | Ja |
| `$sp` | 29 | Stack Pointer | Ja |
| `$fp` | 30 | Frame Pointer | Ja |
| `$ra` | 31 | Return Address | Ja |

**Wichtig:**
- `$zero` ist **immer 0**
- Ein Wort (word) in MIPS = 32 Bit = 4 Bytes

---

## 5. Speicheroperanden

### Speicherorganisation

**Hauptspeicher:** Großes Array von Bytes

```
Adresse | Inhalt (Byte)
--------|---------------
0       | 8 Datenbits
1       | 8 Datenbits
2       | 8 Datenbits
3       | 8 Datenbits
4       | 8 Datenbits
...     | ...
```

**Byte-Adressierung:** Adresse zeigt auf ein Byte

**Wort-Adressierung (32 Bit = 4 Bytes):**

```
Adresse | Inhalt (Wort)
--------|---------------
0       | 32 Datenbits (Bytes 0,1,2,3)
4       | 32 Datenbits (Bytes 4,5,6,7)
8       | 32 Datenbits (Bytes 8,9,10,11)
12      | 32 Datenbits
...     | ...
```

### Adresskalkulation für Arrays

**Adresse von `A[i]`:**

$$\boxed{\text{Adresse von } A[i] = \&A + i \times \text{Elementgröße}}$$

**Beispiele:**
- Byte-Array: `A[2]` → `A + 2`
- Wort-Array: `A[2]` → `A + 2×4 = A + 8`

### Datentransfer-Befehle

**Load Word (lw):**

```assembly
lw $t0, 12($s1)      # $t0 = Mem[$s1 + 12]
```

**Store Word (sw):**

```assembly
sw $t0, 12($s1)      # Mem[$s1 + 12] = $t0
```

- Konstante (hier 12) = **Offset**
- Bei `sw`: Zieladresse steht am Ende!

### Beispiel

**C/Java:**

```c
A[12] = A[8] + h;    // A: Array von Wörtern
```

**MIPS:**

```assembly
lw  $t0, 32($s2)     # $t0 = A[8]  (8×4=32)
add $t0, $t0, $s3    # $t0 = A[8] + h
sw  $t0, 48($s2)     # A[12] = $t0 (12×4=48)
```

- Basisadresse `A` in `$s2`
- Variable `h` in `$s3`

---

## 6. Ausrichtung und Byte-Reihenfolge

### Alignment Restriction

$$\boxed{\text{Wortadressen müssen Vielfache von 4 sein}}$$

**Konsequenz:** Die letzten 2 Bits einer Wortadresse sind **immer 00**

### Endianness (Byte-Reihenfolge)

**Beispiel:** Wert `0xaabbccdd` an Adresse 992

**Big-Endian (MIPS):**

| Adresse | 992 | 993 | 994 | 995 |
|---------|-----|-----|-----|-----|
| Inhalt  | 0xaa | 0xbb | 0xcc | 0xdd |

- MSB (Most Significant Byte) zuerst
- An kleinster Adresse

**Little-Endian (x86/IA32):**

| Adresse | 992 | 993 | 994 | 995 |
|---------|-----|-----|-----|-----|
| Inhalt  | 0xdd | 0xcc | 0xbb | 0xaa |

- LSB (Least Significant Byte) zuerst
- An kleinster Adresse

---

## 7. Konstanten (Immediate Operands)

### Add Immediate

**Entwurfsprinzip 3:**

$$\boxed{\text{Make the common case fast (Optimiere den häufigen Fall)}}$$

**MIPS-Befehl:**

```assembly
addi $s1, $s2, 4     # $s1 = $s2 + 4
```

**Warum kein `subi`?**

```assembly
addi $s1, $s2, -4    # Subtraktion durch negative Addition
```

**Vorteil:**
- Konstanten werden häufig verwendet
- Schneller als aus Speicher laden
- Weniger Befehle benötigt

---

## 8. Maschinensprache

### Von-Neumann-Konzept (Stored-Program Concept)

$$\boxed{\text{Befehle werden wie Daten dargestellt und im Speicher gehalten}}$$

**Erfindung von John von Neumann**

**Konsequenzen:**
- Befehle sind Zahlen (Bitfolgen)
- Programme im Hauptspeicher gespeichert
- Können gelesen/geschrieben werden wie Daten
- **Rechner ist "Metamaschine":** Durch Programmwechsel ändert sich die Maschine

### Befehlsformate

**MIPS-Befehle:**
- **Alle 32 Bit lang**
- **Nur 3 Formate:** R, I, J
- Operanden immer an gleicher Stelle

### R-Format (Register)

```
| op (6) | rs (5) | rt (5) | rd (5) | shamt (5) | funct (6) |
```

**Felder:**
- **op:** Opcode (Operationscode) - Basisoperation
- **rs:** Erstes Quellregister (source register)
- **rt:** Zweites Quellregister oder Zielregister (target register)
- **rd:** Zielregister (destination register)
- **shamt:** Shift amount (nur für Schiebebefehle)
- **funct:** Funktionscode (zusammen mit op bestimmt Operation)

**Beispiel:** `add $t0, $s1, $s2`

```
Dezimal: | 0  | 17 | 18 | 8  | 0  | 32 |
Binär:   |000000|10001|10010|01000|00000|100000|
```

- `$s1` = Register 17
- `$s2` = Register 18
- `$t0` = Register 8

⚠️ **Wichtig:** In Assembler steht Zielregister vorne, in Maschinensprache hinten!

### I-Format (Immediate)

```
| op (6) | rs (5) | rt (5) | Konstante/Adress-Offset (16) |
```

**Entwurfsprinzip 4:**

$\boxed{\text{Good design demands compromises (Guter Entwurf erfordert Kompromisse)}}$

**Verwendung:**
- Datentransfer-Befehle (lw, sw)
- Immediate-Operationen (addi)
- Bedingte Verzweigungen (beq, bne)

**Beispiel:** `lw $t0, 32($s2)`

```
Dezimal: | 35 | 18 | 8  | 32                |
Binär:   |100011|10010|01000|0000000000100000|
```

**16-Bit Offset:**
- Wertebereich: $-2^{15}$ bis $2^{15}-1$
- Bei lw/sw: Beliebiges Wort im Bereich ±32KB adressierbar

### J-Format (Jump)

```
| op (6) | 26-Bit Wortadresse |
```

**Verwendung:** Unbedingter Sprung (j)

**Beispiel:** `j 1000`

```
| 2 (000010) | 1000 |
```

---

## 9. Fetch-and-Execute-Zyklus

### Programmausführung

```c
while (true) {
    instr = Memory[PC];      // Befehl holen
    execute instr;           // Befehl ausführen
    PC = PC + 4;            // Zum nächsten Befehl
}
```

**Program Counter (PC):** Enthält Adresse des nächsten Befehls

**Standardfall:** PC erhöht sich um 4 (Wortgröße)

**Sprünge:** PC wird auf Zieladresse gesetzt

---

## 10. Logische Operationen

### Übersicht

| Operation | C/Java | MIPS-Befehl |
|-----------|--------|-------------|
| Linksschieben | `<<` | `sll` |
| Rechtsschieben | `>>` | `srl` |
| Bitweises UND | `&` | `and`, `andi` |
| Bitweises ODER | `\|` | `or`, `ori` |
| Bitweises NICHT | `~` | `nor` mit `$zero` |

### Shift Left Logical (sll)

**MIPS:**

```assembly
sll $t2, $s0, 4      # $t2 = $s0 << 4
```

**Beispiel:**

```
$s0 = 0000...0000 1001 = 9
$t2 = 0000...1001 0000 = 144 = 9×16
```

$\boxed{\text{Linksschieben um } i \text{ Bits} = \text{Multiplikation mit } 2^i}$

**Vorteil:** Schieben ist schneller als Multiplikation!

**Anwendung:** Array-Adressberechnung

```assembly
sll $t0, $a1, 2      # $t0 = 4×k (statt 2 add-Befehle)
add $t0, $a0, $t0    # $t0 = &v[k]
lw  $t1, 0($t0)      # $t1 = v[k]
```

### Bitweises UND (Maskieren)

**MIPS:**

```assembly
andi $t2, $s0, 15    # $t2 = $s0 & 15
```

**Beispiel:**

```
$s0 = 0000...1001 1001 = 153
 15 = 0000...0000 1111
     -----------------------
$t2 = 0000...0000 1001 = 9
```

**Anwendung:** Bits extrahieren (Maske erzwingt 0 an bestimmten Stellen)

### Bitweises ODER (Bits setzen)

**MIPS:**

```assembly
ori $t2, $s0, 15     # $t2 = $s0 | 15
```

**Beispiel:**

```
$s0 = 0000...1001 1001 = 153
 15 = 0000...0000 1111
     -----------------------
$t2 = 0000...1001 1111 = 159
```

### Bitweises NICHT (NOT)

**MIPS hat kein NOT, sondern NOR:**

```assembly
nor $t0, $s0, $zero  # $t0 = NOT $s0
```

**Begründung:**

$A \text{ NOR } 0 = \overline{A + 0} = \overline{A}$

---

## 11. 32-Bit Konstanten

### Load Upper Immediate (lui)

**Problem:** Immediate-Felder sind nur 16 Bit

**Lösung:** lui + ori

**Beispiel:** Lade $255 \times 2^{16} + 255 = 16\,711\,935$

```assembly
lui $t0, 255         # $t0 = 255 × 2^16
                     # $t0 = 0000 0000 1111 1111 0000 0000 0000 0000
ori $t0, $t0, 255    # $t0 = $t0 | 255
                     # $t0 = 0000 0000 1111 1111 0000 0000 1111 1111
```

### Vorzeichenerweiterung (Sign Extension)

**Regel:** MSB (Vorzeichenbit) wird kopiert

**Beispiel 4-Bit → 8-Bit:**

```
+2:  0010 → 0000 0010
-6:  1010 → 1111 1010
```

**In MIPS:**
- `addi`: Macht Vorzeichenerweiterung
- `andi`, `ori`: Keine Vorzeichenerweiterung (Zero-Extension)

---

## 12. Kontrollbefehle

### Bedingte Verzweigungen

**Branch if Equal:**

```assembly
beq $t0, $t1, label  # if ($t0 == $t1) goto label
```

**Branch if Not Equal:**

```assembly
bne $t0, $t1, label  # if ($t0 != $t1) goto label
```

### Unbedingter Sprung

**Jump:**

```assembly
j label              # goto label
```

### If-Then-Anweisung

**C/Java:**

```c
if (i == j)
    h = i + j;
```

**MIPS:**

```assembly
    bne $s0, $s1, endif  # if (i != j) goto endif
    add $s2, $s0, $s1    # h = i + j
endif:
```

**Trick:** Gegenteilige Bedingung effizienter zu testen!

### If-Then-Else-Anweisung

**C/Java:**

```c
if (i == j)
    f = g + h;
else
    f = g - h;
```

**MIPS:**

```assembly
    beq $s0, $s1, if     # if (i == j) goto if
    sub $s2, $s3, $s4    # f = g - h (else)
    j   endif
if:
    add $s2, $s3, $s4    # f = g + h (then)
endif:
```

### While-Schleife

**C/Java:**

```c
while (save[i] == k)
    i++;
```

**MIPS:**

```assembly
while:
    sll $t0, $s0, 2      # $t0 = 4×i
    add $t0, $s2, $t0    # $t0 = &save[i]
    lw  $t0, 0($t0)      # $t0 = save[i]
    bne $t0, $s1, endwhile  # if (save[i] != k) goto endwhile
    addi $s0, $s0, 1     # i++
    j   while
endwhile:
```

### For-Schleife

**C/Java:**

```c
sum = 0;
for (i = 0; i < n; i++)
    sum = sum + a[i];
```

**MIPS:**

```assembly
    add  $v0, $zero, $zero   # sum = 0
    add  $t0, $zero, $zero   # i = 0
for:
    bge  $t0, $a1, endfor    # if (i >= n) goto endfor
    sll  $t1, $t0, 2         # $t1 = 4×i
    add  $t1, $a0, $t1       # $t1 = &a[i]
    lw   $t1, 0($t1)         # $t1 = a[i]
    add  $v0, $v0, $t1       # sum = sum + a[i]
    addi $t0, $t0, 1         # i++
    j    for
endfor:
```

---

## 13. Vergleichsoperationen

### Set on Less Than

**MIPS:**

```assembly
slt  $t0, $s0, $s1   # $t0 = ($s0 < $s1) ? 1 : 0
slti $t0, $s0, 10    # $t0 = ($s0 < 10) ? 1 : 0
```

**Begründung:** Branch-on-less-than würde Taktzykluszeit verlängern

### Pseudo-Befehle

**Beispiel:** `ble` (branch on less or equal)

```assembly
ble $s1, $s2, label  # Pseudo-Befehl
```

**Wird übersetzt zu:**

```assembly
slt $at, $s2, $s1    # $at = ($s2 < $s1)
beq $at, $zero, label # if (!$at) goto label
```

**Register `$at` (assembler temporary):** Vom Assembler für solche Zwecke verwendet

### Vorzeichenbehaftete vs. Vorzeichenlose Vergleiche

**Vorzeichenbehaftet:** `slt`, `slti`

**Vorzeichenlos:** `sltu`, `sltiu`

**Beispiel:**

```
$s0 = 1111...1111 = -1 (signed), 2^32-1 (unsigned)
$s1 = 0000...0001 = 1 (signed und unsigned)

slt  $t0, $s0, $s1   # $t0 = 1  (-1 < 1 → wahr)
sltu $t1, $s0, $s1   # $t1 = 0  (2^32-1 > 1 → falsch)
```

---

## 14. Adressierung bei Verzweigungen

### PC-relative Adressierung (Branches)

**Befehlszähler (PC):** Enthält Adresse des aktuellen Befehls

$\boxed{\text{Zieladresse} = \text{PC} + 4 + 4 \times \text{Offset}}$

**I-Format:**

```
| op (6) | rs (5) | rt (5) | 16-Bit Offset |
```

**Beispiel:** `bne $t0, $s5, exit`

- PC = 80012 (Adresse des bne-Befehls)
- exit bei Adresse 80024
- Offset = (80024 - 80016) / 4 = 2

**Warum PC+4?** PC zeigt auf nächsten Befehl nach Fetch

**Vorteil:**
- Bedingte Verzweigungen meist zu nahen Befehlen
- 16 Bit reichen für ±32KB Bereich

### Pseudo-direkte Adressierung (Jumps)

**J-Format:**

```
| op (6) | 26-Bit Wortadresse |
```

$\boxed{\text{PC}_{\text{neu}} = \text{PC}_{31..28} \# (4 \times \text{Adresse})}$

**Beispiel:** `j 1000`

```
PC_neu = PC[31..28] # 4000
```

- # = Konkatenation
- 26 Bit × 4 = 28 Bit Adressbereich
- Obere 4 Bit von PC übernommen
- Adressgrenze: 256 MB (= $2^{28}$)

---

## 15. Prozeduren und Funktionen

### 6 Schritte beim Prozeduraufruf

1. **Parameter** an Stelle ablegen, auf die Prozedur zugreifen kann
2. **Programmsteuerung** an Prozedur übergeben
3. **Speicherressourcen** für Prozedur bereitstellen
4. **Prozedur** führt Aufgabe aus
5. **Ergebnis** an Stelle ablegen, auf die Aufrufer zugreifen kann
6. **Rücksprung** an Aufrufstelle

### Registerkonventionen

**Argumentregister:** `$a0-$a3` (4 Parameter)

**Rückgabewerte:** `$v0-$v1` (2 Werte)

**Rücksprungadresse:** `$ra`

### Jump-and-Link (jal)

```assembly
jal FunAddress       # $ra = PC+4; PC = FunAddress
```

**Speichert:** Rücksprungadresse in `$ra`

**Springt:** Zu FunAddress

### Jump-Register (jr)

```assembly
jr $ra               # PC = $ra
```

**Rücksprung:** Kopiert `$ra` in PC

### Beispiel: Blattfunktion

**C:**

```c
void swap(int v[], int k) {
    int tmp;
    tmp = v[k];
    v[k] = v[k+1];
    v[k+1] = tmp;
}
```

**MIPS:**

```assembly
swap:
    sll $t0, $a1, 2      # $t0 = 4×k
    add $t0, $a0, $t0    # $t0 = &v[k]
    lw  $t1, 0($t0)      # tmp = v[k]
    lw  $t2, 4($t0)      # $t2 = v[k+1]
    sw  $t2, 0($t0)      # v[k] = v[k+1]
    sw  $t1, 4($t0)      # v[k+1] = tmp
    jr  $ra              # return
```

**Caller:**

```assembly
jal swap
```

---

## 16. Stack (Keller/Stapel)

### Definition

$\boxed{\text{Stack} = \text{LIFO-Datenstruktur (Last-In-First-Out)}}$

**Operationen:**
- **push:** Element auf Stack legen
- **pop:** Element vom Stack entfernen

### In MIPS

- Stack wächst von **hohen zu niedrigen Adressen**
- **Stack Pointer (`$sp`):** Zeigt auf oberstes Element

### Register auf Stack ablegen

```assembly
addi $sp, $sp, -8    # Platz für 2 Wörter
sw   $s0, 4($sp)     # Speichere $s0
sw   $s1, 0($sp)     # Speichere $s1
```

### Register von Stack entfernen

```assembly
lw   $s1, 0($sp)     # Wiederherstellen $s1
lw   $s0, 4($sp)     # Wiederherstellen $s0
addi $sp, $sp, 8     # Stack Pointer zurücksetzen
```

---

## 17. Registerkonventionen

### Temporäre vs. Gesicherte Register

**`$t0-$t9`:** 10 temporäre Register
- Callee muss **nicht** sichern
- Caller muss vor Aufruf sichern, falls Wert benötigt

**`$s0-$s7`:** 8 gesicherte Register  
- Callee **muss** sichern, falls verwendet
- "Vertrag" zwischen Caller und Callee

### Regeln für Nicht-Blatt-Funktionen

1. Sichere `$ra` auf Stack
2. Variablen nach Aufruf benötigt → `$si`-Register + Stack
3. Variablen nach Aufruf nicht benötigt → `$ti`-Register
4. Argumente (`$ai`) nach Aufruf benötigt → in `$si` kopieren + Stack

### Beispiel: Nicht-Blatt-Funktion

**C:**

```c
int poly(int x) {
    return square(x) + x + 1;
}
```

**MIPS:**

```assembly
poly:
    addi $sp, $sp, -8    # Stack-Reservierung
    sw   $ra, 4($sp)     # Speichere $ra
    sw   $s0, 0($sp)     # Speichere $s0
    addi $s0, $a0, 0     # $s0 = x (retten!)
    jal  square          # $v0 = square(x)
    add  $v0, $v0, $s0   # $v0 = square(x) + x
    addi $v0, $v0, 1     # $v0 += 1
    lw   $ra, 4($sp)     # Wiederherstellen $ra
    lw   $s0, 0($sp)     # Wiederherstellen $s0
    addi $sp, $sp, 8     # Stack bereinigen
    jr   $ra             # return
```

---

## 18. Rekursive Funktionen

### Beispiel: Fakultät

**C:**

```c
int fact(int n) {
    if (n < 1) return 1;
    else return n * fact(n-1);
}
```

**MIPS:**

```assembly
fact:
    slti $t0, $a0, 1         # $t0 = (n < 1)
    beq  $t0, $zero, else    # if (n >= 1) goto else
    addi $v0, $zero, 1       # $v0 = 1
    jr   $ra                 # return
else:
    addi $sp, $sp, -8        # Stack-Reservierung
    sw   $ra, 4($sp)         # Speichere $ra
    sw   $a0, 0($sp)         # Speichere n
    addi $a0, $a0, -1        # $a0 = n-1
    jal  fact                # $v0 = fact(n-1)
    lw   $a0, 0($sp)         # Wiederherstellen n
    lw   $ra, 4($sp)         # Wiederherstellen $ra
    addi $sp, $sp, 8         # Stack bereinigen
    mul  $v0, $a0, $v0       # $v0 = n × fact(n-1)
    jr   $ra                 # return
```

**Wichtig:** Bei jedem rekursiven Aufruf werden `$ra` und `$a0` auf Stack gesichert!

---

## 19. MIPS-Speicheraufteilung

### Speicherlayout

```
0xffffffff ┌─────────────────┐
           │ Reserviert      │
0x7fffffff ├─────────────────┤ ← $sp (initial)
           │ Stack           │ ↓ wächst nach unten
           │       ↓         │
           │                 │
           │       ↑         │
           │ Heap (Dynamic)  │ ↑ wächst nach oben
           ├─────────────────┤ ← malloc/new
           │ Static Data     │ ← $gp
           ├─────────────────┤
0x00400000 │ Text (Code)     │
           ├─────────────────┤
0x00000000 │ Reserviert (OS) │
           └─────────────────┘
```

**Bereiche:**
- **Text:** Programmcode (ab 0x00400000)
- **Static Data:** Globale Variablen (mit $gp)
- **Heap:** Dynamische Daten (C: malloc, Java: new)
- **Stack:** Lokale Variablen, Rücksprungadressen (ab 0x7fffffff)

---

## 20. Zeichen und Zeichenfolgen

### ASCII

**ASCII:** American Standard Code for Information Interchange
- 8-Bit-Bytes (nur 7 Bit genutzt)
- `'a' - 'A' = 32` (für alle Buchstaben)

**Beispiele:**

| ASCII | Zeichen | ASCII | Zeichen |
|-------|---------|-------|---------|
| 32 | Leerzeichen | 64 | @ |
| 33 | ! | 65 | A |
| 34 | " | 97 | a |

### Load/Store Byte

```assembly
lb $t0, 0($gp)       # $t0 = Mem[$gp] (1 Byte, sign-extended)
sb $t0, 0($gp)       # Mem[$gp] = $t0 (1 Byte)
```

**C-String:** Mit Byte 0 (NULL) abgeschlossen

**Beispiel:** `"Abba"` = 65 98 98 97 0

### Zeichenfolge kopieren

**C:**

```c
void strcpy(char d[], char s[]) {
    int i = 0;
    while ((d[i] = s[i]) != '\0')
        i++;
}
```

**MIPS:**

```assembly
strcpy:
    add  $t0, $zero, $zero   # i = 0
strcpy_while:
    add  $t1, $a1, $t0       # $t1 = &s[i]
    lb   $t1, 0($t1)         # $t1 = s[i]
    add  $t2, $a0, $t0       # $t2 = &d[i]
    sb   $t1, 0($t2)         # d[i] = s[i]
    beq  $t1, $zero, strcpy_endwhile
    addi $t0, $t0, 1         # i++
    j    strcpy_while
strcpy_endwhile:
    jr   $ra
```

---

## 21. Multiplikation und Division

### Multiplikation

**Register:** Hi und Lo (je 32 Bit)
- **Hi:** 32 höchstwertigste Bits des 64-Bit Produkts
- **Lo:** 32 niederwertigste Bits

```assembly
mult $s2, $s3        # Hi#Lo = $s2 × $s3
mflo $s1             # $s1 = Lo
mfhi $s1             # $s1 = Hi
```

**Pseudo-Befehl:**

```assembly
mul $s1, $s2, $s3    # Wird übersetzt zu: mult + mflo
```

### Division

```assembly
div $s2, $s3         # Lo = Quotient, Hi = Rest
                     # Lo = $s2 / $s3
                     # Hi = $s2 % $s3
```

**Pseudo-Befehle:**

```assembly
div $s1, $s2, $s3    # $s1 = $s2 / $s3
rem $s1, $s2, $s3    # $s1 = $s2 % $s3
```

---

## 22. Overflow und Exceptions

### Overflow-Behandlung

**Befehle mit Overflow-Erkennung:**
- `add`, `addi`, `sub`

**Befehle ohne Overflow-Erkennung:**
- `addu`, `addiu`, `subu`, `mulu`, `divu`

⚠️ **Wichtig:** `addiu` und `sltiu` machen trotzdem Vorzeichenerweiterung!

### Exception Handling

**Bei Overflow:**
1. Exception (Interrupt) wird ausgelöst
2. Sprung zu vordefinierter Adresse
3. **Interrupt Handler** (Teil des OS) behandelt Exception
4. Register `$k0`, `$k1` für OS reserviert
5. Unterbrochene Adresse in **Exception Program Counter (`$epc`)** gespeichert

```assembly
mfc0 $k0, $epc       # Move from Coprocessor 0
```

---

## 📌 Zusammenfassung

### MIPS-Befehlsformate

**Alle 32 Bit lang, nur 3 Formate:**

**R-Format (Register):**

```
| op (6) | rs (5) | rt (5) | rd (5) | shamt (5) | funct (6) |
```

**I-Format (Immediate):**

```
| op (6) | rs (5) | rt (5) | 16-Bit Konstante/Offset |
```

**J-Format (Jump):**

```
| op (6) | 26-Bit Wortadresse |
```

### 4 Entwurfsprinzipien

1. **Simplicity favors regularity** (Einfachheit begünstigt Regelmäßigkeit)
2. **Smaller is faster** (Kleiner ist schneller)
3. **Make the common case fast** (Optimiere den häufigen Fall)
4. **Good design demands compromises** (Guter Entwurf erfordert Kompromisse)

### Wichtige Befehle

**Arithmetik:**
- `add $rd, $rs, $rt`
- `sub $rd, $rs, $rt`
- `addi $rt, $rs, imm`

**Datentransfer:**
- `lw $rt, offset($rs)`
- `sw $rt, offset($rs)`
- `lb $rt, offset($rs)`
- `sb $rt, offset($rs)`

**Logik:**
- `and $rd, $rs, $rt`
- `or $rd, $rs, $rt`
- `nor $rd, $rs, $rt`
- `sll $rd, $rt, shamt`

**Verzweigungen:**
- `beq $rs, $rt, label`
- `bne $rs, $rt, label`
- `slt $rd, $rs, $rt`

**Sprünge:**
- `j label`
- `jr $rs`
- `jal label`

### Registerkonventionen

| Register | Verwendung | Beibehalten? |
|----------|------------|--------------|
| `$zero` | Konstante 0 | — |
| `$v0-$v1` | Rückgabewerte | Nein |
| `$a0-$a3` | Argumente | Nein |
| `$t0-$t9` | Temporär | Nein |
| `$s0-$s7` | Gesichert | **Ja** |
| `$sp` | Stack Pointer | Ja |
| `$ra` | Return Address | Ja |

### Adressierungsarten

1. **Registeradressierung:** Operand in Register
2. **Basis/Displacement:** Adresse = Register + Konstante
3. **Direkte Adressierung:** Operand ist Konstante
4. **PC-relative:** Adresse = PC + 4 + 4×Offset
5. **Pseudo-direkte:** Adresse = PC[31:28] # (4×Adresse)

---

## 🔗 Verbindungen zu anderen Vorlesungen

- [[VL.01 Grundlegenden Ideen]]: ISA als Abstraktion
- [[VL.02 Zahlensysteme]]: 2-Komplement, Overflow
- [[VL.03 Grundlagen Digitalerentwurf]]: Register, ALU
- [[VL.05 Single Cycle]]: Implementierung der MIPS-Befehle