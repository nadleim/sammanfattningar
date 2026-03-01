# 📐 Kapitel 6.1–6.4 — Integraler: definition, integrering och beräkning

## Omfattande sammanfattning och genomgång

*Baserad på kursboken (sidorna 293–311) och föreläsning 18 (Bestämda integraler)*

---

# 🔷 KAPITEL 6.1 — Integralens definition

## Bakgrund: Varför integraler?

Integralens grundidé är att mäta **arean** under en kurva. Det låter enkelt, men problemet är: hur definierar man "area" rigoröst för ett område som begränsas av en böjd kurva?

Lösningen är att **approximera med rektanglar** — och sedan ta gränsvärdet när rektanglarna blir oändligt smala. Det här är exakt vad vi gör med trappfunktioner och Riemannsummor.

> 🎯 **Koppling till föreläsningen:** Föreläsningen ställer frågan direkt: "Alla vet att integralen ger arean under grafen… men *varför*? Hur hänger primitivfunktioner och arean ihop?" — det är precis det hela kapitel 6 besvarar.

---

## Trappfunktioner (stegfunktioner)

### Definition

En funktion Φ : [a,b] → ℝ kallas en **trappfunktion** om det finns en **indelning** (partition) av [a,b]:

```
a = x₀ < x₁ < x₂ < ... < xₙ₋₁ < xₙ = b
```

så att Φ är **konstant** på varje öppet delintervall:

```
Φ(x) = cₖ   för   xₖ₋₁ < x < xₖ,     k = 1, 2, ..., n
```

> 💡 **Intuitivt:** Tänk dig en trappstegsfunktion — den hoppar mellan konstanta värden vid delningspunkterna. Vad som händer *exakt i* delningspunkterna spelar ingen roll!

### Integralen av en trappfunktion

Integralen av en trappfunktion definieras som **summan av rektangelareorna**, där vi tar hänsyn till tecken (negativa "areor" under x-axeln räknas som negativa):

**DEFINITION 1.** Talet

```
I(Φ) = Σₖ₌₁ⁿ cₖ(xₖ - xₖ₋₁)
```

kallas **integralen** av trappfunktionen Φ. Vi skriver också:

```
         b
I(Φ) =  ∫  Φ(x) dx
         a
```

> 💡 **Varför just detta?** Varje term cₖ · (xₖ - xₖ₋₁) är arean av en rektangel med höjd cₖ och bredd (xₖ - xₖ₋₁). Om cₖ < 0 bidrar rektangeln med en *negativ* area — vi väger alltså in funktionens tecken.

### Räkneregler för trappfunktioners integraler (Sats 1)

**SATS 1.** Följande gäller för integraler av trappfunktioner på [a,b]:

```
(3)  I(αΦ)     = α · I(Φ)             (skalning med konstant)
(4)  I(Φ + Ψ)  = I(Φ) + I(Ψ)         (additivitet)
(5)  Φ ≤ Ψ     ⟹  I(Φ) ≤ I(Ψ)       (monotonitet)
(6)  I(Φ) på [a,b] = I(Φ) på [a,c] + I(Φ) på [c,b]   om a ≤ c ≤ b  (intervalladditivitet)
```

Egenskap (3) och (4) säger att integration är en **linjär** operation. Egenskap (5) säger att den är **monoton** — en större funktion ger en större integral.

> 🎯 **Viktigt:** Dessa egenskaper ärver Riemannintegralen för allmänna funktioner! De överförs direkt till "vanliga" integraler.

---

## Riemannintegralen — den "riktiga" integralen

### Grundidén

Vi vill definiera integralen av en **godtycklig begränsad funktion** f på [a,b]. Idén är:

1. **Klam in** f mellan två trappfunktioner: Φ ≤ f ≤ Ψ
2. Om skillnaden I(Ψ) - I(Φ) kan göras **godtyckligt liten**, så finns det ett unikt tal "i mitten" som vi kallar integralen av f.

> 💡 **Föreläsningens förklaring:** "Approximera f(x) med trappfunktioner → finare partition ger bättre approximation → har finare och finare trappfunktioner ett gränsvärde?"

### Formell definition

**DEFINITION 2.** En begränsad funktion f definierad på [a,b] säges vara **(Riemann)integrerbar** om det till varje reellt ε > 0 finns trappfunktioner Φ och Ψ som satisfierar:

```
Φ(x) ≤ f(x) ≤ Ψ(x),     a ≤ x ≤ b
```

