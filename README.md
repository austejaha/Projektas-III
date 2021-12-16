# Studentų galutinio balo skaičiuoklė #
Programa skirta apskaičiuoti kiekvieno studento galutinį balą panaudojant vidukį/medianą.

- - - 

## Veikimo principas ##

Vartotojo paprašoma įvesti:
* studento vardą ir pavardę;
* studento namų darbų pažymius (galima sugeneruoti);
* studento egzamino balą (galima sugeneruoti).

Naudojami 2 konteineriai:

* ```vector```;
* ```list```.



---------------------------------------------------------------------------------------------------------------------------------------------------------------------
### Vartotojas turi galimybę pasirinkti ###

DUOMENIS SUVESTI RANKINIU BŪDU/NUSKAITYTI IŠ FAILO

* Duomenų suvedimas rankiniu būdu:
   * vartotojas įveda studentų vardus/pavardes;
   * vartotojas įveda namų darbų pažymius;
   * vartotojas įveda egzamino balus;
   * vartotojas pasirenka kaip bus skaičiuojamas galutinis balas (naudojant vidurkį/medianą).

* Duomenų nuskaitymas iš failo:
   * vartotojas pasirenka kokio dydžio studentų sąrašą norės sugeneruoti (1 000, 10 000, 100 000, 1 000 000, 10 000 000 įrašų)  
   * programa nuskaito duomenis iš failo;
   * vartotojas pasirenka kaip bus skaičiuojamas galutinis balas (naudojant vidurkį/medianą).

NAMŲ DARBŲ PAŽYMIUS ĮVESTI RANKINIU BŪDU/SUGENERUOTI ATSITIKTINIUS

* Namų darbų pažymių įvedimas rankiniu būdu:
   * vartotojas nurodo, ar nori įvesti namų darbų pažymių kiekį:
      * **jei taip**, įveda norimą kiekį;
      * **jei ne**, įvedus pažymį klausiama, ar vartotojas nori įvesti dar vieną pažymį (taip kartojama tol, kol vartotojas nusprendžia, jog dar vieno pažymio įvesti nebenori).
* Namų darbų pažymių atsitiktinis generavimas:
   * vartotojo yra paprašoma įvesti pažymių kiekį, pažymiai sugeneruojami.    



EGZAMINO BALA ĮVESTI RANKINIU BŪDU/SUGENERUOTI ATSITIKTINĮ

* Egzamino balo įvedimas rankiniu būdu:
   * vartotojas pats įveda norimą balą.
* Egzamino balo atsitiktinis generavimas:
   * egzamino balas yra sugeneruojamas pačios programos. 

GALUTINĮ BALĄ SKAIČIUOTI NAUDOJANT VIDURKĮ/MEDIANĄ


---------------------------------------------------------------------------------------------------------------------------------------------------------------------

Įvedus visus prašomus duomenis, vartotojas nurodo, ar nori įtraukti dar vieną studentą. Programa kartojama tol, kol vartotojas nusprendžia, kad daugiau studentų įvesti nebenori.

Programa surūšiuoja studentus pagal **pavardes**.

Programa surūšiuoja studentus į dvi kategorijas: „Vargšai" (**galutinis balas < 5.0**) ir „Genijai" (**galutinis balas >= 5.0**), ir išveda į du atskirus failus: ```vargsai.txt``` ir ```genijai.txt```.


Rezultatų išvedimo į failą pavidalas:

 ```                                      
Pavardė    Vardas     Galutinis
--------------------------------

Pavardė1   Vardas2    8.50
Pavardė2   Vardas1    9.99
Pavardė3   Vardas3    7.67
 ```

**Galutinis balas** yra apskaičiuojamas pagal formulę: ```galutinis = 0.4 * vidurkis + 0.6 * egzaminas ```.

- - - 

## Įvedimo instrukcija ##

Vartotojas po kiekvieno pažymio įvedimo turi paspausti *Enter*.

Kai vartotojo prašoma pasirinkti, jis turi įvesti vieną iš nurodytų simbolių *(t/n)* - taip/ne.


Programa išmeta klaidą ir prašo pakartoti įvedimą šiais atvejais:
* Jei studento varde/pavardėje aptinka ne raidę, o neleistiną simbolį;
* Jei namų darbų pažymys/egzamino balas yra:
  * raidė;
  * simbolis;
  * ne intervale [1 - 10].
* Jei vietoje 't' arba 'n' aptinka kitą simbolį.

Sistema nutraukia darbą šiais atvejais:
* Jei failas neegzistuoja/negali buti atidarytas;
* Jei faile studento pažymys nėra intervale [0 - 10];
* Jei faile yra tuščia eilutė;
* Jei įvyksta bet kokia sisteminė klaida.

- - - 

## Programos veikimo greičio (spartos) analizė ##

* AMD Ryzen 5 4500U with Radeon Graphics 2.38 GHz procesorius
* 8 GB RAM
* 256 GB SSD
                   

Duomenų nuskaitymas

|              |   1000   |  10000  | 1000000 | 10000000 | 10000000
| ------------ | -------- | ------- | ------- | -------- | --------- 
| vector       | 0.027 s  | 0.083 s | 0.726 s | 5.704 s  | 62.679 s
| list         | 0.035 s  | 0.086 s | 0.733 s | 5.956 s  | 44.69 s

