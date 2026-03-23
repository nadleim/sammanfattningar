# Komplett genomgång: Derivering & Primitiva funktioner

*Baserad på föreläsningar, kursbok (kap 3.1–3.4, 5.1–5.2) och övningsmaterial*

---

# DEL 1 — DERIVERING

## 1. Vad derivatan egentligen betyder

Derivatan svarar på frågan: **hur snabbt ändras funktionen just nu?**

Tänk dig att du kör bil och tittar på hastighetsmätaren. Sträckan s(t) du kört är en funktion av tiden. Hastighetsmätaren visar s'(t) — den momentana ändringstakten. Om du kört 150 km på 2 timmar är din *genomsnittliga* hastighet 75 km/h, men vid en specifik tidpunkt kanske du kör 90 km/h. Derivatan ger dig det exakta ögonblicksvärdet.

**Formellt:**

$$f'(x_0) = \lim_{h \to 0} \frac{f(x_0 + h) - f(x_0)}{h}$$

Bråket $\frac{f(x_0+h) - f(x_0)}{h}$ kallas **differenskvoten** och mäter genomsnittlig förändring över intervallet $[x_0, x_0+h]$. När $h \to 0$ krymper intervallet till en punkt och vi får den *momentana* förändringen.

**Geometrisk bild:** Differenskvoten = lutningen på en **sekantlinje** genom två punkter på grafen. Derivatan = lutningen på **tangentlinjen** i en enda punkt.

---

## 2. Derivationsreglerna — med förklaring

### 2.1 Konstantregeln

$$D(\alpha \cdot f(x)) = \alpha \cdot f'(x)$$

*En konstant faktor följer med rakt igenom.* Om du dubblar en funktion, dubblas även dess förändringstakt.

### 2.2 Summaregeln

$$D(f(x) + g(x)) = f'(x) + g'(x)$$

*Derivatan av en summa = summan av derivatorna.* Förändringstakten av "lön + bonus" = förändringstakten av lönen + förändringstakten av bonusen.

### 2.3 Produktregeln

$$D(f \cdot g) = f' \cdot g + f \cdot g'$$

