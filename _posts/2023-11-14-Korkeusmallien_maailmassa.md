---
title: '2.2 Korkeusmallien maailmassa'
date: 2023-11-14
layout: post
---

Viikon aiheena oli tutustua korkeusmallien ominaisuuksiin ja hyödyntämiseen. Tasojen metatietoihin tutustuttiin tarkemmin ja korkeusdatan pohjalta selvitettiin potentiaalisia jokiuomia hydrologisella mallinnuksella. Lisäksi harjoiteltiin muutaman rasterityökalun käyttöä.

<!--excerpt_end-->

## Korkeuden salat Kevon kanjonissa

Tällä kertaa tarkastelussa oli Kevon kanjoni Pohjois-Lapista. Varsinaisena aineistona toimi korkeusmalli ja tukena olivat maastokartta ja ortokuvat samalta alueelta.
Ensimmäisenä tarkasteltiin korkeusaineiston ominaisuuksia tason metatiedoista. Ei ollut yllätys, että projisoituna koordinaattijärjestelmänä oli _TM35FIN_ ja yksikköinä toimivat metrit. Spatiaaliseksi resoluutioksi osoittautui 2 metriä per pikseli ja itse rasterin koko oli 3000x3000 pikseliä, eli 36km<sup>2</sup>.
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

> Automaattisesti luodut korkeuskäyrät osuvat tarkasti alla olevan maastokartan korkeuskäyriin

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
        Hydrologisella mallinnuksella tarkoitetaan erilaisia analyysejä veden valumiseen liittyen. (Holopainen et al., 2015, s. 51)
      </td>
    </tr>
  </tbody>
</table>

Ennen varsinaisia analyysejä visualisoitiin korkeusdatassa olevat kuopat, eli analyysien potentiaaliset umpikujat. Korkeusdatasta luotiin ensin _Sink_-työkalulla rasteri kaikista kuopista, joka edelleen muunnettiin vektoritasoksi _Raster to Point_ -työkalulla.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/sinks.PNG %}" width="75%" border="1">
</p>

> Korkeusdatan kuopat visualisoituna pisteinä

Kuten visualisoinnista voi huomata kuopat olivat erityisesti "pakkautuneet" kanjoneihin, jotka ovat juurikin potentiaalisimpia uomien sijainteja. Kuopat oli siis täytettävä _Fill_-työkalulla, jotta hydrologinen mallinnus onnistuisi parhaalla mahdollisella tavalla. Kuopattoman korkeusmallin pohjalta luotiin virtaussuunta-rasteri _Flow Direction_ -työkalulla

<table>
  <tbody>
    <tr>
      <td style="text-align: center;"> 
        Viikon harjoitusohjeissa ollut virtaussuunta ruudukko kiinnitti huomioni tietojenkäsittelytieteen opiskelijana. Ruudukossa ilmansuuntia kuvaavat numeroarvot olivat kahden potensseja, jotka tulevat hyvin tutuiksi binääri arvojen kanssa työskennellessä. Tästä heräsi hieman tangentille lähtenyt pohdiskelu suunta-datan luonteesta.
        Tieto on todennäköisesti tallennettu jokaista pikseliä vastaavaan kahdeksan bitin, eli yhden tavun, kokoiseen pakettiin. Tässä tietomuodossa tavun jokainen bitti vastaa yhtä ilmansuuntaa ja kaikkien bittien ollessa 0 ollaan tasaisella maalla tai tieto puuttuu. Tässä muodossa data on mahdollisimman yksinkertaista ja isommankin rasterin laskutoimitukset varmasti helpottuvat homattavasti.
      </td>
      <td width="30%" style="text-align: center;">
        <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/flowdir_table.PNG %}" border="1">
      </td>
    </tr>
  </tbody>
</table>

Virtaussuunta-rasterin avulla saatiin vihdoin tehtyä ensimmäinen hydrologinen mallinnus _Basin_-työkalulla, joka palautti rasterin kanjonin valuma-alueista. Ja jälleen pääsimme käyttämään yhtä _Raster to..._ -työkaluista, jolla muunsimme rasterin polygoneiksi.

Valuma-alueissa oli paikoittain outouksia, joissa monta yhden pikselin levyistä valuma-aluetta kurkotti tason reunaan vieri vieressä. Oma päätelmäni tästä oli, että alueella kulkisi todellisuudessa leveämpi uoma, mutta koska mallinnuksemme on yksinkertaistus todellisesta maailmasta, jatkaa virtaus jokaisesta pikselistä vain yhteen suuntaan. Tästä johtuen leveämmät alueet pilkkoutuvat yhden pikselin levyisiksi janoiksi.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/weird_basin_1.PNG %}" width="46%" border="1">
  &nbsp;
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/weird_basin_2.PNG %}" width="49%" border="1">
</p>

> Valuma-alueiden outouksia

Toisena hydrologisena mallinnuksena selvitettiin alueen potentiaaliset uomat. Ensin luotiin rasteri, jossa laskettiin kullekkin pikselille, kuinka monesta muusta pikselistä siihen valuisi vettä. Koska koko korkeusrasterissa oli 9 miljoonaa pikseliä, syntyi uuteen rasteriin kaikkia arvoja nollan ja useamman miljoonan väliltä. Tästä rasterista tehtiin _Reclassify_-työkalulla muutama eri versio, joissa normalisoitiin kaikki arvot yhdeksi, jos ne ylittivät tietyn rajan ja muut arvot asetettiin nollaan. Näin saatiin kolmannella _Raster to..._ -työkalulla muunnettua pikselijonot vektoreiksi, jotka kuvastavat potentiaalisia uomia.

Tein normalisoinnin raja-arvoilla 100 000, 10 000 ja 1 000. Näistä korkein raja tuotti aineiston vain kaikista suurimmista uomista ja osa maastokartalla näkyvistä todellisista uomista jäi uupumaan. Keskimmäinen raja tuotti lähes kaikki maastokartalla näkyvät uomat ja loi jopa muutamia, joita ei maastokartan mukaan ole olemassa. Pienin raja tuotti jälleen valuma-alueista tuttuja yhden pikselin kokoisia outouksia.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/weird_1k.PNG %}" border="1">

> Raja-arvon 1 000 tuottamia outouksia

Näiden havaintojen perusteella päätin hyödyntää kahta ensimmäistä aineistoa lopullisessa visualisoinnissani. Lisäksi halusin kokeilla maastokartan hyödyntämistä _Hillshade_-tason tapaan _blend_-toiminnolla, jotta sain paikan nimiä myös näkyviin kartalle. En kuitenkaan ollut aivan vakuuttunut lopputuloksesta, joten tein karttatulosteesta myös toisen version. Lukija tuomitkoon kumpi on parempi.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/KevoUomatMaasto.png %}" border="1">

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk2/KevoUomatValuma.png %}" border="1">

---

**Viittaukset:**

- Holopainen, M., Tokola, T., Vastaranta, M., Heikkilä, J., Huitu, H., Laamanen, R., Alho, P. (2015). Geoinformatiikka luonnonvarojen hallinnassa (7. julkaisu). Helsingin yliopiston metsätieteiden laitos
