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

Par exemple, lui faire envoyer des mails ("Merci à l'infrastructure Adobe d'avoir participé "pro bono" à la diffusion de mes spams !), effacer des fichiers ou récupérer des données d'une autre app colocalisé avec l'appli.

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

