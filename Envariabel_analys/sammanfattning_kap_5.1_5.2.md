# 📐 Kapitel 5.1 & 5.2 — Primitiva funktioner: Definition, Räkneregler, Variabelsubstitution, Partialintegration & Rationella funktioner

## Omfattande sammanfattning och genomgång

*Baserad på kursboken och föreläsning 16–17 (Kap 5.1, 5.2)*

---

# 🔷 KAPITEL 5.1 — Allmänna egenskaper hos primitiva funktioner

## 5.1.1 Grundidén: Derivering baklänges

Hittills i kursen har vi fokuserat på: *givet en funktion f, beräkna derivatan f'*. Nu vänder vi på frågan:

> **Givet en funktion f — hitta en funktion F vars derivata är lika med f.**

Detta kallas det **omvända derivationsproblemet**, och den sökta funktionen F kallas en **primitiv funktion** till f.

### Varför behöver vi detta?

Tänk dig att du vet *hastigheten* v(t) för en bil vid varje tidpunkt, men du vill veta *positionen* s(t). Eftersom v(t) = s'(t), behöver du hitta en funktion s(t) vars derivata är v(t). Det är exakt vad en primitiv funktion gör!

> 💡 **Intuition:** Om derivering svarar på "hur snabbt ändras funktionen?", så svarar primitiva funktioner på "vilken funktion har denna ändringstakt?"

### Motiverande exempel från föreläsningen

**Backhoppning:** En skidbacke i Dubai har lutningsprofil h'(x) = −4/5 + x/80 för 0 ≤ x ≤ 50.

Fråga: Vad blir höjdskillnaden efter 50 meter?

Lutningen h'(x) är derivatan av höjdprofilen h(x). Vi söker alltså h(x) — en primitiv funktion till h'(x):

```
h(x) = −4x/5 + x²/160 + C
```

**Check:** D(−4x/5 + x²/160) = −4/5 + 2x/160 = −4/5 + x/80 ✓

Med h(0) = 0 ger detta h(50) = −40 + 2500/160 = −24.375 m (neråt).

**Elbilsladdning:** Laddningseffekten p(t) = 10/(1+t²) kW. Hur mycket energi laddas under t ∈ [−1, 7]?

Laddningen Q(t) har Q'(t) = p(t), och vi vet att D(arctan x) = 1/(1+x²), så:

```
Q(t) = 10·arctan(t)    ger    ΔQ = 10(arctan 7 − arctan(−1)) ≈ 22.14 kWh
```

---

## 5.1.2 Formell definition

> **DEFINITION 1.** *Låt f vara definierad i ett intervall I. En deriverbar funktion F kallas en **primitiv funktion** (eller bara en **primitiv**) till f om*
>
> **F'(x) = f(x)** för alla x ∈ I.

### Hur många primitiva funktioner finns det?

Om F(x) är en primitiv till f(x), så är även F(x) + C en primitiv för varje konstant C ∈ ℝ, ty:

```
D(F(x) + C) = F'(x) + 0 = f(x)
```

Frågan är: finns det *ännu fler* primitiver? Svaret är nej:

> **SATS (Entydighet upp till konstant).** *Om F är en primitiv funktion till f på ett intervall I, kan varje annan primitiv G till f på intervallet skrivas på formen*
>
> **G(x) = F(x) + C** för en konstant C ∈ ℝ.

**Bevis:** Betrakta H(x) = G(x) − F(x). Då är H'(x) = G'(x) − F'(x) = f(x) − f(x) = 0 på intervallet. Enligt sats 3.15 (f' = 0 ⟹ f konstant) följer H(x) = C. Alltså G(x) = F(x) + C. ∎

> ⚠️ **Från föreläsningen:** "Viktigt att komma ihåg konstanten! Annars glömmer vi gärna bort möjliga lösningar."

---

## 5.1.3 Beteckningar: Den obestämda integralen

Mängden av **alla** primitiva funktioner till f(x) betecknas:

```
∫ f(x) dx
```

Detta kallas den **obestämda integralen** av f(x). Symbolen ∫ kallas **integraltecknet**, f(x) kallas **integranden** och dx anger vilken variabel vi integrerar med avseende på.

