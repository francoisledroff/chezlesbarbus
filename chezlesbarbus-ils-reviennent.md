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

intro
====

### Notre but :

FLD: "audit" on a ce mot dans notre abstract, mais en fait on veut pas vraiment faire un audit une fois tout developpé, on veut changer l'etat d'esprit du dev et de lops pour les sensbiliser à la sécu, on veut montrer plutot comme l'archi, la qa, le dev, l'ops sont partie prenante de la secu et comment la secu se fait "by design" tout au long du projet... en gros le concept d'audit de secu est naze...


### FLD se presente
###  RPE se presente


plan
-----

* ma petit web app intranet
* d'interne à externe
* bienvenu sur le cloud
* CI & Build, tout un monde de faille à exploiter


ma petite web app intranet
==========


avant propos
-----

FLD: Romain, on n'a une petit appli interne, qu'on va mettre en prod, et on m'a dit de faire un audit de sécurité.

RPE: Pourquoi ? C'est déjà trop tard...

FLD: Ben, c'est pas le moment de faire un audit de sécurité ? On voulait faire venir des experts en sécurité.

RPE: Pourquoi faire ? Tu veux qu'il te reconfigure ton FW ? Honnêtement, je vois mal comment des experts externes pourront mieux sécuriser ton appli que tes devs et toi. Eventuellement, ton infra se sécu, mais à la base, pour hacker une appli, il faut la détourner de son fonctionnement "normal". Et, à ton avis, de tes fameux experts en sécurité et ton équipe de dév qui connait mieux le fonctionnement normal de l'appli ?

FLD: Ouais, mais attend mon équipe de dév, y'en a la moitié déjà qui travaille sur Windows, l'autre sous OSX, et l'architecte a rasé sa barbe la semaine dernière - bref, personne n'est calé en sécurité, on va pas faire ça tout seul.

RPE: Non, mais vous allez aire ça ensemble... Bon allez, commençons par le début, parlez moi un peu de ton bouzin en Java (je sens déjà le jar de 200Mb arriver...)

mon appli jhipster
-----

* FLD c'est une appli web intranet, c'est pas une appli pour placer des pubs,  c'est pas big data, pas trop social, pas très hipster, mais comme je voulais me faire plaisir je suis parti sur un stack jhipster

* RPE c'est quoi jhipster ? Encore un framework MVC ? Un truc qui springboot pour lancer un container scala écrit en JRuby qui exécute des greffons groovy ?

* FLD: c'est un generateur d'appli web (à la appfuse) basé sur yeoman, au final tu as un stack assez lean, plutot recent avec du springboot pour la partie serveur et du angularjs pour le partie cliente

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

* RPE ok, bon  à part télécharger la terre entière pour foutre je ne sais combien de couche d'abstraction à la Java, je vois surtout t'es parti sur du oauth2 et du mongodb. MongoDB c'est pour faire cool et dragué les filles sur la plage, c'est ça ?

* FLD: Ouais, exactement !


web app
-------

RPE: donc c'est une web app
FLD: OUi je sais ce que tu vas me dire:

http://www.ivizsecurity.com/blog/penetration-testing/web-application-vulnerability-statistics-of-2012/

* 99% of web applications have at least 1 vulnerability
* 82% of web applications have at least 1 High/Critical Vulnerability
* 90% of hacking incidents are not reported publicly

Sécurité : Java serait le programme le plus exposé aux attaques, suivi par QuickTime, Adobe Reader, VLC et .Ne...

https://twitter.com/Developpez/status/560389865003425792
http://bit.ly/1zaB89X



Intranet
-----

* FLD: Ce qui est cool c'est que l'appli est déployé en interne, au sein de notre intranet
* RPE : just a look 
* FLD: je sais ce que tu vas me dire
* RPE: laisse moi d'abord te poser une question, tes ulisateurs se connecte depuis une variéte de laptop et desktop et se connectet depuis leur machine égagelemt sur internet ?
* FLD oui
* RPE: tes utilisateurs sont-ils root sur leur machine ? tes utilisateurs ont-ils des machine managées ?
* FLD: oui, et tu vas me demander si mes utilisateurs sont usr linux  RHEL 
* RPE: tu l'as compris, intranet ou internet, c'est le même combat.

