other ideas content
============

annexe
-----

1) Github

`RPE` Bon, of course, l'ami Github est le premier auquel on pense. Suffit de voir combien de résultat retourne une requête sur 'mysql_query' dans la code base, pour voir qu'on a déjà un bon point de départ.

https://github.com/search?p=3&q=extension%3Aphp+mysql_query+%24_GET&ref=searchresults&type=Code  (faire une photo)

`RPE` Bon, au final, c'est évident, et je pense que la plupart d'entre vous sont (ou plutôt pensent être) protégé, parce que "aucune personne dans la compagnie ne va jamais commité un mot de passe". Ouais, bon, allez, assumons que c'est vrai. De toute manière, y'a beaucoup plus retour à faire. Comme par exemple commité sous un autre nom - en effet, c'est la grosse faiblesse des DVCS par rapport à SVN/CVS, plus de centralisation. N'importe qui peut fusionner une PR venant de quelqu'un autre contenant des commits avec "d'autres auteurs".

`FLD` Ouais, mais c'est grave ça ?

`RPE` Ben déjà, ça fout en l'air d'audit trail. Tu recherches qui a injecté un code malicieux et ça ne te pointe pas sur la bonne personne, mais surtout ça ouvre la porte à des exploits "social". On a tous dans nos boites des "diva" dont personne ne va remettre le code en question parce que c'est "untel" qui l'a écrit. D'ailleurs, c'est exactement comment ça que Tordvals fait avec le kernel. Il ne pull que depuis des repos de gens qu'il connait et respecte. (@assistance, je vous rassure, les mecs comme ça y'en que 7. Je ne suis pas sûr que Tordvlad accepterait une PR de sa propre femme...)

`FLD` Ouais, Ok, donc tu fais une PR avec des commits venant d'un tel gus, et le code est accepté sans être revu...

`RPE` Laissant rentrer, par exemple, un code malicieux...

`FLD` OK, mais qu'est ce qu'on peut faire concrètement ?

`RPE` Ben des trucs simple, comme 1) se méfier des PR même venant d'auteur de confiance, si elles changent beaucoup de code. En fait, une PR (à mon sens), c'est comme une méthode Java ou un commit, ça doit pas être trop long. La même manière par exemple que je n'écris pas une méthode Java qui dépasse 5,6 lignes, et que je ne fais pas un commit avec 143 changements, je pense qu'une PR devrait contenir un petit ensemble de commit (ou un seul, même si perso, je trouve ça dommage).

`FLD` OK, mais sinon. Quoi d'autre ? Avoir une forme de tracabilité pour l'audit j'imagine ...

`RPE` Oui, exactement. Tu dois pouvoir déterminer qui a crée une PR, qui l'a accepté, etc... mais pas seulement. Par exemple, il faut aussi avoir un process pour nettoyé après le départ d'un employé de l'organisation. Effacer leurs repos, mais aussi, pourquoi pas, auditer leur répos publiques (même si ça pose des questions en terme de respect de la vie privée).




### HSM 

(@FLD, RPE doit lire car là, il connait pas, peut être parlant et ça fera une séquence où tu me fermes la geule et tu me dis 'hey pas que les barbus qui s'y connaissent ;)")

hsm protect private key, proprio non ?
certificate segregated by group
hsm will make offline attacks impossible

this will buy you time to detect an attack and react accordingly

 => useless if no IDS in place or at least monitoring !!!

RPE: Je ne sais pas si le HSM ne serait pas à dropper si on a trop de contenu... my 2c

stufff
----

`FLD` uservice + netflix briques => XUL

ping pong apache /nginx lua

en plus de XUL y a HIRTSC

RPE c quoi ?

`FLD` impl le circuit breaker, deps sur salesforces, mode degrad

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

=====



OAuth2 Key Features

IETF standard
Extremely simple for clients (and developers)
Access tokens carry information (beyond identity)
Clear separation between users and machines
Strong emphasis on not collecting user credentials in client app
Machines act on their own or on behalf of users
Resources are free to interpret token content

So what's wrong with that?

Nothing, but...

et pas mal d'autre probleme
http://www.slideshare.net/CQCON/prsentation-antonio-sanso

http://dev.day.com/content/ddc/en/gems/oauth-server-functionality-in-aem---embrace-federation-and-unlea/_jcr_content/par/download/file.res/OAuth_Server_functionality_in_AEM%207%2023%2014.pdf

pas facile a faire le oauth server



Other Options

OAuth 1.0
SAML assertions
Physical network security IP tables etc.
Kerberos
Combinations of the above (including OAuth 2.0)