och är sådana att:

```
I(Ψ) - I(Φ) < ε
```

> 💡 **Vad innebär detta egentligen?** Om vi kan "klämma" f ovanifrån och underifrån med trappfunktioner vars integraler är *nästan lika* (skillnad < ε för varje ε > 0), så "konvergerar" de mot samma tal. Det talet kallas integralen.

**SATS 2.** Om f är integrerbar så finns precis ett tal λ sådant att:

```
I(Φ) ≤ λ ≤ I(Ψ)
```

för alla trappfunktioner Φ och Ψ med Φ ≤ f ≤ Ψ.

**DEFINITION 3.** Det entydigt bestämda talet λ kallas **integralen av f** över [a,b] och skrivs:

```
 b
 ∫  f(x) dx
 a
```

> ⚠️ **Viktigt:** Integralen är ett **tal** (ett nummer). Det ska inte förväxlas med den obestämda integralen ∫ f(x) dx (utan gränser), som betecknar en **primitiv funktion**.

### Riemannsumma — ett alternativt sätt att se på det

En **Riemannsumma** ger en konkret beräkningsmetod. Givet en indelning D och mellanpunkter ξₖ:

```
D: a = x₀ < x₁ < ... < xₙ = b
Mellanpunkter: xₖ₋₁ ≤ ξₖ ≤ xₖ
```

är Riemannsumman:

```
Rᴅ = Σₖ₌₁ⁿ f(ξₖ)(xₖ - xₖ₋₁)
```

> 💡 **Geometriskt:** Vi approximerar arean med rektanglar. Varje rektangel har bredd (xₖ - xₖ₋₁) och höjd f(ξₖ), där ξₖ är en godtycklig punkt i delintervallet. Summan av dessa rektangelareor ger Riemannsumman.

Från föreläsningen: Riemannsumman är lika med integralen av en trappfunktion Φ_{D,ξ} som har värdet f(ξₖ) på varje delintervall.

---

# 🔷 KAPITEL 6.2 — Integration av kontinuerliga funktioner

## Huvudresultatet: kontinuerliga funktioner är integrerbara

**SATS 3.** *Om funktionen f är kontinuerlig i det slutna intervallet [a,b], så är f integrerbar över detta.*

### Bevisidé (viktig att förstå!)

Beviset bygger på att **kontinuerliga funktioner på slutna intervall** har egenskapen **likformig kontinuitet**: för varje ε > 0 finns δ > 0 sådant att:

```
|f(x) - f(y)| < ε/(b-a)    för alla x, y ∈ [a,b] med |x-y| < δ
```

Med denna δ gör vi en indelning D med finhet l(D) < δ. I varje delintervall [xₖ₋₁, xₖ] definierar vi:

```
mₖ = min f(x)   (på delintervallet)  →  bildar undre trappfunktion Φ_D
Mₖ = max f(x)   (på delintervallet)  →  bildar övre trappfunktion Ψ_D
```

Då gäller Φ_D ≤ f ≤ Ψ_D, och skillnaden:

```
I(Ψ_D) - I(Φ_D) = Σ (Mₖ - mₖ)(xₖ - xₖ₋₁)
                  < ε/(b-a) · Σ (xₖ - xₖ₋₁)
                  = ε/(b-a) · (b-a) = ε
```

Alltså kan skillnaden göras < ε, och f är integrerbar. ∎

> 🎯 **Mer allmänt:** Varje **styckvis kontinuerlig** funktion (kontinuerlig överallt utom i ändligt många punkter) är integrerbar. Funktionen får ha "hopp" i ändligt många ställen.

## Riemannsumma konvergerar till integralen

**SATS 4.** *Antag att f är kontinuerlig på [a,b]. Då gäller för Riemannsumman:*

```
Σₖ₌₁ⁿ f(ξₖ)(xₖ - xₖ₋₁) → ∫ₐᵇ f(x) dx
```

*vid obegränsat förfinad indelning (l(D) → 0).*

> 💡 **Varför är detta viktigt?** Det betyder att vi kan **beräkna** integralen genom att ta gränsvärdet av Riemannsummor. Välj valfri indelning, valfria mellanpunkter — resultatet blir detsamma!

### Exempel 1: Beräkna ∫₀¹ eˣ dx med Riemannsumma

Välj likformig indelning: xₖ = k/n och ξₖ = (k-1)/n (vänster ändpunkt). Då:

```
Rₙ = Σₖ₌₁ⁿ e^((k-1)/n) · (1/n) = (1/n) · Σₖ₌₀ⁿ⁻¹ (e^(1/n))ᵏ
```

Detta är en geometrisk summa med kvot q = e^(1/n):

```
= (1/n) · (e^(n/n) - 1)/(e^(1/n) - 1) = (e-1) · (1/n)/(e^(1/n) - 1)
```

Substitution t = 1/n → 0 ger:

```
lim (1/n)/(e^(1/n) - 1) = lim t/(eᵗ - 1) = 1    (standardgränsvärde)
                n→∞              t→0
```

Alltså: ∫₀¹ eˣ dx = e - 1. ✓

> 🎯 **Från föreläsningen:** Man visade även exemplet ∫₀¹ 2⁻ˣ dx med samma teknik, och fick svaret 1/ln(4). Notera att 2⁻ˣ *inte* har en enkel primitivfunktion i standardform, men integralen kan ändå beräknas via Riemannsumma!

---

# 🔷 KAPITEL 6.3 — Räknelagar och uppskattningar

## Räknelagar för integraler (ärver trappfunktionernas)

**SATS 5.** *Om f och g är integrerbara över [a,b], så gäller:*

```
(9)   ∫ₐᵇ αf(x) dx = α · ∫ₐᵇ f(x) dx            (skalning)

(10)  ∫ₐᵇ (f(x)+g(x)) dx = ∫ₐᵇ f(x) dx + ∫ₐᵇ g(x) dx   (additivitet)

(11)  f(x) ≤ g(x) i [a,b]  ⟹  ∫ₐᵇ f(x) dx ≤ ∫ₐᵇ g(x) dx   (monotonitet)

(12)  ∫ₐᵇ f(x) dx = ∫ₐᶜ f(x) dx + ∫꜀ᵇ f(x) dx    (intervalladditivitet)
```

### Konventioner för integrationsgränser

Regel (12) gäller primärt för a ≤ c ≤ b, men vi **definierar** för b ≤ a:

```
  b              a
  ∫ f(x) dx = - ∫ f(x) dx
  a              b
```

Speciellt: ∫ₐᵃ f(x) dx = 0.

Med denna konvention gäller (12) för **alla** möjliga inbördes lägen av a, b och c.

### Ett viktigt specialfall av monotonicitet

```
g(x) ≥ 0  i [a,b]   ⟹   ∫ₐᵇ g(x) dx ≥ 0
```

> 💡 Arean under en icke-negativ funktion är icke-negativ. Logiskt!

### Uppskattning av integraler med (11)

Monotonicitetregeln (11) är ett **kraftfullt verktyg** för att uppskatta integraler:

Om man vet att m ≤ f(x) ≤ M för alla x ∈ [a,b], så:

```
m(b-a) ≤ ∫ₐᵇ f(x) dx ≤ M(b-a)
```

**Exempel 2 (ur boken):** Visa att 1 ≤ ∫₁⁴ 1/(1+√x) dx ≤ 3/2.

Lösning: f(x) = 1/(1+√x) är avtagande på [1,4], så:

```
f(4) = 1/3 ≤ f(x) ≤ f(1) = 1/2    för 1 ≤ x ≤ 4
```

Därmed: (1/3)·3 = 1 ≤ ∫₁⁴ f(x) dx ≤ (1/2)·3 = 3/2. ✓

> 🎯 **Från föreläsningen:** Samma teknik visades för ∫₄⁹ √x dx, där 2 ≤ √x ≤ 3 ger uppskattningen 10 ≤ ∫₄⁹ √x dx ≤ 15.

---

## Triangelolikheten för integraler

**SATS 6. (TRIANGELOLIKHETEN)** *Om f är styckvis kontinuerlig i [a,b]:*

```
|∫ₐᵇ f(x) dx| ≤ ∫ₐᵇ |f(x)| dx
```

### Bevisidé

Eftersom f(x) ≤ |f(x)| och -f(x) ≤ |f(x)|, ger monotonitet:

```
∫ₐᵇ f(x) dx ≤ ∫ₐᵇ |f(x)| dx     och     -∫ₐᵇ f(x) dx ≤ ∫ₐᵇ |f(x)| dx
```

Men |∫ₐᵇ f(x) dx| är antingen ∫ₐᵇ f(x) dx eller -∫ₐᵇ f(x) dx, så olikheten följer. ∎

