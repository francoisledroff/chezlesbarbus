`Talklet 2` Intranet, FW & RP
====

to check: http://www.arnoldit.com/articles/10intranetSecAug2002.htm

Intranet
----

`FLD` ...Mais, bon, je ne suis pas trop inquiet, car en fait, en interne, on a plein de FW, et de tout manière, on va déployer l'application que sur l'Intranet.

`RPE` oauis, t'étais du genre à croire que les nuages radioactif de Tchernobyl allaient s'arrêter magiquement à la frontière, non ? laisse moi d'abord te poser une question, tes ulisateurs se connectent depuis une variéte de laptop et desktop et se connectent depuis leur machine également sur internet ?

`FLD` oui

`RPE` donc déjà en naviguant sur un site malicieux, on peut lancer des attaques vers les applications internes. Et parmi ces utilisatuers, je suppose que certains sont même "root" et que tous n'ont pas des postes "managés" ?

`FLD` oui

`RPE`, donc il est aussi possible, malgré les mises à jours régulières des postes "managés", d'avoir des systèmes sur le réseau, compromis. Enfin, assumant que les postes "managés" soient toujours plus "sécurisé" que les postes externe, ce qui peut se discuter (spécialement entre un Windows gangrené de Security Pack, face à une laptop sous une distro linux à jour).

`FLD` Ok, et du coup, et tu vas me demander si mes utilisateurs sont usr linux  RHEL

`RPE` What else ? ;) Plus sérieusement, on ne fait pas de laptop en parti pour ce genre de problématique. C'est très dur à sécuriser. Mais imagines  bien que dans le "set up" que tu décris, un développeur ayant accès à l'application peut la compromettre facilement en naviguant sur un site infecté - avec peu de chance que le système d'exploitation puisse y faire quelque chose. Bref, tu l'as compris, intranet ou internet, aujourd'hui c'est le même combat.

`FLD` Au final, ce que tu me dis c'est que: "The only secure computer is one with no power, locked in a room, with no user. Any other system can be compromised."

`RPE` Ouais. Et encore, uniquement si tu as déconnecté le disque dur de la carte mère. Le reste c'est de la paté pour Prism ;)

Firewall
---------

`FLD`: mais attends quand meme t'exagères, on peut pas sauter de machine à machine comme ça, on a des firewalls en place !

`RPE`: Et alors ? Quel rapport ? Les FW ça ne sert pas à sécuriser des applis... Non, sérieusement, le truc du FW, c'est juste de faire de la qualité réseau et d'épargner, le CPU. En gros, si un système reçoit un paquet pour un port "non utilisé", il le "drop" en kernal space, plutôt que de le faire remonter pour rien jusqu'au couche applicative. Le paquet est "oublié" à vitesse grand V, et le système se concentre sur autre chose. Bref, ça fait de la qualité réseau, ça réduit le traffique "inutile"

`FLD`: Mais attends ça bloque des ports, donc ça empêche des attaques, non ?

`RPE`: Ouais, sauf que généralement quand tu as truc qui tourne sur un port, c'est que tu en as besoin, donc du coup, le port est ouvert. Si tu es assez con pour laisser tourner un service dont tu as pas besoin, effectivement, ton FW te "sécuriser", mais à mon avis tu auras d'autres problèmes de sécurité. En gros, un FW c'est comme la ligne Maginot, qui, contrairement à ce qu'on pense, a super bien fonctionner - la preuve, Hitler en avait tellement peur, qu'il a décidé de passer à coté. Mais du coup, toute l'inrastructure de combat qu'elle contenait, a servi à rien. Un FW c'est à peu prêt aussi inutile.

En fait, le vrai truc utile avec les FW, c'est le filtrage applicatif, c'est à dire, non pas bloqué un protocole ou service, mais vérifier que celui-ci a un usage valide. Fais tu STMP si tu veux, mais sur ce port, je veux que du STMP, pas autre chose. Fais du SSH autant que tu veux, mais sur le port 22 et pas à travers HTTPS, et au passage, si tu fais tu ssh, je te loggue (etc...) - c'est d'ailleurs 1000 fois plus malin de faire de l'auditer et de la supervision proactive sur les flux SSHs (pour justement détecté un usage illicite) que tout bloqué et rendre infernal la vie de tout le monde dans l'entreprise.

