`Talklet 5` Auth
==========

`slide-28` JHipster login page
-----------

`RPE` Ah je vois que par défaut, jhipster a sa propre base de donnees d'utilisateur, pas mal pour le dev, mais une cata pour la prod !

`FLD` une véritable plaie, non seuleument pour la sécurité mais également pour l'expérience utilisateur.
En tant qu'utilisateur je trouve difficile à justifier.

Je ne pense pas être le seul, le simple fait de devoir creer et gerer un n-ieme mot de passe peut dramatiquement reduire la retention d'utilisateurs.
  
Pourquoi devrai-je à nouveau créer un nouveau mot de passe ?
Si votre site est publique, pourquoi ne pas me proposer de me logger avec openid, facebook, google, twitter et surtout github si votre public est un public developpeurs.

`RPE` et la je dis merci ou cfp.devoxx...

`FLD` Si votre site est pro, vous avez surement un ldap ou mieux un identity provider ? 

`slide-29` Votre mot de passe (xkcd)
--------

`FLD` Autres questions qui me viennent à l'esprit devant ce genre d'ecran :

Quelles seront les règles spécifiques à ce nouveau mot de passe ?
Va-t-il encore m'imposer des contraintes inèptes relatives à l'ulisation des caractères speciaux et  
chiffres ?

`RPE` Je suis assez fan de ces pass phrase mais toute ma famille se plaint que le mot de passe du wifi à la campagne est trop long ! Pourtant "Romain a des plus jolie cheveux que ses soeurs", c'est pas compliqué à retenir, non ? :)

`FLD` "Romain a des plus jolie cheveux que ses soeurs" 46 caractères dans jhipster 46 characters ca passe mais de justesse... 
La seule contrainte imposée sur ce mot de passe c'est qu'il doit faire entre 6 et 50 caractères.




`slide-30` 1 mot de passe (incorrect)
--------

 `FLD` rien ne m'empêche non plus de choisir un mot de passe "incorrect" 

`RPE` Cette  mauvaise experience utilsateur entraine une reutilisation des mots de passe.

Qui d'entre vous utilise le même mot de passe sur plus d'un site ?

`FLD` pas moi ;-) Et j'en décompte 156 

`slide-31`  156 mots de passe ?
--------

`FLD` je les génère,  les renouvelle, les chiffres, les stock sur mon disque
et pour ca forcemment j'ai un outil


`slide-32` 1 chien ?
------

`RPE` t'as 156 mot de passe, mais a quoi bon ? je connais le nom de ton chien, et celui de Paris Hilton également

`note` on respire, on laisse les gens rigoler

`RPE` ok tout le monde a reconnu Paris Hilton ? 

Paris s'est fait hacke sous compte telephone chez T-Mobile qui pour protéger le mot de passe de ses clients 

T-Mobile n'avait pas choisie une question bien originale... 
Mais est-il si facile de trouver des questions dont les réponses ne soit déjà partagés sur le web à travers reseaux sociaux, blogs, tabloids, et journaux 

`FLD` en meme temps qui voudrait vraiment partager un vrai secret avec son operateur telephonique ? 

`slide-33` des Secrets ? (tweets)
------

`RPE` qui voudrait partager ses secrets avec avec facebook, snapchat, meetic, tinder, gleeden ?

`FLD` Mais qui ne partage quelques secrets avec son banquier ?

`RPE` Et qui n'utilise pas de carte à puces, des cartes SIM ?

`FLD` Dans la vraie vie, un secret c'est quelque chose que vous ne partagez qu'avec une seule personne à la fois.

`RPE` et dans le vraie vie comme sur le web tout des oreilles trainent

`slide-34` 100%
------

`FLD` on est donc d'accord : pour faire court, les mots de passe, c'est juste "mal".

`note` pause respiration, on laisse lire le public

`RPE`  Bref, comme je le dis souvent, si tu veux pas de divorce, te marie pas, ben pareil, si tu veux pas qu'on te vole to password, t'as qu'à pas en avoir !

`FLD` Notre but :
N’être qu’un fournisseur de service
Identifier un fournissseur d’identité de confiance
S’y interfacer

`RPE` A qui peut-on faire confiance ?

`FLD` c'est toute la difficulté


`slide-35` 1 IDP ?
-------

`RPE` : Adobe, comme nous Red Hat, vous avez forcemment fait un choix, vous avez une solution de gestion d'identité ? 

Si vous n'avez pas, je crois qu'on en vends 4 différents au dernier compte ! (Si vous prenez une paire de QUeue JMS, en plus, on fait un prix ;) ).


`FLD`  Oui bien sûr, j'ai donc modifié mon appli généré, 

 
`RPE` ok donc tu présentes donc cette page a mister anonymous, et tu lui propose un lien vers une resource protégé par ton fournisseur d'idendité


