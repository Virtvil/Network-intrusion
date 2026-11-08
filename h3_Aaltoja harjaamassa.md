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
- Sääaseman signaalin anyslointia käyttäen Universal Radio Hackeria.
- Signaalia tutkiessa tämä näkyy lohkoissa.
- Valittu viesti saadaan purettua näkymään muodossa "000101001000".
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

## c) Automaattinen analyysi
## d) Too compex 16?
## e) Ultimate. Asenna URH, the Ultimate Radio Hacker
## f) Yleiskuva
## g) Bittistä

## Lähteet:
Hubacek 2019: Universal Radio Hacker SDR Tutorial on 433 MHz radio plugs. Katsottavissa: https://www.youtube.com/watch?v=sbqMqb6FVMY&t=199s Katsottu 7.11.2026

Cornelius 2022: Decode 433.92 MHz weather station data. Luettavissa: https://github.karllohner.com/SDR/Decoding/Example_2019-01-24/ Luettu 7.11.2026

merbanan, rtl_433. Luettavissa: https://github.com/merbanan/rtl_433 Luettu 8.11.2026
