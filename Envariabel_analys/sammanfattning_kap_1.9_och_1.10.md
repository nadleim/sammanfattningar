# 📐 Kapitel 1.9 & 1.10 — De trigonometriska funktionerna & Arcusfunktionerna

## Omfattande sammanfattning och genomgång

---

# 🔷 KAPITEL 1.9 — De trigonometriska funktionerna

## 1.9.1 Radianer

### Varför radianer istället för grader?

I vardagen mäter vi vinklar i **grader** (360° = ett helt varv). Men i matematik är grader ett opraktiskt mått. Istället använder vi **radianer**, som bygger på enhetscirkeln.

**Så här definieras en radian:**
Tänk dig en cirkel med radie 1 (en *enhetscirkel*) med centrum i origo. Lägg ett koordinatsystem med det ena benet längs positiva x-axeln. En vinkel mäts som **längden av den cirkelbåge** som vinkeln skär ut på enhetscirkeln.

- Vi utgår från punkten (1, 0)
- **Moturs** = positivt t
- **Medurs** = negativt t
- Vi tillåter båglängder som svarar mot mer än ett helt varv

Detta vinkelmått kallas **bågmått** eller **radianer**.

### Omvandlingstabell grader ↔ radianer

| Grader | -30° | 0° | 30° | 45° | 60° | 90° | 180° | 360° | 720° |
|--------|------|-----|------|------|------|------|-------|-------|-------|
| Radianer | -π/6 | 0 | π/6 | π/4 | π/3 | π/2 | π | 2π | 4π |

> 💡 **Minnesregel:** Talet π definieras som halva omkretsen av en cirkel med radie 1. Alltså: ett halvt varv = π radianer, ett helt varv = 2π radianer.

---

## 1.9.2 Sinus och cosinus

### Definitionen

Låt P(t) vara den punkt på enhetscirkelns periferi som svarar mot en cirkelbåge av längden t, mätt med punkten (1, 0) som utgångspunkt. Vi definierar:

- **cos t** = x-koordinaten för punkten P(t)
- **sin t** = y-koordinaten för punkten P(t)

> 🎯 **Enkelt uttryckt:** Om du vandrar en sträcka t längs enhetscirkeln (moturs från punkten (1,0)), så ger din x-position cos t och din y-position sin t.

### Grundläggande funktionsvärden

| t | 0 | π/2 | π | 3π/2 |
|---|---|-----|---|------|
| cos t | 1 | 0 | -1 | 0 |
| sin t | 0 | 1 | 0 | -1 |

### Kopplingen till rätvinkliga trianglar

I en rätvinklig triangel (med spetsig vinkel t) gäller:

- **cos t** = (närliggande katet) / (hypotenusa)
- **sin t** = (motstående katet) / (hypotenusa)

### Vanliga exakta värden (MÅSTE kunnas utantill!)

Dessa fås från "halva liksidig triangel" (30°-60°-90°) och "halva kvadrat" (45°-45°-90°):

| t | π/6 (30°) | π/4 (45°) | π/3 (60°) |
|---|-----------|-----------|-----------|
| cos t | √3/2 | 1/√2 | 1/2 |
| sin t | 1/2 | 1/√2 | √3/2 |

### Grundegenskaper

**Periodicitet:** Funktionerna upprepar sig med perioden 2π:

```
cos(x + k·2π) = cos x       för alla heltal k
sin(x + k·2π) = sin x       för alla heltal k
```

**Definitionsmängd:** Alla reella tal  
**Värdemängd:** Intervallet [-1, 1]

**Jämn/udda:**
- cos är en **jämn** funktion: cos(-x) = cos x
- sin är en **udda** funktion: sin(-x) = -sin x

> 💡 **Vad betyder jämn/udda?**
> - Jämn funktion → grafen är **spegelvänd kring y-axeln** (som x²)
> - Udda funktion → grafen har **punktsymmetri kring origo** (som x³)

### Graferna

**y = cos x:** Startar på y = 1 vid x = 0, har vågform med period 2π. Ser ut som en sinuskurva förskjuten π/2 åt vänster.

**y = sin x:** Startar på y = 0 vid x = 0, stiger till 1 vid π/2, sjunker till 0 vid π, ner till -1 vid 3π/2, och tillbaka till 0 vid 2π.

---

## Trigonometriska formler och trigonometriska ekvationer