`slide-36` SAML ?
-------

`FLD` Oui mon IDP comme la plupart des solutions supporte le standard SAML

c'est un standard qui permet de faire du SSO sur le browser.
si vous voulez débutez et tester votre solution, jetez un coup d'oeil à www.ssocircle.com 


`slide-37` SAML & JHipster ?
-------
`RPE` Mais dis, JHipster ne supporte pas saml

`FLD` non, 
mais Spring Security le fait. 

j'ai viré la gestion de mot de passe, j'ai viré pas mal de code, j'en ai rajouté un peu, j'ai pas mal trébuché, fini avec peu de code et beaucoup d'annotations

`FLD` a choisir je préfère tout de même l'annotation hell au xml hell....
Et Spring Security s'y prête plutot bien.

`RPE` a Quand ton pull request ?
oui c'est en projet, il y a deja un ticket le 695 qui lui associé.


`slide-38` SAML Sequence Diagram
-------

`RPE` Alors Saml ? comment ça marche ?

`FLD` Le plus compliqué finalement, c'est la config.

* il faut recuperer le meta données de l'idp et fournir a ton moteur client saml
elle contienne un certificat et des url à associer à la redirection en vue d'un login ou tout au moins d'une verification  d'identité
* et toi tu fournis à l'idp, quelques metadonnées comme
  *  certificats et url associer à la redirection en vue d'un login et logout.
  
`RPE` ok donc tu présentes donc cette page a mister anonymous, et tu lui propose un lien vers une resource protégé 

`FLD` mon fournisseur de service dit 

* "Not authorized", je te connais pas, je te donne pas le service, je te donne pas la resource, 
* va prouver ton identité au pres du fournisseur d'identité, 
* il reviendra vers moi, 
* si son retour est valide, je te donnerai accès à ma resource 
* tout du moins si les infos d'idendité extraite dans l'enveloppe saml me permette de te donner le role necessaire pour etre autorise à acceder a ce service ou cette resource.



`slide-39` login link
-------

`RPE` ok donc tu présentes donc cette page a mister anonymous, et tu lui propose un lien vers une resource protégé 

`FLD` oui la resource demandé demande un role user, role uniquement attribué si mon IDP valide l'identité de mon
utilisateur. 
 

`slide-40` okta 1 factor
-------

`RPE` ok donc tu es redirigé ici sur ton idp, tu rentres un mot de passe
`FLD` oui ici mon mot de passe ldap sur adobeNet


`slide-41` okta 2nd factor
-------

`RPE` et t'as demandé a ton IDP d'appliquer un second facteur.

`FLD` Oui le user doit me prouver, me donner
 
 * ce qu'il sait : son password
 * ce qu'il a : un telephone ou autre generateur de token
 
 
`slide-42` logged-in
-------
 
 `RPE` c'est pas relou ca pour les utilsateurs ?
 
 `FLD` si, mais c'est indispensable vu le niveau de confidentialité de leurs données.
 


`slide-43` wired
----

`RPE`

vous connaissize Paris Hilton ?
vous connaissez ce gars ?
vous devriez !

pas le temps de raconter son histoire, ou alors on le laisse pour le q&A

`FLD`
mais quand vous aurez lu son histoire, cet article sur wired.
Tou comme moi vous allez activer le 2fa chez tous les fournisseurs de vos identitiés digitales

je l'ai active sur mon compte twitter, facebook, google, 

paypal, github



`slide-34` 2FA
----

`RPE` en tant que developpeurs il est de votre responsabilité de protéger vos secrets, vous êtes la cible des hackers

`FLD` vous avez votre profil sur linked-in, et vous êtes devops ou security specialist chez BNP ou 1 ms valent 100 millions d'euros ? et dont le portefeuille de produits dérivés em 2013 s’élevait à 48 000 milliards d’euros, soit 24 fois le PIB de la France

http://www.lemonde.fr/economie/article/2013/12/17/les-produits-derives-depassent-leur-niveau-d-avant-crise_4335868_3234.html

`RPE` 1ms pur 100 millions, 1 sec 100 milliards, un hack de 8 minutes seconde suffirait-il pour jouer 24 fois le PIB de la France sur les marchés ?

`RPE` en tant que dev ou ops vous êtes une cible .

`FLD` allez faire un tour sur twofactors.org, voyez ou vous pouvez activer le 2FA, et faites vos choix en fonction

`RPE` laissez tomber docker

`FLD` preferez github a bitbucket

`RPE` on remarquera qu'elle est bien secure la finance en ligne

`FLD` que l'internet of things et les applis santé font globalement fi de la securité

`RPE` pareil pour la plupart des micro paiement






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
