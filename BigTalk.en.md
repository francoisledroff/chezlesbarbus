`Talklet 1` Intro
====


Hello
-------

`FLD` Hi everybody ! Welcome to our talk, here, at Code Motion Berlin. We are delighted to have
you with us today. 
But... anyway... we have a lot to cover, let's get started ! Romain, what don't you start by introducing yourself ?


Romain
------

`RPE` Yep, I'll be first. So my name is Romain Pelisse, I'm a sustain developer on JBoss EAP at Red Hat -
sustain developer is a fancy title, but I do is mostly simply fixing bugs in our Java code. If I'm a Java developer, I also
have a strong experience with RHEL (Red Hat Linux) and the infrastructure universe.

And you ?

Francois
------

`FLD` I am Francois, I'm super happy to be in Berlin today, it's been 20 years, since I last came here. I'm a developer at Adobe. I mainly do plumbing....
I implement distributed systems on top of Java, on top of infrastructure I implement using Chef. And I'm lucky to be surrended by a great team, among them hispters, hipsters who imlement great web and desktop UI using vintage languages such as js, css and html.


Security Audit
----

`RPE` Let's go François ? We did sell'em something about "security audit", didn't we ?

`FLD` yeah, but the more I think about it, the less I'm convinced a vintage security audit would make sense these days...

`RPE` Ok cool don't want to do it either, sounds like the job of some bullshiters wearing suit

`FLD` And remember, our killer app, the one we wanted to release for code motion Berlin, is still a prototype.

`RPE` granted, but you do realize that the only thing separating a prototype for being production ready,
is that nobody has yet put the prototype in production... yet.

`FLD` Indeed.  should beAnd if Also don't you think that waiting for the app to be finished, means it's too
late for the audit ?

`RPE` at the end, you won't be able to fix a *broken architecture*, 2 days before prod...

`FLD` Agreed . I would rather spend on continuous security and and security training for all.  Talking about training, the architect is defintely not a security guru, plus, he got maried, shaved his bears, stopped coding at night... he got a kid.


`RPE` Are we you still on speaking terms after that ???

`FLD` Can't do otherwise, i'm the architect

`RPE` Though break

`RPE` No issue, as we'll see, security is about team work...

Continuous Security
----

`RPE` ... and this is s basically our message of today 

`FLD` so if you are manager, Remember "security is continuous or it's not, It's everybody responsability, including yours, provide security training for all"

`RPE` so if you are manager, now it means you can already leave the room or fall asleep.

`pause`

`RPE` That being said, where do we start? Because security is a rather broad topic to say the least

Threat Modeling
--------

`FLD` Indeed. Security is continuous process, touch any and all level, needs to have a global vision 
but I wondered should we deal with such a large scope ? 
I seeked for help.
I've been told to look into an interesting.
methodology pushed from M$ and OWASP.

It's called "Threat Modeling". 

it's supposed to be really helpful.

`RPE` Ok, nice on a resume, cool to brag during interview people or chat over a beer, but
what does it actually do ?

`FLD` Well, you need to isolate, pick a small a small enoug sub-systems, within your overall solution. For the threat model to remain manageable, that is feasible within a projcet iteration sprint, and to be readable, understood by all.  


Identify the threats: STRIDE
-------

`FLD` first step : identifying the threats 
and this model provides a mnemonic acronym to list the
diffents categories of threats.

`RPE` Ok, so we have not time to cover that - it would complete separate talk. Let's be practical,
look at one them. For instance, what R stands for ?

`FLD` the threat behind that is user denial (example)

`RPE` How to fix or mitigate the impact as they say ?

`FLD` Audit trails prooving without doubt cred used

`RPE` ... and that is something you can NOT fix when the app is ready. It's already too late. You're
screwed :)


Assess the risks: DREAD
-------

`FLD` key aspect => assess the risk business wise. thus DREAD providing a classification scheme

`RPE` Damage meaning how bad would an attack be?

`FLD` Reproducibility - how easy is it to reproduce the attack?

