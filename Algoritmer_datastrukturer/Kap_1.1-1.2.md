# Omfattande Sammanfattning: Kapitel 1.1 och 1.2 
## Algorithms (4th Edition) av Sedgewick & Wayne

---

## 📚 Kapitel 1.1: Basic Programming Model (Grundläggande Programmeringsmodell)

### 🎯 Översikt och Syfte

Detta kapitel introducerar den grundläggande programmeringsmodellen som används genom hela boken. Alla program är implementerade i **Java**, vilket ger flera fördelar:

✅ **Fördelar med Java-implementationer:**
- Programmen är **koncisa, eleganta och kompletta beskrivningar** av algoritmer
- Du kan **köra programmen** för att studera algoritmernas egenskaper
- Du kan **omedelbart använda algoritmerna** i praktiska tillämpningar

**Programmeringsmodell** = de programmeringskonstruktioner, mjukvarubibliotek och operativsystemsfunktioner som används för att implementera och beskriva algoritmer.

---

### 1️⃣ Primitiva Datatyper och Uttryck

#### 🔢 De Fyra Grundläggande Datatyperna

Java bygger på fyra primitiva datatyper:

1. **`int`** - Heltal (integers)
   - Värden: heltal mellan -2³¹ och 2³¹ - 1
   - Operationer: `+`, `-`, `*`, `/`, `%` (modulo)
   - Exempel: `42`, `-17`, `0`

2. **`double`** - Reella tal (flyttal)
   - Värden: reella tal med decimaler
   - Operationer: `+`, `-`, `*`, `/`, `Math.sqrt()`, `Math.sin()`, etc.
   - Exempel: `3.14159`, `-2.5`, `1.0e-15`

3. **`boolean`** - Sanningsvärden
   - Värden: endast `true` eller `false`
   - Operationer: `&&` (AND), `||` (OR), `!` (NOT)
   - Exempel: `true`, `false`

4. **`char`** - Tecken
   - Värden: alfanumeriska tecken och symboler
   - Omges av enkla citattecken
   - Exempel: `'a'`, `'Z'`, `'9'`, `'\n'` (newline)

#### 📝 Viktiga Begrepp

**Identifierare (Identifier):**
- Namn på variabler (t.ex. `count`, `myVariable`, `x`)
- Består av bokstäver, siffror, `_` och `$`
- Får **inte** börja med en siffra
- Exempel: `a`, `abc`, `Ab$`, `a_b`, `ab123`

**Variabel:**
- Namnger ett datatyp-värde
- Måste deklareras med en typ: `int x;` eller `double pi = 3.14;`

**Operator:**
- Symbol som anger en operation
- Exempel: `+`, `-`, `*`, `/`, `<`, `>`

**Literal:**
- Direkt representation av ett värde i källkoden
- `int`: `1`, `0`, `-42`
- `double`: `2.0`, `1.0e-15`, `3.14`
- `boolean`: `true`, `false`
- `char`: `'a'`, `'+'`, `'9'`, `'\n'`

**Uttryck (Expression):**
- En literal, en variabel, eller en sekvens av operationer
- Producerar ett värde
- Exempel: 
  - `lo + (hi - lo)/2` (int-uttryck)
  - `1.0e-15 * t` (double-uttryck)
  - `lo <= hi` (boolean-uttryck)

---

### 2️⃣ Statements (Satser)

Java använder **sex typer av statements** för att definiera beräkningar:

#### **A. Deklarationer (Declarations)**
```java
int i;           // Deklarera en variabel
double c;        // Deklarera en double
int i = 1;       // Initialiserande deklaration
double c = 3.14; // Deklarera och tilldela direkt
```

#### **B. Tilldelningar (Assignments)**
```java
a = b + 3;
discriminant = b*b - 4.0*c;
i++;              // Samma som i = i + 1
i += 1;           // Samma som i = i + 1
```

#### **C. Villkorssatser (Conditionals)**

**if-sats:**
```java
if (x < 0) 
    x = -x;  // Exekvera om villkoret är sant
```

**if-else-sats:**
```java
if (x > y) 
    max = x;
else 
    max = y;
```

💡 **Tips:** Använd alltid klammerparenteser `{}` för tydlighet:
```java
if (x > y) {
    max = x;
} else {
    max = y;
}
```

#### **D. Loopar (Loops)**

**while-loop:**
```java
int v = 0;
while (v <= N) {
    v = 2*v;
}
```

```java
double t = c;
while (Math.abs(t - c/t) > 1e-15*t) {
    t = (c/t + t) / 2.0;
}
```

**for-loop:**
```java
for (int i = 1; i <= N; i++) {
    sum += 1.0/i;
}
```

**for-loop struktur:**
```java
for (<initialize>; <boolean expression>; <increment>) {
    <block statements>
}
```

Detta är ekvivalent med:
```java
<initialize>;
while (<boolean expression>) {
    <block statements>
    <increment>;
}
```

#### **E. Metodanrop (Calls)**
```java
int key = StdIn.readInt();
```

#### **F. Return-satser**
```java
return false;
return mid;
```

---

### 3️⃣ Arrayer (Arrays)

En **array** lagrar en sekvens av värden av samma typ. Värden numreras från **0** till **N-1**.

#### 📦 Skapa och Initialisera Arrayer

**Tre steg för att skapa en array:**

