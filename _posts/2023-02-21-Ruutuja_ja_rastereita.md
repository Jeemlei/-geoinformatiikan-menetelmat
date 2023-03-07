---
title: "Ruutuja ja rastereita"
date: 2023-02-21
layout: post
---

Viikon aiheina olivat rasteridatan luominen vektoriaineiston pohjalta ja rasteriaineistojen käsittely. Harjoituksista tuli opittua paljon, sillä aiheet poikkesivat paljon aiemmilta kurssikerroilta, joissa oli pyöritty lähinnä vektorien ympärillä.
<!--excerpt_end-->

### Pääkaupunkiseudun rakennukset

Ensimmäisessä tehtävässä oli tarkoituksena luoda ruudukko pääkaupunkiseudun alueelle, johon kerättiin dataa alueen väestöstä. Käytettävissä oli pisteaineisto pääkaupunkiseudun rakennuksista.

Tehtävässä pääsi hyödyntämään edellisellä kurssikerralla käytettyä työkalua, jolla vertailtiin pisteaineiston ominaisuuksien sijaintia toisen aineiston monikulmioiden sijaintiin. Tällä kertaa kuitenkin yksittäisten ominaisuuksien lukumäärien laskemisen sijaan laskettiinkin pisteaineiston attribuuttitaulun arvoja, kuten asukaslukuja, yhteen ja liitettiin niitä aiemmin luotuun ruudukkoon.

Päätin toteuttaa visualisoinnin sekä 250m<sup>2</sup> että 500m<sup>2</sup> tarkkuudella ja tarkastella alueiden rakennusten keskimääräistä asukkaiden lukumäärää.

<img src="{{ site.base_url }}{% link /assets/imgs/Pks_vaki_500x500.png %}" width="100%">

> 500m x 500m ruuduissa olevien asuinrakennusten keskimääräinen asukkaiden lukumäärä

Asetin väri asteikon vihreän päädyn erottelemaan selkeästi alueet, joilla on paljon muutaman ihmisen omakotitaloja. Asteikon toinen pää sisältää taas karkeammin alueet, joiden rakennuksissa asuu keskimäärin kymmeniä tai satoja asukkaita. Tämä jaottelu tuo selkeästi 500m<sup>2</sup> tarkkuudella esille kerrostalorikkaat asutuskeskittymät, kuten Espoon keskuksen ja Leppävaaran, mutta ei häivytä harvemmin asutettujen alueiden eroja, joissa voi olla paljon omakotitaloja tai pienempiä kerrostaloja.

<img src="{{ site.base_url }}{% link /assets/imgs/Pks_vaki_250x250.png %}" width="100%">

> 250m x 250m ruuduissa olevien asuinrakennusten keskimääräinen asukkaiden lukumäärä

250m<sup>2</sup> tarkkuudella yksittäiset rakennukset alkavat vaikuttaa enemmän ja kartasta tulee ainakin omasta mielestäni hieman vaikeampi tulkita. Kartan sekavampi vaikutelma tulee osittain ehkä myös siitä, että ruudukko pirstoutuu enemmän, sillä rakennettujen alueiden välisi 250m<sup>2</sup> alueita on huomattavasti enemmän kuin 500m<sup>2</sup> alueita.

### Korkeusdataa Pornaisita

<img src="{{ site.base_url }}{% link /assets/imgs/Pornainen.png %}" width="100%">

> Korkeusdatasta luodut korkeuskäyrät ja rinnevarjostus Pornaisten kartalla

<img src="{{ site.base_url }}{% link /assets/imgs/Korkeuskayrat.png %}" width="100%">

> Automaattisesti luotujen korkeuskäyrien outouksia Pornaisten keskustan tuntumassa
