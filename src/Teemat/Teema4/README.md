# 4\. Järjestelmän ylläpito

## 4.1: Käyttäjähallinta

### *1. Luo kaksi uutta käyttäjää (opettaja ja opiskelija). Käytä toisen luomisessa komentoriviä ja toisen graafista käyttöliittymää. Aseta käyttäjille myös kotihakemistot.*

- Lisätään uusi käyttäjä Linuxista löytyvän adduser- komennon avulla

- Käyttäjän voisi myös tehdä komennolla useradd -m username, jossa -m luo käyttäjälle kotihakemiston

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/add.jpg)

Lisääminen graafisen liittymän kautta tapahtuu painamalla Add nappulaa.

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/home.jpg)

Käyttäjien kotihakemistot

---

### *2. Lisää toinen käyttäjistä ryhmään nimeltä “opiskelijat” ja toinen ryhmään "opettajat". Käytä ainakin toisessa operaatiossa komentoriviä.*

sudo usermod -a -G opettajat opettaja

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/group.jpg)

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/opisGroup.jpg)

---

### *3. Luo hakemistot “opiskelijoiden_tiedostot” ja "opettajien_tiedostot", joille annat oikeudet vain asianosaisille ryhmille. Varmista kokeilemalla molemmilla käyttäjillä, että oikeudet ovat voimassa. Käytä ainakin toisessa operaatiossa komentoriviä.*


Opiskelijat:

Luodaan hakemisto:

`sudo mkdir /home/opiskelija/opiskelijoiden_tiedostot`

Asetetaan vaadittavat oikeudet:

`sudo chown opiskelija /home/opiskelija/opiskelijoiden_tiedostot | sudo chgrp opiskelija /home/opiskelija/opiskelijoiden_tiedostot | sudo chmod 770 /home/opiskelija/opiskelijoiden_tiedostot`


Opettajat:

Komennot voidaan myös putkittaa yhteen

`sudo mkdir /home/opiskelija/opiskelijoiden_tiedostot | sudo chown opiskelija /home/opiskelija/opiskelijoiden_tiedostot | sudo chgrp opiskelija /home/opiskelija/opiskelijoiden_tiedostot | sudo chmod 770 /home/opiskelija/opiskelijoiden_tiedostot`

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/hakemistot.jpg)

---

### *4. Lukitse molemmat tunnukset väliaikaisesti. Käytä sekä komentoriviä että graafista käyttöliittymää.*

Lukitaan opettaja komentorivin kautta: Sudo usermod -L opettaja

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/lock.jpg)

Opiskelija käyttöliittymän kautta

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/lock2.jpg)

---

## 4.2: Prosessien hallinta

### *Käynnistä komentoriviltä muutamia ohjelmia, esim pico-editori ja firefox selain. Tutki järjestelmän prosesseja sekä graafisessa käyttöliittymässä että komentoriviltä.*

### *1. Selvitä mitkä ovat prosessien ID numerot ja millä prioriteetilla ohjelmat ajetaan?*

Käytetyt ohjelmat: Firefox ja Celluloid

Firefox ID: 3022, prioriteetti 20. Celluloid ID 3256 prioriteetti 20.

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/process.jpg)

---

### *2. Muuta prosessien nice-arvoja siten, että niitä ajetaan korkeammalla prioriteetilla.*

`nice -n 5 firefox &`

`nice -n 4 celluloid &`

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/niceprio.jpg)

---

### *3. Lopeta prosessit komentorivillä, käyttäen kill-komentoa. Kokeile erilaisia valitsimia. Kerro mitä valitsimet tekevät.*

Lopetetaan prosessi ID:n avulla: `kill % (PID)`

Lopetetaan prosessi ohjelman nimellä: `kill (ohjelman nimi)`

---

### *4 .Etsi käynnistämäsi sovellukset prosessilistauksesta yhdellä tai useammalla grep-komennolla.*

Etsitään "Firefox" ja celluloid

`ps aux | egrep 'firefox|celluloid'`

Etsitään prosesseista termiä ”Firefox” sekä ”Celluloid” ja putkitetaan se niin että AWK tulostaa saatujen hakujen prosessinumerot

`aux | egrep 'firefox|celluloid' | awk '{print $2}'`

---

### *5. Miten lopettaisit ne yhdellä komennolla*

`pkill -9 -f "\.\/.+\s\.|firefox|celluloid|\[^"`

---

### *6. Luo crontabiin joukko ajastuksia. Määrittele ajettavaksi seuraavanlaisia ohjelmia:*

Maanantaisin klo 8:58 suoritetaan komento "firefox http://www.iltalehti.fi"

