# 📚 Elementära Sorteringsalgoritmer och Grundläggande Datastrukturer
## Komplett Svensk Sammanfattning av Avsnitt 2.1 och Delar av 1.3

---

# Del 1: Bags, Queues och Stacks (Avsnitt 1.3)

---

## 🎯 Introduktion till Samlingar

### Varför Studera Dessa Datastrukturer?

Bags, queues och stacks är **fundamentala abstrakta datatyper (ADT:er)** som används som byggstenar i nästan alla algoritmer och datastrukturer. Att förstå dem är viktigt av tre skäl:

1. **Byggstenar** – De används för att konstruera mer komplexa datastrukturer
2. **Illustration** – De visar samspelet mellan datastrukturer och algoritmer
3. **Utgångspunkter** – De är startpunkter för att utveckla kraftfullare ADT:er

---

## 📋 API:er för Grundläggande Samlingar

### Bag (Påse)

```java
public class Bag<Item> implements Iterable<Item>
    Bag()                  // Skapa en tom bag
    void add(Item item)    // Lägg till ett element
    boolean isEmpty()      // Är bag:en tom?
    int size()             // Antal element i bag:en
```

**Karakteristik:** 
- Ingen remove-operation
- Ordningen spelar ingen roll
- Används när vi bara vill samla element och iterera genom dem

### Stack (LIFO – Last In, First Out)

```java
public class Stack<Item> implements Iterable<Item>
    Stack()                // Skapa en tom stack
    void push(Item item)   // Lägg till element överst
    Item pop()             // Ta bort och returnera översta elementet
    boolean isEmpty()      // Är stacken tom?
    int size()             // Antal element i stacken
```

**Karakteristik:**
- Senast tillagda elementet tas bort först
- Som en hög med tallrikar – du tar alltid den översta

### Queue (FIFO – First In, First Out)

```java
public class Queue<Item> implements Iterable<Item>
    Queue()                // Skapa en tom kö
    void enqueue(Item item) // Lägg till element sist
    Item dequeue()         // Ta bort och returnera första elementet
    boolean isEmpty()      // Är kön tom?
    int size()             // Antal element i kön
```

**Karakteristik:**
- Först tillagda elementet tas bort först
- Som en kö i affären – den som kom först betjänas först

---

## 🔧 Generics (Parameteriserade Typer)

### Vad Är Generics?

**Definition:** Generics är en Java-mekanism som låter oss skriva en enda implementation som fungerar för **alla typer av data**.

### Utan Generics vs Med Generics

```
┌─────────────────────────────────────────────────────────────────────┐
│  UTAN GENERICS                  │  MED GENERICS                    │
├─────────────────────────────────┼──────────────────────────────────┤
│  StackOfStrings                 │  Stack<String>                   │
│  StackOfIntegers                │  Stack<Integer>                  │
│  StackOfTransactions            │  Stack<Transaction>              │
│  StackOfDates                   │  Stack<Date>                     │
│                                 │                                  │
│  → Många olika klasser!         │  → EN enda klass för alla!       │
└─────────────────────────────────┴──────────────────────────────────┘
```

### Syntax för Generics

```java
// Deklaration av generisk klass
public class Stack<Item> {
    private Item[] a;       // Item är en typparameter
    private int N;
    
    public void push(Item item) {
        a[N++] = item;
    }
    
    public Item pop() {
        return a[--N];
    }
}

// Användning med konkret typ
Stack<String> stack = new Stack<String>();
stack.push("Test");
String next = stack.pop();
```

### Skapa Generiska Arrayer

**Problem:** Java tillåter inte `new Item[cap]` direkt.

**Lösning:** Använd en cast:

```java
a = (Item[]) new Object[cap];  // Ger kompilatorvarning (kan ignoreras)
```

---

## 📦 Autoboxing och Auto-unboxing

### Vad Är Autoboxing?

**Definition:** Autoboxing är automatisk konvertering mellan primitiva typer och deras wrapper-klasser.

### Primitiver och Deras Wrapper-klasser

| Primitiv | Wrapper |
|----------|---------|
| boolean | Boolean |
| byte | Byte |
| char | Character |
| int | Integer |
| long | Long |
| float | Float |
| double | Double |

