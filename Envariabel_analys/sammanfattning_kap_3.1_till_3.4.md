# 📐 Kapitel 3.1–3.4 — Derivator: Introduktion, Definition, Räkneregler & Elementära derivator

## Omfattande sammanfattning och genomgång

---

# 🔷 KAPITEL 3.1 — Introduktion till begreppet derivata

## Motiverande exempel: Temperaturfördelning

Många praktiska frågeställningar handlar om hur **snabbt** ett visst förlopp ändras:

- "Hur fort kör bilen?"
- "Hur snabbt sjunker lufttrycket med stigande höjd?"
- "Hur snabbt sönderfaller ett radioaktivt ämne?"
- "Hur mycket ökar skatten med växande inkomst?"

Vi vill skaffa oss ett matematiskt verktyg som mäter **hastigheten** i dylika förändringar.

### Det konkreta exemplet

Låt f(x) beteckna temperaturfördelningen längs en tunn stav placerad utefter x-axeln (temperaturen i °C, längden i meter). Frågan: *Hur snabbt ändrar sig temperaturen vid en viss punkt x₀?*

**Steg 1 — Genomsnittlig ändring (differenskvot):**

Från punkten x₀ till en närbelägen punkt x₀ + h har temperaturen ändrats med f(x₀ + h) − f(x₀) grader. I intervallet med ändpunkterna x₀ och x₀ + h är alltså temperaturökningen i *genomsnitt*:

```
(1)     [f(x₀ + h) − f(x₀)] / h       grader per meter
```

Detta uttryck (1) ger inget precist svar på den ställda frågan om hur stor tillväxthastigheten är i *just* punkten x₀, men ju mindre intervall (dvs. ju mindre värde på |h|) vi använder, desto närmare bör vi komma en exakt angivelse.

**Steg 2 — Gränsvärde ger exakt ändring:**

Om gränsvärdet

```
(2)     lim(h→0) [f(x₀ + h) − f(x₀)] / h
```

existerar, är det därför rimligt att betrakta detta som mätetalet för temperaturens ändringstakt i punkten x₀. Gränsvärdet (2) utgör alltså det uttryck vi letar efter.

---

### Exempel 1: f(x) = √x

**Uppgift:** Bestäm temperaturens tillväxthastighet (i °C/m) i punkten x = 1.

**Lösning:** Vi behöver bestämma gränsvärdet:

```
lim(h→0) [f(1+h) − f(1)] / h = lim(h→0) [√(1+h) − 1] / h
```

Förlängning med konjugatkvantiteten ger:

```
[√(1+h) − 1] / h = [√(1+h) − 1][√(1+h) + 1] / [h(√(1+h) + 1)]
                  = [(1+h) − 1] / [h(√(1+h) + 1)]
                  = 1 / [√(1+h) + 1]
                  → 1/2     då h → 0.
```

**Svar:** Temperaturen växer med hastigheten 1/2 grad per meter i x = 1. Ett negativt resultat skulle ha inneburit en motsvarande *minskning*.

---

## Geometrisk tolkning av differenskvoten

**Differenskvoten** [f(x₀ + h) − f(x₀)] / h har en viktig geometrisk tolkning:

Den är **riktningskoefficienten** (lutningen) för den **sekant** ℓ som går genom punkterna (x₀, f(x₀)) och (x₀ + h, f(x₀ + h)) på funktionskurvan y = f(x).

Om gränsvärdet (2) existerar kommer sekanten att få ett gränsläge t när h → 0. Denna gränslinje kallas man **tangent** till kurvan y = f(x) i punkten (x₀, f(x₀)).

> 🎯 **Sammanfattning av den dubbla tolkningen:**
>
> Gränsvärdet (2) = derivatan =
> - **Fysikaliskt:** ändringstakten (tillväxthastigheten) hos f i punkten x₀
> - **Geometriskt:** riktningskoefficienten (lutningen) för tangenten till y = f(x) i (x₀, f(x₀))

---

---

# 🔷 KAPITEL 3.2 — Derivatans definition

## Definition 1 — Den formella definitionen

> **DEFINITION 1.** Antag att funktionen f är definierad i en omgivning av punkten x₀. Om gränsvärdet
>
> ```
> lim(h→0) [f(x₀ + h) − f(x₀)] / h
> ```
>
> existerar, så säges f vara **deriverbar i punkten x₀**. Gränsvärdet kallas **derivatan av f i x₀** och betecknas
>
> ```
> f'(x₀),     df/dx(x₀)     eller     Df(x₀).
> ```

Om en funktion f är deriverbar i **varje punkt** i sin definitionsmängd säger vi kortfattat att f är **deriverbar**. *Funktionen*

```
x ↦ f'(x),     x ∈ Df
```

kallas **derivatan av f**. Alternativa beteckningar:

```
f',     df/dx,     Df
```

I samband med funktionskurvan y = f(x) används också skrivsätten:

```
y'     och     dy/dx
```

---

## Grundexempel — derivatan beräknad direkt ur definitionen

### Exempel 2: Linjär funktion f(x) = ax + b

```
[f(x₀ + h) − f(x₀)] / h = [a(x₀ + h) + b − (ax₀ + b)] / h = ah/h = a → a
```

