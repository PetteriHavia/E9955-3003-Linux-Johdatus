# 3\. Komentorivin käyttö

## 3.1: Komentorivin käyttö

A) cat /var/log/syslog | wc -l

  - Komennolla otetaan selvää syslog tiedoston rivimäärästä.

    Rivimäärä: 7 (Kokeiltu nimet.txt tiedostoon, johon lisätty 7 eri nimeä)

---

B) ls -l | sort  -r |  more

- Tämä komento listaa nykyisen polun tiedostot ja järjestää ne  päinvastaisessa järjestyksessä uusimmasta vanhimpaan, ja more komento putkitettuna helpottaa tulosten selaamista ja hakemista.

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/sort_more.jpg)

---

C) ls | head -3 | tail -1 > myoutput

- Tulostaa nykyisen polun komannen tiedostonimen

  Tulos: Downloads

---

## 2. Tiedostojen etsiminen

A) Miten etsisit locate -komennolla kaikkia tietokoneen mp3 -päätteisiä tiedostoja?

  locate *-mp3

---  

B) Miten etsisit find-komennolla tiedostoja, joita on muokattu tänään?

find . -mtime -1 -print

---

C) Miten etsisit tietokoneesta yli 10 Megatavun kokoisia tiedostoja?

find . -size +10

---

## 3. Tiedostojen pakkaaminen ja purkaminen

A) Pakkaa kotihakemistosi kaikkine alihakemistoineen tar.gz –pakettiin

tar cvfz pakattu.tar.gz *

---
B) Tee sama xz - pakkausohjelmalla, mutta älä sisällytä äsken luomaasi gz-pakettia mukaan.

tar cvfj pakattukaksi.tar.xz *

---

C) Vertaa tiedostojen kokoa, paljonko niillä on eroa?

XZ pakkaa GZ vertaillessa tiedoston kokoa paremmin ja melkein puolittaa pakatun tiedoston koon.

---

## 4. Tiedostojen ja hakemistojen oikeudet

A) Muuta tiedoston oikeuksia siten, että kaikilla on oikeus lukea ja kirjoittaa sitä. Esitä ratkaisu sekä kirjain- että numeromuotoista komentoa käyttäen.

chmod a=rw- pakattu.tar.gz

chmod 666 pakattu.tar.gz

---

B) Miten poistaisit kohdan a tiedostolta kirjoitusoikeudet kaikilta? Lukuoikeudet saavat jäädä. Esitä ratkaisu sekä kirjain- että numeromuotoista komentoa käyttäen.

chmod a-w pakattu.tar.gz

chmod 444 pakattu.tar.gz

---

C) Luo hakemisto ja anna kaikille lukuoikeus sinne, mutta vain omistajalla tulisi olla kirjoitus ja suoritusoikeus siihen.  Esitä ratkaisu sekä kirjain- että numeromuotoista komentoa käyttäen.

mkdir -m go-wx hakemisto

mkdir -m 744 hakemisto

---

# 3.2\. Komentorivityökaluja: GREP, SED, AWK

## 1. Grep

A) Millaisella kaavalla etsisit sosiaaliturvatunnuksia tekstimassan seasta? Huomaa, että sosiaaliturvatunnus voi olla joko muotoa DDMMYY-NNNK tai viiva tilalla voi olla kirjain.

egrep '[0-9]{6}[-]?[0-9]{3}[A-Z]'

---

B) Entä miten etsisit grepin avulla sähköpostiosoitteita kaikista hakemistossa olevista tiedostoista? Voit olettaa, että sähköpostiosoite sisältää vähintään etu- ja sukunimen, @- merkin sekä sukunimen ja maa/domaintunnuksen. Esim. matti.meikalainen@suomi.fi

grep '[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,6}'

Tulos: foo@demo.net bar.ba@test.co.uk mika@sci.fi mika.stenberg@laurea.fi

---

C) Entä vakiomuotoisia IP-osoitteita kaikista hakemistossa olevista tekstitiedostoista? Voit olettaa että IP osoite rakentuu neljästä numerosta, jotka ovat erotettu pisteellä toisistaan ja ovat arvoalueeltaan 0-255 seuraavasti. 1.0.0.0 tai 192.168.0.1 tai 255.255.255.255.

grep -oE ' ([0-9]{1,3}[\.]){3}[0-9]{1,3}'

Tulos: 255.255.255.0 127.0.0.1

---

