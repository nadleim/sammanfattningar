# 📊 Analys av Algoritmer (Avsnitt 1.4)

## Komplett Sammanfattning

---

# Del 1: Introduktion, Vetenskaplig Metod och Observationer

---

## 🎯 Inledning och Motivation

### Fundamentala Frågor

När vi arbetar med datorer ställs vi oundvikligen inför två centrala frågor:

1. **Hur lång tid kommer mitt program att ta?**
2. **Varför får mitt program slut på minne?**

Dessa frågor uppstår i vardagliga situationer som att:

- Bygga om ett musik- eller fotobibliotek
- Installera nya applikationer
- Arbeta med stora dokument
- Bearbeta stora mängder experimentdata

### Komplexiteten i Frågeställningen

Svaren på dessa frågor beror på **flera faktorer**:

- **Datorns egenskaper** – processorkraft, minne, arkitektur
- **Data som bearbetas** – storlek, struktur, innehåll
- **Programmet som körs** – vilken algoritm som implementeras

> 💡 **Nyckelinsikt:** Trots denna komplexitet är vägen till användbara svar ofta förvånansvärt enkel, baserad på **vetenskaplig metod**.

---

## 🔬 Den Vetenskapliga Metoden

### Grundprinciper

Samma tillvägagångssätt som vetenskapsmän använder för att förstå den naturliga världen är effektiv för att studera programprestanda:

```
┌──────────────────────────────────────────────────────────────┐
│              DEN VETENSKAPLIGA METODEN                       │
├──────────────────────────────────────────────────────────────┤
│  1. OBSERVERA    → Mät någon egenskap med precision          │
│  2. HYPOTES      → Skapa en modell som passar observationer  │
│  3. FÖRUTSÄG     → Använd hypotesen för att förutsäga        │
│  4. VERIFIERA    → Kontrollera förutsägelser med nya obs.    │
│  5. VALIDERA     → Upprepa tills hypotes och obs. stämmer    │
└──────────────────────────────────────────────────────────────┘
```

### Viktiga Principer

1. **Reproducerbarhet:** Experiment måste kunna upprepas av andra för att validera hypotesen
2. **Falsifierbarhet:** Vi måste kunna veta när en hypotes är fel (och behöver revideras)

> 📜 **Einstein-citatet:** "Ingen mängd experiment kan någonsin bevisa att jag har rätt; ett enda experiment kan bevisa att jag har fel."

**Viktigt att förstå:** Vi kan aldrig vara helt säkra på att en hypotes är absolut korrekt – vi kan bara validera att den är konsekvent med våra observationer.

---

## 📏 Observationer och Mätningar

### Kvantitativa Mätningar

**Utmaning:** Hur mäter vi körtiden för våra program?

**God nyhet:** Detta är mycket enklare än i naturvetenskaperna – vi behöver inte skicka raketer till Mars eller dela atomer. Vi kan **helt enkelt köra programmet**!

### Problemstorlek (Problem Size)

**Definition:** _Problemstorleken_ karakteriserar svårigheten av en beräkningsuppgift.

Den är vanligtvis:

- Storleken på indata (antal element)
- Värdet av ett kommandoradsargument

**Grundläggande observation:** Körtiden ökar med problemstorleken, men frågan är **hur mycket**?

### Känslighet för Indata

En annan viktig observation:

- **Ofta:** Körtiden beror främst på problemstorleken, inte på specifik indata
- **Ibland:** Körtiden varierar kraftigt beroende på indata (detta kräver djupare analys)

---

## 🧪 ThreeSum – Ett Löpande Exempel

### Problemet

**ThreeSum** räknar antalet tripplar i en fil med N heltal som summerar till 0.

```java
public class ThreeSum {
    public static int count(int[] a) {
        // Räkna tripplar som summerar till 0
        int N = a.length;
        int cnt = 0;
        for (int i = 0; i < N; i++)
            for (int j = i+1; j < N; j++)
                for (int k = j+1; k < N; k++)
                    if (a[i] + a[j] + a[k] == 0)
                        cnt++;
        return cnt;
    }
    
    public static void main(String[] args) {
        int[] a = In.readInts(args[0]);
        StdOut.println(count(a));
    }
}
```

### Förklaring av Algoritmen

1. **Tre nästlade loopar** går igenom alla möjliga kombinationer av tre olika element
2. **Villkoret `j = i+1` och `k = j+1`** säkerställer att vi bara räknar varje trippel en gång
3. **Tidskomplexitet:** Undersöker alla **N(N-1)(N-2)/6 ≈ N³/6** tripplar

### Praktiskt Experiment

Med testfiler `1Kints.txt` (1000 tal), `2Kints.txt` (2000 tal), etc:

- `1Kints.txt`: 70 tripplar som summerar till 0
- `2Kints.txt`: 528 tripplar
- `4Kints.txt`: 4039 tripplar
- `8Kints.txt`: Tar betydligt längre tid...

---

## ⏱️ Stopwatch – Mäta Körtid

### API för Stopwatch

```
┌────────────────────────────────────────────────────────────┐
│  public class Stopwatch                                     │
├────────────────────────────────────────────────────────────┤
│  Stopwatch()           Skapa en ny stopwatch               │
│  double elapsedTime()  Returnerar tid sedan skapande (sek) │
└────────────────────────────────────────────────────────────┘
```

### Implementation

```java
public class Stopwatch {
    private final long start;
    
    public Stopwatch() {
        start = System.currentTimeMillis();
    }
    
    public double elapsedTime() {
        long now = System.currentTimeMillis();
        return (now - start) / 1000.0;
    }
}
```

### Användning

```java
Stopwatch timer = new Stopwatch();
int cnt = ThreeSum.count(a);
double time = timer.elapsedTime();
```

---

## 📈 DoublingTest – Experimentell Analys

### Programmet

DoublingTest producerar experimentella data för ThreeSum genom att **fördubbla** arraystorleken vid varje steg:

```java
public class DoublingTest {
    public static double timeTrial(int N) {
        // Mät tid för ThreeSum.count() med N slumptal
        int MAX = 1000000;
        int[] a = new int[N];
        for (int i = 0; i < N; i++)
            a[i] = StdRandom.uniform(-MAX, MAX);
        Stopwatch timer = new Stopwatch();
        int cnt = ThreeSum.count(a);
        return timer.elapsedTime();
    }
    
    public static void main(String[] args) {
        // Skriv ut tabell över körtider
        for (int N = 250; true; N += N) {
            double time = timeTrial(N);
            StdOut.printf("%7d %5.1f\n", N, time);
        }
    }
}
```

### Typiska Resultat

```
     N    tid (s)
   250      0.0
   500      0.0
  1000      0.1
  2000      0.8
  4000      6.4
  8000     51.1
```

> **Observation:** Varje gång N fördubblas, multipliceras tiden med ungefär **8** (= 2³).

---

## 📊 Grafisk Analys – Log-Log-plottar

### Standard Plot vs Log-Log Plot

```
STANDARD PLOT                     LOG-LOG PLOT
     │                                  │
  50 │         •                    lg T│          •
     │                                  │        •
  40 │       •                          │      •     ← lutning = 3
     │                                  │    •
  30 │                                  │  •
     │     •                            │•
  20 │                            ──────┼────────────
     │   •                              │        lg N
  10 │                                  │
     │ •                                │
   0 ├─•───────────                     │
     └──────────────                    └────────────
           N                                  N
```

### Tolkning av Log-Log-plot

En **rät linje** med lutning 3 på log-log-plotten innebär:

```
lg(T(N)) = 3 · lg(N) + lg(a)
```

vilket är ekvivalent med:

```
T(N) = a · N³
```

### Beräkna Konstanten a

Från experimentdata: T(8000) = 51.1 sekunder

```
51.1 = a · 8000³
a = 51.1 / 8000³
a ≈ 9.98 × 10⁻¹¹
```

### Förutsägelser

Med ekvationen **T(N) = 9.98 × 10⁻¹¹ · N³**:

|N|Förutsagd tid|Verklig tid|
|---|---|---|
|8,000|51.1 s|51.1 s|
|16,000|408.8 s (~6.8 min)|409.3 s|
|32,000|3270.4 s (~55 min)|~3270 s|

> 🎯 **Potenslagen (Power Law):** Många naturliga och syntetiska fenomen beskrivs av T(N) = a·Nᵇ

---

## 🔑 Sammanfattning Del 1

### Viktiga Koncept

1. **Vetenskaplig metod** – Observera → Hypotes → Förutsäg → Verifiera → Validera
2. **Problemstorlek N** – Karakteriserar beräkningens svårighet
3. **Stopwatch** – Verktyg för att mäta körtid
4. **DoublingTest** – Fördubblar N för att upptäcka mönster
5. **Log-log-plottar** – Avslöjar potenssamband (T = aNᵇ)

### Minnesregel: SHLVF

```
S - Scientific method (Vetenskaplig metod)
H - Hypothesis formation (Hypotesbildning)
L - Log-log plots reveal patterns (Avslöjar mönster)
V - Validation through experiments (Validering)
F - Forecasting running times (Förutsägelser)
```

---

_Fortsättning i Del 2: Matematiska modeller och Tilde-approximation..._

# Del 2: Matematiska Modeller och Tilde-Approximation

---

## 🧮 Matematiska Modeller – Knuths Grundinsikt

### Historisk Bakgrund

I datavetenskapens tidiga dagar postulerade **D.E. Knuth** att det är möjligt att bygga matematiska modeller för att beskriva körtiden för **vilket program som helst**.

### Knuths Grundinsikt

Den totala körtiden för ett program bestäms av **två primära faktorer**:

```
┌─────────────────────────────────────────────────────────────────┐
│           KNUTHS TVÅ GRUNDLÄGGANDE FAKTORER                     │
├─────────────────────────────────────────────────────────────────┤
│  1. KOSTNADEN för att exekvera varje sats                       │
│     → Beror på: dator, Java-kompilator, operativsystem          │
│                                                                 │
│  2. FREKVENSEN för exekvering av varje sats                     │
│     → Beror på: programmet och indata                           │
└─────────────────────────────────────────────────────────────────┘
```

### Beräkning av Total Körtid

