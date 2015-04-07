`Talklet 3` Threat Model
--------

`RPE` Pour revenir à l'angoisse que tu exprimais au début, c'est vrai que quand on commence à réflechir en terme de sécurité, on ne voit soit "rien à faire", soit des trous de sécurité partout, et insurmontable. C'est vrai que c'est un peu difficile, comme ça, de regarder son app, et de faire une sorte de sain inventaire, une analyse de menaces en quelques sortes...

`slide-20` Thread Modeling STRIDE
-------

`FLD` Ben justement, y'a une méthode intéressant poussée par Microsoft et OWASP est appelée le "Threat Modeling"

Elle permet de mieux identifier les menaces ainsi que les vulnérabilités de votre système

Avec l'acronyme STRIDE Elle propose une categories des attaques possibles selon les types d'exploitation qui leur sont associés ,

Nous n'avons pas le temps de tout couvrir aujourd'hui mais je vous invite à une lecture sur wikipedia ou sur le site OWASP.

A chaque categorie corresponde des mesures à mettre en place

`RPE` Ok, alors soyons didactique, et prenons un exemple concret. Par exemple, là, ce R de repudiation. Qu'est ce que ça veut dire ?

`FLD` Ben c'est pour éviter que vos utilisateurs contestent les transactions faites avec leur login et depuis leur machines, mettez en place un "audit trail" sur chacun de vos tiers applicatifs.

`RPE` En effet, si on doit inputer à quelqu'un une manipulation malhonnête sur une transaction, c'est probablement de pouvoir le prouvé sans l'ombre d'un doute.

`slide-21` Threat Modeling DREAD
-------

@FLD: il faudrait introduire DREAD , comme pour STRIDE, et soulignes ce qui les différencie.

`FLD` Avec l'acronyme DREAD cette methode propose également un système de classification pour comparer, qualifier et prioritiser les risques associés à chaque menaces.

Cette methode vous aidera à founir à vos équipes de sécu, d'ops et de dev

* une vue d'ensemble de l'applicatif et de ses défenses
* une modélisation les interactions entre les différents composants de l'application, les flux de données, les séparations de privilèges entre composants et les éléments de stockage,

`FLD` cette analyse qui à première vue me paraitre très "barbante" s'avère être un exercice très intéressant.

Elle vous aidera à la décision, et à prendre en vue de sécuriser l'application.

`slide-22` Nos données.
-------

`RPE` il nous faudra beaucoup plus de temps en effet pour creuser l'ensemble des concepts introduits ici, ce qui me parait primordial c'est de comprendre la gravité de voir tes données fuiter. Quelles sont ces données ? Sont elles classifiées ? confidentielles ?


* Spoofing Identity : ensure a single execution context at the application and database level.
* Tampering with Data : data validation
* Repudiation: audit trails at each tier
* Information Disclosure: persist/cache as little info as possible
* Denial of Service, do not allow anonymous, or do as little as possible for anonymous
* Elevation of Privilege : proper ACL in place


Microsoft
https://www.owasp.org/index.php/Threat_Risk_Modeling
http://linuxfr.org/news/threat-modeling-savez-vous-quelles-sont-les-menaces-qui-guette