### Den trigonometriska ettan (SUPERVIKTIG!)

```
(48)    cos²x + sin²x = 1
```

> 🎯 Denna formel följer direkt av Pythagoras sats på enhetscirkeln. Om punkten (cos x, sin x) ligger på enhetscirkeln (radie 1), så måste cos²x + sin²x = 1².

### Inspektionssamband

Dessa samband kan inses genom att studera enhetscirkeln:

```
(49)    cos(π - x) = -cos x
(50)    sin(π - x) = sin x
(51)    cos(x + π) = -cos x
(52)    sin(x + π) = -sin x
(53)    cos(π/2 - x) = sin x
(54)    sin(π/2 - x) = cos x
```

> 💡 Samband (53) och (54) säger att **sinus och cosinus är samma funktion, bara förskjutna π/2** relativt varandra.

---

### Lösning av trigonometriska ekvationer

#### Typ 1: sin-ekvationer

**Grundprincip:** Om sin β = sin α, så finns **två** familjer av lösningar:

```
β = α + k·2π     (k heltal)
β = π - α + k·2π  (k heltal)
```

**Exempel 50:** Lös sin 3x = 1/2 i intervallet 0 ≤ x < 2π.

*Lösning:* Vi söker t sådant att sin t = 1/2. De "grundlösningarna" är t = π/6 och t = 5π/6. Alltså:
- 3x = π/6 + k·2π → x = π/18 + k·2π/3
- 3x = 5π/6 + k·2π → x = 5π/18 + k·2π/3

Med kravet 0 ≤ x < 2π och k = 0, 1, 2 får vi sex lösningar:
**π/18, 5π/18, 13π/18, 17π/18, 25π/18, 29π/18**

#### Typ 2: cos-ekvationer

**Grundprincip:** Om cos β = cos α, så finns **två** familjer:

```
β = α + k·2π      (k heltal)
β = -α + k·2π     (k heltal)
```

**Exempel 51:** Lös cos 5x = cos 3x.

*Lösning:* 
- 5x = 3x + k·2π → x = kπ (k heltal)
- 5x = -3x + k·2π → x = kπ/4 (k heltal)

Den andra uppsättningen innehåller den första, så svaret förenklas till: **x = kπ/4, k ∈ ℤ**.

#### Typ 3: Ekvationer som kräver trigonometriska ettan

**Exempel 52:** Lös cos²x + 3sin²x = 2 i 0 ≤ x < 2π.

*Lösning:* Använd cos²x = 1 - sin²x:
```
(1 - sin²x) + 3sin²x = 2
2sin²x = 1
sin²x = 1/2
sin x = ±1/√2
```
Lösningarna i [0, 2π) blir: **π/4, 3π/4, 5π/4, 7π/4**.

---

## Subtraktionssatsen och additionsformlerna

### Subtraktionssatsen för cosinus (grundformeln)

```
(55)    cos(x - y) = cos x cos y + sin x sin y
```

> 📝 **Beviset** bygger på att beräkna skalärprodukten u·v mellan enhetsvektorerna **u** = (cos x, sin x) och **v** = (cos y, sin y) på två sätt:
> 1. Via definitionen: u·v = |u|·|v|·cos(x-y) = cos(x-y)
> 2. Via komponentformeln: u·v = cos x cos y + sin x sin y

### De viktiga additionsformlerna

Från subtraktionssatsen (55) härleds alla andra:

```
(56)    cos(x + y) = cos x cos y - sin x sin y
(57)    sin(x + y) = sin x cos y + cos x sin y
(58)    sin(x - y) = sin x cos y - cos x sin y
```

### Dubbla vinkeln-formler

Genom att sätta y = x i additionsformlerna:

```
(59)    sin 2x = 2 sin x cos x
(60)    cos 2x = cos²x - sin²x = 2cos²x - 1 = 1 - 2sin²x
```

> 💡 Formel (60) har **tre** likvärdiga former! Vilken du använder beror på situationen.

### Halva vinkeln-formler

Genom att i cos 2x ersätta x med x/2:

```
(61)    cos²(x/2) = (1 + cos x) / 2
(62)    sin²(x/2) = (1 - cos x) / 2
```

### Produktformlerna

```
(63)    cos x cos y = ½[cos(x+y) + cos(x-y)]
(64)    sin x sin y = -½[cos(x+y) - cos(x-y)]
(65)    cos x sin y = ½[sin(x+y) - sin(x-y)]
```

