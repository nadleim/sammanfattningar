# 📈 Kapitel 2.1 & 2.3 — Gränsvärden: Definition, Räkneregler & Talet e

## Omfattande sammanfattning och genomgång

---

# 🔷 KAPITEL 2.1 — Definition och räkneregler

## Varför behöver vi formella definitioner?

I kapitel 1 har vi redan räknat med gränsvärden på ett intuitivt sätt. Vi har till exempel visat att:

```
(1)   x^α / a^x → 0       då x → +∞    (a > 1, α > 0)
(2)   ln x / x^α → 0      då x → +∞    (α > 0)
(3)   sin x / x → 1        då x → 0
```

Men för att bygga en matematiskt *rigorös* teori måste vi ha **exakta definitioner** av vad det betyder att "en funktion närmar sig ett värde". Det är precis detta som kapitel 2.1 handlar om.

---

## Gränsvärdesdefinitionerna

### Definition 1: Gränsvärde då x → +∞ (den centrala definitionen)

> **DEFINITION 1.** Antag att f(x) är en funktion vars definitionsmängd innehåller godtyckligt stora reella tal. Vi säger att f(x) har **gränsvärdet A** då x går mot oändligheten om det **till varje givet tal ε > 0** finns **ett tal ω** (beroende av ε) sådant att:
>
> ```
> x > ω   och   x ∈ Df   ⟹   |f(x) − A| < ε.
> ```

**Notation:**
```
f(x) → A   då   x → +∞

eller ekvivalent:

lim(x→+∞) f(x) = A
```

> 🎯 **Vad betyder detta i klartext?**
>
> Tänk på det så här: Någon ger dig ett **toleranskrav** ε (hur nära A du måste vara). Oavsett hur litet ε är, ska du kunna hitta en gräns ω så att **alla funktionsvärden f(x) med x > ω** ligger inom intervallet (A − ε, A + ε).
>
> **Enkelt uttryckt:** Ju mer precision (mindre ε) som krävs, desto längre ut (större ω) måste man gå — men man *kan alltid* hitta ett sådant ω.

### Grafisk tolkning

Tänk dig att du ritar två horisontella linjer: y = A + ε och y = A − ε. Dessa bildar ett "band" kring värdet A. Definitionen säger att det finns en punkt ω på x-axeln så att hela grafen till höger om x = ω ligger **inuti bandet**. Och detta ska gälla oavsett hur smalt bandet görs!

---

### Exempel 1: Visa formellt att (x+1)/x → 1 då x → +∞

**Strategi:** Vi måste hitta ω (som beror på ε) så att |f(x) − 1| < ε för alla x > ω.

**Steg 1:** Beräkna |f(x) − A|:
```
|f(x) − 1| = |(x+1)/x − 1| = |1/x| = 1/x    (för x > 0)
```

**Steg 2:** Vi vill att 1/x < ε, dvs. x > 1/ε.

**Steg 3:** Välj ω = 1/ε. Då gäller:
```
x > ω = 1/ε   ⟹   |f(x) − 1| = 1/x < ε. ✓
```

Eftersom ε var godtyckligt litet, är gränsvärdet bevisat. ∎

> 💡 **Mönstret vid ε-bevis:**
> 1. Beräkna |f(x) − A| och förenkla
> 2. Bestäm villkoret på x som gör uttrycket < ε
> 3. Välj ω enligt detta villkor
> 4. Verifiera att det fungerar

---

### Exempel 2: En funktion utan gränsvärde

Funktionen f(x) = sin x **saknar gränsvärde** då x → +∞.

Anledning: Funktionsvärdena varierar mellan −1 och +1 i all evighet. De samlas aldrig nära ett bestämt värde A. Villkoret |f(x) − A| < ε kan inte uppfyllas för ε < 1, oavsett vilket A man väljer.

---

### Definition för x → a (gränsvärde i en punkt)