> 💡 **Intuitivt:** Beloppet av "nettoarean" (med hänsyn till tecken) kan aldrig överstiga den totala arean (utan hänsyn till tecken).

---

## Integralkalkylens medelvärdessats

**SATS 7. (INTEGRALKALKYLENS MEDELVÄRDESSATS)** *Om f är kontinuerlig i [a,b], så finns en punkt ξ, a ≤ ξ ≤ b, sådan att:*

```
∫ₐᵇ f(x) dx = f(ξ) · (b - a)
```

### Vad innebär detta?

Geometriskt: Det finns alltid en **rektangel** med basen (b-a) och höjden f(ξ) som har **exakt samma area** som området under grafen av f. Talet:

```
C = 1/(b-a) · ∫ₐᵇ f(x) dx
```

är **medelvärdet** av f på [a,b], och satsen säger att f antar detta medelvärde i minst en punkt.

### Bevisidé

Sätt m = min f(x) och M = max f(x) på [a,b]. Monotonitet ger:

```
m(b-a) ≤ ∫ₐᵇ f(x) dx ≤ M(b-a)
```

Dividera med (b-a): m ≤ C ≤ M. Eftersom f är kontinuerlig och antar värdena m och M, antar f (enligt satsen om mellanliggande värden) varje värde däremellan — speciellt C. ∎

**Exempel 3:** Beräkna lim_{n→∞} ∫ₙⁿ⁺² arctan x dx.

Lösning: Enligt medelvärdessatsen: ∫ₙⁿ⁺² arctan x dx = 2 · arctan ξₙ för något n ≤ ξₙ ≤ n+2. Eftersom arctan x → π/2 då x → ∞ följer att integralen → π.

### Generaliserade medelvärdessatsen

**SATS 8.** *Om f och g är kontinuerliga och g(x) ≥ 0 i [a,b], så finns ξ ∈ [a,b] sådant att:*

```
∫ₐᵇ f(x)g(x) dx = f(ξ) · ∫ₐᵇ g(x) dx
```

> 💡 Denna generalisering väger funktionsvärden med g som "vikter" — ett slags viktat medelvärde.

---

# 🔷 KAPITEL 6.4 — Beräkning av integraler

## Analysens huvudsats — den centrala satsen!

Det här är **den viktigaste satsen** i hela integralteorin. Den kopplar ihop derivering och integration — två operationer som vid första anblick verkar ha lite med varandra att göra.

**SATS 9. (ANALYSENS HUVUDSATS)** *Antag att f är kontinuerlig i [a,b]. Definiera:*

```
S(x) = ∫ₐˣ f(t) dt,    a ≤ x ≤ b
```