**Principen:** Multiplicera kostnad med frekvens för alla instruktioner och summera:

```
Total körtid = Σ (kostnad_i × frekvens_i)
```

---

## 📊 Frekvensanalys av ThreeSum

### Analysera Varje Kodblock

```java
public class ThreeSum {
    public static int count(int[] a) {
        int N = a.length;            // Block A: körs 1 gång
        int cnt = 0;                 // Block A: körs 1 gång
        for (int i = 0; i < N; i++)  // Block B: körs N gånger
            for (int j = i+1; j < N; j++)     // Block C: ~N²/2 gånger
                for (int k = j+1; k < N; k++) // Block D: ~N³/6 gånger
                    if (a[i] + a[j] + a[k] == 0)
                        cnt++;       // Block E: x gånger (beror på indata)
        return cnt;
    }
}
```

### Frekvenssammanställning

|Kodblock|Beskrivning|Frekvens|
|---|---|---|
|A|Initiering|1|
|B|Yttre loopen|N|
|C|Mellan loopen|N²/2 − N/2|
|D|Innersta loopen (if-satsen)|N³/6 − N²/2 + N/3|
|E|cnt++|x (beror på indata, 0 till ~N³/6)|

### Matematisk Härledning av D:s Frekvens

Antalet sätt att välja 3 olika element från N element:

```
C(N,3) = N!/(3!(N-3)!) = N(N-1)(N-2)/6
```

Utvecklat:

```
N(N-1)(N-2)/6 = N³/6 − N²/2 + N/3
```

---

## 〰️ Tilde-Approximation (~)

### Problemet med Komplexa Uttryck

Frekvensanalyser leder ofta till **komplicerade matematiska uttryck**:

```
N³/6 − N²/2 + N/3
```

**Fråga:** Hur förenklar vi detta?

### Definition av Tilde-notation

> **Definition:** Vi skriver **~f(N)** för att representera vilken funktion som helst som, när den divideras med f(N), närmar sig 1 när N växer.
> 
> Vi skriver **g(N) ~ f(N)** för att indikera att g(N)/f(N) närmar sig 1 när N växer.

**Formellt:** f(N) ~ g(N) ⟺ lim(N→∞) f(N)/g(N) = 1

### Praktisk Tillämpning

För N³/6 − N²/2 + N/3:

**Beräkning för N = 1000:**

- Ledande term: N³/6 = 166,666,667
- Resterande termer: −N²/2 + N/3 = −499,667

```
Relativ storlek: 499,667 / 166,666,667 ≈ 0.3% (försumbar)
```

**Slutsats:** N³/6 − N²/2 + N/3 **~ N³/6**

### Visuell Illustration

```
N³/6 − N²/2 + N/3
 │        │
 │        └─ Försumbara termer när N är stort
 │
 └─ LEDANDE TERM (dominerar)

     N = 1000:     166,167,000
     Ledande term: 166,666,667 (~99.7%)
```

---

## 📐 Vanliga Tilde-approximationer

### Exempel på Tilde-approximationer

|Funktion|Tilde-approximation|Tillväxtordning|
|---|---|---|
|N³/6 − N²/2 + N/3|~ N³/6|N³|
|N²/2 − N/2|~ N²/2|N²|
|lg N + 1|~ lg N|lg N|
|3|~ 3|1|

### Allmän Form

De flesta tilde-approximationer har formen:

```
g(N) ~ a·f(N)    där f(N) = Nᵇ(log N)ᶜ
```

med a, b, c som konstanter. Vi kallar f(N) för **tillväxtordningen** (order of growth).

---

## 📈 Tillväxtordningar (Order of Growth)

### Vanliga Tillväxtordningar

```
┌─────────────────────────────────────────────────────────────────┐
│              VANLIGA TILLVÄXTORDNINGAR                          │
├──────────────┬──────────┬───────────────────────────────────────┤
│ Namn         │ Funktion │ Beskrivning                           │
├──────────────┼──────────┼───────────────────────────────────────┤
│ Konstant     │ 1        │ Oberoende av N                        │
│ Logaritmisk  │ log N    │ Knappt långsammare än konstant        │
│ Linjär       │ N        │ Proportionell mot problemstorleken    │
│ Linjäritmisk │ N log N  │ Typisk för effektiva sorteringar      │
│ Kvadratisk   │ N²       │ Typisk för två nästlade loopar        │
│ Kubisk       │ N³       │ Typisk för tre nästlade loopar        │
│ Exponentiell │ 2ᴺ       │ Extremt långsam – oanvändbar          │
└──────────────┴──────────┴───────────────────────────────────────┘
```

### Visuell Jämförelse

```
        Tid
         │
  2ᴺ  →  │                                          ╱
         │                                        ╱
  N³  →  │                                    ╱╱╱
         │                                ╱╱╱
  N²  →  │                          ╱╱╱╱╱
         │                    ╱╱╱╱╱
N log N→ │              ╱─────
         │         ╱────
    N →  │     ╱───
         │  ╱──
 log N→  │╱─────────────────────
    1 →  │════════════════════════
         └────────────────────────────→ N
                Problemstorlek
```

### Praktiska Konsekvenser

|Tillväxtordning|N=1000|N=1000000|Hanterbart?|
|---|---|---|---|
|1|1|1|✅ Alltid|
|log N|10|20|✅ Alltid|
|N|1,000|1,000,000|✅ Ja|
|N log N|10,000|20,000,000|✅ Ja|
|N²|1,000,000|10¹²|⚠️ Gränsfall|
|N³|10⁹|10¹⁸|❌ Problematisk|
|2ᴺ|10³⁰⁰|10³⁰⁰⁰⁰⁰|❌ Omöjligt|

---

## 🔬 Fullständig Analys av ThreeSum

### Detaljerad Frekvenstabell

```
┌──────────┬────────────┬──────────────────────────┬──────────────────────────────┐
│ Block    │ Tid (sek)  │ Frekvens                 │ Total tid                    │
├──────────┼────────────┼──────────────────────────┼──────────────────────────────┤
│ E (cnt++)│ t₀         │ x (beror på indata)      │ t₀ · x                       │
│ D (if)   │ t₁         │ N³/6 − N²/2 + N/3        │ t₁(N³/6 − N²/2 + N/3)        │
│ C (j-loop)│ t₂        │ N²/2 − N/2               │ t₂(N²/2 − N/2)               │
│ B (i-loop)│ t₃        │ N                        │ t₃ · N                       │
│ A (init) │ t₄         │ 1                        │ t₄                           │
├──────────┴────────────┴──────────────────────────┼──────────────────────────────┤
│ TOTAL                                            │ (t₁/6)N³ + (t₂/2−t₁/2)N² +   │
│                                                  │ (t₁/3+t₂/2+t₃)N + t₄ + t₀x   │
├──────────────────────────────────────────────────┼──────────────────────────────┤
│ TILDE-APPROXIMATION (om x är liten)              │ ~ (t₁/6) · N³                │
├──────────────────────────────────────────────────┼──────────────────────────────┤
│ TILLVÄXTORDNING                                  │ N³                           │
└──────────────────────────────────────────────────┴──────────────────────────────┘
```

### Den Inre Loopen (Inner Loop)

**Definition:** De instruktioner som exekveras **flest gånger** utgör programmets _inre loop_.

För ThreeSum är den inre loopen:

1. Inkrementera k och testa om k < N
2. Testa om summan av tre tal är 0
3. (Eventuellt cnt++ beroende på indata)

> 💡 **Viktig observation:** Körtiden för de flesta program beror endast på en **liten delmängd** av deras instruktioner – den inre loopen!

---

## ✅ Property A – Hypotes om ThreeSum

### Formulering

> **Property A:** Tillväxtordningen för körtiden av ThreeSum (för att räkna antalet tripplar som summerar till 0 bland N tal) är **N³**.

### Bevis/Evidence

**Matematisk modell:** T(N) ~ aN³ för någon maskinberoende konstant a

**Experimentell validering:** Experiment på många datorer bekräftar denna approximation

### Terminologi

I boken används:

- **Property** = Hypotes som behöver valideras genom experiment
- **Proposition** = Matematisk sanning om algoritmer (baserat på kostnadsmodell)

---

## 🎯 Kostnadsmodell (Cost Model)

### Definition

En **kostnadsmodell** definierar de grundläggande operationerna som används av algoritmerna vi studerar.

### Kostnadsmodell för 3-sum-problemet

> **3-sum kostnadsmodell:** Vi räknar **arrayåtkomster** (antalet gånger ett arrayelement läses eller skrivs).

### Proposition B

> **Proposition B:** Brute-force 3-sum-algoritmen använder **~N³/2 arrayåtkomster** för att beräkna antalet tripplar som summerar till 0 bland N tal.

**Bevis:** Algoritmen kommer åt var och en av de 3 talen för var och en av ~N³/6 tripplar.

```
3 × (N³/6) = N³/2
```

### Skillnad: Proposition vs Property

```
┌────────────────────────────────────────────────────────────────────┐
│  PROPOSITION                      │  PROPERTY                      │
├────────────────────────────────────────────────────────────────────┤
│  Matematisk sanning               │  Hypotes                       │
│  Baserad på kostnadsmodell        │  Behöver validering            │
│  "Algoritmen använder ~N³/2       │  "Körtiden är ~aN³"            │
│   arrayåtkomster"                 │                                │
│  Gäller för algoritmen            │  Gäller för implementationen   │
└────────────────────────────────────────────────────────────────────┘
```

---

## 📝 Sammanfattning: Att Utveckla en Matematisk Modell

### De Fyra Stegen

