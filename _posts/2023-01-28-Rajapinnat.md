---
title: "Sukellus rajapintoihin"
date: 2023-01-28
layout: post
---

Toisessa työpajassa tarkasteltiin valintatyökaluja ja projektioiden aiheuttamia vääristymiä pinta-aloissa ja etäisyyksissä sekä pureuduttiin aineistorajapinoihin, joihin olinkin jo ehtinyt hieman tutustua edellisen viikon tehtävien yhteydessä.

### Etäisyyksien ja pinta-alojen vertailua

Tarkastelin ensin etäisyyksien ja pinta-alojen vääristymiä Suomessa eri projektioiden välillä.
Alla kuvat mitatusta alueesta ja etäisyydestä sekä taulukko mittaustuloksista eri projektioilla ja mittaustekniikoilla.

<p float="left">
    <img src="{{ site.base_url }}{% link /assets/imgs/TM35FIN_area.PNG %}" width="49%">
    <img src="{{ site.base_url }}{% link /assets/imgs/TM35FIN_dist.PNG %}" width="49%">
</p>

 Projektio       | ID         | Ellipsoidinen alue | Karteesinen alue | Ellipsoidinen etäisyys | Karteesinen etäisyys 
:---------------:|:----------:|:------------------:|:----------------:|:----------------------:|:--------------:
 TM35FIN         | EPSG:3067  | 12 069 km²         | 12 060 km²       | 533,191 km             | 533,140 km 
 Pseudo-Mercator | EPSG:3857  | 12 069 km²         | 98 582 km²       | 533,191 km             | 1166,562 km 
 World Robinson  | ESRI:54030 | 12 069 km²         | 17 045 km²       | 533,191 km             | 766,461 km 
 Sphere Behrman  | ESRI:53017 | 11 982 km²         | 12 030 km²       | 531,181 km             | 1008,841 km 
 Sphere Robinson | ESRI:53030 | 11 982 km²         | 17 008 km²       | 531,181 km             | 765,603 km 

