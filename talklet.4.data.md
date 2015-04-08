`Talket 4` Data and Encryption
=======

`slide-23` Classification
---

`RPE` commencons par évaluer les risques, classifions tes données. Tes données peuvent-elles être considérés comme confidentielles ?

`FLD` contrairement à un app store, un site d'ecommerce ou un backend uber, je ne stocke aucun moyen de paiement, je ne risque donc pas les voir fuiter vers le dark web.

Mais on prévois un beau mashup de données, c'est un "employee productivity tool", à travers mon app vont transiter des données que je ne voudrait pas voir fuiter, comme

* l'adresse, le numero telephone des employés
* l'ensemble de l'arbre organisationel RH
* les salaires
* les congés
* les notes de frais
* des infos sur les deals en cours


`RPE` Bref t'as des données interne, du PII, du confidential et restricted. En fati, c'est intéressant, car, même si les données ne paient pas de mine au premier abord, on s'est vite rendu compte qu'elles étaient en fait confidentiel.

`FLD` Ouais, mais est ce qu'on peut vraiment considérer que le PII est confidentielle ?

`RPE` Ben si un ex jaloux tue son ou sa partenaire, employé de ta boite, parce que Adobe n'a pas respecte la confidentialité de son adresse privée, ça peut se réveler embêtant.

`FLD` Yes, c'est vrai, et en y réflechissant, sans trop succès, on n'a pas trop trouver de cas concrets où les données ne sont pas réellement confidentielles. Dans la pratique, et l'informatique de gestion au moins, c'est très rarement le cas.

`RPE` En fait, on est même arrivé à la conclusion, que au final, dans une app, les données les moins confidentielles, c'est peut être justement son code source !

`RPE` Bref, le mieux, dans le doute, est probablement de considérer que les données sont confidentielles, sauf preuve explicite du contraire.

`FLD` Yes, on a donc plutot intérêt à faire du bon boulot.

`RPE` Ce qui veut dire, qu'il va falloir chiffrer la majorité du flux et de la persistence de ces données de bout en bout, car pour assurer la conidentialité, y'a peu que ça. qu'est ce que tu as prévu pour mettre ça en place ?


`slide-24` Chiffrer le front
-------

`FLD` de bout en bout, commencons alors par le front, on prévoit évidemment de tout servir en https

`RPE` SSL c'est secure, mais faire ça correctement c'est tout un art.

`FLD` Et ça demande une surveillance et une veille techno constante,


`FLD` même les plus grands doivent gérer des situations de crise, vols de certificats, ou la propagation de certificat qu'ils non pas authorisés mais qui sont trustés par la plupart des navigateurs

`RPE` et souvenez vous, avec suffisamment de temps et de ressources, n'importe quelle chiffrement peut-etre cassé .

`FLD` dernier conseil avant de passer à la suite,


* faite ce boulot au niveau du reverse proxy (nginx, apache...), automatiser cela avec Chef ou Puppet
* vous pouvez le faire aussi au niveau du serveur d'app, sachez Jhipster ne le supporte et tout comme Romain ne le conseille pas, cf l'issue jhipster #678
* scannez vous serveur https pour détecter les éventuelles vulnérabilités et obsolesances

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


`RPE` Tu vois, là typiquement, tu as du le coder dans l'appli, ce n'est pas un truc qu'un consultant externe aurait pu faire. La sécurité c'est autant le taff du dév que du soi disant "expert sécurité", dont les compétences se limitent trop souvent, de nos jours, à la configuration de FW...

`FLD` oui je compte fournir ce code à la communauté soit par un pull request sur le project JHIpster ou sur le project spring-data

`slide-25` Chiffrer le back
-------


`RPE` Bon on vient de parler l'authentication et l'authorisation de ton serveur app dans Mongo, mais quand est-il de tes utilisateurs sur ton front ?

`FLD` ca c'est un gros morceau de notre conf en effet.



`Talket 4` Draft
=========

* PII http://en.wikipedia.org/wiki/Personally_identifiable_information
* RH : l'org chart, , les manager pourront également consulter et approuver des demandes de congés et des modifications de salaire
* finance : nos utlisateurs pourront consulter et approuver les achats commes les ventes


TODO
* pitfall https
* https://twitter.com/NorseCorp/status/577895899705270272

But if you use SSL at least all your data transmitted is encrypted (except the target IP because it is used to route your package).

SSL is secure, but remember that any encryption can be broken if given enough time and resources.

Et, surtout, ça ne sert à rien de mettre du HTTPS, partout, juste parce que c'est "secure". C'est le meilleur moyen de détruire les performances de l'application.

Et évidemment, le problème pénible du chiffrement, c'est la gestion des clés et des secrets. Je t'avoue que juste est tellement casse pieds, que ça décourage souvent de le faire.


SSLv2 SSLv2 is Disabled SSLv2 is weak and should be disabled. More information.
SSLv3 SSLv3 is Disabled Consider disabling SSLv3 to mitigate the POODLE attack.
TLSv1 TLSv1 is Enabled  TLSv1 should be enabled.

https://twitter.com/jeremiahg/status/580380300494049280
http://blog.facilelogin.com/2014/10/poodle-attack-and-disabling-ssl-v3-in_18.html

http://foundeo.com/products/iis-weak-ssl-ciphers/test.cfm?test_domain=foundeo.com

https://access.redhat.com/solutions/1232233


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
