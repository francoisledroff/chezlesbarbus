`Talklet 5` Auth
==========

todo



`Talklet 5` Draft
==========


Password regles et limites
------

RPE: Ah je vois que par défaut, jhipster a sa propre base de donnees d'utilisateur, pas mal pour le dev, mais une cata pour la prod !

FLD: Ouais, mais attend, c'est pas si naze, puis, par défaut, on s'est assuré que tout les mots de passe seraient "strong" (à dév) pour éviter ca http://www.ayblog.com/wp-content/uploads/2013/10/Nice-Change-of-Password-to-Incorrect.jpg

RPE: mouais, tu veux implementer ca : http://www.medsyn.fr/perso/g.perrin/joomla/images/stories/food/Blog/mot-passe2.jpg
ou ca https://theeditorsjournal.files.wordpress.com/2014/09/creating-a-password.jpg?w=1240&h=1248

FLD: c'est vrai, que ces strong passwords sont just difficile a retenir mais pas à craquer : http://xkcd.com/936/

RPE: Oui, d'ailleurs toute ma famille se plaint que le mot de passe du wifi à la campagne est trop long ! Pourtant "Romain a des plus jolie cheveux que ses soeurs", c'est pas compliqué à retenir, non ? :)

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


FLD: on est donc d'accord : pour faire court, les mots de passe, c'est juste "mal". Tu sais, comme croiser les effluves ? ;) D'ailleurs, 100% des attaques en 2014 implique des mots de dérobé.

http://idtheftcenter.org/

RPE: Bref, comme je le dis souvent, si tu veux pas de divorce, te marie pas, ben pareil, si tu veux pas qu'on te vole to password, t'as qu'à pas en avoir !

FLD: on souffre tous, on doit tous gerer à notre echelle une ribambelle de mot de passe, moi j'utilise splashid pour stocker et generer mes mots de passe, aucune synchro sur le cloud, juste une synchro entre device. J'ai actuellement 159 mots de passe dans cette base, je ne voudrais pas en créer un autre...

et vous ? carnet ? lastpass ? one password ?


RPE: TODO prob dew revocation


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


