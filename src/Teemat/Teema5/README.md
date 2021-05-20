# 5\. Tietoturva

## 5.2 Linuxin kovennus


### *Tehtävä A: Palomuurin asennus ja säätö*

### *1. Asenna Linuxiisi UFW sekä GUFW -palomuurisovellukset. Käynnistä palomuuri ja katso sen status.*

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/firewallstatus.jpg)

---

### *2. Selvitä millaisia sääntöjä palomuurissasi on oletuksena?*

- Tuleva liikenne on kielletty ja lähtevä sallittu oletuksena

---

### *3. Salli kaikki http ja https liikenne koneelle.*

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/http.jpg)

---

### *4. Kiellä kaikki saapuva ftp liikenne koneelle*

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/ftp.jpg)

---

### *5. Kiellä kaikki ulospäin lähtevä liikenne koneelle porttiin 25*

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/port25.jpg)

---

### *6. Kiellä kaikki liikenne koneelle IP osoitteesta 15.15.15.51*

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/ip.jpg)

---

## Tehtävä B: Linuxin kovennus

### *Asenna Linuxiin ClamAV antivirus-ohjelma. Skannaa sillä oma Linux-asennuksesi*

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/clamscan.jpg)

### *-	Tee myös kovennuslistan vaiheet 1 ja 3.*

- Päivitykset  update ja upgrade

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/update.jpg)

---

- Asennetut sovellukset. Haetaan ne esiin komennolla dpkg -l. Listasta en lähtenyt poistamaan mitään, mutta poistaminen tapahtuu komennolla apt-get remove [paketti]

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/sovellukset.jpg)

---

### *Valitse listasta lisäksi 2 haluamaasi kovennusta ja tee ne järjestelmääsi.*

- Lynis sovelluksen ajo

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/lynis.jpg)

- Verkkoliikennettä kuuntelevien palveluiden tarkistus netstat komennon avulla

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/netstat.jpg)

---

## 5.3 Salasanojen murtaminen

### *TEHTÄVÄ  A: SALASANOJEN MURTAMINEN RAAKAA LASKENTAA KÄYTTÄEN*

1. Luo Linuxiin kolme uutta käyttäjää aiemmin opitulla tavalla. Anna käyttäjille nimeksi: heikko, keski ja vahva. Nimet kuvaavat salasanojen vahvuutta.

Anna käyttäjälle heikko salasanaksi kolmen kirjaimen mittainen salasana, esim. "hei".

Anna käyttäjälle keski salasanaksi hieman pidempi salasana jossa on jo iso kirjain ja numero, esim. "Heik5".

Anna käyttäjälle "vahva" salasanaksi itse keksimäsi isoista ja pienistä kirjaimista, numeroista ja erikoismerkeistä koostuva salasana

Kokeile lopuksi murtaa äsken luomasi käyttäjien salasanat

- Tehtävä suoritettu selaimesssa sijaitsevan Kali linux palvelun kautta virtuaalisesti `https://www.onworks.net/os-distributions/debian-based/free-kali-linux-online`

- Luodaan käyttäjäy komentorivin kautta

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/kayttajat.jpg)

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/heikko.jpg)

- Heikko käyttäjän salasana murtui muutamassa sekunnissa, kun taas keski ja vahva salasanat tuntuivat vievän ikuisuuden. Kun ohjelma oli käynyt läpi oman wordlist tiedostonsa joka ei tuottanut tulosta se siirtyi sen jälkeen ASCII "brute-force" taktiikoihin.

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/heikkopass.jpg)

---

## TEHTÄVÄ B: SALASANOJEN MURTAMINEN SANAKIRJOJEN JA SATEENKAATITAULUKOIDEN AVULLA

1. Kokeile selvittää seuraavat salasanat sateenkaaritaulujen avulla.

`ab87d24bdc7452e55738deb5f868e1f16dea5ace`
`01f7b6a103603487e5ffd126ade782d2bcdd8922`
`08ef1bdfe3096a52749aaa74f1a12cfc04d54e80`
`e38ad214943daad1d64c102faec29de4afe9da3d`
`01b307acba4f54f55aafc33bb06bbbf6ca803e9a`
`55be6dcac991480ba75e05bd72065450af15248e`
`56d9e9f2b6c560bb23e2ff136c24e3fb7e077e7c`

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/hashcracker.jpg)

- Ohjelma suoritti toimintansa nopeasti ja onnistui murtamaan 5/7 salasanaa.
---

2. Koita sitten murtaa seuraavat verkossa kiertävät suomalaiset salasanat.


`055b5174cd20812d6188bde80595ef89`
`cf4c362230c6801a4a5878752e75d7c7`
`4acbf1ae29541e0db453b607d618ae1c`
`106afb67b6819ea3662f79483f5e9371`
`20d9de79fec9848e259a4f92d7219fc1`
`70dca0f15551b30000daffbf1b24d92e`
`2502986f114ceb52c125f3b9f891f728`

- Kokeilin Kali Linuxin tarjoamaa Johnny Gui versiota salasanojen murtamiseen. Ohjelma mursi 6/7 salasanaa listan avulla ja jäi arvuuttelemaan viimeistä salasanaa.

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/johnny.jpg)

- Hashcrack arvasi heti listan avulla kaikki salasanat.

![](https://raw.githubusercontent.com/PetteriHavia/E9955-3003-Linux-Johdatus/main/src/Kuvat/hashcrackerSuomi.jpg)
