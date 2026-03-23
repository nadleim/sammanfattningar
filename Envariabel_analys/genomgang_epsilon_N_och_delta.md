# Komplett genomgång: ε–N och ε–δ definitioner och bevis

## Innehållsförteckning

- **DEL 1: Det stora perspektivet** — Vad handlar allt detta om?
- **DEL 2: ε–N-definitionen** — Talföljder som konvergerar
  - Intuition och "skeptiker-spelet"
  - Den formella definitionen
  - Steg-för-steg-mall för bevis
  - Fullt genomarbetat exempel 1: Enkel talföljd
  - Fullt genomarbetat exempel 2: Svårare talföljd med uppskattning
  - Motbevis: Visa att en följd INTE konvergerar
  - Variationer: ε–N för oegentliga gränsvärden
- **DEL 3: ε–δ-definitionen** — Funktioners gränsvärden i en punkt
  - Intuition: Från talföljder till funktioner
  - Den formella definitionen
  - Skillnader och likheter med ε–N
  - Steg-för-steg-mall för bevis
  - Fullt genomarbetat exempel 1: Linjär funktion (enklaste fallet)
  - Fullt genomarbetat exempel 2: Andragradsfunktion (kräver begränsning)
  - Fullt genomarbetat exempel 3: Rotfunktion (konjugatmultiplikation)
  - Variationer: Ensidiga gränsvärden, oegentliga gränsvärden
- **DEL 4: Vanliga fällor och tentamensstrategi**
- **DEL 5: Övningsuppgifter med fullständiga lösningar**
- **DEL 6: Sammanfattning och minnesregler**

---

---

# DEL 1: Det stora perspektivet

## Varför behövs dessa definitioner?

I kalkylkurser beräknar man gränsvärden med räkneregler: faktorisera, förkorta, konjugatmultiplikation, L'Hôpitals regel, och så vidare. Men dessa regler bygger alla på ett fundament — en **exakt, matematisk definition** av vad det innebär att ett gränsvärde existerar.

Utan den formella definitionen är "gränsvärde" bara en vag känsla: "det verkar som att talen närmar sig 5/2". Med definitionen kan vi **bevisa** att detta stämmer, med samma logiska stringens som vilken matematisk sats som helst.

## Två varianter av samma idé

Det finns två situationer:

| Situation | Notation | Fråga | Formalism |
|-----------|----------|-------|-----------|
| Talföljd | $\lim_{n \to \infty} a_n = L$ | Vad händer med $a_n$ när $n$ växer? | ε–N |
| Funktion i en punkt | $\lim_{x \to x_0} f(x) = L$ | Vad händer med $f(x)$ nära $x_0$? | ε–δ |

Båda bygger på **exakt samma princip**: "oavsett hur noga du mäter (ε), kan jag garantera att vi hamnar tillräckligt nära gränsvärdet."

Skillnaden är bara *hur vi mäter "tillräckligt nära" på input-sidan*:
- ε–N: Vi tar index $n$ tillräckligt **stort** (dvs. $n \geq N$)
- ε–δ: Vi tar $x$ tillräckligt **nära** $x_0$ (dvs. $|x - x_0| < \delta$)

## Kärnidén i en mening

> **"Du väljer toleransen, jag hittar tröskeln."**

Denna mening sammanfattar hela principen. "Du" (skeptikern) sätter ett krav — hur nära gränsvärdet resultatet måste vara. "Jag" (bevisföraren) hittar en tröskel (ett $N$ eller $\delta$) som garanterar att kravet uppfylls.

---

---

# DEL 2: ε–N-definitionen (talföljder)

## 2.1 Intuition: Skeptiker-spelet

Tänk dig en talföljd — till exempel $a_n = \frac{7n + 1}{3n + 2}$. Om du räknar ut de första termerna:

$$a_1 = \frac{8}{5} = 1.6, \quad a_{10} = \frac{71}{32} \approx 2.22, \quad a_{100} = \frac{701}{302} \approx 2.32, \quad a_{1000} \approx 2.332$$

Det ser ut som att termerna närmar sig $\frac{7}{3} \approx 2.333...$

Nu spelas ett spel:

**Skeptikern** (din motståndare) säger: *"Jag tror inte på det. Bevisa att alla termer till slut hamnar inom $\varepsilon = 0.1$ från $\frac{7}{3}$."*

**Du** svarar: *"Inga problem — om vi tittar från och med $n = N$, så ligger alla termer inom det bandet."*

**Skeptikern**: *"Okej... men hur nära som helst? $\varepsilon = 0.001$?"*

**Du**: *"Fortfarande inga problem. Jag väljer bara ett större $N$."*

**Skeptikern**: *"$\varepsilon = 0.0000001$????"*

**Du**: *"Jag har en formel. Ge mig valfritt $\varepsilon > 0$, och jag ger dig ett $N$."*

Det är **exakt** detta som den formella definitionen säger.

## 2.2 Den formella definitionen

### Definition (ε–N)

En talföljd $(a_n)$ **konvergerar** mot $L$ om:

$$\boxed{\forall \, \varepsilon > 0 \;\; \exists \, N_\varepsilon \in \mathbb{N} : \quad n > N_\varepsilon \implies |a_n - L| < \varepsilon}$$

Läst på svenska:

> "**För varje** positivt tal $\varepsilon$ **finns det** ett naturligt tal $N_\varepsilon$ sådant att **för alla** $n > N_\varepsilon$ gäller att **avståndet** $|a_n - L|$ **är mindre än** $\varepsilon$."

### Vad varje del betyder

| Symbol | Betydelse | Roll i "spelet" |
|--------|-----------|------------------|
| $\varepsilon > 0$ | Tolerans/felmarginal | Skeptikerns krav |
| $N_\varepsilon$ | Tröskelvärde (startindex) | Ditt svar |
| $n > N_\varepsilon$ | Alla termer efter tröskeln | Alla testpunkter |
| $\|a_n - L\| < \varepsilon$ | Avståndet till $L$ är litet | Kravet som ska uppfyllas |

### Absolut kritiska detaljer

**1. Ordningen av kvantifierarna:**

Definitionen säger $\forall \varepsilon > 0 \;\; \exists N_\varepsilon$. Det betyder:
- **Först** väljs $\varepsilon$ (av skeptikern — godtyckligt)
- **Sedan** väljs $N$ (av dig — och det **får bero på** $\varepsilon$)

