`Talklet 8` Conclusion
==========





`RPE` Bon, du coup, là tout le monde à soif et après, c'est la bière, donc, si on essayé un peu de résumé tout ça.

`FLD` Yes, mais on a quand même un paquet de chose. Enfin, voilà une liste, pour faire l'inventaire. 

`RPE` C'est ton coté Mésopotamien.

`FLD` Exactement. Bref:

* sandboxing reduces vulnerabilities
* better application server
* keep your secret safe
* use vault + configuration
* analytics on password request
* you leave an audit trail
* avoiding downtime when password/key change

`RPE`

* exploit don't last long - so the plan is to "hold" (availability, ensure your systems can "last long enough" during an attack)

`FLD`

**The three goals of security are confidentiality, integrity and availability**. Intranet security must deliver integrity and availability. Intranets exist to make information available to colleagues. Nevertheless, confidentiality is an issue. Each job function and person holding that job is given a level of access appropriate to his or her role. Intranets are often less secure than information technology professionals and managers realize

http://www.arnoldit.com/articles/10intranetSecAug2002.htm

@FLD, j'ai laissé, mais honnetement, j'aime pas trop tout le début ci dessus, je sauterais bien directement à ci dessous:

`FLD` En fait, au bout du compte, on vient de voir que la sécurité, c'est pas un truc adhoc, isolé, que tu peux implémenter à la fin, après un audit, mais plutôt un "combat de tout les instants".

`RPE` Yes, exactement. La sécurité c'est comme les bogues ou les fonctionnalités, il faut y travailler en harmonie avec le développement de l'applicatif, au fil de l'eau. En fait, on pourrait résumer ce qu'on vient de dire par un truc comme "DevSec". De la même manière, qu'avec Puppet...

`FLD` ou Chef !

`RPE` Oui ! Ou Chef ! Bref, de la même manière qu'avec DevOps, on n'a rapprocher l'infrastructure du développement, la sécurité s'est aussi rapprocher du dev. Le temps où les dévs pouvaient dire "la sécurité, je m'en fous, c'est le truc du barbu au fond du couloir", tout aussi révolu que celle où les dits "barbus" pouvaient limiter leur travail à la mise en place de FW, en se moquant (et se lavant mêmes les mains) des applis Java déployé sur leur système.

`FLD` Oauis, clairement, le gros des faiblesses de sécurité sont aujourd'hui dans les apps plus que l'infrastructure, pour sécuriser un
système, les deux profils doivent s'assurer coté à coté et (par exemple) rédiger ensemble les polices de sécurité du SecurityManager et les règles de filtrages applicatives.

`RPE`Exactement.

`FLD` Et déployer tout ça avec Chef.

`RPE` Ou Puppet.

`FLD` Ou Puppet.