1. **Deklarera arrayen:**
```java
double[] a;    // Deklarera en array av doubles
int[] values;  // Deklarera en array av ints
```

2. **Skapa arrayen:**
```java
a = new double[N];  // Skapa array med N element
```

3. **Initialisera värdena:**
```java
for (int i = 0; i < N; i++)
    a[i] = 0.0;
```

**Kortform (deklarera, skapa och initialisera):**
```java
double[] a = new double[N];  // Alla element sätts till 0.0
int[] b = new int[10];       // Alla element sätts till 0
boolean[] flags = new boolean[5]; // Alla element sätts till false
```

**Initialisera med specifika värden:**
```java
int[] primes = {2, 3, 5, 7, 11, 13};
String[] names = {"Alice", "Bob", "Charlie"};
```

#### 🔍 Använda Arrayer

**Komma åt element:**
```java
a[i]           // Element vid index i
a[0]           // Första elementet
a[a.length-1]  // Sista elementet
```

**Arraylängd:**
```java
int N = a.length;  // Längden på arrayen a
```

⚠️ **Viktigt:** Java gör automatisk gränskontroll (bounds checking):
- Om du använder index < 0 eller >= N får du ett `ArrayOutOfBoundsException`

#### 🔄 Vanliga Array-operationer

**Hitta maximum:**
```java
double max = a[0];
for (int i = 1; i < a.length; i++)
    if (a[i] > max) 
        max = a[i];
```

**Beräkna medelvärde:**
```java
int N = a.length;
double sum = 0.0;
for (int i = 0; i < N; i++)
    sum += a[i];
double average = sum / N;
```

**Kopiera en array:**
```java
int N = a.length;
double[] b = new double[N];
for (int i = 0; i < N; i++)
    b[i] = a[i];
```

❌ **Fel sätt:** `double[] b = a;` - Detta skapar bara en **alias** (referens), inte en kopia!

**Vända ordning på element:**
```java
int N = a.length;
for (int i = 0; i < N/2; i++) {
    double temp = a[i];
    a[i] = a[N-1-i];
    a[N-i-1] = temp;
}
```

#### 📊 Tvådimensionella Arrayer

En **tvådimensionell array** är en array av arrayer.

**Skapa en M×N array:**
```java
double[][] a = new double[M][N];
```

**Långform:**
```java
double[][] a;
a = new double[M][N];
for (int i = 0; i < M; i++)
    for (int j = 0; j < N; j++)
        a[i][j] = 0.0;
```

**Komma åt element:**
```java
a[i][j]  // Element i rad i, kolumn j
```

**Matris-matris multiplikation (kvadratiska matriser):**
```java
int N = a.length;
double[][] c = new double[N][N];
for (int i = 0; i < N; i++)
    for (int j = 0; j < N; j++) {
        // Beräkna skalärprodukten av rad i och kolumn j
        for (int k = 0; k < N; k++)
            c[i][j] += a[i][k] * b[k][j];
    }
```

---

### 4️⃣ Statiska Metoder (Static Methods)

**Statiska metoder** är som matematiska funktioner - de tar argument och returnerar ett värde eller orsakar en bieffekt.

#### 🏗️ Definiera en Statisk Metod

**Metodsignatur:**
```java
public static <returnType> <methodName>(<paramType> <paramName>, ...)
```

**Exempel:**
```java
public static int abs(int x) {
    if (x < 0) 
        return -x;
    else 
        return x;
}
```

```java
public static double sqrt(double c) {
    if (c < 0) 
        return Double.NaN;  // Not a Number
    double err = 1e-15;
    double t = c;
    while (Math.abs(t - c/t) > err * t)
        t = (c/t + t) / 2.0;
    return t;
}
```

#### 📞 Anropa Metoder

```java
int result = abs(-5);          // result blir 5
double sqrtVal = sqrt(2.0);    // Newtons metod för kvadratrot
```

#### 🔁 Rekursion

En metod kan **anropa sig själv** - detta kallas rekursion.

**Exempel: Binär sökning (rekursiv version):**
```java
public static int rank(int key, int[] a) {
    return rank(key, a, 0, a.length - 1);
}

public static int rank(int key, int[] a, int lo, int hi) {
    // Index för key i a[], om den finns, är inte mindre än lo
    // och inte större än hi.
    if (lo > hi) 
        return -1;
    int mid = lo + (hi - lo) / 2;
    if (key < a[mid]) 
        return rank(key, a, lo, mid - 1);
    else if (key > a[mid]) 
        return rank(key, a, mid + 1, hi);
    else 
        return mid;
}
```

**Hur rekursion fungerar:**
1. Basfall: `if (lo > hi) return -1;` - stoppar rekursionen
2. Rekursivt anrop: metoden anropar sig själv med mindre problem
3. Varje anrop får sin egen kopia av parametrar och lokala variabler

#### 📦 Scope (Räckvidd)

**Lokala variabler:**
- Deklareras inuti en metod
- Kan endast användas inom den metoden
- Försvinner när metoden returnerar

**Parametrar:**
- Värden som skickas in till metoden
- Har scope över hela metoden

#### 🔄 Pass by Value

Java använder **pass by value** för alla argument:
- För primitiva typer: värdet kopieras
- För arrayer och objekt: referensen kopieras (men objektet själv kopieras inte)

```java
public static void change(int x) {
    x = 42;  // Ändrar endast lokal kopia
}

int a = 10;
change(a);
// a är fortfarande 10!
```

