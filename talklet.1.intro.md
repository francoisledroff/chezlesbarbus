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

`RPE` Oui, alors "Salut à tous", je m'appelle Romain, je suis développeur Java chez Red Hat - donc dans la branche JBoss. 

Je suis tombé dans le "café Open Source" quand j'étais petit, d'ailleurs, avec François, et depuis cette époque chez Atos, c'est l'Open Source, qu'il s'agisse de Linux ou du monde JEE qui a guidé ma carrière, sans surprise, jusqu'à Red Hat (What else ? ). 

Pendant mes 3 premières années chez Red Hat, j'ai tenu le rôle de consultant, puis d'architecte, et je ne suis passé développeur que depuis peu, donc ne soyez pas surpris si je mentionne des "cas clients" ou des mises en production. Tout ceci étaient mon pain quotidien, il y a encore quelques mois. A toi FLD,

`slide-4` Présentations Francois
------

`FLD` je m'apelle Francois, je suis développeur, chez Adobe IT, je monte des backend en Java, et un peu de front en html javascript et css, et je fais un peu d'ops avec Chef 

et moi avec Puppet !

 ...


Ce ne sera pas un audit
----

#### `slide-5` audit ?


`RPE` on y va Francois ? On leur a vendu un "audit de sécurité" en 45 mn, non, c'est ça ?

#### `slide-6` non pas un audit

`FLD` oui... mais non

`RPE` Ah bon ? Bon, ça tombe bien ça me casse les pieds les audit !

`FLD` ... je me sens pas armé pour un audit de sécurité... On en est encore au stade du POC... mon archi n'est pas sèche et mes dévelopements en sont encore en cours... j'ai pas encore staffé toute l'équipe...  on n'est pas en position de faire un audit.

`RPE` Tu réalises que la différence entre un Poc et une appli en prod, c'est juste que personne n'a encore mis le PoC en prod ? ;) 

Bref, si tu as réellement inquiet pour la sécurité, il vaut mieux commencer dès maintenant, car il n'y aura pas de "miracle" d'ici la production. 

J'ai vu des systèmes avoir comme mot de passe root "password", avec un joli document indiquant, en rouge,  "à changer avant la mise en prod", 

`FLD` et ...  le mot de passe en production trois mois plus tard ?

`RPE` devine


#### `slide-10` Security By Design

`FLD` OK mais voila......  l'architecte s'est marié, a rasé sa barbe, a eu des enfants ... ne code plus la nuit...

`RPE` et tu lui parles encore ?

`FLD` et aucun programmeur de l'équipe n'est un expert en sécurité

`RPE` pas de souci... on va le voir ensemble,  la sécu touche plein de truc, donc on peut pas vraiment avoir un expert ou un spécialiste. 

`FLD` Tu as raison, la sécurité impacte, l'ensemble du projet, nous seuleument les développeurs, les opérations, mais aussi l'intégration continue et l'expérience utilisateurs.


`RPE` Et c'est notre message aujourd'hui

`FLD` ok, par ou on commence ?



