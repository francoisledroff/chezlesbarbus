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
I implement distributed systems on top of Java, on top of infrastructure I implement using Chef. And I'm lucky to be surrended by a great team, among them hispters, hipsters who imlement great web and desktop UI using *vintage languages* such as js, css and html.

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

DeepDive
---

`RPE` Brilliant, we know where to start. let's take a look at our app, now.
Let me guess, it does look fancy, is that a desktop app for creatives ?

`FLD` let's Deep dive => it's a add placement, it's not marketing, high frequency trading
not big data, hadoop, machine learning, not even social,...
 
`RPE` Not going to help win followers on Twitter, or pick up girls at a local geeky bar or the local hackerspace. (don't laugh I've a girlfiends like that)

Our Use Case
---

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

`FLD` Well, fw are securing stuff, aren't they ?

`RPE` No, they are not. FW blocks access to unused ports - but your app needs to be accessed, therefore
the port to it needs to be open, isn't it ?

`FLD` Yes

`RPE` FW mostly aims are helping networking traffic, reducing unneeded load on the system. Its usual usage
does not provide security to *your* app. It reduces DoS attacks, but does not protect apps itself.

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

`RPE` http server + load balancing (control) => Indeed, the reverse proxy can analyze any incoming requests...

`FLD` and so what ?

`RPE`req match the app expectation,ex: form date (300 char) => drop

`FLD` yes, you can also do header validation, add CSRF token,  throttling or even rate limiting

`RPE` And a shitload of very cryptic technical terms. You might get some girls out of that.

`FLD` Right, but can't my RP get hacked too ?

`RPE` In theory yes, but it's more difficult (explains hacks and then how RP are therefore "immune" to it)

`FLD` Yes, it just analyze and clean, does not replies nor interract with the attacker.

Our Data
=====

`FLD` ok so filter content, clean but also need to returns data

Our Data Let's encrypt
---

`FLD` no business, no backend uber, no wire transfer - basically no fund to get hacked to the dark web

`RPE` Always nice to have

`FLD` But a nice data mash up, typical "employee productivity tool", such as

* employee address, phonee number
* salaries, financial package
* current deals and opportunities

ping pong

* PII - bound by law to keep private - especially here in Germany
* restricted - on top of being confidential of course
* confidential 

`FLD` OK, so we need to keep this secure

`RPE` Which means encrypting all data that go through the system, from one end to an other.

Encrypt the front-end
-------

`FLD` ok, so first let's start by the front - no other way around it, I need to encrypt everything
and use SSLde bout en bout, commencons alors par le front, on prévoit évidemment de tout servir en https

`RPE` Right, SSL is secure , but doing it correctly requires a lot of work - it's an art in itself.

`FLD` And requires constant monitoring and following updates thoroughly. even the biggest companines 
must deals with crisis, certificates being compromised or propagtation of unauthorized certificates 
(but still trusted by most browser)

`RPE` and don't forget that, with enough time and resources, any encryption can be broken.

`FLD` scan your https server to detect new weakness and obsolete packages

`RPE` ok, on the front, we're set and good. Let's look at the backend.

Encryp the backend
-------

`RPE` Recap => encrypt 

`FLD` encrypt (explain)


`RPE` MongoDB 40 000 

`FLD` yep, PR

`RPE` PR ? It's been six month !!!

Encrypt at rest
-------

`RPE` recap => storage

`FLD` not sure what to do (explain options) => encrypt on db

`RPE` make admin life easier, but also strong impact on performance - encryption on app level
provided better granularity (ex: Ashley Madison)

ashley madison
-------

`FLD` for password, hash use bcrypt, but remember sometimes it's not only the password you need to 
protect.  it's your *user identity*

`RPE` Right, hidding user id was more important here => but talking about user identity, how did 
you handle that in ur app ? 

JHipster login page
-----------

`FLD`  jhipster default, local db

`RPE`, bullshit for prod 

`FLD` prod, but also UX

`RPE` yet an other password to ask for users => 

Good Password (xkcd)
--------

`FLD` what comes to mind with this kind of screen (password constraint)

respiration

`RPE` since I saw this XKCD, I've become a big fan of those sort of password. That being said, my all 
familly has strangely been relunctant about it

`FLD` why so ?

`RPE` Apparently my sisters have issue with the passphrase I used: "Roman has the best hair of the 
familly". It's not too complicated to remember however...

`FLD` "46 char (in french) , does it but barely, 'cause : 6 to 50 char only ! However, filled with common words

`RPE` and so ?

chtulu
--------

`FLD` extended dictionnary also used => known words - even as bizarre are those !

One (incorrect) password
--------

`RPE` that being said, I can use (as a password) "incorrect"