Men för arrayer:
```java
public static void changeArray(int[] arr) {
    arr[0] = 99;  // Ändrar det faktiska array-objektet
}

int[] myArray = {1, 2, 3};
changeArray(myArray);
// myArray[0] är nu 99!
```

---

### 5️⃣ Binär Sökning - Exempel

**Binär sökning** är en effektiv algoritm för att hitta ett värde i en **sorterad** array.

#### 🎯 Algoritmen

```java
public static int rank(int key, int[] a) {
    // Array måste vara sorterad
    int lo = 0;
    int hi = a.length - 1;
    while (lo <= hi) {
        // key finns i a[lo..hi] eller finns inte alls
        int mid = lo + (hi - lo) / 2;
        if (key < a[mid]) 
            hi = mid - 1;
        else if (key > a[mid]) 
            lo = mid + 1;
        else 
            return mid;
    }
    return -1;  // key hittades inte
}
```

#### 📖 Hur det fungerar:

1. **Initialisering:** `lo = 0`, `hi = array.length - 1`
2. **Loop:** Så länge `lo <= hi`:
   - Beräkna mittpunkt: `mid = lo + (hi - lo) / 2`
   - Jämför `key` med `a[mid]`:
     - Om `key < a[mid]`: sök i vänstra halvan (`hi = mid - 1`)
     - Om `key > a[mid]`: sök i högra halvan (`lo = mid + 1`)
     - Om lika: returnera `mid` (hittat!)
3. **Ej hittad:** Om loopen slutar utan att hitta, returnera `-1`

#### ⚡ Prestanda

- Binär sökning behöver endast undersöka **~log₂ N** element
- För N = 1 000 000: endast ~20 jämförelser behövs!
- **Mycket snabbare** än linjär sökning (brute-force) som behöver undersöka alla N element

**Exempel:**
- Array med 1000 element: max 10 jämförelser
- Array med 1 000 000 element: max 20 jämförelser
- Array med 1 000 000 000 element: max 30 jämförelser

---

### 6️⃣ Strings (Strängar)

**String** är en sekvens av tecken och är en **referenstyp** (inte primitiv).

#### 🔤 Skapa Strings

```java
String s1 = "Hello";
String s2 = "World";
String empty = "";
```

#### 🛠️ Vanliga String-operationer

**Konkatenering (sammanslagning):**
```java
String a = "Hello";
String b = " World";
String c = a + b;  // "Hello World"
String d = a + "!"; // "Hello!"
```

**Längd:**
```java
String s = "Hello";
int len = s.length();  // 5
```

**Komma åt tecken:**
```java
String s = "Hello";
char ch = s.charAt(0);  // 'H'
char ch2 = s.charAt(4); // 'o'
```

**Substring (delsträng):**
```java
String s = "Hello World";
String sub = s.substring(0, 5);  // "Hello" (tecken 0 till 4)
String sub2 = s.substring(6, 11); // "World"
```

**Hitta index:**
```java
String s = "Hello World";
int index = s.indexOf("World");  // 6
int index2 = s.indexOf("o");     // 4 (första förekomsten)
```

**Dela upp sträng:**
```java
String s = "one two three";
String[] words = s.split(" ");  // ["one", "two", "three"]
```

**Jämföra strängar:**
```java
String s1 = "Hello";
String s2 = "Hello";
String s3 = "World";

boolean b1 = s1.equals(s2);      // true
boolean b2 = s1.equals(s3);      // false
int cmp = s1.compareTo(s3);      // negativt tal (H kommer före W)
```

❌ **Använd INTE** `==` för att jämföra strängar!
✅ **Använd** `equals()` metoden

**Konvertera till/från primitiva typer:**
```java
// String till int
String numStr = "42";
int num = Integer.parseInt(numStr);  // 42

// String till double
String piStr = "3.14";
double pi = Double.parseDouble(piStr);  // 3.14

// int till String
int x = 123;
String s = Integer.toString(x);  // "123"
// eller
String s2 = "" + x;  // "123" (implicit konvertering)
```

#### 📝 Exempel: Kontrollera om palindrom

```java
public static boolean isPalindrome(String s) {
    int N = s.length();
    for (int i = 0; i < N/2; i++)
        if (s.charAt(i) != s.charAt(N-1-i))
            return false;
    return true;
}
```

---

### 7️⃣ Input och Output

#### 📥 Standard Input (StdIn)

**Läsa olika typer av data:**

```java
int i = StdIn.readInt();         // Läs ett heltal
double d = StdIn.readDouble();   // Läs ett flyttal
String s = StdIn.readString();   // Läs en sträng (ord)
String line = StdIn.readLine();  // Läs en hel rad
```

**Kontrollera om mer input finns:**
```java
while (!StdIn.isEmpty()) {
    int value = StdIn.readInt();
    // bearbeta value...
}
```

**Läsa en hel fil:**
```java
String content = StdIn.readAll();
```

#### 📤 Standard Output (StdOut)

```java
StdOut.print("Hello");           // Skriv utan newline
StdOut.println("World");         // Skriv med newline
StdOut.printf("%.2f", 3.14159);  // Formaterad output: "3.14"
```

#### 🎨 Formatted Output med printf

