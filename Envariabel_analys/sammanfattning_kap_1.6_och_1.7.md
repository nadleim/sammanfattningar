# 📐 Kapitel 1.6 & 1.7 — Potens- och exponentialfunktioner & Logaritmfunktioner

## Omfattande sammanfattning och genomgång

---

# 🔷 KAPITEL 1.6 — Potens- och exponentialfunktioner

## 1.6.1 Potenser

### Vad är en potens?

Ett uttryck av formen

```
aᵅ
```

består av en **bas** (a) och en **exponent** (α). Med moderna miniräknare kan man enkelt beräkna numeriska närmevärden av potenser — men för att räknaren ska veta *exakt* vad den ska beräkna måste vi ha en ordentlig **definition** av aᵅ för allmänna baser och exponenter.

### Steg-för-steg definition av potenser

Definitionen byggs upp successivt, i flera steg:

**Steg 1 — Naturliga tal som exponent:**
```
a⁰ = 1

aⁿ = a · a · a · ... · a    (n stycken faktorer a)
```

**Steg 2 — Negativa heltalsexponenter:**
```
a⁻ⁿ = 1 / aⁿ       (kräver a ≠ 0)
```

**Steg 3 — Rationella exponenter (bråk):**

För heltal q > 0 definieras a^(1/q) som det entydigt bestämda positiva tal som löser ekvationen xᵠ = a (förutsatt a > 0). Speciellt:

```
a^(1/2) = √a
a^(1/q) = ᵠ√a       (q-te roten ur a)
```

Allmänt, med p/q i reducerad form:
```
a^(p/q) = (a^(1/q))^p
```

**Steg 4 — Reella exponenter:**

Slutligen definieras aᵅ för godtyckliga reella α (och a > 0) genom att **approximera α med rationella tal** p/q och låta aᵅ vara motsvarande "gränsvärde" av de redan definierade talen a^(p/q).

> 💡 I kursen förbigår vi den formella konstruktionen av detta sista steg. Det viktiga är att alla räknelagar förblir giltiga oavsett vilken typ av exponent vi har.

---

### Potenslagarna (SUPERVIKTIGA!)

Dessa gäller för alla baser a, b > 0 och alla reella exponenter α, β:

```
(21)    a⁰ = 1

(22)    a⁻ᵅ = 1/aᵅ

(23)    aᵅ · aᵝ = aᵅ⁺ᵝ

(24)    (aᵅ)ᵝ = aᵅᵝ

(25)    aᵅ · bᵅ = (ab)ᵅ
```

Dessutom gäller ordningsrelationerna:

```
(26)    a > 1 och α < β   ⟹   aᵅ < aᵝ      (exponentiering bevarar ordning om basen > 1)

(27)    0 < a < b och α > 0   ⟹   aᵅ < bᵅ    (potens bevarar ordning om exponenten > 0)
```

> 🎯 **Tolkning av (23):** Att multiplicera potenser med *samma bas* innebär att man **adderar exponenterna**. Till exempel: a³ · a⁵ = a⁸.

> 🎯 **Tolkning av (24):** Att upphöja en potens till ytterligare en potens innebär att man **multiplicerar exponenterna**. Till exempel: (a³)⁵ = a¹⁵.

---

### Exempel 26: Förenkla potensuttryck

**Uppgift:** Förenkla
```
(a¹²b⁻⁹c³) / (c²b⁶)  ·  (a⁻⁹c⁻¹) / b⁴
```

**Lösning:** Slå samman täljarna och nämnarna:

```
= (a¹²⁻⁹ · b⁻⁹⁻⁹⁻⁶⁻⁴ · c³⁻²⁻¹) = a³ · b⁻¹⁹ · c⁰ = a³/b¹⁹
```

> 💡 **Strategi:** Samla alla faktorer med samma bas, addera exponenterna (var noga med tecken!), och skriv om negativa exponenter som bråk om så önskas.

### Exempel 27: Förenkla rotuttryck

**Uppgift:** Förenkla √(⁴√x) · ⁸√(1/x²) · (x³)^(1/4)

**Lösning:** Skriv om alla rötter som bråkexponenter:
```
= (x^(1/4))^(1/2) · (x⁻²)^(1/8) · x^(3/4) = x^(1/8) · x^(-1/4) · x^(3/4) = x^(1/8 - 2/8 + 6/8) = x^(5/8)
```

