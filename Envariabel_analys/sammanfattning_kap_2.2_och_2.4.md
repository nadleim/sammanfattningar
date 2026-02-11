# 📈 Kapitel 2.2 & 2.4 — Kontinuerliga funktioner & Standardgränsvärden

## Omfattande sammanfattning och genomgång

---

# 🔷 KAPITEL 2.2 — Kontinuerliga funktioner

## Definition av kontinuitet

### Bakgrund — varför är kontinuitet viktigt?

I det föregående avsnittet om gränsvärden (2.1) har vi vid flera tillfällen utnyttjat en enkel men kraftfull egenskap hos elementära funktioner:

```
(11)    lim(x→x₀) f(x) = f(x₀)
```

Det vill säga: **gränsvärdet i en punkt är lika med funktionsvärdet i punkten**. Man behöver bara "stoppa in" värdet direkt! Detta gäller exempelvis för:

- lim(x→0) arcsin x = arcsin 0 = 0
- lim(x→1) √x = √1 = 1
- lim(x→0) cos x = cos 0 = 1

Men **alla** funktioner har inte den egenskapen — och det är just detta som begreppet kontinuitet handlar om.

---

### Definition 2: Kontinuitet i en punkt

> **DEFINITION 2.** En funktion f säges vara **kontinuerlig i en punkt x₀** om:
>
> 1. x₀ tillhör definitionsmängden Df, och
> 2. gränsvärdet lim(x→x₀) f(x) existerar (och därmed automatiskt är lika med f(x₀)).

> Om en funktion är kontinuerlig **i varje punkt** i sin definitionsmängd kallas den **kontinuerlig**.

> 🎯 **I klartext:** En funktion är kontinuerlig om en liten ändring av variabeln x bara ger upphov till en liten ändring av funktionsvärdet f(x). Det finns **inga plötsliga hopp** — grafen kan ritas utan att lyfta pennan.

---

### Diskontinuitetspunkter och singulariteter

Punkter där en funktion **inte** är kontinuerlig kallas **diskontinuitetspunkter** eller **diskontinuiteter**. Ibland talar man också om en **singularitet**.

En plötslig förändring av funktionsvärdena indikerar alltså närvaron av en diskontinuitet.

---

### Exempel 11: |x| är kontinuerlig

Funktionen f(x) = |x| är kontinuerlig. Enligt den omvända triangelolikheten gäller:

```
| |x| − |x₀| | ≤ |x − x₀|
```

för varje x₀. Detta visar att |x| → |x₀| då x → x₀, dvs. precis att |x| är kontinuerlig i x₀. ∎

> 💡 Trots att |x| har en "spets" i origo (grafen byter riktning) är funktionen ändå kontinuerlig! Kontinuitet handlar inte om jämnhet eller derivatbarhet — bara om avsaknaden av hopp.

---

### Motexempel: Funktionen utan gränsvärde

Funktionen

```
f(x) = { 0    då x ≤ 0
        { 1    då x > 0
```

är ett enkelt motexempel. Den **saknar gränsvärde** när x → 0, ty:

- Vänstergränsvärdet: lim(x→0⁻) f(x) = 0
- Högergränsvärdet: lim(x→0⁺) f(x) = 1

Dessa är olika, alltså existerar inte lim(x→0) f(x), och funktionen är diskontinuerlig i x = 0.

---

## De elementära funktionerna är kontinuerliga

### Räkneregler och kombination

Av räknelagarna för gränsvärden (sats 2, avsnitt 2.1) följer omedelbart att om f och g är kontinuerliga funktioner så är även:

```
f + g,     f · g,     f/g     (där g ≠ 0),     f ∘ g     (sammansättning)
```

kontinuerliga i sina respektiva definitionsmängder.

> 💡 Regeln gäller för f + g om formeln (11) gäller för f och g var för sig.

### Vilka funktioner är kontinuerliga?

Följande funktionstyper är alla kontinuerliga:

