# h3 Aaltoja harjaamassa
- Kurssi: Verkkoon tunkeutuminen ja tiedustelu (Karvinen 2026)
- Opettaja: Tero Karvinen & Lari Iso-Anttila
- Raportin kirjoittaja: Vili Virtanen
## x) Materiaalit
### Hubacek 2019: Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs
- Signaalien kaappausta käyttäen SDR-ohjelmaa.
- Nauhoitettua signaalia pystyy tutkimaan paremmin tämän leikkaamisella ja rajaamisella.
- Tallennettuja signaaleja pystyy avaamaan erilaisten valmiiden modulaatioiden ja _autodetect parameters_ avulla, joka muuttaa formaatin helpommin luettavaksi.
### Cornelius 2022: Decode 433.92 MHz weather station data
- Sääaseman signaalin anyslointia.
- Signaalin kaappaukseen ja tulkintaan Cornelius käytti rtl_433-ohjelmaa.
- Tallentaakseen ja tutkiakseen signaalia tarkemmin hän käytti URH, Universal Radio Hacker ohjelmaa.
## b) rtl_433
Asennusohjeet löytyvät rtl_433 githubista ja asennus onnistuu helposti komennolla:
```
sudo apt install rtl-433
```

<img width="955" height="585" alt="VirtualBox_Kali_08_11_2026_18_17_20" src="https://github.com/user-attachments/assets/3491b71f-5c81-4f8a-adfc-3d893a64f05f" />


Tarkistetaan vielä asentamamme versio komennolla:
```
rtl_433 -V
```

<img width="656" height="71" alt="VirtualBox_Kali_08_11_2026_18_19_40" src="https://github.com/user-attachments/assets/9f0274a3-8561-4a71-ada5-68ff6af6b2b3" />


HUOM! Asennusvaiheessa tulee käyttää ohjelmassa väliviivaa, vaikka ohjelma esiintyykin Kalilla alaviivalla (ero - ja _).

Tässävaiheessa tehtävänanto pyytää kokeilemaan ohjelman ajettavuus, mutta ilman kuuntelulaitetta tämä on hankalaa... Yhdistettyä laitetta voi ajaa kuitenkin simppleillä komennolla:
```
rtl_433
```

<img width="627" height="96" alt="VirtualBox_Kali_08_11_2026_18_29_15" src="https://github.com/user-attachments/assets/c629b24b-cb4a-4c1c-8013-1eee15dbbaa2" />

Voimme kuitenkin komenolla todistaa ohjelman pyörivän.
## c) Automaattinen analyysi
Ladataan seuraavaksi Karvisen [verkkosivulta](https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu) _Converted_433.92M_2000k.cs8_-tiedosto jota lähdemme tutkimaan. Siirryttyämme Downloads-hakemistoon voimme ajaa komentomme:
```
rtl_433 -r Converted_433.92M_2000k.cs8
```

<img width="955" height="806" alt="VirtualBox_Kali_08_11_2026_18_35_44" src="https://github.com/user-attachments/assets/a57b7c98-807e-48ca-bf80-5365606ff3a9" />

Kuvaa analysoimalla näemmä tämän olevan kolmen eri paketin, _KlikAanKlikUit-Switch_, _Proove-Security_ ja _Nexa-Security_ näyttäytyvän useamman kerran. Tulosteessa näkyy jokaisella paketilla oma aikaleimansa ja pakettien väilillä jaetun saman id-numeron. 

Veikkaisin kyseessä olevan jonkinlaisen kameran ja tämän kaukosäätimen, sillä _KlikAanKlikUit-Switch_ tuntuisi viittaavan jonkinlaiseen klikattavaan autosäätimeen ja molemmat _Proove-Securityn_ ja _Nexa-Securityn_ näyttäisivät jakavan nimessään Security-sanan, sekä tiedoissaan _House Code_-osion.
## d) Too compex 16?
Ladataan jälleen tehtävänannossa annettu tiedosto: _Recorded-HackRF-20250411_183354-433_92MHz-2MSps-2MHz.complex16s_ ja kokeillaan lukea tämä edellisestä osiosta tutulla rtl_433 -r komennolla:
```
rtl_433 -r Recorded-HackRF-20250411_183354-433_92MHz-2MSps-2MHz.complex16s
```

<img width="955" height="319" alt="VirtualBox_Kali_08_11_2026_18_48_11" src="https://github.com/user-attachments/assets/abc94dcb-bec1-410f-84de-6ffca61bb482" />

