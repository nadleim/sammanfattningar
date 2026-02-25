# 📐 Kapitel 3.5 & 3.6 — Egenskaper hos deriverbara funktioner & Derivator av högre ordning

## Omfattande sammanfattning och genomgång

*Baserad på kursboken (sidorna 209–221) och föreläsning 14*

---

# 🔷 KAPITEL 3.5 — Egenskaper hos deriverbara funktioner

## 3.5.1 Lokala extremvärden — Definitioner

### Vad är ett lokalt extremvärde?

Vi vill formalisera idén om "toppar" och "dalar" hos en funktion. I gymnasiet lärde du dig att extrempunkter är ställen där funktionen "vänder" — nu ger vi detta en exakt definition.

**DEFINITION 2.** Låt x₀ vara en punkt i definitionsmängden D_f till en funktion f.

**Lokalt maximum:**
Vi säger att f har ett **lokalt maximum** i x₀ om det finns ett tal δ > 0 sådant att

```
|x − x₀| < δ  }
              ⟹  f(x) ≤ f(x₀)
x ∈ D_f      }
```

> 💡 **I klartext:** f(x₀) är *det största funktionsvärdet i en liten omgivning* runt x₀. Du behöver alltså inte ha det absolut största värdet — bara det största *lokalt*.

Vi kallar x₀ en **lokal maximipunkt** och f(x₀) ett **lokalt maximivärde**. Om dessutom f(x) < f(x₀) för alla x ≠ x₀ i omgivningen talar vi om **strängt** lokalt maximum.

**Lokalt minimum:**
På motsvarande sätt definieras **lokal minimipunkt** och **lokalt minimivärde** — bara med olikheten omvänd:

```
f(x) ≥ f(x₀)  för alla x ∈ D_f med |x − x₀| < δ
```

**Samlingsnamn:**
- Lokala maximipunkter och lokala minimipunkter kallas gemensamt **lokala extrempunkter**
- f sägs ha ett **lokalt extremvärde** i dessa punkter

### Viktiga observationer om extremvärden

1. **Lokalt ≠ globalt:** Ett lokalt maximum behöver *inte* vara funktionens absolut största värde. En funktion kan ha lokala maxima i x₁ och globalt maximum i en helt annan punkt.

2. **Extrempunkter kan finnas utan att f'(x₀) = 0!** Det finns två situationer utöver stationära punkter:
   - **Intervallgränser (ändpunkter):** Funktionen f(x) på [a,b] kan ha sitt maximum i ändpunkten a eller b
   - **Icke deriverbara punkter:** Funktionen f(x) = |x| har ett lokalt minimum i x = 0, men f'(0) existerar inte!

> 🎯 **Nyckelfråga:** Hur definierar vi "lokala extrempunkter" formellt? Med δ-omgivningar — precis som vi gjorde med gränsvärden i kapitel 2!

---

## 3.5.2 Stationära punkter

**DEFINITION:** Punkter i vilka f har derivatan noll, dvs. där funktionens tillväxthastighet är noll, kallas **stationära** punkter.

```
f'(x₀) = 0  ⟹  x₀ är en stationär punkt
```

Stationära punkter kan vara:
- **Lokalt minimum** (dalgång)
- **Lokalt maximum** (bergtopp)  
- **Terrasspunkt** (varken topp eller dal — funktionen planar ut men vänder inte)

> ⚠️ **OBS:** Innebörden av sats 13 är att — förutom i eventuella ändpunkter — **extremvärden bara kan förekomma i stationära punkter**. Men: detta gäller bara för funktioner som är deriverbara i hela sin definitionsmängd!
>
> Motexempel: f(x) = |x| har lokalt minimum i x = 0 men är inte deriverbar där.

---

## 3.5.3 Sats 13 — Nödvändigt villkor för extremvärde

> **SATS 13.** *Om funktionen f har lokalt extremvärde i en inre punkt x₀ i definitionsintervallet och om f är deriverbar i x₀ så är*
>
> **f'(x₀) = 0**

### Bevis (ur boken, förenklat)

Vi betraktar fallet att f har ett lokalt maximum i x₀ (det andra fallet bevisas analogt).

**Steg 1:** För alla tillräckligt små |h| gäller, enligt definitionen av lokalt maximum:

```
f(x₀ + h) − f(x₀) ≤ 0
```

**Steg 2:** Bilda differenskvoten:

- Om h > 0: differenskvoten (f(x₀+h) − f(x₀))/h ≤ 0 (negativt/positivt = negativt)
- Om h < 0: differenskvoten (f(x₀+h) − f(x₀))/h ≥ 0 (negativt/negativt = positivt)

**Steg 3:** Ta gränsvärden:

```
f'(x₀) = lim(h→0⁺) [f(x₀+h) − f(x₀)] / h  ≤ 0

f'(x₀) = lim(h→0⁻) [f(x₀+h) − f(x₀)] / h  ≥ 0
```

Eftersom derivatan existerar måste höger- och vänstergränsvärdet vara lika. Det enda talet som är *både* ≤ 0 och ≥ 0 är noll. Alltså f'(x₀) = 0. ∎

> ⚠️ **Observera:** Omvändningen av denna sats är *inte* sann! Att f'(x₀) = 0 innebär **inte** automatiskt att x₀ är en extrempunkt.
>
> **Motexempel:** f(x) = x³ har f'(0) = 0, men x = 0 är *inte* ett extremvärde utan en terrasspunkt!

**Satsen ger alltså ett nödvändigt men inte tillräckligt villkor.** Derivatan noll säger "här *kan* det vara en extrempunkt" — men vi behöver fler verktyg för att avgöra om det verkligen *är* det.

---

## 3.5.4 Andraderivatan och extrempunkter

Andraderivatan kan hjälpa oss avgöra *typen* av stationär punkt, dvs. karaktärisera extrempunkter där f'(a) = 0:

| Villkor | Slutsats |
|---------|----------|
| f''(a) > 0 | a är en **lokal minimipunkt** (kurvan är "skålformad", konkav uppåt) |
| f''(a) < 0 | a är en **lokal maximipunkt** (kurvan är "kupolformad", konkav nedåt) |
| f''(a) = 0 | **Säger ingenting!** Kan vara min, max eller terrasspunkt |

> 💡 **Intuition:** Om f'(a) = 0 (horisontell tangent) och f''(a) > 0 (derivatan *ökar*), så gick derivatan från negativ till positiv runt a — alltså gick funktionen från avtagande till växande, dvs. en dal = lokalt minimum.

### Genomgånget exempel från föreläsningen: f(x) = e^(-x²) · x

**Steg 1:** Beräkna f'(x):

```
f'(x) = e^(-x²)(-2x²) + e^(-x²) = e^(-x²)(1 − 2x²)
```

**Steg 2:** Hitta stationära punkter genom f'(x) = 0:

Eftersom e^(-x²) > 0 alltid, behöver vi bara lösa:
```
1 − 2x² = 0  ⟹  x = ±1/√2
```

**Steg 3:** Beräkna f''(x) och utvärdera:

```
f''(x) = e^(-x²)(4x³ − 6x)
```

I x = 1/√2:
```
f''(1/√2) = e^(-1/2) · (4/(2√2) − 6/√2) = e^(-1/2) · (1/√2)(−4) < 0
```
⟹ **Maximipunkt** i x = 1/√2

I x = −1/√2:
```
f''(−1/√2) = −f(1/√2) > 0
```
⟹ **Minimipunkt** i x = −1/√2

### Viktigt motexempel: f''(a) = 0 säger ingenting!

| Funktion | f'(0) | f''(0) | Typ av punkt |
|----------|-------|--------|-------------|
| f(x) = x⁴ | 0 | 0 | Minimum (!) |
| g(x) = x³ | 0 | 0 | Terrasspunkt |

Båda har f'(0) = 0 och f''(0) = 0, men den ena är en extrempunkt och den andra inte. Man behöver i sådana fall studera tecknet hos f' i omgivningen av a, eller använda högre derivator.

---

## 3.5.5 Medelvärdessatsen

Medelvärdessatsen (MVS) är en av de allra viktigaste satserna i hela analysen. Den kopplar ihop en funktions *genomsnittliga* förändring med dess *momentana* förändring.

> **SATS 14. (MEDELVÄRDESSATSEN)** *Antag att f är kontinuerlig i det slutna intervallet a ≤ x ≤ b och deriverbar i det öppna intervallet a < x < b. Då finns minst en punkt ξ, a < ξ < b, sådan att*
>
> **(28):**  f(b) − f(a) = f'(ξ)(b − a)

Eller, ekvivalent skrivet:

```
f(b) − f(a)
─────────── = f'(ξ)
    b − a
```