* FLD: "The only secure computer is one with no power, locked in a room, with no user." Any other system can be compromised. 

TODO: trouver une anecdote qui montre - que je raconterais en mode "vieux grumpy" qui montre que le réseau interne n'est pas secure.

**The three goals of security are confidentiality, integrity and availability**. Intranet security must deliver integrity and availability. Intranets exist to make information available to colleagues. Nevertheless, confidentiality is an issue. Each job function and person holding that job is given a level of access appropriate to his or her role. Intranets are often less secure than information technology professionals and managers realize

http://www.arnoldit.com/articles/10intranetSecAug2002.htm


Thread Model
--------

FLD: ce qui compte c'est du comprendre les menaces qui pèsent sur notre système. 

Microsoft 
https://www.owasp.org/index.php/Threat_Risk_Modeling


FLD: pas le temps ici pour faire un cours sur les concepts de STRIDE et DREAD, voici juste un slide


STRIDE is a classification scheme for characterizing known threats according to the kinds of exploit that are used (or motivation of the attacker). 

* Spoofing Identity : ensure a single execution context at the application and database level. 
* Tampering with Data : data validation
* Repudiation: audit trails at each tier
* Information Disclosure: persist/cache as little info as possible
* Denial of Service, do not allow anonymous, or do as little as possible for anonymous
* Elevation of Privilege : proper ACL in place

DREAD is a classification scheme for quantifying, comparing and prioritizing the amount of risk presented by each evaluated threat. 

* Damage Potential
* Reproducibility
* Exploitability
* Affected Users
* Discoverability


