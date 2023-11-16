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

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/highest&lowest.PNG %}" width="75%" border="1">
</p>

> Korkeusaineisto kevon kanjonista

Seuraavaksi tehtiin jo edelliseltä kurssilta tuttu rinnevalovarjostu (_Hillshade_) ja korkeuskäyrät helpottamaan aineiston hahmottamista. Kun Hillshade-tasoa sekoittaa (_blend_) alempiin tasoihin, antaa se kartalle syvyyttä, kuten alla olevasta kuvasta huomaa.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/highest&lowest_hillshade.PNG %}" width="75%" border="1">
</p>

> Korkeusaineisto _Hillshade_-tason kanssa

Toisaalta _Hillshade_ ei anna tarkkaa kuvaa korkeusvaihtelun koosta, vaan tähän toimivat paremmin korkeuskäyrät.
Korkeusaineiston pohjalta luodut korkeuskäyrät vastasivat kohtuullisen tarkasti valmiin maastokartan korkeuskäyriä. Kuitenkin joissain kohdissa maastokartan käyrät olivat hieman tasaisempia, kun taas automaattisesti luoduissa käyrissä oli ehkä tarpeettoman paljon yksityiskohtia.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/contours.PNG %}" border="1">

> Automaattisesti luodut korkeuskäyrät osuvat tarkasti alla olevan maastokartan korkeuskäyriin.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/contours_detail.PNG %}" width="75%" border="1">
</p>

> Tarpeettomia yksityiskohtia automaattisesti luoduissa korkeuskäyrissä

### Korkeusmallin johdannaiset

Pehmeän laskun jälkeen oli aika tutustua korkeusmallin johdannaisiin; _Slope_- ja _Aspect_-analyyseihin. Nämä ovat työkaluja, joiden tuotokset tukevat muiden analyysien toteuttamista.

_Slope_ on funktio, joka laskee rinteen jyrkkyyden rasterin eri kohdissa korkeusdatan avulla. (Holopainen et al., 2015, s. 62) _Aspect_ puolestaan laskee rinteelle suuntatiedon. (Holopainen et al., 2015, s. 84)

Kevon alueella jyrkimmät rinteet olivat jopa 79&deg; ja luonnollisesti tasaisimmat alueet olivat lähellä 0&deg;. Alla olevassa kuvassa visualisoin tasaisimmat alueet vihreällä ja jyrkimmät alueet punaisella. Tämä toi mielestäni _Slope_-analyysin automaattisesti luomaan värimaailmaan hieman lisää informatiivisuutta.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/slopes0-1_72_45-79.PNG %}" width="75%" border="1">
</p>

> Tyylitelty _Slope_-analyysi Kevon kanjonin alueelta

Ilman värimuokkauksiakin laaksojen pohjat ja kanjonin rinteet on helppo tunnistaa, mutta lisäväri tuo paremmin esille muun muassa muutamat korkeammalla olevat lammet, jotka näkyvät hyvin myös ilmakuvissa.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/KevoOrto.PNG %}" width="75%" border="1">
</p>

> Ilmakuvia Kevon kanjonista

_Aspect_-analyysi luo tason, jossa on rinteen suunta asteina ja jokaista ilmansuuntaa vastaavalle astevälille on annettu uniikki väri. Lopputulos on hyvin sekava ihmisen tulkittavaksi, mutta muiden funktioiden käyttöön erittäin hyödyllinen.
Vaikka _Aspect_-tasoa ei olekaan varsinaisesti tarkoitettu itsessään tarkastelavaksi, vaan avuksi muita analyysejä luotaessa, voi myös sen hahmottamista helpottaa _Hillshade_-tason avulla.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/aspect.PNG %}" width="48%" border="1">
  &nbsp;
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/aspect_hillshade.PNG %}" width="48%" border="1">
</p>

> _Aspect_ analyysin tulos ja _Hillshade_-tasolla paranneltu versio

### Hydrologinen mallinnus

<table>
  <tbody>
    <tr>
      <td style="text-align: center;"> 
        Viikon harjoitusohjeissa ollut virtaussuunta ruudukko kiinnitti huomioni tietojenkäsittelytieteen opiskelijana, sillä ilmansuuntia kuvaavat numeroarvot olivat kahden potensseja, jotka tulevat hyvin tutuiksi binääri arvojen kanssa työskennellessä. Tästä heräsi hieman tangentille lähtenyt pohdiskelu suunta-datan luonteesta.
        Tieto on todennäköisesti tallennettu jokaista pikseliä vastaavaan kahdeksan bitin, eli yhden tavun, kokoiseen pakettiin. Tässä tietomuodossa tavun jokainen bitti vastaa yhtä ilman suuntaa ja kaikkien bittien ollessa 0 ollaan tasaisella maalla tai tieto puuttuu. Tässä muodossa data on mahdollisimman yksinkertaista ja ison rasterin laskutoimitukset varmasti helpottuvat.
      </td>
      <td width="30%">
        <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/flowdir_table.PNG %}" border="1">
      </td>
    </tr>
  </tbody>
</table>

---

**Viittaukset:**

- Holopainen, M., Tokola, T., Vastaranta, M., Heikkilä, J., Huitu, H., Laamanen, R., Alho, P. (2015). Geoinformatiikka luonnonvarojen hallinnassa (7. julkaisu). Helsingin yliopiston metsätieteiden laitos
