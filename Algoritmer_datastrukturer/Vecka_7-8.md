# 📚 Undre Gräns, Prioritetskö, Heapsort, Balanserade BST & Intro Grafer
## Komplett Sammanfattning: Avsnitt 2.2 (Prop I & J), 2.4, 3.3, 3.4 (fördjupning), 4.1

**Baserat på:** Sedgewick & Wayne: Algorithms 4th Edition
**Komplement till:** Tidigare sammanfattningar av kap 2.2–2.3 och kap 3.1, 3.2, 3.4

---

# Del 1: Undre Gräns för Jämförelsebaserad Sortering (2.2, Prop I & J)

---

## 🧠 Problemets Komplexitet: Tre Centrala Begrepp

Föreläsningen introducerar ett tankesätt som går *bortom* enskilda algoritmer. Istället för att fråga "hur snabb är *denna* algoritm?" frågar vi: "hur snabbt *kan* sorteringsproblemet lösas?"

**Övre gräns** anger vad vi *kan* uppnå. Den ges av en konkret algoritm — t.ex. mergesort visar att sortering går i ~N lg N jämförelser. Det är som att säga: "Kolla, jag hittade en väg upp på berget som tar 3 timmar, så det går *minst* så snabbt."

**Undre gräns** anger vad som är *omöjligt att slå*. Den måste bevisas för *alla* tänkbara algoritmer, inte bara de vi känner till. Det är som att bevisa att *ingen* väg upp på berget kan ta mindre än 2.5 timmar.

**Optimal algoritm** uppnås när övre och undre gräns möts. Då vet vi att ingen förbättring är möjlig (inom modellen).

---

## 🌳 Beslutsträdsargumentet: Bevis för Proposition I

### Bevisidén i Tre Steg

Vi vill visa att *varje* jämförelsebaserad sorteringsalgoritm måste göra minst ~N lg N jämförelser i värsta fall. Tricket är att modellera *vilken som helst* sådan algoritm som ett binärt beslutsträd.

**Steg 1: Varje algoritm motsvarar ett binärt träd**

Varje jämförelsebaserad algoritm kan beskrivas som en sekvens av ja/nej-frågor: "Är a[i] < a[j]?" Varje sådant beslut grenar till vänster (ja) eller höger (nej). Resultatet är ett binärt träd där:

- Varje **intern nod** representerar en jämförelse (t.ex. "a[0] < a[1]?")
- Varje **löv** representerar en slutgiltig ordning av elementen
- Varje **väg från rot till löv** är den sekvens av jämförelser algoritmen gör för en viss indata

```
                    a[0]:a[1]
                   /          \
              a[1]:a[2]      a[0]:a[2]
             /       \       /       \
          0,1,2   a[0]:a[2] a[1]:a[2]  2,1,0
                  /     \    /     \
               0,2,1  2,0,1 1,0,2  1,2,0
```

**Steg 2: Trädet måste ha minst N! löv**

Det finns N! = N × (N−1) × (N−2) × ... × 1 olika permutationer av N distinkta element. Algoritmen måste kunna skilja mellan *alla* dessa — annars finns en permutation den inte klarar. Alltså krävs minst N! löv.

**Steg 3: Höjden begränsar antalet jämförelser**

Ett binärt träd med höjd h har *högst* 2^h löv (det fullständiga trädet). Kombinerar vi:

```
  2^h ≥ N!          (antal löv ≥ N!)
  
  h ≥ lg(N!)        (ta logaritm av båda sidor)
  
  h ≥ lg(N!) ~ N lg N    (Stirlings approximation)
```

Stirlings formel ger: lg(N!) = lg(1) + lg(2) + ... + lg(N) ~ N lg N

### Proposition I (Bokens formulering)

> **Proposition I:** Ingen jämförelsebaserad sorteringsalgoritm kan garantera att sortera N element med färre än lg(N!) ~ N lg N jämförelser.

**Varför detta är så kraftfullt:** Beviset säger ingenting om *vilken* algoritm vi använder. Det gäller för alla möjliga algoritmer som någon någonsin skulle kunna uppfinna, så länge de baseras på parvis jämförelser. Du kan alltså inte hitta en jämförelsebaserad algoritm som alltid klarar sig med t.ex. 0.5 · N lg N jämförelser.

---

## ✅ Proposition J: Mergesort Är Optimal

> **Proposition J:** Mergesort är en asymptotiskt optimal jämförelsebaserad sorteringsalgoritm.

**Bevis:** Mergesort använder högst ~N lg N jämförelser i värsta fall (Proposition H från kap 2.2). Proposition I säger att varje algoritm behöver minst ~N lg N. Eftersom övre och undre gräns båda är ~N lg N, är mergesort optimal.

### Begränsningar i Optimaliteten

Boken betonar att Proposition J *inte* betyder att mergesort är det bästa valet i alla situationer:

```
┌─────────────────────────────────────────────────────────────────────┐
│  VARFÖR MERGESORTS OPTIMALITET HAR BEGRÄNSNINGAR                   │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  1. Mergesort är INTE optimal avseende minnesanvändning             │
│     (kräver O(N) extra utrymme)                                    │
│                                                                     │
│  2. Värsta fallet kanske sällan inträffar i praktiken              │
│     (quicksort slår mergesort i snitt)                              │
│                                                                     │
│  3. Andra operationer (array-åtkomster) kan dominera               │
│     (heapsort har dåligt cache-beteende)                            │
│                                                                     │
│  4. Man kan sortera UTAN jämförelser!                               │
│     (radix sort, bucket sort — O(N) med begränsade nycklar)         │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Sorteringsalgoritmer i Perspektiv (från föreläsningen)

Föreläsningen kategoriserar algoritmer efter *strukturen* på deras arbete:

- **Linjärt arbete × N gånger → O(N²):** selection sort, insertion sort
- **Linjärt arbete × lg N gånger → O(N lg N):** mergesort, quicksort
- **Logaritmiskt arbete × N gånger → O(N lg N):** heapsort
- **Linjärt arbete × konstant antal gånger → O(N):** bucket sort, radix sort (ej jämförelsebaserade)

> 🔑 **Nyckelinsikt från föreläsningen:** Om man tillåter *alla* CPU-operationer (inte bara jämförelser) finns det algoritmer som slår N lg N! Arne Andersson (svensk forskare) har visat en garanterad O(N log log N)-algoritm, och Mikkel Thorup visade förväntad O(N √(log log N)).

---

# Del 2: Prioritetskö och Binär Heap (Avsnitt 2.4)

---

## 🎯 Varför Behövs Prioritetsköer?

En prioritetskö är en abstrakt datastruktur som löser ett fundamentalt problem: **hur hanterar vi en dynamisk samling där vi ständigt vill ta ut det viktigaste (största/minsta) elementet?**

Tänk på det så här: en vanlig kö ger dig det *äldsta* elementet, en stack ger dig det *nyaste*. Men ibland vill du det *viktigaste* — och vad som är "viktigast" kan förändras allteftersom nya element tillkommer.

**Praktiska tillämpningar:**

- **Operativsystem:** Processer med högst prioritet körs först
- **Händelsesimulering:** Nästa händelse i tidsordning
- **Grafalgoritmer:** Dijkstras kortaste väg, Prims MST (kapitel 4)
- **Datakomprimering:** Huffman-kodning (kapitel 5)
- **TopM-problemet:** Hitta de M största bland en ström av N element (N kan vara enormt)

### API: MaxPQ

```java
public class MaxPQ<Key extends Comparable<Key>>
    MaxPQ()                // Skapa tom prioritetskö
    MaxPQ(int maxN)        // Skapa med initial kapacitet
    void insert(Key v)     // Sätt in element
    Key max()              // Returnera största
    Key delMax()           // Ta bort och returnera största
    boolean isEmpty()      // Är kön tom?
    int size()             // Antal element
