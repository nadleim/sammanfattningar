# 📐 Kapitel 4.1 & 4.2 — Kurvritning och Lokala extremvärden

## Omfattande sammanfattning och genomgång

*Baserad på kursboken (sidorna 225–232)*
*Kapitel för självstudier, med tillhörande övningar 4.1–4.6*

---

# 🔷 KAPITEL 4.1 — Kurvritning

## Vad handlar detta om?

Att **rita grafen** till en funktion y = f(x) för hand, med hjälp av derivatan. Man söker inte en perfekt bild utan en **kvalitativ skiss** som fångar kurvans "personlighet": var den växer och avtar, var den har toppar och dalar, och hur den beter sig i utkanten av sin definitionsmängd.

> 💡 **Varför inte bara använda en dator?** En miniräknare/dator ritar alltid kurvan i ett begränsat fönster och kan missa viktiga beteenden utanför fönstret. Den klassiska metoden ger dig en **fullständig** förståelse av funktionens beteende.

---

## Metoden — fem steg

Boken presenterar en systematisk metod i fem steg. Vi går igenom varje steg i detalj.

---

### Steg 1: Beräkna derivatan

Bestäm f'(x). Skriv om derivatan så att den är **faktoriserad** så mycket som möjligt — det gör det lättare att hitta nollställen och bestämma tecken.

> 🎯 **Tips:** Om f(x) är en kvot, skriv f'(x) på ett gemensamt bråkstreck. Faktorisera sedan täljaren. Nollställena till f'(x) kommer från **täljaren**, medan **nämnaren** berättar var derivatan inte existerar.

**Relevanta tekniker du behöver:**
- Kvotregeln: D(g/h) = (g'h - gh') / h²
- Produktregeln: D(g·h) = g'h + gh'
- Kedjeregeln: D(f(g(x))) = f'(g(x))·g'(x)
- Logaritmisk derivering: om f = g^h, skriv f = e^(h·ln g) och derivera

---

### Steg 2: Undersök derivatans teckenväxling

Lös f'(x) = 0 för att hitta de **stationära punkterna** (alltså de x-värden där derivatan är noll).

Bestäm sedan **tecknet** av f'(x) i varje intervall mellan de stationära punkterna. Flera tekniker:

- **Faktorisering:** Om f'(x) = (x-a)(x-b)/x², bestäm tecknet av varje faktor i varje intervall
- **Testpunkter:** Sätt in enkla x-värden i f'(x) i varje intervall
- **Allmänna resonemang:** T.ex. e^x > 0 alltid, x² ≥ 0 alltid

> 💡 **Observera:** Derivatan kan också byta tecken vid punkter där den **inte existerar** — t.ex. vid nämnarens nollställen. Dessa punkter ska också vara med i teckenschemat!

---

### Steg 3: Upprätta teckenschema och värdetabell

Det här är det centrala verktyget. Man gör en tabell med tre rader:

```
    x   │  ...  │  x₁  │  ...  │  x₂  │  ...  │
  ──────┼───────┼──────┼───────┼──────┼───────┤
  f'(x) │   +   │   0  │   -   │   0  │   +   │
  ──────┼───────┼──────┼───────┼──────┼───────┤
  f(x)  │   ↗   │  f(x₁) │  ↘  │ f(x₂) │  ↗  │
```

**Rad 1 (x):** Alla "intressanta" x-värden: ändpunkter av definitionsmängden, derivatans nollställen, punkter där f eller f' inte är definierade.

