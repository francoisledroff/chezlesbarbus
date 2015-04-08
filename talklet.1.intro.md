`Talklet 1` Intro
====

`slide-1`
------

fond d'ecran si wifi - ou avoir un "film" du site de 10" si Wifi pourri
http://map.ipviking.com/

J'ai une video de 5mn avec Adobe Captivate


`slide-2` Bonjour
-------

`FLD` Bonjour à tous, nous sommes ravis d'être avec vous aujourd'hui. On va commencer par se présenter rapidement...

`slide-3` Présentations Romain
------

`RPE` Oui, alors "Salut à tous", je m'appelle Romain, je suis développeur Java chez Red Hat - donc dans la branche JBoss. Je suis tombé dans le "café Open Source" quand j'étais petit, d'ailleurs, avec François, et depuis cette époque chez Atos, c'est l'Open Source, qu'il s'agisse de Linux ou du monde JEE qui a guidé ma carrière, sans surprise, jusqu'à Red Hat (What else ? ). Pendant mes 3 premières années chez Red Hat, j'ai tenu le rôle de consultant, puis d'architecte, et je ne suis passé développeur que depuis peu, donc ne soyez pas surpris si je mentionne des "cas clients" ou des mises en production. Tout ceci étaient mon pain quotidien, il y a encore quelques mois. A toi FLD,

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

`FLD` ... je me sens pas armé pour un audit de sécurité... On en est encore au stade du POC... mon archi n'est pas sèche et mes dévelopements en sont encore en cours... j'ai pas encore staffé toute l'équipe...  on n'est pas en position de faire un audit.

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

`FLD` je pense pourtant que mes besoins en sécurité sont importants et determinant pour la reussite du projet et pour la perennité de mon SI... mais voila......  l'architecte s'est marié, a rasé sa barbe, a eu des enfants ... ne code plus la nuit... et aucun programmeur de l'équipe n'est un expert en sécurité

`RPE` j'ai souvent été  architecte dans ma carrière, si un archi s'était calé en sécurité - je le serais ! En fait, on va le voir ensemble, mais la sécu touche plein de truc, donc on peut pas vraiment avoir un expert ou un spécialiste. C'est plutôt un truc de "awareness" - comme dirait des hippies de San Francisco.

`FLD` Tu as raison, la sécurité impacte, l'ensemble du projet, nous seuleument les développeurs, les opérations, mais aussi l'intégration continue et l'expérience utilisateurs. Elle impacte  l'ensemble des acteurs  du projet. C'est pour parler de ça qu'on est venu ici aujourd'hui

`RPE`:  En outre, je vois mal comment des experts externes pourront mieux sécuriser ton appli que tes devs et toi. Eventuellement, ton infra se sécu. Mais à la base, pour hacker une appli, il faut la détourner de son fonctionnement "normal". Et, à ton avis, de tes fameux experts en sécurité et ton équipe de dév qui connait mieux le fonctionnement normal de l'appli ? Et donc se prémunir contre son détournement ?

`RPE` La sécurité, c'est comme tout le reste, ça se fait en continue.  Bon, allez, commençons par le début, parles moi un peu de ton appli, c'est du Java j'imagine ou tu as enfin appris un vrai language pour homme ;) ?

`slide-11` Notre cas d'étude
---

`FLD` c'est pas une appli pour placer des pubs, ni pour spéculer sur les marchés financier, ce n'est donc ni big data, ni social, ni très hipster... c'est juste une appli web de gestion

`slide-12` JHipster
---

`FLD` mais comme je voulais me faire plaisir je suis parti sur un stack jhipster

`RPE` c'est quoi jhipster ? Encore un framework MVC ? Un truc qui springboot pour lancer un container scala écrit en JRuby qui exécute des greffons Groovy, avec une extension en cours de fabrication pour trouver une excuse pour utiliser Ceylon ou Closure ?

`FLD` Ouais, exactement ! :) Non, c'est un generateur d'appli web à la appfuse - pour ceux qui s'en rappelle

`RPE` (vers la salle), si vous vous en rappellez, j'ai une mauvaise nouvelle pour vous : vous êtes vieux.

`slide-13` Yo JHipster
---

`FLD` Quant aux jeunes et à ceux qui sont su resté jeunes, eux connaissent certainement javascript et yeoman. JHipser est basé sur yeoman. tu commences par ce script:

`FLD` yo jHipster

`FLD` Tu fais quelques choix ? East Coast ou West Coast ?

`slide-14` JHipster homepage
---

`FLD` le résultat est une stack assez lean, plutot récent avec du springboot pour la partie serveur et du angularjs pour le partie cliente

`RPE` ok, bon  à part télécharger la terre entière pour foutre je ne sais combien de couche d'abstraction à la mode Java, je vois surtout t'es parti sur du oauth2 et du mongodb. MongoDB c'est pour faire cool et draguer les filles sur la plage, c'est ça ?

`FLD` Exactement ! :-)

`slide-15` Spring Security
---

`FLD` Plus sérieusement, ce qui m'a attiré dans ce stack c'est aussi la tringlerie Spring security qui vient avec.
Il m'offre une bonne base de travail pour gérer l'authentication, l'authorisation, les roles. Il me fournit une solution contre les attaques de type Cross site scripting forgery à base crsf Token, et me fournit une bonne trame pour l'audit et logs relatifs à la sécurité.

`RPE` Ouais, c'est plutôt chouette en effet tout ça.

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