C'est pour ça, j'ai l'habitude de dire qu'on estimer la nullité crasse d'une sécurité par le nombre de port bloqué:
- je peux pas relever mes mails en POP, c'est bien naze
- mon accès VPN est bloqué, encore plus naze
- SSH sortant est bloqué, stupide, un coup de tunnel SSH over HTTPS - avec un peu de "forage" de proxy si besoin est, et je sors de toute manière.

Avec tous ça, on n'a certainement pas arrêté les hackers qui sont tout autant libre de faire cross-scripting et d'autres hack à base de pur HTTP, mais on a bien emmerder le reste de la boite.

Reverse Proxy
---

`FLD` Ouais, ok, donc le truc c'est le filtrage applicatif, mais tout le firewall ne peuvent le faire, et puis au final, ça ne te garantit que l'usage du "bon protocole". Si notre appli se prend des requêtes mal intentionné, ça va ne va rien changer.

`RPE` Ben si justement, car tu peux aller loin en filtrage applicatif. Moi, personnellement, je ne préfère pas le faire au niveau du FW cependant, car la plupart du temps, ces derniers dépendent des équipes d'infrastructure qui n'ont généralement pas vraiment une assez bonne compréhension de l'application pour faire ça bien. Mais, de nos jours, avec l'approche DevOps et des outils comme Puppet...

`FLD` ou Chef ! (gros sourire)

`RPE` (regard grumpy) oui, ou chef (@assistance: "pour ceux qui étaient pas là l'année dernière"). Bref, avec cette approche et ces outils, les équipes projets ont de plus en plus la main des composants d'infrastructure comme, par exemple, un serveur web en frontal. Genre, un nginx ou un apache qu'on place devant leur serveur d'app.

`FLD` Ben justement, j'en voyais pas l'intérêt, et ça me demande de la conf en plus, donc j'en ai pas mis.

`RPE` C'est con ça, car tu vas voir que ça sert justement ! Car en fait, quand tu un serveur web en frontal, tu peux t'en servir comme un reverse-proxy (RP). C'est à dire, en terme simple, que, avant de retourner une requête vers ton serveur d'app, tu peux, à l'aide par exemple de regex, filtrer cette dernière pour t'assurer que, par exemple :
* elle est conforme aux attentes de l'application (ex: et hop, on drop les paramètres ajoutés au formulaire histoire de polluer ou même corrompre la données
* dropper aussi les paramètres contenant des morceaux de requêtes SQL ou simplement une taile ou contenu non conforme aux attentes.
* etc...

`FLD` TODO peut être un petit commentaire ou une "blague" ici

`RPE` Y'a plein de trucs que je trouve super avec les RPs. En premier lieux, ça décharge l'application d'un lourd travail de nettoyage / protection qui consomme du CPU "applicatif", alors que généralement ton serveur web en frontal, il est, soyons honnête, payé à rien foutre. Si vous me croyez pas, faites un top sur un serveur dédié à de telles instances, vous verrez vite de quoi je parle.

`RPE` Le second truc que je trouve vraiment rassurant c'est aussi ce que j'appelle l'effet "douanier incorruptible". En effet, la plupart des hacks se basent sur le fait de manipuler la réaction du serveur distant en abusant des requêtes qu'il accepte. La bonne nouvelle avec le RP, c'est qu'il n'exécute pas d'action par rapport aux requêtes, il se contente de les analyser et nettoyer, et laisse donc très, très peu de marge à un attaquant pour le contourner. En outre, si on fait bien les choses, il est dans les faits extremement difficile pour ce dernier de même réaliser qu'un RP est en place !

@FLD, pour respecter l'esprit "Talklet", il faudra faire une sorte de conclusion, mais aussi injecter un "brainbreak" juste après. Note que ta première réplique, je trouve, est une parfait introduction.

`FLD` Bon, en gros, pour résumer tout ce qu'on vient dire, l'intranet, en terme de sécurité, c'est le nouveau internet, et les firewalls, sans filtrage applicatifs, c'est aussi inutile qu'un marteau sans clou (TODO: trouver une meilleur comparaison).

idée de brain break, tu conclus :

`FLD` "c'est aussi efficace que demain des conseils à Romain en veille technologique..."

`RPE` Sachant que j'ai choisie Google Buzz à la place de Twitter, Mercurial à la place de Git, et que j'ai jamais utilisé Google Wave mais toujours pensé que ça erait un carton.