Om vi hade $\exists N \; \forall \varepsilon > 0$ (omvänd ordning) skulle det betyda att **ett enda** $N$ fungerar för **alla** $\varepsilon$ — det är ett mycket starkare påstående (och oftast falskt).

**2. $N$ får (och måste ofta) bero på $\varepsilon$:**

Om skeptikern kräver $\varepsilon = 0.001$, behöver du ett stort $N$. Om hen kräver $\varepsilon = 0.000001$, behöver du ett ännu större $N$. Därför skriver vi ofta $N_\varepsilon$ eller $N(\varepsilon)$ för att betona beroendet.

**3. Det behöver inte vara det minsta möjliga $N$:**

Om $N = 100$ fungerar, och du väljer $N = 10000$ — det är fortfarande korrekt! Du behöver bara hitta **något** $N$ som fungerar. I bevis väljer vi ofta ett $N$ som är bekvämt, inte optimalt.

**4. Det gäller "alla $n > N$", inte bara "något $n > N$":**

Hela poängen är att talföljden **stannar** nära $L$ för alltid, inte att den bara snuddar vid $L$ ibland.

### Visuell förståelse

Föreställ dig ett horisontellt band centrerat på $L$:

```
        L + ε  ═══════════════════════════════
                     ·  · ····················  ← alla termer här
        L      ───────·──·──────────────────────  ← gränsvärdet
                   · ·   ····················  ← och här
        L - ε  ═══════════════════════════════
        
               ↑            ↑
         k = 1,2,...    k ≥ N (alla inom bandet!)
         (kanske utanför)
```

De första termerna (till vänster om $N$) kan ligga var som helst — de får vara utanför bandet. Men **från och med** $N$ måste **varenda** term ligga inuti bandet $[L - \varepsilon, \; L + \varepsilon]$.

Ju mindre $\varepsilon$ (ju smalare band), desto senare måste $N$ väljas (längre till höger).

---

## 2.3 Steg-för-steg-mall för ε–N-bevis

Varje ε–N-bevis följer samma grundstruktur. Här är mallen:

### Fas 1: Kladdpappersarbete (visas INTE i beviset)

**Steg 1 — Gissa gränsvärdet $L$:**
Stoppa in stora $n$ i $a_n$, eller dividera täljare och nämnare med den högsta $n$-potensen. Det ger dig $L$.

**Steg 2 — Beräkna och förenkla $|a_n - L|$:**
Skriv ut differensen $a_n - L$ på ett gemensamt bråkstreck och förenkla. Målet är att få ett uttryck som avtar mot 0 när $n$ växer.

**Steg 3 — Uppskatta ovanifrån (om nödvändigt):**
Ofta kan du inte lösa $|a_n - L| < \varepsilon$ exakt. Då **uppskattar du ovanifrån** med ett enklare uttryck:
$$|a_n - L| \leq \text{(enklare uttryck)} < \varepsilon$$
Tricket: gör nämnaren mindre (→ bråket större) eller gör täljaren större (→ bråket större). Det ger en "slösig" men korrekt uppskattning.

**Steg 4 — Lös olikheten för $n$:**
Lös det förenklade uttrycket $< \varepsilon$ med avseende på $n$. Det ger $N(\varepsilon)$.

### Fas 2: Det formella beviset (det du skriver in)

**Mening 1 — Inledning:**
> "Låt $\varepsilon > 0$ vara godtyckligt."

**Mening 2 — Välj $N$:**
> "Välj $N_\varepsilon = \lceil \text{uttryck i } \varepsilon \rceil$."

(Eller: "Välj $N_\varepsilon = \max(k, \lceil \text{uttryck} \rceil)$" om du behöver $n$ vara tillräckligt stort av andra skäl.)

**Mening 3 — Visa att det fungerar:**
> "Då gäller för alla $n > N_\varepsilon$:"
> $$|a_n - L| = \ldots \leq \ldots < \varepsilon$$

**Mening 4 — Slutsats:**
> "Alltså konvergerar $a_n \to L$. $\square$"

### Varför fungerar det?

Logikkedjan är: du visar att din tröskel $N$ garanterar att alla efterföljande termer ligger inom $\varepsilon$-bandet. Eftersom $\varepsilon$ var godtyckligt, gäller det för *alla* möjliga toleranser — precis vad definitionen kräver.

---

## 2.4 Exempel 1: Enkel talföljd (exakt lösning)

**Uppgift:** Visa med ε–N-definitionen att $\displaystyle \lim_{n \to \infty} \frac{5n + 3}{2n + 1} = \frac{5}{2}$.

### Fas 1: Kladdpapper

**Steg 1 — Gissa $L$:** Dividera täljare och nämnare med $n$:

$$a_n = \frac{5n+3}{2n+1} = \frac{5 + 3/n}{2 + 1/n} \to \frac{5}{2} \quad \text{då } n \to \infty$$

Så $L = \frac{5}{2}$.

**Steg 2 — Beräkna $|a_n - L|$:**

$$a_n - \frac{5}{2} = \frac{5n+3}{2n+1} - \frac{5}{2} = \frac{2(5n+3) - 5(2n+1)}{2(2n+1)} = \frac{10n + 6 - 10n - 5}{2(2n+1)} = \frac{1}{2(2n+1)}$$

Eftersom $2n + 1 > 0$ för alla $n \geq 1$ behöver vi inga absolutbelopp:

$$|a_n - L| = \frac{1}{2(2n+1)}$$

**Steg 3 — Ingen uppskattning behövs!** Uttrycket är redan enkelt nog.

**Steg 4 — Lös $|a_n - L| < \varepsilon$:**

$$\frac{1}{2(2n+1)} < \varepsilon$$

$$2(2n+1) > \frac{1}{\varepsilon}$$

$$2n+1 > \frac{1}{2\varepsilon}$$

$$n > \frac{1}{4\varepsilon} - \frac{1}{2}$$

Alltså: om $n > \frac{1}{4\varepsilon} - \frac{1}{2}$ gäller det. Vi väljer $N_\varepsilon = \left\lceil \frac{1}{4\varepsilon} \right\rceil$ (avrundning uppåt, och vi tar bort $-\frac{1}{2}$ för att vara på säkra sidan).

