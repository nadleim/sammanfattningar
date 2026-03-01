# 📐 Kapitel 7.1, 7.3 & 7.4 — Areabestämningar, Volymberäkningar & Kurvlängd

## Omfattande sammanfattning och genomgång

*Baserad på kursboken (sidorna 321–339)*
*Läsanvisningar för föreläsning 20 (area & volym) och föreläsning 21 (kurvor & kurvlängd)*

---

# 🔷 KAPITEL 7.1 — Areabestämningar

## Grundprincipen

Vi vet redan från kapitel 6 att om f(x) ≥ 0, så ger ∫ₐᵇ f(x) dx arean av området mellan grafen av f och x-axeln. Nu utvidgar vi detta till mer allmänna situationer.

---

## Area mellan kurva och x-axeln (f ≥ 0)

Det enklaste fallet: om f(x) ≥ 0 i [a,b], så är

```
A = ∫ₐᵇ f(x) dx
```

arean av området bestående av alla punkter (x,y) med 0 ≤ y ≤ f(x), a ≤ x ≤ b.

---

## Area mellan två kurvor

Det mer generella fallet: om g(x) ≤ f(x) i [a,b], så har det plana området

```
{ (x,y) : g(x) ≤ y ≤ f(x),   a ≤ x ≤ b }
```

arean:

```
A = ∫ₐᵇ (f(x) - g(x)) dx
```

> 💡 **Intuitivt:** "Övre kurva minus undre kurva." Man integrerar *avståndet* mellan de två kurvorna. Specialfallet g(x) = 0 ger det vanliga fallet med area under en kurva.

> ⚠️ **Viktigt:** Om kurvorna korsar varandra inom [a,b] måste man **dela upp** integralen vid korsningspunkterna och byta vilken som är "övre" respektive "undre" i varje delintervall.

---

## Exempel 1: Arean av en ellips

En ellips ges av x²/a² + y²/b² = 1. Den övre halvan är y = b√(1 - x²/a²).

Genom symmetri (spegla kring x- och y-axeln) är totala arean fyra gånger arean i första kvadranten:

```
A = 4 ∫₀ᵃ b√(1 - x²/a²) dx
```

Med substitutionen x = a sin t, dx = a cos t dt:

```
A = 4ab ∫₀^(π/2) cos² t dt = 4ab · [t/2 + sin(2t)/4]₀^(π/2) = πab
```

> 🎯 **Specialfallet b = a** ger A = πa² — den välkända cirkelareformeln!

---

## Exempel 2: Area begränsad av flera kurvor

Beräkna arean av det ändliga området begränsat uppåt av y = x och y = 2-x, och nedåt av parabeln y² = 2-x.

**Steg 1: Finn skärningspunkter.**

```
y = x och y² = 2-x:  x² = 2-x  ⟹  x = 1 (x = -2 ger punkt (-2,-2))
y = 2-x och y² = 2-x:  (2-x)² = 2-x  ⟹  x = 2 (y=0) eller x = 1 (y=1)
y = x och y = 2-x:  skärning i (1,1)
```

**Steg 2: Dela upp i delområden.** Området delas i D₁ (från x = 1 till x = 2) och D₂ (från x = -2 till x = 1), med olika övre/undre begränsningskurvor.

```
A₁ = ∫₁² ((2-x) - (-√(2-x))) dx = ∫₁² (2 - x + √(2-x)) dx = 7/6

A₂ = ∫₋₂¹ (x - (-√(2-x))) dx = ∫₋₂¹ (x + √(2-x)) dx = 19/6
```

**Total area:** A = 7/6 + 19/6 = **13/3** areaenheter.

> 💡 **Lärdom:** Vid komplicerade områden krävs det alltid att man (1) skissar området, (2) identifierar skärningspunkter, och (3) delar upp i delområden med tydliga övre/undre begränsningsfunktioner.

---

## Exempel 3: Tillämpning — startkapital för ett företag

