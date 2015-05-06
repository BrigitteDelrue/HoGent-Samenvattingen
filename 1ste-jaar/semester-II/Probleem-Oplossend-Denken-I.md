# Probleem Oplossend Denken I

# Hoofdstuk 1

[Oefeningen](/1ste-jaar/semester-II/Oefeningen-Probleem-Oplossend-Denken-I/1.4.oefeningen.md#oefeningen-14-middot-slide-15-17)

* De sequentie
* De Selectie
* De Iteratie

## Algoritme: De Sequentie

---

```pascal
opdracht 1
opdracht 2
opdracht n
```

Voorbeeld: **Algoritme** Bereken BMI

```pascal
VOERUIT(scherm, "geef lengte in meter: ")
VOERIN(klavier, lengte)
VOERUIT(scherm, "geef gewicht in kilo: ")
VOERIN(klavier, gewicht)
bodyMassIndex <- gewicht/(lengte . lengte)
RETOUR bodyMassIndex
```

## Algoritme: De Selectie

---

```pascal
ALS voorwaarde DAN
	component1
ANDERS
	component2
EINDE ALS
```

## De eenzijdige Selectie:

```pascal
ALS voorwaarde DAN
	component1
EINDE ALS
```

Voorbeeld: **Algoritme** Evalueer BMI.

```pascal
VOERUIT(scherm, "Geef BMI:")
VOERIN(klavier, bodyMassIndex)
ALS ((18,5 ≤ bodyMassIndex) EN (bodyMassIndex ≤ 25)) DAN
	VOERUIT(scherm, "Gezond")
ANDERS
	VOERUIT(scherm, "Risico")
EINDE ALS
```

## De Geneste selectiestructuur:

```pascal
VOERUIT(scherm, "Geef BMI:")
VOERIN(klavier, bodyMassIndex)
ALS bodyMassIndex < 18,5 DAN
	VOERUIT(scherm, "Risico voor ondergewicht")
ANDERS
	ALS bodyMassIndex > 25 DAN
		VOERUIT(scherm, "Risico voor obesitas")
	ANDERS
		VOERUIT(scherm, "Gezond")
	EINDE ALS
EINDE ALS
```

## Algoritme: De iteratie

---

```pascal
ZOLANG iteratievoorwaarde DOE
	iteratiecomponent
EINDE ZOLANG
```

> Er is geen do-while lus!

Voorbeeld: **Algoritme** Som van de eerste 10 strikt positieve gehele getallen.

Via `while` lus.

```pascal
i <- 1
som <- 0
ZOLANG i ≤ 10 DOE
	som <- som + i
	i <- i + 1
EINDE ZOLANG
VOERUIT(scherm, "som = " som)
```
Alternatief (for-loop):

> `i` moet niet verhoogd worden in deze lus.

```pascal
som <- 0
VOOR i = 1 TOT 10 DOE
	som <- som + i
EINDE VOOR
VOERUIT(scherm, "som = " som)
```

Met Stappen:

```pascal
som <- 0
VOOR i = 1 TOT 10 STAP 2 DOE
	som <- som + i
EINDE VOOR
VOERUIT(scherm, "som = " som)
```

## Methodes

**Sjabloon**

```pascal
naamAlgoritme (I: ...): ...
	* Preconditie: ...
	* Postconditie: ...
	* Gebruikt: ...
BEGIN
	1: ...
EINDE
```

Voorbeeld: Wat is het grootste getal?

```pascal
bepaalMaximum (I: a, b, c: gehele getallen): x: geheel getal
	* Preconditie: a, b en c zijn drie gehele getallen.
	* Postconditie: het maximum van drie getallen werd bepaald.
	* Gebruikt: /
BEGIN
	x <- a
	ALS (b > x) DAN
		x <- b
	EINDE ALS
	ALS (c > x) DAN
		x <- c
	EINDE ALS
	RETOUR X
EIND
```

Voorbeeld: Bepaal het aantal priemgetallen kleiner dan n.

```pascal
telPriemgetallen (I: n: geheel getal) : aantal: geheel getal
	* Preconditie: n is een natuurlijk getal.
	* Postconditie: het aantal priemgetallen kleiner dan n werd geretourneerd.
	* Gebruikt: /
BEGIN
	aantal <- 0
	p <- 2
	ZOLANG (p < n) DOE
		deler <- 2
		ZOLANG ((deler < p) EN (p MOD deler ≠ 0)) DOE
			deler <- deler + 1
		EINDE ZOLANG
		ALS (deler = p) DAN
			antal <- aantal + 1
		EINDE ALS
		p <- p + 1
	EINDE ZOLANG
	RETOUR aantal
EINDE
```

> Waarom tot vierkantswortel van n lopen:
>
> Stel n = n<sub>1</sub> x n<sub>2</sub>
>
> dan n<sub>1</sub> ≤ √n of n<sub>2</sub> ≤ √n
>
> Bewijs
>
> Stel n<sub>1</sub> > √n en n<sub>2</sub> > √n
>
> n = n<sub>1</sub> x n<sub>2</sub> > √n x √n = n
>
> Dus, n > n, kan niet = contradictie

## Methode 2: De zeef van Eratosthenes

***2*** ***3*** 4 ***5*** 6 ***7*** 8 9 10 ***11*** 12 ***13*** 14 15 16 ***17*** 18 ***19*** 20 21 22 ***23*** 24 25 26 27 28 ***29***

```pascal
telPriemgetallenEratosthenes (I: n: geheel getal) : aantal: geheel getal
	* Preconditie: n is een natuurlijk getal.
	* Postconditie: het aantal priemgetallen kleiner dan n werd geretourneerd.
	* Gebruikt: /
BEGIN
	noteer de rij van natuurlijk getallen 2, 3, ..., n - 1
	p <- 2
	aantal <- 0
	ZOLANG (p < n) DOE
		schrap in de rij van getallen alle veelvouden van p
		aantal <- aantal + 1
		ALS alle elementen uit de rij zijn geschrapt DAN
			p <- n
		ANDERS
			p <- het eerste niet geschrapte element
		EINDE ALS
	EINDE ZOLANG
	RETOUR aantal
EINDE
```

# Hoofdstuk 2

[Oefeningen](/1ste-jaar/semester-II/Oefeningen-Probleem-Oplossend-Denken-I/2.3.oefeningen.md#oefeningen-23-middot-slide-31)

> De tijd is rechtevenredig met het aantal instructies die uitgevoerd worden.
>
> We nemen aan dat alle basis instructies even lang duren, bijvoorbeeld: optelling, aftrekken, deling, vermenigvuldiging, ...

## Het aantal instructies exact gaan tellen.

### Voorbeeld 1:

```pascal
BEGIN
    kwadraat <- n . n
    RETOUR (kwadraat)
EINDE
```

| &nbsp;            | # instructies | # keer | totaal |
| ----------------- | :-----------: | :----: | :----: |
| kwadraat <- n x n | 2             | 1      | 2      |
| RETOUR(kwadraat)  | 1             | 1      | 1      |
| &nbsp;            | &nbsp;        | &nbsp; | 3      |

T(n) = 3

### Voorbeeld 2:

```pascal
BEGIN
    som <- 0
    VOOR i = 1 TOT n DOE
        som <- som + i . i
    EINDE VOOR
    RETOUR (som)
EINDE
```

| &nbsp;                                     | # instructies | # keer | totaal |
| ------------------------------------------ | :-----------: | :----: | :----: |
| som <- 0                                   | 1             | 1      | 1      |
| VOOR i = 1 TOT n DOE                       | 2             | n + 1  | 2n + 2 |
| &emsp;som <- som + i . i | 3               | n             | 3n     |        |
| EINDE VOOR                                 | &nbsp;        | &nbsp; | &nbsp; |
| RETOUR (som)                               | 1             | 1      | 1      |
| &nbsp;                                     | &nbsp;        | &nbsp; | 5n + 4 |

T(n) = 5n + 4

> Een `VOOR` lus heeft altijd 2 instructies.


### Voorbeeld 3:

```pascal
BEGIN
    grootste <- 0
    VOOR i = 0 TOT n - 1 DOE
        ALS a[i] < grootste DAN
            grootste <- a[i]
        EINDE ALS
    EINDE VOOR
    RETOUR (grootste)
EINDE
```

| &nbsp;                          | # instructies | # keer | totaal       |
| ------------------------------- | :-----------: | :----: | :----------: |
| grootste <- 0                   | 1             | 1      | 1            |
| VOOR i = 0 TOT n - 1 DOE        | 2             | n + 1  | 2n + 2       |
| &emsp;ALS a[i] < grootste DAN   | **1** c       | &nbsp; | &nbsp;       |
| &emsp;&emsp;grootste <- a[i]    | **1** c       | n      | cn           |
| &emsp;EINDE ALS                 | &nbsp;        | &nbsp; | &nbsp;       |
| EINDE VOOR                      | &nbsp;        | &nbsp; | &nbsp;       |
| RETOUR (grootste)               | 1             | 1      | 1            |
| &nbsp;                          | &nbsp;        | &nbsp; | (2 + c)n + 4 |

T(n) = (2 + c)n + 4


### Voorbeeld 4:

```pascal
BEGIN
    som <- 0
    VOOR i = 0 TOT n DOE
        VOOR j = 1 TOT n DOE
            som <- som + i . j
        EINDE VOOR
    EINDE VOOR
    RETOUR (som)
EINDE
```

| &nbsp;                          | # instructies | # keer        | totaal                  |
| ------------------------------- | :-----------: | :-----------: | :---------------------: |
| som <- 0                        | 1             | 1             | 1                       |
| VOOR i = 0 TOT n DOE            | 2             | n + 1         | 2n + 2                  |
| &emsp;VOOR j = 1 TOT n DOE      | 2             | (n + 1)n      | 2n<sup>2</sup> + 2n     |
| &emsp;&emsp;som <- som + i . j  | 3             | n<sup>2</sup> | 3n<sup>2</sup>          |
| &emsp;EINDE VOOR                | &nbsp;        | &nbsp;        | &nbsp;                  |
| EINDE VOOR                      | &nbsp;        | &nbsp;        | &nbsp;                  |
| RETOUR (grootste)               | 1             | 1             | 1                       |
| &nbsp;                          | &nbsp;        | &nbsp;        | 5n<sup>2</sup> + 4n + 4 |

T(n) = 5n<sup>2</sup> + 4n + 4

T(n) = &Theta;(n<sup>2</sup>)

> **Examen:** zorg dat je er de &Theta; bij zet!


## &Theta; notatie

> **EXAMEN:** bepaal theta notatie. (Big &Theta; Notation).

![](/afbeeldingen/1ste-jaar/semester-II/Probleem-Oplossend-Denken-I/n_is_5.png)

![](/afbeeldingen/1ste-jaar/semester-II/Probleem-Oplossend-Denken-I/n_is_50.png)

**Voorbeeld 1:**

```pascal
som <- o
VOOR i = 1 TOT n DOE
    som <- som + i
EINDE VOOR
```

T(n) = c<sub>1</sub> + c<sub>2</sub>n

= &Theta;(n)

**Voorbeeld 2:**

```pascal
som <- 0
VOOR i = 1 TOT n DOE
    VOOR j = 1 TOT i DOE
        som <- som + j
    EINDE VOOR
EINDE VOOR
```

| i    | # keer lijn 4 |
| :--: | :-----------: |
| 1    | 1             |
| 2    | 2             |
| 3    | 3             |
| n    | n             |

1 + 2 + 3 + ... + n

= ((n + 1) n) / 2

> `((n + 1) n) / 2` is een geslote formule.

T(n) = &Theta;(n<sup>2</sup>)

**Voorbeeld 3:**

```pascal
som <- 0
VOOR i = 1 TOT n DOE
    VOOR j = 1 TOT n DOE
        som <- som + j
    EINDE VOOR
EINDE VOOR
```

T(n) = &Theta;(n<sup>2</sup>)

**Voorbeeld 4:**

Stel: n = 2<sup>k</sup>

```pascal
som <- 0
i <- i
ZOLANG i ≤ n DOE
    VOOR j = 1 TOT n DOE
        som <- som + j
    EINDE VOOR
    i <- i . 2
EINDE ZOLANG
```

bv.: n = 8 = 2<sup>3</sup>

| i      | # keer lijn 6 |
| :----: | :-----------: |
| 1      | 8 (n keer)    |
| 2      | 8 (n keer)    |
| 4      | 8 (n keer)    |
| 8      | 8 (n keer)    |
| 16     | /             |
| &nbsp; | (k + 1)n      |

T(n) = ((lg(n)) + 1 ) n

T(n) = n . lg(n) + n

T(n) = &Theta;(ng lg(n))

> In &Theta; notatie zijn alle `log`, `lg`, `ln` gelijk. Ze verschillen van een factor die geen rol speelt bij deze notatie.


**Voorbeeld 5:**

Stel: n = 2<sup>k</sup>

```pascal
som <- 0
i <- i
ZOLANG i ≤ n DOE
    VOOR j = 1 TOT i DOE
        som <- som + j
    EINDE VOOR
    i <- i . 2
EINDE ZOLANG
```

| i      | # keer lijn 5 |
| :----: | :-----------: |
| 1      | 1             |
| 2      | 2             |
| 4      | 4             |
| 8      | 8             |
| 16     | /             |
| &nbsp; | (k + 1)n      |

T(n) = 1 + 2 + 4 + 8 + ... + 2<sup>k</sup>

a = 2

= 2<sup>k + 1</sup> - 1 / 2 - 1 = 2<sup>k + 1</sup> - 1 = 2 . 2<sup>k</sup> - 1 = 2n - 1

T(n) = &Theta;(n)

**Formule:**

S<sub>k</sub> = 1 + a + a<sup>2</sup> + a<sup>3</sup> + ... + a<sup>k</sup>

a . S<sub>k</sub> = a + a<sup>2</sup> + a<sup>3</sup> + ... + a<sup>k</sup> + a<sup>k + 1</sup>

---

S<sub>k</sub> - a . S<sub>k</sub> = 1 - a<sup>k + 1</sup>

(1 - a)S<sub>k</sub> = 1 - a<sup>k + 1</sup> / 1 - a = a<sup>k + 1</sup> - 1 / a - 1 = S<sub>k</sub>

# Hoofdstuk 3

[Oefeningen](/1ste-jaar/semester-II/Oefeningen-Probleem-Oplossend-Denken-I/3.4.oefeningen.md#oefeningen-34-middot-slide-45)

```pascal
0! = 1
n! = n x (n - 1)!       als n ≥ 1
```
Voorbeeld:

```
4! = 4 x 3!
   = 4 x (3 x 2!)
   = 4 x (3 x (2 x 1!))
   = 4 x (3 x (2 x (1 x 0!)))
   = 4 x (3 x (2 x (1 x 1)))
   = 4 x (3 x (2 x 1))
   = 4 x (3 x 2)
   = 4 x 6
   = 24
```

```pascal
berekenFaculteit(I: n: geheel getal): fac: geheel getal
    * preconditie: n is een natuurlijk getal
    * postcondotie: n! werd berekend
    * gebruikt: berekenFaculteit
BEGIN
    ALS n = 0 DAN
        faculteit <- 1
    ANDERS
        faculteit <- n . berekenFaculteit(n - 1)
    EINDE ALS
    RETOUR (faculteit)
EINDE
```
**Hoe lang duurt dit?**

T(0) = &Theta;(1)<br>
T(n) = T(n - 1) + &Theta;(1)    als n ≥ 1

**Na vereenvoudiging:**

T(0) = 1<br>
T(n) = T(n - 1) + 1             als n ≥ 1

**Uitwerking:**

T(0) = 1<br>
T(1) = T(0) + 1 = 1 + 1 = 2<br>
T(2) = T(1) + 1 = 2 + 1 = 3<br>
T(3) = T(2) + 1 = 3 + 1 = 4<br>
T(4) = T(3) + 1 = 4 + 1 = 5<br>

Gok:<br>
T(n) = n + 1


## Bewijs (Door inductie):

> Stel je hebt een oneindige rij van personen P<sub>0</sub>, P<sub>1</sub>, P<sub>2</sub>, P<sub>3</sub>, P<sub>4</sub>, P<sub>5</sub>, ...

1. De eerste persoon in de rij weet een geheim
2. Als een persoon een geheim weet dan vertelt die het door aan de volgende persoon in de rij.

Wie weet het geheim? Iedereen want het wordt doorgegeven.

---

```pascal
Gegeven:        T(0) = 1
                T(n) = T(n - 1) + 1             als n ≥ 1
```

Te bewijzen:    T(n) = n + 1

**Bewijs:**

> Kan op een examen komen!


```pascal
1. Basisstap: verifieer dat het te bewijzen waar is voor n = 0
    Linker Lid:     T(0)                        = 1 (gegeven)
    Rechter Lid:    n + 1 = 0 + 1               = 1

2. Inductiestap:
    Veronderstel dat T(m) = m + 1               als m ≤ n
                     (Inductiehypothese)
    T(n + 1) = T(n) + 1                         (gegeven)
             = (n + 1) + 1
             = n + 2                            QED
```

> T(n) = &Theta;(n)


## Torens van Hanoi

| n | # Bewegingen |
| - | ------------ |
| 1 | 1            |
| 2 | 3            |
| 3 | 7            |
| 4 | 15           |
| 5 | 31           |

**Recursiebetrekking:**

```pascal
T(1) = 1
T(n) = 2 T(n - 1) + 1       als n ≥ 2
```

Gok: (n) = 2<sup>n</sup>-1

---

```pascal
Gegeven:        T(1) = 1
                T(n) = 2T(n - 1) + 1             als n ≥ 2
```

Te bewijzen: T(n) = 2<sup>n</sup>-1 als ≥ 1

**Bewijs:**


1. Basisstap: verifieer dat het te bewijzen waar is voor n = 1

    Linker Lid:     T(1) = 1                    (gegeven)<br>
    Rechter Lid:    2<sup>n</sup>-1 = 2<sup>1</sup> - 1 = 2 - 1 = 1

2. Inductiestap:
    Veronderstel dat T(m) = 2<sup>m</sup> - 1   als m ≤ n
                     (Inductiehypothese)

    T(n + 1) = 2T(n) + 1 (gegeven)<br>
    (inductiefase)<br>
    = 2 . (2<sup>n</sup> - 1) + 1<br>
    = 2<sup>n + 1</sup> - 2 + 1<br>
    = 2<sup>n + 1</sup> - 1<br>

T(n) = &Theta;(2<sup>n</sup>)

\# Zetten = 2<sup>64</sup>-1 = 1,84467441 x 10<sup>19</sup>

1 Schijf per dag

\# jaar = 5,05 x 10<sup>16</sup> jaar

leeftijd aarde = 4,5 x 10<sup>19</sup> jaar

1 schijf per seconde

\# jaar = 5,85 x 10<sup>11</sup> jaar

leeftijd universum = 13,8 x 10<sup>9</sup> jaar

## De rij van Fibonacci

F<sub>0</sub> = 1<br>
F<sub>1</sub> = 1<br>
F<sub>n</sub> = F<sub>n - 1</sub> + F<sub>n - 2</sub> als n ≥ 2

> Het volgende algoritme werkt maar is zeer traag.

```pascal
berekenFibRec(I: n: geheel getal): getal: geheel getal
    * Preconditie: n is een natuurlijk getal.
    * Postconditie: het n-de Fibonacci-getal werd geretourneerd.
    * Gebruikt: berekenFibRec
BEGIN
    ALS (n = 0 of n = 1) DAN
        getal <- 1
    ANDERS
        getal <- berekenFibRec(n - 1) + berekenFibRec(n - 2)
    EINDE ALS
    RETOUR (getal)
EINDE
```
T(n) = T(n - 1) + T(n - 2) + &Theta;(1)<br>
T(n) ≥ (3/2)<sup>n-2</sup> voor n ≥ 1

> Het volgende algoritme is veel sneller.

```pascal
berekenFibIter(I: n: geheel getal): getal: geheel getal
    * Preconditie: n is een natuurlijk getal.
    * Postconditie: het n-de Fibonacci-getal werd geretourneerd.
    * Gebruikt: /
BEGIN
    voorvorig <- 1
    vorig <- 1
    getal <- 1
    VOOR i = 2 TOT n
        getal <- voorvorig + vorig
        voorvorig <- vorig
        vorig <- getal
    EINDE VOOR
    RETOUR (getal)
EINDE
```

T(n) = &Theta;(n)


# Hoofdstuk 4

> Zoek- en sorteeralgoritmen

```pascal
zoekSequentieel(I: zoekGetal: geheel getal, rij: array[] van gehele getallen): index: geheel getal
    * Preconditie: rij is een array van lengte n van gehele getallen; zoekGetal is het te zoeken element in de array.
    * Postconditie: index geeft de waarde -1 als zoekGetal niet voorkomt in rij en de waarde van de index van zoekGetal in rij als zoekGetal wel voorkomt in de rij.
    * Gebruikt: /
BEGIN
    i <- 0
    // Volgorde is cruciaal (vals en iets anders is altijd vals bij een AND) => Short Circuit Evaluation
    ZOLANG (i < n) EN (rij[i] ≠ zoekGetal) DOE
        i <- i + 1
    EINDE ZOLANG

    ALS (i = n) DAN
        index <- -1
    ANDERS
        index <- i
    EINDE ALS

    RETOUR (index)
EINDE
```

**Oefening a)**

```pascal
rij = [1, 2, 3, 4, 6]
zoekGetal = 6
```

| i   | rij[i] | iteratievoorwaarde |
| :-: | :----: | :----------------: |
| 0   | 1      | Waar               |
| 1   | 2      | Waar               |
| 2   | 3      | Waar               |
| 3   | 4      | Waar               |
| 4   | 6      | Vals               |


```pascal
? i = n
<=> 4 = 5 -> Vals
    index <- i
    index <- 4
```

> &Theta;(n)

**Oefening b)**

```pascal
rij = [6, 4, 3, 2, 1]
zoekGetal = 6
```

| i   | rij[i] | iteratievoorwaarde |
| :-: | :----: | :----------------: |
| 0   | 6      | Vals               |


```pascal
? i = n
<=> 0 = 5 -> Vals
    index <- i
    index <- 0
```

> Als je getal voorraan staat, maakt het niet uit hoe lang de rij is, je uitvoeringsstij is constant

**Oefening C)**

