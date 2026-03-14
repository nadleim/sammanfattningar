# 📚 Oriktade Grafer & Ohanterlighet (Intractability)
## Komplett Sammanfattning: Avsnitt 4.1 (Undirected Graphs) och sidorna 910–921

**Baserat på:** Sedgewick & Wayne: Algorithms 4th Edition
**Komplement till:** Sammanfattning av kap 4.2 (riktade grafer) och 4.4 (kortaste vägar)

---

# Del 1: Oriktade Grafer (Avsnitt 4.1)

---

## 🧭 Vad Är en Graf?

En **graf** är en av de mest grundläggande strukturerna i datavetenskap. Den modellerar *relationer* mellan objekt.

> **Definition:** En graf består av en mängd **hörn** (vertices) och en samling **kanter** (edges). Varje kant förbinder ett par av hörn.

Tänk på det som en karta med städer (hörn) och vägar (kanter) — men vägarna har *ingen riktning* (du kan köra åt båda hållen).

```
┌─────────────────────────────────────────────────────────────────────┐
│  GRAFER I VERKLIGHETEN                                               │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  Tillämpning          │  Hörn             │  Kant                   │
│  ─────────────────────┼───────────────────┼──────────────────────── │
│  Socialt nätverk       │  Personer         │  "Är vän med"           │
│  Internet              │  Datorer/routrar  │  Nätverkskabel          │
│  Karta                 │  Korsningar       │  Vägar                  │
│  Schack                │  Positioner       │  Möjliga drag           │
│  Kemistruktur          │  Atomer           │  Kemiska bindningar     │
│  Elektrisk krets       │  Komponenter      │  Ledningar              │
│  Proteininteraktion    │  Proteiner        │  "Interagerar med"      │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 📖 Grundläggande Terminologi

### Hörn och Kanter

- **Hörn (vertex):** En punkt/nod i grafen. Representeras med ett heltal (0, 1, 2, ..., V−1).
- **Kant (edge):** En förbindelse mellan två hörn, skriven som v-w.
- **Angränsande (adjacent):** Två hörn är angränsande om en kant förbinder dem.
- **Grad (degree):** Antalet kanter som ansluter till ett hörn. Om hörn 3 har kanter till 1, 4 och 5 så har det grad 3.

### Vägar och Cykler

- **Väg (path):** En sekvens av hörn förbundna med kanter, t.ex. 0–2–3–5.
- **Enkel väg (simple path):** En väg utan upprepade hörn.
- **Cykel (cycle):** En väg som börjar och slutar i samma hörn (med minst 3 kanter).
- **Längd:** Antalet kanter i en väg.

### Sammanhang

- **Sammanhängande (connected):** Två hörn är sammanhängande om det finns en väg mellan dem.
- **Sammanhängande graf:** En graf där *alla* par av hörn är sammanhängande.
- **Sammanhängande komponent (connected component):** En maximal delmängd av ömsesidigt sammanhängande hörn.

### Speciella Graftyper

- **Träd (tree):** En sammanhängande graf utan cykler. Ett träd med V hörn har *exakt* V−1 kanter.
- **Skog (forest):** En acyklisk graf (kan ha flera komponenter — varje komponent är ett träd).
- **Bipartit graf:** En graf vars hörn kan delas i två mängder så att *alla* kanter går mellan mängderna (aldrig inom samma mängd).

```
  Träd (5 hörn, 4 kanter):    Cykel:          Bipartit graf:

      0                        0 --- 1          Grupp A    Grupp B
     / \                       |     |           0 -------- 3
    1   2                      3 --- 2           1 -------- 4
   / \                                           2 -------- 5
  3   4
```

Ytterligare matematiska egenskaper för **träd** — en graf G med V hörn är ett träd om och bara om *någon* av följande gäller:

- G har V−1 kanter och inga cykler.
- G har V−1 kanter och är sammanhängande.
- G är sammanhängande, men att ta bort *vilken* kant som helst gör den icke-sammanhängande.
- G är acyklisk, men att lägga till *vilken* kant som helst skapar en cykel.
- Exakt en enkel väg förbinder varje par av hörn i G.

### Gles vs Tät

- **Gles graf (sparse):** E ≈ c·V (relativt få kanter). De flesta verkliga grafer.
- **Tät graf (dense):** E ≈ V² (nära maximalt antal kanter).
- **Max antal kanter** i en enkel graf utan parallella kanter: V(V−1)/2.

> 🔑 **Viktigt:** Vi antar genomgående att graferna är *glesa*, dvs. E är i storleksordningen V. Detta påverkar vilka datastrukturer som är bäst.

---

## 💾 Graph-datatypen (API och Implementation)

### API:et

```java
public class Graph
    Graph(int V)                // Skapa tom graf med V hörn
    Graph(In in)                // Läs graf från inström
    int V()                     // Antal hörn
    int E()                     // Antal kanter
    void addEdge(int v, int w)  // Lägg till kant v-w
    Iterable<Integer> adj(int v)// Hörn angränsande till v
    String toString()           // Strängrepresentation
