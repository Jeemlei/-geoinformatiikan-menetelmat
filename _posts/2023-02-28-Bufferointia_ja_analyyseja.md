---
title: "Bufferointia ja analyysejä"
date: 2023-02-28
layout: post
---

Viidennellä viikolla kerrattiin QGISin piirtotyökalujen käyttöä ja opeteltiin käyttämään analyyseissä hyödyksi kohteiden etäisyyksiä toisistaan. Kamppailin myös ensimmäisten kunnon haasteen kanssa, törmättyäni viimeisessä tehtävässä virheellisiin geometrioihin. Keräsin kasaan hieman vinkkejä muille saman ongelman kanssa painiville.
<!--excerpt_end-->

Tällä kertaa tekeminen keskittyi karttojen luomisen sijaan erilaisten tulosten selvittämiseen opituilla työkaluilla. Suuressa roolissa olivat valintatyökalut ja statistics-näkymä, josta näki helposti koonteja karttatasojen attribuuttitiedoista.

### Pornainen

Ensimmäisenä tarkastelussa oli sama pornaisten alue kuin edelliselläkin viikolla. Tällä kertaa hyödynnettiin kuitenkin vektorimuotoisia peltoja, teitä ja rakennuksia. Etäisyyksiin liittyvissä kysymyksissä hyödynnettiin puskurivyöhykkeitä ominaisuuksien valinnassa.

- Kuinka monta kilometriä tietä on Pornaisten keskustan alueella?
  - 12,98km
- Kuinka monta neliökilometriä peltoa on keskustarajauksen alueella?
  - 5,70km<sup>2</sup>
- Kuinka monta ihmistä asuu 100m etäisyydellä pääteistä?
  - 424
- Kuinka monta prosenttia edellisen kohdan luku on kaikista alueen asukkaista?
  - 20,0%
- Kuinka monta prosenttia alueen taloista sijaitsee alle 500m päässä Pornaisten terveyskeskuksesta?
  - 27,8%
- Kuinka monta prosenttia alueen taloista on yli kilometrin etäisyydellä Pornaisten koulusta?
  - 37,0%

Kun puskurivyöhykkeiden tekemiseen oli tutustuttu yhteisesti, siirryttiin itsenäisiin tehtäviin.

### Lentokentät ja asemat

Lentokenttien ja asemien kanssa hyödynnettiin myös puskurivyöhykkeitä. Lentokenttien vektoritaso oli kuitenkin ensin luotava itse, mikä onnistuikin ongelmitta jo Johdatus geinformatiikkaan -kurssilta opituilla työkaluilla. Tässä vaiheessa kurssia tuntuukin siltä, että QGISin käytössä on muodostunut kohtuullisen vahva rutiini.

#### Malmin lentokenttä:
- Kaikki asukkaat 2 km säteellä kentästä?
  - 58 799
- Kaikki asukkaat 1 km säteellä kentästä?
  - 9 049

#### Helsinki-Vantaan lentokenttä:
- Kaikki asukkaat 2 km säteellä kentästä?
  - 11 680
- Kuinka monta prosenttia edellisen kohdan asukkaista asuu Helsinki-Vantaa lentokentän pahimmalla melualueella (65dB)?
  - 0,2%
- Kuinka monta ihmistä asuu vähintään 55dB melualueella?
  - 11 923
- Kuinka monta ihmistä asuisi vähintään 60dB lentomelualueella Tikkurilassa, mikäli saapuva liikenne käännettäisiin laskeutumaan tästä poikkeuksellisesta suunnasta?
  - 3 503

#### Juna- ja metroasemat:
- Kuinka monta asukasta asuu kartan alueella alle 500m päässä lähimmästä juna- tai metroasemasta?
  - 111 765
- Kuinka monta prosenttia edellisen kohdan ihmisistä oli työikäisiä (15-64v)?
  - 67,0%
- Kuinka monta prosenttia kaikista alueen asukkaista asuu alle 500m päässä asemasta?
  - 21,7%

### Taajamat

Taajamiin liittyvät kysymykset olivat hyvin suoraviivaisia ja vastaukset muodostuivat edellisten tehtävien jälkeen kuin suoraan liukuhihnalta.

- Kuinka monta prosenttia alueen asukkaista asuu taajamissa?
  - 96,1%
- Kuinka monta kouluikäistä asuu taajamien ulkopuolella?
  - 3 727
- Kuinka monta prosenttia edellisen kohdan luku on kaikista kouluikäisistä? 
  - 3,6%

- Kuinka monella alueella ulkomaalaisten osuus on yli...
  - ...10%
    - 66
  - ...20%
    - 22
  - ...30%
    - 14

### Uima-altaita ja saunoja

Viimeinen tehtävä oli hieman monipuolisempi ja soveltavampi. Törmäsin myös ensimmäisiin kunnon onglemiin, jotka kuitenkin ratkesivat kohtuullisen helposti tietojenkäsittelytieteilijän rutinoituneella googlaustaidolla.

