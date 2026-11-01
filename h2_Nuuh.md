# h2 Nuuh
- Kurssi: Verkkoon tunkeutuminen ja tiedustelu (Karvinen 2026)
- Opettaja: Tero Karvinen & Lari Iso-Anttila
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
Virtuaalikoneen Internet-yhteyden katkaisu onnistuu helposti suuntaamalla Oracle VirtualBox Manageriin ja meidän Kali-koneemme asetuksiin ja poistamalla täpän kohdasta Settings>Network>Enable Network Adapter.

<img width="966" height="616" alt="Näyttökuva 2026-11-01 204000" src="https://github.com/user-attachments/assets/3d4a8f1b-290a-42b8-a6ee-29d05c9a330f" />

Tämän jälkeen voimme kokeilla yhteyttä komennolla:

```
ping 1.1.1.1
```
<img width="524" height="114" alt="VirtualBox_Kali_01_11_2026_20_39_01" src="https://github.com/user-attachments/assets/e40cb2e3-1e89-457a-962e-f66dcf5dbc56" />

Yhteys ei kulje! Pystymme yhteyttä kaivatessa palauttamaan tämän samasta kohdasta kuin irroitimmekin. Yhteyden testaus on suotavaa tämän jälkeen.

<img width="507" height="246" alt="VirtualBox_Kali_01_11_2026_20_45_54" src="https://github.com/user-attachments/assets/2c328416-534e-4f1b-9319-5bfcc5e4820a" />

Yhteytemme toimii jälleen!

HUOM! Näytetty tapa on varma keino jolla yhteys katkeaa. Yhteyden voi myös katkaista Kalista, näytön oikean yläkulman Ethernet Network valikosta simppelillä disconnect valinnalla.

<img width="458" height="193" alt="VirtualBox_Kali_01_11_2026_23_13_49" src="https://github.com/user-attachments/assets/28e07176-cb87-4603-bd6c-32204ddfd76b" />


## c) Wireshark. Asenna Wireshark. Sieppaa liikennettä Wiresharkilla. 
Wireshark löytyy valmiiksi jo Kali-koneestani, mutta tämän asennus onnistuu helposti komennoilla:

```
sudo apt update
sudo apt-get install wireshark
```

Näytetään nyt kuitenkin, että wireshark meiltä löytyy, käyttämällä komentoa:

```
wireshark --version
```

<img width="728" height="247" alt="VirtualBox_Kali_01_11_2026_20_56_04" src="https://github.com/user-attachments/assets/abe5b33c-c212-42ac-8f22-0f85e297578e" />

Avataan seuraavaksi Wireshark ja verkkoyhteys haluamallemme sivulle. Aloitetaan painamalla hain pyrstöä sovelluksen vasemmasta yläkulmasta ja avaamalla verkkosivu (avasin itse verkkosivun Googlen aloitussivulle). Näemmekin heti yhteyden muodostuessa kuinka dataa alkaa "jäämään kiikkiin"!

<img width="1494" height="823" alt="VirtualBox_Kali_01_11_2026_21_03_40" src="https://github.com/user-attachments/assets/294fc3f2-0055-4a2a-9c25-c62a4f394b16" />

Kaappauksen pystyy lopettamaan pyrstön (aloituspainikkeemme) viereisestä stop-painikkeesta.
## d) Oikeesti TCP/IP. Osoita TCP/IP-mallin neljä kerrosta yhdestä siepatusta paketista. Selityksen lisäksi laatikoi ne ruutukaappauksesta.
Pystymme tutkimaan helpommin kuinka nappaamamme data sijoittuu eri kerroksille suuntaamalla Wiresharkissa kohtaan statistics>Protocol Hierarchy.

Normaalisti tiedot näkyisivät helposti vain alaspäin vilkaisemalla, mutta tiedot jäsentyvät mielestäni näin miellyttävemmin.

<img width="787" height="353" alt="VirtualBox_Kali_01_11_2026_21_08_02" src="https://github.com/user-attachments/assets/09211837-0c40-48de-bb3e-36857afe7f57" />

<img width="1208" height="357" alt="VirtualBox_Kali_01_11_2026_21_17_38" src="https://github.com/user-attachments/assets/b05de7c7-e46f-476d-a760-1ffe59a7f901" />

```
Linkkikerros = Ethernet
Internet = Internet Protocol Version 4 
Kuljetuskerros = User Datagram Protocol
Sovelluskerros = Domain Name Protocol
```
## e) Mitäs tuli surffattua? Avaa surfing-secure.pcap. Tutustu siihen pintapuolisesti ja kuvaile, millainen kaappaus on kyseessä. 
Latasin tehtävänannossa mainitun ```surfing-secure.pcap```-tiedoston ja avasin tämän Wiresharkissa.