- 58 8 * * mon export DISPLAY=:0 && firefox http://www.iltalehti.fi

Keskiviikkoisin klo 15:00 suoritetaan komento "sudo apt-get update && sudo apt-get update -y"

- 0 15 * wed sudo apt-get update && sudo apt-get update -y ?

Joka päivä klo 23:55 suoritetaan komento "varmuuskopioi.sh". Komento tulisi suorittaa root-käyttäjän oikeuksin ja sen tulostus tulisi lähettää sähköpostilla osoitteeseen yllapito@yritys.com

--

---

## 4.3: Palveluiden luominen

### *1. Käynnistä Linux-terminaali ja tutki järjestelmän palveluita. Kuinka monta palvelua on running tilassa?*

1 palvelu running tilassa

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/infotop.jpg)

Etsi rsyslog -niminen palvelu. Millä komennolla löydät palvelun?

`ps aux | grep 'rsyslog'`

Onko palvelu käytössä?

- systemctl list-unit-files --type service --state enabled,generated

- rsyslog ei ole käytössä

Onko palvelu käynnissä? (running)

- systemctl list-units --type service state running

- rsyslog on käynnissä

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/running.jpg)

Mikä on Rsyslog palvelun PID

- pgrep ´rsyslog´

- Tulos: 2152

Verkosta tai man-sivuiltas mitä kyseinen palvelu tekee?

- Rsyslog on avoimen lähdekoodin loki seuranta palvelu, jota käytetään UNIX tyyppisissä järjestelmissä lokiviestien edelleen lähettämiseen IP verkossa.

---

### *2. Uudelleenkäynnistä Rsyslog palvelu.*

- sudo service rsyslog restart

---
### *3. Luo sen jälkeen uusi palvelu nimeltä testi. Palvelun tulee sisältää seuraava bash skripti:*

`echo "Testi starttaa"

while :

do

[ -d "/home" ] && echo "Directory /home/ exists.";

sleep 15s;

done`

Ota kuva palvelun Statuksesta.

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/testirunning.jpg)

Mikä on palvelun PID?

- ps aux | grep testipalvelu.service

- PID 3964

- Ylemmässä kuvassa oleva Main PID 2592 viittaa testi.sh tiedostoon

Mitä statuksessa tulostetaan?

- Statuksessa tulostetaan palvelun tila (enabled/disabled) onko palvelu käynnissä (running), muisti määrä, Main PID mikä viittaa bash skriptiin

Ota kuvakaappaus tai tuloste talteen tekemästäsi palvelusta ja sen suorituksesta

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/testistatus.jpg)

---

## 4.4: Resurssien hallinta

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/htop.jpg)

### *1. Mikä palvelu käyttää eniten suoritinta Htop sovelluksessa?*

- PID 1340 – cinnamon

---

### *2. Mikä palvelu käyttää eniten muistia?*

- PID 1340 - cinnamon

---

### *3. Kuinka pitkään tietokone on ollut käynnissä?*

- 9min 54 s

---

### *4. Kuinka paljon muistia on käytössä yhteensä ja mikä on kokonaismäärä?*

- 697M / 981M

---

### *5. Käynnistä Firefox prosessi, etsi se htop sovelluksella ja lopeta prosessi.*

- Käytetään SIGKILL signaalia lopettamaan Firefox

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/sigkill.jpg)

---

### *6.Käyttäen Iostat sovellusta katso kuinka paljon levylle on kirjoitettu yhteensä edellisen käynnistyksen jälkeen? Kuinka paljon dataa on luettu?*

- Dataa kijroitettu 584MB

- Dataa luettu 1324MB

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/iostat.jpg)

---

### *7. Mikä on ollut koneesi keskimääräinen ulospäin menevä liikenne?*

- 424.00 Bit/s

---

### *8. Kuinka paljon koneesi on ladannut dataa yhteensä*

- 2.13MByte

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/nload.jpg)

---

### *9. Mikä on koneesi lokaali IP-osoite?*

- 10.0.2.15

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/ipaddr.jpg)

---

### *10. Testaa toimiiko yhteys www.laurea.fi osoitteeseen. Mikä IP osoite vastaa osoitteesta?*

- 15 pakettia lähetetty, 13 vastaanotettu, 13,33 % hävikki, aika 14048ms (14.048 s)

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/ping.jpg)

---

### *11. Kuinka monta reititintä on matkalla virtuaalikoneestasi osoitteeseen www.laurea.fi linkittyy ulkoiselle sivustolle?*

![](https://github.com/PetteriHavia/E9955-3003-Linux-Johdatus/blob/main/src/Kuvat/traceroute.jpg)