**Varför ser den ut så?** Tänk på arean av en rektangel med sidor f(t) och g(t) som båda växer med tiden. Arean A = f·g ändras genom att:
- sidan f växer (bidrar med f'·g — ny bredd gånger gammal höjd)
- sidan g växer (bidrar med f·g' — gammal bredd gånger ny höjd)

Totalförändringen är summan: $f'g + fg'$.

**Exempel:** $D[(3x+1)(x^2-5)]$

Välj $f = 3x+1$, $g = x^2-5$. Då $f' = 3$, $g' = 2x$.

$$= 3(x^2-5) + (3x+1)(2x) = 3x^2 - 15 + 6x^2 + 2x = 9x^2 + 2x - 15$$

**Generalisering till tre faktorer:**
$$D(f_1 \cdot f_2 \cdot f_3) = f_1' f_2 f_3 + f_1 f_2' f_3 + f_1 f_2 f_3'$$

Mönstret: derivera varje faktor i tur och ordning, lämna övriga oförändrade, summera.

### 2.4 Kvotregeln

$$D\!\left(\frac{f}{g}\right) = \frac{f'g - fg'}{g^2}$$

**Minnesregel:** "Derivatan av täljaren gånger nämnaren, *minus* täljaren gånger derivatan av nämnaren, allt delat med nämnaren i kvadrat."

**Viktigt:** Ordningen spelar roll! Det är $f'g - fg'$, inte tvärtom.

**Exempel:** $D\!\left(\frac{x}{x+1}\right)$

Välj $f = x$, $g = x+1$. Då $f' = 1$, $g' = 1$.

$$= \frac{1 \cdot (x+1) - x \cdot 1}{(x+1)^2} = \frac{1}{(x+1)^2}$$

### 2.5 Kedjeregeln — den viktigaste regeln

$$D\,f(g(x)) = f'(g(x)) \cdot g'(x)$$

> **I ord:** *Derivera det yttre, behåll det inre, multiplicera med derivatan av det inre.*

Kedjeregeln behövs varje gång en funktion sitter *inuti* en annan. Det gäller oftare än man tror!

**Tankegång:** Om du ändrar x lite grann, hur mycket ändras g(x)? Svar: med ungefär $g'(x) \cdot \Delta x$. Och om g(x) ändras lite, hur mycket ändras f(g(x))? Svar: med ungefär $f'(g(x))$ gånger förändringen i g. Kedja ihop dessa två steg och du får $f'(g(x)) \cdot g'(x)$.

**Steg-för-steg-strategi:**
1. Identifiera den **yttre** funktionen (den som appliceras sist)
2. Identifiera den **inre** funktionen (argumentet till den yttre)
3. Derivera yttre, behåll inre som argument
4. Multiplicera med derivatan av inre

**Exempel 1:** $D(\sin^3 x) = D((\sin x)^3)$

- Yttre: $u^3$, inre: $\sin x$
- $= 3(\sin x)^2 \cdot \cos x = 3\sin^2 x \cos x$

**Exempel 2:** $D\!\left(\frac{1}{\sqrt{1-x^2}}\right) = D((1-x^2)^{-1/2})$

- Yttre: $u^{-1/2}$, inre: $1-x^2$
- $= -\tfrac{1}{2}(1-x^2)^{-3/2} \cdot (-2x) = \frac{x}{(1-x^2)^{3/2}}$

Notera hur de två minustecknen tar ut varandra!

**Exempel 3 — dubbel kedjeregel:** $D\,e^{\sin(x^2)}$

Tre lager: $e^u$ → $\sin v$ → $x^2$

$$= e^{\sin(x^2)} \cdot \cos(x^2) \cdot 2x$$

Derivera utifrån och in, multiplicera ihop.

### 2.6 Inversens derivata

$$D(f^{-1})(y) = \frac{1}{f'(x)} \quad \text{där } y = f(x)$$

Med Leibniz' notation: $\frac{dx}{dy} = \frac{1}{dy/dx}$

Detta används främst för att härleda derivatorna av arcusfunktionerna (arcsin, arccos, arctan) från de trigonometriska funktionernas derivator.

### 2.7 Implicit derivering

När y ges *implicit* av en ekvation (t.ex. $x^2 + y^2 = 1$) istället för explicit ($y = \sqrt{1-x^2}$):

1. Derivera *hela ekvationen* med avseende på x
2. Varje gång du deriverar en y-term, använd kedjeregeln → en faktor $y'$ dyker upp
3. Samla alla termer med $y'$ på ena sidan
4. Lös ut $y'$

**Exempel:** $x^4 + y^4 - xy = 1$

Derivera: $4x^3 + 4y^3 y' - (y + xy') = 0$

Samla: $y'(4y^3 - x) = y - 4x^3$

Lös ut: $y' = \frac{y - 4x^3}{4y^3 - x}$

### 2.8 Logaritmisk derivering

Användbart för produkter av många faktorer eller $g(x)^{h(x)}$:

1. Ta $\ln$ av båda sidor: $\ln f = \ln f_1 + \ln f_2 + \cdots$
2. Derivera: $\frac{f'}{f} = \frac{f_1'}{f_1} + \frac{f_2'}{f_2} + \cdots$
3. Multiplicera med f: $f' = f \cdot \left(\frac{f_1'}{f_1} + \cdots\right)$

**Specialfall — $g(x)^{h(x)}$:** Skriv om som $e^{h(x)\ln g(x)}$ och derivera med kedjeregeln:

$$D\!\left[g(x)^{h(x)}\right] = g(x)^{h(x)}\!\left[h'(x)\ln g(x) + h(x)\frac{g'(x)}{g(x)}\right]$$

**Exempel:** $D(x^x) = x^x(1 + \ln x)$

---

## 3. Komplett tabell: Elementära derivator