### Exempel på Autoboxing

```java
Stack<Integer> stack = new Stack<Integer>();

stack.push(17);        // Autoboxing: int → Integer
int i = stack.pop();   // Auto-unboxing: Integer → int
```

> ⚠️ **Prestandavarning:** Autoboxing har en kostnad! Ett Integer-objekt tar 24 bytes medan en int bara tar 4 bytes.

---

## 🔄 Iterable Collections (Iterbara Samlingar)

### Foreach-konstruktionen

**Definition:** `Iterable` är ett Java-interface som tillåter iteration genom en samling med foreach-syntax.

```java
Queue<Transaction> collection = new Queue<Transaction>();

// Foreach-iteration (elegant och tydlig)
for (Transaction t : collection) {
    StdOut.println(t);
}
```

### Implementera Iterable

För att göra en klass iterbar behövs:

1. Klassen implementerar `Iterable<Item>`
2. En `iterator()`-metod som returnerar en `Iterator<Item>`
3. En inre klass som implementerar `Iterator` med `hasNext()` och `next()`

```java
import java.util.Iterator;

public class Bag<Item> implements Iterable<Item> {
    // ...
    
    public Iterator<Item> iterator() {
        return new ListIterator();
    }
    
    private class ListIterator implements Iterator<Item> {
        private Node current = first;
        
        public boolean hasNext() {
            return current != null;
        }
        
        public Item next() {
            Item item = current.item;
            current = current.next;
            return item;
        }
        
        public void remove() { }  // Används ej
    }
}
```

---

## 📏 Array-baserad Implementation

### FixedCapacityStack

**Enklaste möjliga stack:** Fast storlek, bestämd vid skapandet.

```java
public class FixedCapacityStack<Item> {
    private Item[] a;    // stack-element
    private int N;       // antal element
    
    public FixedCapacityStack(int cap) {
        a = (Item[]) new Object[cap];
    }
    
    public boolean isEmpty() { return N == 0; }
    public int size()        { return N; }
    
    public void push(Item item) {
        a[N++] = item;
    }
    
    public Item pop() {
        return a[--N];
    }
}
```

**Problem med fast kapacitet:**
- Klienten måste gissa maxstorlek i förväg
- Slösar minne om samlingen oftast är liten
- Overflow om samlingen växer för stor

---

## 📈 Resizing Array (Dynamisk Array)

### Idé

**Lösning:** Ändra arrayens storlek dynamiskt:
- **Dubbla** storleken när arrayen blir full
- **Halvera** storleken när arrayen är 25% full

### Implementation

```java
public class ResizingArrayStack<Item> implements Iterable<Item> {
    private Item[] a = (Item[]) new Object[1];
    private int N = 0;
    
    private void resize(int max) {
        Item[] temp = (Item[]) new Object[max];
        for (int i = 0; i < N; i++)
            temp[i] = a[i];
        a = temp;
    }
    
    public void push(Item item) {
        if (N == a.length) resize(2 * a.length);  // Dubbla!
        a[N++] = item;
    }
    
    public Item pop() {
        Item item = a[--N];
        a[N] = null;  // Undvik loitering
        if (N > 0 && N == a.length/4) resize(a.length/2);  // Halvera!
        return item;
    }
}
```

### Varför 25% för Halvering?

```
┌─────────────────────────────────────────────────────────────────────┐
│  OM VI HALVERAR VID 50%:                                           │
│  push → full → dubblering → pop → halvering → push → dubblering... │
│  = Thrashing! Varje operation tar O(N) tid!                        │
├─────────────────────────────────────────────────────────────────────┤
│  OM VI HALVERAR VID 25%:                                           │
│  Arrayen är alltid mellan 25% och 100% full                        │
│  = Amorterad konstant tid per operation                            │
└─────────────────────────────────────────────────────────────────────┘
```

### Loitering (Minnesläcka)

**Problem:** När vi poppar, finns referensen kvar i arrayen.

```java
// FEL - orsakar loitering
public Item pop() {
    return a[--N];  // a[N] pekar fortfarande på objektet!
}

// RÄTT - förhindrar loitering
public Item pop() {
    Item item = a[--N];
    a[N] = null;    // Släpp referensen
    return item;
}
```

