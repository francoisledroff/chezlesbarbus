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

### avant propos

"audit" on a ce mot dans notre abstract, mais en fait on veut pas vraiment faire un audit une fois tou developpé, on veut changer l'etat d'esprit du dev et de lops pour les sensbiliser à la sécu, on veut montrer plutot comme l'archi, la qa, le dev, l'ops sont partie prenante de la secu et comment la secu se fait "by design" tout au long du projet...
en gros le concept d'audit de secu est naze...

* a1: c'est le dev
* a2: c'est le sec

### mon appli jhipster

* a1: j'ai cette petite appli web intranet à faire, un truc pas trop big data, pas trop social, pas très hipster, mais comme je voulais me faire plaisir je suis parti sur un stack jhipster
* a2: c'est quoi jhipster ?
* a1: c'est un generateur d'appli web (à la appfuse) basé sur yeoman, au final tu as un stack plutot hispter, plutot recent avec du springboot pour la partie serveur et du angularjs pour le partie cliente
jhipster te donne quelque choix, voici les miens:

    {
    "generator-jhipster": {
    "baseName": "petiteappli",
    "packageName": "com.devoxx.petiteappli",
    "packageFolder": "com/devoxx/petiteappli",
    "authenticationType": "token",
    "hibernateCache": "no",
    "clusteredHttpSession": "no",
    "websocket": "no",
    "databaseType": "nosql",
    "devDatabaseType": "mongodb",
    "prodDatabaseType": "mongodb",
    "useCompass": false,
    "buildTool": "maven",
    "frontendBuilder": "gulp",
    "javaVersion": "7"
    }
    }

* a2: ok donc je vois des choix majeurs ici, t'es parti sur du oauth2 et du mongodb


### just an internal app

* a1: c'est juste une petite appli intranet
* a2: assume there is a breach, never assume you are safe, architect with "assumed breach" mindset

=> ça serait de trouvé un exemple de hack/exploit sur une app "interne" déployé sur un coin de table

### je suis dans le VPN 

* a2: je vois que par defaut, tout passe en clair entre ton mongo et ton serveur d'app
* a1: je suis en intranet
* a2: peu importe, la question à laquelle tu dois repondre c'est tes donnés sont t-elles confidentielles, que peut-il arriver si elle sont compromises
* a1: données rh et finance, ça pourrait faire pas mal de bruit si on les trouvait sur le web
* a2: tu peux pas laisser ca en clair
* a1: je suis en intranet
* a2: http://www.arnoldit.com/articles/10intranetSecAug2002.htm l'intranet n'est plus safe

### Mongo SSL authentication 

la je peux faire un slide et fournir un peu de code
car en fait la x509 authentication n'est pas fourni par defaut dans spring data mongo, j'ai du la coder dans mon appli

### Password

* a2: ah je vois que par défaut, jhipster a sa propre base de donnees d'utilisateur
* a1: oui mais I enforced strong password policies
* a2 : passwords are bad. 100% of attacks in 2014 involve stolen credentials. avoid dealing with passwords.

### t'as pas un IDP dans ton intranet

* a2: mais dis des utilisateurs vont devoir creer un nouveau password juste pour ton app
* a1: oui
* a2: non tu ne veux pas faire ça :


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

* a2: t'as pas un IDP dans ton intranet ?
* a1: si basé sur saml avec du 2FA

### 2 FA and UX


* a2: vas-y qu'est ce que t'attends, put 2fa in place
* a1: bad ux though, https://twitter.com/michaelneale/status/568279010968383488

1. App requires 2FA login.
2. get phone from pants
3. Distracted by 100s of notifications on it
4. Back to computer. Repeat.


* a2: je crois qu'ici tu pourrais utiliser oauth2, une fois l'utilisatuer authentifié
* a1 oui c'est une bonne idée :

et la je peux montrer encore du code modifié de jhispter ou l'authentication est deporté sur un idp saml et ensuite seuleuemtn un oauth token (et un refresh token) est echangé avec le front-end javascript

resultat tu te tappes le 2fa une fois et ensuite a moins de quitter l'app pendant plus de 30 jours tu le referas pas.

on peux montrer les echanges avec des jolies sequence diagram
on peux aussi montrer que l'on peut revoker les tokens pour les stolen device/laptop/desktop
j;ai du code jhipster et une interface pour ca 

### avoid Brute force attack

(pour tout ce que tu évoques ci dessous, ça peut être fait dans app ou en externe, donc je
propose que tu évoques les solutions "in-app" et moi les solutions infra)

rate limiting => safe2ban
password strength => reverse
captchas => AFAIK no out app option

hsm protect private key
certificate segregated by group
hsm will make offline attacks impossible

this will buy you time to detect an attack and react accordingly

 => useless if no IDS in place or at least monitoring !!!






### just a web app

http://www.ivizsecurity.com/blog/penetration-testing/web-application-vulnerability-statistics-of-2012/