`RPE` Exploitability - how much work is it to launch the attack?

`FLD` Affected users - how many people will be impacted?

`RPE` Discoverability - how easy is it to discover the threat?

`FLD` Id treats + risks behind helps to do ...

`RPE` Or not.

`FLD` @first relunctant, proposed by some security expert, but I found it very useful

`RPE` communication tool between top management and low level expert - making each other language
understandeable by the other one

Our App
---

`RPE` Brilliant, we know where to start. let's take a look at our app, now.
Let me guess, it does look fancy, is that a desktop app for creatives ?

`FLD`, nop, It's a add placement, it's not marketing, high frequency trading

 it's not big data, hadoop, machine learning, not even social,...
 
`RPE` Not going to help win followers on Twitter, or pick up girls at a local geeky bar or the local hackerspace. (don't laugh I've a girlfiends like that)

`FLD` True, it's a good old fashion enterprise app. Quite boring to chat about over a beer.

`RPE` unless we throw some docker in 

`FLD` we could, but I have better and trendier , heard about :



JHipster
---

`FLD` jHipster ?

`RPE` JHipster ??? WTF is this ? yet an other meta framework to Springboot a Scala container written in
JRUby (which in turn runs Groovy plugins ?)

`FLD` Almost :) - it's app generator - like jboss forge or appfuse

`RPE` ok, if you recall AppFuse you've been doing this/java for too long - time to change job or even retire.

Yo 
---
`FLD` on the contrary, if you re one of the cool kids, you surely know js + yeoman, based on it, fire with
yo jhiptser + choose


`FLD` end up with sleak stack, both lean and up to date, using springboot on the server side + angular on
client

`RPE` Cool, with that, we might get lucky.

`FLD or RPE ?` But you told them we were Java guys, right, let me tell you about the security features built on top of Java in there  ?

Spring Security
---

`FLD` what was appealing to me in this stack was the spring sec plumbering coming with it.
It brings solid foundation for ACL

`RPE` man in the middle attack

`FLD` Spring Secu supports HSTS - qui indique au client que seul https sera utilisé.

`RPE` and what clickjacking ?

`FLD` frameOptions().sameOrigin()

`RPE` and the infamous XSS attacks ?

`FLD` that too - along Cross site scripting forgery, il me fournit une solution  à base crsf Token,

`RPE` in short - a shit load of fancy acronyms to brag at parties

`FLD` yep, and let's not forget a skeleton for audit trails and security logging

`RPE` like the one you need to address the previously mentione R of STRIDE - repudiation threat.

pause


`Talklet 2` Intranet, FW & RP
====


Intranet
----

`FLD` That being said, I'm not that worried in the end, because my app is only internal, well hidden
within the confine of a compartimented VLAN, behind a bunch of firewalls.

`RPE` Yeeaaahhh, about that. Don't you think it's a bit naive of you ? I mean you do have user
connectiong to your app from their laptop?


`FLD` Yep, and also mobile+tablets

`RPE` of course they are... And from those, I'm guessing they also to the internet

I know where ur getting at - and to make it worse, some has even root privliges, plus not managed

`RPE` Arg, ur killing me ! My Red Hat heart is bleeding ! Bottom line is, internet is just a short
hop away...

`FLD` But I don't have to worry - I got firewalls !!!!

Firewall
---------

`RPE` And so ? What's your point here ?

Well, fw are securing stuff, aren't they ?

`RPE` No, they are not. FW blocks access to unused ports - but your app needs to be accessed, therefore
the port to it needs to be open, isn't it ?

`FLD` Yes

`RPE` FW mostly aims are helping networking traffic, reducing unneeded load on the system. Its usual usage
does not provide security to *your* app. It reduces DoS attacks, but does not protect apps itself.

`FLD` OK, but it does blocks some ports ?

`RPE` Yep, but if you ur running service that you don't need to access, you have other issues you need to
take care of...

`FLD` Ok, but what about open ports ? We can't close them so what do we do ?

