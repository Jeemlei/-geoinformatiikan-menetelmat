---
title: '2.6 Mittausten välillä'
date: 2023-12-14
layout: post
---

Kuinka esittää pintamaisia ilmiöitä, kun mittauksista saadaan vain pistemäinen aineisto? Tähän kysymykseen löytyy monenlaisia ratkaisuja erilaisista interpolointimenetelmistä.

<!--excerpt_end-->

## Deterministisiä interpolintimenetelmiä

Viikolla kuusi tutustuttiin neljään deterministiseen interpolointimenetelmään, jotka tuottavat pisteaineiston pohjalta jatkuvan aineiston joko polygoneina tai rasterina.

| Menetelmä                                | Arvon vaikutus | Alkuperäiset arvot |
| ---------------------------------------- | -------------- | ------------------ |
| Thiessenin polygonit                     | lokaali        | säilyvät           |
| Trendipintainterpolointi                 | globaali       | voivat muuttua     |
| Inverse Distance Weighted -interpolointi | lokaali        | voivat muuttua     |
| Spline interpolointi                     | lokaali        | säilyvät           |

Tutkittavana aineistona toimivat vuoden 2020 lämpötilamittaukset eri puolilta Suomea. Koska arvot olivat lämpötiloja, pyrin visualisoinneissani käyttämään positiivisille arvoille punaisen sävyjä ja negatiivisille sinisen sävyjä. Lisäksi mielestäni oli luontaista asettaa värien edustamat arvovälit yhtä suuriksi toisiinsa verrattuna, jolloin esimerkiksi kapeampi värikaistale kuvaa loogisesti nopeampaa lämpötilan muutosta kahden alueen välillä kuin leveämpi.

### Thiessenin plygonit

_Thiessenin polygonit_ on hyvin yksinkertainen menetelmä, jossa kunkin lähtöaineiston pisteen ympärille luodaan polygoni, jonka jokainen kohta on lähempänä alkuperäistä pistettä kuin mitään muuta aineiston pistettä. Luotu polygoni saa alkuperäisen pisteen arvon.

_Thiessenin polygonit_ poikkeaa kolmesta muusta menetelmästä siinä, että se luo polygonitason rasteritason sijaan ja tuotos sisältää ainoastaa alkuperäisen aineiston arvoja. Toisin sanoen lähtöaineiston pisteiden välille ei synny hitaasti muuttuvia arvoja, vaan arvot vaihtuvat jyrkästi yhdestä toiseen polygonien rajalla. Tämä mahdollistaisi menetelmän käyttämistä siis myös ei jatkuvissa muuttujissa. Esimerkiksi lähimpien ruokakauppojen selvittäminen onnistuisi aineistosta, jossa kutakin ruokakauppaa kuvaisi piste, jolla olisi uniikki numero.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk6/Thiessen.png %}" width="90%" border="1">
</p>

> Thiessenin polygoneilla interpoloidut lämpötilamittaukset

### Trendipintainterpolointi

Trendipintainterpolinneissa pikseleiden arvojen laskemisessa käytetään polynomifunktiota, joka pyritään sovittamaan vastaamaan lähtöaineiston pisteiden arvoja mahdollisimman hyvin. Polynomifunktion aste vaikuttaa siihen kuinka lähelle todellisuutta päästään.

Viikon harjoituksissa käytettiin ensimmäisen, toisen ja kolmannen asteen polynomifunktioita, jotka antavat vain karkean kuvan tarkasteltavan muuttujan globaalista muutossuunnasta. Lopputuloksesta on siis vaikea tehdä tarkkoja päätelmiä alueiden todellisista keskilämpötiloista, sillä jokainen arvo lähtöaineistossa vaikuttaa jokaiseen lopputuloksen arvoon ja lähes kaikki arvot ovat todennäköisesti edes hieman vääristyneitä. Kartasta voidaan kuitenkin nähdä trendinä, että lämpötilat kylmenevät pohjoiseen ja koilliseen liikuttaessa.