### Prestandaanalys

| Operation | Värsta fall | Amorterat |
|-----------|-------------|-----------|
| push() | N (vid resize) | ~1 |
| pop() | N (vid resize) | ~1 |

> **Proposition:** Den amorterade kostnaden per operation är **konstant** i värsta fall.

---

## 🔗 Länkade Listor

### Definition

> **Definition:** En **länkad lista** är en rekursiv datastruktur som antingen är tom (null) eller en referens till en nod som innehåller ett generiskt element och en referens till en länkad lista.

### Node-klassen

```java
private class Node {
    Item item;   // Datat
    Node next;   // Referens till nästa nod
}
```

### Visualisering

```
┌─────────────────────────────────────────────────────────────────────┐
│                     LÄNKAD LISTA                                   │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  first                                                              │
│    │                                                                │
│    ▼                                                                │
│  ┌─────────┐    ┌─────────┐    ┌─────────┐                         │
│  │  "to"   │───▶│  "be"   │───▶│  "or"   │───▶ null                │
│  └─────────┘    └─────────┘    └─────────┘                         │
│                                                                     │
│  Varje box är en Node med:                                         │
│  • item (data)                                                     │
│  • next (referens till nästa nod)                                  │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Bygga en Länkad Lista

```java
Node first = new Node();
Node second = new Node();
Node third = new Node();

first.item = "to";
second.item = "be";
third.item = "or";

first.next = second;
second.next = third;
// third.next är null (standard)
```

---

## 🔧 Operationer på Länkade Listor

### Infoga i Början (O(1))

```java
// Spara referens till gamla första
Node oldfirst = first;

// Skapa ny nod
first = new Node();
first.item = "not";
first.next = oldfirst;
```

```
┌─────────────────────────────────────────────────────────────────────┐
│  FÖRE:  first ──▶ [to] ──▶ [be] ──▶ [or] ──▶ null                  │
│                                                                     │
│  EFTER: first ──▶ [not] ──▶ [to] ──▶ [be] ──▶ [or] ──▶ null        │
└─────────────────────────────────────────────────────────────────────┘
```

### Ta Bort från Början (O(1))

```java
first = first.next;
```

### Infoga i Slutet (O(1) med last-referens)

```java
Node oldlast = last;
last = new Node();
last.item = "not";
last.next = null;

if (isEmpty()) first = last;
else           oldlast.next = last;
```

### Traversera Listan

```java
for (Node x = first; x != null; x = x.next) {
    // Bearbeta x.item
}
```

---

## 📚 Stack med Länkad Lista

### Implementation (Algoritm 1.2)

```java
public class Stack<Item> implements Iterable<Item> {
    private Node first;  // Toppen av stacken
    private int N;       // Antal element
    
    private class Node {
        Item item;
        Node next;
    }
    
    public boolean isEmpty() { return first == null; }
    public int size()        { return N; }
    
    public void push(Item item) {
        Node oldfirst = first;
        first = new Node();
        first.item = item;
        first.next = oldfirst;
        N++;
    }
    
    public Item pop() {
        Item item = first.item;
        first = first.next;
        N--;
        return item;
    }
}
```

### Visuell Spårning

```
Operation    Stack (top → bottom)
─────────────────────────────────
push("to")   [to] → null
push("be")   [be] → [to] → null
push("or")   [or] → [be] → [to] → null
pop()        [be] → [to] → null       returnerar "or"
push("not")  [not] → [be] → [to] → null
```

---

## 📚 Queue med Länkad Lista

### Implementation (Algoritm 1.3)

```java
public class Queue<Item> implements Iterable<Item> {
    private Node first;  // Länk till äldsta elementet
    private Node last;   // Länk till nyaste elementet
    private int N;       // Antal element
    
    private class Node {
        Item item;
        Node next;
    }
    
    public boolean isEmpty() { return first == null; }
    public int size()        { return N; }
    
    public void enqueue(Item item) {
        Node oldlast = last;
        last = new Node();
        last.item = item;
        last.next = null;
        if (isEmpty()) first = last;
        else           oldlast.next = last;
        N++;
    }
    