```pascal
rij = [1, 3, 6, 4, 2]
zoekGetal = 6
```

| i   | rij[i] | iteratievoorwaarde |
| :-: | :----: | :----------------: |
| 0   | 1      | Waar               |
| 1   | 3      | Waar               |
| 2   | 6      | Vals               |

```pascal
? i = n
<=> 2 = 5 -> Vals
    index <- i
    index <- 2
```

**Oefening D)**

```pascal
rij = [0, 2, 4, 6, 8]
zoekGetal = 5
```

| i   | rij[i] | iteratievoorwaarde |
| :-: | :----: | :----------------: |
| 0   | 0      | Waar               |
| 1   | 2      | Waar               |
| 2   | 4      | Waar               |
| 3   | 6      | Waar               |
| 4   | 8      | Waar               |
| 5   | &nbsp; | Vals               |

```pascal
? i = n
<=> 5 = 5 -> Waar
    index <- -1
```

## Gesorteerde rij

```pascal
zoekSequentieelGesorteerd(I: zoekGetal: geheel getal, rij: array[] van gehele getallen): index: geheel getal
    * Preconditie: rij is een gesorteere array van lengte n van gehele getallen; zoekGetal is het te zoeken element in de array.
    * Postconditie: index geeft de waarde -1 als zoekGetal niet voorkomt in rij en de waarde van de index van zoekGetal in rij als zoekGetal wel voorkomt in de rij.
    * Gebruikt: /
BEGIN
    i <- 0
    ZOLANG (i < n) EN (rij[i] < zoekGetal) DOE
        i <- i + 1
    EINDE ZOLANG

    ALS (i = n) OF (rij[i] > zoekGetal) DAN
        index <- -1
    ANDERS
        index <- i
    EINDE ALS

    RETOUR (index)
EINDE
```