### Fas 2: Det formella beviset

Låt $\varepsilon > 0$ vara godtyckligt. Välj $N_\varepsilon = \left\lceil \frac{1}{4\varepsilon} \right\rceil$.

Då gäller för alla $n > N_\varepsilon$:

$$\left|\frac{5n+3}{2n+1} - \frac{5}{2}\right| = \frac{1}{2(2n+1)} < \frac{1}{2 \cdot 2n} = \frac{1}{4n} < \frac{1}{4 N_\varepsilon} \leq \varepsilon$$

Alltså $\displaystyle\lim_{n \to \infty} \frac{5n+3}{2n+1} = \frac{5}{2}$. $\square$

### Vad hände i beviskedjan?

$$\underbrace{\frac{1}{2(2n+1)}}_{\text{exakt}} < \underbrace{\frac{1}{4n}}_{\text{förenklat}} < \underbrace{\frac{1}{4N_\varepsilon}}_{\text{insatt }N} \leq \underbrace{\varepsilon}_{\text{klart!}}$$

Vi gick från det exakta uttrycket till ett enklare (eftersom $2n+1 > 2n$), sedan satte vi in $n > N_\varepsilon$, och till sist använde vi valet $N_\varepsilon \geq \frac{1}{4\varepsilon}$.

---

## 2.5 Exempel 2: Svårare talföljd (kräver uppskattning)

**Uppgift:** Visa att $\displaystyle\lim_{n \to \infty} \frac{3n^2 + 2n}{n^2 + 5} = 3$.

### Fas 1: Kladdpapper

**Steg 1 — $L$:** Dividera med $n^2$: $\frac{3 + 2/n}{1 + 5/n^2} \to 3$. Så $L = 3$.

**Steg 2 — Beräkna $|a_n - 3|$:**

$$\frac{3n^2 + 2n}{n^2 + 5} - 3 = \frac{3n^2 + 2n - 3(n^2 + 5)}{n^2 + 5} = \frac{2n - 15}{n^2 + 5}$$

**Steg 3 — Uppskattning!** Här kan vi inte lösa exakt, så vi uppskattar:

$$|a_n - 3| = \frac{|2n - 15|}{n^2 + 5}$$

**Täljaren:** För $n \geq 8$ gäller $2n - 15 > 0$, alltså $|2n - 15| = 2n - 15 \leq 2n$.

**Nämnaren:** $n^2 + 5 > n^2$ (vi gör nämnaren *mindre* → bråket *större* → uppskattning ovanifrån).

$$|a_n - 3| < \frac{2n}{n^2} = \frac{2}{n} \quad \text{(för } n \geq 8 \text{)}$$

**Steg 4 — Lös $\frac{2}{n} < \varepsilon$:**

$$n > \frac{2}{\varepsilon}$$

Men vi behöver också $n \geq 8$ (från uppskattningen). Så: $N_\varepsilon = \max\!\left(8, \left\lceil \frac{2}{\varepsilon} \right\rceil\right)$.

### Fas 2: Det formella beviset

Låt $\varepsilon > 0$. Välj $N_\varepsilon = \max\!\left(8, \left\lceil \frac{2}{\varepsilon} \right\rceil\right)$.

Då gäller för alla $n > N_\varepsilon$ (notera $n > 8$, så $2n - 15 > 0$ och $|2n-15| = 2n-15 < 2n$):

$$|a_n - 3| = \frac{|2n - 15|}{n^2 + 5} < \frac{2n}{n^2} = \frac{2}{n} < \frac{2}{N_\varepsilon} \leq \varepsilon$$

Alltså $\displaystyle\lim_{n \to \infty} \frac{3n^2 + 2n}{n^2 + 5} = 3$. $\square$

### Varför "max" i $N$-valet?

Vi har **två villkor** som $n$ måste uppfylla:
1. $n > \frac{2}{\varepsilon}$ (för att $\frac{2}{n} < \varepsilon$)
2. $n \geq 8$ (för att uppskattningen $|2n-15| \leq 2n$ ska gälla)

$\max(8, \lceil 2/\varepsilon \rceil)$ garanterar att **båda** villkoren uppfylls.

---

## 2.6 Motbevis: Visa att en följd INTE konvergerar

**Uppgift:** Visa att talföljden $a_n = (-1)^n$ inte konvergerar.

### Tanken

Om $\lim_{n\to\infty} a_n = L$ existerade, skulle **alla** termer från och med $N$ ligga i intervallet $(L - \varepsilon, L + \varepsilon)$. Men termerna hoppar mellan $+1$ och $-1$. Om vi väljer $\varepsilon = 1$, kan inte både $+1$ och $-1$ ligga inom avstånd 1 från samma punkt $L$ (avståndet mellan dem är 2, men bandet har bredd $2\varepsilon = 2$).

Hmm, det *nästan* fungerar. Välj istället $\varepsilon = \frac{1}{2}$ — då är bandet bara 1 brett, men $+1$ och $-1$ har avstånd 2 från varandra. Omöjligt!

### Det formella beviset (motsägelsebevis)

**Antag** att $\lim_{n \to \infty} a_n = L$ för något $L \in \mathbb{R}$.

Välj $\varepsilon = \frac{1}{2}$. Enligt definitionen finns då $N$ så att $|a_n - L| < \frac{1}{2}$ för alla $n > N$.

Betrakta ett **jämnt** $n > N$ (så att $a_n = +1$) och ett **udda** $m > N$ (så att $a_m = -1$). Båda existerar, ty det finns godtyckligt stora jämna och udda tal.

Av triangelolikheten:

$$2 = |1 - (-1)| = |a_n - a_m| = |(a_n - L) - (a_m - L)| \leq |a_n - L| + |a_m - L| < \frac{1}{2} + \frac{1}{2} = 1$$

Men $2 < 1$ är en **motsägelse**. Alltså finns inget sådant $L$, och följden konvergerar inte. $\square$

### Nyckelinsikt: Triangelolikheten

Tricket i motbevis är ofta: hitta två termer som *ligger långt ifrån varandra*. Om båda ska vara nära $L$, leder triangelolikheten till en motsägelse.

---

## 2.7 Variationer av ε–N-definitionen

Din kursbok innehåller flera varianter av definitionen, anpassade för olika situationer:

### Variant 1: $\lim_{n \to \infty} a_n = +\infty$

$$\forall \, M > 0 \;\; \exists \, N_M : \quad n > N_M \implies a_n > M$$

"Oavsett hur stort $M$ du kräver, kan jag hitta $N$ så att alla termer efter $N$ överskrider $M$."

Märk: här finns **inget** $\varepsilon$ — istället har vi $M$ som gör rollen av "krav", och kravet är att $a_n$ ska vara *stor* (inte *nära* ett tal).

### Variant 2: $\lim_{n \to \infty} a_n = -\infty$

$$\forall \, K < 0 \;\; \exists \, N_K : \quad n > N_K \implies a_n < K$$

Samma princip, men åt andra hållet.

---

---

# DEL 3: ε–δ-definitionen (funktioner i en punkt)

## 3.1 Intuition: Från talföljder till funktioner

Vid talföljder frågade vi: *vad händer med $a_n$ när $n$ blir stort?*

Vid funktioner frågar vi istället: *vad händer med $f(x)$ när $x$ kommer nära en specifik punkt $x_0$?*

Det underliggande konceptet är identiskt. Skillnaden är geometrisk:

- **Talföljd (ε–N):** Vi kontrollerar en "halv tallinje" — allt *efter* index $N$.
- **Funktion (ε–δ):** Vi kontrollerar ett litet **intervall** runt punkten $x_0$ — alla $x$ som ligger *inom avstånd $\delta$* från $x_0$.

### Den geometriska bilden

Vid ε–N hade vi ett horisontellt band runt $L$ och letade efter var alla termer "hamnar inuti."

Vid ε–δ har vi **två** band:
- **Horisontellt band:** $L - \varepsilon < y < L + \varepsilon$ (utdata-tolerans)
- **Vertikalt band:** $x_0 - \delta < x < x_0 + \delta$ (indata-kontroll)

Frågan: kan vi välja det vertikala bandet så smalt att funktionskurvan *inom det bandet* aldrig lämnar det horisontella bandet?

```
    y ↑
      |        ─── L + ε ──────────
      |       /                    (horisontellt band)
      |      / ← kurvan f(x)
      |     /
      |  ─── L ─────────────────
      |   /
      |  /
      | ─── L - ε ──────────
      |  |       |
      |  |       |
      +──|───────|──────────→ x
        x₀-δ  x₀  x₀+δ
             (vertikalt band)
```

Om **hela** den del av kurvan som ligger i det vertikala bandet *också* ligger i det horisontella bandet, så fungerar det $\delta$-valet.

---

## 3.2 Den formella definitionen

### Definition (ε–δ)

Vi säger att $\displaystyle\lim_{x \to x_0} f(x) = L$ om:

$$\boxed{\forall \, \varepsilon > 0 \;\; \exists \, \delta > 0 : \quad 0 < |x - x_0| < \delta \implies |f(x) - L| < \varepsilon}$$

Läst på svenska:

> "**För varje** positivt tal $\varepsilon$ **finns det** ett positivt tal $\delta$ sådant att **för alla** $x$ med $0 < |x - x_0| < \delta$ gäller att $|f(x) - L| < \varepsilon$."

### Vad varje del betyder

| Symbol | Betydelse | Geometri |
|--------|-----------|----------|
| $\varepsilon > 0$ | Tolerans på utdata (y-led) | Höjden på det horisontella bandet |
| $\delta > 0$ | Kontrollradie på indata (x-led) | Bredden på det vertikala bandet |
| $0 < \|x - x_0\|$ | $x$ är **inte** $x_0$ (punkterad omgivning) | Vi kollar inte självaste punkten |
| $\|x - x_0\| < \delta$ | $x$ ligger nära $x_0$ | $x$ är inuti det vertikala bandet |
| $\|f(x) - L\| < \varepsilon$ | Funktionsvärdet ligger nära $L$ | Kurvan träffar det horisontella bandet |

### Absolut kritiska detaljer

**1. $0 < |x - x_0|$ — vi exkluderar $x = x_0$:**

Gränsvärdet handlar om vad som händer *nära* $x_0$, inte *i* $x_0$. Funktionen behöver inte ens vara definierad i $x_0$! (Tänk: $\frac{\sin x}{x}$ vid $x = 0$.)

**2. $\delta$ får bero på $\varepsilon$ (och $x_0$), men INTE på $x$:**

Precis som $N$ fick bero på $\varepsilon$ i ε–N-fallet, får $\delta$ bero på $\varepsilon$. Men $\delta$ måste väljas **innan** vi vet vilka $x$ som testas — det är ett fast tal, inte en funktion av $x$.

**3. $L$ behöver inte vara lika med $f(x_0)$:**

Om $f(x_0) = 5$ men $\lim_{x \to x_0} f(x) = 3$, är det helt okej — funktionen har bara en "hoppunkt" i $x_0$. Gränsvärdet bryr sig om omgivningen, inte punkten själv.

---

## 3.3 Jämförelsetabell: ε–N vs ε–δ

| | ε–N (talföljd → ∞) | ε–δ (funktion → punkt) |
|---|---|---|
| **Notation** | $\lim_{n \to \infty} a_n = L$ | $\lim_{x \to x_0} f(x) = L$ |
| **"Nära $L$" (utdata)** | $\|a_n - L\| < \varepsilon$ | $\|f(x) - L\| < \varepsilon$ |
| **"Tillräckligt bra input"** | $n > N_\varepsilon$ | $0 < \|x - x_0\| < \delta$ |
| **Du väljer** | $N$ (startindex) | $\delta$ (radie runt $x_0$) |
| **Geometrisk bild** | Allt efter en vertikal linje | Allt inuti ett vertikalt band |
| **Input-typ** | Heltal $n \in \mathbb{N}$ | Reella tal $x \in \mathbb{R}$ |
| **Exkludering** | Ingen (alla $n > N$ inkluderas) | $x = x_0$ **exkluderas** |
| **Input-riktning** | Ensidig (bara $n \to +\infty$) | Tvåsidig ($x$ från båda håll) |

Kärnan är **identisk**: ge mig vilken $\varepsilon$-tolerans som helst, och jag hittar en input-tröskel.

---

## 3.4 Steg-för-steg-mall för ε–δ-bevis

