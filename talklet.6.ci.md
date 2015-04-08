`Talket 6` Extension du périmètre de la lutte - CI & Cloud
=========

`RPE` Jusqu'à maintenant, quand on pense sécurité des applicatis, on a naturellement tendance à penser au plateforme de production. Et donc, de délaisser, voir d'être laxasiste avec les environements de dev et les plateforme d'intégration continue. Je ne vais pas vous surprendre en disant que c'est certainement une très mauvaise idée. Surtout qu'avec l'arrivée du Cloud, dont la flexibilité repose massivement sur une chaine de déploiement continue irréprochable, tout un univers de faille et d'exploit nouveau s'ouvre aux attaquants, dans un domaine, où les experts de la sécurité sont très loin d'avoir évangélisé et diffusé les bonnes pratiques associées.

`FLD` Pour peu qu'ils aient réussi à correctement évalué tout les risques !

`RPE` Exactement. Alors, commeçons par le début, et listons quelques failles ou exploits intéressant sur du CI.

(in)securité du CI
----

1) Github

`RPE` Bon, of course, l'ami Github est le premier auquel on pense. Suffit de voir combien de résultat retourne une requête sur 'mysql_query' dans la code base, pour voir qu'on a déjà un bon point de départ.

https://github.com/search?p=3&q=extension%3Aphp+mysql_query+%24_GET&ref=searchresults&type=Code  (faire une photo)

`RPE` Bon, au final, c'est évident, et je pense que la plupart d'entre vous sont (ou plutôt pensent être) protégé, parce que "aucune personne dans la compagnie ne va jamais commité un mot de passe". Ouais, bon, allez, assumons que c'est vrai. De toute manière, y'a beaucoup plus retour à faire. Comme par exemple commité sous un autre nom - en effet, c'est la grosse faiblesse des DVCS par rapport à SVN/CVS, plus de centralisation. N'importe qui peut fusionner une PR venant de quelqu'un autre contenant des commits avec "d'autres auteurs".

`FLD` Ouais, mais c'est grave ça ?

`RPE` Ben déjà, ça fout en l'air d'audit trail. Tu recherches qui a injecté un code malicieux et ça ne te pointe pas sur la bonne personne, mais surtout ça ouvre la porte à des exploits "social". On a tous dans nos boites des "diva" dont personne ne va remettre le code en question parce que c'est "untel" qui l'a écrit. D'ailleurs, c'est exactement comment ça que Tordvals fait avec le kernel. Il ne pull que depuis des repos de gens qu'il connait et respecte. (@assistance, je vous rassure, les mecs comme ça y'en que 7. Je ne suis pas sûr que Tordvlad accepterait une PR de sa propre femme...)

`FLD` Ouais, Ok, donc tu fais une PR avec des commits venant d'un tel gus, et le code est accepté sans être revu...

`RPE` Laissant rentrer, par exemple, un code malicieux...

`FLD` OK, mais qu'est ce qu'on peut faire concrètement ?

`RPE` Ben des trucs simple, comme 1) se méfier des PR même venant d'auteur de confiance, si elles changent beaucoup de code. En fait, une PR (à mon sens), c'est comme une méthode Java ou un commit, ça doit pas être trop long. La même manière par exemple que je n'écris pas une méthode Java qui dépasse 5,6 lignes, et que je ne fais pas un commit avec 143 changements, je pense qu'une PR devrait contenir un petit ensemble de commit (ou un seul, même si perso, je trouve ça dommage).

`FLD` OK, mais sinon. Quoi d'autre ? Avoir une forme de tracabilité pour l'audit j'imagine ...

`RPE` Oui, exactement. Tu dois pouvoir déterminer qui a crée une PR, qui l'a accepté, etc... mais pas seulement. Par exemple, il faut aussi avoir un process pour nettoyé après le départ d'un employé de l'organisation. Effacer leurs repos, mais aussi, pourquoi pas, auditer leur répos publiques (même si ça pose des questions en terme de respect de la vie privée).

2) Jenkins

`FLD` Bon, et Jenkins alors ? Lui aussi j'imagine qu'il faut un peu le surveiller.

`RPE` Ah oui à fond, surtout que je connais beaucoup de gens qui non seulement n'impose pas d'authentification sur Jenkins - donc n'importe qui peut créer des jobs, mais le bouzin étant assez extensible, on peut même lui injecte des extensions via la "script console". Mais en fait, même si tu fermes ça, n'importe qui, qui peut crée un job, peut faire exécuter du code au serveur, donc...

`FLD` ... donc il est crucial de bien pouvoir tracer qui, depuis où, à créer ou lancer un job.

`RPE` Exactement.

TODO @FLD, tu veux développer les points ci dessous ?
* adhoc short lived build machine
* what about data ? and rtest data security ?

secret management
-----

`RPE`: Une des grandes failles introduit par les chaines d'intégration continue est bien évidemment, la gestion des secrets. Un développeur embarque un certificat SSL dans son code. Il l'a probablement bricolé à la main sur sa machine, pas forcément à jour, avec une version d'OpenSSL aussi robuste la dernière version de Windows (en fait, non, que n'importe quelle version de Windows). Bref, ce certificat tout pourri est poussé dans le gestionnaire de révisions, l'application est "buildé" par Jenkins, et jeter en production, avec le même certificat, sans même que personne ne se pose de questions...

`FLD`: Ouais, mais tu vois, c'est là qu'on est malin, car pour gérer nos secrets, on utilise chef-vault

TODO: @FLD là fo que tu développe