<p align="center">
  <a href="{{ site.base_url }}{% link /assets/imgs/GIS2/wk6/Trendipinta1.png %}" target="_blank">
    <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk6/Trendipinta1.png %}" width="45%" border="1">
  </a>
  <a href="{{ site.base_url }}{% link /assets/imgs/GIS2/wk6/Trendipinta2.png %}" target="_blank">
    <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk6/Trendipinta2.png %}" width="45%" border="1">
  </a>
  <br>&nbsp;<br>
  <a href="{{ site.base_url }}{% link /assets/imgs/GIS2/wk6/Trendipinta3.png %}" target="_blank">
    <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk6/Trendipinta3.png %}" width="45%" border="1">
  </a>
</p>

> Lämpötilamittauksista kolmen eri asteen funktioilla interpoloidut trendipinnat

### _Inverse Distance Weighted_ -interpolointi (_IDW_)

_IDW_ -interpolointi on menetelmä, jossa lähtöpisteiden arvot painottuvat enemmän mitä lähempänä ne ovat tarkasteltavaa pikseliä. Menetelmä soveltuu siis erityisesti ilmiöiden tutkimiseen, joiden vaikutus on hyvin lokaali. Kokonaisuudessaan _IDW_-interpolointi keskiarvoistaa aineiston arvojoukkoa, mikä tarkoittaa, että alkuperäisissä mittaussijanneissa arvot myös vääristyvät hieman. Poikkeamien suuruuteen voidaan kuitenkin vaikuttaa muun muassa säätämällä etäisyys kertoimen eksponenttia ja huomioon otettavien pisteiden lukumäärää.

_IDW_-interpoloinnin asetusten optimoimiseen käytettiin <i>ArcGIS</i>in _Geostatistical Wizard_-työkalua. Työkalu mahdollisti _IDW_-interpoloinnin tuottaman virheen tarkastelun, mikä auttoi sopivan eksponentin ja vaikuttavien pisteiden lukumäärän valitsemisessa.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk6/IDW_method_report.PNG %}" width="90%" border="1">
  <br>
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk6/IDW_mean.PNG %}" width="65%" border="1">
</p>

> _Geostatistical Wizard_-työkalulla valitut _IDW_-interpoloinnin asetukset ja virhemarginaalit

_IDW_-interpoloinnin lopputulos on selvästi tähän astisista menetelmistä luonnollisimman näköinen, mutta sen alkuperäisiin arvoihin tuottamat virheet ovat pieni haittapuoli lämpötilaa tutkittaessa.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk6/IDW.png %}" width="90%" border="1">
</p>

> _IDW_-interpoloidut lämpötilamittaukset

### _Spline_-interpolointi

_Spline_-interpoloinnissa tuotetaan saman arvon käyriä, jotka kulkevat suoraan lähtöjoukon pisteiden kautta ja tuottavat tasaisesti muuttuvia arvoja pisteiden välille. Menetelmä soveltuu parhaiten hitaasti muuttuvien arvojen, kuten juurikin lämpötilojen, kuvaamiseen. Lisäksi isona plussana alkuperäiset pisteet säilyttävät arvonsa.

_Spline_-interpoloinnilla toteutettiin 12 kuukauden aikasarja keskilämpötiloista ja koska työ sisälsi paljon toistoa, otettiin avuksi jälleen jo tutuksi tullut _ModelBuilder_.

<a href="{{ site.base_url }}{% link /assets/imgs/GIS2/wk6/Spline_12kk_model.PNG %}" target="_blank">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk6/Spline_12kk_model.PNG %}" border="1">
</a>

> ModelBuilder työputki 12kk aikasarjan luomiseen

Viikon aineistossa oli mukana myös valmis symbologia visualisointia varten, jonka liitin työputken loppuun. Valmis tyyli sisälsi huomattavasti enemmän lämpötilaluokkia kuin omat visualisointini aiemmissa kartoissa. Tämä luo kokonaisuuteen ehkä hieman enemmän sekavuutta, mutta mahdollista toisaalta paikallisten muutosten yksityiskohtaisemman tarkastelun. Lopputulos antaa joka tapauksessa selkeän kuvan vuodenaikojen tuomasta lämpötilavaihtelusta eri puolilla Suomea.

<a href="{{ site.base_url }}{% link /assets/imgs/GIS2/wk6/Spline_map_highres.png %}" target="_blank">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk6/Spline_map_lowres.png %}" border="1">
</a>

> Spline interpoloitu 12kk aikasarja