```

> 💡 **MinPQ** fungerar identiskt men med omvända jämförelser — bara att vända `less()` till `greater()`.

---

## 📊 Elementära Implementationer och Deras Brister

Innan vi kommer till heap-lösningen, låt oss förstå *varför* den behövs genom att se vad som händer med naiva lösningar:

**Osorterad array** (lat approach — skjut upp arbetet):
```java
// insert(): O(1) — bara lägg till sist
pq[N++] = x;

// delMax(): O(N) — måste skanna hela arrayen
int max = 0;
for (int i = 1; i < N; i++)
    if (less(max, i)) max = i;
exch(max, N-1);
return pq[--N];
```

**Sorterad array** (ivrig approach — gör arbetet direkt):
- `insert()`: O(N) — måste skifta element för att hålla ordning
- `delMax()`: O(1) — ta sista elementet

**BST** fungerar men: trädets höjd kan bli linjär utan balansering, och BST kan söka *vilken* nyckel som helst — vi behöver bara den största. Det finns en enklare och billigare struktur för just detta!

```
┌─────────────────────────────────────────────────────────────────────┐
│  PRESTANDAJÄMFÖRELSE FÖR PRIORITETSKÖER                             │
├──────────────────────┬──────────────┬──────────────────────────────┤
│  Implementation       │  insert()    │  delMax()                    │
├──────────────────────┼──────────────┼──────────────────────────────┤
│  Osorterad array      │  O(1)        │  O(N)                       │
│  Sorterad array       │  O(N)        │  O(1)                       │
│  Binär heap           │  O(lg N)     │  O(lg N)                    │
│  (Omöjlig) drömmen    │  O(1)        │  O(1)                       │
└──────────────────────┴──────────────┴──────────────────────────────┘
```

---

## 🏗️ Heap-ordnat Komplett Binärträd

### Två Nyckelidéer

**Idé 1: Heap-ordning** — Varje nod har en nyckel som är ≥ nycklarna hos båda barnen. Det betyder att roten *alltid* innehåller det största elementet.

> **Proposition O:** Det största elementet i ett heap-ordnat binärträd finns i roten.

**Idé 2: Komplett binärträd** — Trädet är fyllt nivå för nivå, uppifrån och ner, vänster till höger. Den enda nivån som kan vara ofullständig är den sista.

Kombinationen gör att vi kan representera trädet *utan pekare*, bara som en array!

### Array-representation: Elegant Aritmetik

Istället för att lagra vänster/höger-pekare i varje nod, lägger vi noderna i en array i **nivåordning** (level order). Position 1 är roten, position 0 lämnas tom:

```
  Index:    0   1   2   3   4   5   6   7   8   9  10  11
  Array:    -   T   S   R   P   N   O   A   E   I   H   G

  Trädvy:
                         T (1)
                       /      \
                   S (2)       R (3)
                  /    \      /    \
              P (4)  N (5) O (6)  A (7)
             / \    / \
          E(8) I(9) H(10) G(11)
```

**Navigering utan pekare:**

| Operation | Formel | Exempel (från nod k=3, "R") |
|---|---|---|
| Förälder till k | ⌊k/2⌋ | ⌊3/2⌋ = 1 → "T" |
| Vänster barn till k | 2k | 2×3 = 6 → "O" |
| Höger barn till k | 2k + 1 | 2×3+1 = 7 → "A" |

> **Proposition P:** Höjden på ett komplett binärträd med N noder är ⌊lg N⌋.

Detta är nyckeln till logaritmisk prestanda — vi behöver aldrig gå längre än ~lg N steg.

---

## ⬆️⬇️ Swim och Sink: Heap-ordningens Väktare

Alla heap-operationer bygger på två primitiver som reparerar heap-ordningen när den bryts. Tänk på dem som "gravitationskrafter" i trädet.

### Swim (Bottom-up reheapify)

**När:** En nod har *större* nyckel än sin förälder (bryter heap-ordningen "underifrån").
**Strategi:** Byt med föräldern, upprepa tills ordningen gäller.

```java
private void swim(int k) {
    while (k > 1 && less(k/2, k)) {  // Medan föräldern är mindre
        exch(k, k/2);                 // Byt med förälder
        k = k/2;                      // Gå uppåt
    }
}
```

**Visualisering — "S" simmar upp:**
```
  FÖRE:                    EFTER:
       S                        T
      / \                      / \
     P    R          →        S    R
    / \                      / \
   G   T ← bryter!         G   P
       (T > P)
```

**Tid:** O(lg N) — högst höjden av trädet.

### Sink (Top-down reheapify)

**När:** En nod har *mindre* nyckel än något av sina barn (bryter heap-ordningen "ovanifrån").
**Strategi:** Byt med det *större* barnet, upprepa nedåt.

```java
private void sink(int k) {
    while (2*k <= N) {                    // Medan noden har barn
        int j = 2*k;                      // Vänster barn
        if (j < N && less(j, j+1)) j++;   // Välj det STÖRRE barnet
        if (!less(k, j)) break;           // Ordningen ok? Sluta
        exch(k, j);                        // Byt med större barnet
        k = j;                            // Gå nedåt
    }
}
```

**Varför byta med det *större* barnet?** Om vi byter med det mindre, kan det nya barnets nyckel fortfarande vara mindre än det andra barnet — och heap-ordningen skulle brytas där istället!

**Visualisering — "H" sjunker ner:**
```
  FÖRE:                     EFTER sink(2):
       T                          T
      / \                        / \
     H    R         →           S    R
    / \                        / \
   P   S ← S > H!            P   N
  / \  / \                   / \  / \
 E  I N  G                 E  I H  G