> Låt f vara en funktion och a en punkt som varje omgivning innehåller punkter ur Df. Då sägs f ha **gränsvärdet A då x → a** om det till varje ε > 0 finns ett δ > 0 sådant att:
>
> ```
> (5)   |x − a| < δ   och   x ∈ Df   ⟹   |f(x) − A| < ε.
> ```

> 🎯 **I klartext:** Om x ligger tillräckligt nära a (inom avståndet δ), så ligger f(x) nära A (inom avståndet ε). Och detta ska gälla oavsett hur litet ε väljs.

**Specialfall — om a tillhör definitionsmängden:**

Sätter man x = a i definition (5) fås |f(a) − A| < ε för varje ε > 0, dvs. A = f(a). Alltså:

> Om f är definierad i a och har gränsvärde då x → a, så **måste** gränsvärdet vara lika med funktionsvärdet f(a).

---

### Andra typer av gränsvärden

Alla definieras analogt med definitionerna ovan. Här är en översikt:

| Gränsövergång | Notation | Villkor på x |
|---------------|----------|--------------|
| x → +∞ | lim(x→+∞) f(x) = A | x > ω |
| x → −∞ | lim(x→−∞) f(x) = A | x < −ω (för stort ω) |
| x → a | lim(x→a) f(x) = A | 0 < \|x−a\| < δ |
| x → a⁺ (höger) | lim(x→a⁺) f(x) = A | a < x < a + δ (dvs. a ≤ x < a + δ) |
| x → a⁻ (vänster) | lim(x→a⁻) f(x) = A | a − δ < x ≤ a (dvs. a − δ < x ≤ a) |

**Höger- och vänstergränsvärde:**

```
x → a⁺ betyder att x närmar sig a från höger (x > a)
x → a⁻ betyder att x närmar sig a från vänster (x < a)
```

> 💡 **Viktig koppling:** f(x) har gränsvärde A då x → a **om och bara om** både höger- och vänstergränsvärdet existerar och är lika:
>
> lim(x→a⁺) f(x) = lim(x→a⁻) f(x) = A

---

### Oegentliga gränsvärden

Ibland går funktionsvärden mot +∞ eller −∞ istället för mot ett tal A. Sådana kallas **oegentliga gränsvärden**.

Exempel:
```
f(x) → +∞    då   x → +∞
f(x) → +∞    då   x → a
f(x) → −∞    då   x → a⁺
```

> 🎯 **Oegentligt gränsvärde** definieras genom att byta kravet "|f(x) − A| < ε" mot till exempel "f(x) > c" (godtyckligt stort c), och sedan visa att det finns ω (eller δ) så att detta uppfylls.
>
> Till exempel: lim(x→a⁺) f(x) = −∞ betyder att för varje (stort) tal c finns ett δ > 0 sådant att:
> ```
> a ≤ x < a + δ   ⟹   f(x) < −c
> ```

---

## Räkning med gränsvärden — de fem satserna

I praktiken vill man undvika att jobba med ε-δ-definitioner varje gång. Istället använder vi **räkneregler** (satser) som låter oss beräkna gränsvärden algebraiskt.

> ⚠️ Reglerna nedan gäller för **alla** typer av gränsövergångar: x → +∞, x → −∞, x → a, x → a⁺, x → a⁻, etc.

---

### Sats 1: "Noll gånger begränsad = noll"

> Om **lim f(x) = 0** och **g(x) är begränsad**, så gäller att:
>
> ```
> f(x)·g(x) → 0
> ```

> 🎯 **Tolkning:** En funktion som går mot noll "dominerar" — produkten med vilken begränsad funktion som helst ger också noll.
>
> **Exempel:** lim(x→0) x · sin(1/x) = 0, för x → 0 och |sin(1/x)| ≤ 1.

---

### Sats 2: Summa-, produkt- och kvotreglerna (SUPERVIKTIGA!)

