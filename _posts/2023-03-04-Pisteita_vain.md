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

Itsenäisessä tehtävässä tutustuttii hasardeihin ja päätin itse keskittyä maanjäristyksiin. Tavoitteena oli tuottaa materiaalia, jota voisi opettajana käyttää tuntiopetuksessa.

Maanjäristysdata oli saatavilla pistemäisessä muodossa ja sisälsi muun muassa järistysten voimakkuuden. Latasinkin itselleni kaikki yli 6 magnitudin maanjäristykset kolmelta eri vuosikymmeneltä.

Yritin ensin toteuttaa visualisointeja edellisen tehtävän tavoin interpoloimalla, mutta en saanut aikaiseksi mitään järkevän näköistä tai informatiivista. Siirryinkin siis seuraavaksi tutustumaan muihin tapoihin visualisoida pistemmäistä dataa ja pienen tutkiskelun jälkeen päädyin kokeilemaan _Heatmap_-työkalua.

_Heatmap_-työkalulla sain selkeästi esille alueet, joilla oli paljon voimakkaita maanjäristyksiä. Asetin vielä taustakartan renderöimään mustavalkoisena sinisen kanavan arvoilla ja sekoitin maanjäristystason siihen _Burn_-asetuksella. Laitoin vielä tulivuorten sijannit pieninä kolmioina, jotta niitä voidaan vertailla voimakkaiden maanjäristysten sijainteihin. Lopputulos on mielestäni kohtuullisen tyylikäs ja vetää huomion hyvin tarkasteltavaan aiheeseen.

Tein saman kartan kolmelta eri vuosikymmeneltä, jotta voidaan tarkastella, onko voimakkaiden maanjäristysten aktiivisuudella havaittavissa vaihtelua. Omaan silmääni vaikuttaa ainakin siltä, että Thaimaan edustalla on ollut 2000-luvulla aktiivisuutta hieman enemmän. Ja tälle ajalle ajoittuu myös Suomessa [uutisoitu](https://yle.fi/a/3-5195147)(Yle, 2004) voimakkaan tsunamin aiheuttanut maanjäristys.

<img src="{{ site.base_url }}{% link /assets/imgs/maanjaristykset_90-luku.png %}" width="100%">

> Yli 6 magnitudin maanjäristykset 1990-luvulla

<img src="{{ site.base_url }}{% link /assets/imgs/maanjaristykset_00-luku.png %}" width="100%">

> Yli 6 magnitudin maanjäristykset 2000-luvulla

<img src="{{ site.base_url }}{% link /assets/imgs/maanjaristykset_10-luku.png %}" width="100%">

> Yli 6 magnitudin maanjäristykset 2010-luvulla

En tiedä ovatko luomani kartat erityisen hyödyllisiä opetuskäyttöön. Niitä tehdessä tuli kuitenkin opittua uusia asioita QGISin käytöstä ja toistot vahvistivat jo hyvää työskelntelyrutiinia.

---

**Lähteet:**
- Nuutinen, J. 2023. - Ulkoilua ja maanjäristyksiä. Kirjoitus GEOINFORMATIIKAN MENETELMÄT I -blogissa 27.2.2023. Viitattu 11.3.2023. [https://blogs.helsinki.fi/joznuuti/2023/02/27/ulkoilua-ja-maanjaristyksia/](https://blogs.helsinki.fi/joznuuti/2023/02/27/ulkoilua-ja-maanjaristyksia/).
- Yle. 2004. _Suomalaisturisteja loukkaantunut Aasian järistyksessä_. YLE24 26.12.2004. Viitattu 11.3.2023. [https://yle.fi/a/3-5195147](https://yle.fi/a/3-5195147)