`Talklet 8` Conclusion
==========

`FLD` bon, au final, quand on penses à tout ce qu'on a raconté, ça semble presque mission impossible de sécuriser un système, non ?

`RPE` ben, comme disait l'autre, le seul système vraiment "secure", c'est le système éteint et enfermé à clé. En fait, la vrai question, n'est pas vraiment de savoir si un système est sécurisé, il ne l'est jamais. 

`FLD` Mais alors, à quoi sert tout ce qu'on met en place ?

`RPE` (référence au slide) ben le truc c'est plutôt de te laisser une chance de survivre à l'attaque. Pour prendre l'exemple des pompiers, si ton immeuble, il a des portes coupes feux, des détecteurs de fumées, des extincteurs à chaque étage, il a beaucoup plus de chance de survivre - et même de se tirer indemne, d'un incendie. 

Slide:

it will fail, stability is a myth
* firemen train for fire
* fireman is not afraid of fire

https://www.techn0polis.net/wp-content/uploads/2015/01/security.png

`FLD` Ouais, c'est d'autant plus vrai que aujourd'hui, faire un "exploit" n'est plus quelque chose de réserver à une élite de hackers. Avec les sites recensant les exploits, comme du temps des "script kiddies", n'importe qui peut tenter une attaque sur un système. 

### exploit ? not that big of a deal nowadays

* sandboxing reduces vulnerabilities
* better application server
* keep your secret safe
* use vault + configuration
* analytics on password request
* you leave an audit trail
* avoiding downtime when password/key change

* exploit don't last long - so the plan is to "hold" (availability, ensure your systems can "last long enough" during an attack)



**The three goals of security are confidentiality, integrity and availability**. Intranet security must deliver integrity and availability. Intranets exist to make information available to colleagues. Nevertheless, confidentiality is an issue. Each job function and person holding that job is given a level of access appropriate to his or her role. Intranets are often less secure than information technology professionals and managers realize



http://www.arnoldit.com/articles/10intranetSecAug2002.htm


On pourrait finir en disant qu'après DevOps, il faudrait un DevSec - utilisant le même approche,
impliquant les gens de la sécurité et les dévs. Ne plus laisser les dévs ignorer la sécurité, mais
ne plus laisser les experts sécu considéré les apps comme des "boites noires". Le gros des
faiblesses de sécurité sont aujourd'hui dans les apps plus que l'infrastructure, pour sécuriser un
système, les deux profils doivent s'assurer coté à coté et (par exemple) rédiger ensemble les
polices de sécurité du SecurityManager et les règles de filtrages applicatives.