```
┌─────────────────────────────────────────────────────────────────────┐
│     STEG FÖR ATT UTVECKLA EN MATEMATISK MODELL AV KÖRTID           │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  1️⃣  UTVECKLA EN INDATAMODELL                                      │
│      • Inkludera definition av problemstorlek N                     │
│      • Specificera vilken typ av indata som förväntas               │
│                                                                     │
│  2️⃣  IDENTIFIERA DEN INRE LOOPEN                                   │
│      • Hitta kodavsnittet som körs flest gånger                     │
│      • Detta dominerar den totala körtiden                          │
│                                                                     │
│  3️⃣  DEFINIERA EN KOSTNADSMODELL                                   │
│      • Välj operationer i den inre loopen att räkna                 │
│      • T.ex. jämförelser, arrayåtkomster, etc.                      │
│                                                                     │
│  4️⃣  BESTÄM FREKVENSEN AV DESSA OPERATIONER                        │
│      • Använd matematisk analys                                     │
│      • Kan kräva kombinatorik, summor, etc.                         │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Exempel: Binary Search

|Steg|Binary Search|
|---|---|
|Indatamodell|Array a[] av storlek N|
|Inre loop|Satserna i while-loopen|
|Kostnadsmodell|Jämförelseoperationen|
|Frekvens|Högst lg N + 1 jämförelser|

### Exempel: Whitelist-sökning

|Steg|Whitelist|
|---|---|
|Indatamodell|N tal i whitelist, M tal på standard input (M >> N)|
|Inre loop|Satserna i while-loopen|
|Kostnadsmodell|Jämförelseoperationen (ärvd från binary search)|
|Frekvens|Högst M(lg N + 1) jämförelser|

**Slutsats:** Tillväxtordningen för whitelist-beräkning är **högst M lg N**.

---

## 🔢 Användbara Matematiska Funktioner och Approximationer

### Vanliga Funktioner i Algoritmanalys

|Beskrivning|Notation|Definition|
|---|---|---|
|Golv (floor)|⌊x⌋|Största heltal ≤ x|
|Tak (ceiling)|⌈x⌉|Minsta heltal ≥ x|
|Naturlig logaritm|ln N|logₑ N|
|Binär logaritm|lg N|log₂ N|
|Heltalsbinär logaritm|⌊lg N⌋|(antal bitar i N) − 1|
|Harmoniska tal|Hₙ|1 + 1/2 + 1/3 + ... + 1/N|
|Fakultet|N!|1 × 2 × 3 × ... × N|

### Användbara Approximationer

|Beskrivning|Approximation|
|---|---|
|Harmonisk summa|Hₙ = 1 + 1/2 + ... + 1/N ~ ln N|
|Triangulär summa|1 + 2 + 3 + ... + N ~ N²/2|
|Geometrisk summa|1 + 2 + 4 + ... + N = 2N − 1 ~ 2N (när N = 2ⁿ)|
|Stirlings approximation|lg N! ~ N lg N|
|Binomialkoefficient|C(N,k) ~ Nᵏ/k! (för litet k)|
|Exponential|(1 − 1/x)ˣ ~ 1/e|

---

## 🔑 Sammanfattning Del 2

### Kärnkoncept

1. **Knuths insikt:** Körtid = Σ(kostnad × frekvens)
2. **Tilde-approximation (~):** Ignorera låg-ordningsstermer
3. **Tillväxtordning:** Funktionen som dominerar för stora N
4. **Inre loop:** De instruktioner som exekveras flest gånger
5. **Kostnadsmodell:** Definierar vilka operationer vi räknar
6. **Proposition vs Property:** Matematisk sanning vs experimentell hypotes

### Minnesregel: TIKOF

```
T - Tilde-approximation (ignorera småtermer)
I - Inner loop (den inre loopen dominerar)
K - Kostnadsmodell (definiera vad vi räknar)
O - Order of growth (tillväxtordning)
F - Frekvensanalys (räkna exekveringar)
```

---

# Del 3: Tillväxtklassificeringar och Snabbare Algoritmer

---

## 📊 Detaljerade Tillväxtklassificeringar

### De Sju Grundläggande Klasserna

```
┌──────────────────────────────────────────────────────────────────────────────────┐
│           SAMMANFATTNING AV VANLIGA TILLVÄXTORDNINGAR                            │
├──────────────┬──────────────┬────────────────────────────┬───────────────────────┤
│ Beskrivning  │ Ordning      │ Typisk kod                 │ Exempel               │
├──────────────┼──────────────┼────────────────────────────┼───────────────────────┤
│ KONSTANT     │ 1            │ a = b + c;                 │ Addera två tal        │
│              │              │                            │                       │
│ LOGARITMISK  │ log N        │ [binary search]            │ Binärsökning          │
│              │              │                            │                       │
│ LINJÄR       │ N            │ for(i=0; i<N; i++)         │ Hitta maximum         │
│              │              │   if(a[i]>max) max=a[i];   │                       │
│              │              │                            │                       │
│ LINJÄRITMISK │ N log N      │ [mergesort]                │ Sortering             │
│              │              │                            │                       │
│ KVADRATISK   │ N²           │ for(i=0; i<N; i++)         │ Kontrollera           │
│              │              │   for(j=i+1; j<N; j++)     │ alla par              │
│              │              │     if(a[i]+a[j]==0) cnt++;│                       │
│              │              │                            │                       │
│ KUBISK       │ N³           │ for(i=0; i<N; i++)         │ Kontrollera           │
│              │              │   for(j=i+1; j<N; j++)     │ alla tripplar         │
│              │              │     for(k=j+1; k<N; k++)   │                       │
│              │              │       if(a[i]+a[j]+a[k]==0)│                       │
│              │              │         cnt++;             │                       │
│              │              │                            │                       │
│ EXPONENTIELL │ 2^N          │ [uttömmande sökning]       │ Alla delmängder       │
└──────────────┴──────────────┴────────────────────────────┴───────────────────────┘
```

---

### 1️⃣ Konstant Tid (1)

**Beskrivning:** Körtiden är **oberoende av problemstorleken N**.

```java
// Exempel: Hämta ett specifikt element
int x = a[i];  // Konstant tid

// Exempel: Enkel beräkning
int sum = a + b + c;
```

**Egenskaper:**

- Exekverar ett fast antal operationer
- Går inte att göra snabbare!
- De flesta enskilda Java-operationer är konstant tid

---

### 2️⃣ Logaritmisk Tid (log N)

**Beskrivning:** Körtiden växer **knappt märkbart** när N ökar. Halverar problemet i varje steg.

**Klassiskt exempel: Binärsökning**

```java
public static int binarySearch(int[] a, int key) {
    int lo = 0, hi = a.length - 1;
    while (lo <= hi) {
        int mid = lo + (hi - lo) / 2;
        if      (key < a[mid]) hi = mid - 1;
        else if (key > a[mid]) lo = mid + 1;
        else return mid;  // Hittad!
    }
    return -1;  // Ej hittad
}
```

**Varför logaritmisk?**

```
N = 1,000,000 → ~20 steg (lg 1,000,000 ≈ 20)
N = 1,000,000,000 → ~30 steg
```

**Minnesregel:** Om problemet halveras i varje steg → logaritmisk!

---

### 3️⃣ Linjär Tid (N)

**Beskrivning:** Körtiden är **direkt proportionell** mot problemstorleken.

```java
// Hitta maximum i en array
double max = a[0];
for (int i = 1; i < N; i++)
    if (a[i] > max)
        max = a[i];
```

**Egenskaper:**

- Behöver titta på varje element åtminstone en gång
- Ofta den **bästa möjliga** för problem som kräver att se all data

---

### 4️⃣ Linjäritmisk Tid (N log N)

**Beskrivning:** Typisk för algoritmer som använder **dela-och-härska** (divide and conquer).

**Klassiskt exempel: Mergesort**

- Dela arrayen i halvor
- Sortera varje halva rekursivt
- Sammanfoga (merge) de sorterade halvorna

**Praktisk betydelse:**

```
N = 1,000,000
N log N ≈ 20,000,000 operationer
N² = 1,000,000,000,000 operationer (50,000× långsammare!)
```

> 💡 **Nyckelinsikt:** Många viktiga problem har naturliga N²-lösningar men har smarta N log N-algoritmer. Detta är kritiskt för att hantera stora datamängder!

---

### 5️⃣ Kvadratisk Tid (N²)

**Beskrivning:** Typisk för algoritmer med **två nästlade loopar**.

```java
// TwoSum: Räkna par som summerar till 0
int cnt = 0;
for (int i = 0; i < N; i++)
    for (int j = i+1; j < N; j++)
        if (a[i] + a[j] == 0)
            cnt++;
```

**Varning:** Blir snabbt ohanterlig:

- N = 10,000 → 100,000,000 operationer
- N = 100,000 → 10,000,000,000 operationer

---

### 6️⃣ Kubisk Tid (N³)

**Beskrivning:** Typisk för algoritmer med **tre nästlade loopar**.

**Exempel: ThreeSum** (vårt löpande exempel)

**Praktiska begränsningar:**

```
N = 1,000  → 1 sekund
N = 10,000 → ~17 minuter (1000× längre)
N = 100,000 → ~11 dagar
```

---

### 7️⃣ Exponentiell Tid (2^N)

**Beskrivning:** **Extremt långsam** – fördubblas för varje ökning av N med 1.

**Typiskt:** Uttömmande sökning av alla delmängder

```
N = 20  → 2²⁰ ≈ 1,000,000 (hanterbart)
N = 30  → 2³⁰ ≈ 1,000,000,000 (10 sekunder)
N = 40  → 2⁴⁰ ≈ 1,000,000,000,000 (2 veckor)
N = 50  → 2⁵⁰ ≈ ... (32 år!)
```

> ⚠️ **Kritiskt:** Du kommer **aldrig** kunna köra en exponentiell algoritm till slut för stora problem. Ändå spelar de en viktig roll i algoritmteori.

---

## 📉 Visuell Jämförelse av Tillväxtordningar

### Standard Plot och Log-Log Plot

```
STANDARD PLOT                        LOG-LOG PLOT
(visar verklig tid)                  (visar tillväxtordning som lutning)

  Tid│                                   │
     │             ╱ exponentiell        │        ◢
     │            ╱                      │       ◢
     │         ╱╱ kubisk                 │      ◢    ← lutning 3 (kubisk)
     │       ╱╱                          │     ◢◢   ← lutning 2 (kvadratisk)
     │     ╱╱ kvadratisk                 │    ◢◢◢  ← lutning 1 (linjär)
     │   ─── linjäritmisk               │  ◢◢◢◢   ← lutning <1 (linjäritmisk)
     │  ─── linjär                      │◢◢◢◢◢    ← lutning →0 (logaritmisk)
     │ ─── logaritmisk                  │════════  ← lutning 0 (konstant)
     │═════ konstant                    │
     └────────────────────────           └──────────────────────────
                 N                                 lg N
