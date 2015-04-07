`Talklet 1` Intro
====

`slide-1`
------

fond d'ecran si wifi - ou avoir un "film" du site de 10" si Wifi pourri
http://map.ipviking.com/

J'ai une video de 5mn avec Adobe Captivate


`slide-2` Bonjour
-------

`FLD` Bonjour à tous, nous sommes ravis d'être avec vous aujourd'hui.

`slide-3` Présentations Romain
------

`RPE` je m'appelle Romain, je suis développeur Java chez Red Hat - donc dans la branche JBoss. Je suis tombé dans le "café Open Source" quand j'étais petit, d'ailleurs, avec François, et depuis cette époque chez Atos, c'est l'Open Source, qu'il s'agisse de Linux ou du monde JEE qui a guidé ma carrière, sans surprise, jusqu'à Red Hat (What else ? ). Pendant mes 3 premières années chez Red Hat, j'ai tenu le rôle de consultant, puis d'architecte, et je ne suis passé développeur que depuis peu, donc ne soyez pas surpris si je mentionne des "cas clients" ou des mises en production. Tout ceci étaient mon pain quotidien, il y a encoe quelques moi.

`slide-4` Présentations Francois
------

`FLD` je m'apelle Francois, je suis développeur, chez Adobe IT, je monte des backend en Java, je fais un peu d'ops avec Chef et un peu de front en html javascript et css ...


Ce ne sera pas un audit
----

#### `slide-5` audit ?


`RPE` on y va Francois ? Tu l'air vendu un "audit de sécurité" en 45 mn, non, c'est ça ?

#### `slide-6` non pas un audit

`FLD` oui... mais non

`RPE` Ah bon ? Bon, ça tombe bien ça me casse les pieds les audit !

`FLD` Je ne crois pas être prêt, non... je me sens pas armé pour un audit de sécurité... On en est encore au stade du POC... mon archi n'est pas sèche et mes dévelopements en sont encore en cours... j'ai pas encore staffé toute l'équipe... donc on n'est pas en position de faire un audit.

`RPE` Tu réalises que la différence entre un Poc et une appli en prod, c'est juste que personne n'a encore mis le PoC en prod ? ;) Bref, si tu as réellement inquiet pour la sécurité, il vaut mieux commencer dès maintenant, car il n'y aura pas de "miracle" d'ici la production. J'ai vu des systèmes avoir comme mot de passe "password", avec un joli document indiquant, en rouge,  "à changer avant la mise en prod", et ... devine le mot de passe en production trois mois plus tard ?

(@Public: "Riez pas, c'est vrai, et si ça se trouve, c'était vous sur le projet !")

`RPE` Bref, à quoi tu as pensé déjà ? Qu'as tu regardé ?

#### `slide-7` xss csrf ?

`FLD` Je pense que la plupart des développeurs connaissent les classiques, je pense qu'on saura se prémunir contre les attaques de type injection, cross site scripting et cross request forgery, et le stack sur lequel on est parti fera le plus gros de ce travail pour nous...

#### `slide-8` non pas on parle pas de xss csrf

`RPE` Très, bien, bon débarassas, parlons d'autees choses alors !

#### `slide-9` xss Rachida

`RPE` ... même si les attaques XSS ce serait un bon rappel pour les dev qui bossaient pour le site de Rachida Dati

`FLD` et un bon rappel le procureur de Paris.

`RPE` Je crois que là, pour le moment, il doit probablement essayer de relire la page wikipedia sur le sujet. Qu'il doit trouvé confus et incompréhensible. Un juriste qui trouve un texte, confus, si c'est pas de l'ironie ça...

#### `slide-10` Security By Design

`FLD` Oui mes besoins en sécurité vont plus loin ... et puis l'architecte du projet s'est marié, a donc a rasé sa barbe, a eu des enfants et ne code plus la nuit... personne dans l'équipe n'est un expert en sécurité

`RPE` Sachant que j'ai étais souvent architecte dans ma carrière, si un archi s'était calé en sécurité - ça se saurait et je le serais !!! En fait, on va le voir ensemble, mais la sécu touche plein de truc, donc on peut pas vraiment avoir un expert ou un spécialiste. C'est plutôt un truc de "awareness" - comme dirait des hippies de San Francisco.

`FLD` Tu as raison, la sécurité impacte, l'ensemble du projet, nous seuleument les développeurs, mais aussi bien sûr les opérations, mais aussi l'intégration continue et l'expérience utilisateurs. Elle impacte ainsi l'ensemble des acteurs  du projet. C'est pour parler de ça qu'on est venu ici aujourd'hui

`RPE`:  En outre, je vois mal comment des experts externes pourront mieux sécuriser ton appli que tes devs et toi. Eventuellement, ton infra se sécu. Mais à la base, pour hacker une appli, il faut la détourner de son fonctionnement "normal". Et, à ton avis, de tes fameux experts en sécurité et ton équipe de dév qui connait mieux le fonctionnement normal de l'appli ? Et donc se prémunir contre son détournement ?