- **f(x) = x** (självklart kontinuerlig)
- **Varje polynom** (upprepade summor och produkter av x och konstanter)
- **Varje rationell funktion** f/g (på sin definitionsmängd, dvs. där g ≠ 0)
- **Potensfunktioner** aᵅ (följer av att potenser definieras via gränsvärden)
- **Exponentialfunktioner** aˣ (sträng bevisning via binomialsatsen)
- **Trigonometriska funktioner** sin x, cos x (små vinkeländringar ger små förflyttningar på enhetscirkeln)
- **Hyperboliska funktioner** (uppbyggda av exponentialfunktioner)
- **Logaritmfunktioner och arcusfunktioner** (inverser till strängt monotona, kontinuerliga funktioner)

> Den sista punkten grundas på en allmän sats:
>
> ```
> (12)    Inversen till en strängt monoton och kontinuerlig funktion är kontinuerlig.
> ```

**Slutsats:** Alla de **elementära funktionerna** — från polynom till arcusfunktioner — är alltså kontinuerliga. Detsamma gäller för alla funktioner som är uppbyggda av dessa med hjälp av addition, multiplikation, division och sammansättning.

---

### Exempel 12: Borttagbar diskontinuitet

Funktionen

```
f(x) = sin(2xeˣ) / x,     x ≠ 0
```

är kontinuerlig (eftersom den är uppbyggd av elementära funktioner) utom i x = 0, ty den inte är definierad där. Fråga: *Kan f tilldelas ett värde i x = 0 så att den blir kontinuerlig även där?*

**Lösning:** Vi behöver beräkna lim(x→0) f(x). Gör omskrivningen:

```
f(x) = sin(2xeˣ) / (2xeˣ) · 2eˣ
```

- Den andra faktorn: 2eˣ → 2e⁰ = 2 (exponentialfunktionen kontinuerlig)
- Den första: om vi sätter t = 2xeˣ → 0, blir sin(t)/t → 1 (standardgränsvärde (3) / sats 14)

Alltså: f(x) → 1 · 2 = 2 då x → 0.

Om vi definierar **f(0) = 2** uppfyller funktionen kontinuitetskravet (11) i x = 0. ∎

> 💡 En diskontinuitet som kan "botas" genom att tilldela funktionen ett lämpligt värde kallas **hävbar diskontinuitet**. I det här fallet är f diskontinuerlig i x = 0 men kan göras kontinuerlig genom definitionen f(0) = 2.

---

### Exempel 13: Gränsvärden via kontinuitet (talföljder)

**Visa att:**

```
lim(n→∞) ⁿ√a = 1       för varje fixt a > 0
```

och

```
lim(n→∞) ⁿ√n = 1
```

**Lösning:**

**Första gränsvärdet:** Båda gränsvärdena är konsekvenser av att exponentialfunktionen är kontinuerlig. Det första följer direkt:

```
ⁿ√a = a^(1/n) → a⁰ = 1    då n → ∞
```

(Exponenten 1/n → 0, och funktionen t ↦ aᵗ är kontinuerlig.)

**Andra gränsvärdet:** Kräver en viktig omskrivning:

```
n^(1/n) = e^(ln n^(1/n)) = e^((ln n)/n)
```

Vi vet att (ln n)/n → 0 (standardgränsvärde (24), logaritm förlorar mot potens). Av exponentialfunktionens kontinuitet:

```
ⁿ√n = e^((ln n)/n) → e⁰ = 1    då n → ∞
```

> 💡 **Tricket e^(ln ...)** är en kraftfull teknik. Genom att skriva f(x) = e^(ln f(x)) kan man hantera potensuttryck med variabel exponent. Vi använde detta redan i kap 2.3.

---

### Exempel 14: xˣ och hävbar diskontinuitet

Funktionen f(x) = xˣ för x > 0 kan skrivas:

```
(13)    f(x) = e^(x ln x)
```

Funktionen är kontinuerlig i sin definitionsmängd. Men vad händer vid x = 0?

**Naivt försök 1:** Uppfatta f som en potensfunktion → lim(x→0⁺) f(x) = 0. **Fel!**
**Naivt försök 2:** Uppfatta f som en exponentialfunktion → lim(x→0⁺) f(x) = 1. **Fel!**