```

All grafprocessering i detta kapitel bygger på **`adj()`** — förmågan att iterera genom grannarna till ett hörn.

### Representationsalternativ

Det finns tre huvudsakliga sätt att lagra en graf i datorn:

```
┌────────────────────┬──────────┬───────────┬──────────────┬──────────────────┐
│  Representation     │  Utrymme │  Lägg till│  Kant        │  Iterera         │
│                     │          │  kant     │  existerar?  │  grannar         │
├────────────────────┼──────────┼───────────┼──────────────┼──────────────────┤
│  Lista av kanter    │  E       │  O(1)     │  O(E)        │  O(E)            │
│  Närhetsmatris      │  V²      │  O(1)     │  O(1)        │  O(V)            │
│  Närhetslistor (✓)  │  V + E   │  O(1)     │  O(deg(v))   │  O(deg(v))       │
└────────────────────┴──────────┴───────────┴──────────────┴──────────────────┘
```

> ✅ Vi använder **närhetslistor (adjacency lists)** — optimalt för glesa grafer.

### Implementation med Närhetslistor

```java
public class Graph {
    private final int V;          // Antal hörn
    private int E;                // Antal kanter
    private Bag<Integer>[] adj;   // Närhetslistor

    public Graph(int V) {
        this.V = V;
        this.E = 0;
        adj = (Bag<Integer>[]) new Bag[V];
        for (int v = 0; v < V; v++)
            adj[v] = new Bag<Integer>();   // Tom lista för varje hörn
    }

    public void addEdge(int v, int w) {
        adj[v].add(w);   // Lägg w i v:s lista
        adj[w].add(v);   // Lägg v i w:s lista  ← BÅDA riktningarna!
        E++;
    }

    public Iterable<Integer> adj(int v) {
        return adj[v];
    }
}
```

**Nyckelpoäng om implementationen:**

1. **Varje kant lagras TVÅ gånger** — w finns i v:s lista OCH v finns i w:s lista. Totalt 2E listnoder.
2. Utrymme: O(V + E).
3. Att lägga till en kant: O(1).
4. Iterera genom grannar till v: O(deg(v)) — proportionellt mot v:s grad.
5. Parallella kanter och self-loops tillåts.
6. **Ordningen i listorna beror på insättningsordningen** — samma graf kan ge olika listordningar.

```
  Exempel: tinyG.txt (13 hörn, 13 kanter)

  adj[]
  0:  6 → 2 → 1 → 5
  1:  0
  2:  0
  3:  5 → 4
  4:  5 → 6 → 3
  5:  3 → 4 → 0
  6:  0 → 4
  7:  8
  8:  7
  9:  11 → 10 → 12
  10: 9
  11: 9 → 12
  12: 11 → 9

  Tre sammanhängande komponenter:
  {0,1,2,3,4,5,6}  {7,8}  {9,10,11,12}
```

### Vanliga Grafoperationer (Klientkod)

```java
// Beräkna graden av hörn v
public static int degree(Graph G, int v) {
    int degree = 0;
    for (int w : G.adj(v)) degree++;
    return degree;
}

// Genomsnittlig grad i hela grafen
public static int avgDegree(Graph G) {
    return 2 * G.E() / G.V();    // Summan av alla grader = 2E
}
```

### Designmönster: Grafprocessering

Boken använder ett mönster där man skapar en separat klass för varje grafprocesseringsuppgift:

1. **Konstruktorn** tar en graf (och eventuellt en källa) som argument och gör förbehandling.
2. **Instansmetoder** låter klienten ställa frågor.

```java
// Exempel: Search API
public class Search
    Search(Graph G, int s)         // Hitta hörn förbundna med s
    boolean marked(int v)          // Är v förbundet med s?
    int count()                    // Hur många hörn förbundna med s?
```

Fördelen: Separerar grafrepresentationen från algoritmerna.

---

## 🔍 Depth-First Search (DFS)

DFS är den mest fundamentala grafsökningsalgoritmen. Idén: **gå så djupt som möjligt** innan du backar.

### Analogi: Labyrinten

Tänk dig att du utforskar en labyrint. DFS fungerar som att du rullar ut ett nystan:

1. **Markera** där du är (rita krita på väggen).
2. **Gå framåt** till en omarkerad granne.
3. Om alla grannar redan är markerade → **backa** längs nystanet till förra korridoren.
4. Upprepa tills du testat alla korridorer.

### Implementation (Algorithm 4.1)

```java
public class DepthFirstSearch {
    private boolean[] marked;  // marked[v] = har DFS besökt v?
    private int count;         // Antal hörn förbundna med s

    public DepthFirstSearch(Graph G, int s) {
        marked = new boolean[G.V()];
        dfs(G, s);
    }

    private void dfs(Graph G, int v) {
        marked[v] = true;          // 1. Markera hörnet
        count++;
        for (int w : G.adj(v))     // 2. Besök alla omarkerade grannar
            if (!marked[w])
                dfs(G, w);         // 3. Rekursivt anrop (gå djupare)
    }

    public boolean marked(int v) { return marked[v]; }
    public int count() { return count; }
}
```

### Steg-för-steg Spårning

```
  Graf:  adj[0] = {2,1,5}, adj[1] = {0,2}, adj[2] = {0,1,3,4}
         adj[3] = {5,4,2}, adj[4] = {3,2},  adj[5] = {3,0}

  dfs(0)                         marked: {0}
    → granne 2 omarkerad → dfs(2)     marked: {0,2}
        → granne 0 markerad → skip
        → granne 1 omarkerad → dfs(1)   marked: {0,1,2}
            → granne 0 markerad → skip
            → granne 2 markerad → skip
            → 1 klar (backa till 2)
        → granne 3 omarkerad → dfs(3)   marked: {0,1,2,3}
            → granne 5 omarkerad → dfs(5)   marked: {0,1,2,3,5}
                → granne 3 markerad → skip
                → granne 0 markerad → skip
                → 5 klar (backa till 3)
            → granne 4 omarkerad → dfs(4)   marked: {0,1,2,3,4,5}
                → granne 3 markerad → skip
                → granne 2 markerad → skip
                → 4 klar (backa till 3)
            → granne 2 markerad → skip
            → 3 klar (backa till 2)
        → granne 4 markerad → skip
        → 2 klar (backa till 0)
    → granne 1 markerad → skip
    → granne 5 markerad → skip
    → 0 klar

  ALLA hörn markerade! Grafen är sammanhängande.
