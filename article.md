Chapeau de l'article

François Le Droff et Romain Pelisse, lors de Devoxx France 2015, ont donné une présentation, fort à propos, le lendemain de l'attque contre la chaine de télévision TV5,  sur la problématique des applicatifs Java et la sécurité. Cette article se propose de reprendre le contenu de cette conférence, bien évidemment de manière plus didactique, et adapté à ce nouveau support. En outre, le format papier va permettre de développer certains points techniques, seulement esquisé lors de la présentation.


Intro

`FLD` Dis Romain, je suis entrain de monter une sympathique petite application en interne, mais je m'inquiète un peu de l'aspect sécurité, surtout que je ne me sens pas armé pour un audit ! On en est encore au stade du prototype, mon archi n'est pas sèche et mes dévelopements sont encore en cours... Je n''ai même pas encore staffé toute l'équipe... Bref, comment m'y prendre ?

`RPE` Ben déjà c'est bien de s'y prendre dès maintenant. Les audits "adhoc", qui arrivent à la fin des développements, quand justement les personnes clés du projet sont souvent déjà partie, de mon point de vue, ça ne marche pas souvent. En outre, comme tu vas le voir, la sécurité, c'est comme tout le reste dans le développement logiciel - c'est un travail d'équipe ! Mais c'est vrai que s'est souvent difficile de trouver un "bon point de départ".

Theat Modelling

`FLD` Ben justement, y'a une méthode que je trouve très intéressante et qui est poussée par Microsoft et OWASP. Elle s'appelle le "Threat Modeling". A l'aide de deux acronymes, STRIDE et DREAD, elle donne, je trouve, une bonne vision d'ensemble, qui permet d'une part d'identifier les menaces, et d'autres part, de prioritiser les points à adresser.

`RPE` Super ! Commençons alors par STRIDE, qu'est ce que ça veut dire ?


`FLD` Avec l'acronyme STRIDE, la méthodologie propose une categories d'attaques possibles selon les types d'exploitation qui leur sont associés. Ensuite, à chaque categorie correspond des mesures à mettre en place.

`RPE` Alors on va rester didactique, et pas tout expliciter, sinon, on va y passer tout l'article ! Prenons donc juste un exemple concret. Par exemple, que signifie concrètement le R de repudiation ?


`FLD` Cette catégorie sert à éviter que les utilisateurs contestent les transactions faites avec leur identifiants et depuis leur machines. En bref, l'idée de ne jamais oublier de mettre en place un "audit trail" sur chacun de vos tiers applicatifs.

`RPE` En effet, si on doit inputer à quelqu'un une manipulation malhonnête sur une transaction, c'est bien de pouvoir le prouvé sans l'ombre d'un doute. Et alors, le second acronymes, DREAD ?

`FLD` Avec l'acronyme DREAD, le Threat Modeling propose également un système de classification pour comparer, qualifier et prioritiser les risques associés à chaque menaces.

@FLD, du coup, on pourrait développer une chouille plus DREAD dans l'article.

`RPE` Au final, tu as donc un shema d'archi orientée sécurité, d'assez haut niveau, qui offre  une vue d'ensemble de l'applicatif et de ses défenses.

`FLD` En effet, et l'analyse auquel il s'associe aide grandement à décider quelle action entreprendre et quelle partie du systèmes renforcer. Maintenant, ce genre de diagramme convaic rarement les plus "geeks" de notre profession.

`RPE` C'est vrai, et c'est bien dommage, car cette méthodologie semble être une arme parfaite pour faire comprendre à un management un peu récalcitrant qu'il y a de réelles faiblesses dans le système. Dans un langage et un format qu'ils peuvent non seulement comprendre, mais aussi réutiliser pour convaincre leur propre hiérarchie.

`FLD` Exactement ! Et de manière complémentaire, effectuer ce genre d'inventaire, quand on fait justement parti du "management", est un excellent moyen de vérifier que vos développeurs n'ont pas, par négligence, manque de compétence sur le sujet ou simplement faute de temps, laisser quelques faiblesses critiques dans votre système.

`RPE` Bon, on s'arrête là, car on pourrait probablement faire un article entier sur le sujet de Threat Modelling. Maintenant, que nous avons une méthodologie pour avoir un bon point de départ, regardons donc ta petite application.