    public Item dequeue() {
        Item item = first.item;
        first = first.next;
        if (isEmpty()) last = null;
        N--;
        return item;
    }
}
```

### Visuell Spårning

```
Operation       Queue (front → back)
──────────────────────────────────────
enqueue("to")   [to]
enqueue("be")   [to] → [be]
enqueue("or")   [to] → [be] → [or]
dequeue()       [be] → [or]           returnerar "to"
enqueue("not")  [be] → [or] → [not]
```

---

## 📊 Jämförelse: Array vs Länkad Lista

```
┌────────────────────────────────────────────────────────────────────┐
│              ARRAY vs LÄNKAD LISTA                                │
├─────────────────────┬──────────────────────┬──────────────────────┤
│  Egenskap           │  Array               │  Länkad lista        │
├─────────────────────┼──────────────────────┼──────────────────────┤
│  Indexerad åtkomst  │  O(1) ✓              │  O(N) ✗              │
├─────────────────────┼──────────────────────┼──────────────────────┤
│  Infoga i början    │  O(N) ✗              │  O(1) ✓              │
├─────────────────────┼──────────────────────┼──────────────────────┤
│  Infoga i slutet    │  O(1) amorterat      │  O(1) ✓              │
├─────────────────────┼──────────────────────┼──────────────────────┤
│  Minnesanvändning   │  Fast storlek*       │  Proportionell       │
├─────────────────────┼──────────────────────┼──────────────────────┤
│  Overhead per elem  │  Ingen               │  Referens (8 bytes)  │
├─────────────────────┼──────────────────────┼──────────────────────┤
│  Cache-prestanda    │  Utmärkt ✓           │  Dålig ✗             │
└─────────────────────┴──────────────────────┴──────────────────────┘

* Med resizing array hålls storleken inom konstant faktor av N
```

### Proposition D

> **Proposition D:** I länkade list-implementationer av Bag, Stack och Queue tar alla operationer **konstant tid i värsta fall**.

---

## 🔑 Sammanfattning Del 1 (Avsnitt 1.3)

### Nyckelkoncept

- **Generics** låter oss skriva en implementation för alla datatyper
- **Autoboxing** konverterar automatiskt mellan primitiver och wrappers
- **Iterable** möjliggör foreach-iteration
- **Resizing arrays** ger amorterad konstant tid
- **Länkade listor** ger konstant tid i värsta fall

### Minnesregel: GAILS

```
G - Generics (en implementation för alla typer)
A - Autoboxing (primitiv ↔ wrapper)
I - Iterable (foreach-stöd)
L - Linked lists (konstant tid)
S - Stacks & Queues (LIFO vs FIFO)
```

---

# Del 2: Elementära Sorteringsalgoritmer (Avsnitt 2.1)

---

## 🎯 Introduktion till Sortering

### Varför Studera Sortering?

1. **Kontext** – Lär oss terminologi och grundläggande mekanismer
2. **Praktiskt användbar** – Ibland är enkla algoritmer tillräckliga
3. **Byggstenar** – Används för att förbättra mer avancerade algoritmer

### Spelreglerna

**Mål:** Ordna en array så att varje elements nyckel inte är mindre än nyckeln till vänster och inte större än nyckeln till höger.

```java
public class Example {
    public static void sort(Comparable[] a) {
        // Sorteringsalgoritmen
    }
    
    private static boolean less(Comparable v, Comparable w) {
        return v.compareTo(w) < 0;
    }
    
    private static void exch(Comparable[] a, int i, int j) {
        Comparable t = a[i];
        a[i] = a[j];
        a[j] = t;
    }
    
    private static void show(Comparable[] a) {
        for (int i = 0; i < a.length; i++)
            StdOut.print(a[i] + " ");
        StdOut.println();
    }
    
    public static boolean isSorted(Comparable[] a) {
        for (int i = 1; i < a.length; i++)
            if (less(a[i], a[i-1])) return false;
        return true;
    }
}
```

### Comparable-gränssnittet

```java
public class Date implements Comparable<Date> {
    private final int day;
    private final int month;
    private final int year;
    
