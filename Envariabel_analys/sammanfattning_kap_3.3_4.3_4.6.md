# 📐 Kapitel 3.3, 4.3 & 4.6 — Implicit derivering, Optimering & Konvexa funktioner

## Omfattande sammanfattning och genomgång

*Baserad på kursboken och föreläsning 15 (Kap 3.3, 4.3, 4.6)*

---

# 🔷 FRÅN KAPITEL 3.3 — Implicit derivering (kortfattat)

*Kapitel 3.3 behandlas mer utförligt i sammanfattningen av kapitel 3.1–3.4. Här tas enbart implicit derivering upp, eftersom det är centralt för föreläsning 15.*

## Bakgrund: Kedjeregeln som nyckelverktyg

Implicit derivering bygger helt på **kedjeregeln** (sats 3 i boken):

```
D f(g(x)) = f'(g(x)) · g'(x)
```

> 💡 **"Yttre derivatan gånger inre derivatan."** Om y beror på x (dvs. y = y(x)) gäller t.ex.:
> - D(y²) = 2y · y'(x)
> - D(sin y) = cos(y) · y'(x)
> - D(eʸ) = eʸ · y'(x)

## Vad är implicit derivering?

Ibland ges sambandet mellan x och y *inte* som y = f(x) explicit, utan som en ekvation där x och y är "blandade":

```
F(x, y) = 0     (t.ex. x² + y² = 1, eller x⁴ + y⁴ − xy = 1)
```

Man kan tänka sig att y = y(x) är en funktion av x som uppfyller ekvationen, men det kan vara svårt eller omöjligt att lösa ut y(x) explicit. **Implicit derivering** innebär att man deriverar hela ekvationen med avseende på x — och behandlar y som en funktion av x — utan att behöva lösa ut y först.

## Metod steg för steg