JHipster & SpringSecurity

`FLD` C'est une application très simple. Elle n'est pas conçu pour héberger de publicités, ni pour spéculer sur les marchés financier. Elle n'est donc pas très "big data", elle utilise pas de "hadoop" ou de "machine learning", elle ne sert pas non plus à faire du social.

`RPE` Attends, rassures moi, pour faire quand même un peu "cool" tu utilises au moins du Docker non ?

`FLD` Même pas ! Non, c'est juste une bonne vieille application web de gestion, mais j'ai quand même utilisé une "stack" un peu sexy: jhipster !

`RPE` c'est quoi jhipster ? Encore un framework MVC ? Un truc qui springboot pour lancer un container scala écrit en JRuby qui exécute des greffons Groovy ?

`FLD` Presque :) ! C'est un generateur d'appli web basé sur Yeoman:

@FLD, là du coup, on peut imaginer en dire plus sur tes choix à la création.

`FLD` Au bout du compte, l'application finit avec une stack assez simple et au goût du jour avec du SpringBoot pour la partie serveur et du AngularJS pour le partie cliente.

`RPE` Très bien, mais du point de vue sécurité, tout ceci ne semble pas apporter grand chose, non ?

`FLD` Justement, ce qui m'a attiré dans ce stack c'est aussi parce qu'elle vient avec Spring Security, et que ce dernier offre une bonne base de travail pour gérer l'authentication, l'authorisation et les roles. Mais aussi permet de contrer des attaques assez "classique" dans le monde Web.

`RPE` Oui, comme justement les attaques de types "man in the middle", je crois ?

`FLD` Oui, car le framework supporte HSTS, qui indique au client que seul https sera utilisé.

`RPE` Et aussi le "clickjacking" il me semble ?

@FLD: à développer
`FLD` frameOptions().sameOrigin()

`RPE` et mêmes je crois les attaques XSS, comme celles qui ont, il y a peu, fait beaucoup de tort au site de Rachida Dati ?

`FLD` Exactement, Spring Security contre ce genre d'attaques, mais aussi les attaques de types " Cross site scripting forgery", pour laquelle il fournit une solution  à "base crsf Token".

`RPE` Bref, ça protégère de beaucoup, mais ça n'aide pas beaucoup la langue française, hein ;) ?

`FLD` Et attend, il fournit aussi une bonne trame pour mettre en place l'audit et logs relatifs à la sécurité.

Firewall

@FLD, je ne sais pas si garder mon "rant" sur les FW ne va bouffer de la place pour rien, on ferait peut mieux de zapper (voir aussi le RP) pour détailler la patie SAML et Oauth ?

`RPE`: Et alors ? Quel rapport ? Les FW ça ne sert pas à sécuriser des applis... c'est juste de faire de la qualité réseau et d'épargner, le CPU. En gros, si un système reçoit un paquet pour un port "non utilisé", il le "drop" en kernal space, plutôt que de le faire remonter pour rien jusqu'au couche applicative.

Ca permet aussi de limiter ainsi les attaques de types "déni de service.

`FLD` Bref, ça fait de la qualité réseau en réduissant le traffique "inutile"...

Mais attends ça bloque des ports, donc ça empêche des attaques, non ?

`RPE`: Ouais, sauf que généralement quand tu as truc qui tourne sur un port, c'est que tu en as besoin, donc du coup, le port est ouvert.

Si tu es assez con pour laisser tourner un service dont tu n'as PAS besoin, ...

`FLD`: Bref, en gros, un FW c'est comme la ligne Maginot.

`RPE`
Sauf que contrairement à ce qu'on pense, elle a super bien fonctionné - la preuve, l'armée d'Hitler l'a soigneuseument contournée. Comme ton FW.

`FLD`: Et voilà 10 minutes et on a déjà atteint le point de Godwin.

`RPE` yes !

`FLD` Qu'est ce qu'on fait des ports ouverts alors ?

`RPE` On en verifie l'usage ! Si tu as ouvert un port pour envoyer des mails, on le laisse pas passer autre chose que du SMTP, par exemple.

`FLD` Ouais, mais si on me hack et qu'on se sert de mon app pour envoyer des spams ?