    public int compareTo(Date that) {
        if (this.year  > that.year)  return +1;
        if (this.year  < that.year)  return -1;
        if (this.month > that.month) return +1;
        if (this.month < that.month) return -1;
        if (this.day   > that.day)   return +1;
        if (this.day   < that.day)   return -1;
        return 0;
    }
}
```

---

## 🔍 Selection Sort (Urvalssortering)

### Algoritm

1. Hitta det **minsta** elementet i arrayen
2. Byt det med **första** elementet
3. Hitta det **näst minsta** elementet
4. Byt det med **andra** elementet
5. Fortsätt tills hela arrayen är sorterad

### Implementation (Algoritm 2.1)

```java
public class Selection {
    public static void sort(Comparable[] a) {
        int N = a.length;
        for (int i = 0; i < N; i++) {
            int min = i;  // Index för minsta elementet
            for (int j = i + 1; j < N; j++) {
                if (less(a[j], a[min])) 
                    min = j;
            }
            exch(a, i, min);
        }
    }
}
```

### Visuell Spårning

```
         a[]
i  min   0  1  2  3  4  5  6  7  8  9  10
         S  O  R  T  E  X  A  M  P  L  E
0   6    A  O  R  T  E  X  S  M  P  L  E    ← A är minst, byt med S
1   4    A  E  R  T  O  X  S  M  P  L  E    ← E är minst, byt med O
2  10    A  E  E  T  O  X  S  M  P  L  R    ← E är minst, byt med R
3   9    A  E  E  L  O  X  S  M  P  T  R    ← L är minst, byt med T
...
         A  E  E  L  M  O  P  R  S  T  X    ← Sorterad!
```

### Proposition A

> **Proposition A:** Selection sort använder **~N²/2 jämförelser** och **N byten** för att sortera en array med N element.

**Bevis:**
- För varje i från 0 till N-1 finns det (N-1-i) jämförelser
- Totalt: (N-1) + (N-2) + ... + 1 + 0 = N(N-1)/2 ≈ N²/2
- Exakt N byten (ett per position)

### Egenskaper hos Selection Sort

```
┌─────────────────────────────────────────────────────────────────────┐
│  EGENSKAPER HOS SELECTION SORT                                     │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ✓ Datarörelser är minimala (N byten)                              │
│                                                                     │
│  ✗ Körtid OBEROENDE av indata (alltid ~N²/2 jämförelser)           │
│    • Redan sorterad array? ~N²/2 jämförelser                       │
│    • Slumpmässig array? ~N²/2 jämförelser                          │
│    • Omvänd ordning? ~N²/2 jämförelser                             │
│                                                                     │
│  Använd när: Byten är dyra (stora objekt)                          │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 🃏 Insertion Sort (Insättningssortering)

### Algoritm

1. Gå igenom arrayen från vänster till höger
2. För varje element, flytta det **bakåt** till dess rätta position bland de redan sorterade elementen till vänster

**Analogi:** Som att sortera ett kortspel – du tar ett kort i taget och sätter in det på rätt plats bland de kort du redan håller.

### Implementation (Algoritm 2.2)

```java
public class Insertion {
    public static void sort(Comparable[] a) {
        int N = a.length;
        for (int i = 1; i < N; i++) {
            for (int j = i; j > 0 && less(a[j], a[j-1]); j--) {
                exch(a, j, j-1);
            }
        }
    }
}
```

### Visuell Spårning

```
         a[]
i  j     0  1  2  3  4  5  6  7  8  9  10
         S  O  R  T  E  X  A  M  P  L  E
1  0     O  S  R  T  E  X  A  M  P  L  E    ← O flyttas förbi S
2  1     O  R  S  T  E  X  A  M  P  L  E    ← R stannar mellan O och S
3  3     O  R  S  T  E  X  A  M  P  L  E    ← T stannar (redan rätt)
4  0     E  O  R  S  T  X  A  M  P  L  E    ← E flyttas hela vägen
5  5     E  O  R  S  T  X  A  M  P  L  E    ← X stannar
6  0     A  E  O  R  S  T  X  M  P  L  E    ← A flyttas hela vägen
...
         A  E  E  L  M  O  P  R  S  T  X    ← Sorterad!
```