Alltså: **f'(x) = a** för alla x₀ ∈ ℝ.

> 💡 Speciellt: derivatan av en **konstant funktion** (a = 0) är identiskt noll. Det stämmer med att en konstant funktion inte ändrar sig alls.

### Exempel 3: f(x) = c√x, x > 0

```
[f(x₀ + h) − f(x₀)] / h = c · [√(x₀ + h) − √x₀] / h
```

Konjugatförlängning:

```
= c · [(x₀ + h) − x₀] / [h(√(x₀ + h) + √x₀)] = c / [√(x₀ + h) + √x₀] → c/(2√x₀)
```

Alltså: **f'(x) = c/(2√x)**

### Exempel 4: Monompotens f(x) = xⁿ (n positivt heltal)

Med binomialsatsen:

```
[(x₀ + h)ⁿ − x₀ⁿ] / h = [x₀ⁿ + C(n,1)·x₀ⁿ⁻¹·h + C(n,2)·x₀ⁿ⁻²·h² + ... + hⁿ − x₀ⁿ] / h
                         = nx₀ⁿ⁻¹ + C(n,2)·x₀ⁿ⁻²·h + ... + hⁿ⁻¹
```

Alla termer utom den första har gränsvärdet 0 då h → 0. Alltså:

```
D(xⁿ) = nxⁿ⁻¹
```

> 🎯 **Denna formel — D(xⁿ) = nxⁿ⁻¹ — är en av de viktigaste i kursen.** Den generaliseras senare (i sats 8, avsnitt 3.4) till alla reella exponenter α.

---

## Geometrisk tolkning — Tangent och normal

### Tangentens ekvation

Vi *definierar* **tangenten** i punkten (x₀, f(x₀)) som den räta linje vars ekvation är:

```
(3)     y − f(x₀) = f'(x₀)(x − x₀)
```

Man talar också om f'(x₀) som funktionskurvans **lutning** eller **branthet** i punkten (x₀, f(x₀)).

### Normalens ekvation

Om en rät linje har riktningskoefficienten a ≠ 0 så har en **normal** (vinkelrät linje) till densamma riktningskoefficienten −1/a. Normalen i punkten (x₀, f(x₀)) har alltså ekvationen:

```
y − f(x₀) = −(1/f'(x₀)) · (x − x₀)
```

### Exempel 5: Tangent till y = √x i (9, 3)

Derivatan: dy/dx = 1/(2√x). I x = 9: f'(9) = 1/(2√9) = 1/6.

Tangentens ekvation: y − 3 = (1/6)(x − 9), dvs. **x − 6y + 9 = 0**.

### Exempel 6: Normal i samma punkt

Normalens riktningskoefficient: −1/(1/6) = −6.

Normalen: y − 3 = (−6)(x − 9), dvs. **y + 6x − 57 = 0**.

---

## Derivator i tillämpningarna

De flesta fysikaliska och tekniska tillämpningar bygger på tolkningen:

> **Den hastighet varmed ett visst förlopp y = f(x) tillväxer i en viss punkt x₀ anges av derivatan f'(x₀) i denna punkt.**

**Enheten** för förloppets tillväxthastighet beror på enheterna för x och y i sambandet y = f(x):

| Förlopp y = f(x) | Derivata f'(x₀) | Enhet |
|---|---|---|
| Vägsträcka s(t) [m] som funktion av tid t [s] | s'(t) = momentan hastighet | m/s |
| Radioaktiv massa y(t) [kg] som funktion av tid t [s] | −y'(t) = sönderfallshastighet | kg/s |
| Temperatur f(x) [°C] längs stav vid position x [m] | f'(x) = temperaturstegring | °C/m |

> 💡 Observera minustecknet: om f'(x₀) < 0 innebär det att funktionen *avtar*, dvs. en minskning.

### Exempel 7: Vatten i en triangulär ränna

Ett kärl har formen av en horisontell triangulär ränna med mått enligt figur. Vid tiden t = 0 börjar rännan tappas vatten med en konstant hastighet av 3 m³ per timme. Vattennivån y(t) sökes som funktion av tiden.

**Lösning:** Av likformiga trianglar: vattenytans bredd = y(t) (lika med nivån). Vattenvolymen efter t timmar:

```
3t = [y(t) · y(t) / 2] · 4 = 2y(t)²
```

Alltså: y(t) = √(3t/2).

Derivatan beräknas med c = √(3/2) enligt exempel 3:

```
y'(t) = (1/2)√(3/2) · 1/√t
```

> 💡 Derivatan y'(t) anger hur snabbt vattennivån stiger vid tidpunkten t (meter per timme). Notera att y'(t) → ∞ då t → 0⁺ (vattnet stiger snabbt i den smala botten) och y'(t) → 0 då t → ∞ (stiger långsammare när rännan blir bredare).

---

## Andraderivata

Det kan naturligtvis finnas anledning att studera tillväxthastigheten hos derivatan f' av en funktion f. Man ska då bilda (f')'. Denna funktion kallas **andraderivatan** av f och betecknas på endera av sätten:

```
f'',     f⁽²⁾,     D²f     och     d²f/dx²
```