**Oefening a)**


```pascal
rij = [1, 3, 5, 7, 9]
zoekGetal = 1
```

| i   | rij[i] | iteratievoorwaarde |
| :-: | :----: | :----------------: |
| 0   | 1      | Vals               |

```pascal
? (i = n) OF (rij[i] > zoekGetal)
<=> (0 = 5) OF (1 > 1 ) -> Vals
    index <- i
    index <- 0
```

**Oefening b)**

```pascal
rij = [1, 3, 5, 7, 9]
zoekGetal = 6
```

| i   | rij[i] | iteratievoorwaarde |
| :-: | :----: | :----------------: |
| 0   | 1      | Waar               |
| 1   | 3      | Waar               |
| 2   | 5      | Waar               |
| 3   | 7      | Vals               |

```pascal
? (i = n) OF (rij[i] > zoekGetal)
<=> (3 = 5) OF (7 > 6 ) -> Waar
    index <- -1
```

> In het beste geval: T(n) = &Theta; (1).
>
> In het slechtste geval: T(n) = &Theta;(n).
>
> In het gemiddeld geval: T(n) = &Theta;(n).

```pascal
zoekBinair(I: zoekGetal: geheel getal, rij: array[] van gehele getallen): index: geheel getal
    * Preconditie: rij is een gesorteere array van lengte n van gehele getallen; zoekGetal is het te zoeken element in de array.
    * Postconditie: index geeft de waarde -1 als zoekGetal niet voorkomt in rij en de waarde van de index van zoekGetal in rij als zoekGetal wel voorkomt in de rij.
    * Gebruikt: /
BEGIN
    l <- 0
    r <- n - 1

    ZOLANG (l ≠ r) DOE
        m <- floor((l + r) / 2)
        ALS rij[m] < zoekGetal  DAN
            l <- m + 1
        ANDERS
            r <- m
        EINDE ALS
    EINDE ZOLANG

    ALS rij[l] = zoekGetal DAN
        index <- l
    ANDERS
        index <- -1
    EINDE ALS
    RETOUR (index)
EINDE
```