RPE: commencons par évaluer les risques, classifions tes données. Tes données peuvent être confidentielles. Genre, si ton app gère des dossiers médicaux, Emmanuel Bernard (ou autre mec connu de l'assistance) à pas forcément envie que tout le monde saches combien de stocks

FLD: oui on a beau mashup de données, c'est un "employee productivity tool", on prévois de manipuler des données de type 
* PII http://en.wikipedia.org/wiki/Personally_identifiable_information
* RH : l'org chart, , les manager pourront également consulter et approuver des demandes de congés et des modifications de salaire 
* finance : nos utlisateurs pourront consulter et approuver les achats commes les ventes  

RPE: ok donc, on a plutot intérêt à faire du bon boulot


Https
-----

FLD: Bon je propose que l'on parte de servir l'application sur https uniquement
RPE:  SSL is good, but it depends on how secure is the private key on the server side, how much bits the key has, the algorithm used, how trustworthy the used certificates are, etc ....

But if you use SSL at least all your data transmitted is encrypted (except the target IP because it is used to route your package).

SSL is secure, but remember that any encryption can be broken if given enough time and resources.

### secret management

FLD: pour gèrer mes secrets et mes clefs , j'utilise chef-vault


https://twitter.com/jtimberman/status/568124542553423872
Managing secrets: still the hardest problem in operations.

secret management : https://coderanger.net/chef-secrets/
chef-vault and citadelle

jce chef recipe
chef-vault



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



### Password

RPE: Ah je vois que par défaut, jhipster a sa propre base de donnees d'utilisateur, pas mal pour le dev, mais une cata pour la prod !

FLD: Ouais, mais attend, c'est pas si naze, puis, par défaut, on s'est assuré que tout les mots de passe seraient "strong" (à dév)
pour èviter ca http://www.ayblog.com/wp-content/uploads/2013/10/Nice-Change-of-Password-to-Incorrect.jpg

RPE: mouais, tu veux implementer ca : http://www.medsyn.fr/perso/g.perrin/joomla/images/stories/food/Blog/mot-passe2.jpg
ou ca https://theeditorsjournal.files.wordpress.com/2014/09/creating-a-password.jpg?w=1240&h=1248

FLD: c'est vrai, que ces strong passwords sont just difficile a retenir mais pas à craquer : http://xkcd.com/936/


RPE: Sans compter, qu'il faudra créer un mot de passe pour ton app, en plus du reste. C'est naze, ça va faire chier tout le monde, qui va coller son mot de passe "habituel", déjà craqué par tout le monde - à commencer par les mecs de la NSA, et qu'ils ne vont jamais changé par eux même. 

FLD: Ouais, c'est vrai qu'il suffit de se rappeler de Sonny...
we have so may passwords to deal with, we reused them
sony password reused at yahoo: http://www.troyhunt.com/2012/07/what-do-sony-and-yahoo-have-in-common.html




RPE: Du coup, ton app doit gérer le cycle de vies, envoyés des mails (donc pouvoir envoyer des mails) pour notifier les utilisateurs etc... Bref, la merde.

FLD: je crois qu'en effet Jhipster a toute une tringlerie, avec une page register et de l'envoi de mail avec un password reset link...  moij'avais pensé à faire une page de "password recovery" à base ce question secrète 

You can name her whatever you like but be sure it’s something you can remember. You’ll be using it as a security question answer for the rest of your life

http://positivedoggie.com/you-can-name-her-whatever-you-like-but/

RPE: ca me rappelle le hack de Paris Hilton :

Paris Hilton pet name security hack
http://www.macdevcenter.com/pub/a/mac/2005/01/01/paris.html
http://content5.promiflash.de/article-images/w500/paris-hilton-haelt-zwergspitz-prince-hilton-auf-dem-arm.jpg


RPE: on est donc d'accord : pour faire court, les mots de passe, c'est juste "mal". Tu sais, comme croiser les effluves ? En gros, 100% des attaques en 2014 implique des mots de dérobé. Si tu veux pas de divorce, te marie pas, ben pareil, si tu veux pas qu'on te vole to password, en ai pas !
http://idtheftcenter.org/


FLD: on souffre tous, on doit tous gerer à notre echelle une ribambelle de mot de passe, moi j'utilise splashid pour stocker et generer mes mots de passe, aucune synchro sur le cloud, juste une synchro entre device

j'ai actuellement 159 mots de passe dans cette base, je ne voudrais pas en créer un autre...


### t'as pas un IDP dans ton intranet 

RPE: Puis, bon, Adobe, comme nous Red Hat, on est des boites sérieuses, vous avez bien une solution de gestion d'identité ? Si vous n'avez pas, je crois qu'on en vends 4 différents au dernier compte ! (Si vous prenez une paire de QUeue JMS, en plus, on fait un prix ;) ). 



RPE: Bon, après ces conneries, au final, tu as un IDP dans ton intranet super-secure ?

FLD: Ouais, d'ailleurs c'est la classe, c'est basé du SAML avec du 2FA !

### 2 FA and UX

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


### OAuth secrets 


segregate your secrets from your source code
search in github.com for password, secret, key
et hop la on peut une recherche dans jhipster on y trouveras quelques secrets

we have oauth clientid and secret in jhipster
la encore je peux montrer comment on peut generer le oauth client et le oauth secret à la volée seuleument une fois l'authentication saml reussi

sepration of duties
rotate account information

+1 slide sur ça

@FLD, ok, là je pense qu'il faut qu'on passe à la partie Cloud....




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

RPE: ReST ? Vraiment ? Tu aimes plus te palucher des XSD ;) ? Mais plus sérieusement, ça crée d'autres problèmes...

* rate limits
* header validation
* conditional requests

=> IMHO, Un RP en frontal, faisant du nettoyage de requêtes + mise en place de bannissement si
nécessaire, me semble être essentiel.


### The shit HAS hit the fan

FLD: bon, on est bon là ?

