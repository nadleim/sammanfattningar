# 📚 Riktade Grafer & Kortaste Vägar
## Komplett Sammanfattning: Avsnitt 4.2 (Directed Graphs) och 4.4 (Shortest Paths)

**Baserat på:** Sedgewick & Wayne: Algorithms 4th Edition
**Komplement till:** Tidigare sammanfattning av kap 4.1 (oriktade grafer, DFS, BFS, CC)

---

# Del 1: Riktade Grafer — Digraphs (Avsnitt 4.2)

---

## 🧭 Från Oriktade till Riktade Grafer

I kapitel 4.1 studerade vi oriktade grafer där kanter är symmetriska: om det finns en väg från A till B finns det automatiskt en väg från B till A. Riktade grafer (digraphs) bryter denna symmetri — kanter har en **riktning**.

Denna till synes enkla ändring får djupgående konsekvenser. Tänk på det som skillnaden mellan en tvåfältsväg (kan köra åt båda håll) och en enkelriktad gata (bara en riktning). I en stad full av enkelriktade gator kan det vara möjligt att köra från A till B, men *omöjligt* att köra tillbaka!

```
┌─────────────────────────────────────────────────────────────────────┐
│  RIKTADE GRAFER I VERKLIGHETEN                                       │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  Tillämpning        │  Hörn            │  Riktad kant              │
│  ───────────────────┼──────────────────┼────────────────────────── │
│  Webben             │  Webbsidor       │  Hyperlänkar              │
│  Kursplanering      │  Kurser          │  Förkunskapskrav          │
│  Java-arv           │  Klasser         │  extends                  │
│  Matkedja           │  Arter           │  Äter-relation            │
│  Kalkylblad         │  Celler          │  Formelreferenser         │
│  Twitter/X          │  Användare       │  Följer-relation          │
│  Kompilator         │  Moduler         │  Importerar/Anropar       │
│  Citering           │  Artiklar        │  Citerar                  │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 📖 Terminologi för Riktade Grafer

**Riktad kant (directed edge):** En kant v→w pekar *från* v *till* w. Hörnet v kallas **huvud (head)**, w kallas **svans (tail)**. Vi skriver v→w.

**Ingrad och utgrad:** Antalet kanter som pekar *till* ett hörn är dess **ingrad** (indegree). Antalet kanter som pekar *från* ett hörn är dess **utgrad** (outdegree).

**Nåbarhet (reachability):** Hörn w är *nåbart* från v om det finns en riktad väg från v till w. OBS: att w är nåbart från v säger *inget* om huruvida v är nåbart från w!

**Riktad väg:** En sekvens av hörn förbundna av riktade kanter, alla i samma riktning.

**Riktad cykel:** En riktad väg som börjar och slutar i samma hörn (med minst en kant).

**DAG (Directed Acyclic Graph):** En riktad graf *utan* riktade cykler. Extremt viktig struktur — mer om detta snart.

> 🔑 **Fundamental skillnad mot oriktade grafer:** I en oriktad graf leder "connected" till en symmetrisk relation. I en digraph leder "reachable" till en *asymmetrisk* relation — detta ändrar allt.

---

## 💾 Digraph-datatypen

Implementationen liknar `Graph` från 4.1, men med två avgörande skillnader:

```java
public class Digraph {
    private final int V;
    private int E;
    private Bag<Integer>[] adj;

    public Digraph(int V) {
        this.V = V;
        this.E = 0;
        adj = (Bag<Integer>[]) new Bag[V];
        for (int v = 0; v < V; v++)
            adj[v] = new Bag<Integer>();
    }

    public void addEdge(int v, int w) {
        adj[v].add(w);    // ← BARA en riktning! (jämför med Graph)
        E++;
    }

    public Iterable<Integer> adj(int v) { return adj[v]; }

    public Digraph reverse() {               // ← NY metod!
        Digraph R = new Digraph(V);
        for (int v = 0; v < V; v++)
            for (int w : adj(v))
                R.addEdge(w, v);             // Vänd alla kanter
        return R;
    }
}
```

**Skillnad 1: `addEdge()` lägger bara till i *en* riktning.** I `Graph` anropas `add()` två gånger (v→w och w→v). I `Digraph` bara en gång (v→w). Varje kant lagras alltså en gång, inte två.

**Skillnad 2: `reverse()`-metoden** skapar en ny digraph med alla kanter omvända. Om originalet har v→w så har den omvända w→v. Detta är ovärderligt för algoritmer som Kosarajus (se nedan).

```
  Digraph:                      Reverse:
  0 → 5                         5 → 0
  0 → 1                         1 → 0
  2 → 0                         0 → 2
  2 → 3                         3 → 2
  3 → 5                         5 → 3
  3 → 2                         2 → 3   (cykel 2↔3 bevaras)
```

---

## 🔍 DFS i Riktade Grafer: Nåbarhet

### Samma Kod, Annorlunda Semantik

DFS i en digraph ser *exakt likadan ut* som i en oriktad graf — enda skillnaden är att `Graph` byts mot `Digraph`. Men den *semantiska* innebörden skiljer sig enormt:

- I en **oriktad graf** hittar DFS alla *sammanhängande* hörn (om v kan nå w, kan w nå v)
- I en **digraph** hittar DFS alla *nåbara* hörn (v kan nå w, men w kanske inte kan nå v!)

```java
public class DirectedDFS {
    private boolean[] marked;

    public DirectedDFS(Digraph G, int s) {
        marked = new boolean[G.V()];
        dfs(G, s);
    }

    // Multi-source version — nåbarhet från en MÄNGD av hörn
    public DirectedDFS(Digraph G, Iterable<Integer> sources) {
        marked = new boolean[G.V()];
        for (int s : sources)
            if (!marked[s]) dfs(G, s);
    }