```

### Praktisk Betydelse

**Kvadratiska och kubiska algoritmer är INTE praktiska för stora problem!**

Flera viktiga problem har:

- Naturliga brute-force lösningar som är kvadratiska
- Smarta algoritmer som är linjäritmiska

Dessa smarta algoritmer är **kritiska** – de gör skillnaden mellan att kunna lösa ett problem och inte kunna lösa det.

---

## 🚀 Designa Snabbare Algoritmer

### Strategin

**Fråga:** Hur kan vi designa snabbare algoritmer?

**Svar:** Utnyttja kända effektiva algoritmer som byggstenar!

Vi har redan sett:

- **Mergesort** – linjäritmisk sortering
- **Binary Search** – logaritmisk sökning

### Uppvärmning: 2-sum-problemet

**Problem:** Räkna antalet par av heltal som summerar till 0.

#### Brute-Force: TwoSum (Kvadratisk)

```java
public class TwoSum {
    public static int count(int[] a) {
        int N = a.length;
        int cnt = 0;
        for (int i = 0; i < N; i++)
            for (int j = i+1; j < N; j++)
                if (a[i] + a[j] == 0)
                    cnt++;
        return cnt;
    }
}
```

**Tillväxtordning:** N² (två nästlade loopar)

---

#### Förbättrad: TwoSumFast (Linjäritmisk)

**Nyckelidé:** Ett element a[i] är del av ett par som summerar till 0 **om och endast om** värdet -a[i] finns i arrayen!

```java
import java.util.Arrays;

public class TwoSumFast {
    public static int count(int[] a) {
        Arrays.sort(a);  // Sortera först (N log N)
        int N = a.length;
        int cnt = 0;
        for (int i = 0; i < N; i++)
            // Binärsök efter -a[i]
            if (BinarySearch.rank(-a[i], a) > i)
                cnt++;
        return cnt;
    }
}
```

#### Analys av TwoSumFast

1. **Sortering:** N log N (mergesort)
2. **N binärsökningar:** N × log N = N log N

**Total:** N log N + N log N = **O(N log N)** – linjäritmisk!

#### Varför `> i`?

Testet `BinarySearch.rank(-a[i], a) > i` hanterar tre fall:

```
┌────────────────────────────────────────────────────────────────────┐
│  Fall 1: Sökning misslyckas → rank() returnerar -1               │
│          → Inget par hittat → Räkna INTE                          │
│                                                                    │
│  Fall 2: rank() returnerar j > i                                  │
│          → a[i] + a[j] = 0 → Räkna paret!                         │
│                                                                    │
│  Fall 3: rank() returnerar j mellan 0 och i                       │
│          → Paret finns men redan räknat → Räkna INTE             │
│          (undviker dubbelräkning)                                  │
└────────────────────────────────────────────────────────────────────┘
```

---

### Fast Algorithm för 3-sum: ThreeSumFast

**Samma idé:** Ett par (a[i], a[j]) är del av en trippel som summerar till 0 **om och endast om** värdet -(a[i] + a[j]) finns i arrayen!

```java
import java.util.Arrays;

public class ThreeSumFast {
    public static int count(int[] a) {
        Arrays.sort(a);  // Sortera först
        int N = a.length;
        int cnt = 0;
        for (int i = 0; i < N; i++)
            for (int j = i+1; j < N; j++)
                // Binärsök efter -(a[i] + a[j])
                if (BinarySearch.rank(-a[i]-a[j], a) > j)
                    cnt++;
        return cnt;
    }
}
```

#### Analys av ThreeSumFast

1. **Sortering:** N log N
2. **N(N-1)/2 binärsökningar:** ~N²/2 × log N = N² log N

**Total:** N log N + N² log N ≈ **N² log N**

#### Jämförelse

|Algoritm|Tillväxtordning|
|---|---|
|ThreeSum (brute-force)|N³|
|ThreeSumFast|N² log N|

**Förbättring:** ~N / log N gånger snabbare!

För N = 8000: ThreeSum tar ~51 sekunder, ThreeSumFast tar ~bråkdel av en sekund.

---

## 📊 Sammanställning: 2-sum och 3-sum

```
┌────────────────────────────────────────────────────────────────────┐
│              SAMMANFATTNING AV KÖRTIDER                           │
├────────────────┬──────────────────────────────────────────────────┤
│  Algoritm      │  Tillväxtordning                                 │
├────────────────┼──────────────────────────────────────────────────┤
│  TwoSum        │  N²                                              │
│  TwoSumFast    │  N log N                                         │
│  ThreeSum      │  N³                                              │
│  ThreeSumFast  │  N² log N                                        │
└────────────────┴──────────────────────────────────────────────────┘
```

### Visuell Jämförelse

```
Array-åtkomster (miljoner)                Array-åtkomster (tusentals)
för 3-sum                                 för 2-sum

     │                                          │
1000 │         ╱ ThreeSum (N³/2)                │         ╱ TwoSum (N²)
     │        ╱                            100 │        ╱
 800 │       ╱                                  │       ╱
     │      ╱                               80 │      ╱
 600 │     ╱                                    │     ╱
     │    ╱                                 60 │    ╱
 400 │   ╱                                      │   ╱
     │  ╱                                   40 │  ╱
 200 │ ╱    ══════════ ThreeSumFast             │ ╱   ─────── TwoSumFast
     │╱                (N² log N)           20 │╱            (4N log N)
     └─────────────────────                     └─────────────────────
        1K  2K  4K  8K  N                          1K  2K  4K  8K  N
```

---

## 🔻 Undre Gränser (Lower Bounds)

### Vad är en Undre Gräns?

En **undre gräns** anger den bästa möjliga körtid för **alla** algoritmer som löser ett visst problem.

### Undre Gränser för 2-sum och 3-sum

**2-sum:**

- Undre gräns: Ω(N log N) under en modell som endast tillåter jämförelser
- TwoSumFast är alltså **optimal** i denna modell!

**3-sum:**

- Ingen känd undre gräns bättre än linjär (N)
- Experter **tror** att den bästa möjliga algoritmen är kvadratisk (N²)
- Men detta är fortfarande ett öppet forskningsproblem!

> 💡 **Viktig insikt:** Att bevisa undre gränser är mycket svårare än att designa algoritmer!

---

## 📋 Strategi för Algoritmdesign

### Den Allmänna Metoden

```
┌─────────────────────────────────────────────────────────────────────┐
│              STRATEGI FÖR ATT HANTERA NYA PROBLEM                  │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  1️⃣  IMPLEMENTERA en enkel brute-force-lösning                     │
│      • Säkerställ korrekthet                                        │
│      • Analysera tillväxtordning                                    │
│                                                                     │
│  2️⃣  UNDERSÖK algoritmiska förbättringar                           │
│      • Kan vi använda sortering + binärsökning?                     │
│      • Finns det mönster som kan utnyttjas?                         │
│      • Kan vi minska tillväxtordningen?                             │
│                                                                     │
│  3️⃣  KÖR EXPERIMENT för att validera                               │
│      • Bekräfta att den nya algoritmen är snabbare                  │
│      • Mät faktiska förbättringar                                   │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Varför Detta Fungerar

- **Brute-force först:** Enklare att implementera och verifiera korrekthet
- **Förbättra sedan:** Nu har vi en referens att jämföra med
- **Validera experimentellt:** Teori och praktik överensstämmer inte alltid!

---

## 🔑 Sammanfattning Del 3

### Nyckellärdomar

1. **Sju tillväxtklasser:** 1, log N, N, N log N, N², N³, 2^N
2. **Kvadratiska/kubiska algoritmer** blir snabbt opraktiska
3. **Linjäritmiska algoritmer** är kritiska för stora problem
4. **Sortering + binärsökning** kan ofta förbättra brute-force-lösningar
5. **TwoSumFast & ThreeSumFast** visar kraften i smarta algoritmer

### Praktisk Tumregel

```
┌────────────────────────────────────────────────────────────────┐
│  OM du har nästlade loopar → UNDERSÖK om du kan göra bättre   │
│  OM problemet kan lösas med sortering → ÖVERVÄG det           │
│  OM du söker i sorterad data → ANVÄND binärsökning            │
└────────────────────────────────────────────────────────────────┘
```

### Minnesregel: SBBI

```
S - Sortera först (möjliggör effektiv sökning)
B - Binärsökning i sorterad data (log N)
B - Brute-force först för korrekthet
I - Iterera för att förbättra
```

---

# Del 4: Doubling Ratio och Prestandaförutsägelser

---

## 📈 Doubling Ratio-experiment

### Idén

**Doubling Ratio** är en enkel och kraftfull metod för att:

1. Förutsäga prestanda
2. Bestämma tillväxtordningen för ett program

### Metoden i Tre Steg

```
┌─────────────────────────────────────────────────────────────────────┐
│           DOUBLING RATIO-METODEN                                    │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  STEG 1: Utveckla en indata-generator                              │
│          • Producera indata som modellerar förväntad praktik        │
│          • T.ex. slumptal som i timeTrial()                         │
│                                                                     │
│  STEG 2: Kör DoublingRatio-programmet                              │
│          • Beräkna kvoten mellan varje körtid och den föregående    │
│          • Fördubbla N vid varje iteration                          │
│                                                                     │
│  STEG 3: Kör tills kvoterna närmar sig en gräns 2^b                │
│          • När kvoten stabiliseras → vi har hittat b                │
│          • Tillväxtordningen är N^b                                 │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

### DoublingRatio-programmet

```java
public class DoublingRatio {
    public static double timeTrial(int N) {
        // Samma som i DoublingTest (sida 177)
        int MAX = 1000000;
        int[] a = new int[N];
        for (int i = 0; i < N; i++)
            a[i] = StdRandom.uniform(-MAX, MAX);
        Stopwatch timer = new Stopwatch();
        int cnt = ThreeSum.count(a);
        return timer.elapsedTime();
    }
    
