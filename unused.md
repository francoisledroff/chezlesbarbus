other ideas content
============


### HSM 

(@FLD, RPE doit lire car là, il connait pas, peut être parlant et ça fera une séquence où tu me fermes la geule et tu me dis 'hey pas que les barbus qui s'y connaissent ;)")

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



### misc / unused

update your linux (ghost) we you have docker ! fun !
http://googlecloudplatform.blogspot.fr/2015/02/using-google-cloud-platform-for.html

gemalto hacked : https://firstlook.org/theintercept/2015/02/19/great-sim-heist

vous avez été espionné?
http://www.numerama.com/magazine/32243-avez-vous-ete-espionne-par-la-nsa-voici-une-chance-de-le-savoir.html

https://twitter.com/codinghorror/status/567434195987738624
The best reaction to "this is confusing, where are the docs" is to rewrite the feature to make it less confusing, not write more docs.

draft
-------

`RPE` il nous faudra beaucoup plus de temps en effet pour creuser l'ensemble des concepts introduits ici, ce qui me parait primordial c'est de comprendre la gravité de voir tes données fuiter. Quelles sont ces données ? Sont elles classifiées ? confidentielles ?


* Spoofing Identity : ensure a single execution context at the application and database level.
* Tampering with Data : data validation
* Repudiation: audit trails at each tier
* Information Disclosure: persist/cache as little info as possible
* Denial of Service, do not allow anonymous, or do as little as possible for anonymous
* Elevation of Privilege : proper ACL in place


Microsoft
https://www.owasp.org/index.php/Threat_Risk_Modeling
http://linuxfr.org/news/threat-modeling-savez-vous-quelles-sont-les-menaces-qui-guette

Annexes
=====

### Objectifs

 "audit" on a ce mot dans notre abstract, mais en fait on veut pas vraiment faire un audit une fois tout developpé, on veut changer l'etat d'esprit du dev et de lops pour les sensbiliser à la sécu, on veut montrer plutot comme l'archi, la qa, le dev, l'ops sont partie prenante de la secu et comment la secu se fait "by design" tout au long du projet... en gros le concept d'audit de secu est naze...


### TODO
-------

@FLD, je crois ces statistiques ont disparu du talk, peut être les remettre à la fin de l'into.

http://www.ivizsecurity.com/blog/penetration-testing/web-application-vulnerability-statistics-of-2012/

* 99% of web applications have at least 1 vulnerability
* 82% of web applications have at least 1 High/Critical Vulnerability
* 90% of hacking incidents are not reported publicly



#### `slide-9` xss Rachida

`RPE` ... même si les attaques XSS ce serait un bon rappel pour les dev qui bossaient pour le site de Rachida Dati

`FLD` et un bon rappel le procureur de Paris.

`RPE` Je crois que là, pour le moment, il doit probablement essayer de relire la page wikipedia sur le sujet. Qu'il doit trouvé confus et incompréhensible. Un juriste qui trouve un texte, confus, si c'est pas de l'ironie ça...

=======
=======

draft and notes


 http://www.arnoldit.com/articles/10intranetSecAug2002.htm

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