> 💡 **Tips:** Skriv alltid om rötter till bråkexponenter — det gör det mycket enklare att använda potenslagarna.

### Exempel 28: Skriv som en enda potens

**Uppgift:** (aᵅ/aᵝ)ᵅ · (aᵅ/aᵝ)ᵝ

**Lösning:**
```
= (aᵅ⁻ᵝ)ᵅ · (aᵅ⁻ᵝ)ᵝ = a^((α−β)α) · a^((α−β)β) = a^((α−β)(α+β)) = a^(α²−β²)
```

---

## 1.6.2 Potensfunktioner

### Definition

Om vi i potensuttrycket xᵅ håller exponenten α **fix** och betraktar basen x som variabel får vi en **potensfunktion**:

```
f(x) = xᵅ,       x > 0
```

### Beteende för olika α

| Exponent α | Beteende | Exempel |
|------------|----------|---------|
| α > 1 | Strängt växande, konvex ("böjer uppåt") | x², x³ |
| 0 < α < 1 | Strängt växande, konkav ("böjer nedåt") | √x, ³√x |
| α = 0 | Konstant = 1 | 1 |
| α < 0 | Strängt avtagande, går mot 0 | 1/x, 1/x² |

**Viktiga egenskaper:**
- Om α > 0: xᵅ → +∞ då x → +∞ (egenskap 28)
- Om α < 0: xᵅ = 1/x^(−α) → 0 då x → +∞ (strängt avtagande)
- Alla potensfunktioner med α > 0 passerar genom punkten (1, 1)
- Definitionsmängden är x > 0 för allmän α

> 💡 Potensfunktioner med positiv exponent "drar iväg" mot oändligheten — men deras tillväxthastighet varierar kraftigt. Till exempel: x¹⁰ växer mycket snabbare än √x, trots att båda → +∞.

---

## 1.6.3 Exponentialfunktioner

### Definition

I en potensfunktion är exponenten fix och basen variabel. Om vi istället håller **basen a > 0 fix** och låter **exponenten variera** får vi:

```
f(x) = aˣ,       x ∈ ℝ
```

som kallas **exponentialfunktionen** med bas a. Ibland skrivs den ᵃexp x = aˣ.

### Fall 1: a > 1 (den vanligaste)

