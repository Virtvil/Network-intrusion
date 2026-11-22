# h5 Labratakki
- Kurssi: Verkkoon tunkeutuminen ja tiedustelu (Karvinen 2026)
- Opettaja: Tero Karvinen & Lari Iso-Anttila
- Raportin kirjoittaja: Vili Virtanen
## Mininet asennus
Aloitin lataamalla tunnilla jaetun mininet-virtuaalikoneen ja purin ladatun tiedoston käyttäen WinRar. Mininet-koneen voi tuoda VirtualBox ympäristöön luomalla uuden virtuaalikoneen, käyttäen ```Linux OS``` ja ```Ubuntu OS Distribution```. Tämän jälkeen suuntaamalla ```Specify virtual hard disk``` voimme valita ```Use An Existing Virtual Hard Disk```-osioon juuri purkamamme mininet-virtuaalikoneen ja tämän ```Student-lab.vmdk``` version. HUOM! EI FLAT-VERSIOTA!

<img width="990" height="682" alt="Näyttökuva 2026-11-21 174458" src="https://github.com/user-attachments/assets/7b8a5d0e-6a37-470b-9ae6-ec9fb559ea81" />

<img width="986" height="681" alt="Näyttökuva 2026-11-21 174122" src="https://github.com/user-attachments/assets/63e269b2-fd9a-4efc-ae21-b6f0d2022dd5" />

## a) Aja tunnilla esitetty ARP hyökkäys ja tutki, miten se toimii.
Aloitin tehtävän todeten, että tämä olisi huomattavasti helpompi tehdä Kali-koneeltani käyttäen ssh-yhteyttä mininet laitteelle. Valitettavasti olin päivittänyt ohjelmistoani hiljattain, eikä Kali-laitteeni suostunut käynnistymään graafisessa käyttöliittymässä. Tarkistin virtuaalikoneen logitiedostot ```Machine>Show Log``` avulla ja minulle selvisi, että graafinen liittymä ei tosiaankaan suostunut käynnistymään. Kyselinkin tässä vaiheessa apua ChatGptltä, joka neuvoi minua avaamaan Kali-laitteeni komentoliittymän käyttämällä ```ctr+alt+f2```, jonka avulla pystyin poistamaan tiedostoja laitteen Downloads-kansiosta ja pääsin kunnolla tehtävän kimppuun.

Ryhdyin aluksi yhdistämään koneiden verkko-adaptereita suuntaamalla VirtualBoxin asetuksiin ja asettamalla molemmille laitteille Host-only Adapterin.

<img width="702" height="377" alt="Näyttökuva 2026-11-21 222018" src="https://github.com/user-attachments/assets/217319bc-5949-469c-8cde-1219d319d6ee" />

Seuraavaksi tarkistin Mininet-laitteen ip-osoitteen ```ip a```-komennolla, ja loin yhteyden laitteiden välille komennolla ```ssh -X mininet@192.168.56.105```.

<img width="714" height="365" alt="VirtualBox_Kali_21_11_2026_22_24_02" src="https://github.com/user-attachments/assets/e67ef361-cd88-4137-be2c-bfb45836086c" />

Ryhdyin luomaan verkko-ohjaimella yhteyttä komennolla ```ryu-manager ryu.app.simple_switch_13``` ja jätin tämän taustalle pyörimaan, avaten toisen ikkunan, jolla otin myös yhteyden mininet-koneeseen. Toisella ikkunalla käytin komentoa ```sudo mn --topo single,3 --mac --switch ovsk --controller remote```.

Komennon rakenne:

| sudo mn  | --topo single, 3 | --mac | --switch ovsk | --controller remote |
| ------------- | ------------- | ------------- | ------------- |------------- |
| Antaa sudo oikeudet mininettiin | Yksinkertainen topologia, 1 kytkin, 3 laitetta | Mac osoitteet | virtuaalikytkimen tyyppi (Open v switch kernel) | Mininetin perusohjain |

<img width="1920" height="652" alt="VirtualBox_Kali_21_11_2026_22_29_02" src="https://github.com/user-attachments/assets/4717c3c2-97c7-4a2d-92e7-3a5715572dc2" />

Käytin tehtävänannon ```pingall```-komentoa ja näinkin kuinka paketit pingaantuivat toisella ruudulla, vaikka näissä ei oikein tietoja ollutkaan.

<img width="1641" height="374" alt="VirtualBox_Kali_21_11_2026_22_31_58" src="https://github.com/user-attachments/assets/93177846-05aa-4a54-b661-4aa59b5cb683" />

Käyttäessäni ```xterm```-komentoa sainkin kielteisen vastauksen väärän autentikaation takia.

<img width="582" height="106" alt="VirtualBox_Kali_21_11_2026_22_37_21" src="https://github.com/user-attachments/assets/b1e662b2-82ad-41c3-9e0c-c64ac9c866de" />