### Proposition B

> **Proposition B:** Insertion sort använder i genomsnitt **~N²/4 jämförelser** och **~N²/4 byten** för att sortera en slumpmässigt ordnad array med N distinkta nycklar.
>
> **Värsta fall:** ~N²/2 jämförelser och ~N²/2 byten (omvänd ordning)
> **Bästa fall:** N-1 jämförelser och 0 byten (redan sorterad)

### Inversioner och Delvis Sorterade Arrayer

**Definition:** En **inversion** är ett par element som är i fel ordning.

**Exempel:** E X A M P L E har 11 inversioner:
E-A, X-A, X-M, X-P, X-L, X-E, M-L, M-E, P-L, P-E, L-E

**Definition:** En array är **delvis sorterad** om antalet inversioner är O(N).

**Exempel på delvis sorterade arrayer:**
- Array där varje element är nära sin slutposition
- En liten array tillagd till en stor sorterad array
- En array med bara några få element på fel plats

### Proposition C

> **Proposition C:** Antalet byten i insertion sort är lika med antalet inversioner, och antalet jämförelser är minst antalet inversioner och högst antalet inversioner plus N-1.

**Konsekvens:** Insertion sort är **utmärkt för delvis sorterade arrayer!**

### Jämförelse: Selection Sort vs Insertion Sort

```
┌─────────────────────────────────────────────────────────────────────┐
│           SELECTION SORT vs INSERTION SORT                         │
├──────────────────────────┬──────────────────────────────────────────┤
│  Aspekt                  │  Selection      │  Insertion            │
├──────────────────────────┼─────────────────┼───────────────────────┤
│  Jämförelser (genomsn.)  │  ~N²/2          │  ~N²/4                │
├──────────────────────────┼─────────────────┼───────────────────────┤
│  Byten (genomsnitt)      │  N              │  ~N²/4                │
├──────────────────────────┼─────────────────┼───────────────────────┤
│  Redan sorterad          │  ~N²/2          │  N-1 jämförelser! ✓   │
├──────────────────────────┼─────────────────┼───────────────────────┤
│  Omvänd ordning          │  ~N²/2          │  ~N²/2                │
├──────────────────────────┼─────────────────┼───────────────────────┤
│  Delvis sorterad         │  ~N²/2          │  Linjär! ✓            │
├──────────────────────────┼─────────────────┼───────────────────────┤
│  Bäst när                │  Dyra byten     │  Nästan sorterat      │
└──────────────────────────┴─────────────────┴───────────────────────┘
```

### Property D

> **Property D:** Körtiderna för insertion sort och selection sort är kvadratiska och inom en liten konstant faktor från varandra för slumpmässigt ordnade arrayer med distinkta värden.

---

## 🐚 Shellsort

### Motivering

**Problem med insertion sort:** Element kan bara flyttas ett steg åt gången.

**Idé:** Tillåt byten av element som är **långt ifrån varandra** för att snabbt reducera oordning.

### h-sortering

**Definition:** En array är **h-sorterad** om varje h:te element (med start var som helst) bildar en sorterad delsekvens.

