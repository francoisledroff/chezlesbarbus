`Talklet 7` Firemen 
===========

`RPE` (En effet) Quand on parle de sécurité, la peur domine, et on met souvent en place des politiques ou des stratégies de sécurité, très (et souvent) trop restrictives, pour éviter tout risque. Et le problème de ça, c'est que à force de tout faire pour ne pas être compromis, et bien, on sait rarement quoi faire quand ça arrive. Au final, les attaques (comme le montre la petit démo du début) arrivent tout le temps, et espèrer ne pas être attaqué, ou même compromis, revient à ne pas acheter de pare pluie, et espérant ne jamais être dehors au mauvais moment. Aussi bon, ou foireux que soit votre météo app sur votre téléphone, un jour ou l'autre, il va vous pleuvoir dessus, et vous aurez besoin d'avoir un paraplui mais aussi de savoir vous en servir !

tu m'as hacké et alors ?
---

`FLD`: Oui, mais attends, mon appli est super sécurisé (maintenant).

`RPE` Oui, mais il reste toujours des failles, soient des problèmes pas identifié dans votre code, soit des failles dans la JVM - et Dieu sait que cette dernière avait les "news" ces dernières années à ce sujet, ou même, encore plus simplement, il reste toujours l'exploitation de la faille "humaine". La meilleur source d'information de l'Allemagne de l'Est était les secrétaires des puissants de l'Ouest retourné par des "Roméo", des espèces de Donjuans de l'Est auquel, visiblement, bien des demoiselles avaient du mal à résister. Alors imagine ce qu'une jolie fille d'aujourd'hui peut extirper comme information à n'importe lequel de tes développeurs.

`FLD` Alors, pas besoin d'aller voir mes développeurs, moi je veux bien déjà tout dire :)

`RPE` (ponders) Oui, moi aussi... :) 

`RPE` Bref,  ben c'est dur à dire, on peut jamais être sûr, mais disons que maintenant, ce qui serait sympa, c'est non plus d'éviter le pire, mais de penser à gérer le pire. En fait, l'idée c'est de protéger les copains de nos conneries. Si tu as laissé un trou dans ton appli, que au moins, que elle seule soit compromise.

`FLD` Comment ça ?

`RPE` Ben si un mec à trouver un exploit sur ton app, il peut accéder à ses données, mais aussi éventuellement, modifier son comportement. Par exemple, lui faire envoyer des mails ("Merci à l'infrastructure Adobe d'avoir participé "pro bono" à la diffusion de mes spams !), effacer des fichiers ou récupérer des données d'une autre app colocalisé avec l'appli.

`FLD`: Et tu peux faire qqlchose contre ça ?

`RPE`: Ouais, bien sûr, c'est un peu la même logique qu'avec un RP, ou que combattre les pourriels. En gros, tu défini le comportement "normal" de ton appli et tu banni tout le reste. Dans une infrastructure "classique" (pour nous, Javateux) Tu peux le même faire à deux niveaux. D'abord, sur le JVM avec le Security Manager, que tout le monde connait ici (regard à l'assistance). Acun expert ou dev Java tourne d'applicatif sans, hein ? ;)

`FLD`: Oh là, comment ça marche ce truc déjà ? C'est pas à l'enfer à gérer ? 

`RPE`: Non, pas tant que ça.... TODO

`RPE`: Sinon, si tu es comme moi "linux friendly", tu peux aussi le faire au niveau système avec SE LInux. En gros, les deux technos ont la même fonctionnalité - elle bloque les comportements dit "anormaux" des applications. L'avantage de le faire au niveau SE Linux, c'est que tu peux le faire pour tout le système, et non seulement au niveau de la JVM. Pour des développeurs Java, par contre, c'est souvent plus simple d'opérer sur la JVM, car ils n'ont pas forcément toutes les autorisations ou privilèges nécessaires pour mettre ça en place. 

SELinux & SM
----

`FLD`: Ah ouais, mais du coup, pourquoi pas mettre les deux en places ? 

`RPE`: Théoriquement tu peux, mais c'est déjà beaucoup de boulot, et chaque couche augmente les chances de se tirer dans le pied. Imagines le scénario, tu déploies l'appli en pre prod, et une nouvelle fonctionnalité marche pas comme prévu. En gros, le SM ne laisse pas l'appli ouvrir un fichier dans le répertoire tmp. Tu corriges, tu redéplois, et là ça merde pour la même raison, mais ce coup ci, c'est SE Linux qui dit ton app Java d'aller se faire voir. Sans compter, que chacun techno a la même fonctionnalité, même pas du tout la même syntaxe ou prérequis, donc, rien qu'en coût de formation, ça semble pertinent.

`FLD`: Ouais, en fait, il vaut mieux le faire une fois bien, plutôt que deux fois mal. Et au final, le choix entre SE Linux et SM, se fait plutôt sur les compétences en interne et les besoins - y'en a pas une meilleur que l'autre.

`RPE`: Non, en effet. C'est pas comme Windows versus RHEL - là on sait clairement qui est le meilleur :) 

`FLD`: Ouais, mais dis moi, avec ça en place, ça évite que ton application crée des fichiers, ou exécute des programmes, mais si l'exploit se base sur une "activité" normal. Par exemple modifie le contenu d'un fichier de données légitime de l'application - tu peux gérer ça avec ton SM ou SE Linux ?

`RPE`: Non, j'en doute, et de toute manière, ça ne serait pas vraiment une bonne pratique, de mettre ce genre de contrôle en place là dedans.

`FLD`: Ben moi, j'ai une bonne technique pour ça, super simple pas comme  "ta super science". TODO: simple checksum on sensitive directory only

`RPE`: Ah ouais, c'est pas mal en effet !

`FLD`: Tu as vu, je suis pas si nul que ça, hein ;) 

`RPE`: Ouais, j'irais pas jusque là quand même :) 

It will fail
----

`RPE`: Bon, en tout cas, comme on a dit, le problème de fond c'est que les attaques auront lieu, et certaines réussiront. On ne pourra pas toujours patché les systèmes à temps, et si la faille utilisée par le hacker n'est pas encore identifié, on n'a aucune défense. Bref, il faut être prêt.

`FLD` Oui, j'aime bien ces mots clés pour définir un peu ce que l'ops doit être:

* consentement
* safety
* knowledge
* freedom

`RPE` "consent, safety, freedom," ça ressemble plus à un trailer pour "50 Shades of Grey", non ? 

`FLD` Ben ouais, justement, il faut savoir rester prudent tout en prenant des risques non ? :)

`RPE` Ok, c'est un joli "mantra", mais concrètrement, où ça veut en venir ?

`FLD` Ben en fait, l'idée c'est de considérer une attaque, comme un incendie. La question n'est pas rendre ton immeuble in-inflammable, c'est pas possible, mais t'assurer que si il prends feux, il est une "fighting chance".

`RPE` Oauis, par exemple avoir des portes coupe-feux (comme SELinux) et des détecteurs de fumée (en ayant par exemple, mise en place un "audit trail").

`FLD` Et, à ce sujet, y'a une super page d'audit jhipster.
(nous en plus, on a prévu le coup si un des nos utilisateurs perd son laptop, on reset son token)

CCL
----

`FLD` En conclusion en fait, ce qu'il faut retenir, c'est que:
* firemen train for fire
* fireman is not afraid of fire

https://www.techn0polis.net/wp-content/uploads/2015/01/security.png
