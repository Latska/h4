# h2 package-file-service
**z) Lue ja tiivistä, muutama ranskalainen viiva riittää.**

**SaltStack Configuration Management: Get Started Tutorial**
  * Introduction
  * Functions
  * Files
  – SaltStackin configuration management -järjestelmän avulla voidaan määrittää sovelluksia, tiedostoja ja muita asetuksia specifiin järjestelmään.
  – Järjestelmässä voidaan tehdä konfiguraatioita ja muutoksia tarpeen mukaan.
  – Terminologiaa:
  * Formula – Salt State ja Salt Pillar tiedostoja, jotka määrittelevät sovelluksen tai järjestelmä komponentin.
  * State – Uudestaan käytettävä ilmoitus, joka konffaa tietyn järjestelmän osan. Jokainen state määritellään State Declarationin avulla.
  * State Declaration – State File:n ylin osa, joka listaa State Function kutsut ja argumentit, jotka kaikki muodostavat State:n. Jokainen State Declaration alkaa yksilöllisellä ID:llä.
  * State Functions – Komennot, joilla suoritetaan konfiguraatioita.
  * State File – SLS-tunnisteellinen tiedosto, joka sisältää yhden tai useamman State Declarationin.
  * Pillar File – SLS-tunnisteellinen tiedosto, joka määrittää muuttujat ja datan järjestelmälle.
  – Salt Functionit alkaa komennolla: salt.states.
  – Salt Statet ovat YAML-muodossa:
  * Ensimmäinen rivi Salt Declarationissa on ID
  * ID:n alapuolella voidaan kutsua yhtä tai useampaa Salt State -funktiota
  * ID ja jokainen funktio päättyy kaksoispisteeseen (:) ja jokainen funktiokutsu on sisennetty kahdella välilyönillä tunnuksen alapuolella.
  * Parametrit välitetään luettelona jokaiselle funktiolle, jokainen rivi joka sisältä funktioargumentin, alkaa kahden välilyönnin sisennyksellä, yhdysviivalla ja välilyönnillä.
  * Mikäli argumentilla on yksi arvo, sen nimi ja arvo ovat samalla rivillä erotettuina kaksoispisteellä ja välilyönnillä.
  – Saltin avulla voidaan hallita tiedostoja mallien ja muuttujien avulla
  * salt.states.file – löytää hyvin lisätietoja
  – Esimerkki käyttäjän lisäyksestä Saltilla:

user account for late:
user.present:
- name: late
- shell: /bin/bash
- home: /home/late
- groups:
- sudo



**Karvinen 2008: Install Apache Web Server on Ubuntu**

Apache on avoimeen lähdekoodiin perustuva webbipalvelin Linuxille.
Tärkeimpiä komentoja:
– Apachen asennus:
$ sudo apt-get install apache2
– Voidaan testailla palvelinta paikalliselta koneelta
$ firefox ”http://localhost&#8221;
– Palvelimen näkyminen verkkoon:
$ ip addr
– Omalla IP-osoitteella testaus:
$ firefox ”http://x.x.x.x&#8221;
– Mikäli DNS toimii verkossa, voidaan testata domainin toimivuus:
$ host 1.2.3.4
– Käyttäjäoikeuksien anto sivun luomiselle:
$ sudo a2enmod userdir
– Apassidemonin uudelleenkäynnistys:
$ sudo systemctl restart apache2
– Sivujen testaus:
$ cd
$ mkdir public_html
$ whoami
$ firefox ”http://localhost/~(whoami)&#8221;


Apache User Homepages Automatically – Salt Package-File-Service Example

* Saltin avulla voidaan automatisoida Apachen asennus.
* Ensimmäisellä kerralla kaikki on asennettava manuaalisesti: Automatisointi toimii vain asioille, joita osataan tehdä manuaalisesti.
* Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port

* Configuration management systeemin avulla voidaan hallita valtavaa määrää demoneja.
* Package-file-service on yleinen malli tähän: asennetaan softa, vaihdetaan configuration file ja potkaistaa dmeoni uudestana käyntiin, jotta konffaukset toimii.
* SaltStack contributors 2021: Salt system architecture

* Tarjoaa hyvän yleiskatsauksen Saltin arkkitehtuurista ja komponenteista
* Yksi tapa kuvailla Saltia on julkaisija-tilaaja -malli, jossa master julkaisee suoritettavat työt ja minionit tilaavat nämä työt.
– Kun tietty työ koskee tiettyä minionia, se suorittaa työn.
** a) Oletussivu. Vaihda Apachen oletussivu päällekirjoittamalla /var/ww/html/index.html . Voit käyttää pohjana tunnilla tekemääsi Apache-asennusta.
Apache:n olin jo ehtinyt asentaa koneelleni komennolla:
$ sudo apt-get install apache2



TEKNISIÄ ONGELMIA — KESKEN

(TÄYDENNETÄÄN KESKIVIIKKONA 13.4.)