### Summa-till-produkt (typ "faktorisering av sin/cos")

```
(66)    sin α - sin β = 2 cos((α+β)/2) · sin((α-β)/2)
```

> 🎯 **Alla dessa formler** är lika nödvändiga att kunna som potens- och logaritmlagarna. Lär dig åtminstone additionsformlerna (56)-(58) och dubbla vinkeln (59)-(60) utantill — resten kan härledas vid behov.

### Exempel 53: En ekvation som kräver formulering

**Lös:** cos 2x - (5/2)cos x + sin²x + 1 = 0

*Lösning:* Skriv om allt i termer av cos x:
- cos 2x = 2cos²x - 1 (formel 60)
- sin²x = 1 - cos²x (trigonometriska ettan)

Ekvationen blir: cos²x - (5/2)cos x + 1 = 0

Sätt u = cos x: u² - (5/2)u + 1 = 0 → u = 2 eller u = 1/2.

Eftersom cos x = 2 saknar lösning (cos tar aldrig värden > 1), återstår cos x = 1/2, dvs:
**x = ±π/3 + k·2π, k ∈ ℤ**

---

## Omskrivning med hjälpvinkel

### Metoden

Funktioner av formen

```
(67)    f(x) = a sin x + b cos x
```

kan alltid skrivas om som en **enda sinusfunktion**:

```
f(x) = √(a² + b²) · sin(x + δ)
```

där hjälpvinkeln δ bestäms av:
```
(68)    a/√(a²+b²) = cos δ,    b/√(a²+b²) = sin δ
```

> 🎯 **Varför är detta viktigt?** Formen √(a²+b²)·sin(x+δ) avslöjar direkt:
> - **Amplituden** = √(a²+b²)
> - **Fasförskjutningen** = δ

### Exempel 54

**Lös:** √3 sin 2x - cos 2x = √3

*Lösning:* Detta är av formen (67) med a = √3, b = -1 (och x utbytt mot 2x).

1. Beräkna amplituden: √((√3)² + (-1)²) = √4 = 2
2. Bestäm δ: cos δ = √3/2, sin δ = -1/2 → δ = -π/6
3. Ekvationen blir: 2·sin(2x - π/6) = √3, dvs sin(2x - π/6) = √3/2

Lösningar: 2x - π/6 = π/3 + k·2π eller 2x - π/6 = π - π/3 + k·2π

→ **x = π/4 + kπ** och **x = 5π/12 + kπ**, k ∈ ℤ

---

## Harmoniska svängningar

I tillämpningar representerar sinus- och cosinusfunktionerna ofta **harmoniska svängningar**, med *tiden t* som oberoende variabel:

```
f(t) = A sin ωt
```

Här är:
- **A** = amplituden (maximal utväxling)
- **ω** (omega) = vinkelfrekvensen
- **T** = 2π/ω = perioden (tid för ett helt svängningsvarv)
- **ν** = ω/2π = frekvensen (antal svängningar per tidsenhet)

> Omskrivning med hjälpvinkel visar att a sin ωt + b cos ωt i själva verket är en harmonisk svängning med vinkelfrekvens ω och amplitud √(a² + b²).

---

## Triangelsolvering

### Cosinussatsen och sinussatsen

Låt a, b, c vara sidorna i en triangel och α, β, γ de motstående vinklarna.

**Sats 11 (Cosinussatsen):**
```
a² = b² + c² - 2bc cos α
```

> 💡 Pythagoras sats är specialfallet när α = 90° (då cos 90° = 0 och formeln ger a² = b² + c²).

**Sats 12 (Sinussatsen):**
```
sin α / a = sin β / b = sin γ / c = 1/(2R)
```
där R är den omskrivna cirkelns radie.

### Bevisidéer

**Cosinussatsen** bevisas med vektorer: Inför u = AC och v = AB. Då:
a² = |u - v|² = |u|² + |v|² - 2|u||v|cos α = b² + c² - 2bc cos α.

**Sinussatsen** bevisas genom att betrakta den omskrivna cirkeln. Bågvinkeln vid A' (diametralt motsatt) är lika stor som vid A, och i den rätvinkliga triangeln A'BC: sin α = a/(2R).

### Exempel 55: Komplett triangelsolvering

Givet: b = 3.713, c = 6.101, α = 15.263°

