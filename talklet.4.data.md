`Talket 4` Data and Encryption
=======

`slide 

RPE: commencons par évaluer les risques, classifions tes données. Tes données peuvent être confidentielles.


`Talket 4` Draft
=========

mais tes données c'est quoi
--------




discussions sur les données
* tax
* PII serial killer
* source code


Genre, si ton app gère des dossiers médicaux, Emmanuel Bernard (ou autre mec connu de l'assistance) à pas forcément envie que tout le monde saches la quantité de viaga que lui prescrit son médecin.

FLD: oui on a beau mashup de données, c'est un "employee productivity tool", on prévois de manipuler des données de type
* PII http://en.wikipedia.org/wiki/Personally_identifiable_information
* RH : l'org chart, , les manager pourront également consulter et approuver des demandes de congés et des modifications de salaire
* finance : nos utlisateurs pourront consulter et approuver les achats commes les ventes

RPE: ok donc, on a plutot intérêt à faire du bon boulot. Note que les "barbus" ou les techos en général trouvent ce genre de classification / méthodologie souvent un peu "bullshit", ça fait juste des jolies tableaux ou rapports pour le management mais "ça ne me sert à rien". En fait, ça permet surtout de faire comprendre au management qu'il y a un problème, dans un format qu'ils peuvent comprendre et réutiliser. En outre, si vous êtes coté management et que vous soupçonnez que vos devs ont été un peu trop "libérale" avec la sécu, faire ce genre d'inventaire est aussi un bon moyen de leur faire réaliser le problème. Bref, comme tout méthodo ou approche formelle, c'est certainement pas une solution miracle, mais plutôt à outil à utiliser à bonne escient.

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