* 99% of web applications have at least 1 vulnerability
* 82% of web applications have at least 1 High/Critical Vulnerability
* 90% of hacking incidents are not reported publicly

=> là on pourrait aussi évoquer PMD/Findbugs pour justement mettre en place des contrôles/analyses
de sécurité.

### I made exploits harders

* a1 : I hide headers info to avoid easy exploit : Wappalyzer screenshot
* a2 : exploits is not such a big deal anymore

### never assume your source code is safe

segregate your secrets from your source code
search in github.com for password, secret, key


a $2.375 amazon mistake
http://www.devfactor.net/2014/12/30/2375-amazon-mistake/

et hop la on peut une recherche dans jhipster on y trouveras quelques secrets

we have oauth clientid and secret in jhipster
la encore je peux montrer comment on peut generer le oauth client et le oauth secret à la volée seuleument une fois l'authentication saml reussi


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

=> excellent !

### safer in the cloud

a 10 years old server in your data center is much more vulnerable than a fresh server in the cloud

a 10 years old server, imagine

* accumulated rot
* configuration shift
* quaterly security review ? this clash with continous delivery

a typical aws server last a few days

=> là je peux expliquer le cas de Netflix où justement, aucun serveur en prod ne dure que qql
jours... plus leur approche "Choas Monkey" qui est phénoménale !
http://techblog.netflix.com/2012/07/chaos-monkey-released-into-wild.html

### Avoid security scan false positive

false positive overload : http://infosecnirvana.com/false-positive-in-a-siem/

avoid false positive:

checksum on sensitive directory only
file integrity monitoring tool
http://www.cloudpassage.com/


=> semble être le bon endroit pour évoquer le rôle du Firewall et surtout ses limites, et leur //
avec la ligne Maginot. Du coup, j'évoquerais bien aussi le filtrage applicative et les reverse
proxy.

splunk enterprise security analytics

### Make your Linux *really* secure - SELinux

(je ne sais pas si c'est la meilleur place pour en parler, mais à défaut, enchainer là dessus après
avoir décrits les limites des FW semble pertinent).

limite le comportememt des logiciels

Aller plus loin ? Utiliser Docker et/ou OpenShift pour isoler les processus / apps hostés sur le
même serveur

### CI and security

automated security review based on API
update tomcat / appserver
    => sans faire de la pub à mort pour Red Hat, on peut souligner ici la valeur ajouté d'avoir un produit supporté.
update OS
run test scan

https://www.qualys.com/
http://evident.io/

### secure build env

adhoc short lived build machine
vlan segregation

make swing peeps harders:  disable ping sweeps on a network, administrators can block ICMP ECHO requests from outside sources.

=> bof, moi je suis contre les stratégie consiste à fermer/bloquer les trucs. Je préfère surveiller
que le traffique est sain et correspond aux attentes.

voila un paquet de liens et idees en vrac:
-------

### REST API


* rate limits
* header validation
* conditional requests

=> IMHO, Un RP en frontal, faisant du nettoyage de requêtes + mise en place de bannissement si
nécessaire, me semble être essentiel.

### exploits

not that bif of a deal nowadays
sandboxing reduces vulnerabilities
better application server
harders to implement an exploit
exploit don't last long
you leave a trail

### passwords

100% of attacks in 2014 involve stolen credentials

java
---

https://twitter.com/Developpez/status/560389865003425792
Sécurité : Java serait le programme le plus exposé aux attaques, suivi par QuickTime, Adobe Reader, VLC et .Ne... http://bit.ly/1zaB89X

Sécurisé Java => SecurityManager !

=> On peut aussi mentioner le hack de Prados où il a utiliser un service qui permettait d'uploader
sa propre XSLT et qui lui a permis d'exécuter des commandes sur le système. Typiquement, impossible
avec SELinux +/- SecurityManager.

=> Idée de conclusion

On pourrait finir en disant qu'après DevOps, il faudrait un DevSec - utilisant le même approche,
impliquant les gens de la sécurité et les dévs. Ne plus laisser les dévs ignorer la sécurité, mais
ne plus laisser les experts sécu considéré les apps comme des "boites noires". Le gros des
faiblesses de sécurité sont aujourd'hui dans les apps plus que l'infrastructure, pour sécuriser un
système, les deux profils doivent s'assurer coté à coté et (par exemple) rédiger ensemble les
polices de sécurité du SecurityManager et les règles de filtrages applicatives.

### misc

=> Pas mal de bon truc là dessous, il faudrait au moins parler de Java (donc j'ai remonté la
section juste au dessus) et garder le reste pour "en rajouter" si nécessaire.

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

-> le spoof de Git Hub est intéressant, car c'est un bon exemple d'exploit "social". On peut
imaginer une PR sur un projet prétendant venir de XXX insérant une faille... Je pense qu'il faut
qu'on mentionne que le "hack" social reste une des principales failles de sécurité.