Enligt sin definition mäter f''(x) *hur snabbt tillväxthastigheten ökar i punkten x*. Detta brukar man kalla **accelerationen** hos förloppet f(x).

| Förlopp | Derivata | Andraderivata | Enhet |
|---|---|---|---|
| Vägsträcka s(t) | s'(t) = hastighet [m/s] | s''(t) = acceleration [m/s²] |
| Temperatur f(x) | f'(x) = temp.stegring [°C/m] | f''(x) [°C/m²] |

### Exempel 8: Rätlinjigt förlopp

f(x) = ax + b har f'(x) = a (konstant) och f''(x) = 0. Ett rätlinjigt förlopp har konstant tillväxthastighet och noll acceleration.

---

---

# 🔷 KAPITEL 3.3 — Derivationsregler

## Deriverbarhet och kontinuitet

### Sats 1: Deriverbar ⟹ Kontinuerlig

> **SATS 1.** *Om en funktion f är deriverbar så är den kontinuerlig.*

**Bevis:** Antag att f är deriverbar i x₀ ∈ Df. Enligt definitionen ska vi visa att f(x₀ + h) → f(x₀) då h → 0. Men:

```
f(x₀ + h) − f(x₀) = [f(x₀ + h) − f(x₀)] / h · h → f'(x₀) · 0 = 0     då h → 0.
```

Detta visar satsen. ∎

> ⚠️ **VIKTIGT: Omvändningen gäller INTE!**
>
> En funktion kan vara kontinuerlig utan att vara deriverbar. Det klassiska exemplet är f(x) = |x|:
>
> - f är **kontinuerlig** i x = 0 (ingen diskontinuitet)
> - f är **inte deriverbar** i x = 0 (grafen har en spets)
>
> Vi visar detta: För h > 0: [f(0+h) − f(0)] / h = |h|/h = h/h = 1 → 1
> Men för h < 0: [f(0+h) − f(0)] / h = |h|/h = −h/h = −1 → −1
>
> Höger- och vänstergränsvärdet av differenskvoten existerar men är **olika** (1 resp. −1), alltså existerar inte gränsvärdet och f är inte deriverbar i x = 0.

### Vänster- och högerderivata

När vänster- respektive högergränsvärdet av differenskvoten existerar var för sig talar man om **vänsterderivatan** respektive **högerderivatan** av f.

f är deriverbar i en punkt precis när **både** vänster- och högerderivatan existerar **och de är lika**.

### Deriverbarhet i slutna intervall

Man talar ibland om deriverbara funktioner i slutna intervall [a, b]. Då kräver man att f är deriverbar i a < x < b samt att högerderivatan existerar i a och vänsterderivatan existerar i b.

---

## Algebraiska räkneregler

### Sats 2: De fyra grundläggande derivationsreglerna

> **SATS 2.** *Låt f och g vara deriverbara funktioner och α en konstant. Då är funktionerna αf, f+g, fg och f/g deriverbara i sina respektive definitionsmängder, och vi har följande formler:*

```
(4)     (αf)'(x) = αf'(x)                                          [Konstant faktor]

(5)     (f + g)'(x) = f'(x) + g'(x)                                [Summaregeln]

(6)     (fg)'(x) = f'(x)g(x) + f(x)g'(x)                          [Produktregeln]

(7)     (f/g)'(x) = [f'(x)g(x) − f(x)g'(x)] / g(x)²              [Kvotregeln]
```

> 🎯 **Minneshjälp för produktregeln (6):**
> "Derivatan av en produkt = (första deriverad) · (andra orörd) + (första orörd) · (andra deriverad)"
>
> 🎯 **Minneshjälp för kvotregeln (7):**
> "Täljare-prim gånger nämnare minus täljare gånger nämnare-prim, delat med nämnaren i kvadrat"

### Bevisidéer

**(4):** Specialfall av (6) med g(x) = α (konstant).

**(5):** Differenskvoten för f + g:

```
[f(x+h) + g(x+h)] − [f(x) + g(x)]     f(x+h) − f(x)     g(x+h) − g(x)
─────────────────────────────────── = ───────────────── + ─────────────────
                h                            h                    h
→ f'(x) + g'(x)     då h → 0.
```

**(6):** Tricket: lägg till och dra ifrån f(x)g(x+h) i täljaren:

```
f(x+h)g(x+h) − f(x)g(x)     [f(x+h) − f(x)]·g(x+h) + f(x)·[g(x+h) − g(x)]
───────────────────────── = ──────────────────────────────────────────────────
            h                                        h
```

Eftersom g är kontinuerlig (sats 1) gäller g(x+h) → g(x), så högerledet → f'(x)g(x) + f(x)g'(x).

**(7):** Visa först att D(1/g(x)) = −g'(x)/g(x)²:

```
[1/g(x+h) − 1/g(x)] / h = [g(x) − g(x+h)] / [h · g(x) · g(x+h)]
                          → −g'(x)/g(x)²
```

Sedan: f/g = f · (1/g), tillämpa produktregeln (6).

> 💡 Observera att man behöver g(x) ≠ 0 i kvotregeln, på grund av g(x)² i nämnaren. Att g(x+h) ≠ 0 för tillräckligt små |h| garanteras av att g är kontinuerlig (sats 1).