```

**Tid:** O(lg N) — högst höjden av trädet. Varje nivå kräver 2 jämförelser (en för att hitta det större barnet, en för att jämföra med noden).

---

## 🔧 Insert och DelMax: Heapens Huvudoperationer

### Insert: Lägg till sist och simma upp

```java
public void insert(Key x) {
    pq[++N] = x;    // Lägg till längst ner till höger (sista positionen)
    swim(N);         // Låt elementet simma upp till rätt position
}
```

**Steg-för-steg:**
1. Öka N, placera det nya elementet på position N
2. Det kan bryta heap-ordningen (vara större än sin förälder)
3. Anropa `swim()` för att fixa — elementet bubblar uppåt tills det hamnar rätt

**Tid:** Högst 1 + lg N jämförelser (Proposition Q).

### DelMax: Byt toppen med botten, sjunk ner

```java
public Key delMax() {
    Key max = pq[1];       // Spara det största (roten)
    exch(1, N--);          // Byt rot med sista elementet, minska storlek
    sink(1);               // Det (sannolikt lilla) elementet sjunker till rätt plats
    pq[N+1] = null;        // Undvik minnesläckage (loitering)
    return max;
}
```

**Steg-för-steg:**
1. Roten (position 1) är alltid max — spara den
2. Flytta det sista elementet (längst ner till höger) till roten
3. Minska N
4. Det nya rotelementet är sannolikt för litet → `sink()` fixar det
5. Nolla den gamla positionen så att garbage collector kan frigöra minnet

**Tid:** Högst 2 lg N jämförelser (Proposition Q) — `sink()` gör 2 jämförelser per nivå.

### Proposition Q (formellt)

> **Proposition Q:** I en prioritetskö med N nycklar kräver heap-algoritmerna högst 1 + lg N jämförelser för `insert` och högst 2 lg N jämförelser för `remove the maximum`.

---

## 🏠 Heapkonstruktion: Bygg en Heap i Linjär Tid!

Man kan bygga en heap genom att upprepa `insert()` N gånger → O(N lg N). Men det finns ett bättre sätt!

### Bottom-up Konstruktion med Sink

**Idén:** Fyll arrayen med elementen i godtycklig ordning. Kör sedan `sink()` på alla icke-löv-noder, nerifrån och upp:

```java
for (int k = N/2; k >= 1; k--)
    sink(a, k, N);
```

**Varför börja vid N/2?** Noderna N/2+1 till N är alla löv (de har inga barn). Ett löv är automatiskt en korrekt heap av storlek 1 — inget arbete behövs.

**Varför nerifrån och upp?** När vi kör `sink(k)` har barnen till k *redan* fixats (de har lägre index). Så `sink()` utgår från att subträden redan är korrekta heapar.

### Proposition R: Linjär Tid

> **Proposition R:** Sink-baserad heapkonstruktion använder färre än 2N jämförelser och färre än N byten.

**Bevisidé (från föreläsningen):**

Nyckeln är att *de flesta noder sitter nära botten* och behöver bara sjunka en kort sträcka:

```
  Djup h (löv):     N/2 noder, 0 jämförelser (skippar dem)
  Djup h-1:         N/4 noder, högst 2 jämförelser var
  Djup h-2:         N/8 noder, högst 4 jämförelser var
  Djup h-3:         N/16 noder, högst 6 jämförelser var
  ...
  Djup h-k:         N/2^(k+1) noder, högst 2k jämförelser var
```

Totalt antal jämförelser ≤ N·(2/4 + 4/8 + 6/16 + 8/32 + ...) = N · Σ(2k/2^(k+1)) = **2N**

Serien konvergerar (WolframAlpha bekräftar Σ k·2^(-k) = 2), så hela konstruktionen kostar ~2N jämförelser. Det är *linjärt* — mycket bättre än O(N lg N)!

> 🎯 **Intuition:** Hälften av noderna gör 0 arbete, en fjärdedel gör ~2, en åttondel gör ~4... Det totala arbetet domineras av de många enkla fallen nära botten.

---

## 📈 Heapsort (Algoritm 2.7): Sortering med Heap

Heapsort kombinerar heapkonstruktion med upprepade `delMax()` till en elegant in-place sorteringsalgoritm.

### Två Faser

**Fas 1: Heapkonstruktion** — Omorganisera arrayen till en max-heap.
**Fas 2: Sortdown** — Plocka ut det största elementet ur heapen, placera det i sin slutliga position.

```java
public static void sort(Comparable[] a) {
    int N = a.length;
    
    // Fas 1: Bygg heap (nerifrån och upp)
    for (int k = N/2; k >= 1; k--)
        sink(a, k, N);
    
    // Fas 2: Sortdown (upprepad delMax)
    while (N > 1) {
        exch(a, 1, N--);   // Byt rot (max) med sista elementet
        sink(a, 1, N);     // Reparera heapen
    }
}
```

### Detaljerad Spårning

```
  Indata:     S O R T E X A M P L E

  FAS 1 — Heapkonstruktion (sink-baserad):
  
  k=5: sink(5,11)  →  S O R T L X A M P E E
  k=4: sink(4,11)  →  S O R T L X A M P E E   (ingen förändring)
  k=3: sink(3,11)  →  S O X T L R A M P E E
  k=2: sink(2,11)  →  S T X P L R A M O E E
  k=1: sink(1,11)  →  X T S P L R A M O E E   ← heap-ordnad!

  FAS 2 — Sortdown:
  
  exch(1,11), sink(1,10) →  T P S O L R A M E E | X
  exch(1,10), sink(1,9)  →  S P R O L E A M E | T X
  exch(1,9),  sink(1,8)  →  R P E O L E A M | S T X
  ...                     →  ...
  Slutresultat:              A E E L M O P R S T X ← sorterat!
```

**Vad händer i varje steg av sortdown?**
1. `exch(1, N--)`: Det största elementet (roten) byter plats med det sista osorterade. Det hamnar i sin slutgiltiga, korrekta position.
2. `sink(1, N)`: Heapen har krympt med ett element. Det element som flyttades till roten "sjunker" ner till rätt plats.

### Proposition S: Heapsorts Prestanda

> **Proposition S:** Heapsort använder färre än 2N lg N + 2N jämförelser (och hälften så många byten).

Bevis: 2N för heapkonstruktionen (Prop R) + 2 lg N per delMax × N element = 2N lg N.

### Heapsort i det Stora Perspektivet

```
┌─────────────────────────────────────────────────────────────────────┐
│  HEAPSORT: UNIK POSITION BLAND SORTERINGSALGORITMER                 │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ✅ Garanterad O(N lg N) — ingen dålig indata kan göra det värre    │
│  ✅ In-place — O(1) extra minne (bara ett par temporära variabler) │
│  ✅ Enda algoritmen som är optimal i BÅDE tid OCH minne!           │
│                                                                     │
│  ❌ Inte stabil (ändrar ordning för element med lika nycklar)       │
│  ❌ Dåligt cache-beteende (jämförelser hoppar runt i arrayen)      │
│  ❌ Långsammare inre loop än quicksort i praktiken                 │
│                                                                     │
│  ANVÄNDNING: Inbäddade system och realtidssystem där                │
│  minnesgaranti och tidsgaranti är viktigare än råhastighet         │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Floyds Optimering (frivillig fördjupning)