**Korrekt lösning:** Enligt standardgränsvärdet (9):

```
x ln x → 0    då x → 0⁺
```

(vi visade detta i kapitel 2.1, ex. 8). Av exponentialfunktionens kontinuitet:

```
f(x) = e^(x ln x) → e⁰ = 1    då x → 0⁺
```

Vi måste därför definiera **f(0) = 1** för kontinuitet i origo. ∎

> ⚠️ **Viktig lärdom:** xˣ vid x → 0⁺ ger den obestämda formen **0⁰**. Man kan inte avgöra gränsvärdet genom att bara titta på basen eller exponenten separat — hela uttrycket måste analyseras med t.ex. e^(ln ...)-metoden.

---

## Typer av diskontinuiteter

### Stegfunktionen (språng)

```
θ(x) = { 0    då x < 0
        { 1    då x > 0
```

Denna funktion har **ingen hävbar diskontinuitet** i origo: både vänster- och högergränsvärde existerar, men de är olika (0 resp. 1). En sådan funktion sägs ha ett **språng** i diskontinuitetspunkten.

### Oscillerande singularitet

```
f(x) = sin(1/x),     x ≠ 0
```

I varje omgivning ]−δ, δ[ av diskontinuiteten x = 0 antar f varje värde mellan −1 och 1 **oändligt många gånger**. Det finns inget gränsvärde alls — inte ens ensidiga gränsvärden existerar.

> 💡 Diskontinuitetens "svårighetsgrad" varierar: hävbar < språng < oscillerande singularitet.

---

## Egenskaper hos kontinuerliga funktioner

### Inversen till en strängt monoton, kontinuerlig funktion

Vi har redan nämnt detta resultat:

> **(12)** Inversen till en strängt monoton och kontinuerlig funktion är kontinuerlig.

Denna sats förklarar varför arcsin, arccos, arctan och logaritmfunktionerna alla är kontinuerliga — de är inverser till strängt monotona, kontinuerliga funktioner.

---

### Satsen om mellanliggande värden

> **(14)** Om funktionen f är **kontinuerlig** på det begränsade och slutna intervallet [a, b] och **f(a) ≠ f(b)**, så antar f **varje värde μ** mellan f(a) och f(b).

> 🎯 **I klartext:** Om en kontinuerlig funktion tar värdet 3 i en punkt och värdet 7 i en annan punkt, så måste den ha antagit **alla** värden däremellan (3.5, 4, 5.1, π, ...) någonstans. Man kan inte "hoppa" från 3 till 7 utan att passera allt däremellan.
>
> **Grafiskt:** Varje horisontell linje y = μ med f(a) < μ < f(b) (eller tvärtom) skär kurvan y = f(x) i minst en punkt.

Man brukar kortfattat referera till (14) genom att säga att **en kontinuerlig funktion antar mellanliggande värden**.

> ⚠️ **Förutsättningen om kontinuitet är väsentlig.** Diskontinuerliga funktioner *kan* ha denna egenskap men behöver inte ha det.

---

### Satsen om största och minsta värde

> **(15)** Om funktionen f är **kontinuerlig** på det begränsade och slutna intervallet [a, b], så har f **ett största** och **ett minsta funktionsvärde** på detta intervall.

> 🎯 **I klartext:** En kontinuerlig funktion på ett slutet intervall når alltid sitt maximum och minimum — det finns faktiska punkter där dessa extremvärden uppnås.

> ⚠️ **Båda förutsättningarna behövs:**
>
> - **Begränsat och slutet intervall:** Funktionen f(x) = 1/x på det *öppna* intervallet (0, 1] har inget största värde (den växer obegränsat nära x = 0).
> - **Kontinuitet:** Funktionen f(x) = {0 om x = 0; 1/x om 0 < x ≤ 1} är diskontinuerlig och har inget störst funktionsvärde.

> 💡 Bevisen av satserna (12), (14) och (15) är förhållandevis svåra och hänger samman med de reella talens fullständighetsegenskap (samma axiom som i avsnitt 2.3). Den teoretiskt intresserade läsaren hänvisas till appendix C.

---

---

# 🔷 KAPITEL 2.4 — Standardgränsvärden

## Vad är standardgränsvärden?

Alla viktiga gränsvärden som har uppträtt i bokens tidigare kapitel sammanställs i detta avsnitt under det gemensamma namnet **standardgränsvärden**. Det är resultat som:

- används **mycket ofta** i gränsvärdesberäkningar
- bör vara **aktuella i minnet** hela tiden
- inte är triviala — de kräver bevis och bygger på räknereglerna

> 💡 Standardgränsvärdena är dina **grundverktyg** vid alla gränsvärdesberäkningar. Att kunna dem utantill sparar enormt med tid och gör det möjligt att lösa komplicerade problem genom att dela upp dem i kända delar.

---

## Grupp 1: Rangordning av funktioner (potens, exponential, logaritm)

En jämförelse mellan värdena för stora x av potens-, exponential- och logaritmfunktionerna (satserna 1.8 och 1.10 samt deras ekvivalenter):

```
(23)    xᵅ / aˣ → 0      då x → +∞       (a > 1)

(24)    ln x / xᵅ → 0    då x → +∞       (α > 0)
```

En variant som räknades fram i exempel 8 (avsnitt 2.1):

```
(25)    xᵅ ln x → 0      då x → 0⁺       (α > 0)
```

> 🎯 **Vad säger dessa?**
>
> **(23)** säger att exponentialfunktionen aˣ (a > 1) **dominerar** varje potensfunktion xᵅ. Oavsett hur stor exponenten α är, kommer aˣ att till slut vara ojämförligt mycket större.
>
> **(24)** säger att varje potensfunktion xᵅ (α > 0) **dominerar** logaritmen ln x. Även x^(0.001) slår ln x för tillräckligt stora x.
>
> **(25)** är (24) i förklädnad: vid x → 0⁺ med variabelbytet x = 1/t blir detta samma rangordning.
>
> **Den stora rangordningen:** logaritm ≪ potens ≪ exponential

> ⚠️ **Gränsvärdena (23)–(25) är i princip ekvivalenta.** Om man vet ett av dem kan man härleda de andra genom variabelbyten och omskrivningar.

---

## Grupp 2: Trigonometriskt gränsvärde

I sats 1.14 (avsnitt 1.9) visade vi:

```
(26)    sin x / x → 1    då x → 0
```

> 🎯 **Detta är det viktigaste enskilda standardgränsvärdet i kursen.** Det används inte bara vid trigonometriska gränsvärden utan även vid härledningen av derivatan av sin x, vid Taylorutvecklingar, och i otaliga tillämpningar.
>
> **Observera:** Det här gäller med x i **radianer**, inte grader!

---

## Grupp 3: Gränsvärden kopplade till talet e

Nästa grundläggande gränsvärde finner vi i sats 7 (avsnitt 2.3):

```
(27)    (1 + x)^(1/x) → e     då x → 0
```

Ekvivalenta formuleringar (via sats 8 i avsnitt 2.3):

```
(28)    ln(1 + x) / x → 1     då x → 0

(29)    (eˣ − 1) / x → 1      då x → 0
```

De tre sista gränsvärdena bygger alla på definitionen av talet e, dvs. på gränsvärdet:

```
(30)    (1 + 1/n)ⁿ → e        då n → ∞
```

> 🎯 **Varför är dessa tre ekvivalenta?**
>
> - **(28)** fås direkt från (27) genom att ta logaritmen: ln[(1+x)^(1/x)] = ln(1+x)/x → ln e = 1.
> - **(29)** fås från (28) genom substitutionen y = eˣ − 1, dvs. x = ln(1+y), och y → 0 då x → 0:
>   (eˣ − 1)/x = y/ln(1+y) = 1/[ln(1+y)/y] → 1/1 = 1.
>
> **Alla tre är i grunden samma gränsvärde i olika förklädnader!**

---

## Grupp 4: Gränsvärden för talföljder (n-te rötter)

I exempel 13 (avsnitt 2.2) fann vi gränsvärdena:

```
(31)    ⁿ√a → 1     då n → ∞       (för varje fixt a > 0)

(32)    ⁿ√n → 1     då n → ∞
```

> 🎯 **Tolkning:**
>
> **(31):** Oavsett vilken positiv bas a man tar — vare sig det är 100 eller 0.001 — så konvergerar den n-te roten mot 1. Detta beror på att exponenten 1/n → 0 och a⁰ = 1.
>
> **(32):** Trots att n → ∞ och ⁿ√n alltså är "roten ur ett ständigt växande tal", konvergerar det mot 1. Beviset kräver omskrivningen n^(1/n) = e^((ln n)/n) och standardgränsvärdet (24).

---

## Grupp 5: Exponentialfunktion vs fakultet

Vi avslutar med ytterligare två gränsvärden som jämför exponential- och fakultetsfunktionerna för stora n:

```
(33)    aⁿ / n! → 0       då n → ∞

(34)    ⁿ√(n!) → ∞        då n → ∞
```

### Bevis av (33)

Sätt K = ⌊|a|⌋ + 1 (heltalsdelen av |a| plus 1). Antag a > 0 (fallet a ≤ 0 behandlas analogt).

**Steg 1:** Dela upp faktorn aⁿ/n!:

```
0 ≤ aⁿ/n! = (a/1) · (a/2) · ... · (a/K) · (a/(K+1)) · ... · (a/n)
```

**Steg 2:** De första K faktorerna (a/1, a/2, ..., a/K) ger ett **fixt positivt tal** (oberoende av n).

**Steg 3:** De resterande faktorerna uppfyller a/(K+1), a/(K+2), ..., a/n < a/K < 1. Alltså:

```
aⁿ/n! ≤ (fixt tal) · (a/K)^(n−K) → 0
```

eftersom 0 < a/K < 1. Med instängningsregeln: aⁿ/n! → 0. ∎

> 🎯 **I klartext:** Fakulteten n! växer **snabbare** än vilken exponentialfunktion aⁿ som helst! Jämför: 10¹⁰ = 10 miljarder, men 10! = 3 628 800 och 20! ≈ 2.4 × 10¹⁸. Redan för "lilla" n tar fakulteten över.
>
> **Rangordningen utökas:** logaritm ≪ potens ≪ exponential ≪ fakultet

### Bevis av (34)

Låt c vara ett godtyckligt (stort) tal. Av gränsvärdet (33) följer att:

```
cⁿ / n! < 1    för tillräckligt stora n (säg n > ω)
```

Omskrivet: n! > cⁿ, dvs. ⁿ√(n!) > c för alla n > ω.

Eftersom c var godtyckligt stort visar detta precis att ⁿ√(n!) → ∞. ∎

---

## 📊 Komplett referenstabell: alla standardgränsvärden

| Nr | Gränsvärde | Gränsövergång | Källa |
|----|------------|---------------|-------|
| (23) | xᵅ/aˣ → 0 | x → +∞ (a > 1) | Sats 1.8 |
| (24) | (ln x)/xᵅ → 0 | x → +∞ (α > 0) | Sats 1.10 |
| (25) | xᵅ ln x → 0 | x → 0⁺ (α > 0) | Ex. 8, §2.1 |
| (26) | (sin x)/x → 1 | x → 0 | Sats 1.14 |
| (27) | (1+x)^(1/x) → e | x → 0 | Sats 2.7 |
| (28) | ln(1+x)/x → 1 | x → 0 | Sats 2.8 |
| (29) | (eˣ−1)/x → 1 | x → 0 | Sats 2.8 |
| (30) | (1+1/n)ⁿ → e | n → ∞ | Def. 2.3 |
| (31) | ⁿ√a → 1 | n → ∞ (a > 0) | Ex. 13, §2.2 |
| (32) | ⁿ√n → 1 | n → ∞ | Ex. 13, §2.2 |
| (33) | aⁿ/n! → 0 | n → ∞ | §2.4 |
| (34) | ⁿ√(n!) → ∞ | n → ∞ | §2.4 |

---

## 🧠 Hur man använder standardgränsvärdena — strategi

### Grundprincip

Vid gränsvärdesberäkningar är strategin att **skriva om** det givna uttrycket så att det kan uttryckas i termer av **kända standardgränsvärden**.

### Typiska omskrivningstrick

**Trick 1 — Förkorta med dominerande term:**
```
(eˣ + x²) / (3eˣ + 2ˣ) = [1 + x²/eˣ] / [3 + (2/e)ˣ] → 1/3
```
(Utnyttjar (23): x²/eˣ → 0 och (2/e)ˣ → 0.)

**Trick 2 — Variabelbyte:**
```
lim(x→0) arcsin x / x    [sätt y = arcsin x, dvs. x = sin y]
= lim(y→0) y / sin y = 1/1 = 1
```
(Utnyttjar (26) inverterat.)

**Trick 3 — Omskrivning till e^(ln ...)-form:**
```
lim(n→∞) n^(1/n) = lim(n→∞) e^((ln n)/n) = e⁰ = 1
```
(Utnyttjar (24): (ln n)/n → 0 och exponentialfunktionens kontinuitet.)

**Trick 4 — Dela upp i kända faktorer:**
```
lim(x→0) sinh x / sin x = lim(x→0) [sinh x / x] · [x / sin x] = 1 · 1 = 1
```
(Utnyttjar (29) indirekt och (26) inverterat.)

**Trick 5 — Konjugatkvantitet vid ∞ − ∞:**
```
√(x²−x) − x = −x / (√(x²−x) + x) → −1/2
```
(Eliminerar den obestämda formen genom algebraisk omskrivning.)

---

## 🎯 Checklista: Vad du bör kunna efter kapitel 2.2 och 2.4

**Kapitel 2.2 — Kontinuerliga funktioner:**
- [ ] Definitionen av kontinuitet: lim(x→x₀) f(x) = f(x₀)
- [ ] Veta att alla elementära funktioner (polynom, rationella, trig, exp, log, arcus) är kontinuerliga
- [ ] Att summa, produkt, kvot och sammansättning av kontinuerliga funktioner är kontinuerlig
- [ ] Vad en **diskontinuitetspunkt** är och kunna identifiera olika typer:
  - **Hävbar** diskontinuitet (kan "botas" genom lämpligt val av funktionsvärde)
  - **Språng** (höger- och vänstergränsvärden finns men är olika)
  - **Oscillerande** singularitet (inget gränsvärde alls)
- [ ] Att inversen till en strängt monoton, kontinuerlig funktion är kontinuerlig (12)
- [ ] **Satsen om mellanliggande värden** (14): kontinuerlig funktion antar alla mellänvärden
- [ ] **Satsen om största/minsta värde** (15): kontinuerlig funktion på [a,b] har max och min
- [ ] Förstå varför förutsättningarna i (14) och (15) behövs (slutet intervall + kontinuitet)
- [ ] Kunna visa att ⁿ√a → 1 och ⁿ√n → 1 via kontinuitet och standardgränsvärden
- [ ] **Omskrivningen f(x) = e^(ln f(x))** — när och varför den används

**Kapitel 2.4 — Standardgränsvärden:**
- [ ] Kunna alla 12 standardgränsvärden (23)–(34) **utantill**
- [ ] Förstå rangordningen: logaritm ≪ potens ≪ exponential ≪ fakultet
- [ ] Veta vilka gränsvärden som är ekvivalenta (23≈24≈25; 27≈28≈29≈30)
- [ ] Kunna tillämpa dem vid gränsvärdesberäkningar
- [ ] Behärska omskrivningstricken: förkorta med dominerande term, variabelbyte, e^(ln ...)-metoden, faktorisering, konjugatkvantitet
- [ ] Beviset av (33): varför aⁿ/n! → 0 (fakultet slår exponentialfunktion)
