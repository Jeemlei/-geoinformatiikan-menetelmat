---
title: "Projektioiden pauloissa"
date: 2023-01-28
layout: post
---

Toisessa työpajassa tarkasteltiin valintatyökaluja ja projektioiden aiheuttamia vääristymiä pinta-aloissa ja etäisyyksissä sekä pureuduttiin aineistorajapinoihin, joihin olinkin jo ehtinyt hieman tutustua edellisen viikon tehtävien yhteydessä.
<!--excerpt_end-->

### Monipuolisia valintoja

Työpajan alussa kävimme läpi _QGIS_:in valintatyökaluja, joita onkin erittäin laaja kirjo. Kartalle on muunmuassa mahdollista piirtää alueita, joiden sisältä kaikki kohteet valitaan. Tietojenkäsittelytieteilijänä mielenkiintoisin työkalu oli kuitenkin "_Select by Expression_", jolla on mahdollista kirjoittaa monimutkaisiakin sääntöjä, jotka hyödyntävät valinnassa kohteiden attribuutteja.

Teinkin "_Select by Expression_"-valintatyökalun avulla kartan, jossa korostin Etelä-Karjalan.

<p float="center">
    <img src="{{ site.base_url }}{% link /assets/imgs/Etelä-Karjala.png %}" width="50%">
</p>

> Etelä-Karjala eriytettynä muusta aineistosta valintatyökalun avulla

### Etäisyyksien ja pinta-alojen vertailua

Tarkastelin etäisyyksien ja pinta-alojen vääristymiä Suomessa eri projektioiden välillä.
Alla kuvat mitatuista alueesta ja etäisyydestä sekä taulukko mittaustuloksista eri projektioilla ja mittaustekniikoilla.

<p float="left">
    <img src="{{ site.base_url }}{% link /assets/imgs/TM35FIN_area.PNG %}" width="49%" border="1">
    <img src="{{ site.base_url }}{% link /assets/imgs/TM35FIN_dist.PNG %}" width="49.5%" border="1">
</p>

 Projektio       | ID         | Ellipsoidinen alue | Karteesinen alue | Ellipsoidinen etäisyys | Karteesinen etäisyys 
:---------------:|:----------:|:------------------:|:----------------:|:----------------------:|:--------------:
 TM35FIN         | EPSG:3067  | 12 069 km²         | 12 060 km²       | 533 km                 | 533 km 
 Pseudo-Mercator | EPSG:3857  | 12 069 km²         | 98 582 km²       | 533 km                 | 1166 km 
 World Robinson  | ESRI:54030 | 12 069 km²         | 17 045 km²       | 533 km                 | 766 km 
 Sphere Behrman  | ESRI:53017 | 11 982 km²         | 12 030 km²       | 531 km                 | 1008 km 
 Sphere Robinson | ESRI:53030 | 11 982 km²         | 17 008 km²       | 531 km                 | 765 km 

_TM35FIN_-projektiossa erot ellipsoidin ja tason pinnalta mitattujen tulosten välillä ovat erittäin pieniä, mikä osoittaa projektion hyvän soveltuvuuden Suomen kuvantamiseen tasokartalla.
Seuraavassa taulukossa vielä muiden projektioiden mittausten erot verrattuna _TM35FIN_-projektioon.

 Projektio       | Ellipsoidinen alue | Karteesinen alue   | Ellipsoidinen etäisyys | Karteesinen etäisyys 
:---------------:|:------------------:|:------------------:|:----------------------:|:--------------:
 Pseudo-Mercator | 0 km² / 100%       | 86 522 km² / ~817% | 0 km / 100%            | 633 km / ~219%
 World Robinson  | 0 km² / 100%       | 4 985 km² / ~141%  | 0 km / 100%            | 233 km / ~144%
 Sphere Behrman  | -87 km² / ~99,3%   | -30 km² / ~99,8%   | -2 km / ~99,6%         | 475 km / ~189%
 Sphere Robinson | -87 km² / ~99,3%   | 4 948 km² / ~141%  | -2 km / ~99,6%         | 232 km / ~144%

 Mittauksista huomataan hyvin kuinka vääristymät kasvavat projektiosta riippuen jopa lähes kymmenkertaisiksi, kun mittauksia tehdään tasolla ellipsoidin sijaan. Ellipsoidilla mitattaessa tulokset ovat keskimäärin lähempänä totuutta, sillä maapallon pinta on todellisuudessa lähempänä ellipsoidia kuin tasoa.

#### Vääristymien visualisointi

Pinta-alavääristymien visualisointiin latasin aineiston _WFS_-rajapinnan kautta, jonka toiminnasta ja eroista muihin rajapintoihin saimme vielä aiempaa tutkiskeluani tarkemman kuvauksen.

Vertailukohtana käytin _LAEA Europe_ -projektiota (EPSG:3035), joka on eurooppa keskeinen projektio ja pyrkii minimoimaan vääristymät koossa ja suunnissa. (Annoni, Luzet, Gubler & Ihde, 2001, s. 123.)
Vertailtaviksi projektoiksi valitsin _Spehere Mercator_ -projektion (ESRI:53004) sekä _North Pole Azimuthal Equidistant_ -projektion (ESRI:102016).

<p float="left">
    <img src="{{ site.base_url }}{% link /assets/imgs/SphMerc.png %}" width="49%" border="1">
    <img src="{{ site.base_url }}{% link /assets/imgs/NPoleAzimuth.png %}" width="49%" border="1">
</p>

Mercatorin projektioissa tunnetusti vääristymät kasvavat mentäessä kauemmaksi "projektiolieriön" pallonpintaa koskettavasta keskilinjasta, joka _Spehere Mercator_ -projektiossa kulkee päiväntasaajalla. Koska Suomi on hyvin kaukana päiväntasaajalta kasvavat vääristymät tasolla moninkertaisiksi mitä pohjoisemmaksi mennään, ja onkin luontevaa esittää muutos 100% askelilla.

_North Pole Azimuthal Equidistant_ -projektio pitää etäisyydet keskipisteeseensä nähden oikeina (Wikimedia Foundation, 2023) ja, kuten nimestäkin voi arvata, keskipisteenä on porhjoisnapa. Koska pinta-alan vääristymät kasvavat mitä kauemmaksi keskipisteestä mennään, on vääristymien muutos visualisoinnissa päinvastainen kuin _Spehere Mercator_ -projektiolla. Muutokset ovat Suomen kohdalla kuitenkin vain muutaman prosentin luokkaa, sillä etäisyys pohjoisnavalle on vielä kohtuullisen pieni.

---

**Lähteet:**
- Annoni, A., Luzet, C., Gubler, E. & Ihde, J. (2001) _Map Projections for Europe_. - Ladattu 5.2.2023. [http://mapref.org/LinkedDocuments/MapProjectionsForEurope-EUR-20120.pdf](http://mapref.org/LinkedDocuments/MapProjectionsForEurope-EUR-20120.pdf)
- Wikimedia Foundation (2023) _Azimuthal equidistant projection_ - Vierailtu 5.2.2023. [https://en.wikipedia.org/wiki/Azimuthal_equidistant_projection](https://en.wikipedia.org/wiki/Azimuthal_equidistant_projection)