`RPE` Tu veux dire des mails informatifs sur les techniques d elargissement de ... ?

FLD sourire. respiration

`RPE`: En ccl, moi, j'ai l'habitude de dire qu'on estimer la nullité crasse d'un IT par le nombre de port bloqué:

`FLD` un IT ou on peux pas relever ses mails en POP,

`RPE` c'est naze

`FLD` un IT ou l'accès VPN est bloqué,

`RPE` encore plus naze

`FLD` ou le SSH sortant est bloqué

`RPE` toujours naze et stupide. Un coup de tunnel SSH over HTTPS, et tu sors.

`FLD` Et le proxy HTTP ?

`RPE` Pareil, tu passes au travers avec Corkscrew

`FLD` Par contre, si on a bloqué plein de ports, on est sûr d'avoir donné une illusion de sécurité et cassé les pieds à tout le monde dans la société...

`RPE` Ouais, ok, donc le truc c'est le filtrage applicatif,

`FLD` mais dis ? Les FW savent le faire ça?

`RPE`  en fait personellement je ne préfère pas le faire au niveau du FW ,

`FLD` oui c'est vrai qu'on a pas la main

`RPE` Et les équipes d'infrastructure n'ont généralement pas vraiment une assez bonne compréhension de l'application pour faire ça bien.

`FLD` comment tu fais ?

Reverse Proxy

`RPE` Mais, de nos jours, avec l'approche DevOps et des outils comme Puppet...

`FLD` ou Chef ! (gros sourire)

`RPE`  Bref, avec cette approche et ces outils, les équipes projets ont de plus en plus la main des composants d'infrastructure.

 par exemple, un serveur web en frontal. Genre, un nginx ou un apache qu'on place devant leur serveur d'app.

`FLD` Ben justement, sur ma petite appli intranet, puisqu'on était en mode Proto, on a pas eu le temps..

`RPE` C'est con ça,  Car en fait, quand tu un serveur web en frontal, tu peux t'en servir comme un reverse-proxy (RP).

pour faire simple, que, avant de retourner une requête vers ton serveur d'app, le RP va analyser son contenu

`FLD` et alors ?

`RPE`  si elle n'est pas conforme aux attentes de l'application il la dropped

comme par exemple l'ajout paramètres ou un contenu incohérent
(exemple date sur 200 carateres)

`FLD` ou encore de la validation de header http, l'ajout de token csrf, du throttling ou du rate limiting

`RPE` Tes aimes bien les mots anglais non ?

`FLD` mais on peux pas me le hacker aussi vite et bien le RP ?

`RPE` Plus difficilement, parce que la plupart des hacks se basent sur le fait de manipuler la réaction du serveur distant en abusant des requêtes qu'il accepte. Or le RP ne repond pas a ses reaquetes

`FLD` oui il se contente de les analyser et nettoyer.

`RPE` ce qui laisse donc très, très peu de marge à un attaquant pour le contourner.

`FLD` Pour résumer Romain, on peut dire que des firewalls sans filtrage applicatif, c'est comme une frontière sans douanier.

`RPE` Ou plutôt avec des douaniers qui arrêtent que les "honnêtes citoyen", sans jamais voir que les criminels passe à 20m de leur point de contrôle...

`FLD` ok donc on filtre, on nettoie mais on veut aussi recevoir et envoyer des données sur ce fameux reseau non ?

Data and Encryption

@FLD, même remarque que pour avant. Peut être qu'on peut déjà développer les parties plus "pratiques" et/ou "techniques", et après voir si on garde ou pas cette section.

Classification

`RPE` Et dis Tes données peuvent-elles être considérés comme confidentielles ?

`FLD` contrairement à un app store, un site d'ecommerce ou un backend uber, je ne stocke aucun moyen de paiement, je ne risque donc pas les voir fuiter vers le dark web.

`rpe` ok cool

`FLD`

Mais on prévois un beau mashup de données, c'est un "employee productivity tool", à travers mon app vont transiter des données que je ne voudrait pas voir fuiter, comme

* l'adresse, le numero telephone des employés
* les salaires
* des infos sur les deals en cours

ping pong

* PII
* super sensible confidentiel
* deals internal mais restriced