```java
StdOut.printf("%d bottles of beer\n", 99);
StdOut.printf("%.2f%%\n", 100.0 * ratio);
StdOut.printf("%10s %5d %7.2f\n", name, count, price);
```

**Format-specifikare:**
- `%d` - heltal (int)
- `%f` - flyttal (double)
- `%.2f` - flyttal med 2 decimaler
- `%s` - sträng
- `%10s` - sträng med minst 10 tecken (högerställd)
- `%-10s` - sträng med minst 10 tecken (vänsterställd)

---

### 8️⃣ Kommandoradsargument

**main()**-metoden tar en array av strängar som argument:

```java
public static void main(String[] args) {
    // args[0] är första argumentet
    // args[1] är andra argumentet, osv.
}
```

**Exempel:**
```bash
java MyProgram hello world 42
```

```java
public static void main(String[] args) {
    String first = args[0];   // "hello"
    String second = args[1];  // "world"
    int num = Integer.parseInt(args[2]);  // 42
}
```

---

### 9️⃣ Java-bibliotek

#### 🧮 Math-biblioteket

```java
double pi = Math.PI;              // π ≈ 3.14159...
double e = Math.E;                // e ≈ 2.71828...

double sqrtVal = Math.sqrt(2.0);  // Kvadratrot
double absVal = Math.abs(-5);     // Absolutvärde: 5
double maxVal = Math.max(3, 7);   // Maximum: 7
double minVal = Math.min(3, 7);   // Minimum: 3

double sinVal = Math.sin(Math.PI/2);  // sin(π/2) = 1.0
double cosVal = Math.cos(0);          // cos(0) = 1.0
double powVal = Math.pow(2, 3);       // 2³ = 8.0
double logVal = Math.log(Math.E);     // ln(e) = 1.0

double random = Math.random();    // Slumptal mellan 0.0 och 1.0
```

#### 📊 Arrays-biblioteket

```java
import java.util.Arrays;

int[] numbers = {5, 2, 8, 1, 9};
Arrays.sort(numbers);  // Sorterar arrayen: {1, 2, 5, 8, 9}
```

---

### 🔟 Modulär Programmering

**Viktiga principer:**

1. **Separation of concerns:** Dela upp kod i små, oberoende moduler
2. **Återanvändbarhet:** Skriv metoder som kan användas i många sammanhang
3. **Testbarhet:** Varje modul bör ha en `main()` för unit testing
4. **API som kontrakt:** API:et definierar vad klienten kan förvänta sig

**Exempel: BinarySearch**

```java
public class BinarySearch {
    // Statisk metod för binär sökning
    public static int rank(int key, int[] a) {
        // ... implementation ...
    }
    
    // Test-klient
    public static void main(String[] args) {
        int[] whitelist = In.readInts(args[0]);
        Arrays.sort(whitelist);
        
        while (!StdIn.isEmpty()) {
            int key = StdIn.readInt();
            if (rank(key, whitelist) == -1)
                StdOut.println(key);
        }
    }
}
```

**Fördelar:**
- ✅ Moduler av rimlig storlek
- ✅ Dela och återanvänd kod
- ✅ Enkelt att byta ut implementationer
- ✅ Lättare debugging (unit testing)

---

## 📚 Kapitel 1.2: Data Abstraction (Dataabstraktion)

### 🎯 Översikt och Motivation

**Datatyp** = en uppsättning värden + en uppsättning operationer på dessa värden

**Primitiva datatyper** (som vi såg i 1.1):
- `int`, `double`, `boolean`, `char`
- Begränsade till numeriska och logiska operationer

**Abstract Data Type (ADT)** = en datatyp vars representation är **dold** från klienten
- Klienten fokuserar på **vad** operationerna gör
- Implementationen fokuserar på **hur** data representeras och manipuleras

**Fördelar med ADT:**
- ✅ **Inkapsling (Encapsulation):** Data och operationer samlas i en enhet
- ✅ **Modularitet:** Klient och implementation kan utvecklas oberoende
- ✅ **Återanvändbarhet:** Samma ADT kan användas av många klienter
- ✅ **Substituerbarhet:** Kan byta implementation utan att ändra klientkod
- ✅ **Abstraktion:** Jobba på högre nivå, fokusera på problemet, inte detaljer

---

### 1️⃣ Använda Abstract Data Types

#### 📊 Exempel: Counter ADT

**API (Application Programming Interface):**

```java
public class Counter
    Counter(String id)     // Skapa en räknare med namn id
    void increment()       // Öka räknaren med 1
    int tally()           // Antal ökningar sedan skapandet
    String toString()     // Strängrepresentation
```

**Klientkod - exempel 1: Räkna tärningskast**

```java
public class Rolls {
    public static void main(String[] args) {
        int T = Integer.parseInt(args[0]);
        int SIDES = 6;
        Counter[] rolls = new Counter[SIDES+1];
        
        // Skapa räknare för varje sida
        for (int i = 1; i <= SIDES; i++)
            rolls[i] = new Counter(i + "'s");
        
        // Simulera T kast
        for (int t = 0; t < T; t++) {
            int result = StdRandom.uniform(1, SIDES+1);
            rolls[result].increment();
        }
        
        // Skriv ut resultat
        for (int i = 1; i <= SIDES; i++)
            StdOut.println(rolls[i]);
    }
}
```

**Output:**
```
167308 1's
166540 2's
166087 3's
167051 4's
166422 5's
166592 6's
```

