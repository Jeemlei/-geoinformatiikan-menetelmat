---
title: '2.3 Rasterianalyysejä'
date: 2023-11-20
layout: post
---

Kolmannella viikolla jatkettiin Kevon kanjonin alueen tutkimista erilaisten rasterianalyysien muodossa. Käytössä oli monta aineistoa eri puulajien biomassoista alueella, sekä edellisellä viikolla käytetty korkeusdata ja siitä johdetut potentieaaliset uomat.

<!--excerpt_end-->

## Aineistot

Biomassa-aineistojen yhteydestä löytyi _README_-tiedosto, jossa oli kuvailtu aineistoa ja miten se oli tuotettu. Aineiston tuottamisessa oli hyödynnetty hyödynnetty maastomittauksia yhdessä Sentinel-2 satelliittien monispektri-instrumenteilla (_MSI_[^1]) ja Landsat 8 satelliitin operatiivisella maankuvaajalla (_OLI_[^2]) kerättyjen kuvien kanssa. Kartat toteutettiin pääasiassa vuoden 2019 mittauksilla ja puuttuvaa dataa täydennettiin vuosien 2013, 2015 ja 2017 tuloksilla. Lopputuotoksessa biomassan yksikkönä on _10kg/ha_ ja rasterin spatiaalinen resoluutio on _16m\*16m_.

### Kokonaisbiomassat

Biomassa-aineistot oli jaoteltu puulajien mukaan lehtipuihin, mäntyihin ja kuusiin. Jokaisella puulajilla oli vielä erilliset tiedostot eläville oksille, yli 1cm halkaisijaltaan oleville juurille, kannoille, kuolleille oksille, hukkapuuosalle, lehvästölle ja kuorelliselle runkopuulle. Näiden tiedostojen avulla jokaiselle puulajille laskettiin kokonaisbiomassa _Raster Calculator_ -työkalulla. Laskun yhteydessä biomassa-arvot muunnettiin muotoon _t/ha_.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk3/bm.gif %}" border="1">

> Eri puutyyppien biomassa Kevon kanjonin alueella

Lataa yksittäiset kartat: <a href="{{ site.base_url }}{% link /assets/imgs/GIS2/wk3/bm_lp.png %}" download>Lehtipuut</a> | <a href="{{ site.base_url }}{% link /assets/imgs/GIS2/wk3/bm_ma.png %}" download>Männyt</a> | <a href="{{ site.base_url }}{% link /assets/imgs/GIS2/wk3/bm_ku.png %}" download>Kuuset</a>

Biomassakartoista voi huomata, että lehtipuut viihtyvät paremmin valoisilla rinteillä, jotka osoittava kohti etelää, kun taas havupuita on enemmän pohjoiseen osoittavilla varjoisemmilla rinteillä. Kuvista on selvää, että lehtipuut menestyvät laajimmalla alueella ja näin todennäköisesti biomassaa on myös eniten, mutta männyillä on enemmän biomassaa niiden kaikista vehreimmillä alueilla. Kuusi näyttää pärjäävän heikoiten ja tiiviimpiä rykelmiä löytyykin vain aivan kanjonin pohjalla virtaavan uoman tuntumasta. Todennäköisesti muut alueet ovatkin liian karuja kosteammasta maaperästä nauttivalle kuuselle.

### Uomien etäisyysvyöhykkeet

Seuraavassa työvaiheessa hyödynnettiin edellisen viikon suurimpia potentiaalisia uomia. Ensin jokaiselle pikselille laskettiin etäisyysarvo lähimpään uomaan _Euclidean distance_ -työkalulla.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk3/EuclideanDist.PNG %}" border="1">

> Etäisyysarvot suurista potentiaalisista uomista

Syntyneestä aineistosta saatiin helposti laskettua parin sadan metrin etäisyys vyöhykkeet edelliseltä viikolta tutulla _Reclassify_-työkalulla.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk3/EuclideanDistReclass.PNG %}" border="1">

> Etäisyys vyöhykkeet suurten potentiaalisten uomien ympärillä

Viimeiseksi hyödynnettiin aiemmin luotuja kokonaisbiomassoja etäisyysvyöhykkeiden kanssa ja tuotettiin _Zonal statistics as Table_ -työkalulla taulukot, joissa on kirjattuna biomassa-aineistojen tilastollisia tunnuslukuja eri etäisyysvyöhykkeillä.

#### Biomassa lehtipuut

| Etäisyys uomasta (m) | min (t/ha) | max (t/ha) | Keskiarvo (t/ha) | Keskihajonta (t/ha) | Summa (t)    |
| -------------------- | ---------- | ---------- | ---------------- | ------------------- | ------------ |
| 0 - 200              | 0          | 65,58      | 4,14             | 6,98                | 190 617,76   |
| 200 - 400            | 0          | 39,49      | 1,22             | 3,95                | 46 587,51    |
| 400 - 600            | 0          | 38,73      | 0,81             | 3,23                | 21 988,00    |
| 600 - 800            | 0          | 39,26      | 0,86             | 3,29                | 14 267,28    |
| 800 - 1000           | 0          | 32,23      | 0,56             | 2,17                | 4 501,54     |
| 1000 - 1300          | 0          | 13,49      | 0,31             | 1,17                | 1 036,89     |
|                      |            |            |                  |                     | = 278 998,98 |

#### Biomassa männyt