**b) Tri Kaaaos. Aiheuta erilaisia vikatilanteita ja osoita, kuinka Apache-tilasi korjaa ne. Voit esimerksi sulkea demonin (sudo systemctl stop foobar), poistaa asetukset tai poistaa apachen paketit. Osoita yksinkertaisin testein, saat palvelun toimimattomaksi, ja salt-tilasi saa sen jälleen toimimaan.**


TEKNISIÄ ONGELMIA — KESKEN

(TÄYDENNETÄÄN KESKIVIIKKONA 13.4.)

** c) Shh! Asenna ja konfiguroi SSH-demoni. Laita se porttiin 7373.

Tähän tehtävään otin apuja Teron Pkg-File-Service – Control Daemons with Salt – Change SSH Server Port -ohjeesta:

Aluksi luodaan SSH:lle oma init.sls ja lisätään sinne seuraavat konfiguraatiot:

![image](https://user-images.githubusercontent.com/103587811/168429057-4d28aee9-350a-4e53-bf95-e1a59cbf2085.png)



Tämä ei kuitenkaan mennyt orjalle läpi vaan antoi seuraavan virheen:

![image](https://user-images.githubusercontent.com/103587811/168429062-00bdd2b3-a16b-4db7-887c-f3e3c342e372.png)


Kommentista se kätevästi selvisikin, sshd_config -tiedostoa ei /srv/salt vielä löytynyt, joten kopioin SSH:n ”alkuperäisen” konffitiedoston ja lisäsin sen kyseiseen hakemistoon:

![image](https://user-images.githubusercontent.com/103587811/168429066-cc9b6034-065e-404d-a2ac-a7daf1cd057e.png)



Tässä vaiheessa muistui vielä mieleen tehtävän idea, eli vaihtaa SSH:n portti osoitteeseen 7373:

![image](https://user-images.githubusercontent.com/103587811/168429070-e5474a02-2e0b-4674-8152-b7b34ac65859.png)


Ja kokeiltiin sshd-tilafunktiota uudelleen:

![image](https://user-images.githubusercontent.com/103587811/168429073-54cf35a6-1e62-4de7-954c-df9a3dec5a47.png)



Ja vielä:

![image](https://user-images.githubusercontent.com/103587811/168429077-9fd03dea-709b-4bec-b3f3-edb8b78863dd.png)


Tulimuuriin reiät:

![image](https://user-images.githubusercontent.com/103587811/168429081-df89cd5a-94e6-4f10-9b65-e7346e2d055c.png)



Ja testataan toimiiko SSH-yhteys:

![image](https://user-images.githubusercontent.com/103587811/168429087-b9e3ed05-2b38-4b46-b072-3b021abbaab5.png)



**m) Vapaaehtoinen: Asenna ja konfiguroi Nginx-weppipalvelin.**

Vinkkejä

Ensin käsin, vasta sitten automaattisesti. Raportoi myös käsin (perinteisillä Linux-komennoilla) tekemäsi testit.
SSH-demoni löytyy paketista openssh. Kun saat sen vastaamaan uudesta portista, sinulla on valmis mallitiedosto jaettavaksi masterilta. Katso myös /etc/ssh/sshd_config, ’man ssh’ ja ’man sshd_config’.
Kirjoittamani esimerkki sshd:n säätämisestä on vanhemmalle versiolle, jonka asetustiedosto tuskin toimii sellaisenaan. Mistä löytyisi tuoreempi…
Jos haluat lähettää kokonaisia tiedostoja orjille, laita ne samaan hakemistoon masterilla init.sls kanssa. Jos masterilla tiedosto on ”/srv/salt/heitero/tero.txt”, siihen viitataan file.managed source parametrilla ”salt://heitero/tero.txt”. Eli tuo ”protokolla” salt:// tarkoittaa oikeastaan masterin /srv/salt/-hakemistoa.
Vaikeita kohtia? Ratko kaikki mitä osaat, raportoi ja palauta ajoissa. Vaikeasta tai kesken jääneestä kohdasta erityisen tarkka raportti: mitä teit, mitä tapahtui. Ota ruutukaappaukset ja sanatarkat virheilmoitukset talteen. Mistä arvelet ongelman johtuvan? Mitä ratkaisuvaihtoehtoja vielä voisi kokeilla? Löydätkö (esim virheilmoituksella hakemalla) lähteitä, joissa ehdotetaan ratkaisuja? Ja katsotaan yhdessä tunnilla loput.
LÄHTEET:

https://terokarvinen.com/2021/configuration-management-systems-2022-spring/

https://terokarvinen.com/2008/05/02/install-apache-web-server-on-ubuntu-4/

https://terokarvinen.com//2018/apache-user-homepages-automatically-salt-package-file-service-example/

https://terokarvinen.com//2018/pkg-file-service-control-daemons-with-salt-change-ssh-server-port/