### Anmärkningar och utvidgningar

**Summaregeln utvidgas** till godtyckligt antal termer:

```
D(f₁ + f₂ + ... + fₙ) = f₁' + f₂' + ... + fₙ'
```

**Produktregeln utvidgas** (induktionsbevis) till n faktorer:

```
D(f₁ · f₂ · ... · fₙ) = f₁'f₂...fₙ + f₁f₂'...fₙ + ... + f₁f₂...fₙ'
```

Speciellt för n = 3:

```
(9)     D(f₁f₂f₃) = f₁'f₂f₃ + f₁f₂'f₃ + f₁f₂f₃'
```

> 💡 **Mönstret:** Derivera en faktor i taget, lämna de övriga orörda, och summera alla sådana termer.

---

### Exempel 9: Derivata av polynom

Derivationsreglerna (4) och (5) samt formeln D(xⁿ) = nxⁿ⁻¹ visar att varje polynom

```
p(x) = aₙxⁿ + aₙ₋₁xⁿ⁻¹ + ... + a₁x + a₀
```

är deriverbart och att

```
p'(x) = aₙnxⁿ⁻¹ + aₙ₋₁(n−1)xⁿ⁻² + ... + a₁
```

> 💡 **Derivation av ett polynom sänker alltså gradtalet med en enhet.** Ett polynom av grad n har en derivata av grad n−1.

### Exempel 10: Produktregeln i praktiken

```
D[(7x² + 9x³)√x] = (14x + 27x²)√x + (7x² + 9x³) · 1/(2√x)
                   = (1/2)x^(3/2)(35 + 63x)
```

### Exempel 11: Kvotregeln i praktiken

```
D[(3x + x²)/(1 + x²)] = [(3 + 2x)(1 + x²) − (3x + x²)(2x)] / (1 + x²)²
                        = [3 + 2x − 3x²] / (1 + x²)²
```

---

## Derivation av sammansatt funktion — Kedjeregeln

### Sats 3 (Kedjeregeln)

> **SATS 3.** *(KEDJEREGELN) Om funktionen g är deriverbar i punkten x och funktionen f är deriverbar i punkten g(x), så är den sammansatta funktionen u(x) = f(g(x)) deriverbar i punkten x och*
>
> ```
> (10)     u'(x) = f'(g(x)) · g'(x)
> ```

> 🎯 **I ord:** Derivatan av en sammansatt funktion = (yttre funktionens derivata, utvärderad i den inre funktionen) × (inre funktionens derivata).
>
> Eller kortare: **"Yttre derivata gånger inre derivata"**.

### Bevis (skiss)

**Förenklade fallet:** Anta att g(x+h) ≠ g(x) för alla tillräckligt små h ≠ 0. Sätt k = g(x+h) − g(x). Omskrivning:

```
[u(x+h) − u(x)] / h = [f(g(x+h)) − f(g(x))] / h
                      = [f(g(x+h)) − f(g(x))] / [g(x+h) − g(x)] · [g(x+h) − g(x)] / h
```

Det första bråket → f'(g(x)) (differenskvot för f i punkten g(x) med tillskottet k → 0). Det andra → g'(x). Satsen följer.

**Allmänna fallet:** Om g(x+h) = g(x) för vissa h nära 0 kräver beviset ett tekniskt knep: definiera

```
r(k) = { [f(g(x) + k) − f(g(x))] / k     om k ≠ 0
        { f'(g(x))                          om k = 0
```

Då r(k) → f'(g(x)) då k → 0 (r är kontinuerlig i k = 0). Nu kan omskrivningen [u(x+h) − u(x)] / h = r(g(x+h) − g(x)) · [g(x+h) − g(x)] / h användas oavsett om g(x+h) − g(x) = 0 eller ej. Gränsövergång ger f'(g(x)) · g'(x). ∎

---

### Exempel 12: Kedjeregeln — (x² + 1)ⁿ

```
u(x) = (x² + 1)ⁿ
```

Yttre funktion: f(t) = tⁿ med f'(t) = ntⁿ⁻¹. Inre funktion: g(x) = x² + 1 med g'(x) = 2x.

```
u'(x) = n(x² + 1)ⁿ⁻¹ · 2x
```

### Exempel 13: Nästlade kedjeregeltillämpningar

Derivatan av den inre funktionen g(x) i kedjeregeln kallas ibland "inre derivatan". Om även g(x) är en sammansatt funktion måste den inre derivatan i sin tur beräknas med hjälp av kedjeregeln. Slutresultatet kan bli ett uttryck innehållande **flera** olika inre derivator.

```
D(√(x² + 1) + x)⁴ = 4(√(x² + 1) + x)³ · D(√(x² + 1) + x)
                    = 4(√(x² + 1) + x)³ · (1/(2√(x² + 1)) · 2x + 1)
                    = 4(√(x² + 1) + x)³ · (x/√(x² + 1) + 1)
```

### Exempel 14: Implicit derivering — avstånd mellan fartyg

Två fartyg A och B rör sig i rät linje från punkten O med vinkel AOB = 120°. Sträckan OA = x(t) = 8 sjömil (v = 10 knop) och OB = y(t) = 6 sjömil (v = 20 knop). Hur snabbt ändras avståndet d(t)?