Floyd observerade 1964 att de flesta element som sätts in vid roten under sortdown sjunker *hela vägen ner* till botten. Hans idé: sjunk noden ända till botten utan att kontrollera om den nått rätt plats, och simma sedan upp från botten. Detta halverar antalet jämförelser asymptotiskt (nära mergesorts nivå), men kräver mer bokföring och lönar sig främst när jämförelser är dyra (t.ex. långa strängar).

---

## 🎯 Sammanfattning: Sorteringsalgoritmer — Komplett Översikt

Nu när vi har sett *alla* jämförelsebaserade sorteringsalgoritmer kan vi sammanfatta:

```
┌───────────────────────────────────────────────────────────────────────────┐
│  KOMPLETT SORTERINGSTABELL                                                │
├──────────────┬──────────┬──────────┬─────────┬────────┬────────┬────────┤
│  Algoritm     │Bästa fall│Genomsnitt│Värsta   │Minne   │Stabil? │In-place│
├──────────────┼──────────┼──────────┼─────────┼────────┼────────┼────────┤
│Selection sort │ ½N²     │ ½N²     │ ½N²     │ O(1)   │ Nej    │ Ja     │
│Insertion sort │ N       │ ¼N²     │ ½N²     │ O(1)   │ Ja     │ Ja     │
│Shellsort     │ N       │ ?       │ ?       │ O(1)   │ Nej    │ Ja     │
│Mergesort     │ ½NlgN   │ NlgN    │ NlgN    │ O(N)   │ Ja     │ Nej    │
│Quicksort     │ NlgN    │ 1.39NlgN│ ½N²     │ O(lgN) │ Nej    │ Ja     │
│3-way QS      │ N       │ 1.39NlgN│ ½N²     │ O(lgN) │ Nej    │ Ja     │
│Heapsort      │ NlgN    │ 2NlgN   │ 2NlgN   │ O(1)   │ Nej    │ Ja     │
├──────────────┴──────────┴──────────┴─────────┴────────┴────────┴────────┤
│  Undre gräns (alla jämförelsebaserade): ~ N lg N                        │
└─────────────────────────────────────────────────────────────────────────┘
```

---

# Del 3: Balanserade Sökträd — 2-3-träd och Röd-Svarta BST (Avsnitt 3.3)

---

## 🎯 Problemet: Varför Vanliga BST Inte Räcker

I den tidigare sammanfattningen (kap 3.2) såg vi att BST ger utmärkt *genomsnittlig* prestanda (~1.39 lg N jämförelser). Men i *värsta fall* — t.ex. om nycklar sätts in i sorterad ordning — degenererar trädet till en länkad lista med N höjd.

**Exempel: Insättning av A, B, C, D, E i ordning**
```
  A
   \
    B
     \
      C
       \
        D
         \
          E    ← höjd = N-1, alla operationer O(N)!
```

Vi vill ha **garanterad logaritmisk prestanda** oavsett insättningsordning.

---

## 🌳 2-3-Träd: Den Konceptuella Grunden

### Definition

Ett **2-3-träd** är antingen tomt eller ett träd som har två typer av noder:

**2-nod:** En nyckel, två barn-länkar (precis som vanlig BST-nod)
```
    [K]
   /   \
 <K     >K
```

**3-nod:** Två nycklar, tre barn-länkar
```
    [E  K]
   /   |   \
 <E  E..K   >K
```

**Avgörande egenskap:** Alla null-länkar (löv) befinner sig på **samma djup**. Trädet har alltså *perfekt balans*.

### Sökning i 2-3-Träd

Sökning fungerar som i BST, men med fler jämförelser per nod:

**I en 2-nod:** Jämför med nyckeln, gå vänster eller höger.
**I en 3-nod:** Jämför med *båda* nycklarna — gå till vänster, mitten eller höger barn.

### Insättning i 2-3-Träd: Lokala Transformationer

Nyckelprincipen: vi sätter aldrig in en nod som ett nytt löv (som i BST). Istället *absorberar* vi nyckeln i en befintlig nod vid botten.

**Fall 1: Insättning i en 2-nod → blir en 3-nod**

Det finns plats! Bara lägg till nyckeln.
```
  Sök ner till [K], vill sätta in L:
  
  [K] → [K L]     (2-nod blir 3-nod)
```

**Fall 2: Insättning i en 3-nod → temporär 4-nod → split**

Det finns *inte* plats. Vi skapar en temporär 4-nod och *splittar* den:

```
  Sök ner till [E K], vill sätta in H:
  
  1. [E K] + H → [E H K]   (temporär 4-nod)
  
  2. Splitta: mittnyckel (H) skickas UPPÅT till föräldern
  
     [H]
    /   \
  [E]   [K]     (tre 2-noder)
```

Om föräldern *också* var en 3-nod, upprepas processen uppåt. I värsta fall bubblar en split hela vägen upp till roten. Om roten splittas, skapas en ny rot och **trädhöjden ökar med exakt 1**.

> 🎯 **Fundamental insikt:** 2-3-träd *växer uppåt* (från roten), inte nedåt som BST! Det är därför balansen bevaras — alla löv påverkas lika mycket av en ny nivå.

### Höjdgaranti

> **Proposition (3.3.4):** Höjden på ett 2-3-träd med N nycklar är mellan ⌊log₃ N⌋ ≈ 0.63 lg N (alla 3-noder) och ⌊lg N⌋ (alla 2-noder).

Även i värsta fall är höjden logaritmisk!

---

## 🔴⚫ Röd-Svarta BST: 2-3-Träd i BST-förklädnad

### Varför Inte Implementera 2-3-Träd Direkt?

Direkt implementation av 2-3-träd kräver:
- Två olika nodtyper (2-noder och 3-noder)
- Komplicerad kod för att konvertera mellan dem
- Många specialfall

En röd-svart BST **kodar 2-3-trädets struktur** i ett vanligt BST genom att använda länkfärger istället.

### Kodning av 3-Noder

En **3-nod** med nycklar (a, b) representeras som *två 2-noder* förbundna av en **röd länk** som lutar åt vänster:

```
  3-nod [a  b]          Röd-svart representation:
     /   |   \    
   <a  a..b   >b            b          ("b" är den övre noden)
                           / \
                     röd→ a   >b       ("a" förbunden med röd länk)
                         / \
                       <a  a..b
```

### Tre Definierande Regler

1. **Röda länkar lutar åt vänster** — den mindre nyckeln i en 3-nod är alltid vänster barn
2. **Ingen nod har två röda länkar kopplade till sig** — (det skulle motsvara en 4-nod, som inte tillåts i ett 2-3-träd)
3. **Perfekt svart balans** — varje väg från rot till null-länk har *exakt samma* antal svarta länkar

### 1-1 Korrespondens: Visualisering