### Geometrisk tolkning

```
         y
         │      ╱·  
         │    ╱ · ·╲    
         │  ╱·     ·╲    ← tangent i ξ (parallell med sekanten!)
         │╱ ·   ξ   ·b
         a─────────────── x
```

- **Vänstra ledet** = lutningen på **sekanten** (den räta linjen) genom (a, f(a)) och (b, f(b))
- **Högra ledet** = lutningen på **tangenten** i punkten (ξ, f(ξ))

**Alltså:** Någonstans mellan a och b finns det en punkt ξ där tangentens lutning är *exakt lika med* sekantens lutning. Med andra ord: det finns alltid en punkt där den momentana förändringshastigheten matchar den genomsnittliga förändringshastigheten!

> 🚗 **Analog:** Om du kör 150 km på 2 timmar (genomsnittshastighet 75 km/h), så måste det funnits åtminstone ett ögonblick där din hastighetsmätare visade exakt 75 km/h.

### Bevis av medelvärdessatsen

**Idé:** Konstruera en hjälpfunktion φ som mäter det lodräta avståndet mellan kurvan y = f(x) och sekanten.

**Steg 1:** Linjen ℓ genom (a, f(a)) och (b, f(b)) har ekvationen:

```
y = f(a) + [f(b) − f(a)]/(b − a) · (x − a)
```

**Steg 2:** Definiera hjälpfunktionen:

```
φ(x) = f(x) − f(a) − [f(b) − f(a)]/(b − a) · (x − a)
```

**Steg 3:** Observera att φ(a) = 0 och φ(b) = 0.

**Steg 4:** φ är kontinuerlig på [a,b], alltså antar den sitt högsta och lägsta värde (egenskapen (2.15), se sidan 154).

- Om dessa extremvärden båda infaller i ändpunkterna a och b, så är φ(x) = 0 för alla x ∈ [a,b] (ty φ(a) = φ(b) = 0 och de är extremvärden). Då är f redan en rät linje med lutning [f(b)−f(a)]/(b−a), och man kan välja ξ godtyckligt.

