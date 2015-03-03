Chez les barbus: Java, sécurité et DevOps
=========================================

abstract 1: Java & Sécurité
---------------------------

Titre: Les Barbus contre les Barbares ???

C'est un audit de sécurité participatif que Francois et Romain vous propose dans cette session.
Leur présentation forcement partielle et partiale, puisque exposée en moins d'une heure, sera illustrée par la sécurisation d'une application web construite sur une stack Linux-Java-JHipster.
 
Y seront exposées et débattues, de nombreuses mesures et techniques de sécurité couvrant l'ensemble du cycle de vie du développement de logiciel:
 
* la sécurisation du poste et des outils de travail
* la sécurisation de la chaine d'intégration continue
* la configuration automatisée des serveurs et la gestion des secrets
* la sécurisation de la jvm et l'utilisation du SecurityManager
* les bonnes pratiques et outils contre les attaques web les plus répandues
* la gestion d'identité, d'authentication et d'autorisation avec la mise en oeuvre de SAML et oAuth2
 
Le but: vous sensibiliser, vous armer contre les cyber-attaques des hordes barbares, vous développeurs Java, barbus ou pas.

------


Développeurs Java seniors, François et Romain ont découvert le monde des opérations depuis
maintenant plusieurs années. C'est par un nouveau retour d'expériences croisées sur la thématique de
la sécurité des applicatifs JEE ou WebApp, En sécurisant, une application JHipster, ils démo