> Om **lim f(x) = A** och **lim g(x) = B**, så gäller:
>
> ```
> (6)   f(x) + g(x) → A + B         (summaregeln)
> (7)   f(x)·g(x) → A·B             (produktregeln)
> (8)   f(x)/g(x) → A/B             (kvotregeln, kräver B ≠ 0)
> ```

> 🎯 **I klartext:** Om du vet gränsvärdena för varje del, kan du beräkna gränsvärdet av summan/produkten/kvoten genom vanlig aritmetik. **Det är detta som gör gränsvärdesberäkningar hanterliga!**

> ⚠️ **Kvotregeln kräver B ≠ 0.** Om nämnaren går mot 0 måste man använda andra metoder (omskrivning, faktorisering, konjugatkvantitet, etc.)

---

### Sats 3: Sammansättningsregeln

> Om:
> ```
> lim g(x) = a    och    lim(t→a) f(t) = A
> ```
> så gäller:
> ```
> lim f(g(x)) = A
> ```
> Här kan A såväl som a vara +∞ eller −∞.

> 🎯 **I klartext:** Om den inre funktionen g(x) närmar sig a, och f(t) närmar sig A då t → a, så går hela sammansättningen f(g(x)) mot A. Man kan alltså "beräkna gränsvärdet inifrån och ut".

---

### Sats 4: Instängningsregeln (Squeeze Theorem)

> Om **f(x)** och **g(x)** har **samma gränsvärde A**, och om:
> ```
> f(x) ≤ h(x) ≤ g(x)
> ```
> så har **även h(x) gränsvärdet A**.

> 🎯 **Tänk på det som en smörgås:** Om underbrödet (f) och överbrödet (g) båda går mot A, så *måste* påläggningen (h) däremellan också gå mot A. Det finns ingen annanstans den kan ta vägen!
>
> Kallas även "sandwich theorem" på engelska.

---

### Sats 5: Gränsövergång i olikhet

> Om **f(x) ≤ g(x)** och båda har gränsvärden, så gäller:
> ```
> lim f(x) ≤ lim g(x)
> ```

> ⚠️ **Anmärkning:** Även om det råder **strikt** olikhet f(x) < g(x), kan gränsvärdena bli **lika**!
>
> Exempel: 1/x < 2/x för alla x > 0, men båda har gränsvärdet 0 då x → +∞.

---

## Typiska gränsvärdesproblem — steg för steg

### Grundprincipen

Man försöker alltid först lösa uppgiften **direkt** med räknereglerna (satserna 1–5). Om det inte fungerar (t.ex. om man får en obestämd form som 0/0 eller ∞/∞), krävs en **omskrivning**.

---

### Exempel 3: Enkel direkt beräkning

```
lim(x→0) (x + cos x) / (2 + x³)
```

**Lösning:** Direkt insättning fungerar: täljaren → 0 + 1 = 1, nämnaren → 2 + 0 = 2. Alltså:

```
Gränsvärdet = 1/2
```

> 💡 Om man kan "stoppa in" gränsvärdet direkt och får ett väldefinierat uttryck, är det svaret. Inga konstigheter!

---

### Exempel 4: Obestämd form 0/0 — omskrivning behövs

```
lim(x→0) [x cos x + sin x] / [x + x²]
```

**Lösning:** Direkt insättning ger 0/0 (obestämd form). Vi behöver skriva om!

**Tricket:** Förkorta med nämnarens dominerande term. Dividera täljare och nämnare med x:

```
(x cos x + sin x) / (x + x²) = [cos x + (sin x)/x] / [1 + x]
```

Nu kan vi använda kvotregeln: täljaren → cos 0 + 1 = 2 och nämnaren → 1 + 0 = 1. 

```
Gränsvärdet = 2
```

> 💡 **Nyckelinsikt:** Vi utnyttjade standardgränsvärdet sin x / x → 1 (sats 14 från kapitel 1.9).