> 💡 **Från föreläsningen:** Tänk på ∫ dx som en *operator* på f(x), precis som D är en operator. Om D "deriverar" så "integrerar" ∫ dx. De är i viss mening varandras inverser:
>
> ```
> D(∫ f(x) dx) = f(x)     och     ∫ f'(x) dx = f(x) + C
> ```

---

## 5.1.4 De elementära primitiva funktionerna — tabellen du MÅSTE kunna!

Eftersom primitiv funktion är "derivering baklänges" kan vi vända på derivattabellen:

| Nr | Integral | Primitiv funktion | Villkor |
|----|----------|-------------------|---------|
| (2) | ∫ a dx | ax + C | a konstant |
| (3) | ∫ xᵅ dx | xᵅ⁺¹/(α+1) + C | **α ≠ −1** |
| (4) | ∫ 1/x dx | ln\|x\| + C | x ≠ 0 |
| (5) | ∫ eˣ dx | eˣ + C | |
| (6) | ∫ cos x dx | sin x + C | |
| (7) | ∫ sin x dx | −cos x + C | **OBS minustecknet!** |
| (8) | ∫ 1/cos²x dx | tan x + C | |
| (9) | ∫ 1/sin²x dx | −cot x + C | |
| (10) | ∫ 1/(1+x²) dx | arctan x + C | |
| (11) | ∫ 1/√(1−x²) dx | arcsin x + C | \|x\| < 1 |
| (12) | ∫ 1/√(x²+α) dx | ln\|x + √(x²+α)\| + C | α ∈ ℝ konstant |

Dessutom:

| Nr | Integral | Primitiv funktion | Villkor |
|----|----------|-------------------|---------|
| (extra) | ∫ aˣ dx | aˣ/ln a + C | a > 0 |

> 🎯 **Från föreläsningen:** "Lär dig dessa utantill!" Alla utom den sista (12) följer direkt från standardderivatorna. Formel (12) bevisas genom att derivera högerledet (se föreläsningens sida 5).

### Bevis av formel (12) — derivering av ln|x + √(x²+β)|

```
D(ln|x + √(x²+β)|) = 1/(x + √(x²+β)) · D(x + √(x²+β))
                     = 1/(x + √(x²+β)) · (1 + x/√(x²+β))
                     = 1/(x + √(x²+β)) · (√(x²+β) + x)/√(x²+β)
                     = 1/√(x²+β)     ∎
```

> 💡 **Minnesregel:** Formeln (12) ser komplicerad ut men strukturen är alltid densamma — ln av argumentet plus roten. Den dyker upp varje gång du har 1/√(kvadratiskt uttryck).

---

## 5.1.5 Räkneregler för primitiva funktioner

Precis som för derivator finns det räkneregler:

> **SATS (Linjäritet).** *Om f och g har primitiva funktioner gäller:*
>
> **(15):** ∫ α·f(x) dx = α · ∫ f(x) dx (konstant kan brytas ut)
>
> **(16):** ∫ (f(x) + g(x)) dx = ∫ f(x) dx + ∫ g(x) dx (summa kan delas upp)

**Bevis:** Följer direkt från motsvarande regler för derivator. Om F' = f och G' = g, så är D(αF) = αf och D(F + G) = f + g. ∎

> 💡 **Från föreläsningen:** "Obestämda integralen är en *linjär operator* precis som derivatan!"

### Två extremt nyttiga formler (från kedjeregeln)

Eftersom D(ln|f(x)|) = f'(x)/f(x) och D(f(x)^(α+1)/(α+1)) = f(x)^α · f'(x) får vi:

> **(13):** ∫ f'(x)/f(x) dx = ln|f(x)| + C (om f(x) ≠ 0)
>
> **(14):** ∫ f(x)ᵅ · f'(x) dx = f(x)^(α+1)/(α+1) + C (om α ≠ −1)

**Dessa formler är otroligt användbara!** De fångar mönstret: "funktionen i nämnaren, dess derivata i täljaren" respektive "funktion upphöjt till potens, gånger sin egen derivata."

### Exempel på (13) och (14)