    private void dfs(Digraph G, int v) {
        marked[v] = true;
        for (int w : G.adj(v))
            if (!marked[w])
                dfs(G, w);
    }

    public boolean marked(int v) { return marked[v]; }
}
```

### Proposition D

> **Proposition D:** DFS markerar alla hörn i en digraph som är nåbara från en given mängd källhörn, i tid proportionell mot summan av utgraderna hos de markerade hörnen.

**Multi-source nåbarhet** är speciellt intressant. Frågan "Finns det en riktad väg från *något* hörn i mängden till v?" besvaras genom att starta DFS från alla källor. Denna generalisering används bl.a. i reguljära uttryck (kapitel 5.4).

> 💡 BFS fungerar också i digraphs — med samma kodändring (Graph → Digraph). BFS ger fortfarande kortaste vägar i antal kanter.

---

## 🔄 Cykler i Digraphs: DirectedCycle

### Varför Cykler Är Viktiga

Cykler i riktade grafer indikerar *cirkulära beroenden*. Om kurs A kräver B, B kräver C, och C kräver A — då kan ingen student klara dem! Att upptäcka cykler är förutsättningen för topologisk sortering.

### Hur Cykeldetektering Fungerar

I en *oriktad* graf räcker det att hitta en granne som redan är markerad (och inte är föräldern). I en *digraph* behöver vi vara mer noggranna — vi vill hitta en **back edge**, dvs en kant till ett hörn som fortfarande är *aktivt på rekursionsstacken*.

Vi introducerar en extra boolesk array `onStack[]`:

```java
public class DirectedCycle {
    private boolean[] marked;
    private int[] edgeTo;
    private boolean[] onStack;    // ← NYT: Hörn aktiva i rekursionen
    private Stack<Integer> cycle;

    public DirectedCycle(Digraph G) {
        onStack = new boolean[G.V()];
        edgeTo  = new int[G.V()];
        marked  = new boolean[G.V()];
        for (int v = 0; v < G.V(); v++)
            if (!marked[v]) dfs(G, v);
    }

    private void dfs(Digraph G, int v) {
        onStack[v] = true;       // v är nu aktiv i rekursionen
        marked[v] = true;
        for (int w : G.adj(v)) {
            if (this.hasCycle()) return;
            else if (!marked[w]) {
                edgeTo[w] = v;
                dfs(G, w);
            }
            else if (onStack[w]) {
                // CYKEL HITTAD! w är redan aktiv → back edge
                cycle = new Stack<Integer>();
                for (int x = v; x != w; x = edgeTo[x])
                    cycle.push(x);
                cycle.push(w);
                cycle.push(v);
            }
        }
        onStack[v] = false;      // v lämnar rekursionen
    }

    public boolean hasCycle() { return cycle != null; }
    public Iterable<Integer> cycle() { return cycle; }
}
```

### Varför Behövs `onStack[]`?

I en oriktad graf kan vi skilja back edges från "already-visited" edges med enkla medel. I en digraph kan en granne vara `marked` av en *helt annan* DFS-gren — det indikerar *inte* en cykel. Bara om grannen fortfarande är på den aktuella rekursionsstacken (`onStack[w] == true`) har vi en äkta back edge → cykel.

```
  Exempel — markerad men INTE på stack (ingen cykel):

       DFS(0) → DFS(2) → DFS(3) → klar med 3
                  ↓
                DFS(4) → ser att 3 är markerad
                          men 3 är INTE på stack! (redan klar)
                          → INGEN cykel

  Exempel — markerad OCH på stack (cykel!):

       DFS(0) → DFS(5) → DFS(4) → DFS(3) → ser kant 3→5
                                              5 ÄR på stack!
                                              → CYKEL: 5→4→3→5
```

---

## 📐 DAG och Topologisk Sortering

### Vad Är en DAG?

En **DAG (Directed Acyclic Graph)** är en riktad graf utan cykler. DAG:ar modellerar beroendeförhållanden som *kan* tillfredsställas.

### Topologisk Sortering: Problemet

> **Topologisk sortering:** Ordna hörnen i en digraph så att *alla* riktade kanter pekar från ett hörn tidigare i ordningen till ett hörn senare i ordningen.

**Tillämpning — kursplanering:** Om Algoritmer kräver Intro till CS och Intro till CS kräver Linjär Algebra, måste topologisk ordning lägga Linjär Algebra *före* Intro till CS *före* Algoritmer.

### Proposition E

> **Proposition E:** En digraph har en topologisk ordning om och *bara* om den är en DAG.

**Bevis (⇒):** Om grafen har en riktad cykel kan elementen på cykeln inte ordnas linjärt (varje element kräver att det föregående redan har placerats).
**Bevis (⇐):** Konstruktivt — algorithmen nedan ger en topologisk ordning för varje DAG.

### Depth-First Orders: Pre, Post, och Reverse Post

DFS besöker varje hörn exakt en gång. Vi kan spara hörnen vid olika tidpunkter:

```java
public class DepthFirstOrder {
    private boolean[] marked;
    private Queue<Integer> pre;          // Preorder
    private Queue<Integer> post;         // Postorder
    private Stack<Integer> reversePost;  // Omvänd postorder

    public DepthFirstOrder(Digraph G) {
        pre  = new Queue<Integer>();
        post = new Queue<Integer>();
        reversePost = new Stack<Integer>();
        marked = new boolean[G.V()];
        for (int v = 0; v < G.V(); v++)
            if (!marked[v]) dfs(G, v);
    }

