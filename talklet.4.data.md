`Talket 4` Data and Encryption
=======

`slide-23` Classification
---

`RPE` commencons par évaluer les risques, classifions tes données. Tes données peuvent être confidentielles.

`FLD` contrairement à un app store, un site d'ecommerce ou un backend uber, je ne stocke aucun moyen de paiement, je ne risque donc pas les voir fuiter vers le dark web.

Mais on prévois un beau mashup de données, c'est un "employee productivity tool", à travers mon app vont transiter des données que je ne voudrait pas voir fuiter, comme

* l'adresse, le numero telephone des employés
* l'ensemble de l'arbre organisationel RH
* les salaires
* les congés
* les notes de frais 
* des infos sur les deals en cours   


`RPE` Bref t'as des données interne, du PII, du confidential et restricted 

`FLD`  on a plutot intérêt à faire du bon boulot. 

`RPE` Note que les "barbus" ou les techos en général trouvent ce genre de classification / méthodologie souvent un peu "bullshit", ça fait juste des jolies tableaux ou rapports pour le management mais "ça ne me sert à rien". 

`FLD` En fait, ça permet surtout de faire comprendre au management qu'il y a un problème, dans un format qu'ils peuvent comprendre et réutiliser. En outre, si vous êtes coté management et que vous soupçonnez que vos devs ont été un peu trop "libérale" avec la sécu, faire ce genre d'inventaire est aussi un bon moyen de leur faire réaliser le problème. Bref, comme tout méthodo ou approche formelle, c'est certainement pas une solution miracle, mais plutôt à outil à utiliser à bonne escient.

`RPE` La conclusion, va falloir chiffrer la majorité du flux et de la persistence de ces données de bout en bout, qu'est ce que tu as prévu pour ça ?



`slide-24` Chiffrer le front
-------

`FLD` de bout en bout, commencons alors par le front, on prévoit évidemment de tout servir en https

`RPE` SSL c'est secure, mais faire ça correctement c'est tout un art. 

`FLD` Et ça demande une surveillance et une veille techno constante, même les plus grands doivent gérer des situations de crise, vols de certificats, ou la propagation de certificat qu'ils non pas authorisés mais qui sont trustés par la plupart des navigateurs

`RPE` et souvenez vous, avec suffisamment de temps et de ressources, n'importe quelle chiffrement peut-etre cassé .

`FLD` dernier conseil avant de passer à la suite, demandez à vos équipes de sécu, de scannez vous serveur https pour détecter les éventuelles vulnérabilités et obsolesances 

`RPE` ok, pour le front, admettons qu'on soit bon, regardons le back.

`slide-24` Chiffrer le back
-------

`RPE` Dis, avant mmême de parler chiffrement, Contrairement à ces 40 000 db mongo en prod sur le web et non protégées, j'imagine que tu as mis en place un minimum de sécu ? 

`FLD` Oui on a même du diverger du code généré par Jhipster pour assurer le niveau de sécu requise,

En effet JHipster utilise un outil open source appelé mongeez qui  permet de gérer les modifications de vos documents mongo et propager ces changements en synchronisation avec votre code change lors des déploiements. 

Cet outil a besoin des droits d'admin sur la base, c'est impossible à utiliser en prod pour nous, 
https://github.com/jhipster/generator-jhipster/issues/733

`RPE` ok donc t'as mis en place une authentication et un ACL bien. Mais t'as chiffrer les données qui passe sur le cable entre ton serveur d'app et Mongo ? ou elle passe en clair ?

`FLD` on l'a fait oui, mais ce fut épique, par défaut le support n'est pas fourni dans les distro Mongo, il est disponible dans le code open source, 

* il a donc fallu builder mongo depuis les sources. 
* Il a fallu aussi coder l'authentication par certificat dans le stack spring-data, il n'y etait pas.


`RPE` Tu vois, là typiquement, tu as du le coder dans l'appli, c'est pas un truc qu'un consultant externe aurait pu faire. La sécurité c'est autant le taff du dév que du soi disant "expert sécurité", dont les compétences se limitent trop souvent à la configuration de FW...

`FLD` oui je compte fournir ce code à la communauté soit par un pull request sur le project JHIpster ou sur le project spring-data

`slide-25` Chiffrer le back
-------


`RPE` Bon on vient de parler l'authentication et l'authorisation de ton serveur app dans Mongo, mais quand est-il de tes utlisateurs sur ton front ?

`FLD` ca c'est un gros morceau de notre conf en effet.







==========
===========


`Talket 4` Draft
=========

mais tes données c'est quoi
--------




discussions sur les données
* tax
* PII serial killer
* source code


Genre, si ton app gère des dossiers médicaux, Emmanuel Bernard (ou autre mec connu de l'assistance) à pas forcément envie que tout le monde saches la quantité de viaga que lui prescrit son médecin.


* PII http://en.wikipedia.org/wiki/Personally_identifiable_information
* RH : l'org chart, , les manager pourront également consulter et approuver des demandes de congés et des modifications de salaire
* finance : nos utlisateurs pourront consulter et approuver les achats commes les ventes



Https
-----

FLD: Bon je propose que l'on parte de servir l'application sur https uniquement
RPE:  SSL is good, but it depends on how secure is the private key on the server side, how much bits the key has, the algorithm used, how trustworthy the used certificates are, etc ....

TODO
* pitfall https
* https://twitter.com/NorseCorp/status/577895899705270272

But if you use SSL at least all your data transmitted is encrypted (except the target IP because it is used to route your package).

SSL is secure, but remember that any encryption can be broken if given enough time and resources.

Et, surtout, ça ne sert à rien de mettre du HTTPS, partout, juste parce que c'est "secure". C'est le meilleur moyen de détruire les performances de l'application.

Et évidemment, le problème pénible du chiffrement, c'est la gestion des clés et des secrets. Je t'avoue que juste est tellement casse pieds, que ça décourage souvent de le faire.


Mongo SSL authentication
----

RPE:  regardons aussi les flux entre ton app et le reste du réseau. Déjà, rassures moi, la communication entre MongoDB et ton app, rassumes moi c'est pas en clair quand même ? Parce que c'est le fonctionnement par défaut, je te signal


### mongo leak

https://twitter.com/unix_root/status/565906945488748544
40,000 unprotected MongoDB databases, 8 million telecommunication customer records exposed http://thehackernews.com/2015/02/mongodb-database-hacking.html

FLD: Ok, tu m'as convaincu, j'arrête de faire mon bisounours, on va sécuriser la conf mongo. Surtout qu'en fait, c'est pas si simple ...

la je peux faire un slide et fournir un peu de code
car en fait la x509 authentication n'est pas fourni par defaut dans spring data mongo, j'ai du la coder dans mon appli

RPE: Tu vois, là typiquement, tu as du le coder dans l'appli, c'est pas un truc qu'un consultant externe aurait pu faire. La sécurité c'est autant le taff du dév que du soi disant "expert sécurité", dont les compétences se limitent trop souvent à la configuration de FW...

http://www.slideshare.net/mongodb/securing-mongo-db-mongodc-2014-nosig
http://www.allanbank.com/blog/security/tls/x.509/2014/10/13/tls-x509-and-mongodb/
