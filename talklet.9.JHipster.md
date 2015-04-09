`slide-11` Notre cas d'étude
---

`RPE` maintenant qu'on sait par ou commencer, regardons ton appli

`FLD` c'est pas une appli pour placer des pubs, ni pour spéculer sur les marchés financier, ce n'est donc 
ni big data, 
ni du hadoop, 
ni du machine learning, 
ni social, 
ni du docker,

bref pas  très hipster... 

c'est juste une bonne vieille appli web de gestion

`RPE` mais comment tu vas draguer sur la plage ou te la peter sur  twitter ?

`slide-12` JHipster
---

`FLD` du coup je suis parti sur une stack jhipster

`RPE` c'est quoi jhipster ? Encore un framework MVC ? Un truc qui springboot pour lancer un container scala écrit en JRuby qui exécute des greffons Groovy, avec une extension en cours de fabrication pour trouver une excuse pour utiliser Ceylon ou Closure ?

`FLD` Presque :) C'est un generateur d'appli web à la appfuse - pour ceux qui s'en rappelle

`RPE` (vers la salle), si vous vous en rappellez, vou faites du Java depuis trop longtemps.

`slide-13` Yo JHipster
---

`FLD` Quant aux autres et à ceux qui sont su resté jeunes, eux connaissent certainement javascript et yeoman. JHipster est basé sur yeoman. tu commences par ce script:

`FLD` yo jHipster et tu choisis ....

`FLD` et la du choisis Dr Dree, Eminem, East cost? West Cost ?
 

`slide-14` JHipster homepage
---

`FLD` bon en gros je finis une stack assez simple et au gout du jour avec du springboot pour la partie serveur et du angularjs pour le partie cliente

`RPE` ok mais niveau sécu, t'as quoi ?


`slide-15` Spring Security
---

`FLD` Justement, ce qui m'a attiré dans ce stack c'est aussi la tringlerie Spring security qui vient avec.

Il m'offre une bonne base de travail pour gérer l'authentication, l'authorisation, les roles. 

et me donne un grand choix d'authorisation et authenticatio

`RPE` man in the middle attack

`FLD` Spring Secu supporte HSTS qui indique au client que seul https sera utilisé.

`RPE` clickjacking ?

`FLD` frameOptions().sameOrigin()

`RPE` et les attaques XSS ?

`FLD` ca gère toout comme  les attaques de type Cross site scripting forgery, il me fournit une solution  à base crsf Token, 

`RPE` et plein d'acronyme anglais pour te la peter, et sinon niveau audit ?

`FLD` aussi... il fournit une bonne trame pour l'audit et logs relatifs à la sécurité.
n