### Grundfunktioner

| Funktion $f(x)$ | Derivata $f'(x)$ | Villkor |
|---|---|---|
| $c$ (konstant) | $0$ | |
| $x^{\alpha}$ | $\alpha x^{\alpha-1}$ | $x > 0$ för allmän $\alpha$ |
| $e^x$ | $e^x$ | |
| $a^x$ | $a^x \ln a$ | $a > 0$ |
| $\ln x$ | $1/x$ | $x > 0$ |
| $\ln|x|$ | $1/x$ | $x \neq 0$ |
| ${}^a\!\log x$ | $\frac{1}{x \ln a}$ | $x > 0,\; a > 0$ |

### Trigonometriska funktioner

| Funktion | Derivata | Kommentar |
|---|---|---|
| $\sin x$ | $\cos x$ | |
| $\cos x$ | $-\sin x$ | **OBS minustecknet!** |
| $\tan x$ | $\frac{1}{\cos^2 x}$ | $= 1 + \tan^2 x$ |
| $\cot x$ | $-\frac{1}{\sin^2 x}$ | |

### Arcusfunktioner (inversa trigonometriska)

| Funktion | Derivata | Villkor |
|---|---|---|
| $\arcsin x$ | $\frac{1}{\sqrt{1-x^2}}$ | $|x| < 1$ |
| $\arccos x$ | $-\frac{1}{\sqrt{1-x^2}}$ | $|x| < 1$ |
| $\arctan x$ | $\frac{1}{1+x^2}$ | |
| $\text{arccot}\, x$ | $-\frac{1}{1+x^2}$ | |

### Hyperboliska funktioner

| Funktion | Derivata | Jämfört med trig |
|---|---|---|
| $\sinh x$ | $\cosh x$ | som sin → cos |
| $\cosh x$ | $\sinh x$ | **inget minus** (jfr cos → −sin) |
| $\tanh x$ | $\frac{1}{\cosh^2 x}$ | som tan |
| $\coth x$ | $-\frac{1}{\sinh^2 x}$ | som cot |

---

## 4. Viktiga specialtekniker

### 4.1 Derivera $e^{f(x)}$ (kedjeregel)

$$D\,e^{f(x)} = e^{f(x)} \cdot f'(x)$$

Exponentialfunktionen överlever derivering — den bara multipliceras med den inre derivatan.

**Exempel:** $D\,e^{3x^2+1} = e^{3x^2+1} \cdot 6x$

### 4.2 Derivera $\ln(f(x))$ (logaritmiska derivatan)