Saadakseni oikeat autentikaatiot poistuin ```exit```-komennolla ja käytin komentoa ```./get_xauth.sh``` joka antoi tulosteen ```mininet-vm/unix:13  MIT-MAGIC-COOKIE-1  85c664a665a6c92b76121ecd48468fbe
```. Tämän alkuun lisäämällä ```sudo -s xauth add``` pystyn antamaan itselleni tarvitun autentikaation! Lopullinen käytetty komento on siis muotoa: 

```
sudo -s xauth add mininet-vm/unix:13  MIT-MAGIC-COOKIE-1  85c664a665a6c92b76121ecd48468fbe
```

<img width="895" height="77" alt="VirtualBox_Kali_21_11_2026_22_40_32" src="https://github.com/user-attachments/assets/e0f701e4-8055-4466-859f-95c0a7c78ffb" />

(Kuvassa eri autentikaatio kuin lopullisessa komennossa, sillä Kali-laitteeni hyytyi välissä ja jouduin aloittamaan tehtävän alusta)

<img width="955" height="82" alt="VirtualBox_Kali_21_11_2026_22_51_33" src="https://github.com/user-attachments/assets/858bbc00-6e3a-46c6-87f8-52f577ebbbfd" />

Jonka jälkeen ```xterm```-komentomme toimii!

<img width="933" height="498" alt="VirtualBox_Kali_21_11_2026_22_52_12" src="https://github.com/user-attachments/assets/9996c973-70bc-4ec5-8a20-e806d41081cb" />

Seuraavaksi avasin kaikki kolme ikkunaa (_h1, h2 ja h3_) ja syötin h3-terminaaliin komennot:

```
sysctl -w net.ipv4.ip_forward=1 
```

```
iptables -t nat -A PREROUTING -p tcp --dport 22 -j REDIRECT --to-port 22
```

```
tcpdump –i h3-eth0 –w arp-p.pcap &
```

```
wireshark &
```

Joista viimeisin avasi wiresharkin, jolla pystyn kaappaamaan liikennettä _h3-th0_-kohteesta.

<img width="1767" height="808" alt="VirtualBox_Kali_21_11_2026_22_59_09" src="https://github.com/user-attachments/assets/afe7733f-1bb9-4968-b9cc-702df3fe9c5d" />

Seuraavaksi komennolla ```sshesame -port 22 -listen_address 0.0.0.0``` saamme _h3_-terminaalimme kuuntelemaan kaapattua yhteyttä. Syöttääksemme arp-myrkytyksen avataan uusi _h3_-terminaali ```xterm h3```-komennolla ja käynnistetään myrkytys komennolla ```python3 ./arp_poison.py```.

<img width="767" height="338" alt="VirtualBox_Kali_21_11_2026_23_02_24" src="https://github.com/user-attachments/assets/5266525c-b5ee-4f72-a366-8c7bbdd49a2e" />

Näemme heti liikennettä Wiresharkissa, jossa käynnistetty komento kyselee jatkuvasti APR-kyselyitä.

<img width="1170" height="588" alt="VirtualBox_Kali_21_11_2026_23_03_46" src="https://github.com/user-attachments/assets/c760cac9-fc1d-4b13-bf38-15fcda689538" />

Kokeillaan seuraavaksi yhdistää _h2_-terminaaliin käyttäen _h1_-terminaalia.

<img width="955" height="454" alt="VirtualBox_Kali_21_11_2026_23_05_23" src="https://github.com/user-attachments/assets/88861af0-8ef6-462d-bd58-30959958b3b2" />

Emme saa yhteyttä, sillä ssh näkee identifikaation ja julkisen avaimen muuttuneen ja estää yhteyden. Pystymme poistamaan julkisen avaimen _h2_-terminaaliin komennolla:

```
ssh-keygen –R h2
```

<img width="885" height="115" alt="VirtualBox_Kali_21_11_2026_23_08_44(2)" src="https://github.com/user-attachments/assets/75d42708-ee02-4050-9831-df7911073024" />

Yritetään muodostaa yhteys uudelleen:

<img width="621" height="151" alt="VirtualBox_Kali_21_11_2026_23_08_44" src="https://github.com/user-attachments/assets/09a40842-cbc2-4398-acf5-f2fb819ee04e" />

Yhteys onnistuu ja _h3_-terminaali, jonka asetimme aiemmin kuuntelemaan liikennettä, on tallentanut tapahtuman:

<img width="769" height="358" alt="VirtualBox_Kali_21_11_2026_23_09_03" src="https://github.com/user-attachments/assets/8304fa5f-3519-4568-bffe-46e84a180efa" />

Näemme myös muutokset Wiresharkissa:

<img width="955" height="507" alt="VirtualBox_Kali_21_11_2026_23_09_31" src="https://github.com/user-attachments/assets/27971c35-612f-4527-8c16-6bb911586309" />