```
┌─────────────────────────────────────────────────────────────────────┐
│  h-SORTERAD ARRAY (h = 4)                                          │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  Index:  0  1  2  3  4  5  6  7  8  9 10 11 12 13 14 15            │
│  Array:  L  E  E  A  M  H  L  E  P  S  O  L  T  S  X  R            │
│                                                                     │
│  Delsekvens 1 (start 0): L ─── M ─── P ─── T    (sorterad)         │
│  Delsekvens 2 (start 1): E ─── H ─── S ─── S    (sorterad)         │
│  Delsekvens 3 (start 2): E ─── L ─── O ─── X    (sorterad)         │
│  Delsekvens 4 (start 3): A ─── E ─── L ─── R    (sorterad)         │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Algoritm

1. Välj en sekvens av h-värden som slutar med 1
2. h-sortera arrayen för varje h (med insertion sort)
3. När h = 1 blir arrayen helt sorterad

### Implementation (Algoritm 2.3)

```java
public class Shell {
    public static void sort(Comparable[] a) {
        int N = a.length;
        int h = 1;
        
        // Beräkna startväde för h (sekvens: 1, 4, 13, 40, 121, ...)
        while (h < N/3) h = 3*h + 1;
        
        while (h >= 1) {
            // h-sortera arrayen med insertion sort
            for (int i = h; i < N; i++) {
                for (int j = i; j >= h && less(a[j], a[j-h]); j -= h) {
                    exch(a, j, j-h);
                }
            }
            h = h/3;  // Nästa h
        }
    }
}
```

### Inkrementsekvenser

Boken använder **3x + 1**: 1, 4, 13, 40, 121, 364, ...

Andra sekvenser har studerats:
- **Knuths:** 1, 4, 13, 40, 121, ... (3x + 1)
- **Sedgwick:** 1, 5, 19, 41, 109, ... (mer komplicerad)

> ⚠️ **Ingen bevisbart optimal sekvens har hittats!**

### Visuell Spårning

```
input        S  H  E  L  L  S  O  R  T  E  X  A  M  P  L  E
13-sort      P  H  E  L  L  S  O  R  T  E  X  A  M  S  L  E
4-sort       L  E  E  A  M  H  L  E  P  S  O  L  T  S  X  R
1-sort       A  E  E  E  H  L  L  L  M  O  P  R  S  S  T  X
```

### Prestandaanalys

```
┌─────────────────────────────────────────────────────────────────────┐
│  SHELLSORT PRESTANDA                                               │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  Värsta fall (3x+1 sekvens): O(N^(3/2))                            │
│                                                                     │
│  I praktiken: Betydligt bättre än N²                               │
│                                                                     │
│  Jämförelse med N = 100 000:                                       │
│  • Selection sort: ~10 000 000 000 operationer                     │
│  • Insertion sort: ~10 000 000 000 operationer (värsta fall)       │
│  • Shellsort:      ~   1 000 000 operationer                       │
│                                                                     │
│  Shellsort är ~600x snabbare än insertion sort för stora N!        │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### Varför Shellsort Fungerar

1. **Stora h-värden** flyttar element snabbt över långa avstånd
2. **Små h-värden** finjusterar ordningen
3. **h-sorterade arrayer förblir h-sorterade** efter (h/3)-sortering

> 💡 **Praktiskt tips:** Shellsort är ett bra val när du behöver en enkel, snabb algoritm och inte vill implementera mer komplicerade algoritmer.

---

## 📊 Jämföra Sorteringsalgoritmer

### SortCompare

```java
public class SortCompare {
    public static double time(String alg, Double[] a) {
        Stopwatch timer = new Stopwatch();
        if (alg.equals("Insertion")) Insertion.sort(a);
        if (alg.equals("Selection")) Selection.sort(a);
        if (alg.equals("Shell"))     Shell.sort(a);
        return timer.elapsedTime();
    }
    
    public static double timeRandomInput(String alg, int N, int T) {
        double total = 0.0;
        Double[] a = new Double[N];
        for (int t = 0; t < T; t++) {
            for (int i = 0; i < N; i++)
                a[i] = StdRandom.uniform();
            total += time(alg, a);
        }
        return total;
    }
}
```

### Typiska Resultat

```
% java SortCompare Shell Insertion 100000 100
For 100000 random Doubles
    Shell is 600 times faster than Insertion
```

---

## 👁️ Visuella Spår

### Visualisering med Staplar