```

### Proposition A

> **Proposition A:** DFS markerar alla hörn som är förbundna med källhörnet s, i tid proportionell mot summan av graderna hos de markerade hörnen.

**Bevis:** Varje post i närhetslistorna undersöks exakt en gång. Totalt finns det 2E sådana poster (två för varje kant). Dessutom sätts `marked[v]` en gång per hörn. Alltså: O(V + E) för en sammanhängande graf.

**Varför "summan av graderna"?** Summan av alla grader = 2E (varje kant bidrar med 2 till totalsumman, en gång per ändpunkt).

### DFS Traverserar Varje Kant Två Gånger

En viktig observation: DFS undersöker varje kant *två gånger*. Kanten v-w undersöks en gång från v:s nähetslist (och v hittar w) och en gång från w:s nähetslist (och w hittar v, som redan är markerad → skip). Så en graf med E kanter genererar 2E "check"-operationer.

### DFS och Trädstruktur

DFS bygger implicit ett **DFS-träd**: kanterna som leder till omarkerade hörn bildar ett träd. Övriga kanter (till redan markerade hörn) kallas *back edges* — de bildar aldrig del av trädet.

```
  DFS-träd från exemplet ovan (edgeTo[]-pekare):

       0
       |
       2
      / \
     1   3
        / \
       5   4
```

---

## 🛤️ DFS för Stigsökning (DepthFirstPaths)

Vi vill inte bara veta *om* det finns en väg — vi vill hitta den!

### Implementation

```java
public class DepthFirstPaths {
    private boolean[] marked;
    private int[] edgeTo;     // edgeTo[v] = senaste hörn på väg till v
    private final int s;      // Källhörn

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
                edgeTo[w] = v;     // ← Spara varifrån vi kom!
                dfs(G, w);
            }
    }

    public boolean hasPathTo(int v) { return marked[v]; }

    public Iterable<Integer> pathTo(int v) {
        if (!hasPathTo(v)) return null;
        Stack<Integer> path = new Stack<Integer>();
        for (int x = v; x != s; x = edgeTo[x])
            path.push(x);         // Följ pekarna bakåt
        path.push(s);
        return path;
    }
}
```

### Hur edgeTo[] Fungerar

`edgeTo[]` bildar en **föräldrapekare-representation** av DFS-trädet. Varje hörn (utom källan) pekar på det hörn som DFS kom ifrån.

```
  edgeTo[]:
  v     | 0  1  2  3  4  5
  ------+------------------
  from  | -  2  0  2  3  3

  Att hitta väg till 5:
  5 ← edgeTo[5] = 3 ← edgeTo[3] = 2 ← edgeTo[2] = 0 (källa!)
  Väg: 0-2-3-5
```

> ⚠️ **OBS:** DFS ger INTE kortaste vägar! Vägarna som DFS hittar beror på ordningen i närhetslistorna och kan vara långa och slingriga.

---

## 🌊 Breadth-First Search (BFS)

BFS löser **single-source shortest paths** (minst antal kanter) i oriktade grafer.

### Idé: Expanderande Våg

Istället för att gå djupt som DFS, utforskar BFS i *vågor*: först alla hörn på avstånd 1, sedan avstånd 2, osv.

- **DFS:** Använder en **stack** (rekursion) → utforskar djupt.
- **BFS:** Använder en **kö** (FIFO) → utforskar brett.

```
  DFS vs BFS — samma graf, olika utforskningsordningar:

  DFS: Går djupt → hittar slingrande vägar
  ────── "en person som utforskar en labyrint"

  BFS: Sveper utåt → hittar kortaste vägar
  ────── "en grupp som fläktar ut i alla riktningar"
```

### Implementation (Algorithm 4.2)

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
        Queue<Integer> queue = new Queue<Integer>();
        marked[s] = true;
        queue.enqueue(s);

        while (!queue.isEmpty()) {
            int v = queue.dequeue();          // Ta nästa hörn från kön
            for (int w : G.adj(v)) {
                if (!marked[w]) {
                    edgeTo[w] = v;             // Spara varifrån
                    marked[w] = true;
                    queue.enqueue(w);           // Lägg till i kön
                }
            }
        }
    }

    // hasPathTo() och pathTo() — identiska med DFS-versionen
}
```

### Steg-för-steg Spårning

