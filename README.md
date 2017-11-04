# Luotettava ja helpon deployn palvelin

Palvelimen voi luoda digitalocean ympäristöön, kuten joillain kursseilla opetetaan. Nykyään myös ovh on suosittu. Tämä ohje on erityisen hyödyllinen lähinnä esimerkiksi mobiilin backendin kehittämisessä.

Repositoryssäni ownserver on dokumentoitu palvelimen pystytys.

Luotettavuuden vuoksi olisi hyvä tehdä esimerkiksi roottina tai sudolla seuraava komento:

systemctl tomcat8 enable

Tämä takaa, että tomcat käynnistyy rebootin yhteydessä.

Oman backendin vieminen palvelimelle kannattaa tehdä Maven command line taskina, jotta paketin rakentaminen ja siirto on vaivatonta.

```
Tarvitset:
- tomcat8
- jdk:n
- maven ohjelmiston
## Vaihe 1 - konfiguroi palvelimen tomcat
```

Lisää käyttäjä rooleilla manager-gui ja manager-script.

Tiedosto:
%TOMCAT8_PATH%/conf/tomcat-users.xml

```xml
<?xml version='1.0' encoding='utf-8'?>
<tomcat-users>

	<role rolename="manager-gui"/>
	<role rolename="manager-script"/>
	<user username="admin" password="password" roles="manager-gui,manager-script" />

</tomcat-users>
```

## Vaihe 2 - konfiguroi clientin maven
%MAVEN_PATH%/conf/settings.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<settings ...>
	<servers>

		<server>
			<id>TomcatServer</id>
			<username>admin</username>
			<password>password</password>
		</server>

	</servers>
</settings>
```

## Vaihe 3 pom.xml muutos plugin

pom.xml
```xml
<plugin>
	<groupId>org.apache.tomcat.maven</groupId>
	<artifactId>tomcat7-maven-plugin</artifactId>
	<version>2.2</version>
	<configuration>
		<url>http://localhost:8080/manager/text</url>
		<server>TomcatServer</server>
		<path>/mkyongWebApp</path>
	</configuration>
</plugin>