Ett nystartat företag har inkomst I(t) = 200(1 - e^(-t/100)) och utgift U(t) = 150(1 + 2e^(-t/100)) per dag. Så länge t < a (tidpunkten när inkomst = utgift) går företaget med förlust.

Den totala förlusten som startkapitalet måste täcka:

```
K = ∫₀ᵃ (U(t) - I(t)) dt
```

Geometriskt: K är **arean** mellan de två kurvorna U(t) och I(t) från t = 0 till t = a.

Tidpunkten a fås genom I(a) = U(a), vilket ger a = 100 ln 10. Insättning:

```
K = ∫₀^(100 ln 10) (500e^(-t/100) - 50) dt = 5000(9 - ln 10) kkr
```

> 🎯 **Poängen:** Areaberäkning mellan kurvor har direkta praktiska tillämpningar — här representerar arean en faktisk ekonomisk förlust.

---

# 🔷 KAPITEL 7.3 — Volymberäkningar

## Skivformeln — den allmänna principen

### Grundidé

Vi vill beräkna volymen av en tredimensionell kropp K. Idén: "skiva" kroppen i tunna skivor vinkelrätt mot en axel, beräkna arean av varje skiva, och summera (integrera).

Låt A(x) vara **tvärsnittsarean** vid koordinaten x. En tunn skiva av tjocklek dx har approximativ volym A(x)·dx. Totala volymen fås genom integration:

```
        b
V  =   ∫  A(x) dx
        a
```

> 💡 **Varför fungerar detta?** Det är samma Riemannsumma-princip som vid areaberäkning, fast i tre dimensioner: vi approximerar kroppen med tunna "platta cylindrar" och tar gränsvärdet.

---

## Exempel 5: Volym av en pyramid

En pyramid med basyta B och höjd h. Lägg x-axeln längs höjden med origo i toppen.

Vid avstånd x från toppen har tvärsnittet arean:

```
A(x) = B · (x/h)²     (arean skalas med kvadraten av avståndet)
```

Volymen:

```
V = ∫₀ʰ B · x²/h² dx = B/h² · [x³/3]₀ʰ = Bh/3
```

> 🎯 **V = Bh/3** — den välkända pyramidformeln, som gäller för **godtycklig** basform!

---

## Rotationsvolymer

### Rotation kring x-axeln (skivmetoden)

Om vi roterar grafen y = f(x) (a ≤ x ≤ b) kring x-axeln uppstår en rotationskropp. Ett tvärsnitt vid x är en **cirkelskiva** med radie f(x), alltså area π·f(x)².

```
        b
(2)    V = ∫  π f(x)² dx
        a
```

> 💡 **Enkel regel:** "Pi gånger radien i kvadrat, integrerat."

### Exempel 6: Klotets volym

Rotera halvcirkeln y = √(R² - x²) kring x-axeln:

```
V = ∫₋ᴿᴿ π(R² - x²) dx = π[R²x - x³/3]₋ᴿᴿ = 4πR³/3
```

Den välkända formeln V = 4πR³/3. ✓

---

### Rotation kring y-axeln (skalmetoden / rörformiga element)

Ibland är det smidigare att rotera kring **y-axeln**. Då använder man **rörformiga (cylindriska) volymelement** istället för skivor.

Ett tunt "rör" vid radien x har:
- Radie: x
- Höjd: y = f(x)  (eller avståndet mellan kurvorna)
- Tjocklek: dx
- Basarea: 2πx · dx (mantelarean av en tunn cylinder)
- Volym: 2πx · f(x) · dx

```
V = ∫ₐᵇ 2πx · f(x) dx
```

> 💡 **Tumregel:** Rotation kring x-axeln → skivor (π·f²). Rotation kring y-axeln → rör (2πx·f).

### Exempel 7: Rotation kring y-axeln

Rotera området mellan y = 1 - (x-2)² och x-axeln (1 ≤ x ≤ 3) kring y-axeln.

Volymelementet: 2πx · y · dx = 2πx(1 - (x-2)²) dx = 2π(-x³ + 4x² - 3x) dx.