---

### 2️⃣ Objekt och Referenser

#### 🎁 Objekt - Grundläggande Begrepp

**Objekt** = en entitet som kan ha ett datatyp-värde

**Tre essentiella egenskaper:**
1. **State (Tillstånd):** Ett värde från sin datatyp
2. **Identity (Identitet):** Unikt identifierar objektet (minnesadress)
3. **Behavior (Beteende):** Effekten av operationer på objektet

**Referens** = en mekanism för att komma åt ett objekt (tänk: minnesadress)

#### 🏗️ Skapa Objekt

**Syntax:**
```java
Counter heads = new Counter("heads");
```

**Vad händer:**
1. **Allokera minne** för objektet
2. **Anropa konstruktorn** för att initialisera värdet
3. **Returnera en referens** till objektet
4. **Tilldela referensen** till variabeln `heads`

**Viktigt:**
- Variabeln `heads` innehåller en **referens** till objektet, inte objektet självt
- Flera variabler kan referera till samma objekt (aliasing)

#### 📞 Anropa Instansmetoder

```java
Counter heads = new Counter("heads");

heads.increment();       // Anropa increment() på heads-objektet
heads.increment();       
heads.increment();

int count = heads.tally();  // Få aktuellt värde (3)
String s = heads.toString(); // "3 heads"
```

**Syntax:** `objectReference.methodName(arguments)`

---

### 3️⃣ Implementera Abstract Data Types

#### 🏗️ Grundläggande Struktur

**En ADT-implementation består av:**
1. **Instance variables (Instansvariabler):** Representerar objektets tillstånd
2. **Constructor(s):** Initialiserar objektet
3. **Instance methods:** Operationer på objektet
4. **main() (test client):** För unit testing

#### 📝 Counter - Komplett Implementation

```java
public class Counter {
    // Instance variables (PRIVATE!)
    private final String name;  // final = kan inte ändras efter initialisering
    private int count;
    
    // Constructor
    public Counter(String id) {
        name = id;
        count = 0;
    }
    
    // Instance methods
    public void increment() {
        count++;
    }
    
    public int tally() {
        return count;
    }
    
    public String toString() {
        return count + " " + name;
    }
    
    // Test client
    public static void main(String[] args) {
        Counter heads = new Counter("heads");
        Counter tails = new Counter("tails");
        
        heads.increment();
        heads.increment();
        tails.increment();
        
        StdOut.println(heads + " " + tails);  // "2 heads 1 tails"
        StdOut.println(heads.tally() + tails.tally());  // 3
    }
}
```

#### 🔐 Inkapsling - Viktiga Principer

**Instance variables ska ALLTID vara `private`:**
- ✅ Döljer implementation från klienten
- ✅ Tillåter ändring av representation utan att påverka klienter
- ✅ Kan lägga till validering och felkontroll

**Synlighetsmodifierare:**
- `private`: Endast synlig inom klassen
- `public`: Synlig för alla
- (vi använder inte `protected` eller package-private i denna bok)

**Använd `final` för värden som inte ska ändras:**
```java
private final String name;  // Kan endast sättas i konstruktorn
```

---

### 4️⃣ Scope och Variabler

#### 📦 Tre Typer av Variabler i Instance Methods

1. **Parameter variables (Parametrar):**
   - Anges i metodsignaturen
   - Initialiseras när metoden anropas
   - Scope: hela metoden

2. **Local variables (Lokala variabler):**
   - Deklareras i metodkroppen
   - Scope: från deklaration till slutet av blocket

3. **Instance variables (Instansvariabler):**
   - Tillhör objektet
   - Scope: hela klassen
   - Lever så länge objektet existerar

#### 🎯 Exempel med Scope

```java
public class Example {
    private int var;  // Instance variable
    
    private void method1() {
        int var;  // Local variable (skuggar instance variable)
        ... var ...        // Refererar till LOCAL variable
        ... this.var ...   // Refererar till INSTANCE variable (this. är nödvändigt här)
    }
    
    private void method2() {
        ... var ...  // Refererar till INSTANCE variable
    }
}
```

**Tips:** Använd `this.` för att referera till instance variables när det finns namnkonflikt

---

### 5️⃣ Viktiga ADT-exempel

#### 📅 Date ADT

**API:**
```java
public class Date
    Date(int month, int day, int year)
    int month()
    int day()
    int year()
    String toString()
```

**Implementation:**
```java
public class Date {
    private final int month;
    private final int day;
    private final int year;
    
    public Date(int m, int d, int y) {
        month = m;
        day = d;
        year = y;
    }
    
    public int month() { return month; }
    public int day() { return day; }
    public int year() { return year; }
    
    public String toString() {
        return month + "/" + day + "/" + year;
    }
}
```

**Användning:**
```java
Date birthday = new Date(12, 25, 2000);
int m = birthday.month();  // 12
StdOut.println(birthday);  // "12/25/2000"
```

#### 💰 Transaction ADT

**API:**
```java
public class Transaction
    Transaction(String who, Date when, double amount)
    String who()
    Date when()
    double amount()
    String toString()
```

**Användning:**
```java
Date date = new Date(6, 15, 2023);
Transaction t = new Transaction("Alice", date, 99.99);
String customer = t.who();      // "Alice"
double amt = t.amount();        // 99.99
StdOut.println(t);              // "Alice 6/15/2023 99.99"
```