`RPE` You look at how they are used. If you open a port send mails, it should only have SMTP, for
instance. Sidenote about this, I generally grade how ineffective a security is by the number of port
being uselessly closed.

`FLD` So if you can't get email using POP

`RPE` Bad

`FLD` IT blocks VPN

`RPE` Even more.

`FLD` No SSH inbound ?

`RPE` Worse and pointless, with a SSH outbound, you can connect to a remote server, and then piggy back
your way inside the IT. However, with all those ports being closed or blocked, you did provide a
very strong complete illusion of security

`FLD` While making everyday tasks in the company, a living hell. (in the sake of security => bad
usability).

`RPE` OK, so bottom line is the key to securing app is protocol and content filtering,

`FLD` Right, but can FW do that ?

`RPE` Yes, generally in some limited fashion, but the issue is that you rarely have the control
over'em,...

`FLD` Right, @Adobe, we don't have control over the FW, a dedicated team deals with that

`RPE` Yes, and even if they would like to do it right, they lack the in depth knowledge of your app to
do so.

`FLD` OK, so how do we do here ?


Reverse Proxy
---------

`RPE` You use reverse proxy for this. Nowdays, project often have the control on the HTTP load
balancer in front of their app...

`FLD` Well, sadly because we are still prototyping, we had no time to set up a load balancer in
front

`RPE` It's a shame, because you also have a reverse proxy, and use it to ensure your webapp is not being
attack using malicious content. Indeed, the reverse proxy can analyze any incoming requests...

`FLD` and so what ?

`RPE` well if the request does not match what the app expectation, it will just drop it. Let's take
a simple example. If you have a form with date field and are getting a 300 hundreds characters, it
is both invalid and most likely an attack...

`FLD` yes, you can also do header validation, add CSRF token,  throttling or even rate limiting

`RPE` And a shitload of very cryptic technical terms. You might get some girls out of that.

`FLD` Right, but can't my RP get hacked too ?

`RPE` In theory yes, but it's more difficult (explains hacks and then how RP are therefore "immune" to it)

`FLD` Yes, it just analyze and clean, does not replies nor interract with the attacker.

`FLD` ok so filter content, clean but also need to returns data

`Talket 4` Data and Encryption
=======

`slide-23` Classification
---

`FLD` Well, let's talk about data. Here, no business, no backend uber, no wire transfer - basically
no fund to get hacked to the dark web

`RPE` Always nice to have

`FLD` But a nice data mash up, typical "employee productivity tool", such as

* employee address, phonee number
* salaries, financial package
* current deals and opportunities

ping pong

* PII - bound by law to keep private - especially here in Germany
* super sensible - on top of being confidential of course
* internal and restriced

`FLD` OK, so we need to keep this secure

`RPE` Which means encrypting all data that go through the system, from one end to an other.

`slide-24` Chiffrer le front
-------

`FLD` ok, so first let's start by the front - no other way around it, I need to encrypt everything
and use SSLde bout en bout, commencons alors par le front, on prévoit évidemment de tout servir en https

`RPE` Right, SSL is secure , but doing it correctly requires a lot of work - it's an art in itself.
SSL c'est secure, mais faire ça correctement c'est tout un art.

`FLD` And requires constant monitoring and following updates thoroughly

`FLD`even the biggest companines must deals with crisis, certificates being compromised or
propagtation of unauthorized certificates (but still trusted by most browser)

`RPE` and don't forget that, with enough time and resources, any encryption can be broken.

`FLD` scan your https server to detect new weakness and obsolete packages

`RPE` ok, on the front, we're set and good. Let's look at the backend.

`slide-24` Chiffrer le back
-------

`RPE` First of all, don't tell me your MongoDB is like those 40 000 instances over the web that are
running with default configuration ?

`FLD` Yes, we have fixed that +  mongeez required admin on db, not an option

`RPE` Ok, right so now you have a proper authorization scheme on your instance. But, what about your
data going across the wire from your app to the DB ?

