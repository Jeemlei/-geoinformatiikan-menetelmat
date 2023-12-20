---
title: '2.7 Taidot testiin'
date: 2023-12-20
layout: post
---

DRAFT

<!--excerpt_end-->

- Etsin alueita joissa vaikuttaisi olevan korkeusvaihtelua
- Latasin korkeusdataa yhdeksältä viereiseltä karttalehdeltä

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk7/DEM_mosaic.PNG %}" border="1">

> Paitulista ladatut korkeusmallit

- Yhdistin tasot _Mosaic To New Raster_ -työkalulla
- Tein _HillShade_ tason
- Tein slope analyysin ja visualisoin jyrkkyydet rinteiden haastavuuden mukaan
- Valitsin näiden perustella sopivan oloisen alueen

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk7/Area.png %}" border="1">

> Visualisoitu _Slope_-taso ja _HillShade_-tasolla paranneltu korkeusmalli

- Loin kolme uutta tasoa: Alue, Rinnehahmotelma ja Palveluhahmotelma
- Alue-tasolle piirsin laatikon alueen ympärille ja asetin tämän tason _Geoprocessing Environment_ -asetuksissa _Processing Extent_ ehdoksi
- Rinnehahmotelma-tasolle piirsin silmämääräisesti _Slope_-tason ja _HillShade_-tasolla parannellun korkeusmallin perusteella hahmotelmat rinteistä.
- Palveluhahmotelma-tasolle piirsin silmämääräisesti _Slope_-tason perusteella alueet, jotka olisivat potentiaalisesti tarpeeksi tasaisia rakennuksille tai parkkipaikalle.
- Tein hahmotelmatasoista kolmiulotteiset _Interpolate Shape_-työkalulla

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk7/Hahmotelmat.PNG %}" border="1">

> Hahmotellut rinteet ja alueet palveluille

- Aloin suunnitella <i>ModelBuilder</i>illa työputkea, joka tuottaisi korkeusmallin ja hahmotelmieni perusteella polygonitasot todellisista rinteistä ja sopivista palvelualueista.

<a href="{{ site.base_url }}{% link /assets/imgs/GIS2/wk7/ModelBuilder.PNG %}" target="_blank">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk7/ModelBuilder.PNG %}" border="1">
</a>

> <i>ModelBuilder</i>in työvaiheet

- Työputkessa luodaan korkeusmallista _Slope_- ja _Aspect_-tasot joista tehdään _Reclassify_-työkalulla kolme maskia: pohjois-kaakko välille suuntautuvat rinteet, 10&deg;-55&deg; jyrkät rinteet ja tasaiset alueet (0&deg;-7&deg;)
- Jyrkistä rinteistä ja rinteensuunta maskista luodaan vielä _Raster Calculator_ -työkalulla yhdistelmämaski
- Yhdistelmä maskista ja tasaisten alueiden maskista luodaan polygonitasot _Raster To Polygon_ -työkalulla
- Rinnehahmotelmien ympärille luodaan 10m bufferit
- _Clip_-työkalulla leikataan buffereista pois lasketteluun sopimattomat alueet yhdistelmämaskipolygoneilla
- _Clip_-työkalulla leikataan palveluhahmotelmista liian jyrkät alueet tasaisten alueiden polygoneilla

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk7/Rinnekahvila.PNG %}" border="1">
</p>

> Pitkien rinteiden välissä on tilaa hyvän kokoiselle rinnekahvilalle

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk7/Suunnitelma.png %}" border="1">