### Fas 1: Kladdpappersarbete (visas INTE i beviset)

**Steg 1 — Identifiera $x_0$ och $L$.**

**Steg 2 — Beräkna och förenkla $|f(x) - L|$.**

Skriv ut differensen, förenkla. Försök att isolera faktorn $|x - x_0|$, eftersom det är den variabeln som $\delta$ kontrollerar.

**Steg 3 — Uttryck $|f(x) - L|$ i termer av $|x - x_0|$.**

Idealt: $|f(x) - L| = k \cdot |x - x_0|$ för någon konstant $k$, eller $|f(x) - L| = g(x) \cdot |x - x_0|$ där $g(x)$ kan begränsas.

**Steg 4 — Lös olikheten bakvänt.**

Du vill ha $|f(x) - L| < \varepsilon$. Om $|f(x) - L| = k \cdot |x - x_0|$, då:
$$k \cdot |x - x_0| < \varepsilon \implies |x - x_0| < \frac{\varepsilon}{k}$$

Alltså: välj $\delta = \frac{\varepsilon}{k}$.

Om $|f(x) - L| = g(x) \cdot |x - x_0|$ och $g(x)$ inte är konstant, behöver du **begränsa** $g(x)$ ovanifrån genom att först anta $|x - x_0| < 1$ (eller annat fast tal). Se Exempel 2 nedan.

### Fas 2: Det formella beviset

**Mening 1:** "Låt $\varepsilon > 0$ vara godtyckligt."

**Mening 2:** "Välj $\delta = \ldots$"

**Mening 3:** "Då gäller för alla $x$ med $0 < |x - x_0| < \delta$:"
$$|f(x) - L| = \ldots \leq \ldots < \varepsilon$$

**Mening 4:** "Alltså $\lim_{x \to x_0} f(x) = L$. $\square$"

### Det kritiska tricket: "Begränsning först"

När $|f(x) - L|$ inte direkt ger en konstant gånger $|x - x_0|$, använder vi ett **tvåstegs-δ-trick**:

1. **Anta först** att $\delta \leq 1$ (eller annan konstant). Det begränsar $x$ till intervallet $(x_0 - 1, x_0 + 1)$.
2. I det intervallet, **uppskatta** den variabla faktorn ovanifrån med en konstant $C$.
3. Då: $|f(x) - L| \leq C \cdot |x - x_0|$, och vi vill ha $C \cdot |x - x_0| < \varepsilon$, alltså $|x - x_0| < \frac{\varepsilon}{C}$.
4. Men vi behöver **båda** villkoren ($\delta \leq 1$ och $\delta \leq \frac{\varepsilon}{C}$), så: $\delta = \min\!\left(1, \frac{\varepsilon}{C}\right)$.

---

## 3.5 Exempel 1: Linjär funktion (enklaste fallet)

**Uppgift:** Visa med ε–δ-definitionen att $\displaystyle\lim_{x \to 3} (4x - 7) = 5$.

### Fas 1: Kladdpapper

**Steg 1:** $x_0 = 3$, $L = 5$ (ty $4 \cdot 3 - 7 = 5$).

**Steg 2:** $|f(x) - L| = |(4x - 7) - 5| = |4x - 12| = 4|x - 3|$.

Perfekt! Vi fick en konstant ($4$) gånger $|x - x_0|$.

**Steg 3:** Vi vill $4|x - 3| < \varepsilon$, alltså $|x - 3| < \frac{\varepsilon}{4}$.

**Steg 4:** Välj $\delta = \frac{\varepsilon}{4}$.

### Fas 2: Beviset

Låt $\varepsilon > 0$. Välj $\delta = \frac{\varepsilon}{4}$.

Då gäller för alla $x$ med $0 < |x - 3| < \delta$:

$$|(4x-7) - 5| = |4x - 12| = 4|x - 3| < 4\delta = 4 \cdot \frac{\varepsilon}{4} = \varepsilon$$

Alltså $\displaystyle\lim_{x \to 3}(4x-7) = 5$. $\square$

### Varför var detta enkelt?

Funktionen är linjär: $f(x) = 4x - 7$, så $|f(x) - L| = |4(x-3)| = 4|x-3|$.

Faktorn $4$ (derivatan!) ger ett direkt linjärt samband mellan input-felet ($|x - x_0|$) och output-felet ($|f(x) - L|$). Inget begränsnings-trick behövs.

---

## 3.6 Exempel 2: Andragradsfunktion (kräver begränsning)

**Uppgift:** Visa med ε–δ-definitionen att $\displaystyle\lim_{x \to 2} x^2 = 4$.

### Fas 1: Kladdpapper

**Steg 1:** $x_0 = 2$, $L = 4$.

**Steg 2:** $|f(x) - L| = |x^2 - 4| = |x - 2| \cdot |x + 2|$.

Bra! Vi fick $|x - x_0| = |x - 2|$ som en faktor. Men den **andra** faktorn $|x + 2|$ beror på $x$ — den är inte konstant. Vi måste **begränsa** den.

**Steg 3: Begränsnings-tricket.**

Antag att $\delta \leq 1$. Då: $|x - 2| < 1$, alltså $1 < x < 3$, och därmed:

$$|x + 2| < 3 + 2 = 5$$

Så under antagandet $\delta \leq 1$:

$$|x^2 - 4| = |x-2| \cdot |x+2| < 5 \cdot |x - 2|$$

**Steg 4:** Vi vill $5|x-2| < \varepsilon$, alltså $|x-2| < \frac{\varepsilon}{5}$.

Men vi behöver också $\delta \leq 1$, så:

$$\delta = \min\!\left(1, \frac{\varepsilon}{5}\right)$$

### Fas 2: Beviset

Låt $\varepsilon > 0$. Välj $\delta = \min\!\left(1, \frac{\varepsilon}{5}\right)$.

Då gäller för alla $x$ med $0 < |x - 2| < \delta$:

Eftersom $\delta \leq 1$ har vi $|x - 2| < 1$, dvs. $1 < x < 3$, och därmed $|x+2| < 5$.

$$|x^2 - 4| = |x - 2| \cdot |x+2| < \delta \cdot 5 \leq \frac{\varepsilon}{5} \cdot 5 = \varepsilon$$

Alltså $\displaystyle\lim_{x \to 2} x^2 = 4$. $\square$