Om du ritar röda länkar horisontellt i en röd-svart BST, och sedan "kollapsar" par förbundna av röda länkar, får du exakt motsvarande 2-3-träd:

```
  Röd-svart BST:                   Motsvarande 2-3-träd:
  
       M (svart)                         [E  M]
      / \                               /  |   \
    E    R (svart)                    [A C] [H] [R S]
   /↗\    / \
  A   H  P   S                  (↗ markerar röd länk)
 / \
C
```

### Färgrepresentation i Koden

```java
private static final boolean RED   = true;
private static final boolean BLACK = false;

private class Node {
    Key key;
    Value val;
    Node left, right;
    int N;           // Antal noder i subträdet
    boolean color;   // Färg på länken FRÅN föräldern
}

private boolean isRed(Node x) {
    if (x == null) return false;  // Null-länkar är svarta
    return x.color == RED;
}
```

---

## 🔄 Rotationer och Färgflippar: Verktygen

Tre operationer räcker för att implementera alla balanserings-transformationer:

### Vänsterrotation (rotateLeft)

Rätar upp en *högerlutnande* röd länk:

```
  FÖRE:                        EFTER:
     E                            S
      \↗                        ↗/
       S          →            E
      / \                     / \
    E-S  >S                 <E  E-S
```

```java
private Node rotateLeft(Node h) {
    Node x = h.right;
    h.right = x.left;
    x.left = h;
    x.color = h.color;    // Ärv förälderns länkfärg
    h.color = RED;         // h blir röd (del av ny 3-nod)
    x.N = h.N;
    h.N = 1 + size(h.left) + size(h.right);
    return x;
}
```

### Högerrotation (rotateRight)

Rätar upp en situation med *två konsekutiva vänsterlutnande* röda länkar:

```
  FÖRE:                        EFTER:
       S                         E
      ↗/                          \↗
     E            →                S
    / \                           / \
  <E  E-S                      E-S  >S
```

### Färgflipp (flipColors)

Splittar en nod vars *båda* barn har röda länkar (= temporär 4-nod):

```
  FÖRE (4-nod):               EFTER (split):
       E (svart)                   E (röd ↑ skickas till förälder)
      ↗/ \↗                       / \
     A    S    →                  A    S
   (röd) (röd)                (svart) (svart)
```

```java
private void flipColors(Node h) {
    h.color = RED;              // Skicka mittnyckeln uppåt (röd)
    h.left.color = BLACK;       // Barnen blir svarta
    h.right.color = BLACK;
}
```

---

## 🧩 Put-operationen: Allt Faller på Plats

Den eleganta insikten: bara *tre* `if`-satser efter de rekursiva anropen balanserar hela trädet!

```java
private Node put(Node h, Key key, Value val) {
    if (h == null)  // Ny nod med röd länk till föräldern
        return new Node(key, val, 1, RED);
    
    // Standard BST-insättning
    int cmp = key.compareTo(h.key);
    if      (cmp < 0) h.left  = put(h.left,  key, val);
    else if (cmp > 0) h.right = put(h.right, key, val);
    else              h.val = val;  // Uppdatera värdet
    
    // ── Balanseringsfix (3 rader!) ──
    if (isRed(h.right) && !isRed(h.left))     h = rotateLeft(h);
    if (isRed(h.left) && isRed(h.left.left))  h = rotateRight(h);
    if (isRed(h.left) && isRed(h.right))      flipColors(h);
    
    h.N = 1 + size(h.left) + size(h.right);
    return h;
}
```

**De tre fixerna i ordning:**

| Steg | Villkor | Åtgärd | Syfte |
|------|---------|--------|-------|
| 1 | Högerlutnande röd länk | `rotateLeft` | Rätta till "fel" lutning |
| 2 | Två konsekutiva vänsterröda | `rotateRight` | Temporär 4-nod → balansera |
| 3 | Båda barnen röda | `flipColors` | Splitta 4-nod, skicka nyckel uppåt |

> 🎯 **Nyckelpunkt:** `get()` i en röd-svart BST är **exakt samma** som i en vanlig BST. Färgerna spelar ingen roll vid sökning — de behövs bara vid insättning (och borttagning).

---

## 📊 Analys av Röd-Svarta BST

### Proposition G: Höjdgaranti

> **Proposition G:** Höjden på en röd-svart BST med N noder är högst 2 lg N.

**Bevis (skiss):** Värsta fallet är ett 2-3-träd bestående av bara 2-noder *utom* längs en väg som har 3-noder. Den längsta vägen (med 3-noder) har dubbelt så många BST-noder som den kortaste (bara 2-noder), vars längd är ~lg N. Alltså ≤ 2 lg N.

### Property H: Typisk Prestanda

> **Property H:** Den genomsnittliga väglängden till en nod i en röd-svart BST med N noder är ~1.00 lg N.

I praktiken beter sig röd-svarta BST nästan som perfekt balanserade träd! Jämfört med vanliga BST (1.39 lg N) är detta ~28% färre jämförelser per sökning.

### Proposition I (bokens 3.3): Logaritmisk Garanti för Allt

> **Proposition I:** I en röd-svart BST tar sökning, insättning, min/max, floor/ceiling, rank, select, delete min/max, delete, och range count alla **logaritmisk tid** i värsta fall.

**Bevis:** Alla operationer gör arbete proportionellt mot trädets höjd, som är ≤ 2 lg N (Prop G).

### Uppdaterad Symboltabell-kostnadsöversikt

```
┌───────────────────────────────────────────────────────────────────────────┐
│  SYMBOLTABELLER: FULLSTÄNDIG KOSTNADSÖVERSIKT                            │
├──────────────────────┬────────────┬──────────────┬───────────┬──────────┤
│                       │ Värsta fall│  Genomsnitt  │ Genomsnitt│  Ordnade │
│  Implementation       │  sökning   │  sökning     │ insättning│  op.?    │
├──────────────────────┼────────────┼──────────────┼───────────┼──────────┤
│  Sekventiell sökning  │     N      │    N/2       │     N     │   Nej    │
│  (osorterad lista)    │            │              │           │          │
├──────────────────────┼────────────┼──────────────┼───────────┼──────────┤
│  Binärsökning         │   lg N     │    lg N      │    N      │   Ja     │
│  (ordnad array)       │            │              │           │          │
├──────────────────────┼────────────┼──────────────┼───────────┼──────────┤
│  BST                  │     N      │  1.39 lg N   │ 1.39 lg N │   Ja     │
├──────────────────────┼────────────┼──────────────┼───────────┼──────────┤
│  Röd-svart BST        │  2 lg N    │  1.00 lg N   │ 1.00 lg N │   Ja     │
├──────────────────────┼────────────┼──────────────┼───────────┼──────────┤
│  Separate chaining    │    N       │    N/(2M)    │   N/M     │   Nej    │
├──────────────────────┼────────────┼──────────────┼───────────┼──────────┤
│  Linear probing       │    N       │    ~1.5      │   ~2.5    │   Nej    │
│  (α=0.5)              │            │              │           │          │
└──────────────────────┴────────────┴──────────────┴───────────┴──────────┘
```