Duomenų rūšiavimas

I - oji strategija. Iš ```Studentai``` konteinerio duomenis įrašo į ```Genijai```, jei galutinis balas yra >= 5, o į ```Vargšai```, jei galutinis balas yra < 5. ```Studentai``` konteineris išlieka nepakitęs.

|              |   1000   |  10000  | 1000000 | 10000000 | 10000000
| ------------ | -------- | ------- | ------- | -------- | --------- 
| vector       | 0 s      | 0.007 s | 0.061 s | 0.613 s  | 15.192 s
| list         | 0 s      | 0.006 s | 0.058 s | 0.671 s  | 8.414 s


II - oji strategija (**optimizuota**). Studentų, kurių galutinis balas yra >= 5, duomenys keliami į ```Genijai``` konteinerį ir ištrinami iš bendro ```Studentai``` konteinerio.

|              |   1000   |  10000  | 1000000 | 10000000 | 10000000
| ------------ | -------- | ------- | ------- | -------- | --------- 
| vector       | 0 s      | 0.005 s | 0.053 s | 0.55 s   | 5.102 s
| list         | 0 s      | 0.007 s | 0.087 s | 1.014 s  | 8.814 s

III - oji strategija. Studentų, kurių galutinis balas yra >= 5, duomenys keliami į ```Genijai``` konteinerį ir ištrinami iš bendro ```Studentai``` konteinerio.

|              |   1000   |  10000  | 1000000 | 10000000 | 10000000
| ------------ | -------- | ------- | ------- | -------- | --------- 
| vector       | 0 s      | 0.004 s | 0.045 s | 0.493 s  | 4.639 s
| list         | 0 s      | 0.006 s | 0.061 s | 0.754 s  | 6.428 s


```struct``` ir ```class``` spartos palyginimas. Pasirinktas ```list``` konteineris ir III - oji strategija. 

| ```list```   |   1000   |  10000  | 1000000 | 10000000 | 10000000
| ------------ | -------- | ------- | ------- | -------- | --------- 
| ```struct``` | 0 s      | 0.006 s | 0.061 s | 0.754 s  | 6.428 s
| ```class```  | 0 s      | 0.009 s | 0.062 s | 0.745 s  | 12.072 s
| ```O1```     | 0 s      | 0.004 s | 0.035 s | 0.268 s  | 3.919 s
| ```O2```     | 0 s      | 0.002 s | 0.028 s | 0.257 s  | 2.581 s
| ```O3```     | 0 s      | 0.003 s | 0.028 s | 0.254 s  | 2.576 s
  
- - -

## Apie programą ##





### Įdiegimas ####
* Atsisiųskite ir išarchyvuokite programą;
* Paleiskite programą naudodami komandinę eilutę:
```
   g++ -o main projektas.cpp
   ./main
   ```

### Versijos ###

* [v0.1](https://github.com/austejaha/Projektas/tree/v0.1) Pirminė programos versija. Programa yra realizuota dviem būdais: naudojant ```C``` tipo masyvą - **masyvas.cpp** ir ```<vector>``` tipo konteinerį - **vektorius.cpp**. 
* [v0.2](https://github.com/austejaha/Projektas/tree/v0.2) Pridėta nuskaitymo iš tekstinio failo funkcija. Programa realizuota naudojant ```<vector>``` tipo konteinerį. 
* [v0.3](https://github.com/austejaha/Projektas/tree/v0.3) Pridėtas išimčių valdymas (angl. Exception Handling). Funkcijos išskirstytos į failus.
* [v0.4](https://github.com/austejaha/Projektas/tree/v0.4) Sukurta funkcija, kuri generuoja atsitiktinius studentų sąrašų failus (1 000, 10 000, 100 000, 1 000 000, 10 000 000 įrašų). Pridėtas studentų surūšiavimas į dvi kategorijas: „Idiotai" (**galutinis balas < 5.0**) ir „Genijai" (**galutinis balas >= 5.0**), ir išvedimas į du atskirus failus: ```vargšai.txt``` ir ```genijai.txt```. Atlikta programos veikimo greičio (spartos) analizė.
* [v0.5](https://github.com/austejaha/Projektas/tree/v0.5) Pridėta galimybė pasirinkti norimą konteinerį (```vector```, ```list```). Atlikta ir aprašyta spartos analizė.
* [v1.0](https://github.com/austejaha/Projektas/tree/v1.0) Pridėta galimybė pasirinkti norimą grupavimo strategiją. Atlikta šių strategijų spartos analizė. Pridėtas CMakeLists.txt
* [v1.1](https://github.com/austejaha/Projektas-II/tree/v1.1) Struktūra pakeista į klasę, atnaujinta spartos analizė.
* [v1.2](https://github.com/austejaha/Projektas-II/tree/v1.2) Realizuota **„Rule of three"**.
* [v1.5](https://github.com/austejaha/Projektas-II/tree/v1.5) Sukurtos dvi klasės: **bazinė**: ```zmogus``` ir **išvestinė**: ```studentas```.