- Funktionen är **strängt växande**
- aˣ → +∞ då x → +∞   (formel 29)
- aˣ → 0 då x → −∞     (formel 31)
- Grafen passerar alltid genom (0, 1) (ty a⁰ = 1)
- **Värdemängd:** ]0, ∞[ (bara positiva värden)

> 🎯 Varför aˣ → +∞? Skriv a = 1 + p (p > 0). Med binomialsatsen:
> aˣ = (1+p)ˣ ≥ (1+p)ⁿ ≥ np (där n = ⌊x⌋). Eftersom np → +∞ när x → +∞, följer resultatet.

Mer precist kan man visa att aˣ ≥ (x−1)(x−2)p²/(2x) med binomialsatsen, vilket ger den starkare uppskattningen aˣ/x → +∞.

### Fall 2: 0 < a < 1

Kan återföras på fallet a > 1 genom omskrivningen:

```
aˣ = 1 / (1/a)ˣ
```

Eftersom 1/a > 1 ger detta en **strängt avtagande** funktion.

- aˣ → 0 då x → +∞
- aˣ → +∞ då x → −∞

### Den viktigaste exponentialfunktionen: eˣ

Den mest använda exponentialfunktionen har basen **e = 2.71828...**

Beteckning:
```
exp x = eˣ
```

> 💡 I avsnitt 2.3 ges den fullständiga definitionen av e. Det visar sig att e är den "naturligaste" basen ur ett matematiskt perspektiv — en egenskap som blir uppenbar när man studerar derivata.

---

## 1.6.4 Jämförelse mellan exponential- och potensfunktioner

### Sats 8 — Exponentialfunktionen växer snabbare än alla potensfunktioner

> **Sats 8.** Antag att a > 1. Då gäller att
>
> ```
> (32)    aˣ / xᵅ → +∞       då x → +∞
> ```
>
> eller ekvivalent:
>
> ```
> (32')   xᵅ / aˣ → 0         då x → +∞
> ```

> 🎯 **I klartext:** Oavsett hur stor exponenten α är, kommer exponentialfunktionen aˣ till slut att "köra om" potensfunktionen xᵅ och bli ojämförligt mycket större. Även x¹⁰⁰⁰ kommer till slut att vara försumbar jämfört med 2ˣ.
>
> Denna sats är ett av de allra viktigaste resultaten om tillväxthastigheter!

### Beviset (för α = 1)

Skriv a = 1 + p (p > 0), n = ⌊x⌋. Binomialutvecklingen ger:

```
aˣ ≥ (1+p)ⁿ ≥ C(n,2) · p² = n(n−1)/2 · p²
```

Alltså:
```
aˣ/x ≥ n(n−1)p² / (2x) ≥ (x−1)(x−2)p² / (2x) → +∞
```

Fallet med godtyckligt α > 0 följer av fallet α = 1 genom omskrivningen aˣ/xᵅ = (bˣ/x)ᵅ, där b = a^(1/α) > 1.

### Exempel 29: Tillämpning av sats 8

**Uppgift:** Undersök f(x) = (2ˣ + x²) / (3ˣ + x³⁰) för stora x.

**Lösning:** Dividera täljare och nämnare med nämnarens dominerande term 3ˣ:

```
f(x) = [(2/3)ˣ + x²/3ˣ] / [1 + x³⁰/3ˣ]
```

- (2/3)ˣ → 0 (ty 0 < 2/3 < 1)
- x²/3ˣ → 0 (sats 8, exponentiell slår potens)
- x³⁰/3ˣ → 0 (samma anledning)

Alltså: f(x) → (0 + 0) / (1 + 0) = **0** då x → +∞.

---

---

# 🔷 KAPITEL 1.7 — Logaritmfunktioner

## 1.7.1 Logaritmer

### Vad är en logaritm?

Låt a vara ett positivt tal skilt från 1. Av exponentialfunktionens egenskaper (den är strängt monoton) följer att ekvationen

```
aˣ = s
```

har **en entydig lösning** x för varje givet positivt tal s. Denna lösning kallas **a-logaritmen för s** och betecknas:

```
ᵃlog s
```

### Den grundläggande regeln

```
aˣ = s    ⟺    x = ᵃlog s
```

> 🎯 **I ord:** ᵃlog s är det tal som a ska upphöjas till för att resultatet ska bli s.

### Viktiga specialfall

```
(33)    a^(ᵃlog s) = s           (logaritmen "avbryter" exponentialfunktionen)

(34)    ᵃlog aᵗ = t              (exponent och logaritm "tar ut varandra")
```

> 💡 **Relationen (33) och (34) visar att logaritmen och exponentialfunktionen är varandras inverser.** Om du exponentierar och sedan tar logaritmen (eller tvärtom), kommer du tillbaka till där du startade.

### De viktigaste logaritmbaserna

| Beteckning | Bas | Namn | Typisk användning |
|------------|-----|------|-------------------|
| **ln s** = ᵉlog s | e ≈ 2.718 | Naturliga logaritmen | Matematik, analys |
| **lg s** = ¹⁰log s | 10 | Tiologaritmen | Naturvetenskap, teknik |
| ²log s | 2 | Tvålogaritmen | Datalogi |

> 💡 Man arbetar nästan uteslutande med logaritmer vars bas > 1.

### Exempel 30: Grundläggande beräkningar

```
²log 16 = ²log 2⁴ = 4              (ty 2⁴ = 16)

lg 1000 = lg 10³ = 3                (ty 10³ = 1000)

lg 0.01 = lg 10⁻² = −2              (ty 10⁻² = 0.01)

ln √e = ln e^(1/2) = 1/2            (ty e^(1/2) = √e)

3^(⁹log 17) = (9^(⁹log 17))^(1/2) = 17^(1/2) = √17
```

---

## Logaritmlagarna (Sats 9)

Dessa lagar följer direkt ur potenslagarna (21)–(25) och är grundläggande för all räkning med logaritmer:

> **Sats 9.** *För räkning med logaritmer gäller (där s > 0, t > 0):*

```
(35)    ᵃlog 1 = 0

(36)    ᵃlog(st) = ᵃlog s + ᵃlog t        (logaritm av produkt = summa av logaritmer)

(37)    ᵃlog(s/t) = ᵃlog s − ᵃlog t        (logaritm av kvot = differens av logaritmer)

(38)    ᵃlog sᵗ = t · ᵃlog s               (exponenter kan "lyftas ner" som faktor)

(39)    ᵇlog s = ᵃlog s / ᵃlog b            (basbytesformeln)
```

> 🎯 **De viktigaste att minnas:**
> - **(36)** Logaritmen **omvandlar multiplikation till addition**. Detta var historiskt logaritmens huvudsakliga användning — att förenkla beräkningar!
> - **(38)** Exponenter kan "plockas ner" framför logaritmen
> - **(39)** Basbytesformeln låter dig byta mellan valfria baser

### Bevisidéer

**Bevis av (36):** Enligt definitionen (33) gäller a^(ᵃlog(st)) = st. Men a^(ᵃlog s) · a^(ᵃlog t) = s · t (potenslagen 23). Alltså har VL och HL samma exponent.

**Bevis av (39):** Vi har a^(ᵃlog b · ᵇlog s) = (a^(ᵃlog b))^(ᵇlog s) = b^(ᵇlog s) = s. Men a^(ᵃlog s) = s också. Alltså: ᵃlog b · ᵇlog s = ᵃlog s, dvs. ᵇlog s = ᵃlog s / ᵃlog b.

---

### Exempel 31: Förenkla logaritmuttryck

**Uppgift:** Förenkla ln √2 − (1/3)ln 8 + (1/2)ln(2e²).

**Lösning:** Använd logaritmlagarna steg för steg:

1. Använd (38) på andra termen: (1/3)ln 8 = ln 8^(1/3) = ln 2
2. Använd (38) på tredje termen: (1/2)ln(2e²) = ln(2e²)^(1/2) = ln √(2e²)
3. Sätt ihop med (36) och (37):

```
ln √2 − ln 2 + ln √(2e²) = ln(√2 · √(2e²) / 2)
= ln(√(2 · 2e²) / 2)
= ln(√(4e²) / 2)
= ln(2e / 2)
= ln e = 1
```

---

### Lösa logaritmekvationer

**Grundprincipen:** Skriv om alla logaritmer till **samma bas**, och utnyttja att logaritmfunktionen är injektiv (ᵃlog x = ᵃlog y ⟹ x = y).

### Exempel 32: Ekvation med olika baser

**Lös:** ²log x + ⁴log(x + 1)² = 1

**Lösning:** Byt till samma bas. Använd basbytesformeln (39):

```
⁴log(x+1)² = ²log(x+1)² / ²log 4 = 2 · ²log(x+1) / 2 = ²log(x+1)
```

Ekvationen blir: ²log x + ²log(x+1) = 1

Använd logaritmlagen (36): ²log[x(x+1)] = 1

Definitionen av logaritm: x(x+1) = 2¹ = 2, dvs. **x² + x − 2 = 0**

Lösningar: x = 1 eller x = −2.

Eftersom ²log x bara är definierad för x > 0, måste vi förkasta x = −2.

**Svar: x = 1**

> ⚠️ **Viktig kontroll:** Vid logaritmekvationer måste man alltid kontrollera att lösningarna ger *positiva* argument i alla logaritmer! Falska rötter kan uppstå.

### Exempel 33: Exponentialekvation

**Lös:** 2ˣ + 2^(x+1) + 2^(x+2) = 5ˣ

**Lösning:** Förenkla vänsterledet med potenslagar:
```
2ˣ(1 + 2 + 4) = 2ˣ · 7 = 5ˣ
```

Det sökta talet x uppträder i exponenterna. Logaritmera båda leden:
```
ln(2ˣ · 7) = ln 5ˣ
x ln 2 + ln 7 = x ln 5
ln 7 = x(ln 5 − ln 2)
x = ln 7 / (ln 5 − ln 2) = ln 7 / ln(5/2)
```

---

## 1.7.2 Logaritmfunktioner

### Definition

Om vi i uttrycket ᵃlog x håller basen a > 1 fix och låter x variera får vi en funktion:

```
f(x) = ᵃlog x,       x > 0
```

som kallas **logaritmfunktionen** med bas a.

### Egenskaper (a > 1)

| Egenskap | Värde |
|----------|-------|
| Definitionsmängd | x > 0 (positiva reella tal) |
| Värdemängd | Hela ℝ |
| Monotoni | Strängt växande |
| f(1) | 0 (ty ᵃlog 1 = 0) |

```
(40)    ᵃlog x → +∞     då x → +∞

(41)    ᵃlog x → −∞     då x → 0⁺
```

> 💡 Logaritmfunktionen växer **mycket långsamt**. Även om den förr eller senare passerar varje given nivå, tar det extremt lång tid. Till exempel: lg x = 6 kräver x = 10⁶ = en miljon, och lg x = 9 kräver x = en miljard.

### Fallet 0 < a < 1

Om basen ligger mellan 0 och 1 blir logaritmfunktionen **strängt avtagande** (jämför med exponentialfunktionen med bas < 1).

### Relation till exponentialfunktionen

Logaritmfunktionen f(x) = ᵃlog x är den **inversa funktionen** till exponentialfunktionen g(x) = aˣ.

Grafiskt betyder detta att kurvorna y = aˣ och y = ᵃlog x är **spegelbilder av varandra** i linjen y = x.

---

## 1.7.3 Jämförelse mellan logaritm- och potensfunktioner

### Sats 10 — Potensfunktionen slår logaritmfunktionen

> **Sats 10.** Antag att α > 0 och a > 1. Då gäller att:
>
> ```
> (42)    xᵅ / ᵃlog x → +∞     då x → +∞
> ```
>
> Ekvivalent:
>
> ```
> (42')   ᵃlog x / xᵅ → 0      då x → +∞
> ```

> 🎯 **I klartext:** Alla potensfunktioner xᵅ (med α > 0) dominerar slutligen alla logaritmfunktioner. Även x^(0.001) kommer förr eller senare att vara ojämförligt mycket större än ln x.

### Bevis

Sätt ᵃlog x = t. Då x = aᵗ, och när x → +∞ gäller t → +∞. Alltså:

```
xᵅ / ᵃlog x = (aᵗ)ᵅ / t = (aᵅ)ᵗ / t
```

I täljaren står en exponentialfunktion med bas aᵅ > 1 och i nämnaren en potensfunktion (t¹). Enligt sats 8:

```
(aᵅ)ᵗ / t → +∞    då t → +∞ ✓
```

---

### Den stora rangordningen

Satserna 8 och 10 ger en fullständig **rangordning** för stora x:

```
ᵃlog x    ≪    xᵅ    ≪    bˣ
(logaritm)   (potens)   (exponential)
```

(där a > 1, α > 0, b > 1). Speciellt:

```
bˣ / ᵃlog x → +∞    då x → +∞
```

> 🎯 **Minnesregel:** "Exponentiell tillväxt slår potensiell tillväxt slår logaritmisk tillväxt." Detta är ett fundamentalt resultat som används genomgående i analysen.
>
> Att tänka i termer av "vem som vinner" på lång sikt — exponentiell, polynomisk eller logaritmisk — är en central förmåga i matematik och datalogi.

### Exempel 34: Gränsvärdesberäkning med rangordningen

**Beräkna:** lim(x→+∞) (eˣ + x² + ln x) / (3eˣ + 2ˣ)

**Lösning:** Dividera täljare och nämnare med nämnarens dominerande funktion. Vilken term dominerar? Båda eˣ och 2ˣ är exponentiella, men eˣ dominerar 2ˣ (ty e > 2). Dividera med eˣ:

```
= [1 + x²/eˣ + (ln x)/eˣ] / [3 + (2/e)ˣ]
```

- x²/eˣ → 0 (sats 8: exponentiell slår potens)
- (ln x)/eˣ → 0 (rangordningen: exp slår log)
- (2/e)ˣ → 0 (ty 0 < 2/e < 1)

```
Gränsvärdet = (1 + 0 + 0) / (3 + 0) = 1/3
```

---

## 1.7.4 Några tillämpningar av logaritmer

### Historisk bakgrund

Logaritmerna introducerades ursprungligen (av Napier, 1614) som ett **beräkningsverktyg**: via logaritmlagarna (36) och (37) omvandlas multiplikation och division till addition och subtraktion. Med en logaritmtabell kunde man utföra avancerade beräkningar snabbt. Idag har datorerna tagit över denna roll, men logaritmfunktionen förblir centralt viktig som invers till exponentialfunktionen.

### Logaritmisk skala

Så snart en vetenskaplig storhet spänner över **många tiopotenser** (storleksordningar) är det praktiskt att beskriva den med logaritmer. Istället för mätetalet c använder man ¹⁰log c = lg c. Man talar då om en **logaritmisk skala**.

### pH-värdet (kemi)

```
pH = − lg h
```

där h är vätejonkoncentrationen i mol/dm³. Minustecknet gör att pH oftast blir positivt. Koncentrationen spänner från 10⁻¹⁴ till 10¹:

- pH = 7: lösningen kallas **neutral**
- pH < 7: lösningen kallas **sur**
- pH > 7: lösningen kallas **basisk**

### Decibel (akustik)

Ljudnivån β i decibel definieras som:

```
β = 10 · lg(I / I₀)
```

där I är intensiteten (energi/areaenhet) och I₀ en fastlagd referensintensitet.

En **fördubbling** av intensiteten ger:
```
10 · lg(2I/I₀) − 10 · lg(I/I₀) = 10 · lg 2 ≈ 3
```

dvs. ungefär **3 decibel** ökning.

### Richterskalan (geologi)

Magnitud av jordbävningar mäts på **Richterskalan**, som också bygger på 10-logaritmer.

### Linlog- och loglog-papper

I handeln förekommer speciellt rutade papper:

- **Linlog-papper:** logaritmisk skala på ena axeln, linjär på den andra. En rät linje på sådant papper innebär ett samband av formen y = k · ln x + m, dvs. att x beror exponentiellt av y.

- **Loglog-papper:** logaritmisk skala på *båda* axlarna. En rät linje innebär sambandet ln y = k · ln x + m, dvs. y = eᵐ · xᵏ — en **potensfunktion**.

---

## 📊 Sammanfattande rangordning av funktionstyper

```
         Långsammast                        Snabbast
         tillväxt                            tillväxt
            ↓                                  ↓

       logaritmisk  <  polynomisk  <  exponentiell

       ln x, lg x      x, x², x¹⁰      2ˣ, eˣ, 10ˣ
```

Mer precist, för stora x:
```
ᵃlog x / xᵅ → 0      (logaritm förlorar mot potens)
xᵅ / bˣ → 0           (potens förlorar mot exponential)
ᵃlog x / bˣ → 0       (logaritm förlorar kraftigt mot exponential)
```

---

## 🎯 Checklista: Vad du bör kunna efter kapitel 1.6 och 1.7

**Kapitel 1.6 — Potens- och exponentialfunktioner:**
- [ ] Hur potenser aᵅ definieras steg för steg (heltal → bråk → reella)
- [ ] Alla potenslagarna (21)–(25) och ordningsrelationerna (26)–(27)
- [ ] Kunna förenkla potensuttryck (lyfta ut, addera exponenter)
- [ ] Skilja mellan potensfunktioner (f(x) = xᵅ) och exponentialfunktioner (f(x) = aˣ)
- [ ] Grafernas utseende för olika baser och exponenter
- [ ] Att exponentialfunktioner med a > 1 är strängt växande med värdemängd ]0, ∞[
- [ ] **Sats 8:** aˣ/xᵅ → +∞ (exponentiell slår potensiell tillväxt)
- [ ] Kunna tillämpa sats 8 vid gränsvärdesberäkningar

**Kapitel 1.7 — Logaritmfunktioner:**
- [ ] Definitionen: ᵃlog s är det tal a ska upphöjas till för att ge s
- [ ] De två grundrelationerna: a^(ᵃlog s) = s och ᵃlog aᵗ = t
- [ ] Alla logaritmlagarna (35)–(39), särskilt produktregeln och basbytesformeln
- [ ] Kunna förenkla logaritmuttryck (slå ihop/dela upp logaritmer)
- [ ] Lösa logaritmekvationer (byta till samma bas, kontrollera definitionsmängd)
- [ ] Lösa exponentialekvationer genom att logaritmera båda leden
- [ ] Logaritmfunktionens egenskaper: Df = ]0, ∞[, strängt växande, passerar (1, 0)
- [ ] Att logaritmfunktionen och exponentialfunktionen är varandras inverser
- [ ] **Sats 10:** xᵅ / ᵃlog x → +∞ (potens slår logaritm)
- [ ] **Den stora rangordningen:** logaritm ≪ potens ≪ exponential
- [ ] Tillämpningar: pH-skalan, decibel, logaritmisk skala
