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

**a) Oletussivu. Vaihda Apachen oletussivu päällekirjoittamalla /var/ww/html/index.html . Voit käyttää pohjana tunnilla tekemääsi Apache-asennusta.**

Aloitetaan tehtävä asentamalla Spache virtuaalikoneelle:

>$ sudo apt-get install apache2

Sekä kokeillaan curl-komennolla, näkyykö localhostissa mitään:

>$ curl localhost
>curl: (7) Failed to connect to localhost port 80: Connection refused


Eipä näkynyt, potkaistaan Spache uuusiksi käyntiin ja katsotaan uusiksi:
>$ sudo systemctl restart apache2



Nyt toimii.

![image](https://user-images.githubusercontent.com/103587811/168430709-56e1a912-ef75-43e8-ae34-6de74d674af5.png)


Apachen oletussivun muuttamiseksi käytin seuraavaa Teron ohjetta: 

https://terokarvinen.com/2016/new-default-website-with-apache2-show-your-homepage-at-top-of-example-com-no-tilde/?fromSearch=

Aloitetaan tekemällä uusi virtuaalihost 'sivu.conf'
>$ sudoedit /etc/apache2/sites-available/sivu.conf

Lisätään sinne seuraava:

![image](https://user-images.githubusercontent.com/103587811/168434559-56aa43bd-7966-4a5f-bfd0-3941998e1fae.png)

Otetaan default sivu pois päältä ja laitetaan omat sivut toimintaan,
/sites-enabled/ hakemistossa ajetaan seuraavat komennot:

>$ sudo a2ensite tero.conf
>$ sudo a2dissite 000-default.conf



![image](https://user-images.githubusercontent.com/103587811/168434756-d9fef585-a2e5-4aa1-956b-9cc24561bec2.png)

Ja potkaistaan Apache vielä uusiks käyntiin, jotta muutokset tulevat voimaan

Oleellisin, eli varsinaiset sivut vielä puuttuvat: tehdään uusi kansio kotihakemistoon:

>$ mkdir public_html/

>lauri@latska:~$ cd public_html/

>lauri@latska:~/public_html$ pwd

>/home/lauri/public_html

Tehdään kansioon uusi html page:
>lauri@latska:~/public_html$ micro index.html

![image](https://user-images.githubusercontent.com/103587811/168437595-a2c26569-debf-45fa-89e9-5a75f1ad5d87.png)


>lauri@latska:~/public_html$ ls

>index.html

Ja kokeillaan 'curl localhost' -komennolla:

>lauri@latska:~/public_html$ curl localhost

>Testi ;')

Näyttäisi toimivan, mutta ihmetellään vielä selaimen kautta:

![image](https://user-images.githubusercontent.com/103587811/168438626-2f9b8554-1c4c-409e-8404-f0701f9d1875.png)

Alles goed








**b) Tri Kaaaos. Aiheuta erilaisia vikatilanteita ja osoita, kuinka Apache-tilasi korjaa ne. Voit esimerksi sulkea demonin (sudo systemctl stop foobar), poistaa asetukset tai poistaa apachen paketit. Osoita yksinkertaisin testein, saat palvelun toimimattomaksi, ja salt-tilasi saa sen jälleen toimimaan.**

Tähän tehtävään otin apuja Teron ohjeesta:
https://terokarvinen.com//2018/apache-user-homepages-automatically-salt-package-file-service-example/

Tehdään apachelle hakemisto saltin juureen:

>$ sudo mkdir /srv/salt/apache

Ja lisätään sinne uusi init.sls tilatiedosto:

>$ sudo micro init.sls

![image](https://user-images.githubusercontent.com/103587811/168439837-85bd663e-ad3d-427c-91d1-2f0ed6aa9a37.png)

Testataan toimiiko uusi tilafunktio:

>$ sudo salt '*' state.apply apache

![image](https://user-images.githubusercontent.com/103587811/168439878-3c55ae93-a2a0-4e7a-a99f-33723c5aa67b.png)

Näyttää toimivan - se korvaa edellisessä tehtävässä luodun index.html:n Saltin hakemistossa olevalla. Paketteihin ja conffeihin ei muutoksia. Testataan vielä vielä uusiksi, että onko idempotentti + varmistus curlilla:

>$ sudo salt '*' state.apply apache

>$ curl localhost



![image](https://user-images.githubusercontent.com/103587811/168439893-021c1266-8b2e-4eef-ba5a-9b6c42f13b7d.png)

Hyvin tuntuu toimivan. Sitten tuhotöiden kimppuun:

Ensimmäinen testi, kokeillaan käynnistääkö tilafunktio Apachen mikäli sen sammuttaa:

![image](https://user-images.githubusercontent.com/103587811/168440070-ae818c06-6c84-4bf0-bad0-3a856e340370.png)

Toimii.

Koitetaan vielä poistaa koko Apache-demoni koneelta + testataan saadaanko Saltin avulla takasin sekä conffit kuntoon:

>$ sudo apt-get purge apache2


![image](https://user-images.githubusercontent.com/103587811/168440307-c5c3b5d7-5926-4e1d-a72b-f3f56944104a.png)

Ja kokeillaan uudelleen asennus Saltilla:

![image](https://user-images.githubusercontent.com/103587811/168440374-1e2715f5-3f3c-48bc-9f08-770c95888187.png)

Sekä testi vielä curlilla:

![image](https://user-images.githubusercontent.com/103587811/168440382-20280fdc-7fbe-4bd3-96bc-9be538a6aa58.png)

Kaikki näyttää toimivan, kuten kuuluu!








**c) Shh! Asenna ja konfiguroi SSH-demoni. Laita se porttiin 7373.**

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
