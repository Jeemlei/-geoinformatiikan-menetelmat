---
title: '2.1 Toinen alku ja ArcGIS'
date: 2023-11-08
layout: post
---

Pientä alkujähmeyttä oli heti havaittavissa omassa tekemisessä, kun olin saanut *ArcGIS*in ensimmäistä kertaa auki.
Vaikka olen jo *QGIS*in käytöstä kartuttanut jonkin verran kokemusta, ei *ArcGIS*in käyttö lähtenyt yhtä sujuvasti käyntiin kuin olin olettanut. <!--excerpt_end--> Varmasti osittain tästä johtuen ensivaikutelma *ArcGIS*sistä oli hieman kömpelö ja epäintuitiivinen kilpailijaansa verratuna. Sanottuani asiasta ääneen, ajatukseni saivat myös vastakaikua muutamalta kurssitoveriltani.
Alkukankeudesta huolimatta ohjelmalla tuotettu lopputulos vaikuttaa selvästi laadukasta, kunhan vain jaksaa paneutua prosessiin, eikä hermostu ja luovuta ensimmäisen vastoinkäymisen edessä.

## Maankäyttöä tutkimassa

Ensimmäisen viikon aiheena olivat overlay- eli päällekkäisyys- tai leikkausanalyysit ja näistä erityisesti _Clip_ ja _Intersect_. Ensisilmäyksellä työkalut vaikuttavat hyvin samanlaisilta ja nopea vilkaisu niiden tuottamaan lopputulokseen ei paljasta juurikaan eroja. Eron huomaakin oikeastaan vasta tarkasteltaessa operaatioden tuottamien tasojen atribuuttitauluja.

### Clip

<table>
  <tbody>
    <tr>
      <td> 
        <i>Clip</i> eli leikkaus ottaa attribuutit ja geometrian kohdetasosta (<i>Input Features</i>) ja poistaa niistä kaiken leikkaustason (<i>Clip Features</i>) geometrioiden ulkopuolelle jäävän. Kohdetason geometriat voivat olla pisteitä, viivoja tai alueita, mutta leikkaustaso sisältää aina alueita. (Holopainen et al., 2015, s. 60)
      </td>
    </tr>
  </tbody>
</table>

Ensimmäisessä tehtävässä käytössä olivat Vihdintien ja Lahdenväylän pätkiä edustavat viivageometriat sekä aineisto Helsingin kantakaupungin pohjoispuolella olevien alueiden maankäytöstä.

Otin omaan visualisointiini vahvasti mallia tehtäväohjeiden esimerkkikartasta ja halusin myös lisätä siinä olleen indeksikartan omaan tulosteeseeni. Tämä aiheutti kuitenkin ensimmäisiä kunnon haasteita, sillä toisen kartan lisääminen lisäsi tekijänoikeustiedot tuplana automaattisesti luotuun *Service Layer*iin.
Pitkän Googlailun ja monien muokkausyritysten jälkeen päädyin vain säätämään _Service Layer_ -ikkunan sopivan kokoiseksi, jotta puolet tekstistä leikkautui pois. Ei ehkä elegantein, mutta toimiva, ratkaisu.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk1/vk1osa1.png %}" width="100%">

> Ensimmäisen tehtävän aineistot

Visualisoinnin jälkeen oli aika pureutua itse analyysiin, jonka tarkoituksena oli tarkastella maankäyttöä Vihdintien ja Lahdenväylän lähistöllä.
Ensin luotiin tie-geometrian ympärille muutaman sadan metrin säteellä bufferi. Tämän jälkeen tehtiin leikaus maankäyttöaineistoon käyttäen luotua bufferia leikkaustasona.

Lopputuloksena syntyneelle tasolle _ArcGIS_ laski automaattisesti pinta-alan neliömetreissä, josta laskettiin _Add Geometry Attributes_ -työkalulla hehtaarit. Tämän jälkeen tason atribuuttitaulu tallennettiin _csv_-tiedostona, joista sai helposti luotua alla olevat piirakkadiagrammit excelin avulla.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk1/Vihdintie_Chart.PNG %}" width="100%">

> Maankäyttö Vihdintien lähistöllä

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk1/Lahdenvayla_Chart.PNG %}" width="100%">

