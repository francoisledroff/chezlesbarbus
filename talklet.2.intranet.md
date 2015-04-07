`Talklet 2` Intranet, FW & RP
====


`slide-15` Intranet
----

`FLD`  mon serveur d'app sera bien planqué au fond, loin de la dmz, tranquille en intranet, derrière une ribambelle de Firewall, dans un VLAN cloisonné.

`RPE` oauis, dis moi, à l'époque, t'étais du genre à croire que les nuages radioactif de Tchernobyl allaient s'arrêter magiquement à la frontière, non ? laisse moi te poser une question, tes utilisateurs se connectent depuis une variéte de laptop et desktop, à partir desquels,j'imagine, ils se connectent aussi à internet ?

`FLD` oui, depuis leurs téléphones mobiles et leurs tablettes aussi.

`RPE` OK, donc déjà en naviguant sur un site malicieux, on peut lancer des attaques vers les applications internes. Et parmi ces utilisateurs, je suppose que certains sont même "root" et que tous n'ont pas des postes "managés" ?

`FLD` oui

`RPE`, donc il est aussi possible, malgré les mises à jours régulières des postes "managés", d'avoir des systèmes sur le réseau, compromis. Enfin, assumant que les postes "managés" soient toujours plus "sécurisé" que les postes externes, ce qui peut se discuter (spécialement entre un Windows gangrené de Security Pack, face à une laptop sous une distro linux à jour).

`FLD` Ok, et du coup, et tu vas me demander si mes utilisateurs sont user linux sur RHEL

`RPE` What else ? ;) Plus sérieusement, on ne fait pas de laptop en parti pour ce genre de problématique. C'est très dur à sécuriser. Mais imagines bien que dans le "set up" que tu décris, un développeur ayant accès à l'application peut la compromettre facilement en naviguant sur un site infecté - avec peu de chance que le système d'exploitation puisse y faire quelque chose. Bref, tu l'as compris, intranet ou internet, aujourd'hui c'est le même combat.

### `slide-16` computer locked in a room

`FLD` Au final, ce que tu me dis c'est que: "The only secure computer is one with no power, locked in a room, with no user. Any other system can be compromised."

`RPE` Ouais. Et encore, uniquement si tu as déconnecté le disque dur de la carte mère. Le reste c'est de la paté pour Prism et les autres programmes de la NSA ;)
 - au fait, si vous avez des amis aux USA, rappelez leur que leur congrès doit revalider le Patriot Act en Juillet. Peut être le bon moment pour appeler leur députés...

`slide-17` Firewall
---------

`FLD`: Bon, attends quand meme t'exagères, pas pour le Patriot Act, mais le reste. On peut pas sauter de machine à machine comme ça, on a des firewalls en place, nous !

`RPE`: Et alors ? Quel rapport ? Les FW ça ne sert pas à sécuriser des applis...

`FLD`: (expression de surprise)

`RPE`: Non, sérieusement, le truc du FW, c'est juste de faire de la qualité réseau et d'épargner, le CPU. En gros, si un système reçoit un paquet pour un port "non utilisé", il le "drop" en kernal space, plutôt que de le faire remonter pour rien jusqu'au couche applicative. Le paquet est "oublié" à vitesse grand V, et le système se concentre sur autre chose. Ca permet aussi de limiter ainsi les attaques de types "déni de service". Bref, ça fait de la qualité réseau en réduissant le traffique "inutile"...

`FLD`: Mais attends ça bloque des ports, donc ça empêche des attaques, non ?

`RPE`: Ouais, sauf que généralement quand tu as truc qui tourne sur un port, c'est que tu en as besoin, donc du coup, le port est ouvert. Si tu es assez con pour laisser tourner un service dont tu n'as PAS besoin, ben effectivement, ton FW te "sécuriser". Mais à mon avis tu auras d'autres problèmes de sécurité dans ta boite.

`RPE`: Bref, en gros, un FW c'est comme la ligne Maginot, qui, contrairement à ce qu'on pense, a super bien fonctionné - la preuve, l'armée d'Hitler l'a soigneuseument contournée.

`FLD`: Et voilà 10 minutes et on a déjà atteint le point de Godwin.

`FLD` Ce que tu veux nous dire Romain c'est que le FW tout comme la ligne Maginot, ne peut être ta seule infrastructure de défense. Sinon elle ne sert à rien. Et ce FW sera d'autant plus inutile si il est utilisé comme tu le disais et comme c'est le cas souvent juste pour fermner des ports.

`RPE`: Exactement le vrai truc utile avec les FW, c'est le filtrage applicatif, c'est à dire, non pas bloquer un protocole ou service, mais vérifier que celui-ci a un usage valide. Fais tu STMP si tu veux, mais sur ce port, je veux que du STMP, pas autre chose. Fais du SSH autant que tu veux, mais sur le port 22 et pas à travers HTTPS, et au passage, si tu fais tu ssh, j'enregistre ton activité, et je fais un "audit trail". - c'est d'ailleurs 1000 fois plus malin de faire de l'audit et de la supervision proactive sur les flux SSHs (pour justement détecté un usage illicite) que tout bloquer et juste rendre infernal la vie de tout le monde dans l'entreprise.