> |_ getal _| = afronden naar beneden = floor


```pascal
l = 2, r = 6
m = floor((2 + 6) / 2)) = 4
```

```pascal
l = 2, r = 3
m = floor(((2 + 3) / 2)) = 2
```

> l ≤ m < r

**Oefening a)**

```pascal
rij = [1, 2, 3, 4, 6, 7, 8, 9, 10]
n = 9
zoekGetal = 3
```

| l       | r       | m       | rij[m]    |
| :-----: | :-----: | :-----: | :-------: |
| 0       | &nbsp;  | &nbsp;  | &nbsp;    |
| &nbsp;  | 8       | &nbsp;  | &nbsp;    |
| &nbsp;  | &nbsp;  | 4       | 6         |
| &nbsp;  | 4       | &nbsp;  | &nbsp;    |
| &nbsp;  | &nbsp;  | 2       | 3         |
| &nbsp;  | 2       | &nbsp;  | &nbsp;    |
| &nbsp;  | &nbsp;  | 1       | 2         |
| 2       | &nbsp;  | &nbsp;  | &nbsp;    |

```pascal
? rij[l] = zoekGetal
<=> 3 = 3 -> Waar
    index <- l
    index <- 2
```

**Oefening b)**

```pascal
rij = [1, 2, 3, 4, 6, 7, 8, 9, 10]
n = 9
zoekGetal = 5
```

| l       | r       | m       | rij[m]    |
| :-----: | :-----: | :-----: | :-------: |
| 0       | &nbsp;  | &nbsp;  | &nbsp;    |
| &nbsp;  | 8       | &nbsp;  | &nbsp;    |
| &nbsp;  | &nbsp;  | 4       | 6         |
| &nbsp;  | ***4*** | &nbsp;  | &nbsp;    |
| &nbsp;  | &nbsp;  | 2       | 3         |
| 3       | &nbsp;  | &nbsp;  | &nbsp;    |
| &nbsp;  | &nbsp;  | 3       | 4         |
| ***4*** | &nbsp;  | &nbsp;  | &nbsp;    |

> l = r

```pascal
? rij[l] = zoekGetal
<=> rij[4] = 5
    6 = 5 -> Vals
    index <- -1
```

> ^ **Op Examen!**


```pascal
zoekRecursief(I: zoekGetal: geheel getal, rij: array[] van gehele getallen): index: geheel getal
    * Preconditie: rij is een gesorteere array van lengte n van gehele getallen; zoekGetal is het te zoeken element in de array.
    * Postconditie: index geeft de waarde -1 als zoekGetal niet voorkomt in rij en de waarde van de index van zoekGetal in rij als zoekGetal wel voorkomt in de rij.
    * Gebruikt: zoek
BEGIN
    index <- zoek(zoekGetal, rij, 0, n - 1)
    RETOUR (index)
EINDE

zoek(I: zoekGetal: geheel getal, rij: array[] van gehele getallen, l, r: geheel getal): index: geheel getal
    * Preconditie: rij is een gesorteerde array van lengte n van gehele getallen; zoekGetal is het te zoeken element in de array; l en r geven respectievelijk de posities weer waartussen zoekGetal wordt gezocht.
    * Postconditie: index geeft de waarde -1 als zoekGetal niet voorkomt in rij tussen l en r en de waarde van de index van zoekGetal in rij als zoekGetal wel voorkomt in de rij tussen l en r
    * Gebruikt: zoek
BEGIN
    // Basiscase
    ALS (l = r) DAN
        ALS (rij[l] = zoekGetal) DAN
            index <- l
        ANDERS
            index <- -1
        EINDE ALS

    // Anders
    ANDERS
        m <- floor(((l + r) / 2))
        ALS (rij[m] < zoekGetal) DAN
            index <- zoek(zoekGetal, rij, m + 1, r)
        ANDERS
            index <- zoek(zoekGetal, rij, l, m)
        EINDE ALS
    EINDE ALS
    RETOUR (index)
EINDE
```

**Oefening a)**

```pascal
rij = [1, 2, 3, 4, 6, 7, 8, 9, 10]
n = 9
zoekGetal = 5
```

![](/afbeeldingen/1ste-jaar/semester-II/Probleem-Oplossend-Denken-I/zoekRecursief.png)

## Soorteeralgoritmen

### Mergesort

> Heeft dubbel zoveel geheugen nodig omdat hij een hulp array aanmaakt dat even groot is.

```pascal
rij = [44, 55, 12, 42, 94, 18, 6, 67]
```
> Rij in 2 splitsen