    private void dfs(Digraph G, int v) {
        pre.enqueue(v);          // Spara INNAN rekursiva anrop
        marked[v] = true;
        for (int w : G.adj(v))
            if (!marked[w])
                dfs(G, w);
        post.enqueue(v);         // Spara EFTER rekursiva anrop
        reversePost.push(v);     // Stack → omvänd postorder
    }

    public Iterable<Integer> pre()         { return pre; }
    public Iterable<Integer> post()        { return post; }
    public Iterable<Integer> reversePost() { return reversePost; }
}
```

**Skillnaden:**

| Order | Vad den ger | Spara-tidpunkt |
|---|---|---|
| **Preorder** | Ordningen hörn *påbörjas* | Före rekursiva anrop |
| **Postorder** | Ordningen hörn *slutförs* | Efter rekursiva anrop |
| **Reverse postorder** | Omvänd av postorder | Stack efter rekursiva anrop |

### Proposition F: Reverse Postorder = Topologisk Sortering!

> **Proposition F:** Omvänd postorder i en DAG *är* en topologisk sortering.

**Bevis:** Betrakta en godtycklig kant v→w. När `dfs(v)` anropas finns tre fall:

1. `dfs(w)` har redan anropats *och avslutats* (w markerad) → w placeras i postorder *före* v → w kommer *efter* v i reverse postorder ✓
2. `dfs(w)` har *inte* anropats (w omarkerad) → `dfs(w)` anropas (direkt eller indirekt) från `dfs(v)` → w avslutas före v → w kommer efter v i reverse postorder ✓
3. `dfs(w)` har anropats men *inte* avslutats → **Omöjligt i en DAG!** Det skulle innebära en väg w→...→v och kanten v→w, alltså en cykel.

I de två möjliga fallen avslutas w före v i postorder, så v kommer före w i reverse postorder. Varje kant pekar alltså "framåt" i reverse postorder — precis definitionen av topologisk ordning! ∎

### Topological (Algorithm 4.5)

```java
public class Topological {
    private Iterable<Integer> order;

    public Topological(Digraph G) {
        DirectedCycle cyclefinder = new DirectedCycle(G);
        if (!cyclefinder.hasCycle()) {
            DepthFirstOrder dfs = new DepthFirstOrder(G);
            order = dfs.reversePost();
        }
    }

    public Iterable<Integer> order() { return order; }
    public boolean isDAG() { return order != null; }
}
```

Notera den eleganta strukturen: kontrollera först om grafen har cykler (det skulle göra topologisk sortering omöjlig), och beräkna sedan reverse postorder om den inte har det.

**Tid:** O(V + E) — en DFS för cykeldetektering + en DFS för ordningen.

### Steg-för-steg Spårning

```
  DAG:  0→5, 0→1, 0→6, 2→0, 2→3, 3→5, 5→4, 6→4, 6→9,
        7→6, 8→7, 9→10, 9→11, 9→12, 11→12

  DFS-ordning (börjar vid 0):
  dfs(0) → dfs(5) → dfs(4) [4 done] → [5 done]
         → dfs(1) [1 done]
         → dfs(6) → dfs(9) → dfs(11) → dfs(12) [12 done]
                                      → [11 done]
                            → dfs(10) [10 done]
                   → [9 done]
         → [6 done] → [0 done]
  dfs(2) → dfs(3) [3 done] → [2 done]
  dfs(7) [7 done]
  dfs(8) [8 done]

  Postorder (läs "done" nerifrån):   4, 5, 1, 12, 11, 10, 9, 6, 0, 3, 2, 7, 8
  Reverse postorder (topologisk):    8, 7, 2, 3, 0, 6, 9, 10, 11, 12, 1, 5, 4
                                      ← alla kanter pekar åt höger!
```

---

## 💪 Stark Sammanhängande (Strong Connectivity)

### Definition

> **Definition:** Två hörn v och w är **starkt sammanhängande** om det finns en riktad väg från v till w *och* en riktad väg från w till v. En digraph är starkt sammanhängande om *alla* par av hörn är starkt sammanhängande.

Stark sammanhängande är en **ekvivalensrelation** (reflexiv, symmetrisk, transitiv), precis som "connected" i oriktade grafer. Det innebär att den partitionerar hörnen i **starka komponenter** — maximala delmängder av ömsesidigt nåbara hörn.

```
  Digraph med 5 starka komponenter:

  ┌───┐     ┌───────┐     ┌──────────┐
  │ 1 │     │ 0,2,3,│     │ 9,10,11, │     ┌───┐  ┌───┐
  └───┘     │  4,5  │     │   12     │     │ 6 │  │7,8│
            └───────┘     └──────────┘     └───┘  └───┘
```

> 🔑 **Nyckelinsikt:** Två hörn är starkt sammanhängande om och bara om de ligger på en gemensam riktad cykel. (Bevis: Kombinera vägarna v→w och w→v.)

### Starka Komponenter vs Connected Components

| Egenskap | CC (oriktad) | SCC (riktad) |
|---|---|---|
| Relation | Connectivity (symmetrisk) | Strong connectivity (symmetrisk) |
| Partitionering | Varje hörn i exakt en komponent | Varje hörn i exakt en komponent |
| Specialfall | Träd har 1 komponent | DAG har V komponenter (en per hörn) |
| Naiv algoritm | En DFS räcker | Behöver smartare teknik |

---

## 🌟 Kosarajus Algoritm (Algorithm 4.6)

### Tre Steg — Förvånansvärt Enkelt

Kosaraju löste problemet att hitta starka komponenter med en fantastiskt elegant idé:

1. **Beräkna reverse postorder** av den *omvända* grafen G^R
2. **Kör DFS** på den *ursprungliga* grafen G, men besök omarkerade hörn i den ordningen
3. Alla hörn som nås i varje DFS-anrop tillhör **samma starka komponent**

```java
public class KosarajuSCC {
    private boolean[] marked;
    private int[] id;        // Komponent-ID
    private int count;       // Antal starka komponenter