---

### 6️⃣ Arrayer av Objekt

**Skapa en array av objekt kräver TVÅ steg:**

1. **Skapa arrayen** (skapar referenser, inte objekt)
2. **Skapa varje objekt** i arrayen

```java
Counter[] counters = new Counter[3];  // Steg 1: Skapa array av referenser

// Steg 2: Skapa objekten
for (int i = 0; i < 3; i++) {
    counters[i] = new Counter("counter " + i);
}
```

**Visualisering:**
```
counters[0] ──> Counter object (name="counter 0", count=0)
counters[1] ──> Counter object (name="counter 1", count=0)
counters[2] ──> Counter object (name="counter 2", count=0)
```

---

### 7️⃣ Viktiga String-metoder (Revidering)

```java
String s = "Hello World";

// Längd
int len = s.length();  // 11

// Hämta tecken
char ch = s.charAt(0);  // 'H'

// Konkatenering
String s2 = s.concat("!");  // "Hello World!"

// Hitta substring
int index = s.indexOf("World");  // 6
int notFound = s.indexOf("xyz");  // -1

// Substring
String sub = s.substring(0, 5);  // "Hello"

// Dela upp
String[] words = s.split(" ");  // ["Hello", "World"]

// Jämföra
boolean eq = s.equals("Hello World");  // true
int cmp = s.compareTo("Hello");  // positivt (W > ingenting)
```

---

### 8️⃣ Input/Output med Objekt

#### 📥 In - Läsa från Filer eller Nätverk

**API:**
```java
public class In
    In()                    // Läs från standard input
    In(String name)         // Läs från fil eller URL
    boolean isEmpty()
    int readInt()
    double readDouble()
    String readString()
    String readLine()
    String readAll()
    void close()
```

**Exempel:**
```java
In in = new In("data.txt");
while (!in.isEmpty()) {
    String word = in.readString();
    StdOut.println(word);
}
in.close();
```

#### 📤 Out - Skriva till Filer

**API:**
```java
public class Out
    Out()                    // Skriv till standard output
    Out(String name)         // Skriv till fil
    void print(String s)
    void println(String s)
    void printf(String fmt, ...)
    void close()
```

**Exempel:**
```java
Out out = new Out("output.txt");
out.println("Hello, File!");
out.close();
```

#### 🔗 Exempel: Konkatenera Filer (Cat)

```java
public class Cat {
    public static void main(String[] args) {
        // Sista argumentet är output-fil
        Out out = new Out(args[args.length-1]);
        
        // Läs och kopiera varje input-fil
        for (int i = 0; i < args.length - 1; i++) {
            In in = new In(args[i]);
            String s = in.readAll();
            out.println(s);
            in.close();
        }
        out.close();
    }
}
```

**Användning:**
```bash
java Cat in1.txt in2.txt out.txt
```

---

### 9️⃣ Immutable vs Mutable ADTs

#### 🔒 Immutable (Oföränderlig) ADT

**Definition:** Ett objekt vars tillstånd **inte kan ändras** efter att det skapats.

**Exempel: Date, Transaction, String**

**Kännetecken:**
- Alla instance variables är `final`
- Inga metoder som ändrar tillståndet
- Ger **defensive copies** vid behov

**Fördelar:**
- ✅ Säkrare - ingen risk för oavsiktliga ändringar
- ✅ Kan användas som nycklar i hashtabeller
- ✅ Kan delas mellan trådar utan problem

**Exempel:**
```java
public class Date {
    private final int month;
    private final int day;
    private final int year;
    
    // Ingen set-metoder!
    // Objektet kan inte ändras efter konstruktorn
}
```

#### 🔓 Mutable (Föränderlig) ADT

**Definition:** Ett objekt vars tillstånd **kan ändras** efter skapandet.

**Exempel: Counter, Accumulator**

**Kännetecken:**
- Minst en instance variable som INTE är `final`
- Metoder som ändrar tillståndet

**Exempel:**
```java
public class Counter {
    private final String name;  // final
    private int count;          // INTE final - kan ändras!
    
    public void increment() {
        count++;  // Ändrar tillståndet
    }
}
```

---

### 🔟 Accumulator - Ett Mer Avancerat Exempel

**API:**
```java
public class Accumulator
    Accumulator()
    void addDataValue(double val)
    double mean()
    String toString()
```

**Implementation:**
```java
public class Accumulator {
    private int N;
    private double total;
    
    public void addDataValue(double val) {
        N++;
        total += val;
    }
    
    public double mean() {
        return total / N;
    }
    
    public String toString() {
        return "Mean (" + N + " values): " + String.format("%.5f", mean());
    }
}
```

**Användning:**
```java
int T = 1000;
Accumulator a = new Accumulator();
for (int t = 0; t < T; t++)
    a.addDataValue(StdRandom.random());
StdOut.println(a);  // "Mean (1000 values): 0.51829"
```

---

### 1️⃣1️⃣ VisualAccumulator - ADT med Grafik

**Visar att ADT kan ha "side effects" som att rita:**

