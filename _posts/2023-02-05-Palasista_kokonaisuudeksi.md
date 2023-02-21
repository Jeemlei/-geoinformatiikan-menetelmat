---
title: "Palasista kokonaisuudeksi"
date: 2023-02-05
layout: post
---

Kolmannella kurssikerralla opettelimme yhdistelemään vektoreita kokonaisuuksiksi ja lisäämään niihin dataa ulkoisista lähteistä. Lisäksi pääsimme soveltamaan yhden kokonaisuuden luomiseen tähän mennessä oppimiamme asioita.
<!--excerpt_end-->

### Afrikka

Ensimmäisessä harjoituksessa oli aineistona erillisistä vektoreista muodostettu Afrikan kartta, muutama tiedosto alueen luonnonvaroista ja konflikteista sekä erillinen CSV-tiedosto maanosan valtioden popuilaatioista.

Olinkin jo aiemmilla viikoilla tutustunut oma-aloitteisesti CSV-tidostojen käsittelyyn, joten tiedon liittäminen olemassa oleviin vektoreihin ei tuottanut ongelmia. Uutena asiana tuli kuitenkin valtioiden vektoripalasten yhdistäminen, jota en olisi itse välttämättä tullut heti ajatelleeksi. Myös erilaisten sijaintiin liittyvien laskutoimitusten tekeminen tutustutti uusiin työkaluihin.

Koska tehtävänannossa ei ohjeistettu tekemään karttatulostetta projektista, päätin keksiä itse mielenkiintoisen visualisoinnin kootun datan pohjalta. Kartassa näkyvät öljykenttien, timanttikaivosten ja konfliktien sijainnit. Lisäksi laskin yhteen öljykenttien ja timanttikaivosten lukumäärän, miinustin niistä valtion kokemien konfliktivuosien lukumäärän ja suhteutin lopullisen luvun valtion väkilukuun. Toisin sanoen valtiot joissa öljykenttiä ja timanttikaivoksia on enemmäin kuin konfliktivuosia näkyvät kartalla vihreän sävyissä ja kun konflikteja on suhteessa enemmän on väriskaala keltaisesta punaiseen.

<img src="{{ site.base_url }}{% link /assets/imgs/Oil&Diamonds_VS_Conflicts.png %}" width="100%">

> Öljykenttien ja timanttikaivosten lukumäärä verrattuna valtion kokemiin konfliktivuosiin suhteutettuna väkilukuun.

Tietokannoista löytyy myös tietoa luonnonvarojen löytövuosista, hyödyntämisen aloittamisesta ja kohteiden tuottavuudesta. Näiden avulla voisi visualisoida esimerkiksi niiden vaikutusta konfliktien tiheyteen tai etäisyyteen.

### Suomen valuma-alueet

<img src="{{ site.base_url }}{% link /assets/imgs/tulvaindeksi.png %}" width="100%" border="1">

> Suomen valuma-alueiden järvisyys ja keskiylivirtaaman suhde keskivirtaamaan.