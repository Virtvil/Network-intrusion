# h4 - NFC ja RFID
- Kurssi: Verkkoon tunkeutuminen ja tiedustelu (Karvinen 2026)
- Opettaja: Tero Karvinen & Lari Iso-Anttila
- Raportin kirjoittaja: Vili Virtanen
## a) Tarkastele käytössäsi olevia RFID tuotteita, mieti miten hyvin olet suojautunut RFID urkinnalta?
Yleisimpiä käytössäni olevia RFID tuotteita ovat:

- Maksukortti, sekä erilaiset kanta-asiakaskortit
- Kulkukortti töihin
- Passi ja henkilökortti

Suojautumisen kannalta pyrin pitämään kulkukorttiani kotona aina kun en sitä tarvitse, ja pitämään tätä usein taskussani sen sijaan, että roikottaisin sitä muiden nähtävillä kaulani ympärillä. Lompakkoni kanssa pyrin myös usein pitämään sen käden ulottuvilla, mutta tämä ei tietenkään suojaa mahdollisilta skannauksilta huomioni ollessa muualla. Vaikka pidänkin henkilökorttiani lompakossa, on passini aina kotona ellen tätä erikseen tarvitse. Puhelintani suojaan pitämällä NFC ominaisuudet kokonaan pois päältä.

Korttieni kanssa voisin suojautua urkinnalta huomattavasti paremmin, hankkimalla esimerkiksi lompakon joka olisi rfid suojattu.
## b) Tutustu APDU komentojen rakenteeseen (voit käyttää tekoälyä tutustumiseen)
Tehtävää varten kysyin ChatGPT-6 mallilta seuraavan kysymyksen: _"Voitko kertoa minulle APDU:sta ja APDU komentojen rakenteesta?"_

APDU on keskeinen käsite älykorttien, SIM-korttien, maksukorttien, NFC-teknologian ja erilaisten turvamoduulien kanssa kommunikoitaessa.  Tämä kommunikointi koostuu kahdesta pääosasta:

- Command APDU (C-APDU): Päätelaitteen lähettämä komento.
- Response APDU (R-APDU): Älykortin lähettämä vastaus.

Rakenteeltaan APDU-komennot ovat seuraavanlaisia:

| CLA - Class Byte  | INS - Instruction Byte | P1 & P2 – Parameter Bytes |
| ------------- | ------------- | ------------- |
| CLA kertoo, minkä tyyppiseen komentoluokkaan APDU-komento kuuluu. | INS määrittelee suoritettavan toiminnon eli mitä kortilta pyydetään tekemään | P1 ja P2 ovat komentokohtaisia parametreja, joiden tehtävä on tarkentaa miten annettu komento suoritetaan. |
| Content Cell  | Content Cell  | Content Cell  |

Se voi määrittää esimerkiksi:
- Komentojen luokan.
- Käytetäänkö loogista kanavaa.
- Onko komento osa turvallista viestintää (Secure Messaging).
- Onko kyseessä tietty protokollakohtainen komentotyyppi.


Esimerkiksi SELECT-komennossa ne voivat määrittää:
- Millä tavalla tiedosto tai sovellus valitaan.
- Minkä tyyppistä tunnistetta käytetään valintaan. 

## c) Tutki ja kerro minkä mielenkiintoisen RFID hakkerointi uutisen löysit. 
[Linnaan ei pääse enää vanhalla kulkukortilla](https://www.visiirilehti.fi/linnaan-ei-paase-enaa-vanhalla-kulkukortilla)

Artikkeli kertoo kuinka Tampereen yliopistolla ollaan siirrytty hiljattain mobiililaitteella käytettyyn varmistukseen. Osaan yliopiston keskustakampuksen tiloista ei enää pääse ennen elokuuta 2025 myönnetyllä Treyn opiskelijakortilla, vaan opiskelijoiden on ladattava puhelimilleen sovellus.

Perusteena järjestelmän uusimiselle kerrotaan olevan salattuun koodiin perustuvan uuden kulkukorttityypin ja digitaalisen tunnisteen olevan huomattavasti hankalampia jäljentää kuin fyysinen kulkukortti. 

Uudistuksista ja painotuksesta digitaalisen sovelluksen turvallisuuteen huolimatta opiskelijat voivat kuitenkin pyytää kampuksen infotiskeiltä itselleen erillisen Lenel-kulkukortin.

Mielestäni artikkeli oli kiinnostava, varsinkin opittuani kuinka helposti rfid-pohjaiset kortit ovat jäljennettävissä. Siirtyessä älylaitteisiin olisi turvallisuus oletattavasti myös parempaa, mahdollisen salatun liikenteen avulla.

## Lähteet:
Karvinen 2026: Verkkoon tunkeutuminen ja tiedustelu. Luettavissa: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/ Luettu 15.11.2026

Kiviranta 18.3.2026: Linnaan ei pääse enää vanhalla kulkukortilla, Visiiri. Luettavissa: https://www.visiirilehti.fi/linnaan-ei-paase-enaa-vanhalla-kulkukortilla Luettu 15.11.2026