```java
public class VisualAccumulator {
    private double total;
    private int N;
    
    public VisualAccumulator(int trials, double max) {
        StdDraw.setXscale(0, trials);
        StdDraw.setYscale(0, max);
        StdDraw.setPenRadius(.005);
    }
    
    public void addDataValue(double val) {
        N++;
        total += val;
        StdDraw.setPenColor(StdDraw.DARK_GRAY);
        StdDraw.point(N, val);           // Rita datapunkt
        StdDraw.setPenColor(StdDraw.RED);
        StdDraw.point(N, total/N);       // Rita medelvärde
    }
    
    public double mean() {
        return total / N;
    }
}
```

**Poäng:** Samma klientkod kan använda både `Accumulator` och `VisualAccumulator`!

```java
// Byt bara denna rad:
Accumulator a = new Accumulator();
// Till:
VisualAccumulator a = new VisualAccumulator(trials, max);

// Resten av koden fungerar identiskt!
```

---

### 1️⃣2️⃣ Designa Bra API:er

#### 🎯 Principer för God API-design

**Mål:**
1. Gör det **enkelt att skriva klientkod**
2. Gör det **möjligt att implementera** effektivt

**Vanliga fallgropar att undvika:**

❌ **För svårt att implementera**
- API:et kräver omöjliga eller mycket svåra implementationer

❌ **För svårt att använda**
- Klientkod blir mer komplex än nödvändigt

❌ **För snävt**
- Saknar metoder som klienter behöver

❌ **För brett**
- Innehåller många metoder som få/inga klienter använder
- Svårt att underhålla och dokumentera

❌ **För generellt**
- Ger inga användbara abstraktioner

❌ **För specifikt**
- Abstraktioner är för detaljerade eller diffusa

❌ **För beroende av representation**
- Tvingar klienter att veta om intern representation

#### 📋 Best Practices

✅ **"Provide to clients the methods they need and no others"**

✅ **Använd tydliga, beskrivande namn**

✅ **Dokumentera pre- och postconditions**

✅ **Tänk på framtida användning** - skriv som om koden ska återanvändas

✅ **Inkludera exempel** i dokumentationen

---

### 1️⃣3️⃣ Inherited Methods (Ärvda Metoder)

Java-konventioner kräver vissa metoder i alla klasser:

#### 🔄 toString()

**Syfte:** Returnera en strängrepresentation av objektet

**Default:** Minnesadress (oanvändbar)

**Vi overridar nästan alltid:**
```java
public String toString() {
    return month + "/" + day + "/" + year;
}
```

**Används automatiskt:**
```java
Date d = new Date(5, 22, 1939);
String s = "Date: " + d;  // Anropar automatiskt d.toString()
StdOut.println(d);         // Anropar också toString()
```

#### ⚖️ equals()

**Syfte:** Testa om två objekt är "lika"

**Default:** Samma som `==` (samma referens)

**Vi overridar för värde-jämförelser:**
```java
public boolean equals(Object x) {
    if (this == x) return true;
    if (x == null) return false;
    if (this.getClass() != x.getClass()) return false;
    Date that = (Date) x;
    if (this.day != that.day) return false;
    if (this.month != that.month) return false;
    if (this.year != that.year) return false;
    return true;
}
```

**Användning:**
```java
Date d1 = new Date(5, 22, 1939);
Date d2 = new Date(5, 22, 1939);
boolean same = d1.equals(d2);  // true (samma värden)
boolean sameRef = (d1 == d2);  // false (olika objekt)
```

---

### 1️⃣4️⃣ Wrapper Types

Java har **wrapper-klasser** för primitiva typer:

| Primitiv typ | Wrapper-klass |
|--------------|---------------|
| `int`        | `Integer`     |
| `double`     | `Double`      |
| `boolean`    | `Boolean`     |
| `char`       | `Character`   |
| `long`       | `Long`        |
| `float`      | `Float`       |

**Användning:**
```java
Integer x = new Integer(42);
int value = x.intValue();  // 42

Double y = new Double(3.14);
double d = y.doubleValue();  // 3.14
```

**Autoboxing/Unboxing (automatisk konvertering):**
```java
Integer x = 42;        // Autoboxing: int → Integer
int y = x;             // Unboxing: Integer → int

Double d = 3.14;       // Autoboxing
double val = d + 1.0;  // Unboxing
```

**Varför använda wrapper types?**
- ✅ Kan användas i collections (ArrayList etc.)
- ✅ Har användbara statiska metoder (Integer.parseInt(), etc.)
- ✅ Kan vara `null` (primitiva typer kan inte)

---

### 1️⃣5️⃣ StaticSETofInts - Algoritmer som ADT

**Visar hur algoritmer kapslas in i ADT:**

**API:**
```java
public class StaticSETofInts
    StaticSETofInts(int[] a)
    boolean contains(int key)
```

**Implementation (använder binär sökning):**
```java
import java.util.Arrays;

public class StaticSETofInts {
    private int[] a;
    
    public StaticSETofInts(int[] keys) {
        a = new int[keys.length];
        // Defensive copy
        for (int i = 0; i < keys.length; i++)
            a[i] = keys[i];
        Arrays.sort(a);
    }
    
    public boolean contains(int key) {
        return rank(key) != -1;
    }
    
    private int rank(int key) {
        // Binär sökning
        int lo = 0;
        int hi = a.length - 1;
        while (lo <= hi) {
            int mid = lo + (hi - lo) / 2;
            if (key < a[mid]) hi = mid - 1;
            else if (key > a[mid]) lo = mid + 1;
            else return mid;
        }
        return -1;
    }
}
```

