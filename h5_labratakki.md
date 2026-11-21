<img width="702" height="377" alt="image" src="https://github.com/user-attachments/assets/cfebc3c6-2b29-46fd-87ee-e063bf5d67e1" /># h5 Labratakki
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

Komennon tarkoituksena on INSERT TARKOITUS TÄHÄN!!!

<img width="1920" height="652" alt="VirtualBox_Kali_21_11_2026_22_29_02" src="https://github.com/user-attachments/assets/4717c3c2-97c7-4a2d-92e7-3a5715572dc2" />

Käytin tehtävänannon ```pingall```-komentoa ja näinkin kuinka paketit pingaantuivat toisella ruudulla, vaikka näissä ei oikein tietoja ollutkaan.

<img width="1641" height="374" alt="VirtualBox_Kali_21_11_2026_22_31_58" src="https://github.com/user-attachments/assets/93177846-05aa-4a54-b661-4aa59b5cb683" />

Käyttäessäni ```xterm```-komentoa sainkin kielteisen vastauksen väärän autentikaation takia.

<img width="582" height="106" alt="VirtualBox_Kali_21_11_2026_22_37_21" src="https://github.com/user-attachments/assets/b1e662b2-82ad-41c3-9e0c-c64ac9c866de" />

Saadakseni oikeat autentikaatiot poistuin ```exit```-komennolla ja käytin komentoa ```./get_xauth.sh``` joka antoi tulosteen ```mininet-vm/unix:13  MIT-MAGIC-COOKIE-1  85c664a665a6c92b76121ecd48468fbe
```. Tämän alkuun lisäämällä ```sudo -s xauth add``` pystyn antamaan itselleni tarvitun autentikaation! Lopullinen käytetty komento on siis muotoa: 
```sudo -s xauth add mininet-vm/unix:13  MIT-MAGIC-COOKIE-1  85c664a665a6c92b76121ecd48468fbe
```

<img width="895" height="77" alt="VirtualBox_Kali_21_11_2026_22_40_32" src="https://github.com/user-attachments/assets/e0f701e4-8055-4466-859f-95c0a7c78ffb" />

## b) Samassa hakemistossa on myös ICMP Spoofing ja TCP Session Hijacking. Aja molemmat labrat läpi ja kerro, miten molemmat tekniikat toimivat.
## c) Hakemistossa 02-SDN-DDos_Simulation tryout-kansiossa on työkalut, jotta voit ajaa TCP SYN-Flood-hyökkäyksen turvallisesti. Kirjoita, miten ajoit hyökkäyksen ja miten kyseinen hyökkäys toimii.
## Lähteet:
Karvinen 2026: Verkkoon tunkeutuminen ja tiedustelu. Luettavissa: https://terokarvinen.com/verkkoon-tunkeutuminen-ja-tiedustelu/ Luettu 21.11.2026
