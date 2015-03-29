`Talket 6` Extension du périmètre de la lutte - CI & Cloud
=========

`RPE` Jusqu'à maintenant, quand on pense sécurité des applicatis, on a naturellement tendance à penser au plateforme de production. Et donc, de délaisser, voir d'être laxasiste avec les environements de dev et les plateforme d'intégration continue. Je ne vais pas vous surprendre en disant que c'est certainement une très mauvaise idée. Surtout qu'avec l'arrivée du Cloud, dont la flexibilité repose massivement sur une chaine de déploiement continue irréprochable, tout un univers de faille et d'exploit s'ouvre aux attaquants, où les experts de la sécurité sont loin d'avoir évangélisé et diffusé les bonnes pratiques associées.

`FLD` Pour peu qu'ils aient réussi à correctement évalué tout les risques !

(in)securité du CI
----

git and jenkins , chef, vagrant exploits
https://twitter.com/morlhon/status/554899543150850048

adhoc short lived build machine

audit - si un "build" sur votre serveur d'intégration est à l'origine d'un exploit sur les machines de production, êtes vous en mesure d'identifier qui et quand a démarré le "build" ? 

what about data ? and rtest data security ?


A must-read  : @paulgreg: interesting slide on security of your webapp "DevOoops"  by @carnal0wnage #devops #hacking http://www.slideshare.net/chrisgates/lascon-2014-devooops …”

-> le spoof de Git Hub est intéressant, car c'est un bon exemple d'exploit "social". On peut
imaginer une PR sur un projet prétendant venir de XXX insérant une faille... Je pense qu'il faut
qu'on mentionne que le "hack" social reste une des principales failles de sécurité.

secret management
-----

`RPE`: Une des grandes failles introduit par les chaines d'intégration continue est bien évidemment, la gestion des secrets. Un développeur embarque un certificat SSL dans son code. Il l'a probablement bricolé à la main sur sa machine, pas forcément à jour, avec une version d'OpenSSL aussi robuste la dernière version de Windows (en fait, non, que n'importe quelle version de Windows). Bref, ce certificat tout pourri est poussé dans le gestionnaire de révisions, l'application est "buildé" par Jenkins, et jeter en production, avec le même certificat, sans même que personne ne se pose de questions...

`FLD`: Ouais, mais tu vois, c'est là qu'on est malin, car pour gérer nos secrets, on utilise chef-vault

https://twitter.com/jtimberman/status/568124542553423872
Managing secrets: still the hardest problem in operations.

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

CI and security
-----

FLD: Ok, tout ça a plutôt marcher, mais maintenant, on va se débarrasser notre infra à nous, et migrer notre app, sur le Cloud. Vu qu'elle est déjà "secure", je dois revoir ma copie tu crois ?

RPE: Ben oauis, et plutôt deux fois qu'une ! Parce que maintenant, si tu applis par en sucette, ton provider Web, va littéralement tu le faire payer.

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

CCL:

`RPE`: Voilà, on a fait un tour rapide, mais comme on peut le voir, l'extension du périmètre de lutte de la sécurité est réelle, et offre un monde de nouveau exploit et de failles à exploiter. Il est évident que, pour le moment, on dispose encore peu d'informations et de recul, et que les approches, dans le domaine de la sécurité, consiste essentiellement à appliquer les "vieilles" recettes. Néanmoins, il ne faut pas avoir peur et retomber un travers inutile et nuisibile de rejet de ces nouvelles infrastructures. 

(brain breaks - probablement à améliorer)
`FLD` Ouais, de toute façon, il faut jamais avoir peur.

`RPE` Pourquoi ça ?

`FLD` Ben, la peur c'est le coté obscur non ?