### Borttagning i Röd-Svarta BST (koncept)

Borttagning är den mest komplicerade operationen. Grundidén (utan full implementation):

1. Vid **deleteMin**: Gå nedåt längs vänsterlänkarna. Innan vi går ner, säkerställ att den aktuella noden *inte* är en 2-nod (annars kan vi inte ta bort från den). Vi skapar temporära 4-noder på vägen ner genom att "låna" nycklar från syskon.
2. Vid botten finns en 3-nod eller 4-nod, varifrån vi kan ta bort minsta nyckeln utan problem.
3. På vägen upp splittar vi eventuella kvarvarande 4-noder (precis som vid insättning).

> 💡 **Delete** (godtycklig nyckel) använder samma teknik: om nyckeln är vid botten, ta bort direkt. Om den är intern, ersätt med efterföljaren (som i vanlig BST-delete), och gör sedan deleteMin i högersubträdet.

---

# Del 4: Hashtabeller — Fördjupning (Avsnitt 3.4)

---

Den tidigare sammanfattningen täckte grunderna om separate chaining, linear probing, hashfunktioner, load factor och propositioner K och M. Här fördjupar vi med **designmönster, praktiska överväganden, och avancerade aspekter** som inte täcktes.

## 🔬 Hashtabell vs Balanserat BST: En Djupare Jämförelse

I den tidigare sammanfattningen listade vi *när* man ska använda vilken. Här utforskar vi *varför* mer djupgående:

### Hashtabellens Fundamentala Antagande

Hashtabellens O(1)-prestanda vilar på **Antagande J** (uniform hashing assumption): att hashfunktionen sprider nycklarna jämnt över alla positioner. I verkligheten är detta aldrig *exakt* sant, men bra hashfunktioner approximerar det väl.

Om antagandet *inte* gäller (dålig hashfunktion), kan alla nycklar hamna i samma hink → O(N) per operation. Det är samma problematik som osorterad BST! Skillnaden är att en röd-svart BST *garanterar* lg N oavsett input, medan en hashtabell förlitar sig på hashfunktionens kvalitet.

### Ordnade Operationer: Hashtabellens Akilleshäl

Hashtabeller kastar bort nyckelordningen vid hashning. Det gör följande operationer **omöjliga** (eller kräver O(N)):

- `min()`, `max()` — måste skanna allt
- `floor(key)`, `ceiling(key)` — kräver ordning
- `rank(key)`, `select(k)` — kräver ordning
- `keys(lo, hi)` (range query) — kräver ordning

> 🎯 **Tumregel (uppdaterad):**
> - Behöver du ordnade operationer? → **Röd-svart BST** (eller annat balanserat träd)
> - Behöver du *bara* sökning/insättning/borttagning och vill ha snabbast möjligt? → **Hashtabell**
> - Osäker? → Börja med röd-svart BST (Java: `TreeMap`) — det fungerar alltid bra

### Javas Inbyggda Val

Java använder faktiskt båda:
- `HashMap`: Hashtabell (separate chaining). Snabbast för de flesta fall.
- `TreeMap`: Röd-svart BST. Stödjer ordnade operationer.
- Javas `Arrays.sort()`: Använder mergesort för objekt (stabil), quicksort (dual-pivot) för primitiver.

---

## 🔑 Hashfunktioner: Praktiska Detaljer

### Konsistenskravet

Om `a.equals(b)` är sant, **måste** `a.hashCode() == b.hashCode()`. Annars bryts hashtabellen! (Men det omvända gäller inte: samma hashkod *kan* ge sig för olika objekt — det är en kollision.)

### Varför `(key.hashCode() & 0x7fffffff) % M`?

```java
private int hash(Key key) {
    return (key.hashCode() & 0x7fffffff) % M;
}
```

- `hashCode()` returnerar en `int` (kan vara negativ!)
- `& 0x7fffffff` maskar bort teckenbiten → garanterat icke-negativt
- `% M` mappar till index 0..M-1

### Bra vs Dåliga Hashfunktioner

En bra hashfunktion:
1. Är **deterministisk** (samma input → samma output)
2. Använder **alla delar** av nyckeln
3. **Sprider jämnt** över hashtabellen

En dålig hashfunktion: t.ex. bara första tecknet i en sträng → alla strängar som börjar med 'A' kolliderar.

---

# Del 5: Introduktion till Grafer (Avsnitt 4.1)

---

## 🌐 Vad Är en Graf?

En **graf** är en samling **hörn** (vertices) förbundna med **kanter** (edges). Grafer modellerar *relationer* och *kopplingar* — och dyker upp överallt:

```
┌─────────────────────────────────────────────────────────────────────┐
│  GRAFER I VERKLIGHETEN                                               │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  Tillämpning        │  Hörn            │  Kanter                   │
│  ───────────────────┼──────────────────┼──────────────────────────  │
│  Socialt nätverk    │  Användare       │  Vänskapsrelationer       │
│  Internet           │  Routrar         │  Fysiska anslutningar     │
│  Karta/GPS          │  Korsningar      │  Vägar                    │
│  Schemaläggning     │  Uppgifter       │  Beroenden                │
│  Elektrisk krets    │  Komponenter     │  Ledningar                │
│  Biologi            │  Arter           │  Interaktioner            │
│  Kompilatorer       │  Funktioner      │  Funktionsanrop           │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 📖 Grundläggande Terminologi

**Graf G = (V, E):** V = mängden hörn, E = mängden kanter.

**Grannskap (adjacency):** Två hörn är *grannar* om de förbinds av en kant.

**Grad (degree):** Antalet kanter som ansluter till ett hörn.

**Väg (path):** En sekvens av hörn förbundna av kanter. En *enkel* väg besöker inget hörn mer än en gång.

**Cykel:** En väg som börjar och slutar i samma hörn.

**Sammanhängande (connected):** Det finns en väg mellan varje par av hörn.

**Sammanhängande komponent (connected component):** En maximal sammanhängande delgraf.

**Acyklisk (acyclic):** En graf utan cykler. Ett acykliskt sammanhängande grafrum kallas **träd**.

**Skog (forest):** En acyklisk graf (kan ha flera komponenter, vardera ett träd).

```
  Exempelgraf (tinyG.txt):
  
  0 — 6          7 — 8        9 — 10
  |   |                       |  \
  1   4 — 5                  11 — 12
  |   |   |
  2   3 — 5
  
  13 hörn, 13 kanter
  3 sammanhängande komponenter: {0,1,2,3,4,5,6}, {7,8}, {9,10,11,12}