`FLD` Yes, on a donc plutot intérêt à faire du bon boulot.

`RPE` Ce qui veut dire, qu'il va falloir chiffrer la majorité du flux et de la persistence de ces données de bout en bout, car pour assurer la conidentialité, y'a peu que ça. qu'est ce que tu as prévu pour mettre ça en place ?


Chiffrer le front

`FLD` de bout en bout, commencons alors par le front, on prévoit évidemment de tout servir en https

`RPE` SSL c'est secure, mais faire ça correctement c'est tout un art.

`FLD` Et ça demande une surveillance et une veille techno constante,


`FLD` même les plus grands doivent gérer des situations de crise, vols de certificats, ou la propagation de certificat qu'ils non pas authorisés mais qui sont trustés par la plupart des navigateurs

`RPE` et souvenez vous, avec suffisamment de temps et de ressources, n'importe quelle chiffrement peut-etre cassé .

`FLD` scannez vous serveur https pour détecter les éventuelles vulnérabilités et obsolesances

`RPE` ok, pour le front, admettons qu'on soit bon, regardons le back.

Chiffrer le back


`RPE`  Contrairement à ces 40 000 db mongo en prod sur le web , t'as pas apris la confg par défaut ?

`FLD` Oui l'a fait, Mais il faut savoir que JHipster utilise un outil tier open source appelé mongeez

Cet outil a besoin des droits d'admin sur la base, c'est impossible à utiliser en prod pour nous,

`RPE` logique donc t'as mis en place une authentication et un ACL bien. Mais t'as chiffrer les données qui passe sur le cable entre ton serveur d'app et Mongo ? ou elle passe en clair ?

`FLD` on l'a fait oui, mais ce fut épique, par défaut le support n'est pas fourni dans les distro Mongo, il est disponible dans le code open source,

* il a donc fallu builder mongo depuis les sources.

`RPE` mais c'est vraiment pourri de devoir debuilder mongo...

`FLD` Il a fallu aussi coder l'authentication par certificat dans le stack spring-data, il n'y etait pas.

et t'as fait un pull request ?

`FLD` oui je compte fournir ce code à la communauté soit par un pull request sur le project JHIpster ou sur le project spring-data

`slide-25` Chiffrage au repos ?
-------

`RPE` une fois dans la base comment tu les protège ?

`FLD` j'hesite

`RPE` ecoute on pas le trop le temps mais je te conseille le chiffrage applicatif

`FLD` l'admin du mongo sera plus facile

`RPE` meilleure granularité et   données isolées.

`FLD` Bon on vient de parler l'authentication et l'authorisation de ton serveur app dans Mongo, mais parlons de l'auth tes utilisateurs sur ton front ?

Auth

`RPE` Ah je vois que par défaut, jhipster a sa propre base de donnees d'utilisateur, pas mal pour le dev, mais une cata pour la prod !

`FLD` une véritable plaie, non seuleument pour la sécurité mais également pour l'expérience utilisateur.
En tant qu'utilisateur je trouve difficile à justifier.

`RPE` t'es pas le seul, le simple fait de devoir creer et gerer un n-ieme mot de passe peut dramatiquement reduire la retention d'utilisateurs.

`FLD` Si votre site est publique, pourquoi ne pas me proposer de me logger avec openid, facebook, google, twitter et surtout github si votre public est un public developpeurs.

`RPE` et la je dis merci ou cfp.devoxx...

`FLD` Si votre site est pro, vous avez surement un ldap ou mieux un identity provider ?

`slide-29` Votre mot de passe (xkcd)
--------

`FLD` Autres questions qui me viennent à l'esprit devant ce genre d'ecran :

Quelles seront les règles spécifiques à ce nouveau mot de passe ?
Va-t-il encore m'imposer des contraintes inèptes relatives à l'ulisation des caractères speciaux et
chiffres ?

`respiration`

`RPE` depuis que j'ai vu ce xkcd Je suis assez fan de ces pass phrase mais toute ma famille se plaint que le mot de passe du wifi à la campagne est trop long ! Pourtant "Romain a des plus jolie cheveux que ses soeurs", c'est pas compliqué à retenir, non ? :)