Managing secrets: still the hardest problem in operations (https://twitter.com/jtimberman/status/568124542553423872)

secret management : https://coderanger.net/chef-secrets/
chef-vault and citadelle

jce chef recipe
chef-vault

secret in your secret OAuth secrets
---


segregate your secrets from your source code
search in github.com for password, secret, key
et hop la on peut une recherche dans jhipster on y trouveras quelques secrets

we have oauth clientid and secret in jhipster
la encore je peux montrer comment on peut generer le oauth client et le oauth secret à la volée seuleument une fois l'authentication saml reussi

sepration of duties
rotate account information

Safer in the Clouds ?
-----

FLD: Ok, tout ça a plutôt marcher, mais maintenant, on va se débarrasser notre infra à nous, et migrer notre app, sur le Cloud. Vu qu'elle est déjà "secure", je dois revoir ma copie tu crois ?

RPE: Ben oauis, et plutôt deux fois qu'une ! Parce que maintenant, si ton appli par en sucette, ton fournisseur de "cloud" (comme Amazon), va littéralement tu le faire payer.

a $2.375 amazon mistake
http://www.devfactor.net/2014/12/30/2375-amazon-mistake/

`RPE` Bref, quand les gens pensent au "cloud", ils ont toujours l'image de nuages, tout jolie, flottant dans le ciel. Un doux rêve, où l'infrastructure technique est devenu d'une telle simplicité, executé ailleurs (dans les nuages), sans qu'on est réellement besoin de s'en soucier. C'est vrai que vu d'en bas, les nuages, c'est sympa, mais quand si vous pilotez votre petit avion à l'intérieur d'un nuage, vous allez voir une vision très, très différente de la chose ! Déployé son infrastructure sur le "cloud" demande non seulement de penser à la sécurité, au delà des maigres éléments apportés par le fournisseur, mais aussi et surtout, d'y penser différament !

#### never assume it's safe

`FLD`: Ah oauis, ça fait mal tout ça, surtout qu'on pensait s'intégrer avec S3. Du coup, on va peut être aller voir ailleurs.

`RPE`: Oui, mais ça change rien, dès l'instant où tu t'intègres avec un système externe, il faut grosso modo partir du principe qu'il est pas 'secure' et te protéger de lui.

`FLD`: En fait, il faut se dire "never assume it's safe".

`RPE`: Exactement. Si tu utilises, par exemple, Google Authentification, il faut aussi réflechir, pour la sécurité de ton application, au cas où un attaquant arrive à s'emparer d'un jeton. En soit, ton application ne pourra pas forcément s'en rendre compte, mais c'est là qu'avoir un "audit trail" mais aussi une gestion fine des droits - tiens, c'est bizarre, ça fait trente fois qu'un utilisateur lambda cherche à accéder aux données financière ! - est essentiel.

### safer in the cloud

`FLD`: Bon, en gros, au final, le cloud c'est la jungle, et on est plus secure chez soi en fait ?

`RPE`: Non, au contraire ! Le cloud te force à faire plus gaffe à ta sécurité, pour toutes les raisons qu'on vient d'évoquer, mais t'apportes bcp en termes de sécurité. Y'a qu'on bien de système non maintenu, qui tourne depuis 10 ans, sans le moindre de security patch appliqué dans ton infra ?

`FLD`: (gros sourire) ben aucun bien sûr ;) !

Slide:
a 10 years old server in your data center is much more vulnerable than a fresh server in the cloud

a 10 years old server, imagine
* accumulated rot
* configuration shift
* quaterly security review ? this clash with continous delivery
a typical aws server last a few days

`RPE`: Exactement ;) - dans le cloud tes machines sont constament reconstruit "fraîche" et patché. Un super exemple est Neflix. Il sont très connu par avoir une service irréprochable qui repose sur la solution de Cloud d'Amazon. Si vous avez bossé sur Amazon, vous savez que bien d'excellente qualité, le service n'est pas à 100% fiable. Une VM peut subitement "disparaitre", le réseau peut devenir temporairement inaccessible, et leur SLA prévoit même qu'une zone entière (par exemple l'Irlande) peut tomber pendant plusieurs minutes !
Bref, dans ces conditions, pour fournir un super service comme Netflix, il faut que les applications soient très robuste ! Et là, ils ont été géniaux, c'est qu'ils ont forcé leur developeur à se préparer aux pannes et mettant en place un programme simulant ces pannes - le fameux Chaos Monkey. Et le plus incroyable, c'est qu'ils sont tellement sûr de la résilience de leur applications qu'ils laissent Choas Monkey s'exécuter sur leur plateforme de production !!!
http://techblog.netflix.com/2012/07/chaos-monkey-released-into-wild.html

`FLD`: Ah ouais, c'est une approche courageuse qui l'avantage finalement de dire de remplacer une possibilité (ça peut foirer) par une certitude (ça va foiré).

CCL du talklet

`RPE`: Voilà, on a fait un tour rapide, mais comme on peut le voir, l'extension du périmètre de lutte de la sécurité est réelle, et offre un monde de nouveau exploit et de failles à exploiter. Il est évident que, pour le moment, on dispose encore peu d'informations et de recul, et que les approches, dans le domaine de la sécurité, consiste essentiellement à appliquer les "vieilles" recettes. Néanmoins, il ne faut pas avoir peur et retomber un travers inutile et nuisibile de rejet de ces nouvelles infrastructures.

(brain breaks - probablement à améliorer)
`FLD` Ouais, de toute façon, il faut jamais avoir peur.

`RPE` Pourquoi ça ?

`FLD` Ben, la peur c'est le coté obscur non ? (peut être coller un slide rigolo, genre de Yoda pour appuyer la blague)

`RPE` (prends un air blazé, un peu à la mode "François, tu as encore fait un dessins...")

@FLD, je pense que la notion de "peur" est un bon moyen d'embrayer sur la partie "fireman", si on change le brain break, il faudra penser à garder la peur dans le nouveau motif