1. Beräkna a med cosinussatsen: a² = 6.101² + 3.713² - 2·6.101·3.713·cos 15.263° → **a ≈ 2.702**
2. Beräkna γ med sinussatsen: sin 15.263°/2.702 = sin γ/3.713 → **γ ≈ 21.208°**
3. Beräkna β: β = 180° - 15.263° - 21.208° = **143.529°**

### Areasatsen

Arean av en triangel kan beräknas med:
```
T = ½ · b · c · sin α
```

> 🎯 Om vinkeln är spetsig: T = ½ · grundlinje · höjd, och höjden = b·sin α (direkt av sinusdefinitionen).

---

## 1.9.3 Tangens och cotangens

### Definitioner

```
tan x = sin x / cos x      (definierad då cos x ≠ 0, dvs x ≠ π/2 + kπ)
cot x = cos x / sin x      (definierad då sin x ≠ 0, dvs x ≠ kπ)
```

### Koppling till rätvinklig triangel

- **tan x** = motstående katet / närliggande katet
- **cot x** = närliggande katet / motstående katet

> Alltså: cot x = 1/tan x

### Egenskaper

- Både tan och cot är **udda** funktioner med **period π** (inte 2π!)
- Tangensfunktionen har **vertikala asymptoter** vid x = π/2 + kπ
- Cotangensfunktionen har **vertikala asymptoter** vid x = kπ

### Additionssats och dubbla vinkeln för tangens

```
(69)    tan(x + y) = (tan x + tan y) / (1 - tan x · tan y)
(70)    tan 2x = 2 tan x / (1 - tan²x)
```

### Växling mellan sinus, cosinus och tangens

**Exempel 56:** Om sin x = a, bestäm tan x.

*Lösning:* Ur trigonometriska ettan: cos x = ±√(1 - a²). Därmed:
```
tan x = sin x / cos x = ±a / √(1 - a²)
```
Tecknet beror på vilken kvadrant x ligger i.

**Exempel 57:** Om tan x = b, bestäm sin x.

*Lösning:* Vi startar med sin²x = sin²x/(sin²x + cos²x) = tan²x/(tan²x + 1). Alltså:
```
sin x = ±b / √(b² + 1)
```

---

## 1.9.4 Olikheter och gränsvärden

### Sats 13: Grundläggande olikhet

```
För 0 < x < π/2:    sin x < x < tan x
```

> ⚠️ Vinkeln x **måste mätas i radianer** — annars gäller inte olikheten!

**Beviset** bygger på att jämföra areor och längder i enhetscirkeln:
- sin x = PQ (höjden i triangeln, alltid kortare än båglängden x)
- x = båglängden (alltid kortare än tangens-sträckan RS = tan x)

### Exempel 58

**Visa att** cos x > 1 - x²/2 för 0 < x < π.

*Lösning:* Från sats 13 följer sin(x/2) < x/2 för 0 < x < π. 

Eftersom sin(x/2) > 0 i detta intervall: sin²(x/2) < x²/4.

Med formel (62): cos x = 1 - 2sin²(x/2) > 1 - 2·x²/4 = 1 - x²/2. ∎

### Sats 14: Det berömda gränsvärdet

```
(72)    sin x / x → 1    då x → 0
```

> 🎯 **Detta är ett av de allra viktigaste gränsvärdena i matematiken!** Det används ständigt i analysen, bland annat för att härleda derivatan av sin x.

**Bevisidé:** Från olikheten sin x < x < tan x (sats 13) följer för 0 < x < π/2:

```
sin x < x < sin x / cos x
```

Dividera med sin x (positivt): 1 < x/sin x < 1/cos x

Invertera: cos x < sin x / x < 1

Eftersom cos x → 1 då x → 0⁺, kläms sin x / x mot 1.

Eftersom sin(-x)/(-x) = sin x / x gäller resultatet också för x → 0⁻.

### Exempel 59

**Beräkna** lim(x→0) tan x / x.

*Lösning:* Skriv om: tan x / x = (sin x / x) · (1/cos x) → 1·1 = **1**.

### Approximation

Sats 14 och exempel 59 visar att för x-värden nära 0:
```
sin x ≈ x ≈ tan x     (x nära 0)
```

> 💡 Detta är en *approximation*, inte en exakt likhet. Den används t.ex. inom mekanik för att förenkla pendelekvationer ("liten vinkel-approximation").

