---
title: "1.7 Omatoimista aherrusta"
date: 2023-03-07
layout: post
---

Viimeisellä kurssikerralla jokainen sai valita oman aiheen ja työskentely oli hyvin itsenäistä. Omaksi aiheekseni valitsin maastokartan luomisen maanmittauslaitoksen maastotietokannan avulla.
<!--excerpt_end-->

### Maastokarttaa rakentamassa

Kurssimateriaalissa oli vinkki [Gispo](https://www.gispo.fi/)n toteuttamasta [QGIS-lisäosasta](https://www.gispo.fi/blogi/maastotietokanta-natisti-qgisiin/), jolla voisi automatisoida Maastotietokannan käsittelyä. Päätin tutustua lisäosaan, sillä tarkoituksenani on juurikin täydentää ohjelmisto-osaamistani geoinformatiikan opinnoilla.Lisäosan [GitHub-sivulla](https://github.com/GispoCoding/NLSgpkgloader) oli selkeät asennusohjeet ja kaikki onnistui ilman ongelmia.

En ollut vielä valinnut miltä alueelta karttani teen, mutta päätin kurssikertaa edeltävänä iltana sen enempää miettimättä ladata uudenmaan, kanta-hämeen ja päijät-hämeen kuntien aineistot. Aineiston määrä oli kuitenkin niin valtava, että joudun jättämään lisäosan prosessoimaan yön yli. Aamulla lisäsin kartan taakse rinnevarjostuksen [Paitulin rajapinnan](https://paituli.csc.fi/webservices.html) kautta haetulla korkeusdatalla ja sain napattua seuraavan näyttökuvan ennen kampukselle lähtemistä.

<img src="{{ site.base_url }}{% link /assets/imgs/uusimaa.png %}" width="100%">

> Maastotietokanta-aineistoja keskiuudeltamaalta ja pääkaupunkiseudulta

GIS-luokassa asensin koneelle jälleen Gispon-lisäosan, mutta tällä kertaa latasin vain pääkaupunkiseudun aineistot. Aineistojen lataamisessa ja prosessoinnissa meni pienemmästä koosta huolimatta lähes tunti. Lisäosan tuottama jälki on kuitenkin mielestäni sen verran laadukas, että odottelu on sen arvoista.

Toteutin aineistolla seuraavan kartan Nuuksion alueelta. Säädin hieman muutamia symboleja ja piilotin muun muassa luonnonsuojelualueet ja kansallispuistot. Lisäksi latasin [Paitulin latauspalvelusta](https://paituli.csc.fi/download.html) rajapinnan kautta tarjottavaa korkeusdataa tarkemmat tiedostot alueesta ja toteutin niillä rinnevarjostuksen.

<img src="{{ site.base_url }}{% link /assets/imgs/nuuksio.png %}" width="100%">

> Yksinkertainen maastokartta Nuuksion alueelta

Huomasin kuitenkin myöhemmin, että metsätyyppien symbolit olivat jääneet lopullisessa visualisoinnissa aivan liian ohuiksi, eikä niitä meinaa kartasta edes erottaa. Päätinkin siis toteuttaa kartan vielä uudestaan kotona. Olihan minulla aineistotkin jo, tarkempaa korkeusdataa lukuunottamatta, valmiiksi ladattuna.

Uuden kartan päätin viimeistellä hieman huolellisemmin. Toteutin tällä kertaa myös kartan legendan, joka sisältää kaikki alueella näkyvät symbolit. Legendan toteuttaminen oli kaikista työläin vaihe, sillä koko aineisto sisältää niin monta tasoa ja symbolia. Onneksi legendatyökalussa pystyy valitsemaan vain printissä näkyvät symbolit, mikä helpotti hieman. Työtä kuitenkin riitti symbolien ulkonäön säätämisessä ja niemämisessä, mikä vaati myös maastotietokannan dokumenttien tutkiskelua.

<img src="{{ site.base_url }}{% link /assets/imgs/nuuksio_selitteet.png %}" width="100%">

> Huolellisesti viimeistelty maastokartta Nuuksion alueelta

Olen lopputuloksestä ylpeä ja tyytyväinen siitä, että päätin toteuttaa kartan uudelleen.

#### Näkymäanalyysi

Ohjeissa rohkaistiin vielä tekemään osana työtä näkymäanalyysi (_viewshed analysis_). Pienellä googlailulla selvisi, että kyseessä on tekniikka jolla selvitetään mitkä alueet kartalla näkyvät teoriassa tietystä pisteestä katsottuna. Näkymäanalyysi tehdään korkeusdatan perusteella ja QGIS tarjosi jälleen tehtävään helppokäyttöisen työkalun.

<img src="{{ site.base_url }}{% link /assets/imgs/viewshed.png %}" width="100%">

> Näkymäanalyysi Nuuksiosta Haukkalammen saaresta

---

**Lähteet:**
- Gispo Oy. Viitattu 14.3.2023. [https://www.gispo.fi/](https://www.gispo.fi/)
- Jokela, S. 2019. - Maastotietokanta nätisti QGISiin?. Kirjoitus gispo.fi blogissa 26.6.2019. Viitattu 14.3.2023 [https://www.gispo.fi/blogi/maastotietokanta-natisti-qgisiin/](https://www.gispo.fi/blogi/maastotietokanta-natisti-qgisiin/)
- Gispo, Ltd. _NLS GeoPackage Downloader QGIS plugin_ Viitattu 14.3.2023 [https://github.com/GispoCoding/NLSgpkgloader](https://github.com/GispoCoding/NLSgpkgloader)
- Opetus- ja kulttuuriministeriö. _Paitulin rajapintapalvelut_ Viitattu 14.3.2023. [https://paituli.csc.fi/webservices.html](https://paituli.csc.fi/webservices.html)
- Opetus- ja kulttuuriministeriö. _Paitulin latauspalvelu_ [https://paituli.csc.fi/download.html](https://paituli.csc.fi/download.html)