```
V = 2π ∫₁³ (-x³ + 4x² - 3x) dx = 2π[-x⁴/4 + 4x³/3 - 3x²/2]₁³ = 16π/3
```

---

# 🔷 KAPITEL 7.4 — Längd av kurvor

## Kurvor på parameterform

### Definition

Den intuitiva uppfattningen av en "kurva" är en figur man kan rita utan att lyfta pennan. Matematiskt beskrivs detta med en **vektorfunktion** (parametrisering):

```
r(t) = (x(t), y(t)),     α ≤ t ≤ β
```

där t är **parametern** och [α, β] är **parameterintervallet**.

> 💡 **Tänk på det som en promenad:** parametern t representerar tiden, och r(t) anger var du befinner dig vid tid t. Hela kurvan är den väg du går.

### Tangentvektor (derivatan)

Derivatan av r(t) ger kurvans **tangentriktning** i varje punkt:

```
r'(t) = (x'(t), y'(t))
```

Denna vektor pekar i den riktning kurvan "rör sig" vid tid t.

---

### Exempel 8: Ellipsen

Parameterframställningen:

```
x = a cos t,   y = b sin t,     0 ≤ t ≤ 2π
```

beskriver en ellips (verifiera: x²/a² + y²/b² = cos²t + sin²t = 1). Specialfallet b = a ger en cirkel.

Tangentvektor: **r'**(t) = (-a sin t, b cos t).

### Parameterbyten

En och samma kurva kan beskrivas med **olika parametriseringar**. Till exempel beskriver:

```
x = a cos 2πu,   y = b sin 2πu,     0 ≤ u ≤ 1
```

exakt samma ellips, men parametern u löper från 0 till 1 istället för 0 till 2π.