1. **Skriv upp ekvationen** som definierar sambandet
2. **Derivera båda sidor** med avseende på x
3. **Använd kedjeregeln** varje gång du deriverar en term som innehåller y (du får en faktor y'(x))
4. **Lös ut y'(x)** algebraiskt

## Genomgånget exempel från föreläsningen

**Ekvation:** x⁴ + y⁴ − xy = 1

Denna ekvation definierar en kurva i xy-planet (se föreläsningens graf). Vi vill bestämma y'(x) för att kunna beräkna tangenter.

**Steg 1:** Skriv om: 1 = x⁴ + y(x)⁴ − x·y(x), tänk y som funktion av x.

**Steg 2:** Derivera båda sidor med avseende på x:

```
D(1) = D(x⁴ + y(x)⁴ − x·y(x))
```

**Vänsterled:** D(1) = 0

**Högerled:** Derivera term för term:
- D(x⁴) = 4x³
- D(y⁴) = 4y³ · y'(x)    ← kedjeregeln!
- D(x·y) = y + x·y'(x)    ← produktregeln!

Alltså:

```
0 = 4x³ + 4y³·y'(x) − y(x) − x·y'(x)
```

**Steg 3:** Samla termer med y'(x):

```
0 = (4x³ − y) + y'(x)·(4y³ − x)
```

**Steg 4:** Lös ut:

```
y'(x) = (y − 4x³) / (4y³ − x)     (om 4y³ ≠ x)
```

### Beräkna tangenter med implicit derivering

Nu kan vi stoppa in punkter på kurvan:

**I punkten (1, 0):**
```
y' = (0 − 4) / (0 − 1) = −4/−1 = 4
```
Tangentens ekvation: y − 0 = 4(x − 1), dvs. **y = 4x − 4**

**I punkten (1, 1):**
```
y' = (1 − 4) / (4 − 1) = −3/3 = −1
```
Tangentens ekvation: y − 1 = −1(x − 1), dvs. **y = 2 − x**

> 🎯 **Huvudpoäng:** Vi behövde aldrig lösa ut y(x) explicit — vi fick tangentens lutning genom att bara veta *vilken punkt* vi sitter i och sedan använda formeln för y'.

---

# 🔷 KAPITEL 4.6 — Konvexa funktioner

## 4.6.1 Idén: Vad händer när f''(x) ≥ 0 för alla x?

Vi vet sedan kapitel 3.5 att f''(x₀) > 0 i en stationär punkt x₀ innebär lokalt minimum. Men vad händer om f'' ≥ 0 *överallt*? Då får funktionen en speciell global egenskap: den är **konvex**.

### Geometrisk bild

För en konvex funktion gäller:

> **Kordan (räta linjen) mellan två punkter på grafen ligger alltid *ovanför* (eller på) grafen.**

```
         Q
        ╱╲         ← korda (rät linje mellan P₁ och P₂)
       ╱  ╲
   P₁╱  P ╲P₂     ← P = punkt på grafen under kordan
     ╱      ╲
```

Med andra ord: om du drar ett snöre mellan två punkter på kurvan, hänger kurvan nedanför snöret (eller sammanfaller med det). Tänk på en skålformad kurva.

## 4.6.2 Formell definition

> **DEFINITION 1.** *En funktion f definierad på ett intervall kallas **strängt konvex** om för alla par av punkter x₁ ≠ x₂ i D_f och varje tal θ med 0 < θ < 1 gäller*
>
> **(13):**  f((1−θ)x₁ + θx₂) < (1−θ)f(x₁) + θf(x₂)

Om man i (13) tillåter likhet (dvs. ≤ istället för <) talar man om en **konvex** funktion.

### Vad betyder formeln?

Punkten (1−θ)x₁ + θx₂ är en punkt *mellan* x₁ och x₂ (ett viktat medelvärde av x₁ och x₂):
- θ = 0 ger x₁
- θ = 1 ger x₂  
- θ = 1/2 ger mittpunkten (x₁ + x₂)/2

**Vänsterledet** f((1−θ)x₁ + θx₂) = funktionsvärdet i en mellanliggande punkt (punkt P på grafen).

**Högerledet** (1−θ)f(x₁) + θf(x₂) = motsvarande punkt på **kordan** (viktat medelvärde av funktionsvärdena).

Alltså: **funktionsvärdet av medelvärdet ≤ medelvärdet av funktionsvärdena.**

> 💡 **Från föreläsningen uttryckt:**
> ```
> f(viktat medelvärde av argumenten) ≤ viktat medelvärde av funktionsvärdena
> ```

### Strängt konkav — motsatsen

En funktion f är **strängt konkav** om −f(x) är strängt konvex. Ekvivalent:

```
f((1−θ)x₁ + θx₂) > (1−θ)f(x₁) + θf(x₂)
```

dvs. kordan ligger **under** grafen. Tänk på en kupolformad kurva.

> **OBS (från föreläsningen):** Konkava funktioner ger den omvända olikheten:
> ```
> f''(x) ≤ 0  ⟹  f(θ₁x₁ + ... + θₙxₙ) ≥ θ₁f(x₁) + ... + θₙf(xₙ)
> ```

## 4.6.3 Koppling till derivatan — Sats 5

> **SATS 5.** *En deriverbar funktion f är strängt konvex om och endast om dess derivata f' är strängt växande.*

**Bevisidé (ur boken):** 

*Framåtriktning (konvex ⟹ f' växande):* Om f är strängt konvex kan man visa med riktningskoefficienter att för x₁ < ξ < x₂ gäller:

```
[f(x) − f(x₁)] / (x − x₁)  <  [f(y) − f(x₁)] / (y − x₁)     om x < y
```

dvs. differenskvoterna är strängt växande. Genom gränsövergång följer att f'(x₁) < f'(x₂).

*Bakåtriktning (f' växande ⟹ konvex):* Man använder medelvärdessatsen på intervallen [x₁, ξ] och [ξ, x₂] med ξ = (1−θ)x₁ + θx₂, och utnyttjar att f' är strängt växande.

### Praktiskt kriterium: Följdsats 1

> **FÖLJDSATS 1.** *Om f är två gånger deriverbar och f''(x) ≥ 0 med likhet i högst ändligt många punkter, så är f strängt konvex.*

**Bevis:** Med dessa förutsättningar är f' strängt växande (enligt följdsats 2 i avsnitt 3.5, sidan 215), alltså är f strängt konvex enligt sats 5. ∎

**Sammanfattande tabell:**

| Villkor | Slutsats |
|---------|----------|
| f''(x) > 0 | f strängt konvex (skålformad) |
| f''(x) ≥ 0 (med ändligt många nollor) | f strängt konvex |
| f''(x) < 0 | f strängt konkav (kupolformad) |
| f''(x) ≤ 0 (med ändligt många nollor) | f strängt konkav |

> 💡 **Minnesregel från föreläsningen:**
> f''(x) ≥ 0 ⟹ konvex ⟹ f'(x) är växande

## 4.6.4 Jensens olikhet — generalisering till n punkter

Med induktion kan man visa att konvexitetsvillkoret generaliseras:

> **(14):** Om f är strängt konvex och θ₁ + θ₂ + ... + θₙ = 1 (med alla θᵢ > 0, ej alla identiskt lika xᵢ), gäller:
>
> f(θ₁x₁ + ... + θₙxₙ) < θ₁f(x₁) + ... + θₙf(xₙ)

### Bevisidé (induktion, från föreläsningen)

**Fallet n = 3:** Skriv om θ₁x₁ + θ₂x₂ + θ₃x₃ med θ₁ ≠ 1:

```
θ₁x₁ + (θ₂ + θ₃)·[(θ₂x₂ + θ₃x₃)/(θ₂ + θ₃)]
= θ₁x₁ + (1 − θ₁)·z     där z = (θ₂x₂ + θ₃x₃)/(θ₂ + θ₃)
```

Tillämpa konvexitet först med två punkter x₁ och z, sedan med x₂ och x₃:

```
f(θ₁x₁ + (1−θ₁)z) ≤ θ₁f(x₁) + (1−θ₁)f(z)
                     ≤ θ₁f(x₁) + (1−θ₁)[θ₂/(θ₂+θ₃)·f(x₂) + θ₃/(θ₂+θ₃)·f(x₃)]
                     = θ₁f(x₁) + θ₂f(x₂) + θ₃f(x₃)
```

## 4.6.5 Tillämpning: Olikheten G ≤ A (geometriskt ≤ aritmetiskt medelvärde)

**Exempel 17 (ur boken) / föreläsningen:** Eftersom f(x) = eˣ är strängt konvex (ty f''(x) = eˣ > 0), och med θᵢ = 1/n samt xᵢ = ln aᵢ (där a₁, ..., aₙ > 0), ger (14):

```
e^(1/n·(ln a₁ + ... + ln aₙ)) ≤ 1/n·(e^(ln a₁) + ... + e^(ln aₙ))
```

dvs.

```
e^(ln(a₁·...·aₙ)^(1/n)) ≤ (a₁ + ... + aₙ)/n
```

Alltså:

> **(a₁ · a₂ · ... · aₙ)^(1/n) ≤ (a₁ + a₂ + ... + aₙ)/n**
>
> **Geometriska medelvärdet ≤ Aritmetiska medelvärdet**

med likhet precis då alla aᵢ är lika!

## 4.6.6 Tillämpning: Pluggplanering (från föreläsningen)

Richard har 4q timmar att plugga för två ämnen. Hans poäng per ämne (som funktion av nedlagd tid t) är:

```
p(t) = 10√t     poäng per timme
```

**Fråga:** Hur ska han fördela tiden för att maximera totalpoängen?

**Analys:** p''(t) = −(5/2)t^(−3/2) < 0, alltså är p **konkav**.

Med T = 100 total tid och fördelning t₁ + t₂ = T ger Jensens olikhet för konkava funktioner:

```
p(t₁) + p(t₂) = 2·(½p(t₁) + ½p(t₂)) ≤ 2·p((t₁+t₂)/2) = 2·p(T/2)
```

**Slutsats:** En **jämn fördelning** ger flest poäng. Detta är en direkt konsekvens av konkavitet!

---

# 🔷 KAPITEL 4.3 — Optimering

## 4.3.1 Vad handlar optimering om?

Optimering innebär att under bestämda förutsättningar hitta den **bästa lösningen** på ett givet problem:
- Minimera en vägsträcka eller kostnad
- Maximera en vinst eller area
- Hitta optimala mått på en konstruktion

> **Översatt till matematiskt språk:** Bestäm **största eller minsta värdet** av en given funktion, eventuellt med bivillkor.

## 4.3.2 Tillvägagångssätt (från föreläsningen)

### Mål

Hitta ett optimalt värde — t.ex. störst vinst eller minst kostnad.

### Strategi på slutet intervall

Om funktionen är **kontinuerlig** och intervallet **kompakt** (slutet och begränsat, [a,b]):
- Största och minsta värdet **existerar** (satsen om kontinuerliga funktioner på kompakta mängder)

Man behöver då undersöka **tre typer av kandidater**:

1. **Stationära punkter** — där f'(x) = 0
2. **Punkter där f inte är deriverbar** — t.ex. spetsar
3. **Ändpunkter** av intervallet — a och b

> ⚠️ **Från föreläsningen:** Man ska kontrollera *alla tre* typer. Det optimala värdet kan finnas i vilken som helst av dessa!

### Strategi med derivata (öppet intervall eller obegränsat)

Om optimering sker utan slutet intervall behöver man:
1. Rita funktionskurvan / analysera uppförandet
2. Hitta stationära punkter: lös f'(x) = 0
3. Bekräfta typ med andraderivatatest eller teckenschema
4. Kontrollera beteende vid ändpunkter / gränser

> **OBS (från boken, s. 235):** Optimering är ett **globalt** problem. Ett lokalt maximum (f'(x₀) = 0, f''(x₀) < 0) behöver inte vara det globala maximumet! Man behöver ofta fullständig kurvritning för att bekräfta.

## 4.3.3 Speciella metoder (utan derivata)

Vissa optimeringsproblem löses elegantast med direkta metoder:

### Exempel 3 (boken): Andragradspolynom

Bestäm största/minsta värdet av f(x) = x² + 4x + 7.

**Lösning:** Kvadratkomplettering:
```
x² + 4x + 7 = (x + 2)² + 3
```
Minimum = 3 vid x = −2. Inget maximum (f → +∞). Ingen derivata behövs!

### Exempel 4 (boken): Rektangel med given omkrets

Bestäm längd och bredd på den rektangel med omkrets p som har störst area.

**Lösning:** Sidorna a och b uppfyller 2(a+b) = p. Vi ska maximera ab. Enligt AG-olikheten (sats 0.2):

```
√(ab) ≤ (a + b)/2 = p/4
```

med likhet då a = b (= p/4). Alltså: **kvadraten har störst area**. ∎

## 4.3.4 Optimeringsproblem med derivata

### Metoden

1. **Identifiera** vad som ska optimeras (målfunktionen)
2. **Uttryck** målfunktionen i *en* variabel (använd bivillkor för att eliminera övriga)
3. **Bestäm** definitionsmängden (vilka värden är fysikaliskt rimliga?)
4. **Rita** funktionskurvan eller gör teckenschema
5. **Hitta** stationära punkter (f'(x) = 0)
6. **Bekräfta** med andraderivata eller teckenschema
7. **Kontrollera** ändpunkter!

### Exempel: Kafferosteriproblemet (från föreläsningen)

Kunder betalar mer för kaffe beroende på rostningsgrad. Priset per kilo efter t minuters rostning:

```
p(t) = (1 + (t/10)²) · 90     kr/kilo
```

Men kaffe förloras under rostning: av 100 kg rå vara finns kvar:

```
v(t) = 100 − 5t     kg efter t minuter
```

Rostningstiden kan vara 0 ≤ t ≤ 20.

**Intäktsfunktionen:**
```
I(t) = p(t)·v(t) = 90(1 + t²/100)(100 − 5t) = 90(−t³/20 + t² − 5t + 100)
```

**Steg 1: Stationära punkter.** I'(t) = 0:

```
I'(t) = 90(−3t²/20 + 2t − 5) = 0
⟹  −3t² + 40t − 100 = 0
⟹  t = (20 ± 10)/3 = 10/3 eller 10
```

**Steg 2: Andraderivatatest.**

```
I''(t) = 90(−6t/20 + 2)

I''(10/3) = 90(−1 + 2) = 90 > 0     ⟹  lokalt minimum
I''(10) = 90(−3 + 2) = −90 < 0       ⟹  lokalt maximum
```

**Steg 3: Kontrollera ändpunkter!**

```
I(0)  = 90 · 100 = 9000
I(10) = 90(−50 + 100 − 50 + 100) = 9000
I(20) = ... (beräknas)
```

**Slutsats:** I(10) = 9000 = I(0). I modellen ger *ingen rostning alls* (t = 0) samma intäkt som 10 minuters rostning! Det lokala maximumet i t = 10 är lika bra som ändpunkten t = 0.

> ⚠️ **Viktig lärdom:** Ändpunkter kan ge samma (eller bättre!) värde som den stationära punkten. Man måste *alltid* kontrollera dem!

### Exempel 7 (boken): Konservburk — minimera plåtåtgång

**Problem:** Tillverka en cylindrisk burk med volym V. Minimera plåtåtgången.

**Uppställning:** Med radie r och höjd h gäller V = πr²h, dvs. h = V/(πr²).

Plåtåtgång (bottenarea + lock + mantelyta):

```
f(r) = 2πr² + 2πrh = 2πr² + 2V/r,     r > 0
```

**Derivata:**

```
f'(r) = 4πr − 2V/r² = 2(2πr³ − V)/r²
```

Nollställe: r₀ = ∛(V/(2π)).

**Teckenschema:** f'(r) < 0 för r < r₀ och f'(r) > 0 för r > r₀ ⟹ minimum i r₀.

**Optimala mått:**

```
h = V/(πr₀²) = 2∛(V/(2π)) = 2r₀
```

> 🎯 **Slutsats:** Burken bör utformas så att **höjden = diametern** (h = 2r). Detta minimerar materialåtgången!

### Exempel 10 (boken): Marginalkostnad = styckkostnad

**Problem:** f(x) = kostnaden för att framställa x enheter. Visa att styckkostnaden f(x)/x är minimal när marginalkostnaden f'(x) = styckkostnaden f(x)/x.

**Bevis:** Styckkostnaden g(x) = f(x)/x är minimal då g'(x) = 0:

```
g'(x) = [xf'(x) − f(x)] / x² = 0
⟹  xf'(x) − f(x) = 0
⟹  f'(x) = f(x)/x     ∎
```

> 💡 **Ekonomisk tolkning:** Producera tills kostnaden för *en extra enhet* (marginalkostnaden) är lika med *genomsnittskostnaden per enhet* (styckkostnaden).

### Exempel: Optimal hastighet tunnelbana (från föreläsningen)

**Problem:** En tunnelbana ska köra en sträcka L. Driftskostnaden d(t) = α·t (proportionell mot tid). Energikostnaden E(v) = β·L·v² (proportionell mot hastighet i kvadrat). Total kostnad:

```
K(v) = E(v) + d(v) = L(βv² + α/v)
```

(Ty t = L/v.) Stationära punkter:

```
K'(v) = L(2βv − α/v²) = 0  ⟹  v³ = α/(2β)  ⟹  v = (α/(2β))^(1/3)
```

> 🎯 Den optimala hastigheten beror på förhållandet α/(2β) mellan driftskostnad och energikostnad!

---

## 🧠 Checklista: Vad du bör kunna

### Kapitel 3.3 — Implicit derivering

- [ ] Kedjeregeln: D f(g(x)) = f'(g(x))·g'(x)
- [ ] Metoden för implicit derivering: derivera båda sidor, använd kedjeregeln, lös ut y'
- [ ] Beräkna tangenter till implicit definierade kurvor

### Kapitel 4.6 — Konvexa funktioner

- [ ] **Definitionen** av konvex/konkav med θ-parametrisering (formel 13)
- [ ] **Geometrisk tolkning:** korda ovanför/under grafen
- [ ] **Sats 5:** f strängt konvex ⟔ f' strängt växande
- [ ] **Följdsats 1:** f''(x) ≥ 0 ⟹ konvex; f''(x) ≤ 0 ⟹ konkav
- [ ] **Jensens olikhet** (generalisering till n punkter, formel 14)
- [ ] **Tillämpning:** G ≤ A (geometriskt ≤ aritmetiskt medelvärde) via konvexitet av eˣ
- [ ] Pluggplanering / resursfördelning med konkava funktioner

### Kapitel 4.3 — Optimering

- [ ] **Identifiera** målfunktionen och uttryck den i en variabel
- [ ] Tre kandidater: stationära punkter, icke-deriverbara punkter, ändpunkter
- [ ] **Lös** f'(x) = 0 och bekräfta med f'' eller teckenschema
- [ ] **Kontrollera ändpunkter!** (globalt problem, inte bara lokalt)
- [ ] Speciella metoder: kvadratkomplettering, AG-olikheten
- [ ] Tillämpa optimering i geometriska och ekonomiska problem

---

## 📌 Formler att memorera

| Formel | Beskrivning |
|--------|-------------|
| f((1−θ)x₁ + θx₂) ≤ (1−θ)f(x₁) + θf(x₂) | Definition av konvex funktion |
| f strängt konvex ⟔ f' strängt växande | Sats 5 |
| f''(x) ≥ 0 ⟹ f konvex | Följdsats 1 (praktiskt kriterium) |
| f(Σθᵢxᵢ) ≤ Σθᵢf(xᵢ) | Jensens olikhet (konvex) |
| f(Σθᵢxᵢ) ≥ Σθᵢf(xᵢ) | Jensens olikhet (konkav) |
| (a₁·...·aₙ)^(1/n) ≤ (a₁+...+aₙ)/n | G ≤ A via konvexitet |
| xf'(x) = f(x) vid optimal styckkostnad | Marginalkostnad = styckkostnad |