```
  adj[0]={2,1,5}, adj[1]={0,2}, adj[2]={0,1,3,4},
  adj[3]={5,4,2}, adj[4]={3,2}, adj[5]={3,0}

  BFS från källa 0:

  Steg 0: kö = [0]         marked = {0}

  dequeue 0 → grannarna 2,1,5 (alla omarkerade)
  Steg 1: kö = [2, 1, 5]   marked = {0,1,2,5}   edgeTo[2]=0, edgeTo[1]=0, edgeTo[5]=0

  dequeue 2 → grannar 0(markerad), 1(markerad), 3(omarkerad!), 4(omarkerad!)
  Steg 2: kö = [1, 5, 3, 4] marked = {0,1,2,3,4,5}  edgeTo[3]=2, edgeTo[4]=2

  dequeue 1 → alla grannar markerade → inget nytt
  dequeue 5 → alla grannar markerade → inget nytt
  dequeue 3 → alla grannar markerade → inget nytt
  dequeue 4 → alla grannar markerade → inget nytt

  Kön tom → KLART!

  edgeTo[]:
  v     | 0  1  2  3  4  5
  ------+------------------
  from  | -  0  0  2  2  0

  Kortaste vägar:
  0→1: 0-1         (1 kant)
  0→2: 0-2         (1 kant)
  0→3: 0-2-3       (2 kanter)
  0→4: 0-2-4       (2 kanter)
  0→5: 0-5         (1 kant)
```

### Proposition B

> **Proposition B:** BFS markerar alla hörn förbundna med s i tid proportionell mot V + E, och de vägar som BFS-trädet representerar är *kortaste vägar* (minst antal kanter).

**Bevisidé:** BFS besöker hörn i ordning av deras avstånd från s. När ett hörn markeras, har det besökts via en väg med minimalt antal kanter — alla kortare vägar hade redan utforskats i tidigare "vågor". Formellt: kön innehåller aldrig hörn med avstånd som skiljer sig mer än 1.

### DFS vs BFS — Sammanfattning

```
┌──────────────────────┬─────────────────────┬─────────────────────┐
│  Egenskap             │  DFS                │  BFS                │
├──────────────────────┼─────────────────────┼─────────────────────┤
│  Datastruktur         │  Stack (rekursion)  │  Kö (FIFO)          │
│  Utforskningsstrategi │  Gå djupt först     │  Gå brett först     │
│  Vägar                │  Slingrande, långa  │  KORTASTE vägar     │
│  Tid                  │  O(V + E)           │  O(V + E)           │
│  Användning           │  Connectivity, CC   │  Shortest paths     │
│  Analogi              │  En utforskare      │  En expanderande våg│
└──────────────────────┴─────────────────────┴─────────────────────┘
```

> 🔑 **Nyckelinsikt:** DFS och BFS har *exakt samma* grundstruktur. Enda skillnaden: **stack vs kö**. Stack → senast inlagda hörnet utforskas först (djupt). Kö → först inlagda hörnet utforskas först (brett). Generellt:
>
> - **Ta nästa hörn v** från datastrukturen och markera det.
> - **Lägg alla omarkerade grannar** till v i datastrukturen.
>
> Med LIFO (stack) → DFS. Med FIFO (kö) → BFS.

---

## 🧩 Connected Components (CC)

### Problemet

> Givet en graf, dela upp hörnen i sammanhängande komponenter så att vi kan svara på frågan "Är v och w sammanhängande?" i O(1).

### Implementation (Algorithm 4.3)

```java
public class CC {
    private boolean[] marked;
    private int[] id;       // id[v] = komponent-ID för hörn v
    private int count;      // Antal komponenter

    public CC(Graph G) {
        marked = new boolean[G.V()];
        id = new int[G.V()];
        for (int s = 0; s < G.V(); s++) {
            if (!marked[s]) {
                dfs(G, s);        // Ny komponent!
                count++;
            }
        }
    }

    private void dfs(Graph G, int v) {
        marked[v] = true;
        id[v] = count;           // Alla hörn i samma DFS-anrop → samma ID
        for (int w : G.adj(v))
            if (!marked[w])
                dfs(G, w);
    }

    public boolean connected(int v, int w) { return id[v] == id[w]; }
    public int id(int v)  { return id[v]; }
    public int count()    { return count; }
}
```

### Hur Det Fungerar

1. Gå igenom alla hörn 0, 1, 2, ...
2. Om hörnet är omarkerat → starta DFS därifrån → alla nådda hörn får samma komponent-ID.
3. Öka `count` och fortsätt till nästa omarkerade hörn.

```
  tinyG.txt: 13 hörn, 13 kanter

  DFS(0) → markerar 0,6,2,1,5,4,3  → id = 0
  DFS(7) → markerar 7,8             → id = 1
  DFS(9) → markerar 9,11,12,10      → id = 2

  Resultat: 3 komponenter
  Komponent 0: {0, 1, 2, 3, 4, 5, 6}
  Komponent 1: {7, 8}
  Komponent 2: {9, 10, 11, 12}

  connected(0, 4) → id[0] == id[4] → 0 == 0 → true  (O(1)!)
  connected(0, 7) → id[0] == id[7] → 0 == 1 → false (O(1)!)
```

### Proposition C

> **Proposition C:** DFS-baserad CC använder förbehandlingstid proportionell mot V + E och stödjer sedan `connected()`-frågor i **O(1)**.

**Bevis:** Varje post i närhetslistorna undersöks exakt en gång (2E poster totalt), och det finns V hörn. Instansmetoderna kontrollerar eller returnerar bara en eller två instansvariabler.

### CC vs Union-Find

Jämfört med Union-Find (kapitel 1.5):