D)Lataa verkosta ao. tiedosto wget-komennolla:
wget http://www.gutenberg.org/cache/epub/14152/pg14152.txt
Etsi tiedostosta kaikki sanat “asianajaja”, “poliisi”, “lääkäri”. Miten teet tämän yhdellä komennolla?

grep 'asianajaja\poliisi\|lääkäri' tiedosto.txt

---

E) Millä putkitetulla komennolla etsit edellä kuvatusta tiedostosta kaikki esiintymät sanoista “Tohtori Jekyll” ja lasket samalla montako kertaa ne esiintyvät?

grep -c 'Tohtori Jekyll' tiedosto.txt

Tulos: 5

---

F) Millä valitsimilla (parametrilla) saat grepin etsimään ne rivit, jotka EIVÄT sisällä sanoja “elämä”, “ei” ja “kuolema” sekä tulostamaan rivinumeron, jolta kyseiset sanat löytyvät?

grep -vE 'elämä|ei|kuolema' tiedosto.txt

---

## 2. AWK

A) Tulosta awk-työkalua käyttäen henkilöiden etunimi ja puhelinnumero välilyönnillä erotettuna. Puhelinnumeron tulisi olla suluissa.

awk -F ";" '{print $1,"("$4")"}' awktiedosto.txt

Tulos: Ezra A. Rogers (+91 5206512856)

---

B) Tulosta awk-työkalua käyttäen henkilöiden nimi, katuosoite sekä asuinmaa. Erota tiedot sarkaimellä (tab eli \t). Järjestä tulos aakkosjärjestykseen maan muun aakkostettuna. Vinkki: käytä putkitusta.

Sain tuloksen järjestykseen Nimen mukaan, mutta en maan vaikka kokeilin sort -k3

awk -F ";" '{print $1,$2,$3}' OFS="\t" awktiedosto.txt |sort -k1

---

C) Tekstitiedostossa säilytetään verkkosivulle tehdyn mielipidekyselyn tuloksia. Käytä AWKia ja laske kuinka moni on vastannut kyselyyn “Kyllä” ja Kuinka moni “Ei”. Tulosta summat ruudulle.

awk -F "," '{x+=$2}{y+=$3}END{print "Kyllä " x, "Ei " y}' awkkysely.txt

Tulos: Kyllä 5 Ei 2

---

D) Hae HY:n almanakkatoimiston sivulta (https://almanakka.helsinki.fi/fi/) tms. verkkosivuston etusivu wget -komennon avulla. Etsi siitä Grep-työkalun avulla nimipäiväsankarit. Käytä AWK tai SED -työkaluja tulostaaksesi sankarien nimet ja riisuaksesi HTML tägit.

--

## 3. SED

A) Etsi ja korvaa kaikki tehtävässä 1d lataamasi tiedostossa esiintyvät sanat “lääkäri” sanalla “puoskari”?

sed s/lääkäri/puoskari/g pg14152.txt

---

B) Miten poistaisit tekstitiedostosta kaikki rivit, joilla sana “maailma” esiintyy?

sed '/maailma/d' pg14152.txt

---

C) Miten etsit ja korvaat kaikki tiedostossa esiintyvät sanat kolmelle eri hakusanalle samalla kertaa?

--

---

D) Miten etsit sanaa “Enfield” tiedostosta ja lisäät kaikkien sen esiintymien ympärille lainausmerkit?

Sed s/Enfield/'”Enfield”'/g pg14152.txt

---


## 4. Tekstitiedostojen manipulointia

A) Luo kolme tiedostoa: ensimmäinen tiedosto sisältää kolmen henkilön nimet. Toinen tiedosto sisältää kolme puhelinnumeroa. Ja kolmas kolme osoitetta. Miten käyttäisit paste-komentoa näiden tiedostojen tietojen liittämiseksi yhteen tiedostoon.

paste nimia.txt osoite.txt puhelin.txt

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/paste.jpg)

---

B) Tutki aiemmin haettua tiedostoa pg14152.txt wc-komennolla. Montako riviä siinä on? Jaa tiedosto tämän jälkeen split - komennolla osiin. Montako riviä tulostiedostoissa on oletuksena?

wc -l pg14152.txt

Tulos: 3381 pg14152.txt

split pg14152.txt

Tulos: 7 uutta tiedostoa, jossa jokaisessa oletuksena 1000 riviä

---

c ) Jaa pg14152.txt split-komentoa käyttäen tiedostoihin, joissa on 500 riviä jokaisessa. Mitä valitsinta joudut käyttämään?