`FLD` encrypt (explain)

`RPE` PR ? It's been six month !!!


`slide-25` Chiffrage au repos ?
-------

`RPE` OK, so now we have secure the communication between ur app and the users, and between the app
and the db. But how do we store then there ?

`FLD` not sure what to do (explain options) => encrypt on db

`RPE` make admin life easier, but also strong impact on performance - encryption on app level
provided better granularity (ex: Ashley Madison)

`Talklet 5` Auth
==========

`slide-28` JHipster login page
-----------

`RPE` jhipster default, local db, bullshit for prod Ah je vois que par défaut, jhipster a sa propre base de donnees d'utilisateur, pas mal pour le dev, mais une cata pour la prod !

`FLD` prod, but also UX, yet an other password to ask for users

`slide-29` Votre mot de passe (xkcd)
--------

`FLD` Autres questions qui me viennent à l'esprit devant ce genre d'ecran :

Quelles seront les règles spécifiques à ce nouveau mot de passe ?
Va-t-il encore m'imposer des contraintes inèptes relatives à l'ulisation des caractères speciaux et
chiffres ?

respiration

`RPE` depuis que j'ai vu ce xkcd Je suis assez fan de ces pass phrase mais toute ma famille se plaint que le mot de passe du wifi à la campagne est trop long ! Pourtant "Romain a des plus jolie cheveux que ses soeurs", c'est pas compliqué à retenir, non ? :)

`FLD` "Romain a des plus jolie cheveux que ses soeurs" 46 caractères dans jhipster 46 characters ca passe mais de justesse...
La seule contrainte imposée sur ce mot de passe c'est qu'il doit faire entre 6 et 50 caractères.

extended dictionnary also used => known words

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

`RPE` you have 156 password but what the point ? I know one thing about you - your dog name !

(note: on respire, on laisse les gens rigoleur)

`FLD` et celui de Paris Hilton ?

`FLD` story

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

`slide-38` SAML Sequence Diagram
-------

`RPE` So SAML ? How does it work ?

`FLD` Le plus compliqué finalement, c'est la config.

* il faut recuperer le meta données de l'idp et fournir a ton moteur client saml
elle contienne un certificat et des url à associer à la redirection en vue d'un login ou tout au moins d'une verification  d'identité

`RPE`
* et toi tu fournis à l'idp, quelques metadonnées comme
  *  certificats et url associer à la redirection en vue d'un login et logout.

`FLD` exactement, regardons le flow

 tu ceux acceder a ma une resource protégé
mon fournisseur de service dit

* "Not authorized", je te connais pas, je te donne pas le service, je te donne pas la resource,
* va prouver ton identité au pres du fournisseur d'identité,
* il reviendra vers moi,
* si son retour est valide, je te donnerai accès à ma resource
* tout du moins si les infos d'idendité extraite dans l'enveloppe saml me permette de te donner le role necessaire pour etre autorise à acceder a ce service ou cette resource.

`slide-37` SAML & JHipster ?
-------
`RPE` But ur  JHipster thingy supports SAML ?

`FLD` no but Spring Security does

`FLD` a choisir je préfère tout de même l'annotation hell au xml hell....
Et Spring Security s'y prête plutot bien.

`RPE` a Quand ton pull request ?
oui c'est en projet, il y a deja un ticket le 695 qui lui associé.

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
Oui je l'ai active sur mon compte twitter, facebook, google, yahoo , github, paypal,

`RPE` en tant que developpeurs il est de votre responsabilité de protéger vos secrets, vous êtes la cible des hackers

`FLD` vous avez votre profil sur linked-in, et vous êtes devops ou security specialist chez BNP ou 1 ms valent 100 millions d'euros ?

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

`FLD` oui mais refresh token - can it be hacked ?

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

`FLD` Ah non g peur la

`RPE` Non, au contraire ! Le cloud te force à faire plus gaffe à ta sécurité, pour toutes les raisons qu'on vient d'évoquer, mais t'apportes bcp en termes de sécurité.

