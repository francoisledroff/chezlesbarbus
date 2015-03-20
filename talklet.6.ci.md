`Talket 6` CI & Secret Management & the Cloud
=========

todo


`Talket 6` Draft
=======


secret management
-----

FLD: Ouais, mais tu vois, c'est là qu'on est malin, car pour gérer nos secrets, on utilise chef-vault

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

a $2.375 amazon mistake
http://www.devfactor.net/2014/12/30/2375-amazon-mistake/


+1 slide sur ça

CI and security
-----


### (in)securité du CI

git and jenkins , chef, vagrant exploits
https://twitter.com/morlhon/status/554899543150850048

adhoc short lived build machine

waht about data ? and rtest data security ?


A must-read  : @paulgreg: interesting slide on security of your webapp "DevOoops"  by @carnal0wnage #devops #hacking http://www.slideshare.net/chrisgates/lascon-2014-devooops …”

-> le spoof de Git Hub est intéressant, car c'est un bon exemple d'exploit "social". On peut
imaginer une PR sur un projet prétendant venir de XXX insérant une faille... Je pense qu'il faut
qu'on mentionne que le "hack" social reste une des principales failles de sécurité.


Clouds looks nice from afar, but try piloting your Cessna through one !
-----

FLD: Ok, tout ça a plutôt marcher, mais maintenant, on va se débarrasser notre infra à nous, et migrer notre app, sur le Cloud. Vu qu'elle est déjà "secure", je dois revoir ma copie tu crois ?

RPE: Ben oauis, et plutôt deux fois qu'une ! Parce que maintenant, si tu applis par en sucette, ton provider Web, va littéralement tu le faire payer.

#### never assume it's safe

FLD: Ah oauis, ça fait mal tout ça, surtout qu'on pensait s'intégrer avec S3. Du coup, on va peut être aller voir ailleurs.

RPE: Oui, mais ça change rien, dès l'instant où tu t'intègres avec un système externe, il faut grosso modo partir du principe qu'il est pas 'secure' et te protéger de lui.


### safer in the cloud

FLD: Bon, en gros, au final, le cloud c'est la jungle, et on est plus secure chez soi en fait ?

RPE: Non, au contraire ! Le cloud te force à faire plus gaffe à ta sécurité, pour toutes les raisons qu'on vient d'évoquer, mais t'apportes bcp en termes de sécurité. Y'a qu'on bien de système non maintenu, qui tourne depuis 10 ans, sans le moindre de security patch appliqué dans ton infra ?

FLD: (gros sourire) ben aucun bien sûr ;) !

RPE: Exactement ;) - dans le cloud tes machines sont constament reconstruit "fraîche" et patché (là RPE parle de Netflix)

=> là je peux expliquer le cas de Netflix où justement, aucun serveur en prod ne dure que qql
jours... plus leur approche "Choas Monkey" qui est phénoménale !
http://techblog.netflix.com/2012/07/chaos-monkey-released-into-wild.html

a 10 years old server in your data center is much more vulnerable than a fresh server in the cloud

a 10 years old server, imagine

* accumulated rot
* configuration shift
* quaterly security review ? this clash with continous delivery

a typical aws server last a few days