split -l 500 pg14152.txt

---

e) Miten poistaisit tiedostosta kaikki rivit rivien 200 ja 300:n välillä?

sed 200,300d pg14152.txt

---

# 3.3\. Komentorivin muokkaus ja ohjelmointi

##Komentorivin muokkausta

A) Komentorivikehotteen (promptin) tulisi näyttää käyttäjänimi sekä kellonaika?

export PS1=”\u \d ”

Tulos: osboxes Tue Apr 20

---

B) Komentorivikehotteen (promptin) tulisi näyttää tietokoneen nimi (hostname) sekä käytössä oleva
komentorivitulkki (Shell) sekä sen versio?

Export PS1=”\h \s \v”

Tulos: osboxes bash 5.0

---

C) Komentorivikehotteen (promptin) tulisi näyttää vakiotervehdys “Hei käyttäjännimi, mitä tehdään tänään?” valitsemallasi värillisellä tekstillä? (jossa käyttäjän nimi vaihtuu järjestelmässä kirjautuneena olevan käyttäjän nimellä)

export PS1="\[\e[36m\]Hei \[\e[m\]\[\e[36m\]\u\[\e[m\]\[\e[36m\],mitä tehdään tänään?\[\e[m\]"

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/variteksti.jpg)

---

##2 Luo omia alias-komentoja komentorivikehotteessa

A) luo alias “backup” joka pakkaa kotihakemistosi alihakemistoineen kansioon backup.zip

alias backup="tar -zcvpf pakattu.tar.gz /home/osboxes"

Tulos: Komennon annettua pakkaa kaikki ”home” kansion tiedostot yhteen ”pakattu” nimiseen kansioon

---

B) luo alias “poista” joka poistaa komennon perässä annetun tiedoston mutta kysyy siitä ensin
varmistuksen.

alias poista =”rm -i”

Tulos: poista tiedosto.txt > komento kysyy varmistusta yes/no -i avulla > yes ja tiedosto on poistunut

---

C) luo alias “juureen” joka siirtyy koko järjestelmän juurihakemistoon

alias juureen=”cd /”

---

D) luo alias “päivitä” joka lataa ja tarkistaa järjestelmäpäivitykset pääkäyttäjän oikeuksin

--

---

E) keksi joku näppärä alias, joka helpottaisi omaa tietokoneen käyttöäsi

Alias systeminfo=”free -m -l -t”

Tulos: Näyttää järjestelmän muistin, cpu ja gpu tiedot

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/alias.jpg)

---

##Komentoriviohjelmointi


A) Tee skripti joka kysyy sinulta nimesi ja ikäsi. Tämän jälkeen skripti tulostaa jonkin toteamuksen ikäsi perusteella, esim. “Terve Ville, olet yli 50 v.”

Scripti tiedosto

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/script1.jpg)

Tulos

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/script1x.jpg)

---

B) Tee skripti, joka kysyy käyttäjätunnuksen ja salasanan. Jos tunnus on “opiskelija” ja salasana “demo” tulostetaan “Oikein, tervetuloa!”. Muuten tulostetaan “Syötit väärän tunnuksen tai salasanan”.

Scripti tiedosto

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/script2.jpg)

Tulos

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/script2x.jpg)

---

C) Tee skripti nimeltä “yllapitoa”. Ajettaessa ohjelma kysyy “Suoritetaanko ylläpitotoimet?” Jos vastaus on myönteinen, ajetaan joukko järjestelmäkomentoja, kuten esim. käyttöjärjestelmän päivitys (sudo apt-get update ja sudo apt-get upgrade), locate-komennon tietokannan päivtys (sudo updatedb) sekä kotihakemiston tiedostojen pakkaaminen tar.gz -pakettiin ja kopiointi kansioon nimeltä “backups”. Voit keksiä myös itse haluamiasi operaatioita joukkoon. Kun kaikki nämä ovat suoritettu, ohjelma tulostaa “Valmista tuli”.

--

---

D) Tee arvauspeli joko pyytää käyttäjää syöttämään numeron. Jos numero on “7” ohjelma tulostaa onnittelut ja sen suoritus loppuu. Muuten käyttäjälle kerrotaan osuiko arvaus liian pieneksi/suureksi ja kysely jatkuu. Jos osaat voit arpoa satunnaisnumeron sekä pitää kirjaa arvausyrityksistä.


Scripti tiedostoa

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/arvaanumero.jpg)

Tulos

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/arvaanumerox.jpg)