`RPE`: C'est pour ça, j'ai l'habitude de dire qu'on estimer la nullité crasse d'une sécurité par le nombre de port bloqué:
- je peux pas relever mes mails en POP, c'est naze
- mon accès VPN est bloqué, encore plus naze
- SSH sortant est bloqué, stupide, un coup de tunnel SSH over HTTPS - avec un peu de "forage" de proxy si besoin est, et je sors de toute manière.
- encore un ou deux ports "bloqué" et génèralement je recommande aux clients de virer leur RSSI.

Mais, le pire, c'est avec tout ça, on n'a pas quand même pas résolu les attaques de types cross-scripting évoqué plus haut. Même avec un FW en béton, qui filtre le flux HTTP, il est encore possible de déployer un JS malicieux sur un navigateur s'exécutant dans l'intranet ! Par contre, si on a bloqué plein de ports, on est sûr d'avoir donné une illusion de sécurité et cassé les pieds à tout le monde dans la société...

`FLD` Ouais, ok, donc le truc c'est le filtrage applicatif, mais dis ? Les FW savent le faire ça? ça ne te garantit que l'usage du "bon protocole". Si notre appli se prend des requêtes mal intentionné, ça va ne va rien changer.

`RPE` Ben si justement, car tu peux aller loin en filtrage applicatif. Moi, personnellement, je ne préfère pas le faire au niveau du FW cependant, car la plupart du temps, ces derniers dépendent des équipes d'infrastructure qui n'ont généralement pas vraiment une assez bonne compréhension de l'application pour faire ça bien.

`slide-18` Reverse Proxy
---------


`RPE` Mais, de nos jours, avec l'approche DevOps et des outils comme Puppet...

`FLD` ou Chef ! (gros sourire)

`RPE` (regard grumpy) oui, ou chef (@assistance: "enfin, pour ceux qui étaient pas là l'année dernière"). Bref, avec cette approche et ces outils, les équipes projets ont de plus en plus la main des composants d'infrastructure comme, par exemple, un serveur web en frontal. Genre, un nginx ou un apache qu'on place devant leur serveur d'app.

`FLD` Ben justement, sur ma petite appli intranet, puisqu'on était en mode POC, on en voyais pas l'intérêt, et que ça nous fesait du boulot en plus, on a pas mis.

`RPE` C'est con ça, car tu vas voir que ça sert justement ! Car en fait, quand tu un serveur web en frontal, tu peux t'en servir comme un reverse-proxy (RP). C'est à dire, en terme simple, que, avant de retourner une requête vers ton serveur d'app, tu peux, à l'aide par exemple de regex, filtrer cette dernière pour t'assurer que, par exemple :
* elle est conforme aux attentes de l'application (ex: et hop, on drop les paramètres ajoutés au formulaire histoire de polluer ou même corrompre la données
* dropper aussi les paramètres contenant des morceaux de requêtes SQL ou simplement une taile ou contenu non conforme aux attentes.

`FLD` je pourrais même y deporter ou dupliquer pas mal du boulot que mon stack aurait à faire. comme la validation de header http, l'ajout de token csrf, de  du throttling ou du rate limiting

`RPE` Exactement. Y'a plein de trucs que je trouve super avec les RPs. En premier lieux, ça décharge l'application d'un lourd travail de nettoyage / protection qui consomme du CPU "applicatif", alors que généralement ton serveur web en frontal, il est, soyons honnête, payé à rien foutre. Si vous me croyez pas, faites un top sur un serveur dédié à de telles instances, vous verrez vite de quoi je parle.

`RPE` Le second truc que je trouve vraiment rassurant c'est aussi ce que j'appelle l'effet "douanier incorruptible". En effet, la plupart des hacks se basent sur le fait de manipuler la réaction du serveur distant en abusant des requêtes qu'il accepte. La bonne nouvelle avec le RP, c'est qu'il n'exécute pas d'action par rapport aux requêtes, il se contente de les analyser et nettoyer, et laisse donc très, très peu de marge à un attaquant pour le contourner. En outre, si on fait bien les choses, il est dans les faits extremement difficile pour ce dernier de même réaliser qu'un RP est en place !

`FLD` Pour résumer Romain, on peut dire que des firewalls sans filtrage applicatif, c'est comme une frontière sans douanier.

`RPE` Ou plutôt avec des douaniers qui arrêtent que les "honnêtes citoyen", sans jamais voir que les criminels passe à 20m de leur point de contrôle...

@FLD: est ce que ce slide avec une phrase est vraiment nécessaire ? Je préfère intégrer cette réflexion, en qql phrase, au début du Talklet d'après.
`slide-19` Les Menaces
---------

`FLD` et j'ai beau être en Intranet, il faut que j'évalue les menaces et les risques


=======
=======

draft and notes


 http://www.arnoldit.com/articles/10intranetSecAug2002.htm
