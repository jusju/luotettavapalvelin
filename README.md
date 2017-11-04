# Luotettava ja helpon deployn palvelin

Palvelimen voi luoda digitalocean ympäristöön, kuten joillain kursseilla opetetaan. Nykyään myös ovh on suosittu.

Repositoryssäni ownserver on dokumentoitu palvelimen pystytys.

Luotettavuuden vuoksi olisi hyvä tehdä esimerkiksi roottina tai sudolla seuraava komento:

systemctl tomcat8 enable

Tämä takaa, että tomcat käynnistyy rebootin yhteydessä.

Oman backendin vieminen palvelimelle kannattaa tehdä Maven command line taskina, jotta paketin rakentaminen ja siirto on vaivatonta.