---

---

# 🔷 KAPITEL 1.10 — Arcusfunktionerna

## Grundidé: Varför behöver vi inversa trigonometriska funktioner?

Om vi vet att sin x = 0.5 och vill hitta x, behöver vi en **invers** till sinusfunktionen. Problemet är att sinus med hela reella axeln som definitionsmängd **inte har någon invers** — varje y-värde (mellan -1 och 1) ger oändligt många x-värden.

Lösningen: Vi **begränsar** (restriktar) sinusfunktionen till ett intervall där den är **strängt monoton** (antingen enbart växande eller enbart avtagande) och därmed **injektiv**. Då finns det en invers!

---

## 1.10.1 Arcussinus (arcsin)

### Definition

Vi begränsar sinus till intervallet **[-π/2, π/2]**.

I detta intervall är sin x **strängt växande** (går från -1 till 1), och funktionen är därmed injektiv.

**Inversen kallas arcussinus** och betecknas **arcsin x**.

### Nyckeluppgifter

| Egenskap | Värde |
|----------|-------|
| Definitionsmängd | [-1, 1] |
| Värdemängd | [-π/2, π/2] |
| Typ | Strängt växande |

### De viktiga inversrelationerna

```
(73)    arcsin(sin x) = x      när |x| ≤ π/2
(74)    sin(arcsin x) = x      när |x| ≤ 1
```

### Tolkning i ord

> **arcsin x** = den vinkel (i radianer) **mellan -π/2 och π/2** vars sinusvärde är x.

### Exempel 60: Beräkna standardvärden

```
arcsin(1/2) = π/6        (ty sin π/6 = 1/2 och π/6 ∈ [-π/2, π/2])
arcsin(√3/2) = π/3       (ty sin π/3 = √3/2)
arcsin(-1/√2) = -π/4     (ty sin(-π/4) = -1/√2)
```

### ⚠️ VARNING: arcsin(sin x) = x gäller BARA inom [-π/2, π/2]!

Utanför intervallet måste man "korrigera" värdet:

```
arcsin(sin(3π/4)) ≠ 3π/4     ← FEL! 3π/4 ∉ [-π/2, π/2]
arcsin(sin(3π/4)) = arcsin(1/√2) = π/4     ← RÄTT!
```

> 💡 **Tankemodell:** arcsin "snappar tillbaka" svaret till intervallet [-π/2, π/2]. Om du matar in en vinkel utanför detta intervall, ger arcsin den "spegelvinkel" som ligger inom intervallet.

---

## 1.10.2 Arcuscosinus (arccos)

### Definition

Vi begränsar cosinus till intervallet **[0, π]**.

I detta intervall är cos x **strängt avtagande** (går från 1 till -1), och funktionen är injektiv.

**Inversen kallas arcuscosinus** och betecknas **arccos x**.

### Nyckeluppgifter

| Egenskap | Värde |
|----------|-------|
| Definitionsmängd | [-1, 1] |
| Värdemängd | [0, π] |
| Typ | Strängt avtagande |

### De viktiga inversrelationerna

```
(75)    arccos(cos x) = x      när 0 ≤ x ≤ π
(76)    cos(arccos x) = x      när |x| ≤ 1
```

### Tolkning i ord

> **arccos x** = den vinkel (i radianer) **mellan 0 och π** vars cosinusvärde är x.

### Exempel 61

```
arccos(√3/2) = π/6        (ty cos π/6 = √3/2)
arccos(cos(-π/4)) = arccos(1/√2) = π/4
```

> Notera: arccos(cos(-π/4)) = π/4, **inte** -π/4, för -π/4 ∉ [0, π].

### Sambandet mellan arcsin och arccos

**Exempel 62 / Formel (77):**
```
(77)    arccos x = π/2 - arcsin x      för -1 ≤ x ≤ 1
```

> 🎯 **Tolkning:** arcsin och arccos kompletterar varandra till π/2. Om du vet den ena, vet du den andra!

**Bevis:** Enligt (76): cos(arccos x) = x. Men:
cos(π/2 - arcsin x) = sin(arcsin x) = x (med formel 53).
Så VL = HL. Sedan visar man att båda ligger i samma intervall [0, π], vilket garanterar likhet.

### Anmärkning: Trigonometriska formler → formler för arcusfunktioner