```pascal
// Opsplitsen in 2 delen
rij = [44, 55, 12, 42 | 94, 18, 6, 67]

// Sorteren (beide rijen recursief sorteren)
rij = [12, 42, 44, 55 | 6, 18, 67, 94]

// Volledige rij gesorteerd (samengevoegd)
rij = [6, 12, 18, 42, 44, 55, 67, 94]
```

```pascal
mergeSort (I : a: array[] van getallen) : a: array[] van getallen
    * Preconditie: de array a is gevuld met n elementen.
    * Postconditie: de array a werd gesorteerd.
    * Gebruikt: mergeSorteer.
BEGIN
    a <- mergeSorteer(a, 0, n - 1)
    RETOUR (a)
EINDE



mergeSorteer (I : a: array[ ] van getallen; begin, einde: geheel getal) : a: array[ ] van
getallen
    * Preconditie: de array a is gevuld met n elementen.
    * Postconditie: de elementen met index begin tot en met index einde werden gesorteerd.
    * Gebruikt: mergeSorteer, merge.
BEGIN
    ALS (begin < einde) DAN
        midden <- floor((begin + einde)/2)      // begin ≤ m < einde
        a <- mergeSorteer(a, begin, midden)     // Eerste helft sorteren
        a <- mergeSorteer(a, midden + 1, einde) // Tweede helft sorteren
        a <- merge(a, begin, midden, einde)     // Helften samenvoegen
    EINDE ALS
    RETOUR (a)
EINDE


merge(I: a: array[] van getallen; begin, midden, einde: geheel getal): a: array[] van getallen
    * Preconditie: de array a is gevuld met n elementen; de elementen van de deelrij gaande van de begin-positie tot en met de midden positie zijn gesorteerd; de elementen van de deelrij gaande van de (midden+1)-positie tot en met de eind-positie zijn gesorteerd.
    * Postconditie: de elementen met index begin tot en met index einde werden gesorteerd
    * Gebruikt: /
BEGIN
    i <- begin              // De teller i doorloopt de linkse deelrij
    j <- midden + 1         // De teller j doorloopt de rechtse deelrij
    hulp <- nieuwe array[n] // De hulp array
    k <- i                  // De teller k doorloopt de hulparray hulp

    ZOLANG ((i ≤ midden) EN (j ≤ einde)) DOE
        ALS a[i] ≤ a[j] DAN
            hulp[k] <- a[i]
            i <- i + 1
        ANDERS
            hulp[k] <- a[j]
            j <- j + 1
        EINDE ALS
        k <- k + 1
    EINDE ZOLANG

    ZOLANG (i ≤ midden) DOE
        hulp[k] <- a[i]
        i <- i + 1
        k <- k + 1
    EINDE ZOLANG

    ZOLANG (j ≤ einde) DOE
        hulp[k] <- a[j]
        j <- j + 1
        k <- k + 1
    EINDE ZOLANG

    VOOR k = begin TOT einde DOE
        a[k] <- hulp[k]
    EINDE VOOR

    RETOUR (a)
EINDE
```
![](/afbeeldingen/1ste-jaar/semester-II/Probleem-Oplossend-Denken-I/mergeSort.png)

> Mege T(n) = &Theta;(n)
>
> T(1) = 1
>
> T(n) = T(n / 2) = 2T(n/2) + n    // als n > 1
>
> T(n) = &Theta;(n x lg(n))
>
> VB.: 1000 = (1000 x 10) = 10.000

```pascal
// Grootste element achteraan plaatsen
VOOR i = n - 1 TOT 1 (STAP - 1) DOE
    positie <- i
    max <- a[i]

    VOOR j = i - 1 TOT 0 (STAP - 1) DOE
        ALS (a[j] > max) DAN
            positie <- j
            max <- a[j]
        EINDE ALS
    EINDE VOOR
    a[positie] <- a[i]
    a[i] <- max
EINDE VOOR

// Kleinste element vooraan plaatsen
VOOR i = 0 TOT n - 1 DOE
    positie <- i
    min <- a[i]

    VOOR j = i TOT n - 1 DOE
        ALS (a[j] < min) DAN
            positie <- j
            min <- a[j]
        EINDE ALS
    EINDE VOOR
    a[positie] <- a[i]
    a[i] <- min
EINDE VOOR
```

### Quicksort

```pascal
rij = [12, 42, 67, 55, 06, 18, 44, 84]
spil = 55 // Random element van de rij
```
> Alle elementen kleiner dan de spil, voor de spil zetten. Alle elementen groter dan de spil, achter de spil zetten. Sorteer dan recursief de rij voor de spil en de rij na de spil

```pascal
rij = [12, 42, 6, 18, 44, 55, 67, 94] // De spil staat nu op de correcte plaats
// recursief hetzelfde doen met de rij voor de spil en de rij na de spil

// Gesorteerde rij:
rij = [6, 12, 18, 42, 44, 55, 67, 94]
```

**Tijdcomplexiteit in het slechste geval**

> T(1) = 1
>
> T(n) = T(n - 1) + n // als n > 1 als grootste element als spil gebruikt wordt
>
> T(n) = n(n<sup>2</sup>)


**Tijdcomplexiteit in het beste geval**

> T(1) = 1
>
> T(n) = 2 T(n / 2) + n // als n > 1 als element de mediaan is
>
> T(n) = &Theta;(n x lg(n))

#### Mediaan-van-drie

Het eerste, middelste en laatste element kiezen als mogelijke spillen.

#### Partionering

```pascal
rij = [57, 12, 42, 67, 55, 6, 18, 44, 94]
spil = 55
// Verwissel spil met de laatste

rij = [57, 12, 42, 67, 94, 6, 18, 44, 55]

// Grote elementen moeten rechts, kleine elementen moeten links.
// Probleem 57 is groot en 44 is klein: omwisselen

rij = [44, 12, 42, 67, 94, 6, 18, 57, 55]

// 44 staat nu goed
// 12 staat nu goed
// 42 staat nu goed

// 67 staat verkeerd; we kijken naar de rechterkant
// 57 staat nu goed
// 18 staat verkeerd; we verwisselen 18 met 67

rij = [44, 12, 42, 18, 94, 6, 67, 57, 55]

// 18 staat nu goed
// 94 staat verkeerd; we kijken naar de rechterkant
// 67 staat nu goed
// 6 staat verkeerd; we verwisselen 6 met 94

rij = [44, 12, 42, 18, 6, 94, 67, 57, 55]

// Links (94) en rechts (6) zijn gewisseld; Links duid nu de eerste grote aan.

// We verwisselen nu links met het laatste element

rij = [44, 12, 42, 18, 6, 55, 67, 57, 94]

```