| Etäisyys uomasta (m) | min (t/ha) | max (t/ha) | Keskiarvo (t/ha) | Keskihajonta (t/ha) | Summa (t)    |
| -------------------- | ---------- | ---------- | ---------------- | ------------------- | ------------ |
| 0 - 200              | 0          | 74,32      | 4,88             | 11,82               | 224 963,07   |
| 200 - 400            | 0          | 73,72      | 0,60             | 4,37                | 22 785,87    |
| 400 - 600            | 0          | 80,64      | 0,33             | 3,16                | 8 910,47     |
| 600 - 800            | 0          | 67,73      | 0,32             | 3,09                | 5 349,98     |
| 800 - 1000           | 0          | 72,84      | 0,58             | 4,49                | 4 601,29     |
| 1000 - 1300          | 0          | 65,51      | 0,40             | 3,66                | 1 310,35     |
|                      |            |            |                  |                     | = 267 921,03 |

#### Biomassa kuuset

| Etäisyys uomasta (m) | min (t/ha) | max (t/ha) | Keskiarvo (t/ha) | Keskihajonta (t/ha) | Summa (t)   |
| -------------------- | ---------- | ---------- | ---------------- | ------------------- | ----------- |
| 0 - 200              | 0          | 35,22      | 0,52             | 1,71                | 24 164,61   |
| 200 - 400            | 0          | 11,53      | 0,02             | 0,33                | 865,34      |
| 400 - 600            | 0          | 7,35       | 0,01             | 0,26                | 402,24      |
| 600 - 800            | 0          | 6,16       | 0,02             | 0,29                | 303,79      |
| 800 - 1000           | 0          | 6,44       | 0,04             | 0,40                | 294,60      |
| 1000 - 1300          | 0          | 8,07       | 0,04             | 0,43                | 135,36      |
|                      |            |            |                  |                     | = 26 165,94 |

Taulukot vahvistavat jo kartoista tehdyt havainnot: kuusten kokonaisbiomassa on huomattavasti pienempi kuin lehtipuilla sekä männyillä. Ero on suurin piirtein kymmenkertainen. Lisäksi tiheimmät puustokeskittymät löytyvät selvästi uomien läheisyydestä kaikilla puulajeilla, mikä myös oli havaittavissa kartoista. Taulukkojen avulla voidaan siis todentaa, että karttavisualisoinneissa on onnistuttu keskeisen tiedon välittämisessä.

### Korkeusvyöhykkeet ja latvuspeitto

Viikon toista analyysiä varten oli käytössä latvuspeittävyys aineistot lehtipuista ja kaikista puista yhteensä. _README_-tiedosto tarjosi jälleen vastauksia aineiston varsinaisesta sisällöstä. Latvuspeittävyydellä kuvataan prosentteina kuinka suuren osuuden puuston latvusto peittää koko koealasta. Aineistoa varten oli toteutettu jälleen maastomittauksia, joiden avulla oli voitu arvioida muiden alueiden arvot geneettistä algoritmiä käyttäen[^3].

Koska havupuille ei ollut omaa aineistoa, laskettiin se _Raster Calculator_ -työkalulla, vähentämällä lehtipuurasterin arvot kaikkien puiden yhteisrasterista.

Tämän jälkeen tuotettiin korkeusvyöhykkeet käyttämällä _Reclassify_-työkalua korkeusmalliin, kuten aiemmassa anlyysissä tehtiin etäisyysrasterille.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk3/ZonalDEM.PNG %}" border="1">

> Korkeusvyöhykkeet Kevon kanjonissa

Vyöhykerasteria hyödyntäen saatiin jälleen laskettua tutkittavien aineistojen tunnusluvut taulukkoon.

#### Latvuspeitto lehtipuut

| Korkeus (m) | min (%) | max (%) | Keskiarvo (%) | Mediaani (%) | Keskihajonta (%) |
| ----------- | ------- | ------- | ------------- | ------------ | ---------------- |
| 0 - 200     | 0       | 51      | 15,13         | 13           | 11,42            |
| 200 - 300   | 0       | 49      | 8,08          | 5            | 8,13             |
| 300 - 400   | 0       | 42      | 6,63          | 6            | 5,09             |
| 400 - 500   | 0       | 20      | 7,50          | 8            | 4,35             |

#### Latvuspeitto havupuut

| Korkeus (m) | min (%) | max (%) | Keskiarvo (%) | Mediaani (%) | Keskihajonta (%) |
| ----------- | ------- | ------- | ------------- | ------------ | ---------------- |
| 0 - 200     | −1      | 50      | 8,02          | 3            | 9,68             |
| 200 - 300   | −1      | 46      | 4,75          | 2            | 6,24             |
| 300 - 400   | −1      | 47      | 5,40          | 4            | 4,31             |
| 400 - 500   | 0       | 20      | 7,14          | 7            | 4,28             |

Havupuutaulukosta huomataan, että osa arvoista on miinusmerkkisiä, tosin vain yhden prosentin verran. Tämä johtuu todennäköisesti siitä, että alkuperäiset aineistot on tuotettu vain yhden prosentin tarkkuudella. Kun lehtipuiden latvuspeitto vähennettiin kaikkien puiden yhteispeitosta, osui joissakin kohdissa aineistoja kohdilleen pikselit, joiden arvot on pyöristetty eri suuntiin.

Harjoituksen päätteeksi tulokset vielä visualisoitiin kartoiksi.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk3/latvus_lehtip.png %}" border="1">

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk3/latvus_havup.png %}" border="1">

---

[^1]: MultiSpectral Instrument [https://sentinel.esa.int/web/sentinel/missions/sentinel-2/instrument-payload](https://sentinel.esa.int/web/sentinel/missions/sentinel-2/instrument-payload)
[^2]: Operational Land Imager [https://earth.esa.int/eogateway/instruments/oli-landsat-8-](https://earth.esa.int/eogateway/instruments/oli-landsat-8-)
[^3]: Tomppo, E. & Halme, M. 2004. Using coarse scale forest variables as ancillary information and weighting of variables in k-NN estimation: a genetic algorithm approach. Remote Sensing of Environment 92: 1-20.
