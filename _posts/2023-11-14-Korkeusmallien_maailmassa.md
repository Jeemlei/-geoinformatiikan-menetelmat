---
title: '2.2 Korkeusmallien maailmassa'
date: 2023-11-14
layout: post
---

Viikon aiheena oli tutustua korkeusmallien ominaisuuksiin ja hyödyntämiseen. Tasojen metatietoihin tutustuttiin tarkemmin ja korkeusdatan pohjalta selvitettiin potentiaalisia jokiuomia hydrologisella mallinnuksella. Lisäksi harjoiteltiin muutaman rasterityökalun käyttöä.

<!--excerpt_end-->

## Korkeuden salat Kevon kanjonissa

Tällä kertaa tarkastelussa oli Kevon kanjoni Pohjois-Lapista. Varsinaisen aineistona toimi korkeusmalli ja tukena olivat maastokartta ja ortokuvat samalta alueelta.
Ensimmäisenä tarkasteltiin korkeusaineiston ominaisuuksia tason metatiedoista. Ei ollut yllätys, että projisoituna koordinaattijärjestelmänä oli _TM35FIN_ ja yksikköinä toimivat metrit. Spatiaaliseksi resoluutioksi osoittautui 2 metriä per pikseli ja itse rasterin koko oli 3000x3000 pikseliä, eli 36km^2^.
Alueen korkeus vaihteli suurin piirtein välillä 145m ja 423m merenpinnan yläpuolella. Alla olevassa kuvassa korkeimmat alueet on merkitty ruskealla ja matalimmat alueet tummanvihreällä.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/highest&lowest.PNG %}" border="1">

> Korkeusaineisto kevon kanjonista

Seuraavaksi tehtiin jo edelliseltä kurssilta tuttu rinnevalovarjostu (_hillshade_) ja korkeuskäyrät helpottamaan aineiston hahmottamista. Kun hillshade-tasoa sekoittaa (_blend_) alempiin tasoihin, antaa se kartalle syvyyttä, kuten alla olevasta kuvasta huomaa.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/highest&lowest_hillshade.PNG %}" border="1">

> Korkeusaineisto hillshade-tason kanssa

Toisaalta _hillshade_ ei anna tarkkaa kuvaa korkeusvaihtelun koosta, vaan tähän toimivat paremmin korkeuskäyrät.
Korkeusaineiston pohjalta luodut korkeuskäyrät vastasivat kohtuullisen tarkasti valmiin maastokartan korkeuskäyriä. Kuitenkin joissain kohdissa maastokartan käyrät olivat hieman tasaisempia, kun taas automaattisesti luoduissa käyrissä oli ehkä tarpeettoman paljon yksityiskohtia.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/contours.PNG %}" border="1">

> Automaattisesti luodut korkeuskäyrät osuvat tarkasti alla olevan maastokartan korkeuskäyriin.

<p align="center">
<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/contours_detail.PNG %}" width="75%" border="1">
</p>

> Tarpeettomia yksityiskohtia automaattisesti luoduissa korkeuskäyrissä