    public KosarajuSCC(Digraph G) {
        marked = new boolean[G.V()];
        id = new int[G.V()];

        // Steg 1: Reverse postorder av G^R
        DepthFirstOrder order = new DepthFirstOrder(G.reverse());

        // Steg 2: DFS på G i den ordningen
        for (int s : order.reversePost())
            if (!marked[s]) {
                dfs(G, s);
                count++;    // Ny komponent!
            }
    }

    private void dfs(Digraph G, int v) {
        marked[v] = true;
        id[v] = count;     // Tilldela komponent-ID
        for (int w : G.adj(v))
            if (!marked[w])
                dfs(G, w);
    }

    public boolean stronglyConnected(int v, int w) { return id[v] == id[w]; }
    public int id(int v)    { return id[v]; }
    public int count()      { return count; }
}
```

### Varför Fungerar Det? (Bevisidé)

Beviset är det svåraste i hela kapitlet, men kärnan är:

**Påstående:** Varje hörn v som nås av `dfs(G, s)` i steg 2 är starkt sammanhängande med s.

**Bevisriktning 1 (v nåbar från s i G):** Trivialt — DFS hittade v, alltså finns en väg s→...→v i G.

**Bevisriktning 2 (s nåbar från v i G):** Vi måste visa att det finns en väg v→...→s i G, dvs s→...→v i G^R. Nyckeln: ordningen från steg 1 garanterar att `dfs(G^R, v)` avslutades *innan* `dfs(G^R, s)` (annars hade v redan markerats). Eftersom det finns en väg v→s i G (dvs s→v i G^R), och `dfs(G^R, v)` slutade före `dfs(G^R, s)`, *måste* `dfs(G^R, s)` ha nått v — alltså finns en väg s→v i G^R, dvs v→s i G. ∎

> 💡 **Kommentar:** Kosarajus algoritm är ett extremfall av "lätt att koda, svårt att förstå." Koden skiljer sig från CC (oriktade grafer) bara i den markerade raden! Men beviset kräver noggrant resonemang om DFS-ordningar i G^R.

### Proposition I (4.2)

> **Proposition I:** Kosarajus algoritm använder tid och utrymme proportionellt mot V + E för förbehandling och stödjer sedan frågor om stark sammanhängande i O(1).

**Bevis:** Algoritmen beräknar omvända grafen (O(V+E)), gör DFS på den omvända grafen (O(V+E)), och gör DFS på originalgrafen (O(V+E)). Totalt: O(V+E).

---

## 🔗 Transitiv Closure och All-Pairs Reachability

**Transitiv closure** av en digraph G är en graf med samma hörn men en kant v→w om och bara om w är nåbar från v i G.

En naiv lösning: kör `DirectedDFS` från varje hörn → O(V(V+E)) tid, O(V²) utrymme:

```java
public class TransitiveClosure {
    private DirectedDFS[] all;

    TransitiveClosure(Digraph G) {
        all = new DirectedDFS[G.V()];
        for (int v = 0; v < G.V(); v++)
            all[v] = new DirectedDFS(G, v);
    }

    boolean reachable(int v, int w) { return all[v].marked(w); }
}
```

Detta fungerar för små/täta grafer, men för enorma grafer (som webben) är det opraktiskt. Att hitta en lösning med linjär förbehandlingstid och konstant frågetid för all-pairs reachability i digraphs är ett **öppet forskningsproblem**!

---

## 📋 Sammanfattning Kapitel 4.2

```
┌─────────────────────────────────────────────────────────────────────────┐
│  DIGRAPH-ALGORITMER: ÖVERSIKT                                           │
├───────────────────────────────────┬─────────────────┬───────────────────┤
│  Problem                          │  Algoritm        │  Tid              │
├───────────────────────────────────┼─────────────────┼───────────────────┤
│  Nåbarhet (single/multi-source)   │  DirectedDFS     │  O(V + E)         │
│  Kortaste riktade vägar (ovägt)   │  BFS             │  O(V + E)         │
│  Cykeldetektering                 │  DirectedCycle   │  O(V + E)         │
│  Topologisk sortering             │  Topological     │  O(V + E)         │
│  Stark sammanhängande             │  KosarajuSCC     │  O(V + E)         │
│  All-pairs reachability           │  TransitiveClos. │  O(V(V + E))      │
└───────────────────────────────────┴─────────────────┴───────────────────┘

Alla algoritmer utom TransitiveClosure är baserade på DFS.
```

---

# Del 2: Kortaste Vägar i Viktade Digrapher (Avsnitt 4.4)

---

## 🎯 Problemformulering

Nu kombinerar vi *riktade* grafer med *vikter* på kanterna. Frågan blir: vad är den billigaste vägen från A till B?

> **Single-source shortest paths (SSSP):** Given en kantviktad digraph och ett källhörn s, hitta kortaste vägen från s till varje annat hörn v.

"Kortaste" betyder här *lägsta totalvikt*, inte färst antal kanter.

### Shortest-Paths Tree (SPT)

Lösningen är ett **SPT (shortest-paths tree)** — ett rotfäst träd med rot i s, där vägen i trädet från s till varje hörn v är den kortaste vägen i grafen. Precis som BFS-trädet från 4.1, men nu med vikter.

---

## 🧱 Datatyper: DirectedEdge och EdgeWeightedDigraph

### DirectedEdge

```java
public class DirectedEdge {
    private final int v;           // från-hörn
    private final int w;           // till-hörn
    private final double weight;   // kantvikt