    public static void main(String[] args) {
        double prev = timeTrial(125);
        for (int N = 250; true; N += N) {
            double time = timeTrial(N);
            StdOut.printf("%6d %7.1f ", N, time);
            StdOut.printf("%5.1f\n", time/prev);  // KVOTEN!
            prev = time;
        }
    }
}
```

### Exempelkörning

```
     N     tid (s)  kvot
   250       0.0    2.7
   500       0.0    4.8
  1000       0.1    6.9
  2000       0.8    7.7
  4000       6.4    8.0  ← Kvoten börjar stabiliseras
  8000      51.1    8.0  ← Kvoten ≈ 8
 16000     408.8    8.0  ← Kvoten ≈ 8 (förutsägelse)
 32000    3270.4    8.0  ← Kvoten ≈ 8 (förutsägelse)
 64000   26163.2    8.0  ← Kvoten ≈ 8 (förutsägelse)
```

---

### Tolka Kvoten

**Observation:** Kvoten närmar sig **8**.

**Slutsats:**

```
8 = 2³    →    b = 3    →    Tillväxtordning = N³
```

### Förutsäga Körtider

När kvoten har stabiliserats:

1. **Multiplicera** senaste körtiden med kvoten
2. **Fördubbla** N

**Exempel:**

```
T(8000) = 51.1 sekunder
T(16000) ≈ 51.1 × 8 = 408.8 sekunder
T(32000) ≈ 408.8 × 8 = 3270.4 sekunder
T(64000) ≈ 3270.4 × 8 = 26163.2 sekunder (~7.3 timmar)
```

---

## 📐 Proposition C: Matematisk Grund för Doubling Ratio

### Varför Närmar Sig Kvoten en Konstant?

> **Proposition C (Doubling Ratio):** Om T(N) ~ a·N^b·lg N, då gäller T(2N)/T(N) ~ 2^b.

### Bevis

```
T(2N)     a·(2N)^b · lg(2N)
───── = ─────────────────────
T(N)      a·N^b · lg N

        (2N)^b     lg(2N)
      = ────── × ────────
         N^b       lg N

      = 2^b × (lg 2 + lg N)/lg N

      = 2^b × (1 + lg 2/lg N)

      → 2^b   när N → ∞
```

### Slutsats

- Kvoten **närmar sig 2^b** när N växer
- **Logaritmfaktorn spelar ingen roll** i praktiken för förutsägelser!

---

### Vanliga Kvoter och Motsvarande Tillväxtordningar

```
┌────────────────────────────────────────────────────────────────────┐
│        KVOT OCH TILLVÄXTORDNING                                   │
├──────────────┬────────────────────────────────────────────────────┤
│    Kvot      │    Tillväxtordning                                 │
├──────────────┼────────────────────────────────────────────────────┤
│    ~1        │    Konstant (1)                                    │
│    ~1        │    Logaritmisk (log N) - knappt märkbar ökning     │
│    ~2        │    Linjär (N)                                      │
│    ~2        │    Linjäritmisk (N log N) - log-faktorn försumbar  │
│    ~4        │    Kvadratisk (N²)                                 │
│    ~8        │    Kubisk (N³)                                     │
│    Ej stabil │    Exponentiell (2^N)                              │
└──────────────┴────────────────────────────────────────────────────┘
```

> ⚠️ **OBS:** Linjär och linjäritmisk ger båda kvot ~2. Detaljerad analys behövs för att skilja dem åt!

---

## 🔮 Moores Lag och Framtida Prestanda

### Moores Lag

**Tumregel:** Var 18:e månad kan du förvänta dig en dator som är:

- ~2× snabbare
- ~2× mer minne

Alternativt: ~10× snabbare och ~10× mer minne på 5 år.

### Praktiska Konsekvenser

**Fråga:** Kan vi "växa med" Moores lag?

```
┌────────────────────────────────────────────────────────────────────────────┐
│         MOORES LAG OCH ALGORITMPRESTANDA                                  │
├──────────────┬─────────┬──────────────────────────────────────────────────┤
│ Tillväxt-    │ 2× fak- │ Förutsagd tid för 10N  │ Tid för 10N på         │
│ ordning      │ tor     │ (samma dator)          │ 10× snabbare dator     │
├──────────────┼─────────┼────────────────────────┼────────────────────────┤
│ Linjär N     │ 2       │ 10× längre (en dag)    │ Samma (några timmar)   │
│ Linjärit.    │ 2       │ 10× längre (en dag)    │ Samma (några timmar)   │
│ Kvadratisk   │ 4       │ 100× längre (veckor)   │ 10× längre (en dag)    │
│ Kubisk       │ 8       │ 1000× längre (månader) │ 100× längre (veckor)   │
│ Exponentiell │ 2^N     │ 2^(9N) längre (aldrig) │ 2^(9N)/10 (aldrig)     │
└──────────────┴─────────┴────────────────────────┴────────────────────────┘
```

### Slutsats

> 🎯 **Viktig lärdom:** Du kan **INTE** hålla jämna steg med Moores lag om du använder kvadratiska eller kubiska algoritmer!

Doubling ratio-testet avslöjar snabbt om din algoritm är:

- ✅ Linjär/linjäritmisk (kvot ~2) → Skalbar!
- ⚠️ Kvadratisk (kvot ~4) → Problem vid stora N
- ❌ Kubisk (kvot ~8) → Allvarligt problem
- ❌ Exponentiell (instabil kvot) → Oanvändbar

---

## 📋 Använd Doubling Ratio i Praktiken

### När Ska Du Använda Det?

**Rekommendation:** Kör doubling ratio-experiment för **varje program där prestanda spelar roll**.

### Fördelar

1. **Enkelt:** Kräver minimal kod
2. **Snabbt:** Avslöjar tillväxtordning inom minuter
3. **Praktiskt:** Kan avslöja "prestandabuggar"

### Exempel på Prestandabugg

Du kanske tror att din algoritm är linjär, men doubling ratio avslöjar kvot ~4!

```
Förväntat (linjär):     Faktiskt (kvadratisk):
  N    tid   kvot         N    tid   kvot
 1000  0.1   ~2          1000  0.1   ~4
 2000  0.2   ~2          2000  0.4   ~4
 4000  0.4   ~2          4000  1.6   ~4
 8000  0.8   ~2          8000  6.4   ~4   ← BUGG!
```

**Orsak:** Kanske en gömd nästlad loop, ineffektiv datastruktur, etc.

---

## ⚠️ Varningar och Fallgropar (Caveats)

### Varför Kan Analysen Bli Fel?

Det finns **många anledningar** till inkonsekventa eller missvisande resultat.

---

### 1️⃣ Stora Konstanter

**Problem:** Vi ignorerar konstanta koefficienter i låg-ordningsstermer.

```
T(N) = 2N² + cN

Om c = 10³ eller 10⁶, kan vi inte ignorera cN för små N!
```

**Exempel:**

```
N = 100:  2·100² + 10⁶·100 = 20,000 + 100,000,000
                           ≈ 100,000,000 (domineras av cN!)
```

---

### 2️⃣ Icke-dominant Inre Loop

**Problem:** Vår kostnadsmodell kanske missar den verkliga inre loopen.

**Orsaker:**

- N är inte tillräckligt stort för att ledande termen ska dominera
- Betydande kod utanför den identifierade inre loopen

**Lösning:** Förfina kostnadsmodellen.

---

### 3️⃣ Instruktioners Tidsvariation

**Problem:** Antagandet att varje instruktion tar samma tid är inte alltid sant.

**Cachning:** Minnesåtkomst varierar kraftigt beroende på om data finns i cache.

```
┌─────────────────────────────────────────────────────────────────────┐
│  MINNESTYP          │  ÅTKOMSTTID                                  │
├─────────────────────┼──────────────────────────────────────────────┤
│  L1 Cache           │  ~1 ns                                       │
│  L2 Cache           │  ~4 ns                                       │
│  L3 Cache           │  ~10 ns                                      │
│  RAM                │  ~100 ns                                     │
│  SSD                │  ~100,000 ns                                 │
│  HDD                │  ~10,000,000 ns                              │
└─────────────────────┴──────────────────────────────────────────────┘
```

**Observation:** Efter att kvoten verkar stabiliseras vid 8, kan den hoppa till ett högre värde för stora arrayer (cache-missar).

---

### 4️⃣ Systemfaktorer

**Problem:** Mycket annat pågår på din dator!

**Störningar:**

- Garbage collection i Java
- JIT-kompilering (Just-In-Time)
- Andra processer
- Nätverksaktivitet
- OS-aktiviteter

**Konsekvens:** Experiment kanske inte är reproducerbara.

**Lösning:**

- Kör flera experiment och ta medelvärde
- Isolera testsystemet
- Var medveten om variabiliteten

---

### 5️⃣ "Too Close to Call"

**Problem:** Två algoritmer kan vara jämlika för olika indata.

**Situation:** Algoritm A är snabbare i vissa fall, Algoritm B i andra.

**Varning:** Överdrivet fokus på "racing" för att hitta "bästa" algoritmen är ofta slöseri med tid!

---

### 6️⃣ Stark Beroende av Indata

**Problem:** Körtiden kan variera dramatiskt beroende på indata.

**Exempel:** Modifierad ThreeSum som returnerar `true` vid första träffen:

```java
// Returnera true om någon trippel summerar till 0
for (int i = 0; i < N; i++)
    for (int j = i+1; j < N; j++)
        for (int k = j+1; k < N; k++)
            if (a[i] + a[j] + a[k] == 0)
                return true;  // TIDIG AVSLUTNING!
return false;
```

**Körtid:**

- **Bästa fall:** O(1) – första tre talen summerar till 0
- **Värsta fall:** O(N³) – inga tripplar summerar till 0

---

### 7️⃣ Flera Problemparametrar

**Problem:** Ibland är problemstorleken inte bara "N".

**Exempel:** Whitelist-sökning

```
Problemstorlek: N tal i whitelist, M tal att söka
Körtid: O(M log N)  – beror på BÅDE M och N!
```

Om vi bara varierar N och håller M konstant, eller vice versa, kan vi få missvisande resultat.

---

## 📊 Sammanfattning av Caveats

```
┌─────────────────────────────────────────────────────────────────────┐
│              POTENTIELLA FALLGROPAR                                │
├─────────────────────────────────────────────────────────────────────┤
│  1. Stora konstanter i låg-ordningsstermer                         │
│  2. Icke-dominant inre loop                                        │
│  3. Varierande instruktionstider (cachning)                        │
│  4. Systemfaktorer (GC, JIT, andra processer)                      │
│  5. "Too close to call" mellan algoritmer                          │
│  6. Stark beroende av specifik indata                              │
│  7. Flera problemparametrar                                        │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 🔑 Sammanfattning Del 4

