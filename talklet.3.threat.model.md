`Talklet 3` Threat Model
--------

`RPE` c'est vrai que quand on commence à réflechir en terme de sécurité, on ne voit soit "rien à faire", soit des trous de sécurité partout, et insurmontable. 

C'est vrai que c'est un peu difficile, comme ça, de regarder son app, et de faire une sorte de sain inventaire, une analyse de menaces en quelques sortes...



`FLD` Ben justement, y'a une méthode intéressant poussée par Microsoft et OWASP est appelée le "Threat Modeling"

Elle permet de mieux identifier les menaces ainsi que les vulnérabilités de votre système

`rpe` ccm ?

`slide-20` Identifier les menaces
-------


`FLD` Avec l'acronyme STRIDE Elle propose une categories des attaques possibles selon les types d'exploitation qui leur sont associés ,

Nous n'avons pas le temps de tout couvrir aujourd'hui mais je vous invite à une lecture sur wikipedia ou sur le site OWASP.

A chaque categorie corresponde des mesures à mettre en place

`RPE` Ok, alors soyons didactique, et prenons un exemple concret. Par exemple, là, ce R de repudiation. Qu'est ce que ça veut dire ?

`FLD` Ben c'est pour éviter que vos utilisateurs contestent les transactions faites avec leur login et depuis leur machines, mettez en place un "audit trail" sur chacun de vos tiers applicatifs.

`RPE` En effet, si on doit inputer à quelqu'un une manipulation malhonnête sur une transaction, c'est probablement de pouvoir le prouvé sans l'ombre d'un doute.

`slide-21` priority  
-------


`FLD` Avec l'acronyme DREAD cette methode propose également un système de classification pour comparer, qualifier et prioritiser les risques associés à chaque menaces.

`RPE` au final tu finis avec un shema d'archi orientée sécurité
qui offre  une vue d'ensemble de l'applicatif et de ses défenses


`FLD` cette analyse qui à première vue me paraitre très "barbante" s'avère être un exercice très intéressant.

Elle vous aidera à la décision

`RPE` Note que les "barbus" ou les techos en général trouvent ce genre de méthodologie souvent un peu "bullshit", ça permet surtout de faire comprendre au management qu'il y a un problème, dans un format qu'ils peuvent comprendre et réutiliser.

`FLD` Si vous êtes coté management  et que vous soupçonnez que ces barbus ont été un peu trop "naif" ou paresseux avec la sécu, faire ce genre d'inventaire est aussi un bon moyen de leur faire réaliser le problème.


