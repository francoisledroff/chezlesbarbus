`Talklet 2` Intranet, FW & RP
====


`slide-16` Intranet
----

`FLD`  De toute facon mon serveur d'app sera bien planqué au fond, loin de la dmz, tranquille en intranet, derrière une ribambelle de Firewall, dans un VLAN cloisonné.

`RPE` oauis, dis moi, à l'époque, t'étais du genre à croire que les nuages radioactif de Tchernobyl allaient s'arrêter magiquement à la frontière, non ? 

`FLD` c'est pas le cas ? c'est que j'ai lu dans la presse ?

`RPE` Ok, passons. 

Laisse moi te poser une question, tes utilisateurs se connectent depuis une variéte de laptop et desktop ?

`FLD` oui, depuis leurs téléphones mobiles et leurs tablettes aussi.

`RPE` Ben bien sur... et a partir de ces dernier,j'imagine, ils se connectent aussi à internet ?

`FLD` oui je vois ou tu veux en venir, 

sachent que certains sont même "root" et que tous n'ont pas des postes "managés" ?


`RPE`, donc  malgré les mises à jours régulières des postes "managés", d'avoir des systèmes compromis. 

{Enfin, assumant que les postes "managés" soient toujours plus "sécurisé" que les postes externes, ce qui peut se discuter (spécialement entre un Windows gangrené de Security Pack, face à une laptop sous une distro linux à jour).}

### `slide-17` computer locked in a room

`FLD` Au final, ce que tu me dis, des que c'est en reseau, c'est foutu

mais je suis sauvé j'ai des FW


`slide-18` Firewall
---------


`RPE`: Et alors ? Quel rapport ? Les FW ça ne sert pas à sécuriser des applis...

`FLD`: (expression de surprise)

`RPE`: Non, sérieusement, le truc du FW, c'est juste de faire de la qualité réseau et d'épargner, le CPU. En gros, si un système reçoit un paquet pour un port "non utilisé", il le "drop" en kernal space, plutôt que de le faire remonter pour rien jusqu'au couche applicative. 

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

`FLD` je peux pas relever mes mails en POP, 

`RPE` c'est naze

`FLD` mon accès VPN est bloqué, 

`RPE` encore plus naze

`FLD` SSH sortant est bloqué

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

`slide-18` Reverse Proxy
---------

`RPE` Mais, de nos jours, avec l'approche DevOps et des outils comme Puppet...

`FLD` ou Chef ! (gros sourire)

`RPE`  Bref, avec cette approche et ces outils, les équipes projets ont de plus en plus la main des composants d'infrastructure.

 par exemple, un serveur web en frontal. Genre, un nginx ou un apache qu'on place devant leur serveur d'app.

`FLD` Ben justement, sur ma petite appli intranet, puisqu'on était en mode POC, on a pas eu le temps..

`RPE` C'est con ça,  Car en fait, quand tu un serveur web en frontal, tu peux t'en servir comme un reverse-proxy (RP). 

pour faire simple, que, avant de retourner une requête vers ton serveur d'app, le RP va analyser son contenu

`FLD` et alors ?

`RPE`  si elle n'est pas conforme aux attentes de l'application il la dropped 

comme par exemple l'ajout paramètres ou un contenu incohérent 
(exemple date sur 200 carateres)

`FLD` ou encore de la validation de header http, l'ajout de token csrf, du throttling ou du rate limiting

`RPE` Tes aimes bien les mots anglais non ? 

En plus, généralement ton serveur web en frontal, il est, soyons honnête, payé à rien foutre. 



`FLD` mais on peux pas me le hacker aussi vite et bien le RP ?

`RPE` Plus difficilement, parce que la plupart des hacks se basent sur le fait de manipuler la réaction du serveur distant en abusant des requêtes qu'il accepte. Or le RP ne repond pas a ses reaquetes

`FLD` oui il se contente de les analyser et nettoyer.

`RPE` ce qui laisse donc très, très peu de marge à un attaquant pour le contourner.

`FLD` Pour résumer Romain, on peut dire que des firewalls sans filtrage applicatif, c'est comme une frontière sans douanier.

`RPE` Ou plutôt avec des douaniers qui arrêtent que les "honnêtes citoyen", sans jamais voir que les criminels passe à 20m de leur point de contrôle...

`FLD` ok donc on filtre, on nettoie mais on veut aussi recevoir et envoyer des données sur ce fameux reseau non ?

