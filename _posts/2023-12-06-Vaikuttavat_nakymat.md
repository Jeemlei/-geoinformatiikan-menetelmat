---
title: '2.5 Vaikuttavat näkymät'
date: 2023-12-06
layout: post
---

Viikolla viisi syvennyttiin näkymäanalyyseihin, joihin sain jo pienen kosketuksen edellisen kurssin viimeisellä viikolla.<!--excerpt_end--> ([GIM 1 vk 7](https://jeemlei.github.io/geoinformatiikan-menetelmat/2023/03/07/Omatoimista_aherrusta.html#n%C3%A4kym%C3%A4analyysi))

## Aineisto

Käytettävissä oli korkeusmalli Inarin pohjoispuolisesta lapista ja pisteaineisto, joka kuvasi kuvitteellisia GSM-tukiasemia samalla alueella.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk5/Aineisto.PNG %}" border="1">
</p>

> Viikon 5 aineistot

Lisäksi analyysejä varten digitoitiin manuaalisesti vaellusreitti Kevon tutkimusaseman ja Karigasniementien parkkipaikan välillä. Käytin digitoinnissa apuna _Open Street Map_ -taustakarttaa, jossa todellinen vaellusreitti näkyi. Vaellusreitin lopulliseksi pituudeksi tuli noin 65km.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk5/vaellusreitti.png %}" border="1">
</p>

> Digitoitu vaellusreitti Kevon tutkimusaseman ja Karigasniementien parkkipaikan välillä

## Näkyvyysanalyysit

Seuraavaksi siirryttiin tutkimaan kuinka suuri osa vaellusreitistä oli GSM-tukiasemien kuuluvuusalueella.
Päätin toteuttaa analyysin edellisellä viikolla tutuksi tulleella <i>ModelBuilder</i>illa.
Ensimmäisessä vaiheessa toteutettiin _Visibility_-analyysi, jossa selvitettiin kullekkin pikselille monestako tukiasemasta siihen oli näköyhteys. Seuraavaksi uudelleen luokiteltiin rasteri maskiksi, jossa arvo 1 kuvasti pikseliä, johon on näköyhteys vähintään yhdestä tornista. Maski muunnettiin polygonitasoksi ja lopulta sen avulla poistettiin vaellusreitistä pätkät, jotka olivat polygonien kanssa päällekkäin.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk5/vaellusreitti_GSM.png %}" border="1">
</p>

> Vaellusreitin GSM-katve ja -kuuluvuusalueet

Tein vahingossa aluksi visualisoinnin väärin päin, koska vaellusreitti oli digitoinnin jäljiltä punainen ja <i>ModelBuilder</i>in luomat viivat saivat automaattisesti vihreän värin. Tämä aiheutti virheen myös seuraavassa vaiheessa ja korosti hyvien värivalintojen tärkeyttä visualisoinnissa.

### Mihin masto?

Seuraavaksi heräsikin kysymys miten GSM-kuuluvuutta voitaisiin parantaa reitillä tehokkaimmin. Sopivaa paikkaa lisämastolle lähdettiin selvittämään käänteisesti edellisen kohdan tulosten perusteella. Päätin asettaa jatkoanalyysin <i>ModelBuild</i>eriin työputken jatkoksi.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk5/ex2&3model.PNG %}" border="1">
</p>

> ModelBuilder malli, joka tekee 2. ja 3. tehtävän analyysit

Työskentelyohjeissa neuvottiin laskemaan tuotoksen tarkkuutta, mutta päätin kuitenkin kokeilla mitä korkeusmallin resoluutiolla tehty laskenta tuottaisi. Ensimmäisen prosentin jälkeen laskin, että koko analyysissä kestäisi noin 8 tuntia, joten jätin koneen raksuttamaan yön yli.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk5/high_res_time.PNG %}" width="150%" border="1">
</p>

> Korkeusmallin resoluutiolla ajetun _Visibility_-analyysin prosessointi aika

Lopputulos oli erittäin tarkka, mutta en tiedä oliko se kuitenkaan kahdeksan tunnin odottelun arvoinen. Yritin toteuttaa analyysin myös manuaalisesti asetetulla tarkkuudella, mutta en saanut sitä jostain syystä millään toimimaan. Analyysi törmäsi aina hetken prosessoinnin jälkeen virheeseen, joka ei antanut mitään järkevää virhevistiä, jonka pohjalta ongelmaa olisi voinut lähteä paremmin selvittämään.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk5/extent.PNG %}" border="1">
</p>

> Katvealueiden _Visibility_-analyysin tuotos

Joka tapauksessa sain kahdeksan tunnin tuotoksen avulla selvitettyä tarkan pikselin, josta oli suora näköyhteys mahdollisimman moneen vaellusreitin pisteeseen. Tarkka sijainti (26,7815751&deg;E 69,5328400&deg;N) ei osunut lähellekkään ennen analyysiä tekemääni arvausta optimaalisesta sijainnista.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk5/prediction_reality.PNG %}" border="1">
</p>

> Potentiaalisen GSM-tukiaseman sijainnin arvaus (.vas) ja analyysin perusteella valittu paikka

Syytän kuitenkin huonosta arviosta aiemmin mainitsemaani visualisointivirhettä. Olin nimittäin ajatellut kuuluvuualueita katvealueina ja valinnut vain koko alueen korkeimman kohdan, sillä rinne näytti vain laskevan sieltä "katvealueita" kohti. Todellisuudessa selkeästi suurin katvealue jäi pitkän kanjonin keskelle, joten uuden GSM-maston sijainnista onkin loogisesti näköyhteys kanjoniin pitkittäin reitin kulkusuunnassa.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk5/potential_tower.png %}" border="1">
</p>

### Parempi kuuluvuus?

Seuraavaksi lisättiin uusi masto ja ajettiin _ModelBuilder_ malli uudelleen. Irrotin vielä käänteisanalyysin työputken lopusta, jotten joutunut jälleen odottamaan kahdeksaa tuntia. Lopputuloksella sain visualisoitua parantuneen kuuluvuuden. Uusi GSM-tukiasema laski katvealueiden osuuden reitistä enään 31 prosenttiin aiemman 55 prosentin sijasta.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk5/vaellusreitti_GSM_new.png %}" border="1">
</p>

Loppujen lopuksi näkyvyys analyysi GSM-kuuluvuuden yhteydessä antaa kuitenkin vain karkean kuvan todellisesta kuuluvuudesta. Oikeassa elämässä esimerkiksi kasvillisuus saattaa heikentää signaalia tai erilaiset pinnat voivat heijastaa signaalin sijainteihin, joihin ei ole suoraa näköyhteyttä. Kaikki huomioon otettavat lisämuuttujat tekevät prosessoinnista kuitenkin aina raskaampaa ja toteuttamamme analyysi toimii kyllä todennäköisesti hyvänä pohjatietona esimerkkiksi maastomittausten toteuttamiseen.