Y'a qu'on bien de système non maintenu, qui tourne depuis 10 ans, sans le moindre de security patch appliqué dans ton infra ? Voir sans admin !

`FLD` (gros sourire) ben aucun bien sûr ;) !

`FLD` Cattle vs Pet,

`RPE` Exactement ;) - dans le cloud tes machines sont constament reconstruit "fraîche" et patché. Un super exemple est Neflix.

Ils sont très connu par avoir une service irréprochable qui repose sur la solution de Cloud d'Amazon.

Si vous avez bossé sur Amazon, vous savez que bien d'excellente qualité, le service n'est pas à 100% fiable.

Une VM peut subitement "disparaitre", le réseau peut devenir temporairement inaccessible, et leur SLA prévoit même qu'une zone entière (par exemple l'Irlande) peut tomber pendant plusieurs minutes !

Bref, dans ces conditions, pour fournir un super service comme Netflix, il faut que les applications soient très robuste !

Et là, Netflix a été génial, ils ont forcé leur developeur à se préparer aux pannes et mettant en place un programme simulant ces pannes - le fameux Chaos Monkey.

Et le plus incroyable, c'est qu'ils sont tellement sûr de la résilience de leur applications qu'ils laissent Choas Monkey s'exécuter sur leur plateforme de production !!!

http://techblog.netflix.com/2012/07/chaos-monkey-released-into-wild.html

de choas monkey a hacky monckey


`Talklet 7` Firemen
===========



The House is on fire
----

`RPE` the goal is to give the system a fighting chance
        => firedoor / smoke detector

`FLD` ccm

`RPE` IDS pour reperer des intrusions

`FLD` HSM ben d'attaque offline

`RPE` Ben sinon, si un mec à trouver un exploit sur ton app, il peut accéder à ses données, mais aussi éventuellement, modifier son comportement.

meca qui bloque

co un RP !

Firefigthers
----


`FLD` en fait fo etre pret a etre hacke

`RPE` exactement ! Regarde github

`FLD` tell the story

`RPE` => pret a endurer une attaque

`FLD` pompier metaphore

`FLD` Ouais, mais dis moi, avec ça en place, ça évite que ton application crée des fichiers, ou exécute des programmes, mais si l'exploit se base sur une "activité" normale. Par exemple modifie le contenu d'un fichier de données légitime de l'application - tu peux gérer ça avec ton SM ou SE Linux ?

`RPE` Non, j'en doute, et de toute manière, ça ne serait pas vraiment une bonne pratique, de mettre ce genre de contrôle en place là dedans.

`FLD` Ben moi, j'ai une bonne technique pour ça, super simple pas comme "ta super science".

TODO: simple checksum on sensitive directory only

`RPE` Ah ouais, c'est pas mal en effet !  DevSec


`FLD` In short, what to remember is
* firemen train for fire
* fireman is not afraid of fire

https://www.techn0polis.net/wp-content/uploads/2015/01/security.png

`Talklet 8` Conclusion
==========

`RPE` OK, so time to wrap up - what did we talk about during all this time:

`FLD` security, it's you

`RPE` no ! it's you

`FLD` see the big picture, analyse risks, use threat modelling to see clearly where u stand

`RPE` don't ever think you are actually safe

`FLD` not even behind a compartiment VLAN, and a truckload of FW

`RPE` your data is not safe either

`FLD` so encrypt

`RPE` which means management secrets

`FLD` even at home (private sphere)

`RPE` used 2FA and kill your dog - boom Struppi !

`FLD` UX is not excuse for lack of security - and security is not an excuse for a bad UX

`RPE` Also don't forget that the battefield has extended to new territories

`FLD` such as continuous integration, delivery and cloud

`RPE` treat your servers like a cattle, not like a pet

`FLD` (Anyway the dog is already dead)

`RPE` finally, be *ready* to fight fire - because if you are successful

`FLD` ... you'll be hacked !