Illustrée par la sécurisation d'une application JHipster, la présentation, construite pour un être
un échange avec les auditeurs, couvrira les nombreuses problématiques (du SecurityManager à la
gestion d'identité avec OAuth ou SAML), leurs solutions - et leurs limites. Mais aussi, le pendant
DevOps de la sécurité (Comment la lier à intégration continue et au déploiement continue ?).
Participatif, cette conférence vise aussi à receuillir de nombreux retours d'expériences et discute
des points "manquants à l'appel"...

Plan
1. Java / Security
2. Appli demo sécurisé
3. thèmes couverts
4. DevOps/CD
5. échanges de bonnes pratiques

tags
----

DevOps
Continous Delivery
Java
Linux
Security


Content:

* SpringSecurity
* Integration SAML en entreprise / keycloak
* Pratiques, gestion de password de dev/prod, 2 factor auth
* KeyCloak
* Common Criteria ... Security
* Security Manager / SE Linux + Firewall
* Sortez couvert (HTTPs/2 factor auth)

draft content
============
on joue tour a tous soit l'acteur 1 (a1) soit l'acteur 2 (a2)
plan
-----

### just an internal app

* a1: c'est juste une petite appli intranet
* a2: assume there is a breach, never assume you are safe, architect with "assumed breach" mindset

### just a web app

http://www.ivizsecurity.com/blog/penetration-testing/web-application-vulnerability-statistics-of-2012/

* 99% of web applications have at least 1 vulnerability
* 82% of web applications have at least 1 High/Critical Vulnerability
* 90% of hacking incidents are not reported publicly

### I made exploits harders

* a1 : I hide headers info to avoid easy exploit : Wappalyzer screenshot
* a2 : exploits is not such a big deal anymore 

### I enforced strong password policies

* a1 : strong password policies
* a2 : passwords are bad. 100% of attacks in 2014 involve stolen credentials. avoid dealing with passwords.

we have so may passwords to deal with, we reused them
sony password reused at yahoo: http://www.troyhunt.com/2012/07/what-do-sony-and-yahoo-have-in-common.html

social engineering hack: the wired journalist hack
plus simple: the cartoon with first pet name

You can name her whatever you like but be sure it’s something you can remember. You’ll be using it as a security question answer for the rest of your life

http://positivedoggie.com/you-can-name-her-whatever-you-like-but/

Paris Hilton pet name security hack
http://www.macdevcenter.com/pub/a/mac/2005/01/01/paris.html
http://content5.promiflash.de/article-images/w500/paris-hilton-haelt-zwergspitz-prince-hilton-auf-dem-arm.jpg

http://idtheftcenter.org/

### avoid Brute force attack


rate limiting
password strength
captchas

hsm protect private key
certificate segregated by group
hsm will make offline attacks impossible

this will buy you time to detect an attack and react accordingly
 
 
### 2 FA
 
 
* a2: put 2fa in place.
* a1: bad ux though, https://twitter.com/michaelneale/status/568279010968383488 

1. App requires 2FA login. 
2. get phone from pants 
3. Distracted by 100s of notifications on it 
4. Back to computer. Repeat. 


### never assume your source code is safe

segregate your secrets from your source code
search in github.com for password, secret, key

we have oauth clientid and secret in jhipster

a $2.375 amazon mistake
http://www.devfactor.net/2014/12/30/2375-amazon-mistake/

sepration of duties
rotate account information



### never assume the system you are talking to is safe

siemens stuxnet credentials in the source code
http://en.wikipedia.org/wiki/Stuxnet

### I integrate with this API

keep your secret safe
use vault + configuration
analytics on password request
leave audit trail
avoiding downtime when password/key change

### Operations and security

ops is about
* consentement
* safety
* knowledge
* freedom

it will fail, stability is a myth
* firemen train for fire
* fireman is not afraid of fire


### safer in the cloud

a 10 years old server in your data center is much more vulnerable than a fresh server in the cloud


a 10 years old server, imagine 

* accumulated rot
* configuration shift
* quaterly security review ? this clash with continous delivery

a typical aws server last a few days

### Avoid security scan false positive

false positive overload : http://infosecnirvana.com/false-positive-in-a-siem/

avoid false positive:

checksum on sensitive directory only
file integrity monitoring tool
http://www.cloudpassage.com/


splunk enterprise security analytics




### CI and security

automated security review based on API
update tomcat
update OS
run test scan 

https://www.qualys.com/
http://evident.io/


### secure build env

adhoc short lived build machine
vlan segregation


make swing peeps harders:  disable ping sweeps on a network, administrators can block ICMP ECHO requests from outside sources.



voila un paquet de liens et idees en vrac:
-------

### REST API


* rate limits
* header validation
* conditional requests

### exploits

not that bif of a deal nowadays
sandboxing reduces vulnerabilities
better application server
harders to implement an exploit
exploit don't last long
you leave a trail

### passwords

100% of attacks in 2014 involve stolen credentials


### never assume your source code is safe

segregate your secrets from your source code

### misc


http://www.slideshare.net/mongodb/securing-mongo-db-mongodc-2014-nosig

http://www.allanbank.com/blog/security/tls/x.509/2014/10/13/tls-x509-and-mongodb/



update your linux (ghost) we you have docker ! fun !

http://googlecloudplatform.blogspot.fr/2015/02/using-google-cloud-platform-for.html

gemalto hacked : https://firstlook.org/theintercept/2015/02/19/great-sim-heist


vous avez été espionné?
http://www.numerama.com/magazine/32243-avez-vous-ete-espionne-par-la-nsa-voici-une-chance-de-le-savoir.html


twitter entries 
=====

UX :
----
https://twitter.com/michaelneale/status/568279010968383488 

1. App requires 2FA login. 
2. get phone from pants 
3. Distracted by 100s of notifications on it 
4. Back to computer. Repeat. 

secret management
----
https://twitter.com/jtimberman/status/568124542553423872
Managing secrets: still the hardest problem in operations.

jce chef recipe
chef-vault


documentation
----
https://twitter.com/codinghorror/status/567434195987738624
The best reaction to "this is confusing, where are the docs" is to rewrite the feature to make it less confusing, not write more docs.

mongo leak
---
https://twitter.com/unix_root/status/565906945488748544
40,000 unprotected MongoDB databases, 8 million telecommunication customer records exposed http://thehackernews.com/2015/02/mongodb-database-hacking.html 

java
---
https://twitter.com/Developpez/status/560389865003425792
Sécurité : Java serait le programme le plus exposé aux attaques, suivi par QuickTime, Adobe Reader, VLC et .Ne... http://bit.ly/1zaB89X 

git and jenkins , chef, vagrant exploits
---
https://twitter.com/morlhon/status/554899543150850048
A must-read  : @paulgreg: interesting slide on security of your webapp "DevOoops"  by @carnal0wnage #devops #hacking http://www.slideshare.net/chrisgates/lascon-2014-devooops …”



