# 📐 Kapitel 6.5 & 7.9 — Generaliserade integraler, Integraler och summor

## Omfattande sammanfattning och genomgång

*Baserad på kursboken (sidorna 311–320 och 350–355)*
*Komplement till sammanfattningen av kapitel 6.1–6.4*

---

# 🔷 KAPITEL 6.5 — Generaliserade integraler

## Varför behöver vi generalisera?

Riemannintegralen (kap 6.1) kräver att:
1. Intervallet [a,b] är **ändligt** (begränsat)
2. Funktionen f är **begränsad** på intervallet

Men i praktiken stöter vi ofta på integraler som bryter mot ett eller båda av dessa krav. Till exempel:

- ∫₁^∞ 1/x² dx — oändligt långt intervall
- ∫₀¹ 1/√x dx — funktionen "exploderar" i x = 0

Lösningen: vi definierar integralen som ett **gränsvärde** av vanliga Riemannintegraler.

---

## Fall 1: Oändligt definitionsintervall

### Definition

Betrakta en funktion f definierad på [a, ∞[ som är Riemannintegrerbar över varje begränsat delintervall [a, X].

**DEFINITION 4.** Om gränsvärdet

```
lim    ∫ₐˣ f(x) dx = A
X→+∞
```

existerar, säges den generaliserade integralen ∫ₐ^∞ f(x) dx vara **konvergent** med värdet A. Om gränsvärdet inte existerar är integralen **divergent**.

> 💡 **Tillvägagångssätt:** Man beräknar den "vanliga" integralen ∫ₐˣ f(x) dx (med insättningsformeln eller annan teknik) och undersöker sedan om resultatet har ett gränsvärde när X → ∞.

### Exempel 9: ∫₀^∞ e⁻ˣ dx — konvergent

```
∫₀ˣ e⁻ˣ dx = [-e⁻ˣ]₀ˣ = -e⁻ˣ + 1 → 1    då X → ∞
```

Alltså: ∫₀^∞ e⁻ˣ dx = 1. ✓

> 💡 **Geometriskt:** Arean under kurvan y = e⁻ˣ från 0 till ∞ är *ändlig* (= 1), trots att området sträcker sig oändligt långt åt höger. Funktionen avtar så snabbt att den "kompenserar" för det oändliga intervallet.

### Exempel 10: ∫₀^∞ sin x dx — divergent

```
∫₀ˣ sin x dx = [-cos x]₀ˣ = -cos X + 1
```

Uttrycket -cos X + 1 oscillerar mellan 0 och 2 när X → ∞ — det saknar gränsvärde. Integralen är divergent. ✓

### Exempel 11: ∫₁^∞ 1/x dx — divergent!

```
∫₁ˣ 1/x dx = [ln|x|]₁ˣ = ln X → ∞    då X → ∞
```

> ⚠️ **Det här är kanske det viktigaste exemplet!** 1/x avtar, men inte "tillräckligt snabbt". Arean under 1/x från 1 till ∞ är oändlig.

### ⭐ Exempel 12: Standardresultatet för 1/xᵅ (MEMORERA!)

```
∫₁^∞ 1/xᵅ dx  är  { konvergent   om α > 1
                     { divergent    om α ≤ 1
```

**Beräkning för α ≠ 1:**

```
∫₁ˣ 1/xᵅ dx = [x^(1-α) / (1-α)]₁ˣ = 1/(1-α) · (X^(1-α) - 1)
```

- Om α > 1: exponenten 1-α < 0, så X^(1-α) → 0 när X → ∞. Gränsvärde = 1/(α-1). ✓
- Om α < 1: exponenten 1-α > 0, så X^(1-α) → ∞. Divergent. ✗
- Om α = 1: detta är ∫ 1/x dx = ln X → ∞. Divergent. ✗

> 🎯 **Gränsen ligger vid α = 1.** Funktionen 1/x är "precis för långsam" i sin avtagning — den ger divergens. Allt som avtar snabbare (α > 1) ger konvergens.

### Integraler från -∞

Konvergens och divergens av ∫₋∞ᵇ f(x) dx definieras analogt: som gränsvärdet av ∫_Xᵇ f(x) dx när X → -∞.

---

## Fall 2: Obegränsad integrand

Här är intervallet [a,b] ändligt, men funktionen f(x) → ±∞ i någon punkt (vanligtvis en ändpunkt).

### Definition

Betrakta f definierad i ]a, b] (inte nödvändigtvis i a) och integrerbar över varje [a+ε, b] för ε > 0.