- Om minst ett extremvärde infaller i en *inre* punkt ξ ∈ \]a,b\[, så har φ ett lokalt extremvärde där. Eftersom φ är deriverbar på \]a,b\[ ger sats 13 att φ'(ξ) = 0.

**Steg 5:** Beräkna φ'(x):

```
φ'(x) = f'(x) − [f(b) − f(a)]/(b − a)
```

Sätter vi φ'(ξ) = 0 får vi direkt:

```
f'(ξ) = [f(b) − f(a)]/(b − a)  ∎
```

> 🎯 **Bevisidé att komma ihåg:** Vi subtraherar sekantlinjen från f för att få en funktion som är noll i ändpunkterna, och sedan tillämpar vi sats 13 (derivatan = 0 i extrempunkter).

### Tillämpning 1: Uppskattning med medelvärdessatsen

Medelvärdessatsen kan användas för att ge *konkreta numeriska begränsningar* på funktionsvärden.

**Exempel från föreläsningen:** Antag att f är deriverbar och att f'(x) ≤ 4 för alla x ∈ ℝ. Om f(0) = 1, hur stor kan f(3) vara?

**Lösning:** Medelvärdessatsen ger att det finns ett z, 0 < z < 3, sådant att:

```
f'(z) = [f(3) − f(0)] / 3
```

Alltså:
```
3 · f'(z) + f(0) = f(3)
```

Men f'(z) ≤ 4, så:
```
f(3) = f(0) + 3·f'(z) ≤ 1 + 3·4 = 13
```

**Svar:** f(3) kan vara **högst 13**.

### Tillämpning 2: Existenssatser

**Exempel 20 (ur boken):** Om ekvationen f(x) = 0 har två skilda rötter x₁ och x₂, så har ekvationen f'(x) = 0 minst en rot mellan x₁ och x₂.

**Bevis:** Enligt medelvärdessatsen:

```
0 = f(x₂) − f(x₁) = (x₂ − x₁)·f'(ξ)
```

Eftersom x₂ − x₁ ≠ 0 följer f'(ξ) = 0. ∎

### Tillämpning 3: Visa olikheter

**Exempel 21 (ur boken):** Visa att |sin x₂ − sin x₁| ≤ |x₂ − x₁| för alla x₁ och x₂.

**Bevis:** Medelvärdessatsen ger:

```
sin x₂ − sin x₁ = (x₂ − x₁)·cos ξ
```

Eftersom |cos ξ| ≤ 1 följer olikheten direkt. ∎

> 💡 **Mer generellt:** Om |f'(x)| ≤ C i ett intervall, ger medelvärdessatsen uppskattningen |f(x₂) − f(x₁)| ≤ C·|x₂ − x₁|. Sådana funktioner kallas **Lipschitz-kontinuerliga**.

---

## 3.5.6 Monotonicitet av deriverbara funktioner

### Konstanta funktioner har nollderivata

> **SATS 15.** *Om funktionen f är deriverbar i intervallet a < x < b och om f'(x) = 0 för alla x i detta intervall, så är f en konstant funktion.*

**Bevis:** Låt c vara en fix punkt och x en godtycklig punkt i \]a,b\[. Medelvärdessatsen ger:

```
f(x) − f(c) = f'(ξ)·(x − c) = 0·(x − c) = 0
```

Alltså f(x) = f(c) = konstant för alla x ∈ ]a,b[. ∎

### Följdsats 1: Lika derivata ⟹ funktionerna skiljer sig med en konstant

> **FÖLJDSATS 1.** *Om f'(x) = g'(x) för a < x < b, så är f(x) = g(x) + C för någon konstant C.*

**Bevis:** Tillämpa sats 15 på funktionen f(x) − g(x), vars derivata är 0 överallt. ∎

> 💡 **Varför är detta viktigt?** Detta resultat är *fundamentalt* för integralkalkyl och differentialekvationer! Det är anledningen till att primitiva funktioner alltid har en godtycklig konstant "+C".

### Huvudsats: Derivatans tecken bestämmer monotonicitet

> **SATS 16.** *Om funktionen f är deriverbar med f'(x) > 0 för a < x < b, så är f strängt växande i \]a,b\[. Om dessutom f är kontinuerlig i ändpunkterna a och b, är funktionen strängt växande i [a,b].*

**Bevis:** Låt x₁ och x₂ vara två punkter med a < x₁ < x₂ < b (eller a ≤ x₁ < x₂ ≤ b i det andra fallet). Medelvärdessatsen ger:

```
f(x₂) − f(x₁) = (x₂ − x₁)·f'(ξ)
```

för något ξ mellan x₁ och x₂. Eftersom:
- x₂ − x₁ > 0 (vi valde x₂ > x₁)
- f'(ξ) > 0 (enligt förutsättningen)

följer att f(x₂) − f(x₁) > 0, dvs. f(x₁) < f(x₂). ∎

### Sammanfattande tabell: Derivatans tecken och monotonicitet

| Villkor på derivatan | Slutsats om f |
|---------------------|---------------|
| f'(x) ≥ 0 för a < x < b | f är **växande** |
| f'(x) > 0 för a < x < b | f är **strängt växande** |
| f'(x) ≤ 0 för a < x < b | f är **avtagande** |
| f'(x) < 0 för a < x < b | f är **strängt avtagande** |

> 💡 **Intuition:** Positiv derivata = positiv lutning = funktionen pekar uppåt = växande. Negativ derivata = negativ lutning = funktionen pekar nedåt = avtagande. Enklast möjliga koppling!

### Följdsats 2: Strängt växande trots enstaka nollor i derivatan

> **FÖLJDSATS 2.** *Om f'(x) ≥ 0 i ett intervall och likhet bara inträffar i ett ändligt antal punkter, så är f strängt växande i intervallet.*

**Bevis:** Använd sats 16 på delintervall mellan de enstaka nollställena, och koppla sedan ihop slutsatserna.

**Exempel 23:** f(x) = x³ är strängt växande, ty f'(x) = 3x² ≥ 0 med likhet bara i en enda punkt (x = 0).

### Sats 17: Darboux egenskap (derivatans mellanvärdesegenskap)

Avslutningsvis, ett överraskande resultat:

> **SATS 17. (DARBOUX)** *Antag att funktionen f är deriverbar i intervallet [a,b], och att f'(a) ≠ f'(b). Då antar derivatan f' i intervallet a < x < b varje värde μ strikt mellan f'(a) och f'(b).*

Detta innebär att *derivatan har mellanvärdessatsen*, trots att derivatan inte behöver vara kontinuerlig! En derivata kan aldrig "hoppa" över ett värde.

---

# 🔷 KAPITEL 3.6 — Derivator av högre ordning

## 3.6.1 Definition

Vi vet redan från avsnitt 3.2 att det kan finnas anledning att studera *andraderivatan* av en funktion. Genom att derivera upprepat definierar vi derivator av godtycklig ordning:

> **DEFINITION:** Derivatan av ordning n definieras rekursivt:
>
> D^n f = D(D^(n−1) f) = (f^(n−1))' = f^(n)

### Beteckningar

Man skriver derivatan av ordning n som:

```
f⁽ⁿ⁾,    Dⁿf,    dⁿf/dxⁿ,    dⁿy/dxⁿ,    etc.
```

Det är ibland bekvämt att skriva f⁽⁰⁾ och D⁰f för f själv.

> 💡 **Minnesregel från föreläsningen:** Andra derivatan av f är *derivatan av derivatan* av f:
> D²(f) = D(D(f)) = (f')' = f''

---

## 3.6.2 Högre derivator av elementära funktioner

### Exponentialfunktionen — enklaste fallet!

```
Dⁿ eˣ = eˣ       n = 1, 2, 3, ...
```

Exponentialfunktionen är sin egen derivata, oavsett hur många gånger man deriverar!

### Polynom

Om p(x) är ett polynom av grad k, så blir p⁽ⁿ⁾(x) = 0 för n > k.

> 💡 Varje derivering sänker graden med 1. Efter k+1 deriveringar återstår bara noll.

### Potensfunktioner: Dⁿ xᵅ

```
D¹ xᵅ = α·xᵅ⁻¹
D² xᵅ = α(α−1)·xᵅ⁻²
```

Allmänt:

**(30):** Dⁿ xᵅ = α(α−1)···(α−n+1)·xᵅ⁻ⁿ

**Specialfall α = −1 (ln x):**

```
Dⁿ ln x = (−1)ⁿ⁻¹ · (n−1)! / xⁿ
```

> 🎯 Formel (31) är bra att kunna: notera (−1)^(n−1) som ger alternerande tecken, och (n−1)! i täljaren.

### Trigonometriska funktioner

Med hjälp av omskrivningen D sin x = cos x = sin(x + π/2) kan man genom upprepad derivering visa:

**(32):** Dⁿ sin x = sin(x + nπ/2)

**(33):** Dⁿ cos x = cos(x + nπ/2)

> 💡 **Cosinusexempel från föreläsningen:**
> ```
> g(x) = cos(x)
> g'(x) = −sin(x)
> g''(x) = −cos(x)
> g'''(x) = sin(x)
> g⁽⁴⁾(x) = cos(x) = g(x)  ← Tillbaka till start efter 4 deriveringar!
> ```
>
> Sinusföljden upprepar sig med period 4: sin → cos → −sin → −cos → sin → ...

### Exempel 24 (ur boken): Dⁿ(eˣ sin x)

```
Dⁿ(eˣ sin x) = eˣ · (√2)ⁿ · sin(x + nπ/4)
```

Detta följer genom att skriva om: D(eˣ sin x) = eˣ(sin x + cos x) = eˣ√2 sin(x + π/4), och sedan upprepa!

---

## 3.6.3 Räkneregler för högre derivator

### Additivitet (summaregeln)

```
Dⁿ(f + g) = Dⁿf + Dⁿg
```

Precis som den vanliga summaregeln — den gäller i varje steg, alltså i alla steg!

### Leibniz' formel — Produktregeln för n-te derivatan

> **SATS 18. (LEIBNIZ' FORMEL)** *Om funktionerna f och g är n gånger deriverbara, så är detsamma fallet med deras produkt fg och*
>
> **(34):** Dⁿ(f·g) = Σₖ₌₀ⁿ C(n,k) · Dⁿ⁻ᵏf · Dᵏg

där C(n,k) = n! / (k!(n−k)!) är binomialkoefficienten.

> 🎯 **Jämför med binomialsatsen!** Precis som (a+b)ⁿ = Σ C(n,k) aⁿ⁻ᵏ bᵏ, men med derivator istället för potenser. Från föreläsningen noterades denna koppling explicit.

### Utskrivet för de första fallen:

**n = 1 (vanlig produktregeln):**
```
D(fg) = f'g + fg'
```

**n = 2:**
```
D²(fg) = f''g + 2f'g' + fg''
```

**n = 3:**
```
D³(fg) = f'''g + 3f''g' + 3f'g'' + fg'''
```

Koefficienterna 1, 2, 1 och 1, 3, 3, 1 är precis **Pascals triangel** — binomialkoefficienterna!

### Bevis (induktion)

**Basfall n = 1:** D(fg) = (Df)g + f(Dg), vilket är precis den vanliga produktregeln ✓

**Induktionssteg:** Antag att (34) gäller för n = p−1. Derivera båda sidor:

```
Dᵖ(fg) = D(Dᵖ⁻¹(fg)) = D[Σₖ₌₀ᵖ⁻¹ C(p−1,k) Dᵖ⁻¹⁻ᵏf · Dᵏg]
```

Genom att använda produktregeln på varje term och slå ihop summorna med hjälp av identiteten för binomialkoefficienter:

```
C(p−1,k) + C(p−1,k−1) = C(p,k)
```

erhålls formel (34) för n = p. ∎

### Exempel 25 (ur boken): Beräkna Dⁿ(eˣ · x²) för n > 2

**Lösning:** Eftersom Dᵏx² = 0 för k > 2, ger Leibniz' formel bara tre termer:

```
Dⁿ(eˣ · x²) = Σₖ₌₀² C(n,k) · Dⁿ⁻ᵏeˣ · Dᵏx²

= eˣ · x² + n · eˣ · 2x + n(n−1)/2 · eˣ · 2

= eˣ(x² + 2nx + n² − n)
```

---

## 🧠 Sammanfattning: Vad du bör kunna

### Kapitel 3.5 — Egenskaper hos deriverbara funktioner

- [ ] **Definitionerna** av lokalt maximum/minimum (med δ-omgivning)
- [ ] Skillnaden mellan **stationära punkter**, **extrempunkter** och **terrasspunkter**
- [ ] **Sats 13:** f'(x₀) = 0 i inre extrempunkter — och att detta är *nödvändigt* men inte *tillräckligt*
- [ ] **Andraderivatatest:** f''(a) > 0 ⟹ minimum, f''(a) < 0 ⟹ maximum, f''(a) = 0 ⟹ **vet ej**
- [ ] **Medelvärdessatsen** (sats 14): Formulering, geometrisk tolkning och bevisidé
- [ ] **Tillämpa MVS** för uppskattning av funktionsvärden
- [ ] **Tillämpa MVS** för att visa att ekvationer har rötter (existenssatser)
- [ ] **Sats 15:** f'(x) = 0 överallt ⟹ f är konstant
- [ ] **Följdsats 1:** f'(x) = g'(x) ⟹ f(x) = g(x) + C (fundamentalt för integration!)
- [ ] **Sats 16:** Derivatans tecken bestämmer monotonicitet (växande/avtagande)
- [ ] **Följdsats 2:** Strängt växande trots enstaka nollor i derivatan

### Kapitel 3.6 — Derivator av högre ordning

- [ ] **Definitionen** av Dⁿf = D(Dⁿ⁻¹f) (rekursiv definition)
- [ ] **Elementära formler:** Dⁿ eˣ, Dⁿ xᵅ, Dⁿ sin x, Dⁿ cos x, Dⁿ ln x
- [ ] **Additivitet:** Dⁿ(f+g) = Dⁿf + Dⁿg
- [ ] **Leibniz' formel** (sats 18) och kopplingen till binomialsatsen
- [ ] Kunna beräkna Dⁿ för specifika funktioner (t.ex. eˣ·x², eˣ·sin x)

---

## 📌 Formler att memorera

| Formel | Referens |
|--------|----------|
| f'(x₀) = 0 vid inre extrempunkter | Sats 13 |
| f(b) − f(a) = f'(ξ)(b − a) | Sats 14 (MVS) |
| f'(x) = 0 ∀x ⟹ f konstant | Sats 15 |
| f'(x) > 0 ⟹ f strängt växande | Sats 16 |
| Dⁿ xᵅ = α(α−1)···(α−n+1) xᵅ⁻ⁿ | Formel (30) |
| Dⁿ ln x = (−1)ⁿ⁻¹ (n−1)!/xⁿ | Formel (31) |
| Dⁿ sin x = sin(x + nπ/2) | Formel (32) |
| Dⁿ cos x = cos(x + nπ/2) | Formel (33) |
| Dⁿ(fg) = Σ C(n,k) Dⁿ⁻ᵏf Dᵏg | Sats 18 (Leibniz) |