`FLD` "Romain a des plus jolie cheveux que ses soeurs" 46 caractères dans jhipster 46 characters ca passe mais de justesse...
La seule contrainte imposée sur ce mot de passe c'est qu'il doit faire entre 6 et 50 caractères.




`slide-30` 1 mot de passe (incorrect)
--------

 `RPE` rien ne m'empêche non plus de choisir un mot de passe "incorrect"

`FLD` et j'imagine que tu reutilise le meme mot de passe partout ?

`RPE` pas toi ?

`FLD` pas moi ;-) Et j'en décompte 156

`slide-31`  156 mots de passe ?
--------

`FLD` je les génère,  les renouvelle, les chiffres, les stock sur mon disque
et pour ca forcemment j'ai un outil


`slide-32` 1 chien ?
------

`RPE` t'as 156 mot de passe, mais a quoi bon ? je connais le nom de ton chien

`note` on respire, on laisse les gens rigoler

`FLD` et celui de Paris Hilton ?

`FLD`

Paris s'est fait hacke sous compte  chez T-Mobile qui pour protéger le mot de passe de ses clients

T-Mobile n'avait pas choisie une question bien originale...

Mais est-il si facile de trouver des questions dont les réponses ne soit déjà partagés sur le web à travers reseaux sociaux, blogs, tabloids, et journaux

`RPE` en meme temps qui voudrait vraiment partager un vrai secret avec son operateur telephonique ?

`slide-33` des Secrets ? (tweets)
------

`FLD` qui voudrait partager ses secrets avec avec facebook, snapchat, meetic, tinder, gleeden ?

`RPE` Mais qui ne partage quelques secrets avec son banquier ?

`FLD` Et qui n'utilise pas de carte à puces, des cartes SIM ?

`RPE` Dans la vraie vie, un secret c'est quelque chose que vous ne partagez qu'avec une seule personne à la fois.

`FLD` et dans le vraie vie comme sur le web tout des oreilles trainent

`RPE` Partout

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

`RPE` : Adobe, comme nous Red Hat, vous avez forcemment fait un choix, vous avez une solution de gestion d'identité ?

Si vous n'avez pas, je crois qu'on en vends 4 différents au dernier compte ! (Si vous prenez une paire de QUeue JMS, en plus, on fait un prix ;) ).



`slide-35` 1 IDP ?
-------



`FLD`  Oui bien sûr, j'ai donc modifié mon appli généré,


`RPE` ok donc tu présentes donc cette page a mister anonymous, et tu lui propose un lien vers une resource protégé par ton fournisseur d'idendité

`FLD` Oui mon IDP comme la plupart des solutions supporte le standard SAML


`slide-36` SAML ?
-------

c'est un standard qui permet de faire du SSO sur le browser.
si vous voulez débutez et tester votre solution, jetez un coup d'oeil à www.ssocircle.com

`slide-38` SAML Sequence Diagram
-------

`RPE` Alors Saml ? comment ça marche ?

`FLD` Le plus compliqué finalement, c'est la config.

* il faut recuperer le meta données de l'idp et fournir a ton moteur client saml
elle contienne un certificat et des url à associer à la redirection en vue d'un login ou tout au moins d'une verification  d'identité

`RPE`
* et toi tu fournis à l'idp, quelques metadonnées comme
  *  certificats et url associer à la redirection en vue d'un login et logout.

`FLD` exactement, regardons le flow

 tu ceux acceder a ma une resource protégé
mon fournisseur de service dit

* "Not authorized", je te connais pas, je te donne pas le service, je te donne pas la resource,
* va prouver ton identité au pres du fournisseur d'identité,
* il reviendra vers moi,
* si son retour est valide, je te donnerai accès à ma resource
* tout du moins si les infos d'idendité extraite dans l'enveloppe saml me permette de te donner le role necessaire pour etre autorise à acceder a ce service ou cette resource.



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





`slide-39` login link
-------

`RPE` alors voyons je click!


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

 `FLD` c'est vrai que l'equilibre entre expereience tuisateur. confort et securite n'est  pas evident a trouver.


`slide-43` wired
----

`FLD`

tu connaissez le chien de  Paris Hilton ?
mais tu connaissez ce gars ?

`RPE`
pas avant que tu m'en parles, mais pares avoir lu cet article
je comprends que tu veuilles passer en 2 FA