```
┌──────────────────────┬─────────────────────┬──────────────────────┐
│  Egenskap             │  CC (DFS)           │  Union-Find          │
├──────────────────────┼─────────────────────┼──────────────────────┤
│  Förbehandling        │  O(V + E) — bygger  │  Online — behöver    │
│                       │  hela grafen först  │  inte hela grafen    │
│  Frågor               │  O(1)               │  Nästan O(1)*        │
│  Hitta vägar?         │  JA (med edgeTo)    │  NEJ                 │
│  Online (dynamisk)?   │  NEJ                │  JA                  │
└──────────────────────┴─────────────────────┴──────────────────────┘
  * Union-Find: O(α(N)) per operation, praktiskt ≈ O(1)
```

> 💡 **Tumregel:** Behöver du svara *under* bygget av grafen? → Union-Find. Behöver du också vägar? → DFS.

---

## 📝 Ytterligare Problem (4.1)

Boken nämner flera andra problem som löses med varianter av DFS:

### Cykeldetektering

> Finns det en cykel i grafen?

DFS kan upptäcka cykler: om vi hittar en granne som redan är markerad och **inte är vår förälder** (det hörn vi kom ifrån), har vi hittat en cykel.

```java
private void dfs(Graph G, int v, int u) {  // u = förälder
    marked[v] = true;
    for (int w : G.adj(v)) {
        if (!marked[w])
            dfs(G, w, v);
        else if (w != u)       // Markerad granne som INTE är förälder
            hasCycle = true;   // → CYKEL!
    }
}
```

> 💡 **Observera skillnaden mot digraphs:** I en riktad graf behöver vi `onStack[]`-arrayen (se din sammanfattning av 4.2) eftersom en markerad granne kan ha nåtts via en helt annan gren. I en oriktad graf räcker det att kontrollera förälderpekaren.

### Tvåfärgbarhet (Bipartiteness)

> Kan vi färga hörnen med 2 färger så att inga grannar har samma färg?

DFS med alternering av färger: starta med färg A, ge alla grannar färg B, deras grannar färg A, osv. Om vi hittar en granne med *samma* färg → grafen är INTE bipartit.

### SymbolGraph

I verkligheten har hörn ofta namn (inte bara heltal). `SymbolGraph` kopplar strängar till heltal via en symboltabell (ST):

```
  Indata: "JFK", "ORD"    ←  flygplatsnamn
  Intern: 0, 1             ←  heltal för algoritmen
  Utdata: "JFK", "ORD"    ←  tillbaka till namn
```

Boken visar Kevin Bacon-problemet ("Degrees of Separation") som tillämpning: hitta kortaste "avstånd" mellan skådespelare via filmer de medverkat i. BFS ger exakt svaret.

---

## 📊 Sammanfattning Kapitel 4.1

```
┌───────────────────────────────────┬─────────────────┬───────────────────┐
│  Problem                          │  Algoritm        │  Tid              │
├───────────────────────────────────┼─────────────────┼───────────────────┤
│  Förbundenhet (single-source)     │  DFS             │  O(V + E)         │
│  Enkel-källa vägar                │  DFS (Paths)     │  O(V + E)         │
│  Kortaste vägar (ovägt)           │  BFS             │  O(V + E)         │
│  Sammanhängande komponenter       │  CC (DFS)        │  O(V + E)         │
│  Cykeldetektering                 │  DFS (Cycle)     │  O(V + E)         │
│  Tvåfärgbarhet / Bipartiteness    │  DFS (TwoColor)  │  O(V + E)         │
│  Connectivity-frågor              │  CC              │  O(1) per fråga   │
└───────────────────────────────────┴─────────────────┴───────────────────┘
```

---

# Del 2: Ohanterlighet / Intractability (s. 910–921)

---

## 🧱 Grundfrågan: Vad Kan Vi Lösa Effektivt?

Hittills i kursen har vi studerat problem med effektiva lösningar: sortering i O(N log N), sökning i O(log N), grafproblem i O(V + E). Men det finns problem som verkar kräva *exponentiell* tid.

### Turingmaskinen och Tre Grundidéer

Hela teorin vilar på Alan Turings arbete från 1930-talet:

1. **Universalitet (Church-Turing-tesen):** Alla beräkningsmaskiner (datorer, telefoner, supercomputers) kan simulera varandra. En Turingmaskin kan beräkna allt som någon annan maskin kan.

2. **Beräkningsbarhet:** Det *finns* problem som ingen maskin kan lösa (t.ex. *halting-problemet*: inget program kan för alla program avgöra om de terminerar).

3. **Utvidgade Church-Turing-tesen:** Skillnaden i hastighet mellan olika beräkningsmodeller är *högst polynomisk*. Ett problem som löses i polynomisk tid på en maskin kan löses i polynomisk tid på alla andra.

### Exponentiell vs Polynomisk Tid

```
  Polynomisk tid: N, N log N, N², N³, ...   → HANTERBART
  Exponentiell tid: 2^N, 3^N, N!, ...        → OHANTERLIGT

  Exempel för N = 100:
  ┌────────────────┬──────────────────────────────────────┐
  │  Tidskomplexitet │  Ungefärligt antal operationer       │
  ├────────────────┼──────────────────────────────────────┤
  │  N              │  100                                  │
  │  N²             │  10 000                               │
  │  N³             │  1 000 000                            │
  │  2^N            │  ~10³⁰ (fler än atomer i universum!)  │
  └────────────────┴──────────────────────────────────────┘
```

> 🔑 Ingen kan vänta på 2¹⁰⁰ steg, oavsett datorns hastighet.

---

## 🔎 Sökproblem och NP

