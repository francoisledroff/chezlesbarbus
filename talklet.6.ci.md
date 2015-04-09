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



annexe
-----

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