> Maankäyttö Lahdenväylän lähistöllä

Suurimmat erot alueiden maankäytössä voi huomata avokallioissa ja muussa paljaassa maassa sekä matalassa kasvillisuudessa ja vesistöissä. Karttaa tarkastelemalla voi päätellä että Vantaanjoen ympäristö Lahdenväylän kupeessa on ainakin yksi syy tähän eroon. Lisäksi huomioitavaa on Lahdenväylän alueella puoli hehtaaria peltoa, joka vastaa kuitenkin vain alle 1% kokonaisuudesta, eikä siis edes näy piirakkadiagrammissa.

### Intersect

<table>
  <tbody>
    <tr>
      <td> 
        <i>Intersect</i> eli kaksoisleikkaus ei käytä erillistä leikkaustasoa, toisin kuin <i>Clip</i>, vaan sen sijaan yhdistää useamman kohdetason atribuutit ja geometriat näiden yhteisesti peittämiltä alueilta. (Holopainen et al., 2015, s. 60)
      </td>
    </tr>
  </tbody>
</table>

Toisessa tehtävässä jatkettiin maankäyttöaineiston tutkimista ja otettiin avuksi Helsingin kaupunginosajakoa kuvaava geometria. Kaupunginosista valittiin Käpylä, Kumpula sekä Toukola ja luotiin niistä uusi taso.

Tehtävän tarkoituksena oli selvittää kunkin valitun kaupunginosien luonnon ja rakennetun alan suhde toisiinsa. _Intersect_ sopi täydellisesti tähän tehtävään, sillä sen lopputuloksessa saatiin yhdistettyä maanpeite-tieto toisesta tasosta ja kaupunginosa-tieto toisesta tasosta.

Koska maankäyttöaineistossa ei valmiiksi ollut erittelyä luonnosta ja rakennetusta alueesta, tehtiin jaottelu _Calculate Field_ -työkalulla alla olevaa python luokkaa hyödyntäen.

```python
def Reclass(luokka):
  if luokka == 'Vesistöt' or luokka == 'Matala kasvillisuus' or luokka == 'Avokalliot' or luokka == 'Puusto':
    return 'luonto'
  else:
    return 'rakennettu'
```

Tämän jälkeen aineistosta oli luonteva tehdä tuloste uusien arvojen pohjalta.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk1/vk1osa2.png %}" width="100%">

> _Intersect_-harjoituksen karttatuloste

Viimeisenä vaiheena oli vielä atribuuttitaulun hyödyntäminen diagrammin muodostamisessa, kuten ensimmäisessä tehtävässä. Lopputuloksessa ehkä hieman hämää Toukolan pienin rakennustiheys, joka johtuu suuresta luonnoksi laskettavasta vesi alueesta. Kartasta on kuitenkin selkeästi nähtävissä, että Toukolan maa-alueet ovat näiden kolmen kaupunginosan tiheimmin rakennettuja.

<img src="{{ site.base_url }}{% link /assets/imgs/GIS2/wk1/Maankaytto_Chart.PNG %}" width="100%">

> Luonno ja rakennetun alueen suhde Kumpulassa, Toukolassa ja Käpylässä [^1]

Vaikka alussa sanoinkin, että *ArcGIS*in käyttö tuntui hieman hankalalta *QGIS*iin verrattuna, liittyivät ongelmat lähinnä esteettisten asioiden, kuten karttatulosteen tai symbologioiden, muokkaamiseen. Itse analysointityökalujen käyttö ja löytäminen oli kohtuulisen helppoa.

---

[^1]: Viimeisestä diagrammista vielä sanottakoon, että viimeistelin tehtävän kotikoneellani, jossa ei ole Microsoftin office ohjelmistoja asennettuna, joten excelin sijaan käytin Googlen sheets palvelua. Tässäkin on todettava, että myös näistä kahdesta kilpailijasta ilmaisella vaihtoedolla oli parempi käyttäjäkokemus.

**Lähteet:**

- Holopainen, M., Tokola, T., Vastaranta, M., Heikkilä, J., Huitu, H., Laamanen, R., Alho, P. (2015). Geoinformatiikka luonnonvarojen hallinnassa (7. julkaisu). Helsingin yliopiston metsätieteiden laitos