**Klient (Whitelist):**
```java
public class Whitelist {
    public static void main(String[] args) {
        int[] w = In.readInts(args[0]);
        StaticSETofInts set = new StaticSETofInts(w);
        
        while (!StdIn.isEmpty()) {
            int key = StdIn.readInt();
            if (!set.contains(key))
                StdOut.println(key);
        }
    }
}
```

**Fördelar med ADT-ansatsen:**
- ✅ Tydlig separation mellan klient och implementation
- ✅ Kan enkelt byta algoritm (t.ex. till hash-baserad sökning)
- ✅ API tydliggör vad algoritmen kan göra
- ✅ Enklare att testa och underhålla

---

### 1️⃣6️⃣ Interface Inheritance (Gränssnittsarv)

**Interface** = en lista med metodsignaturer (utan implementation)

**Syfte:** Specificera ett "kontrakt" som implementerande klasser måste uppfylla

#### 📋 Definiera ett Interface

```java
public interface Datable {
    int month();
    int day();
    int year();
}
```

#### 🔨 Implementera ett Interface

```java
public class Date implements Datable {
    private final int month;
    private final int day;
    private final int year;
    
    public Date(int m, int d, int y) {
        month = m;
        day = d;
        year = y;
    }
    
    public int month() { return month; }
    public int day() { return day; }
    public int year() { return year; }
}
```

**Kompilatorn kontrollerar att alla metoder i interfacet är implementerade!**

#### 🎯 Användning

```java
Datable d = new Date(12, 25, 2000);
int m = d.month();  // Kompilerar - month() finns i Datable
```

**Fördelar:**
- ✅ Kompilatorkontroll att API följs
- ✅ Flera klasser kan implementera samma interface
- ✅ Klientkod kan arbeta med interface-typen, inte konkret klass

---

### 1️⃣7️⃣ Sammanfattning: Typer av Java-klasser

| Typ                        | Exempel                      | Kännetecken                                    |
|----------------------------|------------------------------|------------------------------------------------|
| Statiska metoder           | Math, StdIn, StdOut          | Inga instance variables                        |
| Immutable ADT              | Date, Transaction, String    | Alla variables `final`, defensive copies       |
| Mutable ADT                | Counter, Accumulator         | Minst en icke-`final` variable                 |
| ADT med I/O                | VisualAccumulator, In, Out   | Gör I/O i instance methods                     |

---

## 🎓 Viktiga Takeaways från Kapitel 1.1 och 1.2

### 🔑 Från 1.1 (Basic Programming Model):

1. **Primitiva typer:** `int`, `double`, `boolean`, `char`
2. **Statements:** declarations, assignments, conditionals, loops, calls, returns
3. **Arrayer:** Sekvenser av värden, indexerade från 0
4. **Statiska metoder:** Inkapslar beräkningar, kan vara rekursiva
5. **Strings:** Sekvenser av tecken med rika operationer
6. **I/O:** StdIn, StdOut för standard input/output
7. **Binär sökning:** O(log N) algoritm för sorterade arrayer
8. **Modulär programmering:** Dela upp kod i testbara enheter

### 🔑 Från 1.2 (Data Abstraction):

1. **ADT:** Datatyp med dold representation
2. **Objekt:** State, identity, behavior
3. **References:** Variabler innehåller referenser till objekt
4. **Inkapsling:** `private` instance variables, `public` methods
5. **Immutable vs Mutable:** Kan objektet ändras efter skapande?
6. **API-design:** Tydligt gränssnitt mellan klient och implementation
7. **Wrapper types:** Objekt-versioner av primitiva typer
8. **Interface:** Kontrakt för implementation

---

## 📝 Praktiska Tips

### ✅ Best Practices:

1. **Använd beskrivande variabelnamn**
   - ❌ `int x;`
   - ✅ `int numberOfStudents;`

2. **Kommentera kod**
   - Förklara *varför*, inte *vad*

3. **Testa varje metod**
   - Skriv en `main()` för unit testing

4. **Använd `private` för instance variables**
   - Inkapsla alltid!

5. **Använd `final` för konstanter**
   - `private final String name;`

6. **Validera input**
   ```java
   if (day < 1 || day > 31)
       throw new IllegalArgumentException("Invalid day");
   ```

7. **Defensive copying för mutable types**
   ```java
   public StaticSETofInts(int[] keys) {
       a = new int[keys.length];
       for (int i = 0; i < keys.length; i++)
           a[i] = keys[i];  // Kopiera, använd inte originalet!
   }
   ```

---

## 🧠 Minnesregler

### Arrayer:
- Index börjar på **0**
- Sista elementet: `a[a.length - 1]`
- Försök INTE komma åt `a[a.length]` - det ger fel!

### Strings:
- Använd `.equals()` för jämförelser, **INTE** `==`
- Strängar är **immutable** (kan inte ändras)

### Objekt:
- `new` skapar ett objekt
- Variabler innehåller **referenser**, inte objekt
- Tilldelning `b = a` kopierar referensen, inte objektet

### ADT:
- **API** = kontrakt mellan klient och implementation
- **Inkapsling** = göm detaljer bakom API
- **Immutable** = säkrare, men mindre flexibelt

---

**Lycka till med studierna! 🎉**

*Denna sammanfattning täcker de viktigaste koncepten från kapitel 1.1 och 1.2. För djupare förståelse, läs igenom kapitlen i boken och gör övningarna!*