---

### Exempel 5: Obestämd form ∞ − ∞ — konjugatkvantitet

```
lim(x→+∞) (√(x² − x) − x)
```

**Lösning:** Direkt beräkning ger ∞ − ∞ (obestämt!). Standardmetoden: **förlängs med konjugatkvantiteten**.

```
√(x² − x) − x = [√(x² − x) − x] · [√(x² − x) + x] / [√(x² − x) + x]
              = (x² − x − x²) / (√(x² − x) + x)
              = −x / (√(x² − x) + x)
```

Bryt nu ut x ur nämnaren (x > 0):
```
= −x / [x(√(1 − 1/x) + 1)]
= −1 / (√(1 − 1/x) + 1)
→ −1 / (√1 + 1) = −1/2
```

```
Gränsvärdet = −1/2
```

> 💡 **Allmän regel:** Vid ∞ − ∞ med rotuttryck, förlängs alltid med konjugatkvantiteten (a − b)(a + b) = a² − b².

---

### Exempel 6: Obestämd form 0/0 med polynom — faktorisering

```
lim(x→1) (x³ − 1) / (x² + 2x − 3)
```

**Lösning:** Direkt insättning ger 0/0. Båda täljare och nämnare har **faktorn (x − 1)**.

Faktorisera:
```
x³ − 1 = (x − 1)(x² + x + 1)
x² + 2x − 3 = (x − 1)(x + 3)
```

Förkorta med (x − 1):
```
(x² + x + 1) / (x + 3) → (1 + 1 + 1) / (1 + 3) = 3/4
```

```
Gränsvärdet = 3/4
```

> 💡 **Mönster:** Om man får 0/0 vid x = a, innehåller båda täljare och nämnare faktorn (x − a). Polynomdivision eller faktorisering löser problemet.

---

### Exempel 7: "Noll gånger obegränsad" — sats 1

```
lim(x→0) x · sin(1/x)
```

**Lösning:** Här kan produktregeln inte användas direkt, för sin(1/x) saknar gränsvärde (den oscillerar vilt). Men sin(1/x) är **begränsad** (|sin(1/x)| ≤ 1), och x → 0. Enligt **sats 1**:

```
x · sin(1/x) → 0
```

---

### Exempel 8: Obestämd form 0 · (−∞) — variabelbyte

```
lim(x→0⁺) x^α · ln x       (α > 0)
```

**Lösning:** Direkt ger detta formen 0 · (−∞), som är obestämd. 

**Trick — variabelbytet t = 1/x:**

```
x^α · ln x = (1/t)^α · ln(1/t) = −(ln t) / t^α
```

Eftersom t = 1/x → +∞ då x → 0⁺, och vi vet standardgränsvärdet:

```
(ln t) / t^α → 0    då t → +∞
```

Alltså:

```
(9)    x^α · ln x → 0    då x → 0⁺
```

> 💡 **Variabelbyte är en kraftfull teknik!** Genom att byta t = 1/x kan man omvandla ett gränsvärde vid 0 till ett vid +∞ (eller tvärtom).

---

### Exempel 9: Sammansättningsregeln — ny variabel

```
lim(x→0) arcsin x / x
```

**Lösning:** Sätt y = arcsin x. Då gäller att y → 0 då x → 0, och x = sin y. Alltså:

```
arcsin x / x = y / sin y → 1    (då y → 0)
```

ty vi vet att sin y / y → 1, dvs. y / sin y → 1 också. 

```
Gränsvärdet = 1
```

---

### Exempel 10: Oegentligt gränsvärde

```
lim(x→+∞) √x · e^(1/x)
```

**Lösning:** Första faktorn √x → +∞ och den andra e^(1/x) → e⁰ = 1 (via sammansättningsregeln). Produkten "∞ · 1" kan inte hanteras med produktregeln (den kräver att *båda* gränsvärden är ändliga tal). Men med lite eftertanke:

√x blir obegränsat stor och e^(1/x) → 1 > 0. Alltså blir produkten obegränsat stor:

```
√x · e^(1/x) → +∞
```

---

## Obestämda former — en viktig varning

Man kan **inte** direkt gränsövergå vid **obestämda former**. De viktigaste är:

| Obestämd form | Exempel | Kommentar |
|---------------|---------|-----------|
| **∞ − ∞** | √(x²−x) − x | Kan ge vilket värde som helst |
| **∞/∞** | x²/eˣ | Kräver omskrivning |
| **0 · ∞** | x · ln x (vid x→0⁺) | Kräver omskrivning |
| **0/0** | sin x / x (vid x→0) | Kräver omskrivning |
| **1^∞** | (1+1/n)ⁿ | Ger talet e (se kap. 2.3!) |
| **∞⁰** | x^(1/x) | Kräver analys |
| **0⁰** | x^x (vid x→0⁺) | Kräver analys |

> ⚠️ "Obestämd form" betyder att man **inte vet vad gränsvärdet blir** utan ytterligare analys. Uttrycket kan ge 0, 1, ∞, eller vilket annat värde som helst beroende på de specifika funktionerna.

---

## Bevisen av räknereglerna (kortfattat)

Boken ger fullständiga bevis av satserna 1–5 för fallet x → +∞. Här är de centrala idéerna:

**Bevis av sats 1** (noll · begränsad = noll):
Eftersom g(x) är begränsad finns C med |g(x)| < C. Eftersom f(x) → 0 finns ω₁ med |f(x)| < ε/C för x > ω₁. Alltså |f(x)g(x)| < (ε/C)·C = ε.

**Bevis av sats 2 (6)** (summaregeln):
Välj ω₁ och ω₂ så att |f(x)−A| < ε/2 och |g(x)−B| < ε/2. Med ω = max(ω₁, ω₂):
|(f(x)+g(x))−(A+B)| ≤ |f(x)−A| + |g(x)−B| < ε/2 + ε/2 = ε (triangelolikheten).

**Bevis av sats 2 (7)** (produktregeln):
Tricket är omskrivningen f(x)g(x) − AB = (f(x)−A)g(x) + A(g(x)−B). Eftersom f(x)→A ger att g(x) är begränsad nära A+1, och (f(x)−A)→0 är "noll gånger begränsad" = 0. Termen A(g(x)−B)→0 av sats 1 (eller direkt).

**Bevis av sats 2 (8)** (kvotregeln):
Visa först att 1/g(x) → 1/B. Eftersom g(x)→B ≠ 0, är g(x)>B/2 för stora x, så 1/g(x) < 2/B (begränsad). Skillnaden 1/g(x)−1/B = (B−g(x))/(Bg(x)) → 0 genom sats 1. Kvotregeln följer sedan av f/g = f · (1/g) och produktregeln.

**Bevis av sats 3** (sammansättning):
Eftersom f(t)→A då t→a finns δ med |f(t)−A|<ε om |t−a|<δ. Eftersom g(x)→a finns ω med |g(x)−a|<δ för x>ω. Kedja ihop: x>ω ⟹ |g(x)−a|<δ ⟹ |f(g(x))−A|<ε.

**Bevis av sats 4** (instängning):
A−ε < f(x) ≤ h(x) ≤ g(x) < A+ε för stora x, alltså |h(x)−A| < ε.

**Bevis av sats 5** (gränsövergång i olikhet):
Motbevis: Om gränsvärdet C av h(x)=g(x)−f(x) vore negativt, skulle h(x)<C/2<0 för stora x, vilket motsäger h(x) ≥ 0.

---

---

# 🔷 KAPITEL 2.3 — Talet e

## Den grundläggande egenskapen hos reella tal

Innan vi definierar talet e behöver vi ett **axiom** — en grundläggande egenskap som vi accepterar utan bevis:

> **(16)** Varje **växande** och **uppåt begränsad** reellvärd funktion har ett **gränsvärde**.

> 🎯 **Vad betyder detta?**
>
> Tänk på en talföljd som hela tiden ökar (t.ex. 1, 1.5, 1.75, 1.875, ...) men aldrig överstiger ett visst tak (t.ex. 2). Axiomet säger att en sådan följd *måste* konvergera — den närmar sig ett bestämt tal.
>
> **Varför behövs detta?** Det är just denna egenskap som skiljer de reella talen ℝ från de rationella talen ℚ. Bland de rationella talen finns det växande, begränsade talföljder som *inte* konvergerar (deras gränsvärde är irrationellt och "saknas" bland de rationella talen).

Motsvarande gäller naturligtvis för **avtagande och nedåt begränsade** funktioner.

> 💡 Axiom (16) ger oss existens av gränsvärden men säger **inget om storleken**. Trots det visar sig detta vara extremt kraftfullt.

---

## Sats 6: Talföljden (1 + 1/n)ⁿ

> **Sats 6.** Talföljden
> ```
> (1 + 1/n)ⁿ,    n = 1, 2, 3, ...
> ```
> är **växande** och **uppåt begränsad**.

### Beviset — del 1: Växande

Med binomialsatsen:

```
(1 + 1/n)ⁿ = 1 + n·(1/n) + n(n−1)/2! · (1/n²) + ... + n(n−1)...(n−k+1)/k! · (1/nᵏ) + ... + (1/n)ⁿ
```

Den allmänna termen (utom den första) kan skrivas:

```
c(n,k) = [1·(1 − 1/n)·(1 − 2/n)· ... ·(1 − (k−1)/n)] / k!
```

Varje faktor (1 − j/n) **ökar** när n ökar (eftersom j/n minskar). Dessutom har utvecklingen **fler termer** för större n. Bägge effekterna gör att (1+1/n)ⁿ växer med n. ✓

### Beviset — del 2: Uppåt begränsad

Vi behöver en övre gräns. Observera att:

```
c(n,k) < 1/k!
```

(ty alla faktorer (1 − j/n) < 1). Dessutom:

```
1/k! = 1/(1·2·3·...·k) ≤ 1/(1·2·2·...·2) = 1/2^(k−1)    för k ≥ 2
```

Alltså:
```
(1 + 1/n)ⁿ < 1 + 1 + 1/2 + 1/2² + ... + 1/2^(n−1)
            < 1 + (1 + 1/2 + 1/4 + ...)
            = 1 + 1/(1 − 1/2)    (geometrisk serie)
            = 1 + 2 = 3
```

Sammantaget: **(1 + 1/n)ⁿ < 3 för alla n.** ✓

---

## Definition 3: Talet e

Eftersom talföljden (1 + 1/n)ⁿ är växande och uppåt begränsad, existerar dess gränsvärde enligt axiom (16). Vi ger detta gränsvärde ett namn:

> **DEFINITION 3.** Gränsvärdet
>
> ```
> (17)    lim(n→∞) (1 + 1/n)ⁿ
> ```
>
> betecknas med bokstaven **e** och kallas för **den naturliga logaritmens bas**.

### Numeriskt värde

Från beviset vet vi att:

```
2 ≤ e < 3
```

(Nedre gränsen: för n = 1 ger (1 + 1)¹ = 2. Övre gränsen: beviset ovan.)

Med mer noggranna beräkningar (t.ex. via serieutvecklingar) kan man visa:

```
2.7 ≤ e ≤ 2.75
```

De första siffrorna: **e ≈ 2.71828...**

> 💡 Talet e är **irrationellt** (och dessutom transcendent) — det kan alltså inte skrivas som ett bråk p/q, och det är inte lösning till någon polynomekvation med heltalskoefficienter.

---