    public DirectedEdge(int v, int w, double weight) {
        this.v = v;  this.w = w;  this.weight = weight;
    }

    public int from()        { return v; }
    public int to()          { return w; }
    public double weight()   { return weight; }
    public String toString() { return String.format("%d->%d %.2f", v, w, weight); }
}
```

### EdgeWeightedDigraph

```java
public class EdgeWeightedDigraph {
    private final int V;
    private int E;
    private Bag<DirectedEdge>[] adj;

    public EdgeWeightedDigraph(int V) {
        this.V = V;  this.E = 0;
        adj = (Bag<DirectedEdge>[]) new Bag[V];
        for (int v = 0; v < V; v++)
            adj[v] = new Bag<DirectedEdge>();
    }

    public void addEdge(DirectedEdge e) {
        adj[e.from()].add(e);    // Bara i en riktning
        E++;
    }

    public Iterable<DirectedEdge> adj(int v) { return adj[v]; }
}
```

### SPT-datastrukturer

Alla kortaste-vägar-algoritmer bygger på samma två arrayer:

- **`edgeTo[v]`** — sista kanten på kortaste vägen från s till v (parent-link representation)
- **`distTo[v]`** — totala vikten på kortaste vägen från s till v

**Konventioner:** `edgeTo[s] = null`, `distTo[s] = 0.0`, och `distTo[v] = ∞` om v inte är nåbart.

```java
public double distTo(int v)            { return distTo[v]; }
public boolean hasPathTo(int v)        { return distTo[v] < Double.POSITIVE_INFINITY; }

public Iterable<DirectedEdge> pathTo(int v) {
    if (!hasPathTo(v)) return null;
    Stack<DirectedEdge> path = new Stack<>();
    for (DirectedEdge e = edgeTo[v]; e != null; e = edgeTo[e.from()])
        path.push(e);
    return path;
}
```

---

## ⚡ Edge Relaxation: Grundoperationen

All shortest-paths-teori vilar på en enda operation: **relaxering** av en kant.

**Idé:** Om vi hittar en *billigare* väg till w via kanten v→w, uppdaterar vi informationen.

```java
private void relax(DirectedEdge e) {
    int v = e.from(), w = e.to();
    if (distTo[w] > distTo[v] + e.weight()) {    // Finns billigare väg?
        distTo[w] = distTo[v] + e.weight();       // Uppdatera avstånd
        edgeTo[w] = e;                             // Uppdatera föregångare
    }
}
```

**Visualisering:**

```
  FÖRE relaxering av 3→6 (vikt 0.52):
    distTo[3] = 0.99,  distTo[6] = ∞

    0.99 + 0.52 = 1.51 < ∞ ?  JA → uppdatera!

  EFTER:
    distTo[6] = 1.51,  edgeTo[6] = 3→6

  INGET händer om kanten inte ger förbättring:
    distTo[3] = 0.99,  distTo[7] = 0.60

    0.99 + 0.39 = 1.38 < 0.60 ?  NEJ → redan bättre väg till 7!
```

En kant som *kan* ge en förbättring kallas **eligible** (behörig). Relaxering testar om kanten är eligible, och om ja, utför den uppdateringen.

---

## 📏 Optimalitetsvillkor och Generisk Algoritm

### Proposition P: Optimalitetsvillkor

> **Proposition P:** Värdena i `distTo[]` är korrekta kortaste-väg-längder om och bara om inget edge är eligible, dvs `distTo[w] ≤ distTo[v] + e.weight()` gäller för varje kant e från v till w.

**Bevis (⇒ nödvändigt):** Om `distTo[w]` är korrekt kortaste-väg-längd och det fanns en eligible kant, skulle den ge en kortare väg — motsägelse.

**Bevis (⇐ tillräckligt):** Om villkoret gäller för alla kanter, kan vi "kedja" olikheterna längs vilken väg som helst och visa att `distTo[w]` inte kan vara större än den kortaste vägens vikt.

> 🔑 **Varför detta är kraftfullt:** Alla kortaste-väg-algoritmer är *specialfall* av en generisk algoritm: relaxera kanter tills inga fler är eligible. Skillnaden mellan algoritmerna är bara *i vilken ordning* kanterna relaxeras.

### Proposition Q: Generisk Algoritm

> **Proposition Q:** Initiera `distTo[s] = 0` och alla andra `distTo[]` till ∞. Relaxera sedan kanter i valfri ordning tills ingen kant är eligible. Då innehåller `distTo[]` kortaste-väg-längderna.

---

## 🏆 Dijkstras Algoritm (Algorithm 4.9)

### Idé: Girig Expansion av SPT

Dijkstras algoritm bygger SPT genom att upprepa: **välj det onåddda hörn som är närmast källan**, relaxera alla dess kanter.

Tänk på det som en expanderande vattencirkel: vattnet når alltid den närmaste punkten först.

### Implementation

```java
public class DijkstraSP {
    private DirectedEdge[] edgeTo;
    private double[] distTo;
    private IndexMinPQ<Double> pq;

    public DijkstraSP(EdgeWeightedDigraph G, int s) {
        edgeTo = new DirectedEdge[G.V()];
        distTo = new double[G.V()];
        pq = new IndexMinPQ<Double>(G.V());

        for (int v = 0; v < G.V(); v++)
            distTo[v] = Double.POSITIVE_INFINITY;
        distTo[s] = 0.0;

        pq.insert(s, 0.0);
        while (!pq.isEmpty())
            relax(G, pq.delMin());    // Ta hörnet närmast källan
    }

