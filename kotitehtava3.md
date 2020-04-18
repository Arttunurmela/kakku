## Kotitehtävä 3, Palvelinten hallinta. Arttu Nurmela

a) Kohdassa asensimme koneelle typora-editorin, jolla pystyy kirjoittamaan .md tiedostoja. Typora on selkeä ja helppokäyttöinen sovellus, joka muistuttaa paljon windowsin- omia tekstinkäsittelyohjelmia.

Typoran asennusohjeet löytyvät osoitteessa: https://typora.io/#linux

b) **git log**- komento näyttää loki-tiedoston, joka kertoo tekemistäni muutoksista. (Esim luodut tiedostot)

**git diff**- komento näyttää tiedostojen sisällä tehdyt muutokset.

**git blame**- komento kertoo kuka, milloin ja miksi teki muutoksia tiedostoon, riviin yms. 

c) **git reset --hard** - Tein kohtitehtävään tahallaan virheen ja tallensin tekstitiedoston. Komento poisti 'virheelliset' muutokset ja haki edellisin tallennetun version (joka on työnnetty githubiin), jossa ongelmaa ei ollut. 

f) Uutena moduulina asensin fail2ban ohjelman, joka voi blockata halutun ip-osoitteen määritetyksi ajaksi.

Asennus alkoi päivityksellä **sudo apt-get update**

Seuraavaksi asensin fail2banin komennolla: **sudo apt-get install -y fail2ban**

Sen jälkeen siirryttiin hakemistoon **/etc/fail2ban** josta kopioin tiedoston 

**jail.conf** ja nimesin sen nimellä **jail.local** , tämä siitä syystä, että päivitys 

muuttaa jail.conffin tiedostoja.

Seuraavaksi loin polkuun **srv/salt/** uuden kansion fail2ban, jonka sisään kopioin 

**jail.local** tiedoston.

Sitten loin **fail2ban.sls** tiedoston, johon kirjoitin sisään seuraavat tiedot:

fail2ban:
  pkg.installed

/etc/fail2ban/jail.local:

  file.managed:  

-source: salt://fail2ban/jail.conf

fail2banservice:

service.running:

-name:

-file: //etc/fail2ban/jail.local

(välilyönnit eivät täsmää oikein)

Tämän jälkeen komento **sudo salt '*' state.apply fail2ban**

Fail2ban toimii ja asentuu oikein!

Lähteet:

Terokarvinen.com materiaali sekä hannukankkunen.wordpress.com