RPE: ben c'est dur à dire, on peut jamais être sûr, mais disons que maintenant, ce qui serait sympa, c'est de protéger les copains de nos conneries. Bref si tu as laissé un trou dans ton appli, que au moins, seule elle soit compromise.

FLD: Comment ça ?

RPE: Ben si un mec à trouver un exploit sur ton app, il peut accéder à ses données, mais aussi éventuellement, modifier son comportement. Par exemple, lui faire envoyer des mails ("Merci à l'infrastructure Adobe d'avoir participé "pro bono" à la diffusion de mes spams !), effacer des fichiers ou récupérer des données d'une autre app colocalisé avec l'appli.

FLD: Et tu peux faire qqlchose contre ça ?

RPE: Ouais, bien sûr, c'est un peu la même logique qu'avec le RP. En gros, tu défini le comportement "normal" de ton appli et tu banni tout le reste. Tu peux le même faire à deux niveaux. D'abord, sur le JVM avec le Security Manager, que tout le monde connait ici (regard à l'assistance) car aucun expert ou dev Java tourne d'applicatif sans, hein ? ;)

RPE: Et tu peux aussi le faire au niveau système avec SE LInux. En gros, les deux technos ont la même fonctionnalité et voilà comment elles marchent

1,2 slides sur ce truc, avec des petits exemples de config

#### Never safe behind a FW

FLD: Au fait, tu me casses les pieds avec la sécu depuis 20 minutes, mais on n'en pas encore parlé de FW !

RPE: Pourquoi faire ? Les FW ça ne sert pas à sécuriser des applis... Non, sérieusement, le truc du FW, c'est juste de faire de la qualité réseau et d'épargner, le CPU. En gros, si un système reçoit un paquet pour un port "non utilisé", il drop en kernal space, plutôt que de le faire remonter pour rien jusqu'au couche applicative.

FLD: Mais attends ça bloque des ports, donc ça empêche des attaques, non ?

RPE: Ouais, généralement que tu as truc qui tourne sur un port, c'est que tu en as besoin. Si tu es assez con pour laisser tourner un service dont tu as pas besoin, effectivement, ton FW te "sécuriser", mais à mon avis tu auras d'autres problèmes ailleurs. En gros, un FW c'est comme la ligne Maginot, qui, contrairement à ce qu'on pense, à super bien fonctionner - la preuve, Hitler est passé à coté, mais du coup, elle a pas servi à grand chose. Un FW c'est à peu prêt aussi inutile.

Perso, j'ai l'habitude de dire qu'on estimer la nullité crasse d'une sécurité par le nombre de port bloqué:
- je peux pas relever mes mails en POP, naze
- mon accès VPN est bloqué, encore plus naze
- SSH sortant est bloqué, stupide, un coup de tunnel HTTPS et je sors de toute manière.

La vrai sécurité avec les FW, c'est le filtrage applicatif, c'est à dire, non pas bloqué un protocole ou service, mais vérifier que celui-ci a un usage valide. Fais tu STMP si tu veux, mais sur ce port, je veux que du STMP, pas autre chose. Fais du ssh autant que tu veux, mais sur le port 22 et pas à travers HTTPS, et au passage, si tu fais tu ssh, je te loggue (etc...)

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

### Clouds looks nice from afar, but try piloting your Cessna through one !

FLD: Ok, tout ça a plutôt marcher, mais maintenant, on va se débarrasser notre infra à nous, et migrer notre app, sur le Cloud. Vu qu'elle est déjà "secure", je dois revoir ma copie tu crois ?

RPE: Ben oauis, et plutôt deux fois qu'une ! Parce que maintenant, si tu applis par en sucette, ton provider Web, va littéralement tu le faire payer.

FLD: Ah oui, comme le mec qui a voulu apprendre Ruby...

a $2.375 amazon mistake
http://www.devfactor.net/2014/12/30/2375-amazon-mistake/

### never assume the system you are talking to is safe