http://presos.dsyer.com/decks/microservice-security.html#slide12
http://presos.dsyer.com/decks/microservice-security.html#slide27


=======
========




`slide-32` murphy ?
--------

`RPE` et quand ton disque crash ?
`FLD` si tu as toujours ma tablette ou mon telephone, c'est bon
je synchronise mes mots de passes sur ma tablette et mon telephone
`RPE` et si tu les perds
`FLD` dans mon passeport, j'ai 

photo du telephone cassé et du passeport




la reutilisation des mots entraine un enorme probleme de secu.



`Talklet 5` Draft
==========


Password regles et limites
------


FLD: Ouais, mais attend, c'est pas si naze, puis, par défaut, on s'est assuré que tout les mots de passe seraient "strong" (à dév) pour éviter ca http://www.ayblog.com/wp-content/uploads/2013/10/Nice-Change-of-Password-to-Incorrect.jpg

RPE: mouais, tu veux implementer ca : http://www.medsyn.fr/perso/g.perrin/joomla/images/stories/food/Blog/mot-passe2.jpg
ou ca https://theeditorsjournal.files.wordpress.com/2014/09/creating-a-password.jpg?w=1240&h=1248

FLD: c'est vrai, que ces strong passwords sont just difficile a retenir mais pas à craquer : http://xkcd.com/936/






RPE: Mais même si le mot de passe est "strong," l'utilisateur va devoir le créer, et comme on a plein de mot de passe à gérer, fort à parier, qu'il va reprendre le même que "ailleurs", ce qu'on appelle du "common logging". Et ce mot de passe, est probablement déjà craqué par tout le monde - à commencer par les mecs de la NSA.

FLD: Ouais, c'est vrai qu'il suffit de se rappeler de Sonny...
we have so may passwords to deal with, we reused them
sony password reused at yahoo: http://www.troyhunt.com/2012/07/what-do-sony-and-yahoo-have-in-common.html

Password cycle de vie
------

RPE: Ensuite, avec l'approche db users de JHipster, tu retrouves aussi à gérer le cycle de vie du mot de passe. Il faudra créer un mot de passe pour ton app, en plus du reste, et l'app devra permettre à l'utilisateur de le mettre à jour, mais aussi à l'administrateur de gérer ces derniers. Bref, ça va très rapidement faire chier tout le monde, et les utilisateurs vont sans doute faire du "common logging" et coller son mot de passe "habituel", déjà craqué par tout le monde - à commencer par les mecs de la NSA. Et fort à parier que peu, voire aucun, utilisateurs ne le changera par lui même - donc à ton appli de l'exiger - et là encore, des codes à ajouter.

FLD: je crois qu'en effet Jhipster a toute une tringlerie, avec une page register et de l'envoi de mail avec un password reset link...  moi j'avais pensé à faire une page de "password recovery" à base ce question secrète

You can name her whatever you like but be sure it’s something you can remember. You’ll be using it as a security question answer for the rest of your life

http://positivedoggie.com/you-can-name-her-whatever-you-like-but/

RPE: ca me rappelle le hack de Paris Hilton :

Paris Hilton pet name security hack
http://www.macdevcenter.com/pub/a/mac/2005/01/01/paris.html
http://content5.promiflash.de/article-images/w500/paris-hilton-haelt-zwergspitz-prince-hilton-auf-dem-arm.jpg




t'as pas un IDP dans ton intranet
----

RPE: Puis, bon, Adobe, comme nous Red Hat, on est des boites sérieuses, vous avez bien une solution de gestion d'identité ? Si vous n'avez pas, je crois qu'on en vends 4 différents au dernier compte ! (Si vous prenez une paire de QUeue JMS, en plus, on fait un prix ;) ).

RPE: Bref, après toutes ces conneries, au final, tu as un IDP dans ton intranet super-secure ?

FLD: Ouais, d'ailleurs c'est la classe, c'est basé du SAML avec du 2FA !

screencast 

2 FA and UX
----

RPE: vas-y qu'est ce que t'attends, put 2fa in place

FLD: Ouais, mais alors, OK , c'est secure, mais alors bonjour l'expérience utilisateur ! Personne va vouloir l'utiliser notre app à ce compte là

 https://twitter.com/michaelneale/status/568279010968383488

1. App requires 2FA login.
2. get phone from pants
3. Distracted by 100s of notifications on it
4. Back to computer. Repeat.



RPE: Oui, en fait, mais dis francois toi comme moi on utilises 2FA sur nos comptes twitter, google et facebook, n'est ce pas?
c'est pas si douloureux,

FLD: qui ici a activé https et 2fa sur google, facebook, twitter et les autres ?