`FLD`
Oui je l'ai active sur mon compte twitter, facebook, google, yahoo , github, paypal,



`RPE` en tant que developpeurs il est de votre responsabilité de protéger vos secrets, vous êtes la cible des hackers

`FLD` vous avez votre profil sur linked-in, et vous êtes devops ou security specialist chez BNP ou 1 ms valent 100 millions d'euros ?



`slide-34` 2FA
----


`FLD` allez faire un tour sur twofactors.org, voyez ou vous pouvez activer le 2FA, et faites vos choix en fonction

`RPE` laissez tomber docker

`FLD` preferez github a bitbucket

`RPE` si vous navez peur de rien, utiliser ces services de finance en ligne

`FLD` que l'internet of things et les applis santé font globalement fi de la securité,  pareil pour la plupart des micro paiement,


`RPE`en fait le plus secure, etonnamment les reseaux sociaux...

`FLD` et le sreseaux sociaux en UX il sy'connaissent, ils ont trouver un equilibre interesant mais en mettant en place le 2FA
mais en vous permettant egalement de definir vos telephone et vos  navigateurs de confiances sur lesquels votre session sera maintenue.


`RPE` et j'imagine que tu le fais ? ?




slide saml + oauth
-----

`FLD`
rappelle moi romain on a saml
une fois authentifié je vais
* provisionner un client oauth rien que pour toi (avec ton client idet secret )
* et t'inviter a faire a la dance oauth

`RPE` ok donc une fois logué, et apres quelques redirect je receiupre un token...
mais bon il perime le token non ?

`FLD` oui mais refresh tokem

`RPE` ah mais ca pue

`FLD` oui mais c'est revocable

slide revoke
------

`RPE` tu peux aller plus loin

`FLD` oui email...

slide option
----

`FLD`
et sinon on avait d'autre option

`RPE`
oui parce que oauth2 ,  No standard (yet) for request signing

`FLD` en fait avec le JWT token et spring security tu peux le faire...

`RPE` mais oui mais pourquoi pas oauth1 ?

oauth1 ping pong



`Talket 6` Extension du périmètre de la lutte - CI & Cloud
=========

`RPE` Jusqu'à maintenant, quand on pense sécurité des applicatis, on a naturellement tendance à penser au plateforme de production. Et donc, de délaisser, voir d'être laxasiste avec les environements de dev et les plateforme d'intégration continue. Je ne vais pas vous surprendre en disant que c'est certainement une très mauvaise idée. Surtout qu'avec l'arrivée du Cloud, dont la flexibilité repose massivement sur une chaine de déploiement continue irréprochable, tout un univers de faille et d'exploit nouveau s'ouvre aux attaquants, dans un domaine, où les experts de la sécurité sont très loin d'avoir évangélisé et diffusé les bonnes pratiques associées.


slide github secret
--------

`FLD` Commencons par regarder notre code, contient-il des secrets ?

slide rail tweet
-----

`RPE`

slide secret management is not easy
----

`FLD`

slide chef-vault intro
----
`FLD`


`RPE` mais bon faut securiser les servers

slide chef vault problem
---

`FLD`

`RPE` white list ? scale up ?

`FLD` chef server à securiser mais c'est pas le seul dans notre usine logicielle et note build pipeline


slide jenkins
---

`RPE` Ah oui à fond, surtout que je connais beaucoup de gens qui non seulement n'impose pas d'authentification sur Jenkins - donc n'importe qui peut créer des jobs, mais le bouzin étant assez extensible, on peut même lui injecte des extensions via la "script console". Mais en fait, même si tu fermes ça, n'importe qui, qui peut crée un job, peut faire exécuter du code au serveur, donc...

`FLD` ... donc il est crucial de bien pouvoir tracer qui, depuis où, à créer ou lancer un job.

`RPE` Exactement.

slide nexus
----

`FLD` presentation des trucs qu'on chope

`RPE` faut faire un proxy et faire des checksums
satelite

`FLD` nexus aussi

cloud
----
`RPE` Bon j'imagine que apres tu va mettre ton app sur le cloud ?

`FLD`: Ah non g peur la

`RPE`: Non, au contraire ! Le cloud te force à faire plus gaffe à ta sécurité, pour toutes les raisons qu'on vient d'évoquer, mais t'apportes bcp en termes de sécurité.