### Definition: Sökproblem

> **Sökproblem:** Ett problem där vi, givet en lösningskandidat, kan *verifiera* (certifiera) att den är korrekt i polynomisk tid.

Det handlar alltså om att *hitta* en lösning bland enormt många möjligheter — men om någon ger dig en lösning kan du snabbt kontrollera den. Tänk "nål i en höstack" — du kan känna igen nålen, men att *hitta* den är en helt annan sak.

**Fyra viktiga sökproblem från boken:**

```
┌───────────────────────────────┬──────────────────────────────────────────┐
│  Problem                       │  Beskrivning                              │
├───────────────────────────────┼──────────────────────────────────────────┤
│  Linjär ekvationssatisfiering │  Hitta tilldelning av N variabler som     │
│                                │  uppfyller M linjära ekvationer           │
│                                │                                           │
│  Linjär olikhetssatisfiering  │  Hitta tilldelning av N variabler som     │
│  (linjär programmering)        │  uppfyller M linjära olikheter            │
│                                │                                           │
│  0-1 heltals linjär olikhets- │  Samma som ovan, men variablerna måste    │
│  satisfiering (heltals-LP)     │  vara 0 eller 1                           │
│                                │                                           │
│  Boolean satisfiability (SAT) │  Hitta tilldelning av N booleska          │
│                                │  variabler som uppfyller M ekvationer     │
│                                │  med AND och OR                           │
└───────────────────────────────┴──────────────────────────────────────────┘
```

### Definition: NP

> **NP** (Nondeterministic Polynomial time) = mängden av *alla* sökproblem.

NP är alla problem där en lösning kan verifieras i polynomisk tid. "N" i NP står för *nondeterminism* — tanken att en hypotetisk maskin kan "gissa" rätt lösning och sedan verifiera den.

> ⚠️ **Vanlig missuppfattning:** NP betyder INTE "Not Polynomial"! Det betyder "Nondeterministic Polynomial".

### Definition: P

> **P** = mängden av alla sökproblem som kan *lösas* i polynomisk tid.

Problem i P har effektiva algoritmer. Att hitta en effektiv algoritm *bevisar* att problemet är i P.

**Exempel på problem i P:**

```
┌───────────────────────────┬─────────────────────┬───────────────────┐
│  Problem                   │  Algoritm           │  Tid              │
├───────────────────────────┼─────────────────────┼───────────────────┤
│  Sortering                 │  Mergesort          │  O(N log N)       │
│  Kortaste vägar            │  BFS / Dijkstra     │  O(V+E) / O(ElogV)│
│  Linjära ekvationssystem   │  Gausseliminering   │  O(N³)            │
│  Linjär programmering      │  Ellipsoidmetoden   │  Polynomisk       │
└───────────────────────────┴─────────────────────┴───────────────────┘
```

### Relationen mellan P och NP

Alla problem i P tillhör också NP (om du kan *lösa* ett problem snabbt kan du definitivt *verifiera* en lösning snabbt). Men gäller det omvända?

```
  P ⊆ NP   (säkert — alla problem vi kan lösa snabbt kan vi verifiera snabbt)
  P = NP?  (miljonfrågan!)
```

### Nondeterminism — Vad Betyder Det?

Tänk på en nondeterministisk maskin som en som kan "gissa" rätt val vid varje beslutspunkt. I verkligheten finns sådana maskiner inte, men konceptet är användbart:

- En *deterministisk* algoritm prövar systematiskt (och kan ta exponentiell tid).
- En *nondeterministisk* algoritm "gissar" rätt lösning och *verifierar* den (polynomisk tid).

NP-frågan är i grunden: "Ger gissningsförmågan verklig extra kraft?"

---

## ❓ Frågan P = NP?

> **Gäller P = NP?** Det vill säga: om vi snabbt kan *kontrollera* en lösning, kan vi alltid snabbt *hitta* en lösning?

Frågan ställdes först i ett brev från Kurt Gödel till John von Neumann 1950 och har förbryllat matematiker och datavetare sedan dess. Det är det mest kända öppna problemet i datavetenskap (och ett av millennieproblemen med 1 miljon dollar i pris).

**Andra sätt att ställa frågan:**

- Finns det *några* genuint svåra sökproblem?
- Skulle vi kunna lösa vissa problem mer effektivt om vi kunde bygga en nondeterministisk maskin?

**Vad det skulle innebära:**

- Om **P = NP:** Alla problem vars lösningar kan verifieras effektivt kan också *lösas* effektivt. Enorma konsekvenser: kryptering bryts, optimering blir trivial, etc.
- Om **P ≠ NP:** Det finns problem som är genuint svåra att lösa, även om lösningar är lätta att verifiera. (De allra flesta forskare tror detta.)

```
  Två möjliga universum:

  ╔══════════════════════╗    ╔══════════════════════╗
  ║    Om P ≠ NP:        ║    ║    Om P = NP:         ║
  ║                      ║    ║                       ║
  ║   ┌───────────┐      ║    ║   ┌───────────┐       ║
  ║   │    NP     │      ║    ║   │  P = NP   │       ║
  ║   │  ┌─────┐  │      ║    ║   │           │       ║
  ║   │  │  P  │  │      ║    ║   │           │       ║
  ║   │  └─────┘  │      ║    ║   └───────────┘       ║
  ║   │   NPC ←   │      ║    ║                       ║
  ║   └───────────┘      ║    ║                       ║
  ╚══════════════════════╝    ╚══════════════════════╝
    (NPC = NP-komplett)          (Alla problem lika lätta)
```

