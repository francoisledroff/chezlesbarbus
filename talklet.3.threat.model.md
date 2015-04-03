`Talklet 3` Threat Model
--------

`slide-20` Thread Modeling STRIDE
-------

`FLD` Une méthode intéressant poussée par Microsoft et OWASP est appelée le "Threat Modeling"

Elle permet de mieux identifier les menaces ainsi que les vulnérabilités de votre système

Avec l'acronyme STRIDE Elle propose une categories des attaques possibles selon les types d'exploitation qui leur sont associés , 

Nous n'avons pas le temps de tout couvrir aujourd'hui mais je vous invite à une lecture sur wikipedia ou sur le site OWASP.

A chaque categorie corresponde des mesures à mettre en place

`RPE`
prenons le R de repudiation par example, pour éviter que vos utilisateurs contestent les transactions faites avec leur login et depuis leur machines, mettez en place un "audit trail" sur chacun de vos tiers applicatifs.


`slide-21` Threat Modeling DREAD
-------

`FLD`
Avec l'acronyme DREAD cette methode propose également un système de classification pour comparer, qualifier et prioritiser les risques associés à chaque menaces.


Ce methode vous aidera à founir à vos équipes de sécu, d'ops et de dev 

* une vue d'ensemble de l'applicatif et de ses défenses
* une modélisation les interactions entre les différents composants de l'application, les flux de données, les séparations de privilèges entre composants et les éléments de stockage,


`FLD` cette analyse qui à première vue me paraitre très "barbante" s'avère être un exercice très intéressant.

Elle vous aidera à la décision, et à prendre en vue de sécuriser l'application.

`slide-22` Nos données.
-------

`RPE` il nous faudra beaucoup plus de temps en effet pour creuser l'ensemble des concepts introduits ici, ce qui me parait primordial c'est de comprendre la gravité de voir tes données fuiter. Quelles sont ces données ? Sont elles classifiées ? confidentielles ?



====
===== 


* Spoofing Identity : ensure a single execution context at the application and database level.
* Tampering with Data : data validation
* Repudiation: audit trails at each tier
* Information Disclosure: persist/cache as little info as possible
* Denial of Service, do not allow anonymous, or do as little as possible for anonymous
* Elevation of Privilege : proper ACL in place




Microsoft
https://www.owasp.org/index.php/Threat_Risk_Modeling
http://linuxfr.org/news/threat-modeling-savez-vous-quelles-sont-les-menaces-qui-guette
https://www.owasp.org/index.php/Threat_Risk_Modeling