`FLD` Right, and u used that everywhere ?

`RPE` you don't ?

`FLD` no, i don't ;-) I have 156

156 passwords
--------

`FLD` tamagoshi joke

One dog
------

`RPE` you have 156 password but what the point ? I know one thing about you - your dog name !

(pause)

`FLD` and Paris Hilton ? (story)

`RPE` secret question not already answered (ie available on social network)

Secrets (tweets)
------

`FLD` and look at those crazy number.... (pause) + *like in real life, ears everywhere*

`RPE` Everywhere. (Wir sind über all whether ur Stasi / NSA)

2FA 100%
------

`RPE` Right so like I always say to my friend getting married - why ? Do you want to 
get a divorce ? No mariage, no divorce ;) - same thing here, no password, no issue ;) 

`FLD` OK, we agree here : password are unavoidable and just *not enough* to prove id,
you need more than that.

(pause)

`FLD` use 2FA where password is not enough, it is just one step (question 2FA ?)

wired
----

`FLD` do u know this guy ?

`RPE` no since then I've enable 2FA everywhere I Can

`FLD` (wired story)

`RPE` dev as targets for hacker 

`FLD` don't brag too much, or you expose urself => or if u want to brag like us

`RPE` use to 2FA for f**k sake !


2FA
----

`FLD` where can I use 2FA ? (pick tools according to 2FA suppports)

`RPE` so first forget docker :)  (well, at least when u looked into it 6 month ago)

`FLD` chose github over bitbucket

`RPE` if you are a real kamikaze or just don't care, go crazy use those financial micro payments solutions.

`FLD` IoT + health also don't give a crap

`RPE` oddly enough, the best ones here are social security (secure cat)

`FLD` social knows UX, had to find a good compromise between it and security => good job

`RPE` i can see u coming here... you did it for you app, didn't you ? ;) 

`FLD` Adobe employe (spoil kids))are demanding in UX

Our Solution
----

`RPE` => ok, to sum the last 5 slides, how are to handle all of that in ur app ?

`FLD` Our goal : only service provided, integrate trusted and trustworthy idp

`RPE` : has a solution, we have plenty if not :)

`FLD` Yes, we have 2 :) => pick one that supports SAML (standard)

SAML
-------

`RPE` So SAML ? How does it work ?

`FLD` std + SSO browser, go try it

SAML Sequence Diagram
------
 
`RPE` Is it difficult ?

`FLD` complex config + metadata (idp), providing ur own to SAML server (cert+redirect URL)

`RPE` And how does it works ?

`FLD` first u connect => not auth

`RPE` redirect to IdP i guess

`FLD` prove id 

`RPE` right, so password + token 

`FLD` once proven, come back to app with SAML enveloppe with id

`RPE` based on the metadata of the id, you can assess if I have access (or not) to resource

`FLD` right, fine grained 

SAML & JHipster ?
-------

`RPE` Brings us to:  JHipster thingy supports SAML ?

`FLD` no but Spring Security does

`FLD` fantastic demo  !

`RPE` with slides :)

`RPE` click + wtf

`FLD` before the click: the network login 

(okta demo)

`RPE` => still shitty everyday 
 
`FLD` => fair compromise, hard to find

`RPE` so how did u do it ?

`FLD` SAML + OAUTH => tokens

`RPE` no relogging

`FLD` no hack on refresh

`RPE` but what happens if got stolen ?

`FLD` revokable

slide option
----

`RPE` cool but other options ?

`FLD` yes, blah + harden OAuth wuth signed request (JWT token) 
=> Treat Model for OAuth, ping mine => identify CI server is a risk

CI & Cloud
=========

`RPE` Right, nowadays CI holds secrets than can be used to hack app 
=> needs to be secure too => battlefield has extended to encompass
all chains

slide github secret
--------

`FLD` code holds secrets ?

slide rail tweet
-----

slide secret management is not easy
----

slide chef-vault intro => jenkins 

slide nexus
----

`FLD` proxy all you get, checksum, 

`RPE` model pushed by RH with Satelite

`FLD` right, but nexus too

cloud
----

`RPE` Ready now, so cloud like all the cool kids ?

cloud is someone else computer
----

`FLD` too afraid

`RPE` don't be, cloud forces u to be more secure, system always rebuild

`FLD` better than 10y old sys with no patches

`RPE` however handling so many sys hards...

Cattle vs pet
------

`FLD` => Cattle vs Pet + crazy number

Crazy number
----

NetFlix
-----

`RPE` netflix story

ready to be hacked?
===========

The House is on fire
----
Firefigthers
----

`FLD` github story

`RPE` side note on transparency

`FLD` train for fire 

Conclusion
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