---

## 🔗 Polynomisk Reduktion

### Idén

Om vi kan *omvandla* ett problem A till ett problem B (och tillbaka) i polynomisk tid, säger vi att A **poly-time reduceras** till B.

```
  Problem A → Transformera → Problem B → Lös B → Transformera tillbaka → Lösning A

  Om transformeringarna tar polynomisk tid
  OCH B kan lösas i polynomisk tid
  → Då kan A lösas i polynomisk tid!
```

**Men reduktion fungerar åt BÅDA hållen för svårhet:**

- Om A är *svårt* och reduceras till B → B är *minst lika svårt* som A.
- Varför? Om B var lätt, skulle A också vara lätt (via reduktionen) — men A var svårt!

Mer precist: vi löser högst ett polynomiskt antal instanser av B, med transformeringar som tar högst polynomisk tid. Om allt detta är polynomiskt → A löses i polynomisk tid.

### Konkret Exempel: SAT reduceras till Heltals-LP

**Proposition L** i boken visar att boolean satisfiability (SAT) poly-time-reduceras till 0-1 heltals linjär olikhetssatisfiering:

Givet en boolesk formel, t.ex.: `(x₁' OR x₂ OR x₃) AND (x₁ OR x₂' OR x₃)`

Kan vi konstruera ett system av heltals-olikheter med 0-1 variabler:
- Varje boolesk variabel x → heltals 0-1 variabel
- Varje klausul → en olikhet
- En extra variabel s som är 1 om och bara om alla klausuler är sanna

Om SAT är svårt → heltals-LP är *minst* lika svårt.

> **Corollary:** Om satisfiability är svårt att lösa, så är heltals linjär programmering det också.

---

## 🏆 NP-fullständighet

### Definition

> **NP-komplett:** Ett sökproblem A är NP-komplett om *alla* problem i NP poly-time-reduceras till A.

Det betyder: om du kunde lösa ETT NP-komplett problem effektivt, kunde du lösa ALLA problem i NP effektivt! NP-kompletta problem är alltså de "svåraste" i NP.

### Cook-Levin-satsen (Proposition M)

> **Proposition M (Cook-Levin):** Boolean satisfiability (SAT) är NP-komplett.

Cook och Levin bevisade (oberoende, tidigt 1970-tal) att SAT är NP-komplett.

**Bevisidé (extremt förenklad):** Varje problem i NP kan lösas av en nondeterministisk Turingmaskin. Man kan beskriva maskinens beteende med logiska formler — detta ger en SAT-instans. Att lösa SAT-instansen simulerar i princip maskinen.

> 💡 Bara ETT sådant bevis behövdes. Sedan kan man bevisa andra problem NP-kompletta via reduktion.

### Dominoeffekten

Sedan Cook-Levin-satsen har tiotusentals problem visats vara NP-kompletta, startande med Richard Karps banbrytande arbete 1972:

```
  SAT (Cook-Levin bevisar den NP-komplett)
    ↓ poly-time-reduceras till
  Heltals-LP (Proposition L)
    ↓ reduceras till
  Vertex Cover, Hamiltonsk väg, lastbalansering, ...
```

Det kollektiva misslyckandet att hitta polynomiska algoritmer för NÅGOT av dessa problem ses som starkt indicium på att P ≠ NP.

### Berömda NP-kompletta Problem

```
┌────────────────────────────────────────────────────────────────────┐
│  BERÖMDA NP-KOMPLETTA PROBLEM                                      │
├────────────────────────────────────────────────────────────────────┤
│                                                                    │
│  • Boolean satisfiability (SAT): Uppfyll en logisk formel          │
│  • Heltals linjär programmering: Optimera med heltalsbegränsningar │
│  • Lastbalansering: Schemalägg jobb på 2 processorer inom tid T    │
│  • Vertex cover: Hitta C hörn som täcker alla kanter               │
│  • Hamiltonsk väg: Besök alla hörn exakt en gång                   │
│  • Proteinvikning: Hitta konfiguration under energinivå M          │
│  • Ising-modellen: Subgraf med fri energi under tröskelvärde       │
│  • Riskportfölj: Minimera risk givet avkastningskrav               │
│                                                                    │
└────────────────────────────────────────────────────────────────────┘
```

### Klassificering av Problem

Att visa att ett problem tillhör P eller är NP-komplett:

```
  Visa att det är i P:
  → Hitta en polynomisk algoritm, eller
  → Reducera det till ett känt P-problem

  Visa att det är NP-komplett:
  → Visa att ett känt NP-komplett problem poly-time-reduceras till det

  Svårighetsgrad av klassificering:
  ┌─────────────────────┬──────────────────────────────────────────┐
  │  Enkel               │  Sortering (mergesort), kortaste vägar   │
  │  Klurig men ej svår  │  Vissa reduktionsbevis                   │
  │  Extremt utmanande   │  Linjär programmering (Khachiyans bevis) │
  │  Öppna problem       │  Grafisomorfism, faktorisering           │
  └─────────────────────┴──────────────────────────────────────────┘
```

> 🔑 **Praktisk betydelse:** Om du möter ett NP-komplett problem i verkligheten, vet du att det (troligen) inte finns någon snabb exakt lösning — byt strategi!

---

## 🛠️ Att Hantera NP-fullständighet i Praktiken

