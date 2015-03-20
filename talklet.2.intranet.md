`Talklet 2` Intranet, FW & RP 
====

Intranet
----

`FLD`  ce qui me rassure c'est que je suis en Intranet

`RPE` laisse moi d'abord te poser une question, tes ulisateurs se connectent depuis une variéte de laptop et desktop et se connectent depuis leur machine également sur internet ?

`FLD` oui

`RPE` tes utilisateurs sont-ils root sur leur machine ? tes utilisateurs ont-ils des machine managées ?

`FLD` oui, et tu vas me demander si mes utilisateurs sont usr linux  RHEL

`RPE` tu l'as compris, intranet ou internet, c'est le même combat.

`FLD` "The only secure computer is one with no power, locked in a room, with no user." Any other system can be compromised.

Firewall 
---------

todo

Reverse Proxy
---

todo


`Talklet 2` Draft
===== 

http://www.arnoldit.com/articles/10intranetSecAug2002.htm



### Firewall 
---------

FLD: mais attends quand meme on a des firewalls

RPE: Pourquoi faire ? Les FW ça ne sert pas à sécuriser des applis... Non, sérieusement, le truc du FW, c'est juste de faire de la qualité réseau et d'épargner, le CPU. En gros, si un système reçoit un paquet pour un port "non utilisé", il drop en kernal space, plutôt que de le faire remonter pour rien jusqu'au couche applicative.

FLD: Mais attends ça bloque des ports, donc ça empêche des attaques, non ?

RPE: Ouais, généralement que tu as truc qui tourne sur un port, c'est que tu en as besoin. Si tu es assez con pour laisser tourner un service dont tu as pas besoin, effectivement, ton FW te "sécuriser", mais à mon avis tu auras d'autres problèmes ailleurs. En gros, un FW c'est comme la ligne Maginot, qui, contrairement à ce qu'on pense, à super bien fonctionner - la preuve, Hitler est passé à coté, mais du coup, elle a pas servi à grand chose. Un FW c'est à peu prêt aussi inutile.

Perso, j'ai l'habitude de dire qu'on estimer la nullité crasse d'une sécurité par le nombre de port bloqué:
- je peux pas relever mes mails en POP, naze
- mon accès VPN est bloqué, encore plus naze
- SSH sortant est bloqué, stupide, un coup de tunnel HTTPS et je sors de toute manière.


La vrai sécurité avec les FW, c'est le filtrage applicatif, c'est à dire, non pas bloqué un protocole ou service, mais vérifier que celui-ci a un usage valide. Fais tu STMP si tu veux, mais sur ce port, je veux que du STMP, pas autre chose. Fais du ssh autant que tu veux, mais sur le port 22 et pas à travers HTTPS, et au passage, si tu fais tu ssh, je te loggue (etc...)


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