**Lösning:** Cosinussatsen ger:

```
(11)     d(t)² = x(t)² + y(t)² − 2x(t)y(t)cos 120° = x(t)² + y(t)² + x(t)y(t)
```

Derivera *båda sidor* med avseende på t (produktregeln + kedjeregeln):

```
(12)     2d(t)·d'(t) = 2x(t)x'(t) + 2y(t)y'(t) + x'(t)y(t) + x(t)y'(t)
```

Vid aktuell tidpunkt: x = 8, y = 6, x' = 10, y' = 20.

Från (11): d² = 64 + 36 + 48 = 148, dvs. d = √148 = 2√37.

Insättning i (12): 2·2√37·d'(t) = 2·8·10 + 2·6·20 + 10·6 + 8·20 = 160 + 240 + 60 + 160 = 620.

Alltså: d'(t) = 620 / (4√37) = 155/√37 ≈ 25.5 knop.

> 💡 **Implicit derivering** innebär att man deriverar en relation (som (11)) direkt med avseende på t, utan att först lösa ut den okända funktionen. Kedjeregeln tillämpas "automatiskt" på alla termer.

---

### Kedjeregeln i Leibniz-notation

Om u = u(y(x)), kan kedjeregeln (10) skrivas suggestivt:

```
du/dx = (du/dy) · (dy/dx)
```

> 💡 Det ser ut som om dy "förkortas bort" — men detta är bara en **minnesregel**, inte ett äkta bråk! De mer utförliga men entydiga formlerna (10) och (13) ger mer information om i vilka punkter derivatorna ska beräknas.

---

## Derivata av invers funktion

### Sats 4

> **SATS 4.** *Antag att funktionen f har en invers funktion som är kontinuerlig. Om f är deriverbar i en punkt x och om f'(x) ≠ 0 så är f⁻¹ deriverbar i punkten y = f(x) och*
>
> ```
> (13)     (Df⁻¹)(y) = 1 / f'(x)
> ```

### Bevis

Låt k ≠ 0 vara ett litet tillskott till y. Sätt y + k = f(x + h), alltså h = f⁻¹(y + k) − f⁻¹(y). Eftersom f⁻¹ antas kontinuerlig: h → 0 då k → 0. Differenskvoten:

```
[f⁻¹(y + k) − f⁻¹(y)] / k = h / [f(x + h) − f(x)] = 1 / {[f(x + h) − f(x)] / h}
→ 1 / f'(x)     då k → 0.
```

∎

### I Leibniz-notation

Om y = f(x) och x = f⁻¹(y), dvs. x = x(y), kan regeln skrivas:

```
dx/dy = 1 / (dy/dx)
```

> ⚠️ Var uppmärksam: dy/dx beräknas i punkten x, men dx/dy beräknas i punkten y = f(x). Dessa är olika punkter!

### Geometrisk tolkning

Tangenten till kurvan y = f(x) har lutning tan α = f'(x). Tangenten till inversen x = f⁻¹(y) (samma kurva!) har lutning tan β = 1/f'(x). Ur triangeln ser vi att α + β = π/2, dvs. β = π/2 − α, och tan β = cot α = 1/tan α. ✓

### Exempel 15: Derivatan av x^(1/n)

Funktionen x = y^(1/n) är invers till y = xⁿ (x > 0). Enligt sats 4 och D(xⁿ) = nxⁿ⁻¹:

```
dx/dy = 1 / (dy/dx) = 1 / (nxⁿ⁻¹)
```

Uttryckt i y: x = y^(1/n), alltså xⁿ⁻¹ = (y^(1/n))ⁿ⁻¹ = y^((n−1)/n):

```
d/dy(y^(1/n)) = 1 / (n · y^((n−1)/n)) = (1/n) · y^(1/n − 1)
```

Med byte av beteckningar:

```
d/dx(x^(1/n)) = (1/n) · x^(1/n − 1)
```

> 🎯 Alltså gäller formeln D(xᵅ) = αxᵅ⁻¹ även för exponenten α = 1/n. (Vi visar i nästa avsnitt att den gäller för *alla* reella α.)

---

---

# 🔷 KAPITEL 3.4 — De elementära funktionernas derivator

Nu ska vi systematiskt härleda alla de elementära funktionernas derivator med hjälp av derivatans definition, kedjeregeln och satsen om inversens derivata.

---

## Polynom och rationella funktioner

Vi har redan sett (exempel 9) att varje polynom

```
p(x) = aₙxⁿ + aₙ₋₁xⁿ⁻¹ + ... + a₁x + a₀
```

är deriverbart med

```
p'(x) = aₙnxⁿ⁻¹ + aₙ₋₁(n−1)xⁿ⁻² + ... + a₁
```

Enligt kvotregeln är därför varje rationell funktion r(x) = p(x)/q(x) (p, q polynom) deriverbar i alla punkter x där q(x) ≠ 0, med

```
r'(x) = [p'(x)q(x) − p(x)q'(x)] / q(x)²
```

---

## Exponential-, logaritm- och potensfunktioner

### Sats 5: Exponentialfunktionen eˣ