![](http://upload.wikimedia.org/wikipedia/commons/6/6a/Sorting_quicksort_anim.gif)

#### Mediaan-van-drie Partionering

```pascal
rij = [57 12 42 67 55 06 18 44 94]
mogelijkeSpillen = [57, 55, 94] // eerste, middelste, laatste

// De 3 spillen ordenen
rij = [55, 12, 42, 67, 57, 6, 18, 44, 94]

// We gaan wisselen met de voorlaatste omdat de laatste een mogelijke spil was
rij = [55, 12, 42, 67, 44, 6, 18, 57, 94]

// We kijken pas vanaf de eerste omdat de eerste ook een mogelijke spil was
rij = [55, 12, 42, 67, 44, 6, 18, 57, 94]
links = 67
rechts = 6

// Links en rechts zijn al gewisseld
rij = [55, 12, 42, 18, 44, 6, 57, 67, 94]
```

> Quicksort is zeer **snel** als de rijen lang zijn; Voor kleine rijen zeer **traag**.

```pascal
quickSort(I: a: array[] van getallen) : a: array[] van getallen
    * Preconditie: de array a is gevuld met n elementen.
    * Postconditie: de array a werd gesorteerd.
    * Gebruikt: quickSorteer
BEGIN
    a <- quickSorteer(a, 0, n - 1)
    RETOUR (a)
EINDE
```

```pascal
quickSorteer(I: a: array[] van getallen; begin, midden, einde: geheel getal): a: array[] van getallen
    * Preconditie: de array a is gevuld met n elementen
    * Postconditie: in de array a werden alle elementen tussen de positie begin en de positie einde gesorteerd
    * Gebruikt: quickSorteer, cardSortBis
BEGIN
    cutoff <- 5
    ALS (begin + cutoff > einde) DAN
        a <- cardSortBis(a, begin, einde)
    ANDERS
        // Spil Bepalen
        midden <- floor((begin + einde) / 2)

        ALS (a[midden] < a[begin]) DAN
            verwissel a[midden] en a[begin]
        EINDE ALS

        ALS (a[einde] < a[begin]) DAN
            verwissel a[einde] en a[begin]
        EINDE ALS

        ALS (a[einde] < a[midden]) DAN
            verwissel a[einde] en a[midden]
        EINDE ALS
        spil <- a[midden]

        // Partitioneren
        verwissel spil met a[einde - 1]

        links <- begin + 1
        rechts <- einde - 2

        ZOLANG (links ≤ rechts) DOE
            ZOLANG (a[links] < spil) DOE
                links <- links + 1
            EINDE ZOLANG

            ZOLANG (a[rehts] > spil) DOE
                rechts <- rechts - 1
            EINDE ZOLANG

            ALS (links ≤ rechts) DAN
                verwissel a[links] en a[rechts]
                links <- links + 1
                rechts <- rechts - 1
            EINDE ALS
        EINDE ZOLANG
        verwissel a[links] met spil
        spilindex <- links
        a <- quickSorteer(a, begin, spilindex - 1)
        a <- quickSorteer(a, spilindex + 1, einde)
    EINDE ALS
EINDE
```

> **Examen**: van cardSort naar CardSortBis: welke lijnen moet je aanpassen en wat moet je aanpassen:

```pascal
cardSortBis (I : a: array[] van getallen; begin, einde: geheel getal) : a: array[] van getallen
   * Preconditie: de array a is gevuld met n elementen.
   * Postconditie: in de array a werden de elementen met index begin tot en met index einde gesorteerd.
   * Gebruikt: /
BEGIN
    VOOR i = begin + 1 TOT einde DOE
        x <- a[i]
        j <- i
        ZOLANG j > begin EN x < a[j - 1] DOE
            a[j] <- a[j - 1]
            j <- j - 1
        EINDE ZOLANG
        a[j] <- x
    EINDE VOOR
    RETOUR (a)
EINDE
```

#### Voorbeeld oefening:

**14** 40 31 28 03 **15** 17 51 77 04 07 **63**<br>
14 40 31 28 03 07 17 51 77 04 **15** 63<br>
14 40 07 28 03 31 17 51 77 40 **15** 63<br>
14 40 07 03 28 31 17 51 77 40 **15** 63<br>
14 40 07 03 28 31 17 51 77 40 **15** 63<br>
14 40 07 03 **15** 31 17 51 77 40 28 63<br>

`spilIndex = 4`

"cardSort": 03 04 07 14 **15** 31 17 51 77 40 28 63 omdat 0+5 > 4 // 0 = Begin; 5 = Cutoff; Einde = 3<br>

`spilIndex = 5`

14 40 07 03 |15| **31** 17 51 **77** 40 28 **63**<br>
14 40 07 03 15 **31** 17 51 **63** 40 28 **77**<br>
14 40 07 03 15 31 17 51 28 40 **63** 77<br>
14 40 07 03 15 31 17 51 28 40 **63** 77<br>

`spilIndex = 10`

"cardSort": 14 40 07 03 15 31 17 28 31 40 51 63 77

![](/afbeeldingen/1ste-jaar/semester-II/Probleem-Oplossend-Denken-I/quickSort.png)

# Hoofdstuk 5

[Oefeningen](/1ste-jaar/semester-II/Oefeningen-Probleem-Oplossend-Denken-I/5.6.oefeningen.md#oefeningen-56-middot-slide-89-91)

Stapels:

> Een datastructuur waarbij je enkel bovenaan kan toevoegen en ook enkel het bovenste element bekijken en verwijderen: `LIFO` **(last in first out)**

```pascal
Stack(): constructor
empty(): controleert of een stapel al dan niet leeg is
push(): voegt een nieuw element toe bovenaan een stapel
pop(): verwijdert het bovenste element van een stapel en retourneert het verwijderde element
peek(): geeft het bovesnte element van de stapel terug, zonder het te verwijderen
```

| Stack |
| ----- |
| - data: array[] van Element <br> - t : geheel getal |
| + Stack(n: geheel getal) <br> + empty(): boolean <br> + push(x: Element): / <br> + pop() : Element <br> + peek(): Element |

> `t` is de top index, dus om het laatste element te zien moet je `data[t]` gebruiken.


## Implementatie van Stack()

```pascal
Stack(I: n: geheel getal): /
    * Preconditie: n is een natuurlijk getal
    * Postconditie: de array data van lengte n werd gealloceerd en t werd geïnitialiseerd
    * Gebruikt: /
BEGIN
    data <- nieuwe array[n]
    t <- - 1 // Geen element op de stapel
EINDE
```

## Implementatie van empty()

```pascal
empty(I: /): vlag: Boolean
    * Preconditie: de stapel s bestaat
    * Postconditie: de waarde true of false werd afgeleverd, afhankelijk van het feit of de stapel s leeg is of niet
    * Gebruikt: /
BEGIN
    RETOUR (t = - 1) // in java zou het ( t == - 1) zijn.
EINDE
```

## Implementatie van push(x)

```pascal
push(I: x: Element): /
    * Preconditie: de stapel s bestaat en is nog niet vol
    * Postconditie: het element x werd als top-element op de stapel s geplaatst.
    * Gebriukt: /
BEGIN
    t <- t + 1
    data[t] <- x
EINDE
```

## Implementatie van pop()

```pascal
pop(I: /): x: Element
    * Preconditie: de stapel s bestaat en is niet leeg
    * Postconditie: de top van de stapel s werd verwijderd en geretourneerd
    * Gebruikt: /
BEGIN
    x <- data[t]
    t <- t - 1
    RETOUR(x)
EINDE
```

## Implementatie van peek()

```pascal
ppeekop(I: /): x: Element
    * Preconditie: de stapel s bestaat en is niet leeg
    * Postconditie: de waarde van de top werd toegekend aan x en geretourneerd, de stapel s werd niet gewijzigd
    * Gebruikt: /
BEGIN
    RETOUR data[t]
EINDE
```

> Alle methodes zijn T(n) = &Theta;(1)

## Voorbeeld: methode one

> Bevat de stack 1 element of niet

```pascal
one(I: s: Stack): vlag: boolean
    * Preconditie: een stapel s wordt meegegeven
    * Postconditie: indien juist één element tot s behoort, werd true geretourneerd anders false; de stapel s werd niet gewijzigd.
    * Gebruikt: empty, push, pop
BEGIN
    ALS (s.empty()) DAN
        vlag <- false
    ANDERS
        x <- s.pop()
        vlag <- s.empty()
        s.push(x)
    EINDE ALS
    RETOUR vlag
EINDE
```

## Toepassing 1: controle van haakjes

```pascal
controleerHaakjes(I: uitdrukking: array[] van Strings): /
    * Preconditie: uitdrukking is een uitdrukking waarin eventueel haakjes voorkomen
    * Postconditie: indien alle open haakjes correct worden afgesloten werd er geen foutmelding gegenereerd
    * Gebruikt: Stack, empty, push, pop, lengte, getal
BEGIN
    s <- nieuwe Stack(uitdrukking.lengte)
    VOOR i = 0 TOT uitdrukking.lengte - 1 DOE
        symbool <- uitdrukking[i]
        ALS (symbool e {  ),],}  }) DAN
            s.push(symbool)
        ANDERS
            ALS s.empty() DAN
                ALS (symbool e {  ),],}  }) DAN
                    VOERUIT(scherm, "Te veel sluit symbolen")
                ANDERS
                    voorgaand <- s.pop()
                    ALS(symbool != voorgaand) DAN
                        VOERUIT(scherm, "Fout symbool")
                    EINDE ALS
                EINDE ALS
            EINDE ALS
        EINDE ALS
    EINDE VOOR
    ALS (NIET s.empty()) DAN
        VOERUIT(scherm, "Te veel open symbolen")
    EINDE ALS
EINDE
```

## Toepassing 2: het berekenen van postfix-uitdrukkingen


**Infix:**

> De operator staat tussen de operandum (parameters)

```java
3 + 4 = 7
3 + 4 x 5 = 23
(3 + 4) x 5 = 35
```

**Postfix:**

> De operatoren staan na de operandum (parameters)

```java
3 4 +
3 4 5 x +
3 4 + 5 x
```

**Uitrekenen:**


### Voorbeeld Rekenmachine 1

`3 4 5 x +`

```pascal
// De stapel
 5
 4    20
 3    3   23
---  -–- --–
```

1. Kom je een getal tegen -> op de stapel plaatsen
2. Kom je een teken tegen -> laatste 2 waarden van de stapel uitwerken en terug op de stapel plaatsen
3. Herhalen tot het einde

### Voorbeeld Rekenmachine 2

`3 4 + 5 x`


```pacal
// De stapel

 4    5
 3    7    35
---  ---  ---
```

### Van infix naar postfix

**Eigenschappen:**

1. Volgorde van getallen is altijd gelijk
2. Volgorde van getallen is niet altijd gelijk, maar kan wel
3. Er zijn nooit haakjes

**Uitwerking:**

1. Lees de invoertekst van links naar rechts
2. Een operand wordt naar de uitvoertekst geschreven
3. Een operator of een haakje wordt op de stapel bewaard als:
    * de stapel leeg is
    * de gelezen operator een hogere prioriteit heeft dan de operator die bovenaan de stapel ligt
    * het gelezen haakje een openingshaakje is
    
    Als de gelezen operator gelijke of lagere prioriteit heeft dan de operator aan de top van de stapel, dan worden alle operatoren van de stapel met gelijke of hogere prioriteit van de stapel gehaald en worden deze toegevoegd aan de uitvoertekst. Dit totdat een operator met lagere prioriteit bereikt wordt of totdat de stapel leeg is. Vervolgens wordt de ingelezen operator op de stapel geplaatst. <br>Als een sluitingshaakje wordt ingelezen dan worden alle operatoren van de stapel gehaald en toegevoegd aan de uitvoertekst totdat een openhaakje wordt bereikt. Het haakje wordt eveneens van de stapel gehaald maar niet aan de uitvoertekst toegevoegd.
4. Als het einde van de invoertekst bereikt is, worden alle operatoren van de stapel gehaald en aan de uitvoertekst toegevoegd todat de stapel leeg is 

**Voorbeeld 1:**

`(3 + 4) x 5` 

```pascal
// De Stapel

 +
 (  (     x
-- -- -- -- --
```

```pascal
// De uitvoertekst
3 4 + 5 x
```

**Voorbeeld 2:**


`a + (b + c) x d x (e + f x g)` 

```pascal
// De Stapel

             x
             +   +
 +           (   (   (
 (   (   x   x   x   x   x
 +   +   +   +   +   +   +   +
--- --- --- --- --- --- --- --- ---
```

```pascal
// De uitvoertekst
a b c + d x e f g x + x +
```

# Hoofdstuk 6

[Oefeningen](/1ste-jaar/semester-II/Oefeningen-Probleem-Oplossend-Denken-I/6.5.oefeningen.md#oefeningen-65-middot-slide-100-102)

> Wachtrijen (Queues), dit is een **FIFO structuur (First In First Out)**

* `Queue()` constructor
* `empty()` controleert of een wachtrij al dan niet leeg is
* `enqueue()` voegt een gegeven element toe aan de start van een wachtrij
* `dequeue()` verwijdert het element aan de kop in een wachtrij en retourneert het verijwderde element
* `front()` retourneert het voorste element, m.a.w. de kop, van een wachtrij zonder het te verwijderen

| Queue |
| ----- |
| - data: array[] van Element <br> - k : geheel getal <br> - s : geheel getal |
| + Queue(n: geheel getal) <br> + empty(): boolean <br> + enqueue(x: Element): / <br> + dequeue() : Element <br> + front(): Element |

**Voorbeeld:**

```pascal
|   |   |   |   |   |     // k = s = -1
| a |   |   |   |   |     // k = s = 0
| a | b |   |   |   |     // k = 0   s = 1
| a | b | c |   |   |     // k = 0   s = 2
|   | b | c |   |   |     // k = 1   s = 2
|   |   | c |   |   |     // k = 2   s = 2
|   |   | c | d |   |     // k = 2   s = 3
|   |   | c | d | e |     // k = 2   s = 4
| f |   | c | d | e |     // k = 2   s = 0
```

> Een wachtrij is een **circulaire** array, je kan dus alle plaatsen gebruiken.

## De implementatie van Queue()

```pascal
Queue(I: n: geheel getal): /
    * Preconditie: n is een natuurlijk getal
    * Postconditie: de array data van lengte n werd gealloceerd en t werd geïnitialiseerd
    * Gebruikt: /
BEGIN
    data <- nieuwe array[n]
    k <- - 1 // Geen element op de stapel
    s <- - 1
EINDE
```

## De implementatie van empty() in Queue

```pascal
empty(I: /): vlag: Boolean
    * Preconditie: de wachtrij q bestaat
    * Postconditie: de waarde true of false werd afgeleverd, afhankelijk van het feit of de wachtrij q leeg is of niet
    * Gebruikt: /
BEGIN
    RETOUR (k = -1)
EINDE
```

## De implementatie van enqueue()

```pascal
enqueue(I: x: Element): /
    * Preconditie: de wachtrij q bestaat en is nog niet vol
    * Postconditie: het element x werd aan de staart van de wachtrij q toegevoegd
    * Gebruikt: empty, length
BEGIN
    ALS empty() DAN
        k <- 0
    EINDE ALS
    
    n <- data.length
    s <- (s + 1) MOD n
    
    data[s] <- x
EINDE
```

## De implementatie van dequeue()

```pascal
dequeue(I: /): x: Element
    * Preconditie: de wachtrij q bestaat en is neit leeg
    * Postconditie: de kop van de wachtrij q werd verwijderd en geretourneerd
    * Gebruikt: length
BEGIN
    x <- data[k]
    
    ALS (k = s) DAN
        k <- -1
        s <- -1
    ANDERS
        n <- data.length
        k <- (k + 1) MOD n
    EINDE ALS
    
    RETOUR (x)
EINDE
```

## De implementatie van front()

```pascal
front(I: /): x: Element
    * Preconditie: de wachtrij q bestaat en is neit leeg
    * Postconditie: de kop van de wachtrij q werd geretourneerd, de wachtrij q werd neit gewijzigd.
    * Gebruikt: /
BEGIN
    RETOUR data[k]
EINDE
```

> Alle methodes zijn T(n) = &Theta;(1)

## Voorbeeld: methode one (in Queue)

```pascal
one(I: q: Queue): vlag: boolean
    * Preconditie: een wachtrij q wordt meegegeven; q bevat maximaal 50 elementen
    * Postconditie: indien q juist één element heeft dan werd true weergegeven anders false, de wachtrij q werd neit gewijzigd.
    * Gebruikt: Queue, empty, dequeue, enqueue
BEGIN
    ALS (q.empty()) DAN
        vlag <- false
    ANDERS
        x <- q.dequeue()
        vlag <- q.empty()
        
        qHulp <- nieuwe Queue(50)
        
        ZOLANG NIET q.empty() DOE
            qHulp.enqueue(q.dequeue())
        EINDE ZOLANG
        
        q.enqueue(x)
        
        ZOLANG NIET qHulp.empty() DOE
            q.enqueue(qHulp.dequeue())
        EINDE ZOLANG
    EINDE ALS
    
    RETOUR vlag
EINDE
```

# Hoofdstuk 7

[Oefeningen](/1ste-jaar/semester-II/Oefeningen-Probleem-Oplossend-Denken-I/7.4.oefeningen.md)

> In lijsten kan je data opvragen en verwijderen of vervangen in willekeurige plaatsen, of waar je maar wilt.

* `List()` Constructor
* `empty()` controleert of een lisjt al dan niet leeg is.
* `size()` geeft het aantal elementen van een lisjt terug
* `geefElem()` retourneert het element dat zich bevindt op de positie bepaald door het argument
* `geefPositie()` retourneert de positie van het eerste voorkomen van het meegeleverde argument
* `verwijderElem()` verwijdert het element dat zich op de positie bepaald door het argumenet bevindt en geeft dit element terug
* `invoegenNa()` het element, dat als tweede argument wordt meegeleverd, wordt ingevoegd in de lijst na de meegegeven positie.
* `invoegenVoor()` het element, dat als tweede argument wordt meegeleverd, wordt ingevoegd in de lijst voor de meegegeven positie.
* `vervang()` het element in de lijst op de positie bepaald door het eerste argument, wordt vervangen door het meegeleverde nieuwe lijstelement

| List                         |  
| ---------------------------- |
| - data: array[] van Element<br>- aantal: geheel getal |
| + List(n: geheel getal)<br>+ empty() : boolean<br>+ size() : geheel getal<br>+ geefElem(p: geheel getal) : Element<br>+ geefPositie(x: Element) : geheel getal<br>+ verwijderElem(p: geheel getal) : Element<br>+ invoegenNa(p: geheel getal, x: Element): /<br>+ invoegenVoor(p: geheel getal, x: Element): /<br>+ vervang(p: geheel getal, x: Element): / |

## Implementatie van geefElem()

```pascal
geefElem(I: p: geheel getal): x: Element
    * Preconditie: de lisjt l bestaat; l bevat minstens p+1 elementen
    * Postconditie: het element op de p-de positie in de lijst werd geretourneerd
    * Gebruikt: /
BEGIN
    RETOUR data[p]
EINDE
```

## Implementatie van geefPositie()

```pascal
geefPositie(I: x: Element): p: geheel getal
    * Preconditie: de lijst l bestaat
    * Postconditie: de positie van x werd geretourneerd
    * Gebruikt: /
BEGIN
    i <- 0
    ZOLANG i < aantal EN data[i] ≠ x DOE
        i <- i + 1
    EINDE ZOLANG
    
    ALS i = aantal DAN
        p <- -1
    ANDERS
        p <- i
    EINDE ALS
    
    RETOUR (p)
EINDE
```

## Implementatie van verwijderElem()

```pascal
verwijderElem(I: p: geheel getal): x: Element)
    * Preconditie: de lijst l bestaat
    * Postconditie: het element op de p-de positie werd verwijderd uit de lijst l en werd geretourneerd
    * Gebruikt: /
BEGIN
    x <- data[p]
    
    VOOR i = p TOT aantal - 2 DOE
        data[i] <- data[i + 1]
    EINDE VOOR
    
    aantal <- aantal - 1
    
    RETOUR (x)
EINDE
```

## Implementatie van vervang()

```pascal
vervang(I: p: geheel getal, x: Element): /
    * Preconditie: de lisjt l bestaat.
    * Postconditie: het element op de p-de positie van de lijst l werd vervangen door x
    * Gebruikt: /
BEGIN
    data[p] <- x
EINDE
```

# Hoofdstuk 8

[Oefeningen](/1ste-jaar/semester-II/Oefeningen-Probleem-Oplossend-Denken-I/8.5.oefeningen.md)

```java
class Knoop {
    private Object data;
    
    private Knoop volgende;
}

class Lijst {
    private Knoop eerste;
}
```

```java
// Hoe het echt zou zijn
class Lijst {

    private Knoop eerste;

    class Knoop {
        private Object data;
        
        private Knoop volgende;
    }
}
```

| Knoop |
| ----- |
| - data : Element<br>- volgende : Knoop |
| + Knoop() |

**Implementatie van Knoop**

```pascal
Knoop (I: /): /
    * Preconditie: /
    * Postconditie: er werd een nieuwe knoop aangemakat.
    * Gebruikt: /
BEGIN
    data <- null
    volgende <- null
EINDE
```

| GelinkteLijst |
| ------------- |
| - eerste : Knoop |
| + GelinkteLijst()<br>+ zoek(x: Element) : Knoop<br>+ verwijder(ref : Knoop): Element<br>+ voegToe(ref: Knoop, x : Element): / |

![](/afbeeldingen/1ste-jaar/semester-II/Probleem-Oplossend-Denken-I/gelinkte_lijst.png)

**Implementatie van GelinkteLijst**

```pascal
GelinkteLijst(I: /): /
    * Preconditie: /
    * Postconditie: er werd een nieuwe gelinkte lijst
    * Gebruikt: /
BEGIN
    eerste <- null
EINDE
```

## Implementatie van zoek() in GelinkteLijst

```pascal
zoek(I: x: Element): ref: Knoop
    * Preconditie: de gelinkte lijst l bestaat
    * Postconditie: de referentie naar de knoop met dataveld x werd geretourneerd, indien x niet voorkomt in de lijst werd referentie null geretourneerd.
    * Gebruikt: /
BEGIN
    ref <- eerste
    ZOLANG (ref ≠ null EN ref.data ≠ x) DOE
        ref <- ref.volgende // Equivalent van i++
    EINDE ZOLANG
    RETOUR (ref)
EINDE
```

## Implementatie van verwijder() in GelinkteLijst

![](/afbeeldingen/1ste-jaar/semester-II/Probleem-Oplossend-Denken-I/gelinkte_lijst_verwijderen.png)

```pascal
verwijder(I: ref: Knoop): x: Element
    * Preconditie: de gelinkte lijst l bestaat, ref is niet de laatste knoop in de lijst
    * Postconditie: de knoop die volgt na de knoop met referentie ref werd verwijderd uit de lijst, het data-veld van de verwijderde knoop werd geretourneerd
BEGIN
    x <- ref.volgende.data
    ref.volgende <- ref.volgende.volgende
    RETOUR (x)
EINDE
```

## Implementatie van toevoegen() in GelinkteLijst

![](/afbeeldingen/1ste-jaar/semester-II/Probleem-Oplossend-Denken-I/gelinkte_lijst_toevoegen.png)

```pascal
voegToe(I: ref: Knoop, x: Element): /
    * Preconditie: de gelinkte lijst l bestaat.
    * Postconditie: na de knoop, waarnaar gerefereerd wordt door de referentie ref, werd een nieuwe knoop met data-veld x toegevoegd.
    * Gebruikt: /
BEGIN
    hulp <- nieuwe Knoop()
    hulp.data <- x
    hulp.volgende <- ref.volgende
    ref.volgende <- hulp
EINDE
```