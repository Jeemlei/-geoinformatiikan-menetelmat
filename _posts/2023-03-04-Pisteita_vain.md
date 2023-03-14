---
title: "Pisteitä vain?"
date: 2023-03-04
layout: post
---

Kuudes kurssikerta alkoi pienellä ulkoilulla, jonka aikan tuotimme pistemäistä dataa Kumpulan ympäristöstä. Käytössämme oli [Epicollect5](https://five.epicollect.net/)-kännykkäsovellus, jonka avulla vastasimme eri sijainneissa muutamaan viihtyvyyteen ja turvallisuuteen liittyvään kysymykseen.
<!--excerpt_end-->

### Kumpulan koettu turvallisuus

Kerätystä datasta tehtiin ohjatusti visualisointi, mutta päätin toteuttaa visualisoinnin vielä uudelleen kotona, yhdistämällä kurssin kaikkien ryhmien keräämät aineistot yhteen.

Visualisoinnissa käytettiin hyväksi interpolointia, jossa arvioidaan aineiston pisteiden välisiä arvoja. Näin saadaan koko tutkitun alueen kattava arvojoukko rasterina, vaikka lähtöaineisto ei sisälläkään dataa alueen jokaiselta neliömetriltä.

Interpoloinnilla saatu visualisointi on huomattavasti pisteitä informatiivisempi, mutta ei vastaa kuitenkaan aivan täysin todellisuutta. Visualisoinnista ei suoraan pysty sanomaan miltä alueilta dataa puutuu, joten tarkkoja päätelmiä yksittäisten paikkojen suhteen ei välttämättä kannata tehdä.

Yleisesti omasta visualisoinnistani voisi kuitenkin päätellä ainakin, että turvattomiksi koetut alueet keskittyvät paljon vilkkaiden teiden ja tienylitysten ympärille. Turvallisiksi taas koetaan puistoalueet ja pienempien teiden ympäristö.

<img src="{{ site.base_url }}{% link /assets/imgs/Kumpulan_turvallisuus.png %}" width="100%">

> Kumpulan alueelta kerätystä datasta tuotettu visualisointi

Inspiraatiota visualisointiini sain Jonna Nuutisen blogista. Kaikissa aiemmissa visualisoinneissani olen asettanut legendan, pohjoisnuolen ja mittakaavan aina kartan päälle. Jonnan visualisoinnista kuitenkin tajusin, että kartalle voi varata oman alueen ja asettaa muun informaation sen viereen tai vaikka yläpuolella. Vaikka tämä jälkikäteen vaikuttaa itsestäänselvyydeltä, oli se itselleni todella mullistava oivallus, sillä olin huomaamattani alitajuisesti jumittunut samaan kaavaan.

### Hasardit

<img src="{{ site.base_url }}{% link /assets/imgs/maanjaristykset_90-luku.png %}" width="100%">

<img src="{{ site.base_url }}{% link /assets/imgs/maanjaristykset_00-luku.png %}" width="100%">

<img src="{{ site.base_url }}{% link /assets/imgs/maanjaristykset_10-luku.png %}" width="100%">

---

**Lähteet:**
- Nuutinen, J. 2023. - Ulkoilua ja maanjäristyksiä. Kirjoitus GEOINFORMATIIKAN MENETELMÄT I -blogissa 27.2.2023. Viitattu 11.3.2023. [https://blogs.helsinki.fi/joznuuti/2023/02/27/ulkoilua-ja-maanjaristyksia/](https://blogs.helsinki.fi/joznuuti/2023/02/27/ulkoilua-ja-maanjaristyksia/).