### Varför $\min(1, \varepsilon/5)$?

Vi har **två villkor** på $\delta$:
1. $\delta \leq 1$ (för att begränsningen $|x+2| < 5$ ska gälla)
2. $\delta \leq \frac{\varepsilon}{5}$ (för att slutuppskattningen ska ge $< \varepsilon$)

$\min(1, \varepsilon/5)$ uppfyller **båda** villkoren, oavsett hur stort eller litet $\varepsilon$ är.

**Notera:** Talet $1$ i $\min(1, \ldots)$ är godtyckligt — vi kunde valt $\delta \leq 2$ (och fått $|x+2| < 6$, $\delta = \min(2, \varepsilon/6)$) eller $\delta \leq \frac{1}{2}$ (och fått $|x+2| < 4.5$, $\delta = \min(1/2, \varepsilon/4.5)$). Alla val ger korrekta bevis. Konventionen $\delta \leq 1$ är bara det enklaste.

---

## 3.7 Exempel 3: Rotfunktion (konjugatmultiplikation)

**Uppgift:** Visa med ε–δ-definitionen att $\displaystyle\lim_{x \to 9} \sqrt{x} = 3$.

### Fas 1: Kladdpapper

**Steg 1:** $x_0 = 9$, $L = 3$.

**Steg 2:** $|f(x) - L| = |\sqrt{x} - 3|$.

Hmm — detta innehåller inte $|x - 9|$ direkt. Vi behöver använda **konjugatmultiplikation**:

$$|\sqrt{x} - 3| = |\sqrt{x} - 3| \cdot \frac{|\sqrt{x} + 3|}{|\sqrt{x} + 3|} = \frac{|x - 9|}{|\sqrt{x} + 3|}$$

Nu har vi $|x - 9| = |x - x_0|$ i täljaren!

**Steg 3:** Vi behöver uppskatta $\frac{1}{|\sqrt{x}+3|}$ ovanifrån. Eftersom $\sqrt{x} \geq 0$:

$$\sqrt{x} + 3 \geq 3 \quad \implies \quad \frac{1}{\sqrt{x}+3} \leq \frac{1}{3}$$

Denna uppskattning gäller för **alla** $x \geq 0$ — vi behöver inte ens begränsa $\delta$!

$$|\sqrt{x} - 3| = \frac{|x-9|}{\sqrt{x}+3} \leq \frac{|x-9|}{3}$$

**Steg 4:** $\frac{|x-9|}{3} < \varepsilon \implies |x-9| < 3\varepsilon$. Välj $\delta = 3\varepsilon$.

Men OBS: vi behöver $x \geq 0$ (annars är $\sqrt{x}$ odefinierad). Om $\delta = 3\varepsilon$ och $x_0 = 9$, ger $|x - 9| < 3\varepsilon$ att $x > 9 - 3\varepsilon$. Om $\varepsilon \geq 3$ kan detta ge negativa $x$. Lösning: $\delta = \min(9, 3\varepsilon)$. (Men vanligtvis nöjer vi oss med $\delta = 3\varepsilon$ och noterar att det gäller för $x$ i definitionsmängden.)

### Fas 2: Beviset

Låt $\varepsilon > 0$. Välj $\delta = 3\varepsilon$.

Då gäller för alla $x \geq 0$ med $0 < |x - 9| < \delta$:

$$|\sqrt{x} - 3| = \frac{|x - 9|}{\sqrt{x} + 3} \leq \frac{|x - 9|}{3} < \frac{\delta}{3} = \frac{3\varepsilon}{3} = \varepsilon$$

Alltså $\displaystyle\lim_{x \to 9} \sqrt{x} = 3$. $\square$

### Nyckelinsikt

Konjugatmultiplikation omvandlar ett rotuttryck till ett bråk med $|x - x_0|$ i täljaren. Det är samma algebraiska trick som i gränsvärdersberäkningar, men här används det i bevissammanhanget.

---

## 3.8 Variationer av ε–δ-definitionen

### Variant 1: Ensidigt gränsvärde $\lim_{x \to x_0^+} f(x) = L$

$$\forall \, \varepsilon > 0 \;\; \exists \, \delta > 0 : \quad 0 < x - x_0 < \delta \implies |f(x) - L| < \varepsilon$$

Skillnad: $x$ kommer bara **från höger** (vi kollar inte $x < x_0$).

### Variant 2: Ensidigt gränsvärde $\lim_{x \to x_0^-} f(x) = L$

$$\forall \, \varepsilon > 0 \;\; \exists \, \delta > 0 : \quad 0 < x_0 - x < \delta \implies |f(x) - L| < \varepsilon$$

$x$ kommer bara **från vänster**.

### Variant 3: $\lim_{x \to x_0} f(x) = +\infty$

$$\forall \, M > 0 \;\; \exists \, \delta > 0 : \quad 0 < |x - x_0| < \delta \implies f(x) > M$$

"Nära $x_0$ blir $f(x)$ godtyckligt stort."

### Variant 4: $\lim_{x \to \infty} f(x) = L$ (ε–ω-definitionen)

$$\forall \, \varepsilon > 0 \;\; \exists \, \omega > 0 : \quad x > \omega \implies |f(x) - L| < \varepsilon$$

Denna är egentligen en hybrid: input-sidan ser ut som ε–N (vi tar $x$ stort), output-sidan ser ut som ε–δ (vi vill nära $L$). I din kursbok kallas tröskeln $\omega$ (omega) istället för $N$.

### Variant 5: $\lim_{x \to 0^+} \ln(x) = -\infty$ (K–δ-definition)

$$\forall \, K < 0 \;\; \exists \, \delta > 0 : \quad 0 < x < \delta \implies \ln(x) < K$$

**Exempel-bevis:** Låt $K < 0$. Välj $\delta = e^K$ (notera $e^K \in (0,1)$ ty $K < 0$).

Om $0 < x < \delta = e^K$: Eftersom $\ln$ är strängt växande: $\ln(x) < \ln(e^K) = K$. $\square$

---

---

# DEL 4: Vanliga fällor och tentamensstrategi

## 4.1 Tio vanliga misstag

**Misstag 1: $\delta$ (eller $N$) beror på $x$ (eller $n$).**