    private void relax(EdgeWeightedDigraph G, int v) {
        for (DirectedEdge e : G.adj(v)) {
            int w = e.to();
            if (distTo[w] > distTo[v] + e.weight()) {
                distTo[w] = distTo[v] + e.weight();
                edgeTo[w] = e;
                if (pq.contains(w)) pq.change(w, distTo[w]);  // Uppdatera prio
                else                pq.insert(w, distTo[w]);   // Ny kandidat
            }
        }
    }
}
```

### Steg-för-steg Spårning

```
  tinyEWD.txt, källa = 0:
  
  Initialt: distTo = [0, ∞, ∞, ∞, ∞, ∞, ∞, ∞]
  pq = {0:0.00}

  delMin() → 0 (dist 0.00)
    relax 0→2 (0.26): distTo[2] = 0.26      pq: {2:0.26, 4:0.38}
    relax 0→4 (0.38): distTo[4] = 0.38

  delMin() → 2 (dist 0.26)
    relax 2→7 (0.34): distTo[7] = 0.60      pq: {4:0.38, 7:0.60}

  delMin() → 4 (dist 0.38)
    relax 4→5 (0.35): distTo[5] = 0.73      pq: {7:0.60, 5:0.73}
    relax 4→7 (0.37): 0.38+0.37=0.75 > 0.60 → ineligible!

  delMin() → 7 (dist 0.60)
    relax 7→3 (0.39): distTo[3] = 0.99      pq: {5:0.73, 3:0.99}
    relax 7→5 (0.28): 0.60+0.28=0.88 > 0.73 → ineligible

  delMin() → 5 (dist 0.73)
    relax 5→1 (0.32): distTo[1] = 1.05      pq: {3:0.99, 1:1.05}
    ...

  delMin() → 3 (dist 0.99)
    relax 3→6 (0.52): distTo[6] = 1.51      pq: {1:1.05, 6:1.51}

  delMin() → 1 (dist 1.05)  → inga förbättringar
  delMin() → 6 (dist 1.51)  → inga förbättringar

  RESULTAT:
  0→0 (0.00):
  0→1 (1.05): 0→4  4→5  5→1
  0→2 (0.26): 0→2
  0→3 (0.99): 0→2  2→7  7→3
  0→4 (0.38): 0→4
  0→5 (0.73): 0→4  4→5
  0→6 (1.51): 0→2  2→7  7→3  3→6
  0→7 (0.60): 0→2  2→7
```

### Proposition R: Korrekthet

> **Proposition R:** Dijkstras algoritm löser single-source shortest-paths-problemet i kantviktade digrapher med *icke-negativa* vikter.

**Bevis:** När hörn v tas bort från PQ, kan `distTo[v]` aldrig minska mer (alla vikter ≥ 0, och vi tar alltid minsta `distTo[]`-värdet). Alltså gäller `distTo[w] ≤ distTo[v] + e.weight()` för alla redan relaxerade kanter v→w. När alla hörn är relaxerade gäller optimalitetsvillkoren (Prop P). ∎

**Tidskomplexitet:** O(E log V) med en IndexMinPQ (binär heap).

### Samband med Prims MST-algoritm

Dijkstra och Prim är strukturellt nästan identiska! Båda bygger ett träd genom att lägga till det "billigaste" hörnet:

- **Prim:** Närmaste hörn *till trädet* (kantvikt)
- **Dijkstra:** Närmaste hörn *till källan* (total väglängd)

> 💡 **Minnesregel:** Ta bort referenserna till `distTo[v]` i Dijkstras `relax()` och du får i princip Prims eager implementation!

---

## 🔺 Kortaste Vägar i DAG:ar (Edge-Weighted DAGs)

### Varför DAG:ar Är Speciella

Om grafen saknar cykler kan vi göra *bättre* än Dijkstra:
- **Snabbare:** O(E + V) istället för O(E log V)
- **Hanterar negativa vikter!** (Dijkstra kräver ≥ 0)

### Idé: Relaxera i Topologisk Ordning

Om vi relaxerar hörn i topologisk ordning, relaxeras varje kant *exakt en gång*, och vid den tidpunkten har vi redan den korrekta `distTo[]`-värdet för kantkällan.

```java
public class AcyclicSP {
    private DirectedEdge[] edgeTo;
    private double[] distTo;

    public AcyclicSP(EdgeWeightedDigraph G, int s) {
        edgeTo = new DirectedEdge[G.V()];
        distTo = new double[G.V()];
        for (int v = 0; v < G.V(); v++)
            distTo[v] = Double.POSITIVE_INFINITY;
        distTo[s] = 0.0;

        // Adaptera Topological till EdgeWeightedDigraph
        Topological top = new Topological(G);
        for (int v : top.order())         // Topologisk ordning!
            relax(G, v);
    }