Även om vi (troligen) inte kan lösa NP-kompletta problem exakt och effektivt, behöver vi fortfarande hantera dem. Fyra strategier:

### 1. Approximationsalgoritmer
Hitta en lösning som är *nära* optimal med garanti. Exempel: Euklidisk handelsresande-problem — det finns algoritmer som garanterar en lösning inom faktor 2 av optimum. Tyvärr räcker detta inte alltid — för vissa problem är även approximation NP-svårt.

### 2. Algoritmer som fungerar "i praktiken"
Även om värsta fallet är exponentiellt, kan de flesta verkliga instanser vara mycket lättare. Det bästa exemplet: heltals-LP-lösare har använts i industrin i decennier och fungerar utmärkt — trots att de *kan* kräva exponentiell tid.

### 3. Backtracking / Branch-and-Bound
Använd intelligent sökning för att undvika att utforska *alla* möjligheter. Avbryt tidigt om en dellösning inte kan leda till en bättre lösning.

### 4. "Effektiva" Exponentiella Algoritmer
Stor skillnad finns mellan tid proportionell mot N^(log N) och 2^N. Forskningen söker ständigt efter algoritmer med lägre exponentiell bas.

---

## 🔗 Kopplingar Till Grafer och Resten av Kursen

NP-fullständighet dyker upp i kursens grafkapitel på ett viktigt ställe:

```
  Kortaste vägar (shortest paths):  P (Dijkstra, BFS, Bellman-Ford)
  Längsta vägar (longest paths):    NP-komplett (i generella grafer)!
  Längsta vägar i DAG:              P (negera vikter + AcyclicSP, Prop T)
```

Skillnaden är dramatisk: att lägga till cykler gör longest-paths-problemet exponentiellt svårare. Att begränsa till DAG:ar gör det linjärt!

```
┌──────────────────────────────────────────────────────────────────┐
│  Lätt (P)                     │  Svårt (NP-komplett)             │
├──────────────────────────────┼──────────────────────────────────┤
│  Kortaste vägar              │  Längsta vägar (generell graf)   │
│  Längsta vägar i DAG         │  Hamiltonsk väg                  │
│  2-SAT                       │  3-SAT                           │
│  Eulersk väg                 │  Hamiltonsk väg                  │
│  Linjär programmering        │  Heltals linjär programmering    │
│  2-färgbarhet                │  3-färgbarhet                    │
└──────────────────────────────┴──────────────────────────────────┘
```

> 🔑 **Lärdomen:** Små förändringar i ett problem (2-SAT → 3-SAT, DAG → generell graf) kan göra det från polynomiskt till NP-komplett. Att känna igen dessa gränser är en nyckelkompetens.

---

## 📊 Sammanfattningstabell: P, NP, NP-komplett

```
┌────────────────────┬───────────────────────────────────────────────────────┐
│  Klass              │  Beskrivning                                          │
├────────────────────┼───────────────────────────────────────────────────────┤
│  P                  │  Kan LÖSAS i polynomisk tid                           │
│                     │  (sortering, kortaste vägar, linjär programmering)    │
│                     │                                                       │
│  NP                 │  Lösning kan VERIFIERAS i polynomisk tid              │
│                     │  (alla sökproblem — P ⊆ NP)                          │
│                     │                                                       │
│  NP-komplett        │  De "svåraste" problemen i NP                         │
│  (NPC)              │  — alla NP-problem reduceras till dem                  │
│                     │  (SAT, Hamiltonsk väg, vertex cover, ...)             │
│                     │                                                       │
│  Oklassificerade    │  Varken bevisade i P eller NP-kompletta               │
│                     │  (grafisomorfism, faktorisering)                      │
└────────────────────┴───────────────────────────────────────────────────────┘
```

---

# 🧠 Propositioner att Komma Ihåg

| Proposition | Kapitel | Innehåll |
|---|---|---|
| **A** | 4.1 | DFS markerar alla förbundna hörn, tid O(sum of degrees) |
| **B** | 4.1 | BFS ger kortaste vägar (antal kanter), O(V + E) |
| **C** | 4.1 | CC med DFS: O(V + E) förbehandling, O(1) frågor |
| **L** | Intractability | SAT poly-time-reduceras till 0-1 heltals-LP |
| **M** | Intractability | Cook-Levin: SAT är NP-komplett |

---

## 🎯 Minnesregler

### GRAF (Kapitel 4.1)

```
G - Graph-datatypen: adj() ger grannarna
R - Representation: närhetslistor (V + E utrymme)
A - Algoritmer: DFS och BFS — stack vs kö
F - Förbundenhet: CC delar upp hörn i komponenter
```

### NP-KOMPLETT

```
N - NP: lösning verifierbar i polynomisk tid
P - P: lösning kan HITTAS i polynomisk tid
K - Koppling: P ⊆ NP, men P = NP? (öppet)
O - Omöjligt? Troligen — ingen har hittat snabb lösning för NPC
M - Massor av problem: SAT, Hamiltonsk väg, vertex cover...
P - Poly-time reduktion: visar att problem är lika svåra
L - Lev med det: approximera, backtrack, eller specialfall
E - Enorm praktisk betydelse: NPC → byt strategi
T - Tiotusentals NP-kompletta problem kända
T - Tror P ≠ NP: starkaste "beviset" = kollektivt misslyckande
```

---

*Detta material är baserat på "Algorithms, 4th Edition" av Robert Sedgewick och Kevin Wayne.*
