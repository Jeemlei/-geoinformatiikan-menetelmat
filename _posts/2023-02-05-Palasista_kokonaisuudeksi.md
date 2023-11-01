---
title: "1.3 Palasista kokonaisuudeksi"
date: 2023-02-05
layout: post
---

Kolmannella kurssikerralla opettelimme yhdistelemään vektoreita kokonaisuuksiksi ja lisäämään niihin dataa ulkoisista lähteistä. Lisäksi pääsimme soveltamaan tähän mennessä oppimiamme asioita yhden kokonaisuuden luomiseen.
<!--excerpt_end-->

### Afrikka

Ensimmäisessä harjoituksessa oli aineistona erillisistä vektoreista muodostettu Afrikan kartta, muutama tiedosto alueen luonnonvaroista ja konflikteista sekä erillinen CSV-tiedosto maanosan valtioden popuilaatioista.

Olinkin jo aiemmilla viikoilla tutustunut oma-aloitteisesti CSV-tidostojen käsittelyyn, joten tiedon liittäminen olemassa oleviin vektoreihin ei tuottanut ongelmia. Uutena asiana tuli kuitenkin valtioiden vektoripalasten yhdistäminen, jota en olisi itse välttämättä tullut heti ajatelleeksi. Myös erilaisten sijaintiin liittyvien laskutoimitusten tekeminen tutustutti uusiin työkaluihin.

Koska tehtävänannossa ei ohjeistettu tekemään karttatulostetta projektista, päätin keksiä itse mielenkiintoisen visualisoinnin kootun datan pohjalta. Kartassa näkyvät öljykenttien, timanttikaivosten ja konfliktien sijainnit. Lisäksi laskin yhteen öljykenttien ja timanttikaivosten lukumäärän, miinustin niistä valtion kokemien konfliktivuosien lukumäärän ja suhteutin lopullisen luvun valtion väkilukuun. Toisin sanoen valtiot joissa öljykenttiä ja timanttikaivoksia on enemmäin kuin konfliktivuosia näkyvät kartalla vihreän sävyissä ja kun konflikteja on suhteessa enemmän on väriskaala keltaisesta punaiseen.

<img src="{{ site.base_url }}{% link /assets/imgs/Oil&Diamonds_VS_Conflicts.png %}" width="100%">

> Öljykenttien ja timanttikaivosten lukumäärä verrattuna valtion kokemiin konfliktivuosiin suhteutettuna väkilukuun.

Afrikan konfliktialueista omaan mieleeni on voimakkaimmin painunut Libya ja Muammar Gaddafin syrjäyttämisen jälkeinen uutisointi, minkä takia Libyan vihreä väri ja konfliktimerkkien puute hieman ihmetytti. Vastaus tähän kuitenkin selvisi selaillessani muiden blogeja. Tuukka Katajamäki tekee blogissaan hyvän huomion, että aineisto loppuu vuoteen 2008, kun taas Libyan levottomuudet alkoivat vasta 2011.

Tietokannoista löytyy myös tietoa luonnonvarojen löytövuosista, hyödyntämisen aloittamisesta ja kohteiden tuottavuudesta. Näiden avulla voisi visualisoida esimerkiksi niiden vaikutusta konfliktien temporaaliseen tiheyteen tai etäisyyteen löytöpaikoista.

### Suomen valuma-alueet

Toinen harjoitus tehtiin hyvin itsenäisesti ja tuntui että ensimmäistä kertaa pääsi laajemmin soveltamaan useita kurssilla opittuja asioita. Hyödynsin muun muassa edellisessä tehtävässä opittua vektorien yhdistämistä, jotta sain helposti meret eroteltua maa-alueista visualisointia varten. Lisäksi käytin erilaisia laskentatyökaluja ja panostin paljon visualisoinnin yksityiskohtien säätämiseen. Uutena asiana opettelin myös datan visualisointia diagrammeilla.

<img src="{{ site.base_url }}{% link /assets/imgs/tulvaindeksi.png %}" width="100%" border="1">

> Suomen valuma-alueiden järvisyys ja keskiylivirtaaman suhde keskivirtaamaan.

Kartasta on selkeästi havaittavissa, että järvien suhteellinen määrä alueella korreloi käänteisesti tulvariskin kanssa. Vierekkäistenkin alueiden keskiylivirtaamien erot voivat olla hyvin suuret, jos myös alueiden järvisyyksissä on huomattava ero.
Tästä voisi päätellä, että järvet pienentävät tulvariskiä.

---

**Lähteet:**
- Katajamäki, T. 2023. - 3. Kurssikerta. Kirjoitus TUUKAN GIS-BLOGI -blogissa 20.2.2023. Viitattu 21.2.2023. [https://blogs.helsinki.fi/katuukka/2023/02/20/3-kurssikerta/](https://blogs.helsinki.fi/katuukka/2023/02/20/3-kurssikerta/).