> **SATS 5.** *Exponentialfunktionen eˣ är deriverbar med*
>
> ```
> (14)     D eˣ = eˣ
> ```

**Bevis:** Differenskvoten:

```
[e^(x+h) − eˣ] / h = eˣ · (eʰ − 1) / h
```

Enligt standardgränsvärdet (2.29): (eʰ − 1)/h → 1 då h → 0. Alltså har differenskvoten gränsvärdet eˣ. ∎

> 🎯 **eˣ är sin egen derivata!** Detta är en helt unik egenskap — ingen annan funktion (förutom skalade versioner ceˣ) har den. Det är denna egenskap som gör e till den "naturliga" basen.

### Exempel 16: Kedjeregeln med eˣ

```
f(x) = √(1 + 2e^(x²))
f'(x) = 1/(2√(1 + 2e^(x²))) · 2 · e^(x²) · 2x = 2xe^(x²) / √(1 + 2e^(x²))
```

---

### Sats 6: Naturliga logaritmen ln x

> **SATS 6.** *Den naturliga logaritmfunktionen ln x är deriverbar med*
>
> ```
> (15)     D ln x = 1/x,     x > 0
> ```

**Bevis:** Räknelagarna för logaritmer och standardgränsvärdet (2.28):

```
[ln(x + h) − ln x] / h = (1/h) · ln[(x + h)/x] = (1/x) · ln(1 + h/x) / (h/x)
→ (1/x) · 1 = 1/x     då h → 0.
```

∎

> 🎯 **Derivatan av ln x = 1/x.** Denna koppling mellan logaritm och 1/x är fundamental. Tillsammans med D eˣ = eˣ bekräftar den att e är den naturligaste basen.

---

### Följdsats 1: Allmänna exponential- och logaritmfunktioner

> *De allmänna exponential- och logaritmfunktionerna aˣ och ᵃlog x är deriverbara med:*
>
> ```
> D aˣ = aˣ · ln a
>
> D ᵃlog x = 1/(x · ln a),     x > 0
> ```

**Bevis:** Omskrivningen aˣ = e^(x ln a) och kedjeregeln ger D aˣ = e^(x ln a) · ln a = aˣ ln a.

Den andra formeln: ᵃlog x = ln x / ln a (basbytesformeln), derivera direkt.

> 💡 Genom dessa satser ser vi **varför talet e** är den matematiskt sett naturligaste basen: derivationsformlerna är enklast i denna bas (ln a-faktorn försvinner).

---

### Sats 7: Funktionen ln |x|

> **SATS 7.** *Funktionen ln |x| är deriverbar med*
>
> ```
> (16)     D ln |x| = 1/x,     x ≠ 0
> ```
>
> *Om funktionen f(x) är deriverbar och f(x) ≠ 0 så är ln |f(x)| deriverbar med*
>
> ```
> (17)     D ln |f(x)| = f'(x)/f(x)
> ```

**Bevis:** ln |x| = ln x om x > 0 (derivata 1/x direkt) och ln |x| = ln(−x) om x < 0 (kedjeregeln: (1/(−x)) · (−1) = 1/x). Formel (17) följer av (16) och kedjeregeln.

> 💡 Formel (17) är extremt användbar vid **logaritmisk derivering** (se nedan).

---

### Logaritmisk derivering

> **Metod:** Om f(x) = f₁(x) · f₂(x) · f₃(x) (en produkt av funktioner), ta absolutbeloppet, logaritmera och derivera:
>
> ```
> ln |f(x)| = ln |f₁(x)| + ln |f₂(x)| + ln |f₃(x)|
> ```
>
> Derivering ger:
>
> ```
> f'(x)/f(x) = f₁'(x)/f₁(x) + f₂'(x)/f₂(x) + f₃'(x)/f₃(x)
> ```

Genom att multiplicera båda leden med f(x) ser vi att resultatet överensstämmer med den utvidgade produktregeln (9).

> 🎯 Logaritmisk derivering är speciellt användbar för produkter av *många* faktorer och för funktioner på formen g(x)^(h(x)) (variabel bas och variabel exponent).

---

### Sats 8: Potensfunktionen xᵅ (allmän reell exponent)

> **SATS 8.** *Potensfunktionen xᵅ är deriverbar med*
>
> ```
> (18)     D xᵅ = αxᵅ⁻¹,     x > 0
> ```

**Bevis:** Omskrivningen xᵅ = e^(α ln x) visar att xᵅ är en sammansättning av exponential- och logaritmfunktionen. Kedjeregeln ger:

```
D xᵅ = D e^(α ln x) = e^(α ln x) · D(α ln x) = xᵅ · α/x = αxᵅ⁻¹
```

∎

> 🎯 **Formeln D(xᵅ) = αxᵅ⁻¹ gäller nu för ALLA reella exponenter α** — inte bara positiva heltal. Den gäller för α = 1/2 (derivatan av √x), α = −1 (derivatan av 1/x), α = π, etc.

### Exempel 18: Irrationell exponent

D(x^√3) = √3 · x^(√3 − 1). Och D(x^(2/3)) = (2/3) · x^(2/3 − 1) = 2/(3x^(1/3)).

---

### Exempel 19: Funktioner på formen g(x)^(h(x))