    private void relax(EdgeWeightedDigraph G, int v) {
        for (DirectedEdge e : G.adj(v)) {
            int w = e.to();
            if (distTo[w] > distTo[v] + e.weight()) {
                distTo[w] = distTo[v] + e.weight();
                edgeTo[w] = e;
            }
        }
    }
}
```

### Proposition S

> **Proposition S:** Genom att relaxera hörn i topologisk ordning löser vi single-source shortest paths i en kantviktad DAG i tid proportionell mot E + V.

**Bevis:** Varje kant v→w relaxeras exakt en gång (när v relaxeras). Eftersom v kommer före w i topologisk ordning, ändras inte `distTo[v]` efter att v relaxerats. Topologisk sortering tar O(E + V) (Prop G), och varje kant relaxeras en gång → totalt O(E + V). ∎

### Längsta Vägar i DAG:ar (Proposition T)

En bonus: genom att **negera alla vikter** och köra AcyclicSP hittar vi *längsta* vägar! (Eller: ändra `>` till `<` i relaxering och initiera `distTo[]` till `−∞`.)

> **Proposition T:** Vi kan lösa single-source longest-paths i kantviktade DAG:ar i tid proportionell mot E + V.

Detta är anmärkningsvärt eftersom longest paths i *generella* grafer är NP-svårt!

### Tillämpning: Critical Path Method (CPM)

Att hitta längsta vägen i en DAG har en direkt tillämpning i **projektplanering**. Om varje jobb har en varaktighet och beroenden, ger den längsta vägen den **minsta totala tiden** för att slutföra alla jobb (den kritiska vägen).

Modellen använder en DAG med:
- Nod för varje jobbs *start* och *slut*
- En kant med vikt = jobbets varaktighet från start till slut
- Zero-weight kanter för beroendeförordningar

---

## 🔄 Bellman-Ford-algoritmen

### Problemet: Negativa Vikter

Dijkstras algoritm kräver att alla vikter är ≥ 0. Men i verkligheten kan vikter vara negativa (t.ex. vinst vs kostnad, eller valutaväxling). Vi behöver en algoritm som hanterar negativa vikter.

### Negativa Cykler: En Fundamental Komplikation

Om det finns en **negativ cykel** (en cykel vars totala vikt är negativ) som är nåbar från s, har shortest-paths-problemet *ingen lösning* — vi kan minska avståndet obegränsat genom att gå runt cykeln upprepade gånger.

```
  Negativ cykel:  4 → 5 (vikt 0.35) → 4 (vikt −0.66)
                  Total: 0.35 + (−0.66) = −0.31

  Varje varv minskar avståndet med 0.31!
  distTo[4] → −∞  (ej definierat)
```

### Proposition X: Bellman-Ford-algoritmen

> **Proposition X:** Initiera `distTo[s] = 0` och alla andra till ∞. Relaxera sedan *alla* kanter, i valfri ordning, totalt V gånger (V "pass"). Om det inte finns negativa cykler nåbara från s, innehåller `distTo[]` kortaste-väg-längderna.

**Bevis (induktion):** Betrakta en specifik kortaste väg s = v₀→v₁→...→vₖ = t (med k ≤ V−1 kanter, eftersom inga negativa cykler). Efter pass i har algoritmen hittat kortaste vägen till vᵢ. Pass 0: distTo[s] = 0 (basfall). Pass i+1: kanten vᵢ→vᵢ₊₁ relaxeras, och distTo[vᵢ] är korrekt sedan pass i, så distTo[vᵢ₊₁] uppdateras korrekt. ∎

**Tid:** O(VE) — V pass × E kanter per pass.

### Kö-baserad Bellman-Ford (optimering)

Den generiska versionen relaxerar *alla* E kanter i varje pass, men de flesta kanter ger ingen förbättring! Vi kan optimera genom att bara relaxera kanter från hörn vars `distTo[]` ändrades i föregående pass:

```java
public class BellmanFordSP {
    private double[] distTo;
    private DirectedEdge[] edgeTo;
    private boolean[] onQ;
    private Queue<Integer> queue;
    private int cost;                         // Räknare för neg. cykel-check
    private Iterable<DirectedEdge> cycle;

    public BellmanFordSP(EdgeWeightedDigraph G, int s) {
        distTo  = new double[G.V()];
        edgeTo  = new DirectedEdge[G.V()];
        onQ     = new boolean[G.V()];
        queue   = new Queue<Integer>();

        for (int v = 0; v < G.V(); v++)
            distTo[v] = Double.POSITIVE_INFINITY;
        distTo[s] = 0.0;

        queue.enqueue(s);
        onQ[s] = true;
        while (!queue.isEmpty() && !hasNegativeCycle()) {
            int v = queue.dequeue();
            onQ[v] = false;
            relax(G, v);
        }
    }

    private void relax(EdgeWeightedDigraph G, int v) {
        for (DirectedEdge e : G.adj(v)) {
            int w = e.to();
            if (distTo[w] > distTo[v] + e.weight()) {
                distTo[w] = distTo[v] + e.weight();
                edgeTo[w] = e;
                if (!onQ[w]) {
                    queue.enqueue(w);
                    onQ[w] = true;
                }
            }
            if (cost++ % G.V() == 0)      // Kontrollera periodiskt
                findNegativeCycle();        // för negativa cykler
        }
    }
}
```

### Proposition Y

> **Proposition Y:** Den kö-baserade Bellman-Ford-algoritmen löser SSSP (eller hittar en negativ cykel nåbar från s) i tid proportionell mot EV i värsta fall, och extra utrymme proportionellt mot V.

I praktiken är Bellman-Ford ofta *mycket* snabbare än O(VE) — typiskt nära O(E+V).

### Negativ Cykel-detektering

Om kön aldrig töms efter V pass, finns en negativ cykel. Implementationen kontrollerar detta genom att periodiskt (var V:e relaxering) leta efter cykler i `edgeTo[]`-subgrafen:

```java
private void findNegativeCycle() {
    int V = edgeTo.length;
    EdgeWeightedDigraph spt = new EdgeWeightedDigraph(V);
    for (int v = 0; v < V; v++)
        if (edgeTo[v] != null)
            spt.addEdge(edgeTo[v]);
    // Kör cykeldetektering på SPT
    EdgeWeightedCycleFinder cf = new EdgeWeightedCycleFinder(spt);
    cycle = cf.cycle();
}
```

### Tillämpning: Arbitrage

En klassisk tillämpning av negativ cykel-detektering: **valutaarbitrage**. Om vi kan växla USD → EUR → GBP → USD och få tillbaka *mer* än vi startade med, har vi hittat en arbitragemöjlighet.

Modell: Skapa en kantviktad digraph där kantvikten för valutapar A→B sätts till `−ln(kurs_AB)`. En negativ cykel i denna graf motsvarar en arbitragemöjlighet!

**Varför logaritm?** Valutaväxling är *multiplikativ* (vi multiplicerar belopp × kurs), men shortest paths arbetar med *addition*. Logaritmen konverterar: ln(a × b) = ln(a) + ln(b). Negering: vi söker maximal produkt → minimal negativ summa → negativ cykel.

---

## 📊 Jämförelse: Tre Shortest-Paths-algoritmer

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│  SHORTEST-PATHS ALGORITMER: KOMPLETT ÖVERSIKT                                   │
├────────────────────┬──────────────────┬───────────┬──────────┬─────────────────┤
│  Algoritm           │  Restriktion     │  Typisk   │  Värsta  │  Extra utrymme  │
├────────────────────┼──────────────────┼───────────┼──────────┼─────────────────┤
│  Dijkstra (eager)   │  Positiva vikter │  E log V  │  E log V │  V              │
│  Topologisk sort    │  DAG (acyklisk)  │  E + V    │  E + V   │  V              │
│  Bellman-Ford (kö)  │  Inga neg cykler │  E + V    │  VE      │  V              │
└────────────────────┴──────────────────┴───────────┴──────────┴─────────────────┘
```