$$\text{FEL: } \delta = \frac{\varepsilon}{2x} \qquad \text{RÄTT: } \delta = \frac{\varepsilon}{2 \cdot C} \text{ där } C \text{ är en konstant}$$

$\delta$ väljs **innan** $x$ testas. Det är som att måla staketet innan besökaren kommer — du kan inte anpassa staketet efter besökarens position.

**Misstag 2: Glömma $0 < |x - x_0|$ i ε–δ.**

Utan $0 <$-villkoret inkluderar vi $x = x_0$, men gränsvärdet handlar om *omgivningen*, inte punkten. (I ε–N finns inte denna fälla, ty $n$ är alltid strikt större än $N$.)

**Misstag 3: Visa det "åt fel håll".**

Du ska visa: om input är tillräckligt bra ($|x - x_0| < \delta$), **då** är output bra ($|f(x) - L| < \varepsilon$).

Att visa det omvända (om output är bra, då input...) bevisar ingenting.

**Misstag 4: Skriva "$|a_n - L| = \varepsilon$" istället för "$< \varepsilon$".**

Definitionen kräver **strikt** olikhet. Vi vill att avståndet är **mindre** än toleransen, inte lika med.

**Misstag 5: Använda specifika $\varepsilon$-värden.**

"Låt $\varepsilon = 0.01$. Då..." — FEL! Definitionen kräver att det fungerar för **varje** $\varepsilon > 0$. Att visa det för ett specifikt $\varepsilon$ bevisar ingenting (utom om du motbevisar konvergens, se §2.6).

**Misstag 6: Glömma att $N$ måste vara ett heltal.**

$N_\varepsilon = \sqrt{3/\varepsilon}$ är oftast inte ett heltal. Lösning: avrunda uppåt med $\lceil \cdot \rceil$.

**Misstag 7: Glömma att motivera uppskattningar.**

Om du skriver "$|2n - 15| < 2n$" måste du förklara **varför** (t.ex. "ty $n \geq 8$, alltså $2n - 15 > 0$").

**Misstag 8: Hoppa över att visa att $\delta > 0$.**

$\delta$ måste vara **positivt**. Om ditt uttryck för $\delta$ kan bli $\leq 0$ (det bör aldrig hända om du gjort rätt), är beviset felaktigt.

**Misstag 9: Skriva $n \geq N$ istället för $n > N$ (eller tvärtom) utan att vara konsekvent.**

Kontrollera vilken konvention din kursbok använder. Båda fungerar, men byt inte mitt i beviset. Din kurs använder $n > N_\varepsilon$.

**Misstag 10: Inte skriva slutsatsen.**

Avsluta alltid med "Alltså $\lim_{...} = L$" eller "Alltså konvergerar $a_n$ mot $L$", följt av $\square$.

---

## 4.2 Tentamensstrategi

### Strategi 1: Identifiera bevistypen

Frågan säger "visa med definitionen" eller "bevisa med ε–N-definitionen" eller "visa att gränsvärdet är..."
→ Det är ett formellt bevis. Använd mallen.

### Strategi 2: Börja alltid med kladdpappersarbete

Skriv $|a_n - L| = \ldots$ (eller $|f(x) - L| = \ldots$) och förenkla tills du ser $N$ eller $\delta$.

### Strategi 3: Om det inte förenklas snyggt — uppskatta

Gör nämnaren mindre, täljaren större. Mist: $n^2 + 5 > n^2$, $|2n-15| \leq 2n$ (för stora $n$).

### Strategi 4: Skriv det formella beviset separat

Kladdpappret visar du bara om du vill. Det "riktiga" beviset börjar vid "Låt $\varepsilon > 0$..."

### Strategi 5: Kontrollera med ett numeriskt exempel

Stoppa in t.ex. $\varepsilon = 0.01$ i din formel. Vad ger det för $N$? Kolla att $|a_N - L|$ verkligen $< 0.01$.

---

---

# DEL 5: Övningsuppgifter med fullständiga lösningar

## Övning 1 (ε–N, enkel)

**Uppgift:** Visa att $\displaystyle\lim_{n \to \infty} \frac{2n - 1}{n + 3} = 2$.

### Kladdpapper

$a_n - 2 = \frac{2n-1}{n+3} - 2 = \frac{2n - 1 - 2(n+3)}{n+3} = \frac{-7}{n+3}$

$|a_n - 2| = \frac{7}{n+3} < \frac{7}{n}$

$\frac{7}{n} < \varepsilon \implies n > \frac{7}{\varepsilon}$

### Bevis

Låt $\varepsilon > 0$. Välj $N_\varepsilon = \left\lceil \frac{7}{\varepsilon} \right\rceil$.

För alla $n > N_\varepsilon$:

$$\left|\frac{2n-1}{n+3} - 2\right| = \frac{7}{n+3} < \frac{7}{n} < \frac{7}{N_\varepsilon} \leq \varepsilon$$

Alltså $\displaystyle\lim_{n\to\infty} \frac{2n-1}{n+3} = 2$. $\square$

---

## Övning 2 (ε–N, med $n^2$ i nämnaren)

**Uppgift:** Visa att $\displaystyle\lim_{n \to \infty} \frac{n + 1}{n^2} = 0$.

### Kladdpapper

$|a_n - 0| = \frac{n+1}{n^2} = \frac{1}{n} + \frac{1}{n^2} \leq \frac{1}{n} + \frac{1}{n} = \frac{2}{n}$ (ty $n^2 \geq n$ för $n \geq 1$).

$\frac{2}{n} < \varepsilon \implies n > \frac{2}{\varepsilon}$.

### Bevis

Låt $\varepsilon > 0$. Välj $N_\varepsilon = \left\lceil \frac{2}{\varepsilon} \right\rceil$.

För alla $n > N_\varepsilon$ ($n \geq 1$):

$$\frac{n+1}{n^2} = \frac{1}{n} + \frac{1}{n^2} \leq \frac{2}{n} < \frac{2}{N_\varepsilon} \leq \varepsilon$$

Alltså $\displaystyle\lim_{n\to\infty} \frac{n+1}{n^2} = 0$. $\square$

---

## Övning 3 (ε–δ, linjär)

**Uppgift:** Visa att $\displaystyle\lim_{x \to 1} (3x + 2) = 5$.

### Kladdpapper

$|(3x+2) - 5| = |3x - 3| = 3|x - 1|$