Y'a qu'on bien de système non maintenu, qui tourne depuis 10 ans, sans le moindre de security patch appliqué dans ton infra ? Voir sans admin !

`FLD`: (gros sourire) ben aucun bien sûr ;) !

`FLD` Cattle vs Pet,

`RPE`: Exactement ;) - dans le cloud tes machines sont constament reconstruit "fraîche" et patché. Un super exemple est Neflix.

Ils sont très connu par avoir une service irréprochable qui repose sur la solution de Cloud d'Amazon.

Si vous avez bossé sur Amazon, vous savez que bien d'excellente qualité, le service n'est pas à 100% fiable.

Une VM peut subitement "disparaitre", le réseau peut devenir temporairement inaccessible, et leur SLA prévoit même qu'une zone entière (par exemple l'Irlande) peut tomber pendant plusieurs minutes !

Bref, dans ces conditions, pour fournir un super service comme Netflix, il faut que les applications soient très robuste !

Et là, Netflix a été génial, ils ont forcé leur developeur à se préparer aux pannes et mettant en place un programme simulant ces pannes - le fameux Chaos Monkey.

Et le plus incroyable, c'est qu'ils sont tellement sûr de la résilience de leur applications qu'ils laissent Choas Monkey s'exécuter sur leur plateforme de production !!!

http://techblog.netflix.com/2012/07/chaos-monkey-released-into-wild.html

de choas monkey a hacky monckey


`Talklet 7` Firemen
===========

slide devops -> devsec
----

FLD en fait fo etre pret a etre hacke

RPE exactement ! Regarde github

FLD tell the story

RPE => pret a endurer une attaque

FLD pompier metaphore

combattre le feu
----

`RPE` le but - fighting chance, du coup detecteur de fume et porte feu

`FLD` ccm

`RPE` IDS pour reperer des intrusions

`FLD` HSM ben d'attaque offline

`RPE` Ben sinon, si un mec à trouver un exploit sur ton app, il peut accéder à ses données, mais aussi éventuellement, modifier son comportement.

meca qui bloque

co un RP !



slide devsec devops
----

`FLD`: Ouais, mais dis moi, avec ça en place, ça évite que ton application crée des fichiers, ou exécute des programmes, mais si l'exploit se base sur une "activité" normale. Par exemple modifie le contenu d'un fichier de données légitime de l'application - tu peux gérer ça avec ton SM ou SE Linux ?

`RPE`: Non, j'en doute, et de toute manière, ça ne serait pas vraiment une bonne pratique, de mettre ce genre de contrôle en place là dedans.

`FLD`: Ben moi, j'ai une bonne technique pour ça, super simple pas comme  "ta super science".

TODO: simple checksum on sensitive directory only

`RPE`: Ah ouais, c'est pas mal en effet !  DevSec

CCL
----

`FLD` En conclusion en fait, ce qu'il faut retenir, c'est que:
* firemen train for fire
* fireman is not afraid of fire

https://www.techn0polis.net/wp-content/uploads/2015/01/security.png

`Talklet 8` Conclusion
==========



`RPE` bon que ce qu'il fallair retenir ?

`FLD` la securité c'est toi

`RPE` c'est vous, pensez-y

`FLD` prenez un peu de hauteur, analyser les risques, lancez vous dans un thread

`RPE` n'imaginez jamais etre a l'abri

`FLD` meme pas dans mon VLAN cloisonné, la bas au fond de mon intranet, loin de la dmz ?

`RPE` non t'es pas a l'abri et tes données non plus

`FLD` dun coup je chiffre

`RPE` qui dit chiffrement dit gestion des secrets

`FLD` même de la sphère privé

`RPE` passe au 2FA et tue le chien

`RPE` pan medor

`FLD` l'experience utilisateur n'est pas un pretexte pour une mauvaise securité

`RPE` et vice versa ! N'oublie l'extension du domain de la lutte jusqu'au CI

`FLD` et au cloud

 traite tes serveurs comme du betail, et non pas comme un animal domestique

 `RPE` tout de façon medor est mort

`FLD` 1.2

`en coeur`  soyez prêt à combattre le feu






`