mais crois qu'ici tu pourrais utiliser oauth2, une fois l'utilisatuer authentifié

FLD: Oui, c'est une bonne idée

RPE: Comme quoi, c'est malin de bosser Dev + Sécu ;) - vas y montre moi comment tu fais avec ton app:

et la je peux montrer encore du code modifié de jhispter ou l'authentication est deporté sur un idp saml et ensuite seuleuemtn un oauth token (et un refresh token) est echangé avec le front-end javascript

resultat tu te tappes le 2fa une fois et ensuite a moins de quitter l'app pendant plus de 30 jours tu le referas pas.

on peux montrer les echanges avec des jolies sequence diagram
on peux aussi montrer que l'on peut revoker les tokens pour les stolen device/laptop/desktop
j'ai du code jhipster et une interface pour ca


RPE: Ok, je pense que là t'es bon pour au moins déployé en interne.

FLD: Ben, c'est ce qu'on a fait après ça, mais maintenant que ça marche bien, on veut ouvrir le service à l'extérieur.

RPE: Ah ouais, mais alors du coup, on n'a pas fini, il reste des trucs à voir. A commencer, par les attaques de types "brute forces" tes mots de passes.


### avoid Brute force attack

FLD: Attend, on y a pensé, et on a mis des contraintes sur les password pour qu'il soit difficile à craquer

(@FLD, là si tu as , on montre du code jhipster)

RPE: Ouais, c'est bien, mais ça n'empêche pas un attaquant d'essayer quand même et, soit d'éventuellement réussir, ou juste rendre ton service inaccessible (par effet de bord). C'est pourr ça que moi j'aime bien avoir un reverse proxy en place en frontal de tout appli.

@FLD, la je ferais une petit explication du concept sur 1,2 slides

RPE: Donc avec un RP en place, pour ton problème de mot de passe, tu peux déjà controllé qu'un utilisateur ou une IP essaye pas "en boucle" de se logguer, sans encombrer le code ou la logique de ton app. Tu peux aussi nettoyer les paramètres transmis ou simplement dropper des requêtes invalides. Quand on sait que, en fin de compte, le gros des exploits se font en abusant des paramètres - comme le classique "; drop database", c'est une bonne protection de s'assurer qu'on  ne recevra que des requêtes dotés de paramètres valides.

(là tu peux rebondir avec les CAPCHAs que tu as mis en place sur ton app jhipster

@FLD, peut être que tu as du code JHipster qui fait pareil, et là on peut faire un micro débat sur ce point entre "a1, je veux le faire dans mon app" et "a2, mais non, laisse l'infra faire...",

### API en ligne

FLD: Au fait, Romain, on n'en a pas parlé, mais mon appli a un service en ligne - un service ReST,

RPE: ReST ? Vraiment ? Tu aimes plus te palucher des XSD et le "savon" (SOAP) ? Mais plus sérieusement, ça crée d'autres problèmes...

* rate limits
* header validation
* conditional requests

=> IMHO, Un RP en frontal, faisant du nettoyage de requêtes + mise en place de bannissement si
nécessaire, me semble être essentiel.

===

150 max: https://github.com/jhipster/generator-jhipster/blob/master/app/templates/src/main/java/package/web/rest/_AccountResource.java#L200

===

TODO @FLD, tu veux développer les points ci dessous ?
* adhoc short lived build machine
* what about data ? and rtest data security ?

secret management
-----

`RPE`: Une des grandes failles introduit par les chaines d'intégration continue est bien évidemment, la gestion des secrets. Un développeur embarque un certificat SSL dans son code. Il l'a probablement bricolé à la main sur sa machine, pas forcément à jour, avec une version d'OpenSSL aussi robuste la dernière version de Windows (en fait, non, que n'importe quelle version de Windows). Bref, ce certificat tout pourri est poussé dans le gestionnaire de révisions, l'application est "buildé" par Jenkins, et jeter en production, avec le même certificat, sans même que personne ne se pose de questions...

`FLD`: Ouais, mais tu vois, c'est là qu'on est malin, car pour gérer nos secrets, on utilise chef-vault

TODO: @FLD là fo que tu développe