$3|x-1| < \varepsilon \implies |x-1| < \frac{\varepsilon}{3}$

### Bevis

Låt $\varepsilon > 0$. Välj $\delta = \frac{\varepsilon}{3}$.

Då gäller för alla $x$ med $0 < |x - 1| < \delta$:

$$|(3x+2) - 5| = 3|x - 1| < 3\delta = 3 \cdot \frac{\varepsilon}{3} = \varepsilon$$

Alltså $\displaystyle\lim_{x \to 1}(3x+2) = 5$. $\square$

---

## Övning 4 (ε–δ, andragrad med min-trick)

**Uppgift:** Visa att $\displaystyle\lim_{x \to 3} x^2 = 9$.

### Kladdpapper

$|x^2 - 9| = |x-3| \cdot |x+3|$

Antag $\delta \leq 1$: $|x - 3| < 1 \implies 2 < x < 4 \implies |x + 3| < 7$

$|x^2 - 9| < 7|x - 3|$

$7|x-3| < \varepsilon \implies |x-3| < \frac{\varepsilon}{7}$

$\delta = \min(1, \varepsilon/7)$

### Bevis

Låt $\varepsilon > 0$. Välj $\delta = \min\!\left(1, \frac{\varepsilon}{7}\right)$.

Då gäller $|x-3| < 1$, alltså $2 < x < 4$ och $|x+3| < 7$.

$$|x^2 - 9| = |x-3| \cdot |x+3| < 7|x-3| < 7 \cdot \frac{\varepsilon}{7} = \varepsilon$$

Alltså $\displaystyle\lim_{x \to 3} x^2 = 9$. $\square$

---

## Övning 5 (ε–δ, oegentligt gränsvärde $\to +\infty$)

**Uppgift:** Visa att $\displaystyle\lim_{x \to 2} \frac{1}{(x-2)^2} = +\infty$.

### Kladdpapper (definitionen)

Vi behöver: $\forall M > 0 \; \exists \delta > 0 : 0 < |x - 2| < \delta \implies \frac{1}{(x-2)^2} > M$

$\frac{1}{(x-2)^2} > M \iff (x-2)^2 < \frac{1}{M} \iff |x-2| < \frac{1}{\sqrt{M}}$

Alltså: välj $\delta = \frac{1}{\sqrt{M}}$.

### Bevis

Låt $M > 0$. Välj $\delta = \frac{1}{\sqrt{M}}$.

Då gäller för alla $x$ med $0 < |x - 2| < \delta$:

$$(x-2)^2 < \delta^2 = \frac{1}{M}$$

$$\frac{1}{(x-2)^2} > M$$

Alltså $\displaystyle\lim_{x \to 2} \frac{1}{(x-2)^2} = +\infty$. $\square$

---

## Övning 6 (ε–N, oegentligt gränsvärde)

**Uppgift:** Visa att $\lim_{n \to \infty} n^2 = +\infty$.

### Bevis

Låt $M > 0$. Välj $N_M = \lceil \sqrt{M} \rceil$.

För alla $n > N_M$: $n^2 > N_M^2 \geq M$.

Alltså $\lim_{n \to \infty} n^2 = +\infty$. $\square$

---

---

# DEL 6: Sammanfattning och minnesregler

## Minnesregel: GFVS

**G**issa gränsvärdet.
**F**örenkla $|a_n - L|$ (eller $|f(x) - L|$).
**V**älj $N$ eller $\delta$ (från kladdpappret).
**S**kriv beviset formellt.

## Minnesregel: Bevisstrukturen

Varje formellt bevis har **exakt fyra meningar**:

1. "Låt $\varepsilon > 0$ (eller $M > 0$)."
2. "Välj $N = \ldots$ (eller $\delta = \ldots$)."
3. "Då gäller: $|a_n - L| = \ldots < \varepsilon$."
4. "Alltså $\lim = L$. $\square$"

## Sammanfattningstabell: Alla definitionstyper

| Gränsvärde | Kvantifierare | Input-villkor | Output-villkor | Du väljer |
|------------|---------------|---------------|----------------|-----------|
| $\lim_{n\to\infty} a_n = L$ | $\forall \varepsilon > 0 \;\exists N$ | $n > N$ | $\|a_n - L\| < \varepsilon$ | $N(\varepsilon)$ |
| $\lim_{n\to\infty} a_n = +\infty$ | $\forall M > 0 \;\exists N$ | $n > N$ | $a_n > M$ | $N(M)$ |
| $\lim_{x\to x_0} f(x) = L$ | $\forall \varepsilon > 0 \;\exists \delta$ | $0<\|x-x_0\|<\delta$ | $\|f(x)-L\|<\varepsilon$ | $\delta(\varepsilon)$ |
| $\lim_{x\to x_0^+} f(x) = L$ | $\forall \varepsilon > 0 \;\exists \delta$ | $0<x-x_0<\delta$ | $\|f(x)-L\|<\varepsilon$ | $\delta(\varepsilon)$ |
| $\lim_{x\to x_0} f(x) = +\infty$ | $\forall M > 0 \;\exists \delta$ | $0<\|x-x_0\|<\delta$ | $f(x) > M$ | $\delta(M)$ |
| $\lim_{x\to\infty} f(x) = L$ | $\forall \varepsilon > 0 \;\exists \omega$ | $x > \omega$ | $\|f(x)-L\|<\varepsilon$ | $\omega(\varepsilon)$ |
| $\lim_{x\to 0^+} f(x) = -\infty$ | $\forall K < 0 \;\exists \delta$ | $0<x<\delta$ | $f(x) < K$ | $\delta(K)$ |

## Checklista innan du lämnar in ett bevis

- [ ] Börjar beviset med "Låt $\varepsilon > 0$ (eller $M$, $K$)?"
- [ ] Är $N$ (eller $\delta$) uttryckt **enbart** i termer av $\varepsilon$ (och eventuellt $x_0$)?
- [ ] Beror $N$/$\delta$ **inte** på $n$/$x$?
- [ ] Är alla uppskattningar motiverade?
- [ ] Ger varje steg strikt olikhet i rätt riktning?
- [ ] Slutar kedjan med "$ < \varepsilon$" (eller "$> M$")?
- [ ] Finns en explicit slutsats med $\square$?