### Kärnkoncept

1. **Doubling Ratio:** Fördubbla N, beräkna kvot → bestäm tillväxtordning
2. **Proposition C:** T(2N)/T(N) ~ 2^b för T(N) ~ aN^b log N
3. **Moores lag:** Snabbare datorer hjälper inte mot dåliga algoritmer
4. **Caveats:** Var medveten om potentiella felkällor

### Praktiska Tips

```
┌─────────────────────────────────────────────────────────────────────┐
│  ✅ DO:                                                            │
│     • Kör doubling ratio för prestandakritiska program             │
│     • Var misstänksam om kvoten inte stabiliseras                  │
│     • Kör flera experiment för tillförlitliga resultat             │
│                                                                     │
│  ❌ DON'T:                                                         │
│     • Anta att snabbare dator löser algoritmiska problem           │
│     • Ignorera höga kvoter (>4)                                    │
│     • Lita blint på ett enda experiment                            │
└─────────────────────────────────────────────────────────────────────┘
```

### Minnesregel: DKVP

```
D - Doubling ratio (fördubbla och mät)
K - Kvoten avslöjar tillväxtordning
V - Var medveten om fallgropar
P - Praktiska experiment validerar teori
```

---

# Del 5: Minnesanalys och Prestandagarantier

---

## 💾 Minnesanvändning

### Varför Analysera Minne?

**Två centrala frågor:**

1. Hur lång tid tar mitt program? ✓ (Redan behandlat)
2. **Varför får mitt program slut på minne?** ← Nu!

### Javaminne – Översikt

```
┌─────────────────────────────────────────────────────────────────────┐
│                      JAVA MINNESMODELL                             │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│   ┌──────────────────────────────────────────────────────────┐     │
│   │  OBJEKT                                                   │     │
│   │  ┌────────────────────────────────────────────────────┐  │     │
│   │  │  Object overhead (16 bytes)                        │  │     │
│   │  ├────────────────────────────────────────────────────┤  │     │
│   │  │  Instansvariabler (beroende på typ)                │  │     │
│   │  ├────────────────────────────────────────────────────┤  │     │
│   │  │  Padding (till multipel av 8 bytes)                │  │     │
│   │  └────────────────────────────────────────────────────┘  │     │
│   └──────────────────────────────────────────────────────────┘     │
│                                                                     │
│   Referens: 8 bytes (på 64-bit system)                             │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 📏 Minneskostnader för Primitiva Typer

### Primitiva Datatyper

```
┌────────────────────────────────────────────────────────────────────┐
│              MINNESANVÄNDNING FÖR PRIMITIVA TYPER                 │
├──────────────┬─────────────────────────────────────────────────────┤
│    Typ       │    Bytes                                           │
├──────────────┼─────────────────────────────────────────────────────┤
│    boolean   │    1                                                │
│    byte      │    1                                                │
│    char      │    2                                                │
│    short     │    2                                                │
│    int       │    4                                                │
│    float     │    4                                                │
│    long      │    8                                                │
│    double    │    8                                                │
└──────────────┴─────────────────────────────────────────────────────┘
```

---

## 📦 Objekt och Arrayer

### Objektoverhead

Varje Java-objekt har en **fast overhead på 16 bytes**:

- 8 bytes för referens till klassens metoder
- 4 bytes för garbage collection info
- 4 bytes för synkroniseringslås

### Arrayer

Arrayer är objekt och har **24 bytes overhead**:

- 16 bytes standard objektoverhead
- 4 bytes för längden (int)
- 4 bytes padding

```
┌────────────────────────────────────────────────────────────────────┐
│  MINNESANVÄNDNING FÖR ARRAYER                                     │
├──────────────────────────────────────────────────────────────────┬─┤
│  int[] med N element:                                            │ │
│  24 (overhead) + 4N (data) ≈ 4N bytes                           │ │
├──────────────────────────────────────────────────────────────────┼─┤
│  double[] med N element:                                         │ │
│  24 (overhead) + 8N (data) ≈ 8N bytes                           │ │
├──────────────────────────────────────────────────────────────────┼─┤
│  Object[] med N element (referenser):                            │ │
│  24 (overhead) + 8N (referenser) + N × (storlek per objekt)     │ │
└──────────────────────────────────────────────────────────────────┴─┘
```

### Tvådimensionella Arrayer

**Varning:** Tvådimensionella arrayer i Java är arrayer av arrayer!

```java
double[][] a = new double[M][N];
```

**Minnesförbrukning:**

```
Huvudarray:        24 + 8M bytes (M referenser)
M underarrayer:    M × (24 + 8N) bytes

Total: 24 + 8M + M(24 + 8N)
     = 24 + 8M + 24M + 8MN
     ≈ 8MN bytes (för stora M och N)
```

---

## 🔗 Länkade Strukturer

### Node-klass för Länkade Listor

```java
private class Node {
    Item item;      // 8 bytes (referens)
    Node next;      // 8 bytes (referens)
}
```

**Minneskostnad per nod:**

```
16 (objektoverhead) + 8 (item) + 8 (next) = 32 bytes
+ 8 bytes om Item är ett objekt (extra referens overhead)
```

### Stackimplementation med Länkad Lista

```java
public class Stack<Item> {
    private Node first;  // 8 bytes (referens)
    private int N;       // 4 bytes
    
    private class Node { ... }  // 32 bytes per nod
}
```

**Total minnesanvändning för stack med N element:**

```
16 (objektoverhead) + 8 (inner class overhead) + 8 (first) + 4 (N) + 4 (padding)
+ N × 32 (noder)
= 40 + 32N bytes
```

---

## 📊 Exempel: Minneskostnad för Integer-objekt

### Ett Integer-objekt

```
┌────────────────────────────────────────────────────────────────────┐
│            INTEGER OBJEKT I MINNET                                │
├────────────────────────────────────────────────────────────────────┤
│  ┌─────────────────────────────────────┐                          │
│  │  Object overhead        16 bytes   │                          │
│  ├─────────────────────────────────────┤                          │
│  │  int value               4 bytes   │                          │
│  ├─────────────────────────────────────┤                          │
│  │  Padding                 4 bytes   │                          │
│  ├─────────────────────────────────────┤                          │
│  │  TOTAL                  24 bytes   │                          │
│  └─────────────────────────────────────┘                          │
│                                                                    │
│  Jämfört med primitiv int: 4 bytes                                │
│  Overhead-faktor: 6× mer minne!                                   │
└────────────────────────────────────────────────────────────────────┘
```

### Konsekvens: Autoboxning är Dyrt!

```java
// Primitiv array - effektiv
int[] prims = new int[N];     // ~4N bytes

// Objekt-array - ineffektiv  
Integer[] objs = new Integer[N];  // ~24N + 24 bytes (6× mer!)
```

---

## 📈 Minnesanvändning i Praktiken

### Resizing Array-stack

```
┌────────────────────────────────────────────────────────────────────┐
│        MINNESANVÄNDNING FÖR RESIZING ARRAY                        │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│  Bästa fall:   Array är full                                      │
│                ~8N bytes (för referenser)                         │
│                                                                    │
│  Värsta fall:  Array är 25% full (just efter halvering)           │
│                ~32N bytes                                         │
│                                                                    │
│  Genomsnitt:   Mellan 8N och 32N bytes                            │
│                Beror på pushmönster                               │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

### Sammanfattande Jämförelse

|Implementation|Dataminne (per objekt)|Skapar objekt|
|---|---|---|
|Länkad lista (int)|32N bytes|N|
|Länkad lista (Integer)|64N bytes|2N|
|Resizing array (int)|4N - 16N bytes|lg N|
|Resizing array (Integer)|32N - 56N bytes|~N|

---

## 🛡️ Prestandagarantier

### Typer av Analys

```
┌─────────────────────────────────────────────────────────────────────┐
│              OLIKA TYPER AV PRESTANDAANALYS                        │
├──────────────────────────┬──────────────────────────────────────────┤
│  Värsta fall (Worst case)│  Maximal kostnad för ALLA möjliga       │
│                          │  indata. Garanterar en övre gräns.       │
├──────────────────────────┼──────────────────────────────────────────┤
│  Bästa fall (Best case)  │  Minimal kostnad för optimala indata.   │
│                          │  Ofta orealistiskt optimistisk.          │
├──────────────────────────┼──────────────────────────────────────────┤
│  Genomsnitt (Average)    │  Förväntad kostnad för typisk indata.   │
│                          │  Kräver en indatamodell.                 │
├──────────────────────────┼──────────────────────────────────────────┤
│  Amorterad (Amortized)   │  Total kostnad delat med antal op.      │
│                          │  Tillåter enstaka dyra operationer.      │
└──────────────────────────┴──────────────────────────────────────────┘
```

---

### Varför Behövs Värsta Fall-garantier?

**Scenario 1: Säkerhetskritiska System**

- Kärnkraftverksoftware
- Pacemakerstyrning
- Bromssystem i bilar

> "Vi MÅSTE garantera att mjukvaran avslutar inom tidsgränsen!"

**Scenario 2: Denial-of-Service-attacker**

Webbplatser utan prestandagarantier kan attackeras med "patologiska" förfrågningar:

```
Angripare skickar indata som triggar värsta fall-beteende
→ Servern blir överväldigad
→ Legitima användare nekas service
```

---

### Proposition D: Garantier för Länkade Implementationer

> **Proposition D:** I länkade list-implementationerna av Bag (Algoritm 1.4), Stack (Algoritm 1.2), och Queue (Algoritm 1.3), tar alla operationer **konstant tid i värsta fall**.

**Bevis:** Direkt från koden – antalet instruktioner för varje operation är begränsat av en liten konstant.

**Förutsättning:** Vi antar att Java skapar nya Node-objekt i konstant tid (rimligt antagande).

---