### Beslutsträd: Vilken Algoritm?

```
  Finns negativa vikter?
  ├── NEJ → Finns cykler?
  │         ├── NEJ (DAG) → Topologisk sort (E+V) ← snabbast!
  │         └── JA → Dijkstra (E log V) ← bästa garantin
  └── JA → Finns negativa cykler?
            ├── NEJ → Bellman-Ford (E+V typiskt, VE värsta)
            └── JA → Problemet ej väldefinierat!
                      (Bellman-Ford detekterar dem)
```

---

# 🧠 Propositioner att Komma Ihåg

| Proposition | Kapitel | Innehåll |
|---|---|---|
| **D** | 4.2 | DFS markerar alla nåbara hörn i digraph, tid O(sum of outdegrees) |
| **E** | 4.2 | Digraph har topologisk ordning ⟺ den är en DAG |
| **F** | 4.2 | Reverse postorder i en DAG = topologisk sortering |
| **H** | 4.2 | Kosarajus algoritm: DFS-anropen når exakt starka komponenter |
| **I** | 4.2 | Kosaraju: O(V+E) tid, O(1) frågor |
| **P** | 4.4 | Optimalitetsvillkor: distTo korrekt ⟺ inga eligible kanter |
| **Q** | 4.4 | Generisk SP-algoritm: relaxera tills inga kanter eligible |
| **R** | 4.4 | Dijkstra: korrekt för icke-negativa vikter, O(E log V) |
| **S** | 4.4 | DAG SP: topologisk ordning + relaxering, O(E + V) |
| **T** | 4.4 | Longest paths i DAG: O(E + V) (negera vikter) |
| **X** | 4.4 | Bellman-Ford: V pass av relaxering ger kortaste vägar |
| **Y** | 4.4 | Kö-baserad Bellman-Ford: O(VE) värsta fall |

---

## 🎯 Minnesregel: DIGRAPH

```
D - Directed: kanter har riktning (v→w ≠ w→v)
I - Indegree/outdegree: in-kanter vs ut-kanter
G - Graf-representation: addEdge() anropas EN gång
R - Reverse(): vänd alla kanter (nyckeln till Kosaraju!)
A - Acyclic (DAG): inga cykler → topologisk sortering möjlig
P - Postorder (reverse): DFS-ordning ger topologisk sort
H - Hörn nåbara ≠ Hörn sammanhängande (asymmetrisk!)
```

## 🎯 Minnesregel: DIJKSTRA

```
D - Distans-ordning: alltid närmaste hörnet först
I - IndexMinPQ: prioritetskö håller kandidater
J - Just positiva vikter (ej negativa!)
K - Kanter relaxeras en gång per hörn
S - SPT (shortest-paths tree) byggs stegvis
T - Tid: O(E log V) med binär heap
R - Relaxering: grundoperationen
A - Analogt med Prims MST-algoritm!
```

## 🎯 Minnesregel: BELLMAN

```
B - Bred tillämpning (hanterar negativa vikter!)
E - Eligible kanter → relaxera tills inga finns kvar
L - Linjär i E+V typiskt (men VE i värsta fall)
L - Loopar V gånger genom alla kanter
M - Minskar distTo[] steg för steg via pass
A - Arbitrage: hittar negativa cykler (valutaväxling!)
N - Negativa cykler detekteras (findNegativeCycle)
```

---

## 🔗 Kopplingar Mellan Kapitlen

```
  Kapitel 4.1 (Oriktade grafer)
       │
       ├── Graph, DFS, BFS, CC
       │
  Kapitel 4.2 (Riktade grafer)   ←── Du är här!
       │
       ├── Digraph, DirectedDFS, Topological, KosarajuSCC
       │
       ├── Nyckelinsikt: Riktning ändrar allt!
       │     - "Connected" → "Reachable" (asymmetrisk)
       │     - CC (en DFS) → SCC (Kosaraju, två DFS)
       │     - Cykler → DAG, topologisk sortering
       │
  Kapitel 4.4 (Kortaste vägar)   ←── Och här!
       │
       ├── EdgeWeightedDigraph, Relaxation, SPT
       │
       ├── Dijkstra (positiva vikter, girig, PQ)
       ├── AcyclicSP (DAG, topologisk ordning)
       └── Bellman-Ford (negativa vikter, kö-baserad)
```

---

*Detta material är baserat på "Algorithms, 4th Edition" av Robert Sedgewick och Kevin Wayne.*
