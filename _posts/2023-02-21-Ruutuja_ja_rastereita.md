---
title: "Ruutuja ja rastereita"
date: 2023-02-21
layout: post
---

Viikon aiheina olivat ruutumuotoisen datan luominen vektoriaineiston pohjalta ja valmiiden rasteriaineistojen käsittely. Aiheet poikkesivat hieman aiemmilta kurssikerroilta, joissa oli pyöritty lähinnä vain vektorien ympärillä.
<!--excerpt_end-->

### Pääkaupunkiseudun rakennukset

Ensimmäisessä tehtävässä oli tarkoituksena luoda ruudukko pääkaupunkiseudun alueelle, johon kerättiin dataa alueen väestöstä. Käytettävissä oli pisteaineisto pääkaupunkiseudun rakennuksista.

Tehtävässä pääsi hyödyntämään edellisellä kurssikerralla käytettyä työkalua, jolla vertailtiin pisteaineiston ominaisuuksien sijaintia toisen aineiston monikulmioiden sijaintiin. Tällä kertaa kuitenkin yksittäisten ominaisuuksien lukumäärien laskemisen sijaan laskettiinkin pisteaineiston attribuuttitaulun arvoja, kuten asukaslukuja, yhteen ja liitettiin niitä aiemmin luotuun ruudukkoon.

Päätin toteuttaa visualisoinnin sekä 250m<sup>2</sup> että 500m<sup>2</sup> tarkkuudella ja tarkastella alueiden rakennusten keskimääräistä asukkaiden lukumäärää.

<img src="{{ site.base_url }}{% link /assets/imgs/Pks_vaki_500x500.png %}" width="100%">

> 500m x 500m ruuduissa olevien asuinrakennusten keskimääräinen asukkaiden lukumäärä

Asetin väri asteikon vihreän päädyn erottelemaan selkeästi alueet, joilla on paljon muutaman ihmisen omakotitaloja. Asteikon toinen pää sisältää taas karkeammin alueet, joiden rakennuksissa asuu keskimäärin kymmeniä tai satoja asukkaita. Tämä jaottelu tuo selkeästi 500m<sup>2</sup> tarkkuudella esille kerrostalorikkaat asutuskeskittymät, kuten Espoon keskuksen ja Leppävaaran, mutta ei häivytä harvemmin asutettujen alueiden eroja, joissa voi olla paljon omakotitaloja tai pienempiä kerrostaloja.

<img src="{{ site.base_url }}{% link /assets/imgs/Pks_vaki_250x250.png %}" width="100%">

> 250m x 250m ruuduissa olevien asuinrakennusten keskimääräinen asukkaiden lukumäärä

250m<sup>2</sup> tarkkuudella yksittäiset rakennukset alkavat vaikuttaa enemmän ja kartasta tulee ainakin omasta mielestäni hieman vaikeampi tulkita. Kartan sekavampi vaikutelma tulee osittain ehkä myös siitä, että ruudukko pirstoutuu enemmän, sillä rakennettujen alueiden välisi 250m<sup>2</sup> alueita on huomattavasti enemmän kuin 500m<sup>2</sup> alueita.

#### Onko ruututeemakartalla hyväksyttävää esittää absoluuttisia arvoja?

Kurssin aiemmissa tehtävissä on ollut tarvetta suhteuttaa esitettyjä arvoja aina johonkin toiseen alueen arvoon. Tämä on johtunut siitä, että tarkastellut alueet ovat olleet paikoin hyvinkin eri kokoisia tai alueiden väkiluku on voinut vaihdella huomattavasti. Tällöin käsitys tarkasteltavien asioiden tai ilmiöiden merkittävyydestä olisi voinut vääristyä ilman suhteuttamista.

Ruututeemakartalla alueet on valmiiksi jaettu standardikokoisiin alueisiin, jolloin luvut suhteutuvat automaattisesti ainakin pinta-alaan. Tämä tarkoittaa, että ainakin tietyissä tapauksissa absoluuttisten arvojen esittäminen on täysin hyväksyttävää.

Tyyne Turusen blogista löytyy hyvä esimerkki alueen väkiluvun esittämisestä ruudussa absoluuttisena arvona. Tämä luo automaattisesti kartan, josta voi tarkastella väestön tiheyttä erialueilla. Vastaavan kartan luominen maakunnittain vaatisi jokaisen kunnan väestönluvun suhteuttamista kyseisen kunnan pinta-alaan, minkä jälkeen laskettua lukua voisi käyttää visualisoinnissa.

### Korkeusdataa Pornaisita

Toisessa tehtävässä päästiin työskentelemään rasterimuotoisen korkeusdatan kanssa ja tarkasteltavana alueena oli Pornaisten keskusta ja sen lähialueet. Korkeusdata on rasterissa esitetty harmaalla väriskaalalla, missä korkeammat arvot ovat vaaleammalla ja matalammat tummalla. Konsepti oli itselleni ennestään tuttu muun muassa pelikehityksestä, mikä teki aineiston kanssa työskentelystä intuitiivista.

Alueen laajuudeen takia rasteri oli neljässä osassa. QGISin merge työkalulla rasterien ja väriskaalan yhdistäminen onnistui helposti. Yhdistetystä rasterista saatiin automaattisesti luotua korkeuskäyrät sekä rinnevarjostus, joka sulautettiin pohjakarttaan pienen kolmiulotteisuusilluusion luomiseksi.

<img src="{{ site.base_url }}{% link /assets/imgs/Pornainen.png %}" width="100%">

> Korkeusdatasta luodut korkeuskäyrät ja rinnevarjostus Pornaisten kartalla

Vertaillessani luomiani korkeuskäyriä Maanmittauslaitoksen peruskarttalehden korkeuskäyriin huomaan, että ainakin omassa visualisoinnissani olisi hieman parannettavaa, sillä korkeuskäyriä on niiden kapeuden takia hieman hankala nähdä pienemmältä näytöltä.

Alla olevista kuvista voi huomata myös muita eroja. Automaattisesti luoduissa korkeuskäyrissä löytyy outoja alueita, jossa korkeus vaihtelee edestakaisin juuri korkeuskäyrän korkeuden tuntumassa. Esimerkkikuvassa tälläinen alue löytyy Mätikistö-tekstin luota.

<p float="left">
    <img src="{{ site.base_url }}{% link /assets/imgs/Korkeuskayrat.png %}" width="49%" border="1">
    <img src="{{ site.base_url }}{% link /assets/imgs/peruskartta_pornainen.png %}" width="49%" border="1">
</p>

> Automaattisesti luotujen korkeuskäyrien (vas.) outouksia Pornaisten keskustan tuntumassa verrattuna Maanmittauslaitoksen peruskarttalehden korkeuskäyriin.

Koska alue on pellolla, voidaan olettaa että korkeusvaihtelu on todennäköisesti korkeintaan kymmeniä senttejä, mutta se aiheuttaa alueelle laikukkaat ja sotkuiset korkeuskäyrät. Maanmittauslaitoksen kartassa kyseisessä kohdassa ei ole korkeuskäyriä. Muidenkin alueiden korkeuskäyrät ovat huomattavasti siistimpiä ja niistä on jätetty pois turhat yksityiskohdat.

---

**Lähteet:**
- Turunen, T. 2023. - 4. harjoituskerta 8.2.2023. Kirjoitus TTYYNE'S BLOG -blogissa 8.2.2023. Viitattu 5.3.2023. [https://blogs.helsinki.fi/ttyyne/2023/02/08/4-harjoituskerta-8-2-2023/](https://blogs.helsinki.fi/ttyyne/2023/02/08/4-harjoituskerta-8-2-2023/).