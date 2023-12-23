---
title: '2.7 Taidot testiin'
date: 2023-12-20
layout: post
---

Viimeisellä viikolla sovellettiin kurssin aikana läpikäytyjä analyysejä ja demonstroitiin mitä on tullut opittua. Tehtävänä oli tehdä pienimuotoinen suunnitelma uudesta laskettelukeskuksesta.

<!--excerpt_end-->

## Alueen valinta ja pohja-aineisto

Ensin piti löytää sopiva alue, josta etsiä keskukselle optimaalista sijaintia korkeusdatan avulla. Hain [paikkatietoikkunasta](https://kartta.paikkatietoikkuna.fi/) eri nimisiä vaaroja ja tarkastelin aluiden korkeuskäyriä maastokartalta. Lopulta päädyin Pielisen ja Koitereen välille, missä näytti olevan huomattavan paljon korkeusvaihtelua. Latasin alueelta yhdeksän karttalehden korkeusdatan [Paitulin latauspalvelusta](https://paituli.csc.fi/download.html).

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk7/DEM_mosaic.PNG %}" border="1">
</p>

> Paitulista ladatut korkeusmallit

Yhdistin aineistot yhdeksi korkeusmalliksi _Mosaic To New Raster_ -työkalulla. Loin korkeusmallin pohjalta _HillShade_ tason ja toteutin _Slope_-analyysin, jonka tuotoksessa visualisoin 10&deg;-55&deg; jyrkät rinteet kurssimateriaalissa kuvatun vaikeusasteikon mukaa.

Näiden visualisointien ja mittaustyökalun avulla valitsin rinteen, jossa oli laajoja yhtenäisiä vaikeusasteikon kriteerit täyttäviä alueita ja pituutta useampi sata metriä.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk7/Area.png %}" border="1">

> Visualisoitu _Slope_-taso ja _HillShade_-tasolla paranneltu korkeusmalli

## Aineistojen valmistelu

Seuraavaksi aloin valmistella aineistoja soveltuvuusanalyysiä varten. Aluksi loin kolme uutta vektori-tasoa: Alue, Rinnehahmotelma ja Palveluhahmotelma.

Alue-tasolle piirsin laatikon tutkittavan alueen ympärille. Asetin tämän tason _Geoprocessing Environment_ -asetuksissa _Processing Extent_ ehdoksi, jotta tulevat analyysit toteutettaisiin kaikki vain tutkittavalta alueelta.

Rinnehahmotelma-tasolle piirsin silmämääräisesti hahmotelmat rinteistä. Varmistin _Slope_-tason ja _HillShade_-tasolla parannellun korkeusmallin perusteella, että rinteet olivat tarpeeksi jyrkkiä eivätkä vaihdelleet vähän väliä suuntaa ylös alas.

Palveluhahmotelma-tasolle rajasin alueet rinteiden lähellä, jotka olisivat potentiaalisesti tarpeeksi tasaisia rakennuksia, parkkipaikkoja tai muuta infrastruktuuria varten.

Lopuksi laitoin rinne- ja palveluhahmotelmat mukailemaan korkeusmallia _Interpolate Shape_-työkalun avulla.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk7/Hahmotelmat.PNG %}" border="1">

> Hahmotellut rinteet ja alueet palveluille

## Suunnitelman toteutus

Aloin suunnitella <i>ModelBuilder</i>illa työputkea, joka tuottaisi korkeusmallin ja hahmotelmieni perusteella polygonitasot todellisista rinteistä ja sopivista palvelualueista.

<a href="{{ site.base_url }}{% link /assets/imgs/GIS2/wk7/ModelBuilder.PNG %}" target="_blank">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk7/ModelBuilder.PNG %}" border="1">
</a>

> <i>ModelBuilder</i>in työvaiheet

Työputken ensimmäisessä vaiheessa luodaan korkeusmallista _Slope_- ja _Aspect_-tasot joista tehdään _Reclassify_-työkalulla kolme maskia: pohjois-kaakko välille suuntautuvat rinteet, 10&deg;-55&deg; jyrkät rinteet ja tasaiset alueet (0&deg;-7&deg;). Jyrkistä rinteistä ja rinteensuunta maskista luodaan vielä _Raster Calculator_ -työkalulla yhdistelmämaski.

Seuraavaksi yhdistelmä maskista ja tasaisten alueiden maskista luodaan polygonitasot _Raster To Polygon_ -työkalulla. Lisäksi rinnehahmotelmien ympärille luodaan rinnealueita kuvaavat 10m bufferit.

Lopuksi _Clip_-työkalulla leikataan buffereista pois lasketteluun sopimattomat alueet yhdistelmämaskista luoduilla polygoneilla ja palveluhahmotelmista liian jyrkät alueet tasaisten alueiden polygoneilla.

Pitkien rinteiden väliin jäi pieni tasainen alue. Tutkin vielä mittaustyökalulla mahtuisiko paikalle rakennus vai sopisiko se paremmin esimerkiksi hiihtohissin poistumispaikaksi.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk7/Rinnekahvila.PNG %}" border="1">
</p>

> Pitkien rinteiden välissä on tilaa esimerkiksi hyvän kokoiselle rinnekahvilalle

### Valmis suunnitelma

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk7/Suunnitelma.png %}" border="1">

> 2D- ja 3D-näkymät Uuronvaaran laskettelukeskus -suunnitelmasta

Suunnitelmaa olisi voinut vielä täydentää hiihtohisseillä ja teillä, jotka eivät vaadi yhtä tasaisia alueita kuin muut palvelut. Soveltuvuusanalyysiä olisi voinut myös parantaa lisäaineistoilla, esimerkiksi varmistamalla, että maaperän koostumus on sopivaa rakennettavalle infrastruktuurille. Biomassa-aineistojen avulla olisi myös mahdollista selvittää kuinka paljon metsää joudutaan kaatamaan keskuksen tieltä.

Suunnitelman toteutus sujui ilman suurempia vaikeuksia ja tuntuukin, että kurssin aikana on syntynyt hyvä rutiini <i>ArcGIS</i>in käytössä. Loppujen lopuksi työskentely on hyvin samanlaista kuin <i>QGIS</i>in kanssa ja hyvien tiedonhakutaitojen ansiosta ongelmat analyysien kanssa ovat vain hidasteita eivätkä esteistä.

Kurssin hyödyllisin oppi on ollut <i>ModelBilder</i>in olemassa olo. Lisäksi syventyminen hydrologisen mallintamisen ja näkyvyysanalyysin toimintaan konepellin alla oli erittäin mielenkiintoista.
