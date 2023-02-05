---
title: "Sukellus rajapintoihin"
date: 2023-01-28
layout: post
---

Toisessa työpajassa tarkasteltiin valintatyökaluja ja projektioiden aiheuttamia vääristymiä pinta-aloissa ja etäisyyksissä sekä pureuduttiin aineistorajapinoihin, joihin olinkin jo ehtinyt hieman tutustua edellisen viikon tehtävien yhteydessä.

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

TM35FIN-projektiossa erot ellipsoidin ja tason pinnalta mitattujen tulosten välillä ovat erittäin pieniä, mikä osoittaa projektion hyvän soveltuvuuden Suomen kuvantamiseen tasokartalla.
Seuraavassa taulukossa vielä muiden projektioiden mittausten erot verrattuna TM35FIN-projektioon.

 Projektio       | Ellipsoidinen alue | Karteesinen alue   | Ellipsoidinen etäisyys | Karteesinen etäisyys 
:---------------:|:------------------:|:------------------:|:----------------------:|:--------------:
 Pseudo-Mercator | 0 km² / 100%       | 86 522 km² / ~817% | 0 km / 100%            | 633 km / ~219%
 World Robinson  | 0 km² / 100%       | 4 985 km² / ~141%  | 0 km / 100%            | 233 km / ~144%
 Sphere Behrman  | -87 km² / ~99,3%   | -30 km² / ~99,8%   | -2 km / ~99,6%         | 475 km / ~189%
 Sphere Robinson | -87 km² / ~99,3%   | 4 948 km² / ~141%  | -2 km / ~99,6%         | 232 km / ~144%

 Mittauksista huomataan hyvin kuinka vääristymät kasvavat projektiosta riippuen jopa lähes kymmenkertaisiksi, kun mittauksia tehdään tasolla ellipsoidin sijaan. Ellipsoidilla mitattaessa tulokset ovat keskimäärin lähempänä totuutta, sillä maapallon pinta on todellisuudessa lähempänä ellipsoidia kuin tasoa.