$$D\,\ln|f(x)| = \frac{f'(x)}{f(x)}$$

"Derivatan av det inre, delat med det inre." Denna formel dyker upp ständigt.

**Exempel:** $D\,\ln(\cos x) = \frac{-\sin x}{\cos x} = -\tan x$

### 4.3 Tangentens ekvation

Tangentlinjen till $f(x)$ i punkten $x = x_0$:

$$y = f'(x_0)(x - x_0) + f(x_0)$$

Tre steg: (1) beräkna $f'(x_0)$ = lutningen, (2) beräkna $f(x_0)$ = y-värdet, (3) sätt in i formeln.

### 4.4 Tips för att undvika vanliga fel

- **Skriv om innan du deriverar:** $\frac{1}{x^3} = x^{-3}$, $\sqrt[3]{x^2} = x^{2/3}$. Potensregeln är enklare än kvotregeln.
- **Glöm inte kedjeregeln!** $D(\sin(3x)) = \cos(3x) \cdot 3$, inte bara $\cos(3x)$.
- **Tecken vid cos:** $D(\cos x) = -\sin x$. Minustecknet glöms ofta.
- **Dubbelkolla med insättning:** Om du fått $f'(x)$, testa med ett specifikt x-värde och jämför med en numerisk differenskvot.

---

---

# DEL 2 — PRIMITIVA FUNKTIONER (INTEGRATION)

## 5. Vad en primitiv funktion är

**Derivering** svarar på: "givet $f$, vad är $f'$?"

**Primitiv funktion** svarar på den omvända frågan: "givet $f$, hitta $F$ så att $F' = f$."

> Om derivering är att gå "framåt" (funktion → förändringstakt), så är att hitta en primitiv funktion att gå "bakåt" (förändringstakt → funktion).

**Praktiskt exempel:** Du vet att en bils hastighet vid tiden $t$ är $v(t) = 3t^2$ m/s. Vilken sträcka $s(t)$ har bilen kört? Jo, $s(t)$ måste uppfylla $s'(t) = v(t) = 3t^2$. Testa: $D(t^3) = 3t^2$ ✓. Alltså $s(t) = t^3 + C$.

**Definition:** $F$ kallas en **primitiv funktion** till $f$ på intervallet $I$ om $F'(x) = f(x)$ för alla $x \in I$.

### Beteckningar

$$\int f(x)\,dx = F(x) + C$$

betyder: mängden av *alla* primitiva funktioner till $f(x)$. Symbolen $\int$ kallas integraltecknet, $f(x)$ kallas integranden, $dx$ anger variabeln.

### Varför $+C$?

Om $F'(x) = f(x)$, så är även $(F(x) + 7)' = f(x)$ och $(F(x) - 42)' = f(x)$. Konstanten "försvinner" vid derivering, så vi måste lägga till en godtycklig konstant $C$ för att fånga alla möjliga primitiver.

**Sats (entydighet):** Alla primitiver till $f$ på ett intervall $I$ skiljer sig med en konstant. Dvs om $F' = G' = f$ på $I$, så är $F(x) - G(x) = C$.

**Bevis:** $(F-G)' = f - f = 0$ på hela intervallet, och en funktion med derivata 0 överallt är konstant.

---

## 6. Komplett tabell: Elementära primitiver

Det här är derivattabellen "baklänges" — den måste sitta i ryggmärgen:

| Nr  | Integral                               | Primitiv funktion                   | Villkor/kommentar     |      |                                                    |
| --- | -------------------------------------- | ----------------------------------- | --------------------- | ---- | -------------------------------------------------- |
| 1   | $\int x^{\alpha}\,dx$                  | $\frac{x^{\alpha+1}}{\alpha+1} + C$ | $\alpha \neq -1$      |      |                                                    |
| 2   | $\int \frac{1}{x}\,dx$                 | $\ln                                | x                     | + C$ | $x \neq 0$ (specialfall av nr 1 när $\alpha = -1$) |
| 3   | $\int e^x\,dx$                         | $e^x + C$                           |                       |      |                                                    |
| 4   | $\int a^x\,dx$                         | $\frac{a^x}{\ln a} + C$             | $a > 0, a \neq 1$     |      |                                                    |
| 5   | $\int \cos x\,dx$                      | $\sin x + C$                        |                       |      |                                                    |
| 6   | $\int \sin x\,dx$                      | $-\cos x + C$                       | **OBS minustecknet!** |      |                                                    |
| 7   | $\int \frac{1}{\cos^2 x}\,dx$          | $\tan x + C$                        |                       |      |                                                    |
| 8   | $\int \frac{1}{\sin^2 x}\,dx$          | $-\cot x + C$                       |                       |      |                                                    |
| 9   | $\int \frac{1}{1+x^2}\,dx$             | $\arctan x + C$                     |                       |      |                                                    |
| 10  | $\int \frac{1}{\sqrt{1-x^2}}\,dx$      | $\arcsin x + C$                     | $                     | x    | < 1$                                               |
| 11  | $\int \frac{1}{\sqrt{x^2+\alpha}}\,dx$ | $\ln                                | x+\sqrt{x^2+\alpha}   | + C$ | $\alpha \in \mathbb{R}$                            |

### Räkneregler (linjäritet)

$$\int \alpha \cdot f(x)\,dx = \alpha \int f(x)\,dx \qquad \text{(bryt ut konstanter)}$$

$$\int (f(x) + g(x))\,dx = \int f(x)\,dx + \int g(x)\,dx \qquad \text{(dela upp summor)}$$

### Två extremt nyttiga mönsterformler

Dessa kommer direkt från kedjeregeln, läst baklänges:

**Formel A — "derivatan i täljaren":**

$$\int \frac{f'(x)}{f(x)}\,dx = \ln|f(x)| + C$$

Känn igen mönstret: om täljaren är derivatan av nämnaren, är svaret $\ln$ av nämnaren.

**Exempel:** $\int \frac{2x}{x^2+1}\,dx = \ln(x^2+1) + C$ eftersom $D(x^2+1) = 2x$.

**Formel B — "potenskedjeregeln":**

$$\int f(x)^{\alpha} \cdot f'(x)\,dx = \frac{f(x)^{\alpha+1}}{\alpha+1} + C \qquad (\alpha \neq -1)$$

Känn igen mönstret: en funktion upphöjd till en potens, multiplicerad med sin egen derivata.

**Exempel:** $\int \sin^3 x \cos x\,dx = \frac{\sin^4 x}{4} + C$ eftersom $D(\sin x) = \cos x$.

---

## 7. Integrationsmetoder

### 7.1 Linjär substitution (enklaste variabelbytet)

Om $F$ är primitiv till $f$, dvs $\int f(x)\,dx = F(x) + C$, så:

$$\int f(kx + m)\,dx = \frac{1}{k}\,F(kx+m) + C$$

**Varför $1/k$?** Kedjeregeln ger $D\,F(kx+m) = f(kx+m) \cdot k$, alltså behöver vi dela med $k$ för att kompensera.

**Exempel:** $\int \cos(3x+2)\,dx = \frac{1}{3}\sin(3x+2) + C$

**Exempel:** $\int e^{-5x}\,dx = \frac{1}{-5}e^{-5x} + C = -\frac{1}{5}e^{-5x} + C$

**Exempel:** $\int \frac{1}{2x+7}\,dx = \frac{1}{2}\ln|2x+7| + C$

### 7.2 Variabelsubstitution (generell)

Variabelsubstitution är kedjeregeln baklänges. Idén: byt ut en komplicerad del av integranden mot en ny variabel $t$ för att förenkla.

**Metoden i fyra steg:**

1. **Välj substitution:** $t = g(x)$ (välj den "jobbiga" inre funktionen)
2. **Beräkna $dt$:** $dt = g'(x)\,dx$, lös ut $dx = \frac{dt}{g'(x)}$
3. **Byt ut allt:** Ersätt alla $x$ och $dx$ med $t$ och $dt$
4. **Integrera och återsubstituera:** Integrera i $t$, byt sedan tillbaka till $x$

**Fyra vanliga mönster att känna igen:**

**Mönster 1 — $f(g(x)) \cdot g'(x)$:** Derivatan av det inre finns som faktor.

Exempel: $\int \sin x \cdot \cos^{-4/3}(x)\,dx$

Sätt $t = \cos x$, $dt = -\sin x\,dx$:

$$= \int t^{-4/3} \cdot (-dt) = -\frac{t^{-1/3}}{-1/3} + C = 3\cos^{-1/3}(x) + C$$

**Mönster 2 — $\frac{1}{x} \cdot f(\ln x)$:** Substitution $t = \ln x$.

Exempel: $\int \frac{(\ln x)^2}{x}\,dx$

Sätt $t = \ln x$, $dt = \frac{1}{x}dx$:

$$= \int t^2\,dt = \frac{t^3}{3} + C = \frac{(\ln x)^3}{3} + C$$

**Mönster 3 — $e^x \cdot f(e^x)$:** Substitution $t = e^x$.

**Mönster 4 — Rotuttryck:** $\sqrt{ax+b}$ → sätt $t = \sqrt{ax+b}$ eller $t = ax+b$.

### 7.3 Partialintegration

Partialintegration är produktregeln baklänges.

Produktregeln: $D(f \cdot g) = f' \cdot g + f \cdot g'$

Integrera båda sidor: $f \cdot g = \int f' \cdot g\,dx + \int f \cdot g'\,dx$

Ordna om:

$$\boxed{\int f' \cdot g\,dx = f \cdot g - \int f \cdot g'\,dx}$$

> **Idén:** Byt ut en integral du *inte* kan lösa mot en som du *kan* lösa. Priset är en randterm $f \cdot g$.

**Hur väljer man $f'$ och $g$?**

Tumregel **LIATE** — den som kommer *först* i listan bör vara $g$ (den du deriverar):

| Prioritet | Typ | Exempel |
|---|---|---|
| 1 | **L**ogaritmer | $\ln x$, $\log x$ |
| 2 | **I**nversa trig | $\arctan x$, $\arcsin x$ |
| 3 | **A**lgebraiska | $x^2$, $x^3$, polynom |
| 4 | **T**rigonometriska | $\sin x$, $\cos x$ |
| 5 | **E**xponentiella | $e^x$, $2^x$ |

Poängen: logaritmer och arcusfunktioner *vill bli deriverade* (de förenklas), medan exponentialfunktioner *vill bli integrerade* (de överlever).

**Exempel 1: $\int x \cdot e^x\,dx$**

Välj: $g = x$ (algebraisk, deriveras → 1) och $f' = e^x$ (integreras → $e^x$).

$$= x \cdot e^x - \int 1 \cdot e^x\,dx = xe^x - e^x + C = e^x(x-1) + C$$

**Exempel 2: $\int \ln x\,dx$ — "tricket gånger 1"**

Skriv $\ln x = \ln x \cdot 1$. Välj $g = \ln x$, $f' = 1$:

$$= x \ln x - \int x \cdot \frac{1}{x}\,dx = x\ln x - x + C$$

Kontroll: $D(x\ln x - x) = \ln x + 1 - 1 = \ln x$ ✓

**Exempel 3: $\int e^x \sin x\,dx$ — det cirkulära tricket**

Här blir man aldrig "klar" — man hamnar i en loop. Lösningen: kalla integralen $I$ och lös en ekvation.

Partialintegrera *två gånger* (samma riktning varje gång!):

Steg 1: $g = \sin x$, $f' = e^x$:

$$I = e^x \sin x - \int e^x \cos x\,dx$$

Steg 2: $g = \cos x$, $f' = e^x$:

$$I = e^x \sin x - \left[e^x \cos x - \int e^x(-\sin x)\,dx\right]$$
$$I = e^x \sin x - e^x \cos x - I$$

Lös ut: $2I = e^x(\sin x - \cos x)$

$$\boxed{I = \frac{e^x(\sin x - \cos x)}{2} + C}$$

---

## 8. Rationella funktioner (partialbråksuppdelning)

### Översikt: Fyrstegsschemat

Varje rationell funktion $\frac{P(x)}{Q(x)}$ kan integreras systematiskt:

**Steg 1 — Polynomdivision** (om grad $P \geq$ grad $Q$): Dela och skriv $\frac{P}{Q} = S(x) + \frac{R(x)}{Q(x)}$ där grad $R <$ grad $Q$.

**Steg 2 — Faktorisera nämnaren** $Q(x)$ i linjära och irreducibla kvadratiska faktorer.

**Steg 3 — Partialbråksuppdelning:** Skriv $\frac{R}{Q}$ som en summa av enklare bråk.

**Steg 4 — Integrera** varje delbråk (alla har kända primitiver).

### Ansatsregler

Varje faktor i nämnaren ger ett bidrag till ansatsen:

| Nämnarfaktor | Bidrag till ansatsen |
|---|---|
| $(x-a)$ | $\frac{A}{x-a}$ |
| $(x-a)^2$ | $\frac{A}{x-a} + \frac{B}{(x-a)^2}$ |
| $(x-a)^n$ | $\frac{A_1}{x-a} + \frac{A_2}{(x-a)^2} + \cdots + \frac{A_n}{(x-a)^n}$ |
| $(x^2+px+q)$ irreducibel | $\frac{Ax+B}{x^2+px+q}$ |

### De fyra elementära bråktyperna

Varje delbråk som uppstår hör till en av dessa fyra typer, och alla har kända primitiver:

**Typ 1:** $\displaystyle\int \frac{A}{x-a}\,dx = A\ln|x-a| + C$

**Typ 2:** $\displaystyle\int \frac{A}{(x-a)^n}\,dx = \frac{A}{(1-n)(x-a)^{n-1}} + C$ för $n \geq 2$

**Typ 3:** $\displaystyle\int \frac{A}{t^2+\beta}\,dt = \frac{A}{\sqrt{\beta}}\arctan\!\left(\frac{t}{\sqrt{\beta}}\right) + C$ (kvadratkomplettera först om nödvändigt)

**Typ 4:** $\displaystyle\int \frac{At+B}{(t^2+\beta)^n}\,dt$ — delas i $A$-del (substitution $u = t^2+\beta$) och $B$-del (rekursiv formel).

### Metod: Bestämma koefficienterna

**Metod 1 — Ekvationssystem:** Multiplicera båda sidor med $Q(x)$, utveckla och jämför koefficienter för varje potens av $x$.

**Metod 2 — Handpåläggning (smarta x-värden):** Sätt in $x = a$ (nollställen till nämnaren) för att eliminera termer.

**Exempel:** $\int \frac{1}{x^2-1}\,dx = \int \frac{1}{(x-1)(x+1)}\,dx$

Ansats: $\frac{1}{(x-1)(x+1)} = \frac{A}{x-1} + \frac{B}{x+1}$

Multiplicera med $(x-1)(x+1)$: $1 = A(x+1) + B(x-1)$

Handpåläggning:
- $x = 1$: $1 = 2A \Rightarrow A = 1/2$
- $x = -1$: $1 = -2B \Rightarrow B = -1/2$

Alltså:
$$\int \frac{dx}{x^2-1} = \frac{1}{2}\ln|x-1| - \frac{1}{2}\ln|x+1| + C = \frac{1}{2}\ln\!\left|\frac{x-1}{x+1}\right| + C$$

---

## 9. Beslutsträd — vilken metod ska jag använda?

Stå inför en integral? Gå igenom detta:

**1. Finns integralen direkt i tabellen?** (avsnitt 6) → Använd tabellen.

**2. Är det en linjär substitution?** Dvs $f(kx+m)$ → Använd $\frac{1}{k}F(kx+m)$.

**3. Har integranden mönstret $\frac{f'(x)}{f(x)}$?** → Svaret är $\ln|f(x)| + C$.

**4. Har integranden mönstret $f(x)^\alpha \cdot f'(x)$?** → Potenskedjeregeln.

**5. Finns en "inre funktion" vars derivata (nästan) finns som faktor?** → Variabelsubstitution.

**6. Är det en produkt av "olika typer" av funktioner?** (t.ex. polynom × trig, polynom × exp) → Partialintegration (LIATE-regeln).

**7. Är det en rationell funktion?** → Fyrstegsschemat (polynomdivision → faktorisering → partialbråk → integration).

**8. Hjälper en trigonometrisk identitet?** (t.ex. $\sin^2 x = \frac{1-\cos 2x}{2}$) → Skriv om och försök igen.

**9. Inget fungerar?** → Prova kreativ omskrivning, t.ex. "gånger 1"-tricket, konjugatförlängning, eller hyperbolisk substitution.

---

## 10. Verifieringstrick

**Gyllene regeln:** Derivera alltid ditt svar! Om $\int f(x)\,dx = F(x) + C$, kontrollera att $F'(x) = f(x)$.

Detta fångar teckenfel, glömda konstanter och felaktiga substitutioner. Det tar 30 sekunder och sparar poäng på tentan.