Ett allmänt parameterbyte har formen t = φ(u), där φ är **strängt växande** med kontinuerlig derivata (φ'(u) ≥ 0).

---

## Kurvlängd

### Härledning

Givet kurvan γ: **r**(t) = (x(t), y(t)), α ≤ t ≤ β.

Vi approximerar längden genom att dela upp kurvan i korta bitar. Under ett litet tidsintervall dt förflyttas vi ungefär:

```
r(t + dt) - r(t) ≈ r'(t) · dt
```

Längden av denna förflyttning:

```
|r'(t)| dt = √(x'(t)² + y'(t)²) · dt
```

Genom att summera (integrera) dessa infinitesimala bitar:

### Kurvlängdsformeln

```
(5)     L = ∫_α^β |r'(t)| dt = ∫_α^β √(x'(t)² + y'(t)²) dt
```

> 🎯 **Det här är huvudformeln!** Man beräknar hastigheten |**r'**(t)| i varje punkt och integrerar den.

### Bågelementet ds

Man inför den (parameter-)invarianta **differentialen**:

```
(6)     ds = √(dx² + dy²) = √(x'(t)² + y'(t)²) dt
```

som kallas **bågelementet**. Kurvlängden skrivs kompakt:

```
L = ∫_γ ds
```

> 💡 **Invariant under parameterbyte:** Om man gör substitutionen t = φ(u) i formeln, visar boken att resultatet M = ∫ₐᵇ |**r'**(φ(u))| · φ'(u) du = L. Kurvlängden beror alltså bara på kurvans geometri, inte på vilken parametrisering man använder.

---

## Specialfall: Kurvan y = f(x)

En funktionskurva y = f(x), a ≤ x ≤ b, kan parametriseras med x som parameter:

```
r(x) = (x, f(x))    ⟹    r'(x) = (1, f'(x))
```

Kurvlängden blir:

```
L = ∫ₐᵇ √(1 + f'(x)²) dx
```

> 🎯 **Det här är den formel du oftast använder i praktiken** — den gäller för alla "vanliga" funktionskurvor.

---

## Exempel 9: Cykloiden

En **cykloid** är kurvan som en punkt på kanten av ett rullande hjul ritar ut:

```
x = R(θ - sin θ),     y = R(1 - cos θ),     0 ≤ θ ≤ 2π
```

**Derivator:**

```
x'(θ) = R(1 - cos θ),     y'(θ) = R sin θ
```

**Bågelelement:**

```
ds = √(x'² + y'²) dθ = R√((1-cos θ)² + sin²θ) dθ
   = R√(1 - 2cos θ + cos²θ + sin²θ) dθ
   = R√(2 - 2cos θ) dθ
   = R√(2) · √(1 - cos θ) dθ
```

Använd identiteten 1 - cos θ = 2sin²(θ/2):

```
ds = R√2 · √(2sin²(θ/2)) dθ = 2R |sin(θ/2)| dθ = 2R sin(θ/2) dθ
```

(Eftersom 0 ≤ θ ≤ 2π ger 0 ≤ θ/2 ≤ π, alltså sin(θ/2) ≥ 0.)

**Kurvlängden:**

```
L = ∫₀^(2π) 2R sin(θ/2) dθ = 2R[-2cos(θ/2)]₀^(2π) = 2R · (2 + 2) = 8R
```

> 🎯 **Resultat:** Cykloidbågens längd för ett helt varv = **8R** = 8 gånger hjulets radie. Anmärkningsvärt enkelt svar!

---

## Kurvor på polär form

### Polära koordinater — snabb påminnelse

Istället för (x, y) beskriver man en punkt med **(r, θ)** där:

- r = avstånd från origo
- θ = vinkel mot positiva x-axeln

Sambandet: x = r cos θ,  y = r sin θ.

### Kurvor i polär form

En kurva ges av r = r(θ), α ≤ θ ≤ β. Det vill säga: avståndet från origo varierar med vinkeln.

**Exempel:** Arkimedes spiral: r = θ, θ ≥ 0. (Avståndet från origo växer proportionellt mot vinkeln.)

### Bågelelement i polär form

Man konverterar till parametrisk form: x = r(θ)cos θ, y = r(θ)sin θ, beräknar x' och y', och efter förenkling:

```
ds = √(r(θ)² + r'(θ)²) dθ
```

> 💡 **Geometrisk tolkning:** Man kan förstå formeln genom att betrakta en liten vinkeländring dθ. Förflyttningen har två komponenter: en **radiell** komponent dr och en **tangentiell** komponent r·dθ. Pythagoras ger ds = √((r dθ)² + (dr)²).

### Exempel 11: Arkimedes spiral

Längden av r = θ mellan θ = 0 och θ = 2:

```
L = ∫₀² √(θ² + 1) dθ = [θ/2 · √(θ²+1) + 1/2 · ln(θ + √(θ²+1))]₀²
  = √5 + 1/2 · ln(2 + √5)
```

---

## Rymdkurvor (3D)

Formeln generaliseras direkt till tre dimensioner:

```
r(t) = (x(t), y(t), z(t)),     α ≤ t ≤ β
```

```
L = ∫_α^β √(x'(t)² + y'(t)² + z'(t)²) dt
```

### Exempel 12: Skruvlinje (helix)

Kurvan **r**(t) = (a cos t, a sin t, bt) beskriver en spiralformad kurva kring z-axeln med radie a och stigning 2πb per varv. Längden av ett varv (0 ≤ t ≤ 2π):

```
|r'(t)| = √(a²sin²t + a²cos²t + b²) = √(a² + b²)     (konstant!)

L = ∫₀^(2π) √(a² + b²) dt = 2π√(a² + b²)
```

> 💡 **Notera:** Skruvlinjen har konstant "hastighet" — varje liten del av kurvan är lika lång. Det beror på att både rotations- och stigningskomponenten är konstanta.

---

# 🧠 Sammanfattning: Vad du bör kunna

### Kapitel 7.1 — Areabestämningar (Föreläsning 20)

- [ ] **Area mellan två kurvor:** A = ∫ₐᵇ (f(x) - g(x)) dx där f ≥ g
- [ ] **Skärningspunkter:** Alltid hitta dessa först — de bestämmer integrationsgränserna
- [ ] **Uppdelning:** Om kurvorna korsar varandra → dela upp integralen
- [ ] Kunna lösa **tillämpade** areaproblem (t.ex. ekonomiska modeller)
- [ ] **Ellipsens area** = πab (specialfall av arean under en kurva + substitution)

### Kapitel 7.3 — Volymberäkningar (Föreläsning 20)

- [ ] **Skivformeln:** V = ∫ₐᵇ A(x) dx (generell — gäller för *alla* kroppar med känd tvärsnittsarea)
- [ ] **Rotationsvolym kring x-axeln:** V = ∫ₐᵇ π f(x)² dx (skivmetoden)
- [ ] **Rotationsvolym kring y-axeln:** V = ∫ₐᵇ 2πx f(x) dx (skalmetoden/rörformiga element)
- [ ] **Pyramidformeln:** V = Bh/3 (härled med skivformeln!)
- [ ] **Klotvolymen:** V = 4πR³/3 (härled med rotation av halvcirkel!)
- [ ] Kunna **välja rätt metod** (skivor vs rör) beroende på rotationsaxel

### Kapitel 7.4 — Kurvlängd (Föreläsning 21)

- [ ] **Kurva på parameterform:** r(t) = (x(t), y(t)), tangentvektor r'(t) = (x'(t), y'(t))
- [ ] **Kurvlängdsformeln:** L = ∫_α^β √(x'² + y'²) dt
- [ ] **Specialfall y = f(x):** L = ∫ₐᵇ √(1 + f'(x)²) dx
- [ ] **Bågelementet:** ds = √(dx² + dy²) — invariant under parameterbyte
- [ ] **Polär form:** ds = √(r² + r'²) dθ
- [ ] **Rymdkurvor (3D):** L = ∫ √(x'² + y'² + z'²) dt
- [ ] Kunna beräkna kurvlängd för cykloid, cirkel, ellips, spiral, skruvlinje

---

## 📌 Formler att memorera

| Formel | Beskrivning |
|--------|-------------|
| A = ∫ₐᵇ (f(x) - g(x)) dx | Area mellan två kurvor |
| A(ellips) = πab | Ellipsens area |
| V = ∫ₐᵇ A(x) dx | Skivformeln (generell volym) |
| V = ∫ₐᵇ π f(x)² dx | Rotationsvolym kring x-axeln |
| V = ∫ₐᵇ 2πx f(x) dx | Rotationsvolym kring y-axeln |
| V(pyramid) = Bh/3 | Pyramidvolymen |
| V(klot) = 4πR³/3 | Klotets volym |
| L = ∫_α^β √(x'² + y'²) dt | Kurvlängd (parameterform) |
| L = ∫ₐᵇ √(1 + f'(x)²) dx | Kurvlängd (funktionskurva) |
| ds = √(r² + r'²) dθ | Bågelelement (polär form) |
| L(cykloid, 1 varv) = 8R | Cykloidens båglängd |
| L(skruvlinje, 1 varv) = 2π√(a²+b²) | Skruvlinjens båglängd |

---

## 💡 Den röda tråden

Alla tre kapitlen bygger på **samma grundprincip** — "ström­linjeformade resonemang":

1. **Dela upp** storheten (area, volym, längd) i oändligt många infinitesimala bitar
2. **Uttryck** varje bit med hjälp av kända formler (rektangelarea, cirkelarea, Pythagoras)
3. **Summera** genom integration

```
Area:    dA = (f(x) - g(x)) dx        →  A = ∫ dA
Volym:   dV = A(x) dx  eller  π f² dx →  V = ∫ dV
Längd:   ds = √(dx² + dy²)            →  L = ∫ ds
```

Det som skiljer tillämpningarna åt är bara *vilken geometrisk formel* man använder för varje infinitesimal bit. Integrationstekniken (insättningsformeln, substitution, partiell integration) från kapitel 5 och 6 är densamma.