```

**Nyckeltal:**
- **Gles graf (sparse):** E ~ V (vanligast i praktiken)
- **Tät graf (dense):** E ~ V² (alla par förbundna)
- **Träd med V hörn:** Har exakt V-1 kanter

---

## 💾 Grafrepresentation: Adjacency Lists

Tre alternativ finns, men boken (och vi) använder **adjacenslista** (adjacency list):

### Tre Möjliga Representationer

| Representation | Plats | Lägg till kant | Kolla om v-w kant | Iterera grannar till v |
|---|---|---|---|---|
| Lista av kanter | E | O(1) | O(E) | O(E) |
| Adjacensmatris | V² | O(1) | O(1) | O(V) |
| **Adjacenslistor** | **V + E** | **O(1)** | **O(degree(v))** | **O(degree(v))** |

**Adjacensmatris** (V×V boolean-matris) slösar minne: en graf med 1 miljon hörn och 10 miljoner kanter behöver 10⁶ × 10⁶ = 10¹² bitar ≈ 125 GB! Adjacenslistor behöver bara ~10⁷ poster.

### Implementation: Graph

```java
public class Graph {
    private final int V;            // Antal hörn
    private int E;                   // Antal kanter
    private Bag<Integer>[] adj;      // Adjacenslistor
    
    public Graph(int V) {
        this.V = V;
        this.E = 0;
        adj = (Bag<Integer>[]) new Bag[V];
        for (int v = 0; v < V; v++)
            adj[v] = new Bag<Integer>();  // Tom lista för varje hörn
    }
    
    public void addEdge(int v, int w) {
        adj[v].add(w);   // Lägg till w i v:s lista
        adj[w].add(v);   // Lägg till v i w:s lista (oriktat → dubbelriktat)
        E++;
    }
    
    public Iterable<Integer> adj(int v) {
        return adj[v];   // Alla grannar till v
    }
    
    public int V() { return V; }
    public int E() { return E; }
}
```

> 💡 **Varje kant lagras TVÅ gånger** — en gång i varje ändpunkts lista. Det är nödvändigt för att effektivt kunna iterera över grannar åt båda håll.

**Adjacenslistor för tinyG.txt:**
```
  adj[]
  0: 6 → 2 → 1 → 5          (ordningen beror på insättningsordning)
  1: 0
  2: 0
  3: 5 → 4
  4: 5 → 6 → 3
  5: 3 → 4 → 0
  6: 0 → 4
  7: 8
  8: 7
  ...
```

---

## 🔍 Depth-First Search (DFS)

### Idén: Utforska Så Djupt Som Möjligt

DFS är inspirerad av Trémaux's labyrintalgoritm: gå framåt så länge du kan, backa när du stöter på en återvändsgränd eller ett redan besökt hörn.

```java
public class DepthFirstSearch {
    private boolean[] marked;  // marked[v] = sant om v är besökt
    private int count;         // Antal besökta hörn
    
    public DepthFirstSearch(Graph G, int s) {
        marked = new boolean[G.V()];
        dfs(G, s);
    }
    
    private void dfs(Graph G, int v) {
        marked[v] = true;      // Markera v som besökt
        count++;
        for (int w : G.adj(v)) // För varje granne w till v:
            if (!marked[w])    //   Om w inte redan besökt:
                dfs(G, w);     //     Utforska rekursivt!
    }
    
    public boolean marked(int v) { return marked[v]; }
    public int count() { return count; }
}
```

### Proposition A: DFS Prestanda

> **Proposition A:** DFS markerar alla hörn förbundna med källan s, i tid proportionell mot summan av deras grader.

**Bevisskiss:** Varje hörn besöks högst en gång (tack vare `marked[]`). Varje kant undersöks högst två gånger (en gång per ändpunkt). Total tid: O(V + E) för hela den sammanhängande komponenten.

### Steg-för-steg Spårning

```
  Graf:  0—2—1, 0—5, 2—3—5, 2—4, 3—4
  adj[]: 0:[2,1,5]  1:[0,2]  2:[0,1,3,4]  3:[5,4,2]  4:[3,2]  5:[3,0]
  
  dfs(0):
    markera 0
    → granne 2 (ej markerad) → dfs(2):
        markera 2
        → granne 0 (markerad, skippa)
        → granne 1 (ej markerad) → dfs(1):
            markera 1
            → granne 0 (markerad) → skippa
            → granne 2 (markerad) → skippa
            ← KLAR med 1
        → granne 3 (ej markerad) → dfs(3):
            markera 3
            → granne 5 (ej markerad) → dfs(5):
                markera 5
                → granne 3 (markerad) → skippa
                → granne 0 (markerad) → skippa
                ← KLAR med 5
            → granne 4 (ej markerad) → dfs(4):
                markera 4
                → granne 3 (markerad) → skippa
                → granne 2 (markerad) → skippa
                ← KLAR med 4
            → granne 2 (markerad) → skippa
            ← KLAR med 3
        → granne 4 (markerad) → skippa
        ← KLAR med 2
    → granne 1 (markerad) → skippa
    → granne 5 (markerad) → skippa
    ← KLAR med 0
  
  Besöksordning: 0, 2, 1, 3, 5, 4
```

---

## 🛤️ DFS för Vägfinnning (DepthFirstPaths)

Utöver att bara markera vilka hörn som nås, kan DFS hitta *vägar*:

```java
public class DepthFirstPaths {
    private boolean[] marked;
    private int[] edgeTo;    // edgeTo[w] = v innebär att v→w var kanten
    private final int s;     // Källhörnet
    
    public DepthFirstPaths(Graph G, int s) {
        marked = new boolean[G.V()];
        edgeTo = new int[G.V()];
        this.s = s;
        dfs(G, s);
    }
    
    private void dfs(Graph G, int v) {
        marked[v] = true;
        for (int w : G.adj(v))
            if (!marked[w]) {
                edgeTo[w] = v;     // Kom ihåg: vi kom till w VIA v
                dfs(G, w);
            }
    }
    
    public boolean hasPathTo(int v) { return marked[v]; }
    
    public Iterable<Integer> pathTo(int v) {
        if (!hasPathTo(v)) return null;
        Stack<Integer> path = new Stack<>();
        for (int x = v; x != s; x = edgeTo[x])  // Följ edgeTo[] bakåt
            path.push(x);
        path.push(s);
        return path;
    }
}
```

`edgeTo[]` bildar ett **träd med rötter i s** (parent-link representation). Varje hörn pekar på det hörn som "upptäckte" det.

> ⚠️ **OBS:** DFS hittar *en* väg, men inte nödvändigtvis den *kortaste* vägen!

---

## 🌊 Breadth-First Search (BFS): Kortaste Vägar

### Idén: Utforska Nivå för Nivå

Till skillnad från DFS (som dyker djupt) undersöker BFS alla hörn på avstånd 1 först, sedan avstånd 2, etc. Detta garanterar att vi hittar den **kortaste vägen** (i antal kanter).

BFS använder en **kö** (FIFO) istället för rekursion (som implicit använder en stack):

```java
public class BreadthFirstPaths {
    private boolean[] marked;
    private int[] edgeTo;
    private final int s;
    
