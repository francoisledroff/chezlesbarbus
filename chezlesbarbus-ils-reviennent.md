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





### HSM (@FLD, RPE doit lire car là, il connait pas, peut être parlant et ça fera une séquence où tu me fermes la geule et tu me dis 'hey pas que les barbus qui s'y connaissent ;)")

hsm protect private key, proprio non ?
certificate segregated by group
hsm will make offline attacks impossible

this will buy you time to detect an attack and react accordingly

 => useless if no IDS in place or at least monitoring !!!

RPE: Je ne sais pas si le HSM ne serait pas à dropper si on a trop de contenu... my 2c


### never assume your source code is safe

FLD: Bon après tout ça, au final, je peux laisser tomber mon audit, non ?
RPE: Non, pas vraiment, mais plutôt qu'auditer l'appli, maintenant, avec les usuels test de sécurité (qu'elle devrait passer maintenant), tu devrais ton concentrer sur le code. On doit jamais assumer qu'un code source est sûr.

FLD: Tu veux dire pour trouver des failles ou des contournemt ? (@FLD: on peut peut être parler du hack de Prados là, où il a exploiter des XLST)

### Avoid security scan false positive

false positive overload : http://infosecnirvana.com/false-positive-in-a-siem/

avoid false positive:

file integrity monitoring tool
http://www.cloudpassage.com/

splunk enterprise security analytics


plan
-----

* ma petit web app intranet
* d'interne à externe
* bienvenu sur le cloud
* CI & Build, tout un monde de faille à exploiter




19 mars
=======================



intro
====














tu m'as hacké et alors ?
---

FLD: bon, on est bon là ?

RPE: ben c'est dur à dire, on peut jamais être sûr, mais disons que maintenant, ce qui serait sympa, c'est de protéger les copains de nos conneries. Bref si tu as laissé un trou dans ton appli, que au moins, seule elle soit compromise.

FLD: Comment ça ?

RPE: Ben si un mec à trouver un exploit sur ton app, il peut accéder à ses données, mais aussi éventuellement, modifier son comportement. Par exemple, lui faire envoyer des mails ("Merci à l'infrastructure Adobe d'avoir participé "pro bono" à la diffusion de mes spams !), effacer des fichiers ou récupérer des données d'une autre app colocalisé avec l'appli.

FLD: Et tu peux faire qqlchose contre ça ?

RPE: Ouais, bien sûr, c'est un peu la même logique qu'avec le RP. En gros, tu défini le comportement "normal" de ton appli et tu banni tout le reste. Tu peux le même faire à deux niveaux. D'abord, sur le JVM avec le Security Manager, que tout le monde connait ici (regard à l'assistance) car aucun expert ou dev Java tourne d'applicatif sans, hein ? ;)

RPE: Et tu peux aussi le faire au niveau système avec SE LInux. En gros, les deux technos ont la même fonctionnalité et voilà comment elles marchent

1,2 slides sur ce truc, avec des petits exemples de config

FLD: apres la super science , plus simple checksum on sensitive directory only


It will fail
----

ops is about
* consentement
* safety
* knowledge
* freedom

=> consent, safety, freedom, sounds like a trailer for 50 Shades of Grey :p

it will fail, stability is a myth
* firemen train for fire
* fireman is not afraid of fire

https://www.techn0polis.net/wp-content/uploads/2015/01/security.png



a ce propos

dans jhipster tu as une page d'audit de secu.

nous en plus, on a prévu le coup si un des nos utilisateurs perd son laptop, on reset son token

=> excellent !





CONCLUSION
--------

it will fail, stability is a myth
* firemen train for fire
* fireman is not afraid of fire

https://www.techn0polis.net/wp-content/uploads/2015/01/security.png

keep your secret safe
use vault + configuration
analytics on password request
leave audit trail
avoiding downtime when password/key change


**The three goals of security are confidentiality, integrity and availability**. Intranet security must deliver integrity and availability. Intranets exist to make information available to colleagues. Nevertheless, confidentiality is an issue. Each job function and person holding that job is given a level of access appropriate to his or her role. Intranets are often less secure than information technology professionals and managers realize

http://www.arnoldit.com/articles/10intranetSecAug2002.htm


### exploit ? not that bif of a deal nowadays

* sandboxing reduces vulnerabilities
* better application server
* harders to implement an exploit
* exploit don't last long
* you leave a trail

On pourrait finir en disant qu'après DevOps, il faudrait un DevSec - utilisant le même approche,
impliquant les gens de la sécurité et les dévs. Ne plus laisser les dévs ignorer la sécurité, mais
ne plus laisser les experts sécu considéré les apps comme des "boites noires". Le gros des
faiblesses de sécurité sont aujourd'hui dans les apps plus que l'infrastructure, pour sécuriser un
système, les deux profils doivent s'assurer coté à coté et (par exemple) rédiger ensemble les
polices de sécurité du SecurityManager et les règles de filtrages applicatives.


### misc / unused

update your linux (ghost) we you have docker ! fun !
http://googlecloudplatform.blogspot.fr/2015/02/using-google-cloud-platform-for.html

gemalto hacked : https://firstlook.org/theintercept/2015/02/19/great-sim-heist

vous avez été espionné?
http://www.numerama.com/magazine/32243-avez-vous-ete-espionne-par-la-nsa-voici-une-chance-de-le-savoir.html

https://twitter.com/codinghorror/status/567434195987738624
The best reaction to "this is confusing, where are the docs" is to rewrite the feature to make it less confusing, not write more docs.

* a1 : I hide headers info to avoid easy exploit : Wappalyzer screenshot
* a2 : exploits is not such a big deal anymore

conc