Omskrivningen i beviset för sats 8 är effektiv vid derivation av *alla* funktioner av formen g(x)^(h(x)):

```
D[g(x)^(h(x))] = D[e^(h(x) ln g(x))] = e^(h(x) ln g(x)) · D[h(x) ln g(x)]
               = g(x)^(h(x)) · [h'(x) ln g(x) + h(x) · g'(x)/g(x)]
```

> 💡 Funktionen xˣ, som varken är en ren exponentialfunktion eller ren potensfunktion, får derivatan:
>
> D xˣ = D e^(x ln x) = e^(x ln x) · D(x ln x) = xˣ · (1 + ln x)

---

## Trigonometriska funktioner och arcusfunktioner

### Sats 9: De trigonometriska funktionerna

> **SATS 9.** *De trigonometriska funktionerna är deriverbara med*
>
> ```
> (19)     D sin x = cos x
>
> (20)     D cos x = −sin x
>
> (21)     D tan x = 1/cos²x,          x ≠ π/2 + nπ
>
> (22)     D cot x = −1/sin²x,         x ≠ nπ
> ```

**Bevis av (19):** Med trigonometriska formeln sin A − sin B = 2 cos((A+B)/2) sin((A−B)/2):

```
[sin(x + h) − sin x] / h = (2/h) · cos(x + h/2) · sin(h/2) = cos(x + h/2) · sin(h/2)/(h/2)
```

Den andra faktorn → 1 då h → 0 (standardgränsvärde (2.26)). Cosinusfunktionen är kontinuerlig, alltså cos(x + h/2) → cos x. ✓

**Bevis av (20):** Skriv cos x = sin(π/2 − x) och kedjeregeln:

```
D cos x = D sin(π/2 − x) = cos(π/2 − x) · (−1) = −sin x
```

**Formler (21) och (22):** Följer direkt av kvotregeln:

```
D tan x = D(sin x/cos x) = [cos x · cos x − sin x · (−sin x)] / cos²x = (cos²x + sin²x)/cos²x = 1/cos²x
```

> 💡 **Anmärkning:** Med trigonometriska ettan (cos²x + sin²x = 1) i täljaren i (21) kan man också skriva:
>
> ```
> D tan x = 1 + tan²x
> ```
>
> Denna alternativa form är ibland behändig.

---

### Sats 10: Arcusfunktionerna arcsin och arccos

> **SATS 10.** *Funktionerna arcsin x och arccos x är deriverbara i intervallet −1 < x < 1 med*
>
> ```
> (23)     D arcsin x = 1/√(1 − x²)
>
> (24)     D arccos x = −1/√(1 − x²)
> ```

**Bevis av (23):** y = arcsin x är invers till x = sin y, −π/2 < y < π/2. Sats 4 ger:

```
dy/dx = 1/(dx/dy) = 1/cos y = 1/√(1 − sin²y) = 1/√(1 − x²)
```

Här utnyttjades att cos y > 0 (positiv i intervallet −π/2 < y < π/2).

**Formel (24)** följer av (23) och arccos x = π/2 − arcsin x:

```
D arccos x = D(π/2 − arcsin x) = −D arcsin x = −1/√(1 − x²)
```

---

### Sats 11: arctan och arccot

> **SATS 11.** *Funktionerna arctan x och arccot x är deriverbara med*
>
> ```
> (25)     D arctan x = 1/(1 + x²)
>
> (26)     D arccot x = −1/(1 + x²)
> ```

**Bevis av (25):** y = arctan x är invers till x = tan y, −π/2 < y < π/2. Enligt sats 4 och formel (21):

```
dy/dx = 1/(dx/dy) = 1/(1/cos²y) = cos²y
```

Men cos²y = cos²y / (cos²y + sin²y) = 1/(1 + tan²y) = 1/(1 + x²).

Formel (26) följer av arccot x = π/2 − arctan x. ∎

---

## Hyperboliska funktioner

### Sats 12: Derivator av hyperboliska funktioner

> **SATS 12.** *De hyperboliska funktionerna är deriverbara med*
>
> ```
> D sinh x = cosh x
>
> D cosh x = sinh x
>
> D tanh x = 1/cosh²x
>
> D coth x = −1/sinh²x,     x ≠ 0
> ```

> 💡 Lägg märke till den slående **likheten** mellan de hyperboliska och de trigonometriska funktionernas derivator! Skillnaden är bara i **tecknen**: D cos x = −sin x men D cosh x = +sinh x, och D cot x = −1/sin²x men D coth x = −1/sinh²x.

Bevisen utgår direkt från definitionerna sinh x = (eˣ − e⁻ˣ)/2 och cosh x = (eˣ + e⁻ˣ)/2, och lämnas som övning.

---

## 📊 Komplett tabell: Alla elementära derivator

### Potensfunktioner och polynom

| Funktion      | Derivata | Giltighetsområde  |
| ------------- | -------- | ----------------- |
| xᵅ            | αxᵅ⁻¹    | x > 0 (allmänt α) |
| xⁿ (heltal n) | nxⁿ⁻¹    | x ∈ ℝ (n ≥ 1)     |
| √x            | 1/(2√x)  | x > 0             |
| 1/x           | −1/x²    | x ≠ 0             |

