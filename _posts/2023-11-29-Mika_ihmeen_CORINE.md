---
title: '2.4 Mikä ihmeen CORINE'
date: 2023-11-29
layout: post
---

Neljännellä viikolla tutustuttiin CORINE-maanpeiteaineistoon ja yksinkertaisiin tietokantaliitoksiin. Lisäksi harjoiteltiin useista aineistoista ja työvaiheista koostuvien kokonaisuuksien automatisointia, tekemällä soveltuvuusanalyysi hyvistä telttapaikoista Kevon kanjonin alueella.

<!--excerpt_end-->

## CORINE

CORINE, eli "Coordination of information on the environment", on EU-alueen kattava inventaario maankäytöstä, joka sisältää 44 eri maankäytön luokkaa.[^1] Aineisto päivitetään kuuden vuoden välein ja harjoituksessa käytössä oli uusin aineisto Suomesta vuodelta 2018.[^2]

Suomen aineisto on tuotettu olemassa oleviin paikkatietoaineistoihin sekä satelliittikuvatulkintaan perustuen ja tuottajana on toiminut Suomen ympäristökeskus (SYKE).[^3] Rasteriaineiston spatiaalinen resoluutio on 20m\*20m ja harjoitusta varten siitä oli leikattu vain Pohjois-Lapin kattava alue.

### Aineiston visualisointi

Tarkasteltavana oli jälleen Kevon kanjonin alue, joten aineistoa leikattiin vielä pienemmäksi käyttämällä ensimmäiseltä viikolta tuttua _Clip_-työkalua.

<p align="center">
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk4/Corine_orig_large.PNG %}" width="49%">
  &nbsp;
  <img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk4/Corine_orig_large_clip.PNG %}" width="48%">
</p>

> Pohjois-Lapin aineisto ja leikattu Kevon kanjonin aineisto

Seuraavaksi rasteriin liitettiin taulukko, jossa oli selitteet maankäyttöluokille. Selitteet oli jaettu neljälle eri tarkkuus tasolle, joista ensimmäisellä luokat oli ryhmitelty viiteen eri ryhmään (rakennetut alueet, maatalousalueet, metsät sekä avoimet kankaat ja kalliomaat, kosteikot ja avoimet suot, vesialueet) ja viimeisellä jokaisella luokalla oli oma selite.

Omassa kartassani käytin tason kaksi tarkkuutta, sillä mielestäni se tarjosi hieman tarkempia tasoja enemmän visuaalista selkeyttä kuitenkaan yleistämättä liikaa. Syvempää pohdiskelua varten tarkemmat luokkamäärittelyt olisivat ehkä olleet parempi valinta, mutta tuottamastani kartasta on kuitenkin hyvin havaittavissa esimerkiksi tiheämmän metsän ja kosteikkojen keskittyminen vesistöjen ympärille. Lisäksi aiemmilta viikoilta tuttu _Hillshade_-aineisto auttaa hieman hahmottamaa, että korkeilla huipuilla maasto on avoimempaa.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk4/Corine_2018.png %}" border="1">

## Soveltuvuusanalyysi

Soveltuvuus analyysissä tarkoituksena oli löytää Kevon kanjonin alueelta telttailuun sopivia sijainteja. Tässä hyödynnettiin viittä eri aineistoa (CORINE-maanpeitedata, korkeusmalli, rinteen suunta -ainesto, uomadata, rinteen jyrkkyys -aineisto) ja tehtävä sisälsi jokaiselle aineistolle useita käsittelyvaiheita. Jotta kokonaisuutta olisi helpompi hahmottaa ja hallinnoida, otettiin käyttöön <i>ArcGIS</i>in _ModelBuilder_.

<i>ModelBuilder</i>illa eri aineistot ja työkalut linkitetään yhteen, niin että kussakin vaiheessa käytetyn työkalun tuotos toimii syötteenä seuraavan vaiheen työkalulle. Toteutuksen jälkeen koko työputken pystyy suorittamaan yhtä nappia painamalla, niin monta kertaa kuin haluaa. Tämä helpottaa erityisesti pienten muutosten ja eri lähtöaineistojen testaamista.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk4/Analysis_Model.PNG %}" border="1">

> Soveltuvuusanalyysin lopullinen malli

### Työvaiheiden erittely

Ensimmäisessä vaiheessa on tarkoituksena luoda jokaisesta aineistosta soveltuvuus maski, jossa arvo 1 kuvaa kriteerin täyttävää solua ja rasterin muut solut sisältävät arvon 0.

Rasteri aineistoille tämä tapahtuu jo erittäin tutuksi tulleella _Reclassify_-työkalulla. Kriteerit eri rasteriaineistoille olivat:

1. Maanpeitteen tulee olla lehti-, seka- tai havumetsä kivennäismaalla, tai lehti- tai sekametsä turvemaalla
2. Alle 260m korkeudessa
3. Rinne suuntautuu välille itä - etelä - länsi
4. Jyrkkyys saa olla korkeintaan 10&deg;

Viimeisenä kriteerinä oli "korkeintaan 200m etäisyydellä uomista". Käytössä ollut uomadata oli toisella viikolla tehty vektori aineisto, joten etäisyys rasteria varten toteutettiin kolmannelta viikolta tutut työvaiheet _Euclidean Distance_- ja _Raster Calculator_-työkaluilla.

Ensimmäisen vaiheen maskit kerrotaan seuraavaksi toisillaan, jolloin syntyy yhdistetty soveltuvuusmaski. Tällöin lopputuloksessa kaikki solut joiden kohdalla edes yhdessa maskissa on arvo 0, saavat myös lopputuloksessa arvon 0. Toisin sanoen lopputuloksena syntyvässä rasterissa arvo 1 kuvaa solua, jossa jokainen kriteeri täyttyy.

Kahdessa viimeisessä työvaiheessa malli vielä poistaa 0-soluilta arvon kokonaan ja luo jäljelle jääneistä 1-soluista polygonit.

Lopputuloksesta huomaa, että maanpeittoaineiston spatiaalinen resoluutio ei ollu ehkä tarpeeksi tarkka, sillä paikoittain soveltuvuuspolygonit leikkaavat uomia. Toisaalta myös kriteerejä olisi voinut muokata, esimerkiksi asettamalla uomien soveltuvuusbufferille ylärajan lisäksi alarajan.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk4/Kevo_Tent.png %}" border="1">

> Soveltuvuusanalyysin tuottamat polygonit

Soveltuvuus analyysi avaa mahdollisuuksia erilaisten aineistojen ja kriteerien hyödyntemiseen monissa eri tarkoituksissa, kuten kurssimateriaalissa ehdotettujen helikopterin laskeutumispaikkojen tunnistamisessa. Muita mahdollisia sovellutus kohteita voisivat olla erilaisten rakennusprojektien sijaintien valinta, tai esimerkiksi Kevon alueella sopivien kulkureittien kartoittaminen.

---

**Viittaukset:**

[^1]: https://www.eea.europa.eu/help/faq/what-is-corine-land-cover
[^2]: https://land.copernicus.eu/en/products/corine-land-cover
[^3]: https://ckan.ymparisto.fi/dataset/corine-maanpeite-2018