**DEFINITION 5.** Om gränsvärdet

```
lim    ∫_(a+ε)ᵇ f(x) dx = A
ε→0⁺
```

existerar kallas den generaliserade integralen **konvergent** med värdet A.

> 💡 **Intuitivt:** Vi "klipper bort" en liten bit nära singulariteten och undersöker om arean stabiliseras när vi tar med mer och mer av det problematiska området.

### Exempel 13: ∫₁² 1/√(x-1) dx — konvergent

Integranden → ∞ när x → 1⁺. Beräkna:

```
∫_(1+ε)² 1/√(x-1) dx = [2√(x-1)]_(1+ε)² = 2 - 2√ε → 2    då ε → 0⁺
```

Alltså: ∫₁² 1/√(x-1) dx = 2. ✓

### Exempel 14: ∫₀¹ 1/x dx — divergent

```
∫_ε¹ 1/x dx = [ln|x|]_ε¹ = -ln ε → +∞    då ε → 0⁺
```

Divergent. (Samma funktion 1/x som var divergent vid ∞ är också divergent vid 0!)

### ⭐ Exempel 15: Standardresultatet för 1/xᵅ vid origo (MEMORERA!)

```
∫₀¹ 1/xᵅ dx  är  { konvergent   om α < 1
                    { divergent    om α ≥ 1
```

**Beräkning för α ≠ 1:**

```
∫_ε¹ 1/xᵅ dx = [x^(1-α)/(1-α)]_ε¹ = 1/(1-α) · (1 - ε^(1-α))
```

- Om α < 1: exponenten 1-α > 0, så ε^(1-α) → 0. Gränsvärde = 1/(1-α). ✓
- Om α > 1: exponenten 1-α < 0, så ε^(1-α) → ∞. Divergent. ✗
- Om α = 1: ∫ 1/x dx = -ln ε → ∞. Divergent. ✗

> 🎯 **Notera kontrasten med Fall 1!** Vid oändligt intervall: konvergent om α > 1. Vid singularitet i origo: konvergent om α < 1. Gränsen α = 1 ger *alltid* divergens.

---

## Jämförelsesatser — avgör konvergens utan att beräkna

Ofta kan man inte beräkna en generaliserad integral explicit, men man vill ändå veta om den konvergerar. Då använder man **jämförelse** med en känd standardintegral.

**SATS 11. (JÄMFÖRELSESATSEN)** Om 0 ≤ f(x) ≤ g(x) för alla x i integrationsintervallet, så gäller:

a) Om ∫ g(x) dx är **konvergent** ⟹ ∫ f(x) dx är också **konvergent**.
b) Om ∫ f(x) dx är **divergent** ⟹ ∫ g(x) dx är också **divergent**.

> 💡 **Intuitivt:**
> - (a) Om den "större" funktionen har ändlig area, så har den "mindre" det också.
> - (b) Om den "mindre" funktionen har oändlig area, så har den "större" det också.

### Strategi: Jämför med standardfunktioner!

Funktionerna 1/xᵅ (exempel 12 och 15) fungerar som **referensfunktioner**. Du jämför din integrand med 1/xᵅ för lämpligt α.

### Exempel 16: ∫₀¹ 1/(√x · eˣ) dx — konvergent

Integranden → ∞ när x → 0⁺. Vi behöver en uppskattning:

```
0 ≤ 1/(√x · eˣ) ≤ 1/√x    när 0 < x ≤ 1
```

(ty eˣ ≥ 1 för x ≥ 0). Och ∫₀¹ 1/√x dx = ∫₀¹ x^(-1/2) dx konvergerar (α = 1/2 < 1). Alltså konvergerar den ursprungliga integralen. ✓

### Exempel 17: ∫₁^∞ 1/(√x · eˣ) dx — konvergent

Här gäller istället:

```
0 ≤ 1/(√x · eˣ) ≤ 1/eˣ = e⁻ˣ    när x ≥ 1
```

Och ∫₁^∞ e⁻ˣ dx konvergerar (exempel 9). Alltså konvergerar integralen. ✓