Komentomme toimii ja tiedoston sisätlö vaikuttaa samalta kuin aiemmassa tehtävässä. 
## e) Ultimate. Asenna URH, the Ultimate Radio Hacker
Asennetaan seuraavaksi URH, the Ultimate Radio Hacker. URH GitHub repo tarjoaa meille suoraan ohjeet asennukseen käyttämällä pipx, joten asennetaan se samalla käyttäen seuraavia komentoja:
```
sudo apt-get -y install pipx
pipx install urh
pipx ensurepath
```

<img width="955" height="506" alt="VirtualBox_Kali_08_11_2026_18_59_25" src="https://github.com/user-attachments/assets/b0c8d42d-5e22-4274-96b6-8d4979c67558" />

Ladataan jälleen kerran tehtävänannossa annettu tiedosto, _ 1-on-on-on-HackRF-20250412_113805-433_912MHz-2MSps-2MHz.complex16s_ ja avataan tämä käyttäen URHia. URH aukeaa simppelillä  ```urh``` komennolla, jonka jälkeen meidän tarvitsee vain etsiä ohjelman _File>Open_-reittiä lataamamme tiedosto.

<img width="1920" height="564" alt="VirtualBox_Kali_08_11_2026_19_02_35" src="https://github.com/user-attachments/assets/c7f75a11-61db-424c-bc63-8ea453bc66e9" />

## f) Yleiskuva
- Näyte näyttää olevan sieppaus kolmesta signaalista.
- Klikkaamalla i-painiketta näemme, että näytteen kesto on 5.49 sekunttia.
- Tiedoston koko on 10.47MB.
- Tieto-osio näyttää luomispäiväksi ajan jona se on ladattu, mutta tiedostonimen _"20250412"_-osio kertoo tämän olevan varmemminkin luotu 12.4.2025.

<img width="955" height="488" alt="VirtualBox_Kali_08_11_2026_19_24_36" src="https://github.com/user-attachments/assets/aee1d475-f4df-430f-971d-08400fbc5793" />

## g) Bittistä
Aloitetaan demodulaatiomme painamalla _Autodetect parameters_-nappia. Tämä näyttää pitävän modulaatiomme ASK-muodossa.

<img width="288" height="312" alt="VirtualBox_Kali_08_11_2026_19_37_40" src="https://github.com/user-attachments/assets/f75ae413-d1f7-432a-a20f-fac7159fac24" />

Vaihdetaan seuraavaksi _Signal View_ muotoon _Demodulated_. Tämän avulla näkymämme muuttuu hieman helpommin tarkasteltavaksi.

<img width="955" height="549" alt="VirtualBox_Kali_08_11_2026_19_40_24" src="https://github.com/user-attachments/assets/16c0dc53-b1f6-4b18-80f4-2c306b35f19f" />

Nyt voimme valita näkymästämme yhden bitin ja tarkastella tästä tietoja!

<img width="695" height="485" alt="VirtualBox_Kali_08_11_2026_19_42_12" src="https://github.com/user-attachments/assets/8a013f2f-e2f6-4465-99dd-ae0ddc93be6d" />

Raakabittimme pituus näyttäisi olevan 522µs. 1µs on kestoltaan microsekuntti, eli MILJOONASOSA sekuntti. Verrattaessa tähän ihmisen silmänräpäytys kestää 0.1-0.4 sekunttia. Nopealla laskutoimituksella (silmänräpäytyksen ollessa keskiarvo) tämä yksi bitti on siis 383 kertaa nopeampi kuin yksi silmänräpäytys!

## Lähteet:
BNID 100706: Average duration of a single eye blink – Human Homo sapiens. Luettavissa: https://bionumbers.hms.harvard.edu/bionumber.aspx?id=100706 Luettu 8.11.2026

Cornelius 2022: Decode 433.92 MHz weather station data. Luettavissa: https://www.onetransistor.eu/2022/01/decode-433mhz-ask-signal.html Luettu 7.11.2026

Hubacek 2019: Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs. Katsottavissa: https://www.youtube.com/watch?v=sbqMqb6FVMY&t=199s Katsottu 7.11.2026

jopohl, urh github Luettavissa: https://github.com/jopohl/urh Luettu 8.11.2026

Karvinen 2026: Verkkoon tunkeutuminen ja tiedustelu. Luettavissa: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/ Luettu 8.11.2026

merbanan, rtl_433. Luettavissa: https://github.com/merbanan/rtl_433 Luettu 8.11.2026
