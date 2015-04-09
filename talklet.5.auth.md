`Talklet 5` Auth
==========

`slide-28` JHipster login page
-----------

`RPE` Ah je vois que par défaut, jhipster a sa propre base de donnees d'utilisateur, pas mal pour le dev, mais une cata pour la prod !

`FLD` une véritable plaie, non seuleument pour la sécurité mais également pour l'expérience utilisateur.
En tant qu'utilisateur je trouve difficile à justifier.

`RPE` t'es pas le seul, le simple fait de devoir creer et gerer un n-ieme mot de passe peut dramatiquement reduire la retention d'utilisateurs.
  
`FLD`
Si votre site est publique, pourquoi ne pas me proposer de me logger avec openid, facebook, google, twitter et surtout github si votre public est un public developpeurs.

`RPE` et la je dis merci ou cfp.devoxx...

`FLD` Si votre site est pro, vous avez surement un ldap ou mieux un identity provider ? 

`slide-29` Votre mot de passe (xkcd)
--------

`FLD` Autres questions qui me viennent à l'esprit devant ce genre d'ecran :

Quelles seront les règles spécifiques à ce nouveau mot de passe ?
Va-t-il encore m'imposer des contraintes inèptes relatives à l'ulisation des caractères speciaux et  
chiffres ?

`respiration`

`RPE` depuis que j'ai vu ce xkcd Je suis assez fan de ces pass phrase mais toute ma famille se plaint que le mot de passe du wifi à la campagne est trop long ! Pourtant "Romain a des plus jolie cheveux que ses soeurs", c'est pas compliqué à retenir, non ? :)

`FLD` "Romain a des plus jolie cheveux que ses soeurs" 46 caractères dans jhipster 46 characters ca passe mais de justesse... 
La seule contrainte imposée sur ce mot de passe c'est qu'il doit faire entre 6 et 50 caractères.




`slide-30` 1 mot de passe (incorrect)
--------

 `RPE` rien ne m'empêche non plus de choisir un mot de passe "incorrect" 

`FLD` et j'imagine que tu reutilise le meme mot de passe partout ?

`RPE` pas toi ?

`FLD` pas moi ;-) Et j'en décompte 156 

`slide-31`  156 mots de passe ?
--------

`FLD` je les génère,  les renouvelle, les chiffres, les stock sur mon disque
et pour ca forcemment j'ai un outil


`slide-32` 1 chien ?
------

`RPE` t'as 156 mot de passe, mais a quoi bon ? je connais le nom de ton chien

`note` on respire, on laisse les gens rigoler

`FLD` ok tout le monde a reconnu Paris Hilton ? 

`RPE` moi j;ai reconnu le chien

`FLD`

Paris s'est fait hacke sous compte  chez T-Mobile qui pour protéger le mot de passe de ses clients 

T-Mobile n'avait pas choisie une question bien originale... 

Mais est-il si facile de trouver des questions dont les réponses ne soit déjà partagés sur le web à travers reseaux sociaux, blogs, tabloids, et journaux 

`RPE` en meme temps qui voudrait vraiment partager un vrai secret avec son operateur telephonique ? 

`slide-33` des Secrets ? (tweets)
------

`FLD` qui voudrait partager ses secrets avec avec facebook, snapchat, meetic, tinder, gleeden ?

`RPE` Mais qui ne partage quelques secrets avec son banquier ?

`FLD` Et qui n'utilise pas de carte à puces, des cartes SIM ?

`RPE` Dans la vraie vie, un secret c'est quelque chose que vous ne partagez qu'avec une seule personne à la fois.

`FLD` et dans le vraie vie comme sur le web tout des oreilles trainent

`RPE` Partout

`slide-34` 100%
------

`FLD` on est donc d'accord : pour faire court, les mots de passe, c'est juste "mal".

`note` pause respiration, on laisse lire le public

`RPE`  Bref, comme je le dis souvent, si tu veux pas de divorce, te marie pas, ben pareil, si tu veux pas qu'on te vole to password, t'as qu'à pas en avoir !

`FLD` Notre but :
N’être qu’un fournisseur de service
Identifier un fournissseur d’identité de confiance
S’y interfacer

`RPE` A qui peut-on faire confiance ?

`FLD` c'est toute la difficulté

`RPE` : Adobe, comme nous Red Hat, vous avez forcemment fait un choix, vous avez une solution de gestion d'identité ? 

Si vous n'avez pas, je crois qu'on en vends 4 différents au dernier compte ! (Si vous prenez une paire de QUeue JMS, en plus, on fait un prix ;) ).



`slide-35` 1 IDP ?
-------



`FLD`  Oui bien sûr, j'ai donc modifié mon appli généré, 

 
`RPE` ok donc tu présentes donc cette page a mister anonymous, et tu lui propose un lien vers une resource protégé par ton fournisseur d'idendité

`FLD` Oui mon IDP comme la plupart des solutions supporte le standard SAML


`slide-36` SAML ?
-------



c'est un standard qui permet de faire du SSO sur le browser.
si vous voulez débutez et tester votre solution, jetez un coup d'oeil à www.ssocircle.com 


`slide-37` SAML & JHipster ?
-------
`RPE` Mais dis, JHipster ne supporte pas saml