### Varning: Produktregeln kan inte användas direkt på (1 + 1/n)ⁿ

Det kan vara frestande att resonera: "Varje faktor (1 + 1/n) → 1 då n → ∞, så produkten borde gå mot 1ⁿ = 1." **Men detta är fel!**

Produktregeln (sats 2) kan bara användas för ett **fixt antal** faktorer. I uttrycket (1 + 1/n)ⁿ växer antalet faktorer med n. Denna obestämda form **1^∞** kräver specialbehandling.

---

## Sats 7: Utvidgning till reella x

> **Sats 7.** Det gäller att:
>
> ```
> (18)    (1 + 1/x)ˣ → e    då   x → +∞
>
> (19)    (1 + 1/x)ˣ → e    då   x → −∞
>
> (20)    (1 + x)^(1/x) → e    då   x → 0
> ```

### Varför gäller (18)?

**Bevis:** Låt n vara det heltal med n ≤ x < n+1. Då gäller för x ≥ 1:

```
(1 + 1/(n+1))ⁿ  ≤  (1 + 1/x)ˣ  ≤  (1 + 1/n)^(n+1)
```

- Vänsterledet → e (via (17) med n+1 istället för n)
- Högerledet = (1 + 1/n)ⁿ · (1 + 1/n) → e · 1 = e

Av instängningsregeln (sats 4) följer att (1 + 1/x)ˣ → e. ✓

### Varför gäller (19)?

Genom variabelbytet x = −y (y → +∞) och omskrivningen:

```
(1 + 1/x)ˣ = (1 − 1/y)^(−y) = [(y−1)/y]^(−y) = [y/(y−1)]^y = (1 + 1/(y−1))^(y−1) · (1 + 1/(y−1))
```

→ e · 1 = e. ✓

### Varför gäller (20)?

Sätt x = 1/t. Då t → +∞ (eller −∞) om x → 0⁺ (eller 0⁻):

```
(1 + x)^(1/x) = (1 + 1/t)^t → e
```

enligt (18) och (19). ✓

---

## Sats 8: Två viktiga standardgränsvärden

Från sats 7 följer:

> **Sats 8.** Det gäller att:
>
> ```
> (21)    ln(1 + x) / x → 1      då   x → 0
>
> (22)    (eˣ − 1) / x → 1       då   x → 0
> ```

### Bevis av (21)

```
ln(1 + x) / x = (1/x) · ln(1 + x) = ln[(1 + x)^(1/x)]
```

Enligt (20) gäller (1 + x)^(1/x) → e. Eftersom ln är en kontinuerlig funktion:

```
ln[(1 + x)^(1/x)] → ln e = 1   ✓
```

### Bevis av (22)

Gränsvärde (22) är ekvivalent med (21). Visa genom substitutionen y = eˣ − 1, dvs. x = ln(1 + y):

```
(eˣ − 1) / x = y / ln(1 + y) = 1 / [ln(1 + y)/y] → 1/1 = 1   ✓
```

(ty y → 0 när x → 0, och ln(1+y)/y → 1 enligt (21))

---

### Exempel 15

```
lim(n→∞) (1 + 1/(2n))ⁿ
```

**Lösning:** Skriv om:

```
(1 + 1/(2n))ⁿ = [(1 + 1/(2n))^(2n)]^(1/2)
```

Med sammansättningsregeln och potensfunktionens kontinuitet:

```
(1 + 1/(2n))^(2n) → e    (specialfall av (17) med 2n istället för n)
```

Alltså:

```
(1 + 1/(2n))ⁿ → e^(1/2) = √e
```

---

### Exempel 16

```
lim(x→0) sinh x / sin x
```

**Lösning:** Vi skriver om med definitionen sinh x = (eˣ − e⁻ˣ)/2:

```
sinh x / sin x = [(eˣ − e⁻ˣ) / 2] / sin x
              = (1/2) · e⁻ˣ · (e²ˣ − 1) / sin x
              = (1/2) · e⁻ˣ · [(e²ˣ − 1) / (2x)] · [2x / sin x] · 1
```