### Exempel 18: ∫₁^∞ (arctan x)/x dx — divergent

Vi har:

```
(arctan x)/x ≥ (π/4)/x = (π/4) · (1/x)    när x ≥ 1
```

(ty arctan x ≥ π/4 för x ≥ 1). Och ∫₁^∞ 1/x dx divergerar. Alltså divergerar integralen. ✓

---

## Integraler generaliserade på flera sätt

En integral kan vara generaliserad vid **flera punkter** samtidigt. Då delar man upp:

### Exempel 19: ∫₀^∞ 1/(√x · eˣ) dx

Generaliserad i **både** 0 (integrand → ∞) och ∞ (oändligt intervall). Dela upp:

```
∫₀^∞ 1/(√x · eˣ) dx = ∫₀¹ 1/(√x · eˣ) dx + ∫₁^∞ 1/(√x · eˣ) dx
```

Båda delarna konvergerar (exempel 16 och 17), alltså konvergerar hela integralen. ✓

### Exempel 20: ∫₀^∞ 1/xᵅ dx — ALLTID divergent!

Dela upp i ∫₀¹ 1/xᵅ dx + ∫₁^∞ 1/xᵅ dx.

- Om α < 1: första delen konvergerar, men andra divergerar (kräver α > 1)
- Om α ≥ 1: första delen divergerar redan

Alltså: för **inget** val av α konvergerar båda delarna. Integralen ∫₀^∞ 1/xᵅ dx divergerar för alla α!

> 💡 Det här visar varför det är viktigt att kontrollera **alla** problempunkter — det räcker att en del divergerar för att hela integralen ska divergera.

---

## Gammafunktionen — ett smakprov

**Exempel 21.** Integralen

```
Γ(s) = ∫₀^∞ x^(s-1) · e⁻ˣ dx
```

definierar för s > 0 den så kallade **gammafunktionen**. Den uppfyller:

```
Γ(n+1) = n!    (för naturliga tal n)
```

och generaliserar alltså fakultetsfunktionen till alla positiva reella tal! Konvergensen visas genom uppdelning i [0,1] och [1,∞) med jämförelse.

---

# 🔷 KAPITEL 7.9 — Integraler och summor

## Grundidén: uppskatta summor med integraler

Vid definitionen av Riemannintegralen gick vi från summor (Riemannsummor) till integraler. Nu vänder vi på det: vi använder **kända integraler** för att **uppskatta svårberäknade summor**.

> 💡 **Varför?** Vi har insättningsformeln för att beräkna integraler (hitta primitiv, sätt in gränser). Men det finns ingen motsvarande generell formel för summor. Integraler kan alltså vara lättare att beräkna!

---

## Uppskattning av integraler med summor

### Härledning med rektanglar

Betrakta en kontinuerlig, positiv och **avtagande** funktion f för x ≥ 1, och låt n vara ett positivt heltal.

Integralen ∫₁ⁿ f(x) dx representerar arean under kurvan. Vi kan uppskatta denna area med rektanglar av bredd 1:

**Överskattning (vänsterpunkter):** Rektanglarna med höjder f(1), f(2), ..., f(n-1) ligger *ovanför* kurvan (f är avtagande), alltså:

```
∫₁ⁿ f(x) dx ≤ f(1) + f(2) + ... + f(n-1) = Σₖ₌₁ⁿ⁻¹ f(k)
```

**Underskattning (högerpunkter):** Rektanglarna med höjder f(2), f(3), ..., f(n) ligger *under* kurvan:

```
f(2) + f(3) + ... + f(n) = Σₖ₌₂ⁿ f(k) ≤ ∫₁ⁿ f(x) dx
```

### Den centrala olikheten (formel 14)

Genom att kombinera dessa uppskattningar:

```
(14)    ∫₁ⁿ f(x) dx + f(n)  ≤  Σₖ₌₁ⁿ f(k)  ≤  ∫₁ⁿ f(x) dx + f(1)
```

> 🎯 **Det här är verktyget!** Summan kläms in mellan integralen plus det sista respektive första funktionsvärdet. Eftersom integraler ofta kan beräknas exakt ger detta kraftfulla uppskattningar av summor.

Liknande olikheter gäller även för **växande** funktioner (med omvända roller).

---

## Exempel 20: Harmoniska serien och ln n

Betrakta den **harmoniska summan**:

```
sₙ = Σₖ₌₁ⁿ 1/k = 1 + 1/2 + 1/3 + ... + 1/n
```

Med f(x) = 1/x (avtagande, positiv) och ∫₁ⁿ 1/x dx = ln n ger olikheten (14):

```
ln n + 1/n  ≤  sₙ  ≤  ln n + 1
```

> 💡 **Vad säger detta?** Den harmoniska summan sₙ = 1 + 1/2 + ... + 1/n **växer som ln n**. Mer precist: skillnaden sₙ - ln n är alltid mellan 1/n och 1.

---

## Eulers konstant

Uppskattningen visar att talen

```
cₙ = 1 + 1/2 + ... + 1/n - ln n
```

uppfyller cₙ ≥ 1/n > 0 för alla n. Man kan dessutom visa att cₙ **avtar** (beviset i boken använder att cₙ - cₙ₊₁ = ∫ₙⁿ⁺¹ 1/x dx - 1/(n+1) ≥ 0).

Alltså: cₙ är positiv och avtagande, och har ett gränsvärde:

```
C = lim (1 + 1/2 + ... + 1/n - ln n) ≈ 0.57722
    n→∞
```

Talet C kallas **Eulers konstant** (ofta betecknad γ). Det är ett av matematikens mest kända tal — och man vet fortfarande inte om det är rationellt eller irrationellt!

> 🎯 **Praktisk tolkning:** För stora n gäller 1 + 1/2 + ... + 1/n ≈ ln n + γ. Det ger en snabb uppskattning av harmoniska summor.

---

## Positiva serier och Cauchys integralkriterium

### Bakgrund: serier

En serie Σₖ₌₀^∞ aₖ = a₀ + a₁ + a₂ + ... kallas **konvergent** om delsummorna

```
sₙ = Σₖ₌₀ⁿ aₖ
```

har ett gränsvärde när n → ∞. Annars kallas serien **divergent**.

Ett stort problem i praktiken: det är ofta svårt att avgöra om en serie konvergerar genom att beräkna delsummorna explicit. Cauchys integralkriterium ger en elegant lösning.

### Cauchys integralkriterium

**SATS 1. (CAUCHYS INTEGRALKRITERIUM)** *Antag att f(x) är positiv och avtagande för x ≥ 1. Då är serien*

```
Σₖ₌₁^∞ f(k)
```

*konvergent om och endast om den generaliserade integralen*

```
∫₁^∞ f(x) dx
```

*är konvergent.*

### Bevisidé

Nyckeln är olikheten (14). Eftersom f(x) ≥ 0 är delsumman sₙ = Σ f(k) en **växande** talföljd. Gränsvärdet existerar om och endast om sₙ är **uppåt begränsad** (sats 2.16 i boken). Men (14) visar:

```
sₙ ≤ ∫₁ⁿ f(x) dx + f(1)
```

så sₙ är uppåt begränsad precis när ∫₁ˣ f(x) dx är det, dvs precis när ∫₁^∞ f(x) dx konvergerar. ∎

> 💡 **Varför är detta så kraftfullt?** Det översätter konvergensfrågor om serier till konvergensfrågor om integraler — och integraler kan vi ofta beräkna med insättningsformeln!

### Exempel 21: Σ k/(1+2k²) — divergent

