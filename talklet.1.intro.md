`Talklet 1` Intro 
====

fond d'ecran si wifi
http://map.ipviking.com/


Bonjour
-------

`FLD` Bonjour à tous, nous sommes ravis d'être avec vous aujourd'hui....


Présentations
------

`RPE` je m'appelle Romain...


`FLD` je m'apelle Francois...


Ce ne sera pas un audit
----

`RPE` on y va Francois ? on a promis un "audit de sécurité" en 45 mn

`FLD` oui... mais non

`RPE` ?

`FLD` Mon archi n'est pas sèche et mes dévelopements en sont encore em mode POC et j'ai pas encore staffé toute l'équipe

`RPE` c'est parfait, c'est le meilleur moment

`FLD` ?

`RPE` TODO


`FLD` Ouais, mais attend l'architecte a rasé sa barbe la semaine dernière, personne n'est calé en sécurité

`RPE` commençons par le début, parlez moi un peu de ton appli, c'est du Java j'imagine ?(je sens déjà le jar de 200Mb arriver...)

 
 Ma petite appli
 --------
 

`FLD` c'est une appli web intranet, c'est pas une appli pour placer des pubs,  c'est pas big data, pas trop social, pas très hipster, mais comme je voulais me faire plaisir je suis parti sur un stack jhipster

`RPE` c'est quoi jhipster ? Encore un framework MVC ? Un truc qui springboot pour lancer un container scala écrit en JRuby qui exécute des greffons groovy ?

`FLD` c'est un generateur d'appli web à la appfuse

`RPE` appFuse, moi oui, mais les jeunes dans la salle je suis pas sûr...

`FLD` Justement ces jeunes dont tu parles connaissent javascript et yeoman. JHipser est basé sur yeoman. tu commences par ce script:

`FLD` yo jHipster

`FLD` Tu fais quelques choix 

`FLD` le résultatun stack assez lean, plutot recent avec du springboot pour la partie serveur et du angularjs pour le partie cliente


`RPE` ok, bon  à part télécharger la terre entière pour foutre je ne sais combien de couche d'abstraction à la Java, je vois surtout t'es parti sur du oauth2 et du mongodb. MongoDB c'est pour faire cool et dragué les filles sur la plage, c'est ça ?

`FLD` : :-)


`FLD` Ce qui me fait peur c'est ce genre de chiffre :

http://www.ivizsecurity.com/blog/penetration-testing/web-application-vulnerability-statistics-of-2012/

* 99% of web applications have at least 1 vulnerability
* 82% of web applications have at least 1 High/Critical Vulnerability
* 90% of hacking incidents are not reported publicly

Sécurité : Java serait le programme le plus exposé aux attaques, suivi par QuickTime, Adobe Reader, VLC et .Net§...

https://twitter.com/Developpez/status/560389865003425792
http://bit.ly/1zaB89X

`FLD` ce qui me rassure c'est que je suis en Intranet


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