## 🎲 Randomiserade Algoritmer

### Idé

**Introducera slumpmässighet** för att ge probabilistiska prestandagarantier.

### Exempel: Quicksort

- **Värsta fall (deterministisk):** O(N²) – kvadratisk
- **Med slumpmässig ordning:** O(N log N) med mycket hög sannolikhet

```java
// Slumpa arrayen först
StdRandom.shuffle(a);
// Kör quicksort
sort(a, 0, a.length - 1);
```

**Sannolikhet att det tar linjäritmisk tid:** Så hög att det är som att få garantier!

> "Sannolikheten för dålig prestanda är mindre än sannolikheten att din dator träffas av blixten."

### Exempel: Hashning

- **Värsta fall:** O(N) – linjär
- **Med bra hashfunktion:** O(1) konstant med hög sannolikhet

---

## 🔄 Amorterad Analys

### Idé

**Tillåt enstaka dyra operationer** så länge genomsnittet är lågt.

### Prototypiskt Exempel: Resizing Array-stack

```java
public void push(Item item) {
    if (N == a.length) 
        resize(2 * a.length);  // DYR operation!
    a[N++] = item;
}
```

**Fråga:** push() kan ta O(N) tid (vid resize). Är detta acceptabelt?

### Analys

**Scenario:** Starta med kapacitet 1, pusha N element.

```
Resizes sker vid: 1, 2, 4, 8, 16, ..., N/2, N
Kostnad per resize: 2, 4, 8, 16, ..., N

Total resize-kostnad: 2 + 4 + 8 + ... + N = 2N - 2 ≈ 2N
Total antal push-operationer: N

Amorterad kostnad per push: 2N / N = 2 = O(1) konstant!
```

**Visualisering:**

```
┌─────────────────────────────────────────────────────────────────────┐
│  AMORTERAD ANALYS AV RESIZING ARRAY                               │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  Kostnad │                                                          │
│     N    │            █ (dyrt resize)                              │
│          │                                                          │
│    N/2   │        █                                                 │
│          │                                                          │
│    N/4   │    █                                                     │
│          │                                                          │
│     4    │  █                                                       │
│     2    │ █                                                        │
│     1    │█──────────────────────── (genomsnitt ~2)                │
│          └────────────────────────────────────────────────────→    │
│            1  2  4  8  16        N/2       N    Operationer        │
│                                                                     │
│  De flesta operationer kostar 1                                    │
│  Få operationer kostar mycket (resize)                             │
│  GENOMSNITTET är konstant!                                         │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Proposition: Resizing Array-prestanda

> **Proposition:** I en resizing array-implementation av stack är den amorterade kostnaden per operation **konstant**.

---

## 📋 Indatamodeller

### Varför Behövs Indatamodeller?

**Problem:** Körtiden kan variera kraftigt beroende på indata.

**Lösning:** Definiera en **modell** för typisk indata.

### Vanliga Indatamodeller

```
┌─────────────────────────────────────────────────────────────────────┐
│              VANLIGA INDATAMODELLER                                │
├──────────────────────────┬──────────────────────────────────────────┤
│  Slumpmässig ordning     │  Alla permutationer lika sannolika      │
│                          │  Bra för sortering                       │
├──────────────────────────┼──────────────────────────────────────────┤
│  Uniform fördelning      │  Alla värden i ett intervall lika       │
│                          │  sannolika (ThreeSum)                    │
├──────────────────────────┼──────────────────────────────────────────┤
│  Markov-modell           │  Sannolikheter beror på tidigare        │
│                          │  element (naturlig text)                 │
├──────────────────────────┼──────────────────────────────────────────┤
│  Empirisk                │  Baserad på verklig data                │
│                          │  (trafikloggar, genomik)                 │
└──────────────────────────┴──────────────────────────────────────────┘
```

### Utmaningar med Indatamodeller

1. **Modellen kan vara orealistisk**
    - Verklig data följer ofta inte enkla fördelningar
2. **Analysen kan vara extremt svår**
    - Kräver avancerad matematisk kompetens

> 💡 **Praktisk lösning:** Kör experiment med verklig data OCH analysera värsta fall.

---

## 🎯 Balans: Två Vanliga Misstag

### Misstag 1: Överdriven Fokus på Prestanda

> "Premature optimization is the root of all evil." – C.A.R. Hoare (upphovsmannen till quicksort)
> 
> Donald Knuth tillade: "(or at least most of it) in programming"

**Varför det är ett problem:**

- Leder till komplicerad, svårförståelig kod
- Tar tid från viktigare uppgifter
- Marginella förbättringar kanske inte märks

**Rekommendation:** Gör koden **klar och korrekt** först!

### Misstag 2: Ignorera Prestanda Helt

**Varför det är ett problem:**

- Brute-force-algoritmer kan ta dagar/månader
- Användare väntar onödigt länge
- Vissa problem blir olösbara

**Rekommendation:** Ha alltid en **uppfattning** om prestanda!

### Den Gyllene Medelvägen

```
┌─────────────────────────────────────────────────────────────────────┐
│              BALANSERAD APPROACH                                   │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  1. Skriv KLAR och KORREKT kod först                               │
│                                                                     │
│  2. Mät prestanda – förstå var tiden går                           │
│                                                                     │
│  3. Optimera BARA om det behövs:                                   │
│     • Körtid är oacceptabel                                        │
│     • Du vet exakt var flaskhalsen är                              │
│     • Förbättringen är betydande                                   │
│                                                                     │
│  4. Ha koll på tillväxtordningen – undvik N² och N³ om möjligt     │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 📊 Sammanfattning: Den Kompletta Analysen

### Den Övergripande Metodiken

```
┌─────────────────────────────────────────────────────────────────────┐
│         KOMPLETT ALGORITMANALYS – SAMMANFATTNING                   │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  1. UTVECKLA EN TILDE-APPROXIMATION                                │
│     → Identifiera den dominerande termen                           │
│                                                                     │
│  2. BESTÄM TILLVÄXTORDNINGEN                                       │
│     → 1, log N, N, N log N, N², N³, 2^N                            │
│                                                                     │
│  3. SKAPA EN MATEMATISK MODELL                                     │
│     → Indatamodell, kostnadsmodell, frekvensanalys                 │
│                                                                     │
│  4. VALIDERA MED EXPERIMENT                                        │
│     → Doubling ratio, mätningar på verklig data                    │
│                                                                     │
│  5. UPPSKATTA MINNESANVÄNDNING                                     │
│     → Objektoverhead, arrayer, länkade strukturer                  │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 🔑 Sammanfattning Del 5

### Minnesanalys

- **Primitiver:** 1-8 bytes beroende på typ
- **Objekt:** 16 bytes overhead + instansvariabler + padding
- **Arrayer:** 24 bytes overhead + data
- **Autoboxning:** Kostsamt! Integer tar 24 bytes vs int:s 4 bytes

### Prestandagarantier

- **Värsta fall:** Absolut garanti, viktig för säkerhetskritiska system
- **Randomiserade:** Probabilistisk garanti, praktiskt lika bra
- **Amorterad:** Genomsnitt över tid, tillåter enstaka dyra operationer

### Praktiska Råd

- Skriv klar kod först, optimera sedan (om nödvändigt)
- Undvik kvadratiska/kubiska algoritmer för stora N
- Använd doubling ratio för att validera
- Var medveten om minnesförbrukning

### Minnesregel: MAPVO

```
M - Minnesanalys (objekt, arrayer, overhead)
A - Amorterad analys (genomsnitt över tid)
P - Prestandagarantier (värsta fall, probabilistisk)
V - Validera med experiment
O - Optimera med omdöme
```

---

# Del 6: Big-O Notation, Ordlista och Avslutande Sammanfattning

---

## 📐 Big-O, Big-Omega och Big-Theta

### Varför Finns Olika Notationer?

Boken använder primärt **tilde-notation** (~), men du kommer stöta på andra notationer:

```
┌─────────────────────────────────────────────────────────────────────┐
│              ASYMPTOTISKA NOTATIONER                               │
├──────────────────────────┬──────────────────────────────────────────┤
│  Notation                │  Betydelse                              │
├──────────────────────────┼──────────────────────────────────────────┤
│  f(N) ~ g(N)             │  f(N)/g(N) → 1 när N → ∞               │
│  (Tilde)                 │  EXAKT asymptotiskt beteende            │
├──────────────────────────┼──────────────────────────────────────────┤
│  f(N) = O(g(N))          │  |f(N)| ≤ c·g(N) för N > N₀            │
│  (Big-O)                 │  ÖVRE GRÄNS                             │
├──────────────────────────┼──────────────────────────────────────────┤
│  f(N) = Ω(g(N))          │  |f(N)| ≥ c·g(N) för N > N₀            │
│  (Big-Omega)             │  UNDRE GRÄNS                            │
├──────────────────────────┼──────────────────────────────────────────┤
│  f(N) = Θ(g(N))          │  f(N) är både O(g(N)) och Ω(g(N))       │
│  (Big-Theta)             │  EXAKT tillväxtordning                  │
└──────────────────────────┴──────────────────────────────────────────┘
```

---

### Big-O: Övre Gräns

**Definition:** f(N) = O(g(N)) om det finns konstanter c och N₀ sådana att |f(N)| ≤ c·g(N) för alla N > N₀.

**Exempel:**

```
3N² + 5N + 7 = O(N²)

Bevis: För N > 10, gäller 3N² + 5N + 7 < 4N²
       Alltså c = 4, N₀ = 10