    public BreadthFirstPaths(Graph G, int s) {
        marked = new boolean[G.V()];
        edgeTo = new int[G.V()];
        this.s = s;
        bfs(G, s);
    }
    
    private void bfs(Graph G, int s) {
        Queue<Integer> queue = new Queue<>();
        marked[s] = true;
        queue.enqueue(s);
        
        while (!queue.isEmpty()) {
            int v = queue.dequeue();         // Ta nästa hörn från kön
            for (int w : G.adj(v)) {
                if (!marked[w]) {
                    edgeTo[w] = v;           // v upptäckte w
                    marked[w] = true;        // Markera INNAN enqueue!
                    queue.enqueue(w);        // Lägg till i kön
                }
            }
        }
    }
    
    // pathTo() och hasPathTo() — identiska med DFS-versionen
}
```

### DFS vs BFS: Visuell Skillnad

```
  DFS: Dyk djupt, backa vid återvändsgränd     
  
  Steg:  0 → 2 → 1 (backa) → 3 → 5 (backa) → 4
  Väg 0→5: 0-2-3-5  (lång, vindlande)
  
  BFS: Utforska i vågor, nivå för nivå          
  
  Steg:  0 → {2,1,5} → {3,4} → {}
  Väg 0→5: 0-5  (kortast möjlig!)
```

### Proposition B: BFS Ger Kortaste Vägar

> **Proposition B:** BFS beräknar kortaste vägar (i antal kanter) från s till alla förbundna hörn, i tid proportionell mot V + E.

### Generellt Mönster

DFS och BFS är varianter av samma schema:

1. Lägg källhörnet på en **datastruktur**
2. Så länge datastrukturen ej tom:
   - Ta ut ett hörn v
   - Markera v
   - Lägg in alla omarkerade grannar till v

Skillnaden: **DFS** använder en **stack** (sist in, först ut), **BFS** använder en **kö** (först in, först ut).

---

## 🧩 Connected Components med DFS

Vi kan använda DFS för att hitta *alla* sammanhängande komponenter:

```java
public class CC {
    private boolean[] marked;
    private int[] id;       // id[v] = komponent-ID för hörn v
    private int count;      // Antal komponenter
    
    public CC(Graph G) {
        marked = new boolean[G.V()];
        id = new int[G.V()];
        for (int v = 0; v < G.V(); v++) {
            if (!marked[v]) {
                dfs(G, v);
                count++;     // Ny komponent upptäckt!
            }
        }
    }
    
    private void dfs(Graph G, int v) {
        marked[v] = true;
        id[v] = count;      // Alla hörn i samma DFS-sökning får samma ID
        for (int w : G.adj(v))
            if (!marked[w])
                dfs(G, w);
    }
    
    public boolean connected(int v, int w) { return id[v] == id[w]; }
    public int id(int v) { return id[v]; }
    public int count() { return count; }
}
```

### Proposition C

> **Proposition C:** DFS-baserad CC använder förbehandlingstid proportionell mot V + E och stödjer sedan `connected()`-frågor i **O(1)**.

### DFS vs Union-Find för Connectivity

Jämfört med Union-Find (kap 1.5):

- **DFS (CC):** Måste bygga hela grafen först, sedan O(1) per fråga. Kan även ge *vägar*.
- **Union-Find:** Kan svara under pågående konstruktion (online). Kan *inte* ge vägar. Praktiskt snabbare om vi inte behöver hela grafen.

---

## 📝 Ytterligare Grafprocesseringsproblem (4.1)

Boken nämner flera problem som löses med varianter av DFS:

**Cykeldetektering:** Finns det en cykel i grafen? → DFS, kontrollera om vi hittar en granne som redan är markerad (och inte är vår förälder).

**Tvåfärgbarhet / Bipartiteness:** Kan vi färga hörnen med 2 färger så att inga grannar har samma färg? → DFS, försök alternera färger.

---

# 🧠 Propositioner att Komma Ihåg

| Proposition | Innehåll |
|---|---|
| **I** (2.2) | Undre gräns: ≥ lg(N!) ~ N lg N jämförelser krävs |
| **J** (2.2) | Mergesort är asymptotiskt optimal (jämförelsebaserat) |
| **O** (2.4) | Största nyckeln i heap-ordnat träd finns i roten |
| **P** (2.4) | Komplett binärträd med N noder har höjd ⌊lg N⌋ |
| **Q** (2.4) | Heap: insert ≤ 1 + lg N, delMax ≤ 2 lg N jämförelser |
| **R** (2.4) | Heapkonstruktion med sink: < 2N jämförelser |
| **S** (2.4) | Heapsort: < 2N lg N + 2N jämförelser |
| **G** (3.3) | Röd-svart BST: höjd ≤ 2 lg N |
| **H** (3.3) | Röd-svart BST: genomsnittlig väg ~1.00 lg N |
| **I** (3.3) | Röd-svart BST: ALLA operationer O(lg N) i värsta fall |
| **A** (4.1) | DFS markerar alla förbundna hörn i tid O(sum of degrees) |
| **B** (4.1) | BFS ger kortaste vägar, i tid O(V + E) |
| **C** (4.1) | CC med DFS: O(V + E) förbehandling, O(1) frågor |

---

## 🎯 Minnesregel: HEAP-SORT

```
H - Heapkonstruktion med sink: O(N)
E - Extra minne: O(1) — in-place!
A - Alltid O(N lg N) — garanterad
P - Prioritetskö: hjärtat i algoritmen
S - Sink & Swim: de två primitiva operationerna
O - Optimal i BÅDE tid och minne (unik!)
R - Roten innehåller alltid max
T - Trädstruktur i en array (elegant!)
```

## 🎯 Minnesregel: RÖD-SVART

```
R - Röda länkar lutar åt vänster (left-leaning)
Ö - Överensstämmer 1:1 med 2-3-träd
D - Dubbel höjd i värsta fall: ≤ 2 lg N
S - Samma get() som vanlig BST
V - Varje väg: lika många svarta länkar
A - Alla operationer logaritmiska (garanterat)
R - Rotationer + färgflippar balansar
T - Tre rader kod fixar allt i put()!
```

## 🎯 Minnesregel: GRAF-DFS-BFS

```
G - Graf = hörn + kanter
R - Representation med adjacenslistor: O(V+E) plats
A - Adjacency: granne-relation
F - Finns väg? DFS svarar!

D - Djupt först (stack/rekursion)
F - Följer kanter tills återvändsgränd
S - Stack-baserad (implicit via rekursion)

B - Bredd först (kö/FIFO)
F - Finner KORTASTE vägen
S - Sveper nivå för nivå
```

---

*Detta material är baserat på "Algorithms, 4th Edition" av Robert Sedgewick och Kevin Wayne, samt föreläsningsanteckningar av Jesper Larsson.*