FLD: Ah oauis, ça fait mal tout ça, surtout qu'on pensait s'intégrer avec S3. Du coup, on va peut être aller voir ailleurs.

RPE: Oui, mais ça change rien, dès l'instant où tu t'intègres avec un système externe, il faut grosso modo partir du principe qu'il est pas 'secure' et te protéger de lui.

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

https://www.techn0polis.net/wp-content/uploads/2015/01/security.png

a ce propos

dans jhipster tu as une page d'audit de secu.

nous en plus, on a prévu le coup si un des nos utilisateurs perd son laptop, on reset son token



=> excellent !

### safer in the cloud

FLD: Bon, en gros, au final, le cloud c'est la jungle, et on est plus secure chez soi en fait ?

RPE: Non, au contraire ! Le cloud te force à faire plus gaffe à ta sécurité, pour toutes les raisons qu'on vient d'évoquer, mais t'apportes bcp en termes de sécurité. Y'a qu'on bien de système non maintenu, qui tourne depuis 10 ans, sans le moindre de security patch appliqué dans ton infra ?

FLD: (gros sourire) ben aucun bien sûr ;) !

RPE: Exactement ;) - dans le cloud tes machines sont constament reconstruit "fraîche" et patché (là RPE parle de Netflix)

=> là je peux expliquer le cas de Netflix où justement, aucun serveur en prod ne dure que qql
jours... plus leur approche "Choas Monkey" qui est phénoménale !
http://techblog.netflix.com/2012/07/chaos-monkey-released-into-wild.html

a 10 years old server in your data center is much more vulnerable than a fresh server in the cloud

a 10 years old server, imagine

* accumulated rot
* configuration shift
* quaterly security review ? this clash with continous delivery

a typical aws server last a few days

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

@FLD: bof, moi je suis contre les stratégie consiste à fermer/bloquer les trucs. Je préfère surveiller
que le traffique est sain et correspond aux attentes. Je pense qu'on peut avoir un micro débat sur ce sujet, c'est intéressant. Et genre, tu pourrais conclure "ben dans tout les cas, moi je le fais co ça, si ce n'est que pour te faire chier !" :) 

git and jenkins , chef, vagrant exploits
https://twitter.com/morlhon/status/554899543150850048

A must-read  : @paulgreg: interesting slide on security of your webapp "DevOoops"  by @carnal0wnage #devops #hacking http://www.slideshare.net/chrisgates/lascon-2014-devooops …”

-> le spoof de Git Hub est intéressant, car c'est un bon exemple d'exploit "social". On peut
imaginer une PR sur un projet prétendant venir de XXX insérant une faille... Je pense qu'il faut
qu'on mentionne que le "hack" social reste une des principales failles de sécurité.

### Avoid security scan false positive

false positive overload : http://infosecnirvana.com/false-positive-in-a-siem/

avoid false positive:

checksum on sensitive directory only
file integrity monitoring tool
http://www.cloudpassage.com/

splunk enterprise security analytics

CONCLUSION

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



rate limiting => @FLD, tu pensais à quoi là ? Tu as un truc jhipster sur ce point ?.

update your linux (ghost) we you have docker ! fun !

http://googlecloudplatform.blogspot.fr/2015/02/using-google-cloud-platform-for.html

gemalto hacked : https://firstlook.org/theintercept/2015/02/19/great-sim-heist

vous avez été espionné?
http://www.numerama.com/magazine/32243-avez-vous-ete-espionne-par-la-nsa-voici-une-chance-de-le-savoir.html

siemens stuxnet credentials in the source code
http://en.wikipedia.org/wiki/Stuxnet

https://twitter.com/codinghorror/status/567434195987738624
The best reaction to "this is confusing, where are the docs" is to rewrite the feature to make it less confusing, not write more docs.

* a1 : I hide headers info to avoid easy exploit : Wappalyzer screenshot
* a2 : exploits is not such a big deal anymore