Harjoituksen ideana on lähettää _h3_-terminaalilla toistuvia ARP-vastauksia, jossa se tämä väittää omaavansa harjoituksen _h1_ ja _h2_-laitteiden IP-osoitteet. Hyökkäyksessä siis lähetetään väärennettyjä ARP-vastauksia joiden kautta kohdekone päätyy väärään IP-/MAC-osoitteeseen. Tällöin kohdekoneen likenne päätyy hyökkääjälle, eikä alkuperäiselle kohteelle.
## b) Samassa hakemistossa on myös ICMP Spoofing ja TCP Session Hijacking. Aja molemmat labrat läpi ja kerro, miten molemmat tekniikat toimivat.
### ICMP Spoofing
Suljin aiemman tehtävän xterm-terminaalit ja siirryin mininet koneella kohteeseen /lab/01_Network-Security-Lab/scripts, jossa pääsin tehtävään käsiksi komennolla ```sudo python3 hub_topo.py```. Törmäsin jälleen kerran ongelmaan autentikoinnin kanssa ja ChatGPT:ltä kysellessä sain ehdotukseksi valtuuksien selvittämiseen ```xauth list```-komennon.

<img width="955" height="409" alt="VirtualBox_Kali_22_11_2026_14_58_18" src="https://github.com/user-attachments/assets/da3e0b3f-d5af-432e-ae6c-00f94d2a4b90" />

Komennon avulla sainkin autentikaatiot tietooni, ja pystyin lisäämään ne itselleni aiemmasta tehtävästä tutuilla ```sudo xauth add```-komennoilla:
```
sudo xauth add mininet-vm/unix:11  MIT-MAGIC-COOKIE-1  d7dc501e8619120c5a1b3b8fef974b1b
```
```
sudo xauth add mininet-vm/unix:12  MIT-MAGIC-COOKIE-1  c075527a6cbd3011f2406a9ae4a66a3c
```
```
sudo xauth add mininet-vm/unix:13  MIT-MAGIC-COOKIE-1  85c664a665a6c92b76121ecd48468fbe
```
```
sudo xauth add mininet-vm/unix:10  MIT-MAGIC-COOKIE-1  a8c3eabb4d12fdbecf5ad23fb32b3813
```

<img width="955" height="277" alt="VirtualBox_Kali_22_11_2026_15_02_51" src="https://github.com/user-attachments/assets/600a6881-bfce-4287-a180-d99cc7a3cf06" />

Nyt ajamalla aiemman ```sudo python3 hub_topo.py```-komennon pystyin luomaan itselleni terminaalit ```xterm```-komennoilla.

<img width="1223" height="727" alt="VirtualBox_Kali_22_11_2026_15_05_00" src="https://github.com/user-attachments/assets/1e25f5bc-3a65-43db-bddc-c3d62326d505" />

- _H1_-terminaalissa ajetaan komento ```python3 sniff_icmp.py```, joka kuuntelee liikennettä.
- _H2_-terminaalissa lähetetään ```ping 10.0.0.1``` komento.
- _H3_-terminaalissa käytetään komentoa ```python spoof_icmp.py```, joka lähettää ylimääräisiä ICMP-paketteja.

<img width="955" height="703" alt="VirtualBox_Kali_22_11_2026_15_07_24" src="https://github.com/user-attachments/assets/6b928505-ae5d-492a-bf40-b58330be23e9" />

Verkkoon ilmestyy lisää paketteja, joilla on väärennettyjä lähdeosoitteita ja jotka tämän vuoksi näyttävät tulevan oikeasta osoitteesta.
### TCP Session Hijacking
Seuraava tehtävä suoritetaan samassa labrassa, vaihdetaan vain terminaalit uusiin. ```xterm```-komennolla _h1_, _h2_, _h3_ terminaalit pyörimään ja ajetaan terminaaleilla seuraavat komennot:

- _H1_-terminaaliin ```python tcp_server.py```, joka kuuntelee taustalla.
- _H2_-terminaaliin ```python tcp_client.py``` jolla muodostamme yhteyden.
- _H3_-terminaaliin ```python sniff_tcp_session.py```, joka kuuntelee ("sniffaa") liikennettä.
- Avataan tämän lisäksi vielä toinen _h3_-terminaali, koska aiempi terminaalimme kuuntelee liikennettä, johon laitamme ```python tcp_hijack.py```-komennon. Komento syöttää väärennettyjä paketteja istuntoon.

<img width="955" height="678" alt="VirtualBox_Kali_22_11_2026_15_24_16" src="https://github.com/user-attachments/assets/709eab18-7a19-4a0b-a40b-574718fe62c7" />

Näemme syötteessä aktiiviseen yhteyteen ilmestyvän lisää paketteja!
## c) Hakemistossa 02-SDN-DDos_Simulation tryout-kansiossa on työkalut, jotta voit ajaa TCP SYN-Flood-hyökkäyksen turvallisesti. Kirjoita, miten ajoit hyökkäyksen ja miten kyseinen hyökkäys toimii.

## Lähteet:
DDoS Simulation in a Software Defined Network, README. Luettavissa: https://github.com/santhisenan/SDN_DDoS_Simulation?tab=readme-ov-file Luettu 22.11.2026


Karvinen 2026: Verkkoon tunkeutuminen ja tiedustelu. Luettavissa: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/ Luettu 21.11.2026

Network-Security-Lab, README. Luettavissa: https://github.com/ssam246/Network-Security-Lab Luettu: 22.11.2026