```
┌─────────────────────────────────────────────────────────────────────┐
│  INSERTION SORT                    SELECTION SORT                  │
│  (sorterar vänster→höger)          (sorterar vänster→höger)        │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  █                                 █                                │
│  ██                                ██                               │
│  ███                               ███                              │
│  ████  ← Sorterat                  ████  ← Sorterat                 │
│  █████                             █████                            │
│                                                                     │
│  Rör element                       Rör INTE element                 │
│  till VÄNSTER om pekaren           till VÄNSTER om pekaren          │
│                                                                     │
│  Rör INTE element                  Rör element                      │
│  till HÖGER om pekaren             till HÖGER om pekaren            │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 📋 Sammanfattande Jämförelse

```
┌─────────────────────────────────────────────────────────────────────┐
│              JÄMFÖRELSE AV ELEMENTÄRA SORTERINGSALGORITMER         │
├────────────────┬───────────────┬──────────────┬─────────────────────┤
│  Algoritm      │  Tid (genomsn)│  Tid (värsta)│  Extra minne        │
├────────────────┼───────────────┼──────────────┼─────────────────────┤
│  Selection     │  ~N²/2        │  ~N²/2       │  1                  │
│  Insertion     │  ~N²/4        │  ~N²/2       │  1                  │
│  Shellsort     │  ?            │  O(N^(3/2))  │  1                  │
├────────────────┼───────────────┼──────────────┼─────────────────────┤
│  Bäst för:                                                         │
│  • Selection: Dyra byten, minnesbegränsning                        │
│  • Insertion: Nästan sorterade arrayer, små arrayer                │
│  • Shellsort: Medelstora arrayer, enkel implementation             │
└────────────────┴───────────────┴──────────────┴─────────────────────┘
```

---

## ❓ Vanliga Frågor (Q&A)

### F: Varför behöver vi så många sorteringsalgoritmer?

**S:** Prestanda beror på indata. Olika algoritmer är bättre för olika situationer. Insertion sort är bäst för nästan sorterade arrayer, selection sort är bra när byten är dyra.

### F: Varför används hjälpfunktionerna less() och exch()?

**S:** De är abstrakta operationer som behövs av alla sorteringsalgoritmer. Koden blir tydligare och lättare att porta till andra språk eller situationer (t.ex. sortering av primitiva typer).

### F: Varför olika resultat varje gång jag kör SortCompare?

**S:** Dator, operativsystem, JVM och bakgrundsprocesser påverkar. Kör många försök och ta medelvärde för mer tillförlitliga resultat.

---

## 🎯 Praktiska Övningar

### Från Boken

**2.1.1** Visa hur selection sort sorterar E A S Y Q U E S T I O N.

**2.1.4** Visa hur insertion sort sorterar E A S Y Q U E S T I O N.

**2.1.6** Vilken metod är snabbare för en array där alla nycklar är identiska?
> **Svar:** Insertion sort (linjär tid) – selection sort är fortfarande kvadratisk.

**2.1.7** Vilken metod är snabbare för en array i omvänd ordning?
> **Svar:** Lika – båda är kvadratiska i värsta fall.

**2.1.9** Visa hur shellsort sorterar E A S Y S H E L L S O R T Q U E S T I O N.

---

## 🔑 Sammanfattning Del 2 (Avsnitt 2.1)

### Nyckelkoncept

- **Selection sort:** Hitta minsta, byt med första – alltid ~N²/2 jämförelser
- **Insertion sort:** Sätt in på rätt plats – utmärkt för delvis sorterade arrayer
- **Shellsort:** h-sortering med minskande h – subkvadratisk, praktiskt snabb
- **Inversioner:** Mått på oordning – direkt koppling till insertion sorts prestanda

### Minnesregel: SISH

```
S - Selection sort (minsta först, N byten)
I - Insertion sort (sätt in på plats, bra för nästan sorterat)
S - Shellsort (h-sortering, snabbare än kvadratisk)
H - Hjälpfunktioner (less, exch, isSorted)
```

### När Använda Vilken?

| Situation | Rekommendation |
|-----------|----------------|
| Nästan sorterad array | Insertion sort |
| Små arrayer (<50 element) | Insertion sort |
| Dyra byten | Selection sort |
| Medelstora arrayer | Shellsort |
| Stora arrayer | Mergesort/Quicksort (kapitel 2.2-2.3) |

---

## 📖 Framåtblick

I nästa avsnitt (2.2 och 2.3) behandlas:
- **Mergesort** – N log N garanterat, dela-och-härska
- **Quicksort** – N log N i genomsnitt, på plats

Dessa algoritmer är **betydligt snabbare** för stora arrayer!

---

*Detta material är baserat på "Algorithms, 4th Edition" av Robert Sedgewick och Kevin Wayne.*