```
∫ cot(x) dx = ∫ cos(x)/sin(x) dx = ln|sin(x)| + C
```
(Här: f(x) = sin x, f'(x) = cos x — perfekt matchning med formel (13)!)

```
∫ ln(x)²/x dx = ∫ (ln x)² · (1/x) dx = (ln x)³/3 + C
```
(Här: f(x) = ln x, f'(x) = 1/x, α = 2 — matchning med formel (14).)

---

## 5.1.6 Variabelsubstitution (variabelbyte)

### Grundidén — att "ångra" kedjeregeln

Vi vet att kedjeregeln ger: D(F(g(x))) = F'(g(x)) · g'(x) = f(g(x)) · g'(x).

Om vi "integrerar" detta baklänges får vi:

> **Variabelsubstitution:**
> ```
> ∫ f(g(x)) · g'(x) dx = F(g(x)) + C
> ```
> där F' = f.

### Det praktiska skrivsättet

I praktiken gör man substitutionen genom att införa en ny variabel:

```
u = g(x)     ⟹     du = g'(x) dx
```

och skriver om integralen:

```
∫ f(g(x)) · g'(x) dx  =  ∫ f(u) du  =  F(u) + C  =  F(g(x)) + C
```

> 💡 **Tanken:** Du byter variabel så att integralen *i den nya variabeln* blir enklare. Sedan löser du den enklare integralen och byter tillbaka till den ursprungliga variabeln.

### Formell sats

> **SATS 2 (Variabelsubstitution).** *Antag att g i variabelbytet x = g(t) är en deriverbar funktion. Då är*
>
> ```
> ∫ f(x) dx = [∫ f(g(t)) g'(t) dt]_{t=g⁻¹(x)}
> ```

### Steg-för-steg-guide: Hur gör man en substitution?

1. **Identifiera** en "inre funktion" g(x) i integranden som komplicerar saker
2. **Sätt** u = g(x)
3. **Beräkna** du = g'(x) dx, dvs. lös ut dx = du/g'(x)
4. **Skriv om** hela integralen i variabeln u (det får *inte* finnas kvar något x!)
5. **Beräkna** integralen i u
6. **Byt tillbaka** till x med u = g(x)
7. **Testa** ditt svar genom att derivera! (Alltid en bra idé.)

---

## 5.1.7 Vanliga substitutionstyper (med exempel)

### Typ 1: Linjär förskjutning — u = kx + m

När argumentet är en linjär funktion av x:

```
∫ f(kx + m) dx  =  [u = kx + m, du = k·dx]  =  (1/k) ∫ f(u) du  =  (1/k) F(u) + C
```

> 💡 **Minnesregel:** "Dela med koefficienten framför x."

**Exempel:**
```
∫ (3x+5)² dx  =  [u = 3x+5, du = 3dx]  =  (1/3) ∫ u² du  =  u³/9 + C  =  (3x+5)³/9 + C

∫ e^(−4x+2) dx  =  [v = −4x+2, dv = −4dx]  =  −(1/4) eᵛ + C  =  −(1/4) e^(−4x+2) + C

∫ sin(ωt + φ) dt  =  [u = ωt+φ, du = ω·dt]  =  −(1/ω) cos(ωt + φ) + C
```

### Typ 2: Kvadratisk term — u = kx² + d

Signal: du ser **x²** inne i f( ) och **x·dx** i integranden.

```
∫ f(kx² + d) · x dx  =  [v = kx²+d, dv = 2kx·dx]  =  (1/2k) ∫ f(v) dv
```

**Exempel:**
```
∫ x/(1+x²) dx  =  [v = 1+x², dv = 2x·dx]  =  (1/2) ∫ 1/v dv  =  (1/2) ln|v| + C
                =  (1/2) ln(1+x²) + C     (obs: 1+x² > 0 alltid)

∫ e^(−2x²) · 4x dx  =  [v = −2x², dv = −4x·dx]  =  −eᵛ + C  =  −e^(−2x²) + C
```

### Typ 3: sin/cos-substitution

Om du ser f(sin x)·cos x eller f(cos x)·sin x:

```
∫ f(sin x) cos x dx  =  [u = sin x, du = cos x dx]  =  ∫ f(u) du

∫ f(cos x) sin x dx  =  [v = cos x, dv = −sin x dx]  =  −∫ f(v) dv
```

**Exempel:**
```
∫ cos³(4x) dx  =  ∫ cos²(4x)·cos(4x) dx  =  ∫ (1−sin²(4x))·cos(4x) dx

    [u = sin(4x), du = 4cos(4x)dx]

    = (1/4) ∫ (1−u²) du  =  (1/4)(u − u³/3) + C  =  (1/4)sin(4x)(1 − sin²(4x)/3) + C
```

### Typ 4: Trigonometrisk substitution — att bli av med rotuttryck

| Om integranden innehåller | Prova substitutionen | Ty |
|---|---|---|
| √(1 − x²) | x = sin t | 1 − sin²t = cos²t |
| √(1 + x²) | x = tan t | 1 + tan²t = 1/cos²t |
| √(x² − 1) | x = 1/cos t | 1/cos²t − 1 = tan²t |

**Exempel:** ∫ √(1−x²) dx med x = sin t, dx = cos t dt:

```
∫ √(1−sin²t) · cos t dt  =  ∫ cos²t dt  =  (1/2)(t + sin t cos t) + C
                           =  (1/2)(arcsin x + x√(1−x²)) + C
```

---

## 5.1.8 Partialintegration

### Grundidén — att "ångra" produktregeln

Produktregeln säger: D(F(x)·g(x)) = f(x)·g(x) + F(x)·g'(x), dvs.:

```
F(x)·g(x) = ∫ f(x)·g(x) dx + ∫ F(x)·g'(x) dx
```

Omstälning ger:

> **SATS 1 (Partialintegration).** *Om F är en primitiv funktion till f, så är*
>
> **(17):** ∫ f(x)·g(x) dx = F(x)·g(x) − ∫ F(x)·g'(x) dx

> ⚠️ **Från föreläsningen:** "+C behövs inte här" ty vi har obestämda integraler i *båda* led. Konstanten "bor" inuti ∫-tecknet.

### Strategin: Välj f och g klokt!

Dela upp integranden i f(x) · g(x) så att:
- **f** har känd primitiv **F** (den du integrerar)
- **g'** är enklare än **g** (derivering förenklar)

> 💡 **LIATE-regeln** (minnesregel för vad som ska vara g):
> **L**ogaritmiska → **I**nversa trig → **A**lgebraiska → **T**rigonometriska → **E**xponentiella
>
> Välj g som den funktion som står *först* i listan (den som förenklas mest av derivering).

### Grundexempel

**∫ x·eˣ dx:**

Välj g(x) = x (algebraisk, g'=1 förenklar!) och f(x) = eˣ (F = eˣ):

```
∫ x·eˣ dx  =  eˣ·x − ∫ eˣ·1 dx  =  x·eˣ − eˣ + C  =  (x−1)eˣ + C
```

**∫ ln x dx** — tricket "gånger 1":

```
∫ ln x dx  =  ∫ 1 · ln x dx      (f = 1, F = x, g = ln x, g' = 1/x)
            =  x·ln x − ∫ x · (1/x) dx  =  x·ln x − ∫ 1 dx  =  x(ln x − 1) + C
```

### Partialintegration i flera steg

Ibland måste man upprepa partialintegrationen:

**∫ (x²−4x) sin x dx:**

Steg 1: g = x²−4x, g' = 2x−4, f = sin x, F = −cos x
```
= −cos(x)(x²−4x) − ∫ (−cos x)(2x−4) dx
= −cos(x)(x²−4x) + ∫ cos(x)(2x−4) dx
```

Steg 2: g₂ = 2x−4, g₂' = 2, f₂ = cos x, F₂ = sin x
```
= −cos(x)(x²−4x) + sin(x)(2x−4) − ∫ sin(x)·2 dx
= (−x²+4x+2)cos x + (2x−4)sin x + C
```

### Det cirkulära tricket — eˣ·sin eller eˣ·cos

Vid integraler av typen ∫ eˣ sin(ax) dx hamnar man efter *två* partialintegrationer tillbaka på samma integral — men med ändrat tecken! Då kan man lösa ut:

**∫ eˣ sin(x/2) dx:**

```
Steg 1: = eˣ sin(x/2) − ∫ eˣ cos(x/2)·(1/2) dx

Steg 2: = eˣ sin(x/2) − (eˣ·(1/2)cos(x/2) − ∫ eˣ·(−1/4)sin(x/2) dx)

       = eˣ(sin(x/2) − (1/2)cos(x/2)) − (1/4) ∫ eˣ sin(x/2) dx
```

Den sista integralen = samma som vi startade med! Kalla den I:

```
I = eˣ(sin(x/2) − (1/2)cos(x/2)) − (1/4)I

⟹  (5/4)I = eˣ(sin(x/2) − (1/2)cos(x/2)) + C̃

⟹  I = (4/5)eˣ(sin(x/2) − (1/2)cos(x/2)) + C
```

> 🎯 **Denna teknik fungerar alltid** för ∫ eᵃˣ sin(bx) dx och ∫ eᵃˣ cos(bx) dx. Partialintegrera två gånger, känn igen originalet, lös ut algebraiskt!

---

# 🔷 KAPITEL 5.2 — Rationella funktioner (partialbraksuppdelning)

## 5.2.1 Vad är problemet?

En **rationell funktion** är en kvot av två polynom:

```
f(x) = g(x)/h(x)
```

Vi vill hitta ∫ g(x)/h(x) dx. Poängen med detta avsnitt är att det alltid *går* — det finns en systematisk metod.

> 💡 **Den stora idén:** Varje rationell funktion kan brytas ned i enklare bitar som vi redan vet hur man integrerar. Det är som att ta isär en komplicerad maskin i enkla delar.

## 5.2.2 Det systematiska receptet — fyra steg

### Steg I: Polynomdivision (om grad g ≥ grad h)

Om täljaren har **minst lika hög** grad som nämnaren, utför polynomdivision:

```
g(x)/h(x) = q(x) + r(x)/h(x)     där grad r < grad h
```

Polynomet q(x) kan integreras direkt (det är bara x-potenser). Resten r(x)/h(x) är ett **äkta bråk** (täljarens grad < nämnarens grad).

**Exempel 10 (boken):**
```
(x³ + 3x² + 5x + 3)/(x² + x + 1) = x + 2 + (2x+1)/(x² + x + 1)
```
Nu: ∫ (x+2) dx = x²/2 + 2x, och ∫ (2x+1)/(x²+x+1) dx = ln(x²+x+1) + C (formel 13!).

### Steg II: Faktorisera nämnaren

Faktorisera h(x) i **reella** faktorer av grad 1 och 2:
- Förstagradsfaktorer: (x − α) från reella nollställen
- Andragradsfaktorer: (x² + ax + b) utan reella nollställen (dvs. diskriminant < 0)

Samla faktorer som är lika till potenser: (x − α)ⁿ, (x² + ax + b)ᵐ.

### Steg III: Partialbraksuppdelning

Här är nyckeln! Varje äkta bråk r(x)/h(x) kan **alltid** skrivas som en summa av enklare bråk enligt följande schema:

| Faktor i nämnaren | Ger partialbraken |
|---|---|
| (x − α) | A/(x − α) |
| (x − α)ⁿ | A₁/(x−α) + A₂/(x−α)² + ... + Aₙ/(x−α)ⁿ |
| (x² + ax + b) | (A₁x + B₁)/(x² + ax + b) |
| (x² + ax + b)ᵐ | (A₁x+B₁)/(x²+ax+b) + (A₂x+B₂)/(x²+ax+b)² + ... + (Aₘx+Bₘ)/(x²+ax+b)ᵐ |

> 💡 **Tumregel:**
> - Varje linjär faktor (x−α)ⁿ bidrar med **n stycken** bråk med konstanta täljare
> - Varje kvadratisk faktor (x²+ax+b)ᵐ bidrar med **m stycken** bråk med linjära täljare (Ax+B)
> - Antalet okända koefficienter = graden av nämnaren

### Steg IV: Integrera varje del

Varje partialbråk är av en typ vi vet hur man integrerar (se avsnitt 5.2.3 nedan).

## 5.2.3 De fyra elementära bråktyperna

Från föreläsning 17 — det finns fyra grundtyper av bråk du behöver kunna integrera:

### Typ 1: ∫ 1/(x−a) dx

```
∫ 1/(x−a) dx = ln|x−a| + C
```
(Direkt från formel (4) med substitution u = x−a.)

### Typ 2: ∫ 1/(x−a)ⁿ dx  (n ≥ 2)

```
∫ 1/(x−a)ⁿ dx = [u = x−a] = ∫ u⁻ⁿ du = u⁻ⁿ⁺¹/(−n+1) + C = −1/((n−1)(x−a)ⁿ⁻¹) + C
```

### Typ 3: ∫ t/(t²+a) dt  och  ∫ 1/(t²+a) dt  (a > 0)

**Med t i täljaren:**
```
∫ t/(t²+a) dt = [u = t²+a, du = 2t·dt] = (1/2) ln(t²+a) + C
```

**Utan t i täljaren (viktig!):**
```
∫ 1/(t²+a) dt = [v = t/√a, dv = dt/√a] = (1/√a) ∫ 1/(v²+1) dv = (1/√a) arctan(t/√a) + C
```

### Typ 4: Högre potenser — ∫ 1/(t²+a)ⁿ dt

Dessa löses med en **rekursionsformel** (partialintegration):

```
∫ 1/(t²+a)ⁿ⁺¹ dt = t/(2an·(t²+a)ⁿ) + (2n−1)/(2an) · ∫ 1/(t²+a)ⁿ dt
```

Man börjar med n=1 (typ 3b) och jobbar sig uppåt.

> 💡 **I praktiken:** Typ 4 är jobbig men ovanlig på tentor. Det viktigaste är att kunna typ 1–3 snabbt och säkert.

## 5.2.4 Hur bestämmer man koefficienterna?

### Metod A: Ekvationssystem (koefficienter)

Multiplicera bort nämnaren, utveckla högerledet, och identifiera koefficienter för xⁿ, xⁿ⁻¹, ...

**Exempel (föreläsningen):** 3x/(x²−1) = A/(x+1) + B/(x−1)

```
3x = A(x−1) + B(x+1) = (A+B)x + (B−A)

⟹  A+B = 3  och  B−A = 0  ⟹  A = B = 3/2
```

### Metod B: Handpåläggning (snabbare!)

Om nämnaren bara har enkla linjära faktorer kan man sätta x = nollstället i varje faktor:

**Exempel 12 (boken):** (−2x²+3x−4)/(x(x+1)(x−2)) = A/x + B/(x+1) + C/(x−2)

Multiplicera med nämnaren:
```
−2x²+3x−4 = A(x+1)(x−2) + B·x(x−2) + C·x(x+1)
```

**Sätt x = 0:** −4 = A(1)(−2) ⟹ A = 2

**Sätt x = −1:** −2−3−4 = B(−1)(−3) ⟹ B = −3

**Sätt x = 2:** −8+6−4 = C(2)(3) ⟹ C = −1

> ⚠️ **Varning (från boken):** Handpåläggning fungerar bara för *enkla* nollställen. För multipla nollställen (t.ex. (x+1)²) måste man använda ekvationssystem eller kombinera metoderna.

## 5.2.5 Komplett genomarbetat exempel

**Beräkna** ∫ (x²+3)/((x²+4)(x−1)²) dx

**Steg 1:** Grad täljare (2) < grad nämnare (4) — äkta bråk, ingen polynomdivision behövs.

**Steg 2:** Nämnaren: (x²+4) (irreducibel, diskriminant < 0) och (x−1)² (dubbelt nollställe).

**Steg 3:** Ansats enligt schemat:

```
(x²+3)/((x²+4)(x−1)²) = (Ax+B)/(x²+4) + C/(x−1) + D/(x−1)²
```

Multiplicera med (x²+4)(x−1)²:

```
x²+3 = (Ax+B)(x−1)² + C(x−1)(x²+4) + D(x²+4)
```

**Handpåläggning med x = 1:** 1+3 = D(1+4) ⟹ D = 4/5

**Koefficienter:** Utveckla och identifiera (A+C = 0, B−2A−C+D = 1, etc.) → löser systemet.

**Steg 4:** Integrera varje del separat:

```
∫ (Ax+B)/(x²+4) dx  →  (A/2)ln(x²+4) + (B/2)arctan(x/2)     (typ 3)
∫ C/(x−1) dx         →  C·ln|x−1|                               (typ 1)
∫ D/(x−1)² dx        →  −D/(x−1)                                (typ 2)
```

---

## 5.2.6 Integration av andragradsfaktorer — kvadratkomplettering

När du stöter på ∫ 1/(x²+ax+b) dx, **kvadratkomplettera** först:

```
x² + ax + b = (x + a/2)² + (b − a²/4)
```

Sedan substituera t = x + a/2, dt = dx, och du hamnar på formen ∫ 1/(t² + k) dt som du kan lösa.

**Exempel 9 (boken):**
```
∫ 1/(x²+4x+6) dx  =  ∫ 1/((x+2)² + 2) dx  =  [t = x+2]  =  ∫ 1/(t²+2) dt
                    =  (1/√2) arctan(t/√2) + C  =  (1/√2) arctan((x+2)/√2) + C
```

---

## 🧠 Sammanfattning: Vilken teknik ska jag använda?

Här är ett beslutsträd att följa vid beräkning av primitiver:

```
Ser integralen ut som en standardprimitiv?
  ├─ JA → Slå upp i tabellen, klart!
  └─ NEJ → Fortsätt...

Kan jag förenkla (bryta ut, dela upp, förkorta)?
  ├─ JA → Gör det, sedan standardprimitiv
  └─ NEJ → Fortsätt...

Finns det mönstret f(g(x))·g'(x)?
  ├─ JA → Variabelsubstitution u = g(x)
  └─ NEJ → Fortsätt...

Är integranden en produkt av "olika" funktioner?
  ├─ JA → Partialintegration (LIATE-regeln)
  └─ NEJ → Fortsätt...

Är integranden en rationell funktion p(x)/q(x)?
  ├─ JA → Partialbraksuppdelning
  └─ NEJ → Fortsätt...

Finns det rotuttryck √(1−x²), √(1+x²), etc.?
  ├─ JA → Trigonometrisk substitution
  └─ NEJ → Pröva kreativ omskrivning eller kombinera metoder
```

> ⚠️ **Från föreläsningen:** "Det kan vara svårt att beräkna primitiv. Testa därför gärna ditt resultat F(x) genom att beräkna derivatan F'(x) — vilket är enkelt!"

---

## 🎯 Checklista: Vad du bör kunna

### Kapitel 5.1 — Primitiva funktioner

- [ ] Definitionen av primitiv funktion (F'(x) = f(x))
- [ ] Entydighet: alla primitiver skiljer sig med en konstant C
- [ ] **Alla 12 standardprimitiverna utantill!**
- [ ] Räknereglerna (15)–(16): linjäritet
- [ ] Formlerna (13)–(14): f'/f-typen och f^α · f'-typen
- [ ] **Variabelsubstitution:** identifiera u, beräkna du, byt, integrera, byt tillbaka
- [ ] Vanliga substitutionstyper: linjär, kvadratisk, sin/cos, trigonometrisk
- [ ] **Partialintegration:** formeln ∫ fg dx = Fg − ∫ Fg' dx
- [ ] LIATE-regeln för val av g
- [ ] Tricket "gånger 1" (för ln x, arctan x, etc.)
- [ ] Det cirkulära tricket (för eˣ sin/cos)

### Kapitel 5.2 — Rationella funktioner

- [ ] De fyra stegen: polynomdivision → faktorisering → partialbraksuppdelning → integration
- [ ] Korrekt ansats för partialbraksuppdelning (linjära och kvadratiska faktorer, multipliciteter)
- [ ] Bestämma koefficienter (ekvationssystem och/eller handpåläggning)
- [ ] Integrera de fyra elementära bråktyperna
- [ ] Kvadratkomplettering för andragradsfaktorer

---

## 📌 Formler att memorera

| Formel | Beskrivning |
|--------|-------------|
| ∫ xᵅ dx = xᵅ⁺¹/(α+1) + C | Potensregel (α ≠ −1) |
| ∫ 1/x dx = ln\|x\| + C | Logaritmregel |
| ∫ eˣ dx = eˣ + C | Exponentialfunktion |
| ∫ cos x dx = sin x + C | |
| ∫ sin x dx = −cos x + C | OBS minustecken! |
| ∫ 1/(1+x²) dx = arctan x + C | |
| ∫ 1/√(1−x²) dx = arcsin x + C | |
| ∫ 1/√(x²+α) dx = ln\|x+√(x²+α)\| + C | |
| ∫ f'(x)/f(x) dx = ln\|f(x)\| + C | "Derivatan i täljaren" |
| ∫ f(x)ᵅ f'(x) dx = f(x)ᵅ⁺¹/(α+1) + C | Potenskedjeregel |
| ∫ f·g dx = F·g − ∫ F·g' dx | Partialintegration |
| ∫ f(kx+m) dx = (1/k) F(kx+m) + C | Linjär substitution |
| ∫ 1/(x−a) dx = ln\|x−a\| + C | Partialbråk typ 1 |
| ∫ 1/(t²+a) dt = (1/√a) arctan(t/√a) + C | Partialbråk typ 3 |