`RPE` La sécurité, c'est comme tout le reste, ça se fait en continue.  Bon, allez, commençons par le début, parles moi un peu de ton appli, c'est du Java j'imagine ou tu as enfin appris un vrai language pour homme ;) ?

`slide-11` Notre cas d'étude
---

`FLD` c'est une appli web intranet, c'est pas une appli pour placer des pubs,  c'est pas big data, pas trop social, pas très hipster,

`slide-12` JHipster
---

mais comme je voulais me faire plaisir je suis parti sur un stack jhipster

`RPE` c'est quoi jhipster ? Encore un framework MVC ? Un truc qui springboot ton app pour lancer un container Scala, lui-même écrit en JRuby, qui exécute des greffons Groovy, avec une extension en cours de fabrication pour trouver une excuse pour utilser Ceylon ou Closure ?

(@Public, riez pas, et si l'un de vous pense que c'est une bonne idée, je le descend).

`FLD` Ouais, exactement ! :) Non, c'est un generateur d'appli web à la appfuse - pour ceux qui s'en rappelle

`RPE` (vers la salle), si vous vous en rappellez, j'ai une mauvaise nouvelle pour vous : vous êtes vieux.

`slide-13` Yo JHipster
---

`FLD` Quant aux jeunes et à ceux qui sont su resté jeunes connaissent certainement javascript et yeoman. JHipser est basé sur yeoman. tu commences par ce script:

`FLD` yo jHipster

`FLD` Tu fais quelques choix ? East Coast ou West Coast ?

`FLD` le résultat est une stack assez lean, plutot récente avec du springboot pour la partie serveur et du angularjs pour le partie cliente

`RPE` ok, bon  à part télécharger la terre entière pour foutre je ne sais combien de couche d'abstraction à la mode Java, je vois surtout t'es parti sur du oauth2 et du mongodb. MongoDB c'est pour faire cool et draguer les filles sur la plage, c'est ça ?

`FLD` Exactement ! :-)

`slide-14` Spring Security
---

`FLD` Plus sérieusement, ce qui m'a attiré dans ce stack c'est aussi la tringlerie Spring security qui vient avec.
Il m'offre une bonne base de travail pour gérer l'authentication, l'authorisation, les roles. Il me fournit une solution contre les attaques de type Cross site scripting forgery à base crsf Token, et me fournit une bonne trame pour l'audit et logs relatifs à la sécurité.

`FLD` ce qui me rassure beaucoup  également c'est que je suis en Intranet



=======
========




`Talklet 1` old draft
==================


### Notre but :

FLD: "audit" on a ce mot dans notre abstract, mais en fait on veut pas vraiment faire un audit une fois tout developpé, on veut changer l'etat d'esprit du dev et de lops pour les sensbiliser à la sécu, on veut montrer plutot comme l'archi, la qa, le dev, l'ops sont partie prenante de la secu et comment la secu se fait "by design" tout au long du projet... en gros le concept d'audit de secu est naze...

audit non
------------

FLD: Romain, on n'a une petit appli interne, qu'on va mettre en prod, et on m'a dit de faire un audit de sécurité.

RPE: Pourquoi ? C'est déjà trop tard...

FLD: Ben, c'est pas le moment de faire un audit de sécurité ? On voulait faire venir des experts en sécurité.

RPE: Pourquoi faire ? Tu veux qu'il te reconfigure ton FW ? Honnêtement, je vois mal comment des experts externes pourront mieux sécuriser ton appli que tes devs et toi. Eventuellement, ton infra se sécu, mais à la base, pour hacker une appli, il faut la détourner de son fonctionnement "normal". Et, à ton avis, de tes fameux experts en sécurité et ton équipe de dév qui connait mieux le fonctionnement normal de l'appli ?

FLD: Ouais, mais attend mon équipe de dév, y'en a la moitié déjà qui travaille sur Windows, l'autre sous OSX, et l'architecte a rasé sa barbe la semaine dernière - bref, personne n'est calé en sécurité, on va pas faire ça tout seul.

RPE: Non, mais vous allez aire ça ensemble... Bon allez, commençons par le début, parlez moi un peu de ton bouzin en Java (je sens déjà le jar de 200Mb arriver...)

jhipster ?
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


web app Java
-------

RPE: donc c'est une web app...
FLD: OUi je sais ce que tu vas me dire:

http://www.ivizsecurity.com/blog/penetration-testing/web-application-vulnerability-statistics-of-2012/

* 99% of web applications have at least 1 vulnerability
* 82% of web applications have at least 1 High/Critical Vulnerability
* 90% of hacking incidents are not reported publicly

Sécurité : Java serait le programme le plus exposé aux attaques, suivi par QuickTime, Adobe Reader, VLC et .Net§...

https://twitter.com/Developpez/status/560389865003425792
http://bit.ly/1zaB89X