**Rad 2 (f'(x)):** Tecknet (+, 0, eller -) i varje intervall.

**Rad 3 (f(x)):** Pilar (↗ för växande, ↘ för avtagande) samt beräknade funktionsvärden vid de intressanta punkterna.

> 🎯 **Från teckenschemat avläser man direkt:**
> - **Lokalt maximum:** f' byter tecken + → 0 → - (kurvan slutar stiga, börjar sjunka)
> - **Lokalt minimum:** f' byter tecken - → 0 → + (kurvan slutar sjunka, börjar stiga)
> - **Terrasspunkt:** f' = 0 men byter **inte** tecken (kurvan planar ut men fortsätter åt samma håll)

---

### Steg 4: Komplettera med gränsvärdesberäkningar

Vid varje **ändpunkt av definitionsmängden** som inte är en vanlig punkt (t.ex. om f inte är definierad där, eller vid ±∞) beräknar man det ensidiga gränsvärdet.

Typiska situationer:

- **x → ±∞:** Vad händer med f(x) för stora |x|? Går f mot ett ändligt värde (horisontell asymptot), mot ±∞, eller finns en **sned asymptot**?
- **x → c** (där c är en "problempunkt"):** T.ex. om nämnaren har ett nollställe i c, undersök om f(x) → ±∞ (vertikal asymptot).

#### Asymptoter — tre typer

**Vertikal asymptot:** x = c är en vertikal asymptot om f(x) → ±∞ när x → c (från ena eller båda sidor). Typiskt: nollställen i nämnaren som inte förenklas bort.

**Horisontell asymptot:** y = L är en horisontell asymptot om f(x) → L när x → ±∞.

**Sned (snedstreckad) asymptot:** y = kx + m är en sned asymptot om f(x) - (kx + m) → 0 när x → ±∞.

> 🎯 **Hur hittar man sneda asymptoter med polynomdivision?** Om f(x) = p(x)/q(x) är en rationell funktion där täljaren har högre grad än nämnaren, utför polynomdivision:
>
> f(x) = (kx + m) + r(x)/q(x)
>
> Kvoten kx + m ger den sneda asymptoten och resttermen r(x)/q(x) → 0 då x → ±∞.
>
> **Exempel:** f(x) = x²/(x+1). Polynomdivision ger f(x) = x - 1 + 1/(x+1). Alltså är y = x - 1 en sned asymptot.

---

### Steg 5: Gör en skiss av funktionskurvan

Sätt ihop allt: rita koordinataxlarna, markera de beräknade punkterna (lokala max/min, skärningspunkter med axlarna), rita in asymptoter som streckade linjer, och rita kurvan så att den stämmer med teckenschemats information om växande/avtagande-beteende.

> 💡 **Extra information som kan förbättra skissen:**
> - Skärning med x-axeln: lös f(x) = 0 (om möjligt)
> - Skärning med y-axeln: beräkna f(0) (om 0 ∈ Df)
> - Symmetri: f(-x) = f(x) ger spegling i y-axeln (jämn funktion), f(-x) = -f(x) ger punktsymmetri kring origo (udda funktion)

---

## Bokens genomgångna exempel

Boken behandlar funktionen f(x) = x + 2/x + 2·arctan x, x ≥ -√3, x ≠ 0 och går igenom alla fem stegen i detalj. Det genomarbetade exemplet visar hur faktorisering av derivatan leder till ett teckenschema, och hur gränsvärden vid ändpunkterna (x → 0⁻, x → 0⁺, x → +∞) kompletterar bilden.

---

# 🔷 KAPITEL 4.2 — Lokala extremvärden

## Stationära punkter och extrempunkter — begreppsöversikt

En punkt x₀ kallas **stationär** om f'(x₀) = 0. Men inte alla stationära punkter är extrempunkter! Det finns tre möjligheter:

1. **Lokalt maximum:** Funktionen är störst i x₀ jämfört med alla närliggande punkter
2. **Lokalt minimum:** Funktionen är minst i x₀ jämfört med alla närliggande punkter
3. **Terrasspunkt:** Funktionen har horisontell tangent men varken max eller min

> ⚠️ **Viktigt:** En deriverbar funktion kan ha lokala extrempunkter **bara** i stationära punkter (sats 3.13). Men en stationär punkt behöver *inte* vara en extrempunkt. Det krävs extra information för att avgöra vilken typ det rör sig om.

---

## Metod 1: Derivatans teckenväxling (förstaderivatatest)

Den mest grundläggande metoden. Från teckenschemat (steg 2–3 i kurvritningen) avläser man:

**SATS 1.** *Antag att f'(x₀) = 0. Om f' har teckenväxlingen:*

```
(i)   - 0 +   ⟹  strängt lokalt minimum i x₀
(ii)  + 0 -   ⟹  strängt lokalt maximum i x₀
(iii) + 0 +   ⟹  terrasspunkt i x₀ (inget extremvärde)
(iv)  - 0 -   ⟹  terrasspunkt i x₀ (inget extremvärde)
```

> 💡 **Geometrisk tolkning:**
> - (i): Kurvan sjunker, planar ut, börjar stiga = dal = minimum
> - (ii): Kurvan stiger, planar ut, börjar sjunka = topp = maximum
> - (iii) och (iv): Kurvan planar ut men fortsätter åt samma håll = S-form/platå

> ⚠️ **Observera:** Villkoren i (i)–(ii) är **tillräckliga** men inte **nödvändiga** för extremvärde. En deriverbar funktion *kan* ha ett extremvärde i x₀ utan att derivatan har ett bestämt tecken till vänster eller höger — t.ex. vid oscillerande funktioner. Men detta är sällsynt i vanliga övningar.

---

## Metod 2: Andraderivatatest

Ett alternativt (och ibland snabbare) sätt att klassificera stationära punkter.

**SATS 2.** *Antag att f'(x₀) = 0 och att f'' existerar och är kontinuerlig i en omgivning av x₀. Då gäller:*

```
(i)   f''(x₀) > 0  ⟹  strängt lokalt minimum i x₀
(ii)  f''(x₀) < 0  ⟹  strängt lokalt maximum i x₀
```

**BEVISIDÉ (för (i)):** Om f''(x₀) > 0 och f'' är kontinuerlig, så är f'' > 0 i en hel omgivning av x₀. Det betyder att f' är strängt växande nära x₀. Och eftersom f'(x₀) = 0, måste f' byta tecken från - till +. Alltså har vi lokalt minimum enligt sats 1. ∎

### Vad händer om f''(x₀) = 0?

Då säger sats 2 **ingenting** — alla tre fallen (max, min, terrasspunkt) är möjliga!

**Klassiskt motexempel:** f(x) = x⁴ har f'(0) = 0 och f''(0) = 0, men x = 0 är ändå ett lokalt minimum. Å andra sidan har f(x) = x³ också f'(0) = 0 och f''(0) = 0, men x = 0 är en terrasspunkt.

> 🎯 **När f''(x₀) = 0 måste du falla tillbaka på derivatans teckenväxling (metod 1).**

### Sats 2 vs Sats 1 — när använda vad?

Boken påpekar att **sats 2 är av mer teoretisk natur**. I praktiken har du redan derivatans nollställen och faktorisering från kurvritningen (steg 2), vilket direkt ger teckenväxlingen. Att dessutom beräkna andraderivatan kan vara onödigt arbete — speciellt om f'(x) är komplicerad.

> 💡 **Tumregel:** Använd andraderivatatest (sats 2) om f''(x₀) är **enkel att beräkna** och ger ett tydligt svar (≠ 0). Använd teckenväxlingstest (sats 1) om faktoriseringen av f'(x) redan är klar, eller om f''(x₀) = 0.

---

# 🧰 Praktisk guide: Så gör du en kurvdiskussion

Här är en komprimerad checklista du kan följa för övningarna:

### 1. Definitionsmängd
Var är f(x) definierad? Se upp med:
- Nämnare = 0 (rationella funktioner)
- Argument ≤ 0 i logaritmer
- Argument < 0 i rötter (jämna)

### 2. Symmetri (bonus — sparar arbete!)
- f(-x) = f(x)? → Jämn funktion (symmetri kring y-axeln)
- f(-x) = -f(x)? → Udda funktion (punktsymmetri kring origo)

### 3. Derivata och stationära punkter
- Beräkna f'(x)
- Faktorisera f'(x)
- Lös f'(x) = 0

### 4. Teckenschema
- Fyll i tabellen (x, f'(x), f(x))
- Bestäm max/min/terrasspunkter

### 5. Funktionsvärden
- Beräkna f i alla stationära punkter
- Beräkna f(0) om det är enkelt (skärning med y-axeln)

### 6. Asymptoter och gränsvärden
- **Vertikala:** Undersök f(x) nära nämnarens nollställen
- **Horisontella:** Beräkna lim f(x) då x → ±∞
- **Sneda:** Om täljaren har exakt en grad högre → polynomdivision!

### 7. Skissa!
- Rita asymptoter (streckade linjer)
- Markera extrempunkter
- Rita kurvan som respekterar all information

---

# 🔑 Snedstreckade asymptoter och polynomdivision

Eftersom detta lyfts fram som extra viktigt i övningarna (specifikt i 4.5), går vi igenom det mer i detalj.

## Vad är en sned asymptot?

Om f(x) för stora x beter sig som en linjär funktion — dvs f(x) ≈ kx + m — men inte exakt, så är linjen y = kx + m en **sned asymptot**. Formellt:

```
lim [f(x) - (kx + m)] = 0    när x → +∞ eller x → -∞
x→±∞
```

## Polynomdivision — steg för steg

Givet f(x) = p(x)/q(x) där grad(p) = grad(q) + 1, utför polynomdivision.

**Tillvägagångssätt:** Dela p(x) med q(x) precis som vid "lång division" med tal.

**Generellt mönster:**

```
p(x)/q(x) = (kx + m) + r(x)/q(x)
```

- **kx + m** = den sneda asymptoten
- **r(x)/q(x)** → 0 när x → ±∞ (resttermen)

> 💡 **Varför fungerar det?** Resttermen r(x) har lägre grad än q(x), så kvoten r(x)/q(x) har en nämnare som "vinner" i tillväxthastighet. Därmed → 0.

## Några viktiga specialfall

**Om grad(p) = grad(q):** Ingen sned asymptot men det finns en **horisontell** asymptot y = aₙ/bₙ (kvoten av ledande koefficienter).

**Om grad(p) < grad(q):** Horisontell asymptot y = 0.

**Om grad(p) > grad(q) + 1:** Ingen rak asymptot (kurvan växer snabbare än linjärt).

---

# 🧠 Sammanfattning: Vad du bör kunna

### Kapitel 4.1 — Kurvritning

- [ ] **Femstegsmetoden:** Derivata → tecken → schema → gränsvärden → skiss
- [ ] Beräkna och **faktorisera** derivatan
- [ ] Upprätta **teckenschema** med pilar och funktionsvärden
- [ ] Bestämma **vertikala, horisontella och sneda asymptoter**
- [ ] Använda **polynomdivision** för att hitta sneda asymptoter
- [ ] Beräkna relevanta **gränsvärden** (x → ±∞ och vid singulariteter)
- [ ] Rita en korrekt kvalitativ skiss utifrån all information

### Kapitel 4.2 — Lokala extremvärden

- [ ] **Stationär punkt:** f'(x₀) = 0
- [ ] **Sats 1 (teckenväxling):** -0+ ⟹ min, +0- ⟹ max, ±0± ⟹ terass
- [ ] **Sats 2 (andraderivatatest):** f''(x₀) > 0 ⟹ min, f''(x₀) < 0 ⟹ max
- [ ] Veta att f''(x₀) = 0 **inte ger information** — faller tillbaka på sats 1
- [ ] Kunna klassificera alla stationära punkter i en given funktion
- [ ] Veta att stationär punkt ≠ extrempunkt (terrasspunkter!)

---

## 📌 Formler att memorera

| Koncept | Formel/Villkor |
|---------|---------------|
| Stationär punkt | f'(x₀) = 0 |
| Lokalt min (teckenväxling) | f': - 0 + |
| Lokalt max (teckenväxling) | f': + 0 - |
| Terrasspunkt | f': + 0 + eller - 0 - |
| Lokalt min (andraderivata) | f'(x₀) = 0 och f''(x₀) > 0 |
| Lokalt max (andraderivata) | f'(x₀) = 0 och f''(x₀) < 0 |
| Vertikal asymptot | f(x) → ±∞ då x → c |
| Horisontell asymptot | f(x) → L då x → ±∞ |
| Sned asymptot | f(x) = kx + m + r(x)/q(x) via polynomdivision |

---

## 💡 Tips inför övningarna

Övningarna 4.1–4.6 testar alla delar av kurvdiskussionen. Här är några tips utan att avslöja lösningar:

**Uppgift 4.1 & 4.2** handlar om att hitta stationära punkter och extrempunkter. Nyckeln är att **faktorisera derivatan noggrant** — det är ofta det svåraste steget. Kom ihåg att derivatans nollställen sitter i **täljaren** (inte nämnaren) om f'(x) skrivs som ett bråk.

**Uppgift 4.4** kräver en fullständig kurvritning i stora drag. Följ femstegsmetoden systematiskt. Tips i övningsboken nämner att de tre första uppgifterna återanvänder beräkningarna från 4.1, så du får använda dina resultat därifrån.

**Uppgift 4.5** betonar **sneda asymptoter**. Här är polynomdivision centralt. Dela täljaren med nämnaren och identifiera kvoten som den sneda asymptoten. Kontrollera också vertikala asymptoter (nämnarens nollställen) och rita in dem i skissen.

**Uppgift 4.6** testar din förmåga att arbeta med **sammansatta funktioner** (arctan, ln). Kom ihåg att D(arctan x) = 1/(1+x²) och att ln x bara är definierad för x > 0. Teckenschemat kräver lite extra omsorg här.