### Exponential- och logaritmfunktioner

| Funktion    | Derivata   | Giltighetsområde    |
| ----------- | ---------- | ------------------- |
| eˣ          | eˣ         | x ∈ ℝ               |
| aˣ          | aˣ · ln a  | x ∈ ℝ, a > 0        |
| ln x        | 1/x        | x > 0               |
| ln \|x\|    | 1/x        | x ≠ 0               |
| ᵃlog x      | 1/(x ln a) | x > 0, a > 0, a ≠ 1 |
| ln \|f(x)\| | f'(x)/f(x) | f(x) ≠ 0            |

### Trigonometriska funktioner

| Funktion | Derivata            | Undantag     |
| -------- | ------------------- | ------------ |
| sin x    | cos x               | —            |
| cos x    | −sin x              | —            |
| tan x    | 1/cos²x = 1 + tan²x | x ≠ π/2 + nπ |
| cot x    | −1/sin²x            | x ≠ nπ       |

### Arcusfunktioner (inversa trigonometriska)

| Funktion | Derivata     | Giltighetsområde |
| -------- | ------------ | ---------------- |
| arcsin x | 1/√(1 − x²)  | −1 < x < 1       |
| arccos x | −1/√(1 − x²) | −1 < x < 1       |
| arctan x | 1/(1 + x²)   | x ∈ ℝ            |
| arccot x | −1/(1 + x²)  | x ∈ ℝ            |

### Hyperboliska funktioner

| Funktion | Derivata  | Undantag |
| -------- | --------- | -------- |
| sinh x   | cosh x    | —        |
| cosh x   | sinh x    | —        |
| tanh x   | 1/cosh²x  | —        |
| coth x   | −1/sinh²x | x ≠ 0    |

### Räkneregler

| Regel              | Formel                       |
| ------------------ | ---------------------------- |
| Konstant faktor    | (αf)' = αf'                  |
| Summa              | (f + g)' = f' + g'           |
| Produkt            | (fg)' = f'g + fg'            |
| Kvot               | (f/g)' = (f'g − fg')/g²      |
| Kedjeregeln        | D f(g(x)) = f'(g(x)) · g'(x) |
| Inversens derivata | (Df⁻¹)(y) = 1/f'(x)          |

---

## 🎯 Checklista: Vad du bör kunna efter kapitel 3.1–3.4

**Kapitel 3.1 — Introduktion:**
- [ ] Förstå differenskvotens fysikaliska tolkning (genomsnittlig ändringstakt)
- [ ] Förstå gränsövergången h → 0 som ger momentan ändringstakt
- [ ] Den geometriska tolkningen: sekant → tangent

**Kapitel 3.2 — Derivatans definition:**
- [ ] Den formella definitionen: f'(x₀) = lim(h→0) [f(x₀+h) − f(x₀)] / h
- [ ] Alla beteckningar: f', df/dx, Df, y', dy/dx
- [ ] Kunna beräkna derivator direkt ur definitionen (med gränsvärde av differenskvoten)
- [ ] Tangentens ekvation: y − f(x₀) = f'(x₀)(x − x₀)
- [ ] Normalens ekvation (vinkelrät tangenten): riktningskoefficient = −1/f'(x₀)
- [ ] Andraderivata f'' och dess tolkning (acceleration)
- [ ] Tillämpad derivering: hastighet, sönderfallshastighet, temperaturstegring

**Kapitel 3.3 — Derivationsregler:**
- [ ] **Sats 1:** Deriverbar ⟹ kontinuerlig (men INTE tvärtom, motexempel: |x|)
- [ ] Vänster- och högerderivata
- [ ] **Sats 2:** Alla fyra algebraiska reglerna (4)–(7) med bevis
  - Konstant faktor, summa, produkt, kvot
- [ ] Utvidgad produktregel för n faktorer
- [ ] **Sats 3 (Kedjeregeln):** u'(x) = f'(g(x)) · g'(x) — "yttre gånger inre"
- [ ] Leibniz-notation: du/dx = (du/dy)(dy/dx)
- [ ] Nästlade kedjeregeltillämpningar
- [ ] **Implicit derivering** — derivera en relation utan att lösa ut funktionen
- [ ] **Sats 4 (Inversens derivata):** (Df⁻¹)(y) = 1/f'(x)

**Kapitel 3.4 — De elementära funktionernas derivator:**
- [ ] **Alla derivatatabellens formler utantill** (se tabellen ovan)
- [ ] Speciellt: D eˣ = eˣ, D ln x = 1/x, D sin x = cos x, D cos x = −sin x
- [ ] D xᵅ = αxᵅ⁻¹ för **alla** reella α (bevis via e^(α ln x))
- [ ] D aˣ = aˣ ln a, D ᵃlog x = 1/(x ln a)
- [ ] D ln |x| = 1/x och D ln |f(x)| = f'(x)/f(x)
- [ ] **Logaritmisk derivering** som metod
- [ ] Funktioner g(x)^(h(x)) — deriveras med e^(h ln g)-metoden
- [ ] Alla arcusfunktionsderivator med bevis via sats 4
- [ ] Hyperboliska funktionernas derivator (likhet med trigonometriska)