<img width="1478" height="701" alt="VirtualBox_Kali_01_11_2026_21_55_14" src="https://github.com/user-attachments/assets/ef25133a-3668-499b-83e6-503e9a5ed7bf" />

Aukeava tiedosto paljaa kaapatun verkkoyhteyden, jossa nopealla vilkaisulla näemme käyttäjän menneen Googleen ja täältä terokarvinen.com -sivulle. Tämän lisäksi näemme tiedoista, että kyseinen kaappaus sisältää 283 pakettia.
## g) Minkä merkkinen verkkokortti käyttäjällä on? 
Normaalisti voimme tutkia käyttäjän verkkokorttia MAC-osoitteen avulla. MAC-osoite sijaitsee ETHERNET II-tasolla, ja pystymme kurkkaamaankin helposti tästä tietoja hakutulostemme alta.

<img width="1486" height="703" alt="VirtualBox_Kali_01_11_2026_22_01_06" src="https://github.com/user-attachments/assets/0ff209ba-dfbc-4d2e-8e1f-f2232ec7a1ef" />

Kurkistaessamme kaappaukseen näemme kuitenkin, että kaapattussa lähetyksessä käytetty MAC-osoite ei ole oletuksellinen osoite, jolloin emme löydä tästä helposti lisätietoja käyttäen verkosta löytyviä MAC-osoitteiden tarkistuspalveluita... MAC-osoitteemme on siis satunnaistettu, emmekä pysty selvittämään tätä (ainakaan tällä hetkellä oppimillamme toiminnoilla).
## h) Millä weppipalvelimella käyttäjä on surffaillut? 
Hakemalla hakukentästä "dns" näemme kaikki nimipalvelut joilla käyttäjä on käynyt.

<img width="1920" height="601" alt="VirtualBox_Kali_01_11_2026_22_19_43" src="https://github.com/user-attachments/assets/143e1c21-242d-4f21-ab76-b27b185b0a03" />

Sivustoja ovat:
- google.com
- terokarvinen.com
- gc.zgo.at
- goatcounter.netlify.com
- commentero.terokarvinen.com
## i) Analyysi. Sieppaa pieni määrä omaa liikennettäsi. 
Päätin ottaa tehtävää varten vain muutaman paketin, joten päädyin pingaamaan Cloudflaren nimipalvelinta (ping 1.1.1.1) muutaman kerran, tallentaen liikenteen Wiresharkilla.

<img width="1920" height="886" alt="VirtualBox_Kali_01_11_2026_22_54_43" src="https://github.com/user-attachments/assets/81ce93c5-cf14-42db-a010-66f07edc3596" />

Rivit 1, 3, 5 ja 7 näyttävät virtuaalikoneelta lähtevät ping-pyynnöt palvelimelle ja rivit 2, 4, 6 ja 8 näyttävät täältä palautuvat vastaukset.

Riveillä 9 ja 10 näkyvät tapahtuman ARP-kyselyt, joissa ARP-kyselyillä kysellään MAC osoitteita.

Length-osio kertoo meille ICMP-protokollan viestien pituudeksi 98 tavua, ensimmäisen ARP kyselyn pituudeksi 42 tavua ja tämän vastauksen olleen 64 tavua.

<img width="1055" height="323" alt="VirtualBox_Kali_01_11_2026_23_01_13" src="https://github.com/user-attachments/assets/a8306bfd-59ff-4105-9bcd-24a75a4f405a" />

Tutkimalla kyselyn alla olevia tietokenttiä pystymme näkemään kyselyn tarkan ajankohdan (1.11.2026, klo 22:53).

<img width="1030" height="197" alt="VirtualBox_Kali_01_11_2026_23_03_28" src="https://github.com/user-attachments/assets/90aa1759-7bd1-48b3-bd4b-d8e116024875" />

Jatkamalla tutkintaa näemme, että käytössämme on PCSSystemtec_79 verkkokortti!

Tehtävässä olisi varmasti ollut järkevämpää käyttää esimerkiksi aiempaa Googlen etusivua, sillä tämä verkkoyhteys loisi paljon enemmän kyselyitä tutkittavaksi.
## Lähteet:
Karvinen 2025: Wireshark - Getting Started. Luettavissa: https://terokarvinen.com/wireshark-getting-started/ Luettu 1.11.2026

Karvinen 2025: Network Interface Names on Linux. Luettavissa: https://terokarvinen.com/network-interface-linux/ Luettu 1.11.2026

Karvinen 2026: Verkkoon tunkeutuminen ja tiedustelu. Luettavissa: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/ Luettu 1.11.2026