Precis som exponentialfunktionens räknelagar "översätts" till logaritmregler, kan trigonometriska formler översättas till arcusfunktionsformler. Formel (77) är ett sådant exempel: formeln cos(π/2 - x) = sin x ter sig efter omformulering som arccos x = π/2 - arcsin x.

---

## 1.10.3 Arcustangens och arcuscotangens

### Arcustangens (arctan)

**Restriktion:** Tangensfunktionen begränsas till intervallet **(-π/2, π/2)** (öppet intervall). Där är tan x strängt växande.

**Inversen** kallas **arcustangens** och betecknas **arctan x**.

### Nyckeluppgifter

| Egenskap | Värde |
|----------|-------|
| Definitionsmängd | Hela ℝ (alla reella tal) |
| Värdemängd | (-π/2, π/2) (öppet intervall) |
| Typ | Strängt växande |

### Inversrelationer

```
arctan(tan x) = x      när -π/2 < x < π/2
tan(arctan x) = x      för alla x ∈ ℝ
```

### Tolkning i ord

> **arctan x** = den vinkel i intervallet **(-π/2, π/2)** vars tangensvärde är x.

### Asymptotiskt beteende

```
arctan x → π/2     då x → +∞
arctan x → -π/2    då x → -∞
```

Grafen har **horisontella asymptoter** vid y = ±π/2.

### Arcuscotangens (arccot)

**Restriktion:** cot x begränsas till **(0, π)**. Dess invers kallas **arccot x**.

| Egenskap | Värde |
|----------|-------|
| Definitionsmängd | Hela ℝ |
| Värdemängd | (0, π) |

> 💡 I praktiken räknar man sällan med arccot direkt. De flesta miniräknare saknar denna funktion. Istället uttrycker man arccot x via arctan:

### Sambandet arctan–arccot

**Exempel 63 / Formel:**
```
arccot x = π/2 - arctan x      för alla x ∈ ℝ
```

**Bevis:** Vi visar att cot(π/2 - arctan x) = tan(arctan x) = x. Eftersom både VL och HL ligger i (0, π), är beviset klart.

---

## 📊 Sammanfattande översikt: Alla fyra arcusfunktioner

| Funktion | Def.mängd | Värdemängd | Monotoni | Grundfunktion |
|----------|-----------|------------|----------|---------------|
| arcsin x | [-1, 1] | [-π/2, π/2] | Strängt växande | sin |
| arccos x | [-1, 1] | [0, π] | Strängt avtagande | cos |
| arctan x | ℝ | (-π/2, π/2) | Strängt växande | tan |
| arccot x | ℝ | (0, π) | Strängt avtagande | cot |

---

## 🧠 Samband att minnas

1. **arccos x = π/2 - arcsin x** (för -1 ≤ x ≤ 1)
2. **arccot x = π/2 - arctan x** (för alla x ∈ ℝ)
3. **arcsin(sin x) = x** BARA om x ∈ [-π/2, π/2]
4. **arccos(cos x) = x** BARA om x ∈ [0, π]
5. **arctan(tan x) = x** BARA om x ∈ (-π/2, π/2)

---

## 🎯 Checklista: Vad du bör kunna efter kapitel 1.9 och 1.10

- [ ] Omvandla mellan grader och radianer
- [ ] Rita enhetscirkeln och avläsa sin/cos/tan för standardvinklar
- [ ] Kunna standardvärdena för sin, cos, tan vid π/6, π/4, π/3 utantill
- [ ] Trigonometriska ettan och hur den används för omskrivning
- [ ] Additionsformlerna (56)-(58) och dubbla vinkeln-formlerna (59)-(60)
- [ ] Lösa grundläggande trigonometriska ekvationer (sin x = a, cos x = a)
- [ ] Omskrivning med hjälpvinkel: a sin x + b cos x = √(a²+b²)·sin(x+δ)
- [ ] Cosinussatsen och sinussatsen, samt triangelsolvering
- [ ] Olikheten sin x < x < tan x (för 0 < x < π/2)
- [ ] Gränsvärdet sin x / x → 1 då x → 0
- [ ] Definitionerna av arcsin, arccos, arctan, arccot
- [ ] Definitionsmängder och värdemängder för alla arcusfunktioner
- [ ] Sambanden arccos x = π/2 - arcsin x och arccot x = π/2 - arctan x
- [ ] Varför arcsin(sin x) ≠ x om x ligger utanför [-π/2, π/2]