Managing secrets: still the hardest problem in operations (https://twitter.com/jtimberman/status/568124542553423872)

secret management : https://coderanger.net/chef-secrets/
chef-vault and citadelle

jce chef recipe
chef-vault

secret in your secret OAuth secrets
---


segregate your secrets from your source code
search in github.com for password, secret, key
et hop la on peut une recherche dans jhipster on y trouveras quelques secrets

we have oauth clientid and secret in jhipster
la encore je peux montrer comment on peut generer le oauth client et le oauth secret à la volée seuleument une fois l'authentication saml reussi

sepration of duties
rotate account information

SELinux & SM
----

`FLD`: Ah ouais, mais du coup, pourquoi pas mettre les deux en places ? 

`RPE`: Théoriquement tu peux, mais c'est déjà beaucoup de boulot, et chaque couche augmente les chances de se tirer dans le pied. Imagines le scénario, tu déploies l'appli en pre prod, et une nouvelle fonctionnalité marche pas comme prévu. En gros, le SM ne laisse pas l'appli ouvrir un fichier dans le répertoire tmp. Tu corriges, tu redéplois, et là ça merde pour la même raison, mais ce coup ci, c'est SE Linux qui dit ton app Java d'aller se faire voir. Sans compter, que chacun techno a la même fonctionnalité, même pas du tout la même syntaxe ou prérequis, donc, rien qu'en coût de formation, ça semble pertinent.

`FLD`: Ouais, en fait, il vaut mieux le faire une fois bien, plutôt que deux fois mal. Et au final, le choix entre SE Linux et SM, se fait plutôt sur les compétences en interne et les besoins - y'en a pas une meilleur que l'autre.

`RPE`: Non, en effet. C'est pas comme Windows versus RHEL - là on sait clairement qui est le meilleur :) (@assistance, et si quelque répond Windows, je le tue)

`FLD`: Ouais, mais dis moi, avec ça en place, ça évite que ton application crée des fichiers, ou exécute des programmes, mais si l'exploit se base sur une "activité" normale. Par exemple modifie le contenu d'un fichier de données légitime de l'application - tu peux gérer ça avec ton SM ou SE Linux ?

`RPE`: Non, j'en doute, et de toute manière, ça ne serait pas vraiment une bonne pratique, de mettre ce genre de contrôle en place là dedans.

===

 


`RPE` Bon, du coup, là tout le monde à soif et après, c'est la bière, donc, si on essayai un peu de résumé tout ça.

`FLD` Yes, mais on a quand même un paquet de chose. Enfin, voilà une liste, pour faire l'inventaire.

`RPE` C'est ton coté Mésopotamien.

`FLD` Exactement. Bref:

* sandboxing reduces vulnerabilities
* better application server
* keep your secret safe
* use vault + configuration
* analytics on password request
* you leave an audit trail
* avoiding downtime when password/key change

`RPE`

* exploit don't last long - so the plan is to "hold" (availability, ensure your systems can "last long enough" during an attack)

`FLD`

**The three goals of security are confidentiality, integrity and availability**. Intranet security must deliver integrity and availability. Intranets exist to make information available to colleagues. Nevertheless, confidentiality is an issue. Each job function and person holding that job is given a level of access appropriate to his or her role. Intranets are often less secure than information technology professionals and managers realize

http://www.arnoldit.com/articles/10intranetSecAug2002.htm

@FLD, j'ai laissé, mais honnetement, j'aime pas trop tout le début ci dessus, je sauterais bien directement à ci dessous:

`FLD` En fait, au bout du compte, on vient de voir que la sécurité, c'est pas un truc adhoc, isolé, que tu peux implémenter à la fin, après un audit, mais plutôt un "combat de tout les instants".

`RPE` Yes, exactement. La sécurité c'est comme les bogues ou les fonctionnalités, il faut y travailler en harmonie avec le développement de l'applicatif, au fil de l'eau. En fait, on pourrait résumer ce qu'on vient de dire par un truc comme "DevSec". De la même manière, qu'avec Puppet...

`FLD` ou Chef !

`RPE` Oui ! Ou Chef ! Bref, de la même manière qu'avec DevOps, on n'a rapprocher l'infrastructure du développement, la sécurité s'est aussi rapprocher du dev. Le temps où les dévs pouvaient dire "la sécurité, je m'en fous, c'est le truc du barbu au fond du couloir", tout aussi révolu que celle où les dits "barbus" pouvaient limiter leur travail à la mise en place de FW, en se moquant (et se lavant mêmes les mains) des applis Java déployé sur leur système.

`FLD` Oauis, clairement, le gros des faiblesses de sécurité sont aujourd'hui dans les apps plus que l'infrastructure, pour sécuriser un
système, les deux profils doivent s'assurer coté à coté et (par exemple) rédiger ensemble les polices de sécurité du SecurityManager et les règles de filtrages applicatives.

`RPE`Exactement.

`FLD` Et déployer tout ça avec Chef.

`RPE` Ou Puppet...

`FLD` Ou Puppet.