Ainakin [Leo Mäklin](https://blogs.helsinki.fi/lmaklin/2023/03/03/harjoitus-5/) ja [Lucas Yoni](https://blogs.helsinki.fi/luberger/2023/02/20/viikko-5-bufferointia-reflektointia/) mainitsevat blogeissaan törmänneensä samaan virheellisiin geometrioihin liittyvään ongelmaan kuin minä. Leo kertoo ratkaisseensa ongelman automaattista _Fix geometries_ -työkalua käyttäen, mutta ei ole varma mistä ongelmassa oli kyse tai mitä työkalu teki. Lucas puolestaan onnistui paikantamaan virheelliset geometriat, mutta ei onnistunut niitä korjaamaan. Ratkaisuna hän päätyi poistamaan geometriat kokonaan.

<div style="border: solid 0.15rem; border-radius: 10px; padding: 0.5rem; margin: 0.1rem; background-color: #eeeeee">
  <p><u><b>Vinkkejä virheellisten geometrioiden löytämiseen ja korjaamiseen:</b></u></p>
  <p>
    Virheellisten geometrioiden löytämiseen voi käyttää <i>Check Validity</i> -työkalua, jonka löytää helposti <i>Processing Toolbox</i> -hakukentästä tai Vektori-valikon geometria-työkaluista.
  </p>
  <p>
    <i>Input Layer</i> -kohtaan valitaan tarkasteltava taso ja muita asetuksia ei pitäisi olla tarvetta muuttaa. Työkalu luo kolme tasoa, joista yksi sisältää virheettömät geometriat, toinen virheelliset ja kolmas virheiden sijainnit pisteinä.
  </p>
  <p float="left">
    <img src="{{ site.base_url }}{% link /assets/imgs/geometry_errors_layers.PNG %}" width="50%" border="1">
    <img src="{{ site.base_url }}{% link /assets/imgs/geometry_errors.PNG %}" width="47%">
  </p>
  <blockquote>Check Validity -työkalun luomat kolme tasoa</blockquote>
  <p>
    Pistetason attribuuttitaulusta löytyy virheen tyyppi, joka itselläni oli <i>Self-intersection</i>, eli geometriat leikkaavat itseään. Tämä on kohtuullisen helppo korjata, koska tiedämme missä virheet sijaitsevat.
  </p>
  <p>
    Ensin valitaan muokattava taso ja asetetaan se muokkaustilaan <i>Toggle Editing</i> -napilla, jossa on keltaisen kynän kuva. Seuraavaksi valitaan <i>Vertex Tool</i> -työkalu, jonka pitäisi sijaita oikealla muutaman napin päässä edellisestä. <i>Vertex Tool</i> -työkalulla voimme liikuttaa polygonien kulmia klikkaamalla ensin kulmaa ja sen jälkeen uutta sijaintia.
  </p>
  <p>
    Kulmien ollessa samassa sijainnissa muiden polygonien kulmien kanssa joudut ehkä muuttamaan väliaikaisesti viereisten polygonien muotoa, että pääset käsiksi onglemalliseen kulmaan.
  </p>
  <p>
    Ongelmana voi myös olla saman polygonin erikulmien päällekkäisyys. Tällöin voi olla järkevää poistaa ylimääräisiä kulmia klikkaamalla kulmaa kerran ja painamalla <i>Delete</i>-näppäintä.
  </p>
  <p>
    Lopuksi poistu muokkaustilasta ja tallenna muutokset.
  </p>
</div>

Kun olin saanut geometriat korjattu sain viimeisteltyä tehtävän nopeasti. Visualisoinnissa oli kuitenkin mahdotonta saada pienillä alueilla näkymään sekä suuri numero että pylväsdiagrammi. Olenkin [Lucas Yonin](https://blogs.helsinki.fi/katuukka/2023/02/25/5-kurssikerta/) kanssa samaa mieltä, "että histogrammien käyttäminen esittämään yhden muuttujan vaihtelua kartalla on vähän huono".

<img src="{{ site.base_url }}{% link /assets/imgs/uima-altaat.png %}" width="100%" border="1">

#### Uima-altaat
- Kuinka monta uima-altaalla varustettua rakennusta löytyy pääkaupunkiseudulta?
  - 855
- Kuinka paljon asuu asukkaita sellaisissa taloissa, joissa on uima-allas?
  - 12 170

Kuinka moni edellisen kohdan taloista on...
- ...omakotitaloja?
  - 345
- ...kerrostaloja?
  - 181
- ...rivitaloja?
  - 113

#### Saunat
- Kuinka monessa talossa on sauna?
  - 2 169
- Kuinka monta prosenttia edellisen kohdan luku on kaikista asutuista taloista pääkaupunkiseudulla?
  - 2,4%

### Missä nyt mennään?

Koen että tällä hetkellä tekninen osaamiseni QGISin käytössä on sillä tasolla, että voisin käyttää ohjelmistoa kohtuullisen vaivatta työelämässä. Tietojenkäsittelytiedetaustani auttaa selvästi teknisten asioiden sisäistämisessä ja vastaan tulevien ongelmien ratkaisussa. Maantieteen aiempien opintojen puute puolestaan heijastuu analysointitaitoihini. Analysointitaidoissani aineistoja ja tuloksia tarkastellessa voisi olla parannettavaa.

---

**Lähteet:**
- Mäklin, L. 2023. - Harjoitus 5. Kirjoitus LMAKLIN’S BLOG -blogissa 3.3.2023. Viitattu 10.3.2023. [https://blogs.helsinki.fi/lmaklin/2023/03/03/harjoitus-5/](https://blogs.helsinki.fi/lmaklin/2023/03/03/harjoitus-5/).
- Yoni, L. 2023. - Viikko 5: Bufferointia & reflektointia. Kirjoitus GIS-AVAUTUMISET -blogissa 20.2.2023. Viitattu 10.3.2023. [https://blogs.helsinki.fi/luberger/2023/02/20/viikko-5-bufferointia-reflektointia/](https://blogs.helsinki.fi/luberger/2023/02/20/viikko-5-bufferointia-reflektointia/).
