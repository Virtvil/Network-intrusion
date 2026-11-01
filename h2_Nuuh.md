# h2 Nuuh
- Kurssi: Verkkoon tunkeutuminen ja tiedustelu (Karvinen 2026)
- Opettaja: Tero Karvinen
- Raportin kirjoittaja: Vili Virtanen
## x) Materiaalit
### Karvinen 2025: Wireshark - Getting Started
- Wireshark on ohjelma jolla voidaan kaapata, sekä analysoida verkkoliikennettä reaaliajassa.
- Kaapattua liikennettä pystyy tutkimaan ja filtteröimään.
- Kaapatun liikenteen pystyy myös tallentamaan myöhempää tutkailua varten.
### Karvinen 2025: Network Interface Names on Linux
- Verkkoliittymä (Network Interface) on toimii kuten verkkokortti, mutta tämän ei tarvitse olla fyysinen.
- Nimeämiskäytännöt:
  - en = langallinen ethernet
  - wl = wlan (langaton verkkoyhteys)
  - lo = loopback a
## a) Linux. Asenna Debian tai Kali Linux virtuaalikoneeseen. 
Olin asentanut Kalin itselleni jo aiemmalla kurssilla, tässä kuitenkin nopeat tiedot Kalin omaan asentamiseen:

```
Latasin itselleni Kali-imagen VirtualBox asennusta varten sivulta https://www.kali.org/get-kali/#kali-installer-images.
Aluksi ihmettelin eri valintojen välillä, mutta päädyin normaaliin installer valintaan.

Asennuksen aikana muutin virtuaalikonetta antamalla tälle enemmän muistia (4 GB) ja enemmän CPU voimaa (2 cpu).
Asennuksessa käytin kalin sivuilta saatavaa "kali-linux-2026.2-installer-amd64" iso-tiedostoa.
Asennus suijuikin ilman kummempia vaivoja, vaikka veikin normaalia Debian-versiota enemmän aikaa.

Tämän jälkeen varmistin kaikkien ohjelmieni olevan päivitettynä komennoilla "sudo apt-get update" ja "sudo apt-get upgrade"
```
## b) Ei voi kalastaa. Osoita, että pystyt katkaisemaan ja palauttamaan virtuaalikoneen Internet-yhteyden.
## c) Wireshark. Asenna Wireshark. Sieppaa liikennettä Wiresharkilla. (Vain omaa liikennettäsi. Voit käyttää tähän esimerkiksi virtuaalikonetta).
## d) Oikeesti TCP/IP. Osoita TCP/IP-mallin neljä kerrosta yhdestä siepatusta paketista. Selityksen lisäksi laatikoi ne ruutukaappauksesta.
## e) Mitäs tuli surffattua? Avaa surfing-secure.pcap. Tutustu siihen pintapuolisesti ja kuvaile, millainen kaappaus on kyseessä. Tässä siis vain lyhyesti ja yleisellä tasolla. Voit esimerkiksi vilkaista, montako konetta näkyy, mitä protokollia pistää silmään. Määrästä voit arvioida esimerkiksi pakettien lukumäärää, kaappauksen kokoa ja kestoa.
## g) Minkä merkkinen verkkokortti käyttäjällä on? surfing-secure.pcap
## h) Millä weppipalvelimella käyttäjä on surffaillut? surfing-secure.pcap
## i) Analyysi. Sieppaa pieni määrä omaa liikennettäsi. 
Analysoi se, eli selitä mahdollisimman perusteellisesti, mitä tapahtuu. (Tässä pääpaino on siis analyysillä ja selityksellä, joten liikennettä kannattaa ottaa tarkasteluun todella vähän - vaikka vain pari pakettia. Gurut huomio: Selitä myös mielestäsi yksinkertaiset asiat.)
## Lähteet:
Karvinen 2025: Wireshark - Getting Started. Luettavissa: https://terokarvinen.com/wireshark-getting-started/ Luettu 1.11.2026

Karvinen 2025: Network Interface Names on Linux. Luettavissa: https://terokarvinen.com/network-interface-linux/ Luettu 1.11.2026
