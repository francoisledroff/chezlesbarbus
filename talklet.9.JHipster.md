`slide-11` Notre cas d'étude
---

`FLD` c'est pas une appli pour placer des pubs, ni pour spéculer sur les marchés financier, ce n'est donc ni big data, ni social, ni très hipster... c'est juste une appli web de gestion

`slide-12` JHipster
---

`FLD` mais comme je voulais me faire plaisir je suis parti sur un stack jhipster

`RPE` c'est quoi jhipster ? Encore un framework MVC ? Un truc qui springboot pour lancer un container scala écrit en JRuby qui exécute des greffons Groovy, avec une extension en cours de fabrication pour trouver une excuse pour utiliser Ceylon ou Closure ?

`FLD` Ouais, exactement ! :) Non, c'est un generateur d'appli web à la appfuse - pour ceux qui s'en rappelle

`RPE` (vers la salle), si vous vous en rappellez, j'ai une mauvaise nouvelle pour vous : vous êtes vieux.

`slide-13` Yo JHipster
---

`FLD` Quant aux jeunes et à ceux qui sont su resté jeunes, eux connaissent certainement javascript et yeoman. JHipser est basé sur yeoman. tu commences par ce script:

`FLD` yo jHipster

`FLD` Tu fais quelques choix ? East Coast ou West Coast ?

`slide-14` JHipster homepage
---

`FLD` le résultat est une stack assez lean, plutot récent avec du springboot pour la partie serveur et du angularjs pour le partie cliente

`RPE` ok, bon  à part télécharger la terre entière pour foutre je ne sais combien de couche d'abstraction à la mode Java, je vois surtout t'es parti sur du oauth2 et du mongodb. MongoDB c'est pour faire cool et draguer les filles sur la plage, c'est ça ?

`FLD` Exactement ! :-)

`slide-15` Spring Security
---

`FLD` Plus sérieusement, ce qui m'a attiré dans ce stack c'est aussi la tringlerie Spring security qui vient avec.
Il m'offre une bonne base de travail pour gérer l'authentication, l'authorisation, les roles. Il me fournit une solution contre les attaques de type Cross site scripting forgery à base crsf Token, et me fournit une bonne trame pour l'audit et logs relatifs à la sécurité.

`RPE` Ouais, c'est plutôt chouette en effet tout ça.