**Varje faktor har ett känt gränsvärde:**
- e⁻ˣ → e⁰ = 1
- (e²ˣ − 1)/(2x) → 1 (standardgränsvärde (22) med 2x istället för x)
- x/sin x → 1 (standardgränsvärde (3), inverterat)

Alltså:
```
sinh x / sin x → (1/2) · 1 · 1 · 2 · 1 = 1
```

> Alternativt kan man se att sinh x / sin x = (sinh x / x) · (x / sin x), och båda faktorer → 1.

---

## 📋 Sammanställning: Alla standardgränsvärden (avsnitt 2.4)

Boken samlar alla viktiga standardgränsvärden i avsnitt 2.4. Här är de alla:

### Rangordning av funktioner (för x → +∞)

```
(23)   x^α / aˣ → 0    då x → +∞       (a > 1)
(24)   ln x / x^α → 0  då x → +∞       (α > 0)
(25)   x^α · ln x → 0  då x → 0⁺       (α > 0)
```

> 💡 Dessa tre säger: **exponentiell tillväxt slår potenstillväxt, som slår logaritmisk tillväxt.**

### Trigonometriskt gränsvärde

```
(26)   sin x / x → 1    då x → 0
```

### Gränsvärden kopplade till talet e

```
(27)   (1 + x)^(1/x) → e         då x → 0
(28)   ln(1 + x) / x → 1         då x → 0
(29)   (eˣ − 1) / x → 1          då x → 0
(30)   (1 + 1/n)ⁿ → e            då n → ∞
```

### Gränsvärden för n-te rötter (talföljder)

```
(31)   ⁿ√a → 1      då n → ∞    (a > 0 fixt)
(32)   ⁿ√n → 1      då n → ∞
```

### Exponentialfunktion vs fakultet

```
(33)   aⁿ / n! → 0       då n → ∞
(34)   ⁿ√(n!) → ∞        då n → ∞
```

---

## 🎯 Checklista: Vad du bör kunna efter kapitel 2.1 och 2.3

**Kapitel 2.1 — Definitioner och räkneregler:**
- [ ] Förstå den formella definitionen av gränsvärde (ε-ω och ε-δ)
- [ ] Kunna genomföra ett enkelt ε-bevis (som i exempel 1)
- [ ] Skilja mellan gränsvärde då x → ∞, x → a, x → a⁺, x → a⁻
- [ ] Förstå och kunna använda alla fem satser (1–5)
- [ ] Identifiera obestämda former (0/0, ∞/∞, 0·∞, ∞−∞, 1^∞, ∞⁰, 0⁰)
- [ ] Lösa gränsvärdesproblem med: direkt insättning, faktorisering, konjugatkvantitet, variabelbyte, förkorta med dominerande term
- [ ] Kunna koppla samman standardgränsvärdena (1)–(3) med beräkningar

**Kapitel 2.3 — Talet e:**
- [ ] Förstå axiom (16): växande + uppåt begränsad ⟹ gränsvärde finns
- [ ] Veta att (1 + 1/n)ⁿ är växande och begränsad (och förstå bevisskissen)
- [ ] Kunna definitionen av e som lim(n→∞) (1 + 1/n)ⁿ
- [ ] Veta att 2 ≤ e < 3 (och e ≈ 2.718...)
- [ ] Kunna de tre varianterna: (1+1/x)ˣ→e, (1+1/x)ˣ→e, (1+x)^(1/x)→e
- [ ] Kunna standardgränsvärdena ln(1+x)/x → 1 och (eˣ−1)/x → 1
- [ ] Kunna tillämpa dessa vid beräkningar (som i exempel 15–16)
- [ ] Förstå varför 1^∞ inte automatiskt ger 1 (och att det kräver analys)