Funktionen f(x) = x/(1+2x²) är positiv för x ≥ 1. Vi verifierar att den är avtagande (derivatan f'(x) = (1-2x²)/(1+2x²)² ≤ 0 för x ≥ 1). Beräkna integralen:

```
∫₁ˣ x/(1+2x²) dx = [1/4 · ln(1+2x²)]₁ˣ = 1/4 · ln(1+2X²) - 1/4 · ln 3  →  ∞
```

Integralen divergerar, alltså divergerar serien. ✓

### ⭐ Exempel 22: p-serien (MEMORERA!)

```
Σₖ₌₁^∞ 1/kᵅ  är  { divergent    om 0 < α ≤ 1
                     { konvergent   om α > 1
```

**Bevis:** Funktionen f(x) = 1/xᵅ är positiv och avtagande för x ≥ 1. Enligt Cauchys integralkriterium konvergerar serien om och **endast** om ∫₁^∞ 1/xᵅ dx konvergerar, vilket sker precis då α > 1 (exempel 12 i kap 6.5). ∎

Speciellt: **den harmoniska serien** Σ 1/k (α = 1) är **divergent**. Det följer också direkt från uppskattningen sₙ ≥ ln n + 1/n → ∞ i exempel 20.

> ⚠️ **Viktigt:** Cauchys integralkriterium säger bara om serien konvergerar eller divergerar. Det bestämmer **inte** seriens summa! Att beräkna exakta summor av serier kräver helt andra metoder.

---

# 🧠 Sammanfattning: Vad du bör kunna

### Kapitel 6.5 — Generaliserade integraler

- [ ] **Två typer:** Oändligt intervall (def 4) och obegränsad integrand (def 5)
- [ ] **Metod:** Beräkna vanlig integral med parameter (X eller ε), undersök gränsvärdet
- [ ] **Standardresultat 1:** ∫₁^∞ 1/xᵅ dx konvergerar ⟺ α > 1
- [ ] **Standardresultat 2:** ∫₀¹ 1/xᵅ dx konvergerar ⟺ α < 1
- [ ] **Konsekvens:** ∫₀^∞ 1/xᵅ dx divergerar för *alla* α
- [ ] **Jämförelsesatsen** (sats 11): 0 ≤ f ≤ g ger att konvergens av g ⟹ konvergens av f
- [ ] Kunna använda **standardfunktionerna** 1/xᵅ och e⁻ˣ som jämförelseobjekt
- [ ] Integraler generaliserade på **flera sätt** — dela upp och undersök varje del

### Kapitel 7.9 — Integraler och summor

- [ ] **Olikheten (14):** ∫₁ⁿ f dx + f(n) ≤ Σf(k) ≤ ∫₁ⁿ f dx + f(1) (avtagande f)
- [ ] **Uppskattning av harmoniska serien:** ln n + 1/n ≤ sₙ ≤ ln n + 1
- [ ] **Eulers konstant** γ ≈ 0.577: gränsvärdet av (1 + 1/2 + ... + 1/n - ln n)
- [ ] **Cauchys integralkriterium** (sats 1): Σ f(k) konvergerar ⟺ ∫₁^∞ f(x) dx konvergerar
- [ ] **p-serien:** Σ 1/kᵅ konvergerar ⟺ α > 1

---

## 📌 Formler att memorera

| Formel | Referens |
|--------|----------|
| ∫₁^∞ 1/xᵅ dx konvergerar ⟺ α > 1 | Exempel 12 |
| ∫₀¹ 1/xᵅ dx konvergerar ⟺ α < 1 | Exempel 15 |
| 0 ≤ f ≤ g, ∫g konv. ⟹ ∫f konv. | Sats 11 (jämförelse) |
| ∫₁ⁿ f dx + f(n) ≤ Σf(k) ≤ ∫₁ⁿ f dx + f(1) | Formel (14) |
| sₙ = 1+1/2+...+1/n ≈ ln n + γ | Euler |
| Σ f(k) konv. ⟺ ∫₁^∞ f(x) dx konv. | Sats 1 (Cauchy) |
| Σ 1/kᵅ konvergerar ⟺ α > 1 | p-serien (ex 22) |
| Γ(s) = ∫₀^∞ x^(s-1)e⁻ˣ dx, Γ(n+1) = n! | Gammafunktionen |

---

## 💡 Den röda tråden: hur allt hänger ihop

Dessa kapitel visar en elegant cirkel av idéer:

```
Kapitel 6.1-6.4:  Summor → definierar → Integraler
                  (Riemannsummor → Riemannintegralen → insättningsformeln)

Kapitel 6.5:      Integraler → utvidgas → Generaliserade integraler
                  (gränsvärden av vanliga integraler)

Kapitel 7.9:      Integraler → uppskattar → Summor
                  (den omvända riktningen!)
                  Integraler → avgör konvergens av → Serier
                  (Cauchys integralkriterium)
```

Samspelet mellan summor och integraler är ett centralt tema i hela analysen. Summor kan användas för att definiera integraler (Riemann), och integraler kan användas för att uppskatta och analysera summor (Cauchy). De två konvergensresultaten — ∫₁^∞ 1/xᵅ dx och Σ 1/kᵅ — har *exakt samma gräns* (α > 1), vilket inte är en slump utan en direkt konsekvens av integralkriteriet.