```

### Varför Big-O Inte Räcker

**Problem:** Big-O ger bara en övre gräns!

```
En algoritm med körtid ~ N log N är OCKSÅ O(N²), O(N³), O(2ᴺ), ...
```

**Konsekvens:** Big-O kan inte användas för att förutsäga prestanda eller jämföra algoritmer!

**Exempel:**

- ThreeSum är O(N³) ✓ (sant)
- ThreeSum är O(2ᴺ) ✓ (också sant, men meningslöst!)

> 📘 **Bokens förhållningssätt:** Vi föredrar tilde-notation eftersom den ger mer precision.

---

### Jämförelse: Tilde vs Big-O

|Aspekt|Tilde (~)|Big-O|
|---|---|---|
|Precision|Exakt asymptotiskt|Endast övre gräns|
|Konstanter|Bevarar ledande konstant|Döljer alla konstanter|
|Praktisk användning|Bra för förutsägelser|Bra för teoretiska bevis|
|Doubling ratio|Kan valideras|Kan inte valideras|

**Bokens rekommendation:**

> "Vi säger 'ThreeSum använder ~N³/2 arrayåtkomster' vilket är mer informativt än 'körtiden för ThreeSum är O(N³)'."

---

## 📚 Ordlista och Termer

### Svenska Termer med Engelska Motsvarigheter

```
┌─────────────────────────────────────────────────────────────────────┐
│              ORDLISTA                                              │
├──────────────────────────┬──────────────────────────────────────────┤
│  Svenska                 │  Engelska                               │
├──────────────────────────┼──────────────────────────────────────────┤
│  Algoritm                │  Algorithm                              │
│  Algoritmanalys          │  Analysis of algorithms                 │
│  Tillväxtordning         │  Order of growth                        │
│  Kostnadsmodell          │  Cost model                             │
│  Inre loop               │  Inner loop                             │
│  Problemstorlek          │  Problem size                           │
│  Tilde-approximation     │  Tilde approximation                    │
│  Ledande term            │  Leading term                           │
│  Frekvenstabell          │  Frequency table                        │
│  Doubling ratio          │  Doubling ratio                         │
│  Värsta fall             │  Worst case                             │
│  Bästa fall              │  Best case                              │
│  Genomsnittlig prestanda │  Average case                           │
│  Amorterad analys        │  Amortized analysis                     │
│  Prestandagaranti        │  Performance guarantee                  │
│  Undre gräns             │  Lower bound                            │
│  Övre gräns              │  Upper bound                            │
│  Brute-force             │  Brute force                            │
│  Dela-och-härska         │  Divide and conquer                     │
│  Linjäritmisk            │  Linearithmic (N log N)                 │
│  Objektoverhead          │  Object overhead                        │
│  Minnesallokering        │  Memory allocation                      │
│  Garbage collection      │  Garbage collection                     │
│  Cachning                │  Caching                                │
└──────────────────────────┴──────────────────────────────────────────┘
```

---

## 🏆 Viktiga Propositioner och Properties

### Sammanfattning av Satser

```
┌─────────────────────────────────────────────────────────────────────┐
│  PROPERTY A: Körtiden för ThreeSum är ~ aN³                        │
│              (experimentellt validerad hypotes)                     │
├─────────────────────────────────────────────────────────────────────┤
│  PROPOSITION B: Brute-force 3-sum använder ~N³/2 arrayåtkomster    │
│                 (matematiskt bevis)                                 │
├─────────────────────────────────────────────────────────────────────┤
│  PROPOSITION C: Om T(N) ~ aN^b lg N, då T(2N)/T(N) ~ 2^b           │
│                 (doubling ratio)                                    │
├─────────────────────────────────────────────────────────────────────┤
│  PROPOSITION D: Länkade list-operationer tar konstant tid          │
│                 i värsta fall                                       │
└─────────────────────────────────────────────────────────────────────┘
```

---

## ❓ Vanliga Frågor (Q&A)

### F: Varför inte använda StdRandom istället för testfiler?

**S:** Det är lättare att felsöka och reproducera experiment med fasta testfiler. StdRandom ger olika värden varje gång, vilket gör debugging svårare.

### F: Min DoublingRatio gav inte stabila resultat. Varför?

**S:** Se avsnittet om "caveats" (fallgropar). Troliga orsaker:

- Garbage collection
- Andra processer på datorn
- JIT-kompilering
- Cache-effekter

**Lösning:** Kör fler experiment och ta medelvärde.

### F: Vad betyder "as N grows" i tilde-definitionen?

**S:** Formellt: lim(N→∞) f(N)/g(N) = 1

### F: Räknas `int[] a = new int[N]` som N arrayåtkomster?

**S:** Troligen ja, eftersom Java initialiserar alla element till 0.

### F: Skillnad mellan O(N log N) och ~N log N i doubling test?

**S:** Båda ger kvot ~2 i doubling test, vilket gör dem svåra att skilja experimentellt. Noggrann analys behövs för att avgöra vilket som gäller.

---

## 📋 Praktiska Övningar och Uppgifter

### Övningar från Boken (Urval)

**1.4.1** Visa att antalet sätt att välja 3 element från N är N(N-1)(N-2)/6.

**1.4.5** Ge tilde-approximationer för:

- N + 1 → ~N
- 1 + 1/N → ~1
- 2N³ - 15N² + N → ~2N³
- lg(N² + 1)/lg N → ~2

**1.4.6** Bestäm tillväxtordningen för:

```java
// (a)
for (int n = N; n > 0; n /= 2)
    for (int i = 0; i < n; i++)
        sum++;
// Svar: ~2N (linjär)

// (b)
for (int i = 1; i < N; i *= 2)
    for (int j = 0; j < i; j++)
        sum++;
// Svar: ~2N (linjär)

// (c)
for (int i = 1; i < N; i *= 2)
    for (int j = 0; j < N; j++)
        sum++;
// Svar: ~N lg N (linjäritmisk)
```

**1.4.8** Skriv ett program som hittar antalet lika par i en fil. Först kvadratiskt, sedan linjäritmiskt med sortering.

**1.4.12** Givet två sorterade arrayer med N element, skriv ut alla gemensamma element i O(N) tid.

---

## 🎯 Komplett Sammanfattning av Avsnitt 1.4

### Huvudbudskap

```
┌─────────────────────────────────────────────────────────────────────┐
│              ALGORITMANALYS – DE TIO BUDORDEN                      │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  1. Använd VETENSKAPLIG METOD för att analysera prestanda          │
│                                                                     │
│  2. Mät KÖRTID med Stopwatch och DoublingTest                      │
│                                                                     │
│  3. Använd LOG-LOG-PLOTTAR för att identifiera potenssamband       │
│                                                                     │
│  4. Utveckla MATEMATISKA MODELLER baserade på kostnadsmodell       │
│                                                                     │
│  5. Fokusera på DEN INRE LOOPEN – den dominerar körtiden           │
│                                                                     │
│  6. Använd TILDE-NOTATION för att förenkla uttryck                 │
│                                                                     │
│  7. Känn till TILLVÄXTORDNINGARNA: 1, log N, N, N log N, N², N³    │
│                                                                     │
│  8. Använd DOUBLING RATIO för att validera hypoteser               │
│                                                                     │
│  9. Designa SNABBARE ALGORITMER med sortering + binärsökning       │
│                                                                     │
│  10. Balansera KORREKTHET och PRESTANDA – optimera med omdöme      │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Nyckelalgoritmer

|Algorithm|Problem|Tid|Förbättring|
|---|---|---|---|
|TwoSum|Räkna par = 0|N²|Baseline|
|TwoSumFast|Räkna par = 0|N log N|~N / log N|
|ThreeSum|Räkna tripplar = 0|N³|Baseline|
|ThreeSumFast|Räkna tripplar = 0|N² log N|~N / log N|

### Viktiga Verktyg

1. **Stopwatch** – Mäter körtid
2. **DoublingTest** – Genererar experimentdata
3. **DoublingRatio** – Beräknar kvoter
4. **Log-log-plottar** – Visualiserar tillväxt

### Minnesregler

```
SHLVF  – Scientific method, Hypothesis, Log-log, Validate, Forecast
TIKOF  – Tilde, Inner loop, Kostnadsmodell, Order of growth, Frekvens
SBBI   – Sortera, Binärsök, Brute-force först, Iterera
DKVP   – Doubling ratio, Kvot, Varningar, Praktiska experiment
MAPVO  – Minnesanalys, Amorterad, Prestandagaranti, Validera, Optimera
```

---

## 🎓 Examenstips

### Vanliga Examensfrågor

1. **Bestäm tillväxtordningen** för given kod med nästlade loopar
2. **Utveckla tilde-approximation** för komplexa uttryck
3. **Analysera körtid** med kostnadsmodell
4. **Designa snabbare algoritm** med sortering/binärsökning
5. **Förutsäg körtid** med doubling ratio
6. **Beräkna minnesanvändning** för datastrukturer

### Snabbguide för Tentasvar

**För att analysera kod:**

1. Identifiera loopar och nästlingsnivå
2. Räkna iterationer för varje loop
3. Multiplicera (nästlade) eller addera (sekventiella)
4. Förenkla med tilde-notation

**För att förbättra algoritm:**

1. Överväg sortering (N log N)
2. Sök med binärsökning (log N)
3. Undvik onödigt arbete
4. Minska antalet nästlade loopar

---

## 📖 Referenser och Vidare Läsning

### I Boken

- **Avsnitt 2.2** – Mergesort (N log N sortering)
- **Avsnitt 2.3** – Quicksort (randomiserad algoritm)
- **Avsnitt 3.1** – Symboltabeller med binärsökning
- **Avsnitt 3.4** – Hashning (amorterad O(1))

### Externa Resurser

- **booksite** – Testfiler och kompletterande material
- **Algoritmer i Java** – Relaterat kursinnehåll
- **The Art of Computer Programming** – Knuths klassiska verk

---

## ✅ Checklista: Har Du Förstått?

- [ ] Kan förklara den vetenskapliga metoden för algoritmanalys
- [ ] Kan använda Stopwatch för att mäta körtid
- [ ] Förstår skillnaden mellan tilde-notation och Big-O
- [ ] Kan identifiera inre loop i kod
- [ ] Kan skapa kostnadsmodell för ett problem
- [ ] Känner till de sju tillväxtklasserna
- [ ] Kan tolka log-log-plottar
- [ ] Förstår och kan utföra doubling ratio-test
- [ ] Kan förbättra brute-force med sortering + binärsökning
- [ ] Förstår amorterad analys
- [ ] Kan uppskatta minnesanvändning för Java-objekt
- [ ] Vet skillnaden mellan Property och Proposition

---

**🎉 Grattis! Du har nu gått igenom hela avsnitt 1.4 om Algoritmanalys!**

---

_Detta material är baserat på "Algorithms, 4th Edition" av Robert Sedgewick och Kevin Wayne._