*Då är S(x) deriverbar i ]a,b[ med:*

```
S'(x) = f(x),    a < x < b
```

### Vad innebär detta?

> 🎯 **Derivatan av en integral (med variabel övre gräns) ger tillbaka integranden!**

Funktionen S(x) = ∫ₐˣ f(t) dt är alltså en **primitiv funktion** till f. Det här kopplar ihop de två grundoperationerna i analysen: **integration** ("beräkna arean") och **derivering** ("beräkna lutningen").

### Beviset — steg för steg

**Bilda differenskvoten:**

```
[S(x+h) - S(x)] / h = (1/h) · [∫ₐˣ⁺ʰ f(t) dt - ∫ₐˣ f(t) dt]
                     = (1/h) · ∫ₓˣ⁺ʰ f(t) dt
```

**Använd medelvärdessatsen** (sats 7): Det finns ξₕ med x ≤ ξₕ ≤ x+h sådant att:

```
∫ₓˣ⁺ʰ f(t) dt = f(ξₕ) · h
```

**Sätt in och låt h → 0:**

```
S'(x) = lim_{h→0} [S(x+h) - S(x)] / h = lim_{h→0} f(ξₕ) = f(lim_{h→0} ξₕ) = f(x)
```

Det sista steget utnyttjar att f är **kontinuerlig** och att ξₕ → x då h → 0. ∎

> 💡 **Geometrisk tolkning:** S(x) mäter arean under f från a till x. Om x ökar lite (med h) så ökar arean med ungefär f(x)·h — alltså är "tillväxthastigheten" av arean just f(x).

### Direkt konsekvens

**Varje kontinuerlig funktion har en primitiv funktion.** Man kan alltid skriva:

```
F(x) = ∫ₐˣ f(t) dt
```

som en primitiv funktion till f. Däremot behöver denna primitiv **inte** kunna uttryckas med elementära funktioner!

**Exempel 4:** Enligt analysens huvudsats:

```
d/dx ∫ₐˣ e^(-t²) dt = e^(-x²)
```

Funktionen S(x) = ∫ₐˣ e^(-t²) dt är en primitiv till e^(-x²), trots att den inte kan skrivas med vanliga funktioner.

**Exempel 5:** Kedjeregeln + analysens huvudsats. Om f(t) = ∫₀^(2√t) e^(-u²) du, beräkna f'(t):

```
Sätt S(x) = ∫₀ˣ e^(-u²) du,  så f(t) = S(2√t)

f'(t) = S'(2√t) · (2√t)' = e^(-4t) · 1/√t
```

---

## Insättningsformeln — det praktiska verktyget

**SATS 10. (INSÄTTNINGSFORMELN)** *Om f är kontinuerlig i [a,b] och F är en primitiv funktion till f, så gäller:*

```
∫ₐᵇ f(t) dt = F(b) - F(a)
```

Högerledet skrivs ofta med hakparentesnotation:

```
∫ₐᵇ f(t) dt = [F(t)]ₐᵇ = F(b) - F(a)
```

### Bevisidé

Enligt analysens huvudsats är S(x) = ∫ₐˣ f(t) dt en primitiv till f. Eftersom F också är en primitiv, skiljer de sig med en konstant: S(x) = F(x) + C. Sätt x = a: S(a) = 0 ger C = -F(a). Sätt x = b: S(b) = F(b) - F(a). ∎

> 🎯 **Det här är den formel du använder mest!** Istället för att beräkna Riemannsummor (jobbigt!) hittar du en primitiv funktion F och sätter in gränserna.

### Exempel 6: ∫₀¹ eˣ dx

```
∫₀¹ eˣ dx = [eˣ]₀¹ = e¹ - e⁰ = e - 1
```

(Jämför med den långa Riemannsummeberäkningen i kapitel 6.2!)

### Exempel 7: Arean mellan x-axeln och y = (x+1)/(x+2), 1 ≤ x ≤ 2

```
∫₁² (x+1)/(x+2) dx = ∫₁² (1 - 1/(x+2)) dx = [x - ln|x+2|]₁² 
                     = (2 - ln 4) - (1 - ln 3) = 1 - ln(4/3)
```

---

## Partiell integration och variabelsubstitution (bestämda integraler)

### Partiell integration

Formeln för primitiva funktioner överförs direkt till bestämda integraler:

```
∫ₐᵇ f(x)g(x) dx = [F(x)g(x)]ₐᵇ - ∫ₐᵇ F(x)g'(x) dx
```

### Variabelsubstitution

Substitutionsformeln för bestämda integraler:

```
∫ₐᵇ f(x) dx = ∫_α^β f(g(t)) g'(t) dt
```

där a = g(α) och b = g(β).

> ⚠️ **Viktigt:** Vid variabelsubstitution i bestämda integraler måste man **byta integrationsgränserna** från a,b till α,β. Man behöver inte gå tillbaka till variabeln x.

### Exempel 8: Beräkna ∫₂³ x³ · e^(x²) dx

Substitution: x² = t, 2x dx = dt:

```
∫₂³ x³ · e^(x²) dx = (1/2) ∫₄⁹ t · eᵗ dt
```

Sedan partiell integration:

```
= (1/2) ([teᵗ]₄⁹ - ∫₄⁹ eᵗ dt) = (1/2)(9e⁹ - 4e⁴ - [eᵗ]₄⁹) = (1/2)(8e⁹ - 3e⁴)
```

---

# 🧠 Sammanfattning: Vad du bör kunna

### Kapitel 6.1 — Integralens definition

- [ ] **Trappfunktion:** Definition (konstant på öppna delintervall) och dess integral som summan Σ cₖ(xₖ - xₖ₋₁)
- [ ] **Räkneregler** för trappfunktioners integraler: linjäritet, monotonitet, intervalladditivitet (sats 1)
- [ ] **Riemannintegrerbar:** Definitionen med ε-klämning av trappfunktioner (def 2)
- [ ] Att integralen är ett **entydigt bestämt tal** (sats 2, def 3)
- [ ] **Riemannsumma:** Definition och koppling till trappfunktionsintegralen
- [ ] Skillnaden mellan bestämd integral ∫ₐᵇ f(x)dx (ett **tal**) och obestämd integral ∫ f(x)dx (en **funktion**)

### Kapitel 6.2 — Integration av kontinuerliga funktioner

- [ ] **Sats 3:** Kontinuerliga funktioner på [a,b] är integrerbara
- [ ] **Bevisidén:** Likformig kontinuitet → övre/undre trappfunktioner med liten skillnad
- [ ] **Styckvis kontinuerliga** funktioner är också integrerbara
- [ ] **Sats 4:** Riemannsumman konvergerar till integralen vid finare indelning
- [ ] Kunna **beräkna** integraler med Riemannsummor (t.ex. ∫₀¹ eˣ dx via geometrisk summa)

### Kapitel 6.3 — Räknelagar och uppskattningar

- [ ] **Sats 5:** Räknereglerna (9)–(12) för integraler
- [ ] **Konventionen** ∫ₐᵇ f(x)dx = -∫ᵇₐ f(x)dx
- [ ] **Uppskattning** av integraler med monotonitet: m(b-a) ≤ ∫ₐᵇ f(x)dx ≤ M(b-a)
- [ ] **Sats 6:** Triangelolikheten |∫ₐᵇ f(x)dx| ≤ ∫ₐᵇ |f(x)|dx
- [ ] **Sats 7:** Integralkalkylens medelvärdessats: ∫ₐᵇ f(x)dx = f(ξ)(b-a)
- [ ] **Sats 8:** Generaliserade medelvärdessatsen

### Kapitel 6.4 — Beräkning av integraler

- [ ] **Sats 9 (Analysens huvudsats):** Om S(x) = ∫ₐˣ f(t)dt, så S'(x) = f(x) — *detta är den viktigaste satsen!*
- [ ] Bevisidén: differenskvot + medelvärdessatsen + kontinuitet
- [ ] **Sats 10 (Insättningsformeln):** ∫ₐᵇ f(t)dt = F(b) - F(a)
- [ ] Kunna beräkna integraler med insättningsformeln
- [ ] **Partiell integration** och **variabelsubstitution** för bestämda integraler
- [ ] Kunna använda **kedjeregeln + analysens huvudsats** (ex: derivera ∫₀^(2√t) e^(-u²) du)

---

## 📌 Formler att memorera

| Formel | Referens |
|--------|----------|
| I(Φ) = Σ cₖ(xₖ - xₖ₋₁) | Def 1: Trappfunktions integral |
| Rᴅ = Σ f(ξₖ)(xₖ - xₖ₋₁) | Riemannsumma |
| ∫ₐᵇ f dx = -∫ᵇₐ f dx | Konvention |
| \|∫ₐᵇ f dx\| ≤ ∫ₐᵇ \|f\| dx | Sats 6: Triangelolikheten |
| ∫ₐᵇ f dx = f(ξ)(b-a) | Sats 7: MVS för integraler |
| d/dx ∫ₐˣ f(t)dt = f(x) | Sats 9: Analysens huvudsats |
| ∫ₐᵇ f(t)dt = F(b) - F(a) | Sats 10: Insättningsformeln |
| ∫ₐᵇ f·g dx = [F·g]ₐᵇ - ∫ₐᵇ F·g' dx | Partiell integration |
| ∫ₐᵇ f(x) dx = ∫_α^β f(g(t))g'(t) dt | Variabelsubstitution |

---

## 💡 Den röda tråden

Hela kapitel 6 bygger en **logisk kedja**:

1. **Trappfunktioner** → enkel definition av "integral" som summa av rektanglar
2. **Riemannintegralen** → utvidga till alla begränsade funktioner genom att klämma med trappfunktioner
3. **Kontinuerliga funktioner är integrerbara** → den viktiga funktionsklassen vi arbetar med
4. **Räknelagar** → samma som för trappfunktioner (linjäritet, monotonitet, additivitet)
5. **Analysens huvudsats** → kopplar derivering och integration: d/dx ∫ₐˣ f(t)dt = f(x)
6. **Insättningsformeln** → praktiskt verktyg: ∫ₐᵇ f dx = F(b) - F(a)

Steg 5 är det centrala: det visar **varför** primitiva funktioner (kapitel 5) är relevanta för att beräkna areor (kapitel 6). Derivering och integration är *inversa operationer* — och det är analysens mest fundamentala insikt.