`FLD` non, 
mais Spring Security le fait. 

j'ai viré la gestion de mot de passe, j'ai viré pas mal de code, j'en ai rajouté un peu, j'ai pas mal trébuché, fini avec peu de code et beaucoup d'annotations

`FLD` a choisir je préfère tout de même l'annotation hell au xml hell....
Et Spring Security s'y prête plutot bien.

`RPE` a Quand ton pull request ?
oui c'est en projet, il y a deja un ticket le 695 qui lui associé.


`slide-38` SAML Sequence Diagram
-------

`RPE` Alors Saml ? comment ça marche ?

`FLD` Le plus compliqué finalement, c'est la config.

* il faut recuperer le meta données de l'idp et fournir a ton moteur client saml
elle contienne un certificat et des url à associer à la redirection en vue d'un login ou tout au moins d'une verification  d'identité

`RPE`
* et toi tu fournis à l'idp, quelques metadonnées comme
  *  certificats et url associer à la redirection en vue d'un login et logout.
  
`FLD` ok donc tu ceux acceder a ma une resource protégé 

`FLD` mon fournisseur de service dit 

* "Not authorized", je te connais pas, je te donne pas le service, je te donne pas la resource, 
* va prouver ton identité au pres du fournisseur d'identité, 
* il reviendra vers moi, 
* si son retour est valide, je te donnerai accès à ma resource 
* tout du moins si les infos d'idendité extraite dans l'enveloppe saml me permette de te donner le role necessaire pour etre autorise à acceder a ce service ou cette resource.



`slide-39` login link
-------

`RPE` alors voyons je click! 
 

`slide-40` okta 1 factor
-------

`RPE` ok donc tu es redirigé ici sur ton idp, tu rentres un mot de passe
`FLD` oui ici mon mot de passe ldap sur adobeNet


`slide-41` okta 2nd factor
-------

`RPE` et t'as demandé a ton IDP d'appliquer un second facteur.

`FLD` Oui le user doit me prouver, me donner
 
 * ce qu'il sait : son password
 * ce qu'il a : un telephone ou autre generateur de token
 
 
`slide-42` logged-in
-------
 
 `RPE` c'est pas relou ca pour les utilsateurs ?
 
 `FLD` c'est vrai que l'equilibre entre expereience tuisateur. confort et securite n'est  pas evident a trouver.
 

`slide-43` wired
----

`FLD`

tu connaissez le chien de  Paris Hilton ?
mais tu connaissez ce gars ?

`RPE`
pas avant que tu m'en parles, mais pares avoir lu cet article 
je comprends que tu veuilles passer en 2 FA

`FLD`
Oui je l'ai active sur mon compte twitter, facebook, google, yahoo 

paypal, github


`RPE` en tant que developpeurs il est de votre responsabilité de protéger vos secrets, vous êtes la cible des hackers

`FLD` vous avez votre profil sur linked-in, et vous êtes devops ou security specialist chez BNP ou 1 ms valent 100 millions d'euros ? et dont le portefeuille de produits dérivés em 2013 s’élevait à 48 000 milliards d’euros, soit 24 fois le PIB de la France

http://www.lemonde.fr/economie/article/2013/12/17/les-produits-derives-depassent-leur-niveau-d-avant-crise_4335868_3234.html

`RPE` Quoi ?

`FLD` 1ms pur 100 millions, 1 sec 100 milliards, je me demandais juste un hack de 8 minutes seconde suffirait-il pour jouer 24 fois le PIB de la France sur les marchés ?

`RPE` Bret.. en tant que dev ou ops vous êtes une cible .


`slide-34` 2FA
----


`FLD` allez faire un tour sur twofactors.org, voyez ou vous pouvez activer le 2FA, et faites vos choix en fonction

`RPE` laissez tomber docker

`FLD` preferez github a bitbucket

`RPE` si vous navez peur de rien, utiliser ces services de finance en ligne

`FLD` que l'internet of things et les applis santé font globalement fi de la securité,  pareil pour la plupart des micro paiement, 


`RPE`en fait le plus secure, etonnamment les reseaux sociaux...

`FLD` et le sreseaux sociaux en UX il sy'connaissent, ils ont trouver un equilibre interesant mais en mettant en place le 2FA
mais en vous permettant egalement de definir vos telephone et vos  navigateurs de confiances sur lesquels votre session sera maintenue.


`RPE` et j'imagine que tu le fais ? ?




slide saml + oauth
-----

`FLD`
rappelle moi romain on a saml
une fois authentifié je vais
* provisionner un client oauth rien que pour toi (avec ton client idet secret )
* et t'inviter a faire a la dance oauth

`RPE` ok donc une fois logué, et apres quelques redirect je receiupre un token...
mais bon il perime le token non ?

`FLD` oui mais refresh tokem

`RPE` ah mais ca pue 

`FLD` oui mais c'est revocable

slide revoke
------

`RPE` tu peux aller plus loin

`FLD` oui email...

slide option
----

`FLD`
et sinon on avait d'autre option

`RPE`
oui parce que oauth2 ,  No standard (yet) for request signing

`FLD` en fait avec le JWT token et spring security tu peux le faire...

`RPE` mais oui mais pourquoi pas oauth1 ?

oauth1 ping pong



