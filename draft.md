
#Master Chef & Puppet Show
-----
---------



# Quoi?
# Comment?
## Quelque études de cas
# Pourquoi?


------
presenter's notes:

---


Chef et puppet sont deux solutions concurrentes de gestion de configuration
Nous allons rapidement lever le voile sur la nature de ces solutions



Avant de passer à l'exploration rapide de quelque cas concrets 
mettant en oeuvre la configuration de back-end java


Et enfin nous conlurons par ce qui devrait alors vous paraite evident. Pourquoi Chef ? Pourquoi Puppet ?  Pourquoi cet engouement pour coder nos infrastructure ? 

----
-----

## Quoi?

---
---

## Quoi?
### - Infrastructure 

**Infrastructure** [in-fruh-struhk-cher]
nom féminin

.red[[1]] une collection de
* ressources:
 * réseaux, noeuds 
 * systèmes de fichiers, fichiers, répertoires, liens symboliques, montages disques
 * utilisateurs, groupes
 * packages, logiciels, services
 * configuration
 
* agissant de concert

* pour fournir un service


[1] [Introduction to Chef](http://www.slideshare.net/JulianDunn/chef-introduction-princeton-meetup)

------
presenter's notes:

----

notes à déplacer:

Donc forcemment toujours sujet au changement...
on commence par un app server, une db
on ajoute un load balancer devant les app serveurs
puis on veut aussi du HA sur la base, puis sur les LBs
on scale, on passe a 2 load balancers
puis on rajoute du cache distribué
puis on doit maintenir ca par env,
monter des data centers par geographie


---
---

## Quoi?
### - Infrastructure 
### - Infrastructure as code  


Chef & Puppet sont 2 solutions concurrentes 
* de gestion de configuration
* d' * **Infrastructure as Code** *

Il ne remplacent pas juste tes scripts shell, il te permettent de:

* abstraire la facon dont tu manages ton infra
* de la coder 
 * de la (re)construire à partir de serveurs 'nus'
* faire converger tes systèmes 
* de façon idempotente 
```   
    EtatA --> Etat B --> Etat B
```
]

------
presenter's notes:

----


http://www.slideshare.net/jedi4ever/infrastructure-as-code-abug-session
http://architects.dzone.com/articles/infrastructure-code
https://www.youtube.com/watch?v=cuJZbRngWC0



---

## Quoi?
### - Infrastructure 
### - Infrastructure as code
### - Puppet


Puppet:

- créé en 2005
- édité par PuppetLabs
- license TBD
- langage dédié (DSL) 
- blablabla TBD


---

## Quoi?
### - Infrastructure 
### - Infrastructure as code
### - Puppet
### - Chef


Chef:

- créé en 2009
- édité par Opscode/Chef
- license Apache
- écrit en Ruby
- langage dédié (DSL) et pure Ruby
- different modes
 * Chef solo 
 * Chef zero 
 * Chef server + client



------
presenter's notes:

----

https://www.ibm.com/developerworks/library/a-devops2/

Chef has been around since 2009. It was influenced by Puppet and CFEngine. 
Chef supports multiple platforms including Ubuntu, Debian, RHEL/CentOS, Fedora, Mac OS X, Windows 7, and Windows Server. 
It is often described as easier to use — particularly for Ruby developers, 
because everything in Chef is defined as a Ruby script and follows a model that developers are used to working in. 
Chef has a passionate user base, and the Chef community is rapidly growing while developing cookbooks for others to use.

chef-solo: http://docs.opscode.com/chef_solo.html
chef-solo is an open source version of the chef-client that allows using cookbooks with nodes without requiring access to a server. chef-solo runs locally and requires that a cookbook (and any of its dependencies) be on the same physical disk as the node. chef-solo is a limited-functionality version of the chef-client and does not support the following:

Node data storage
Search indexes
Centralized distribution of cookbooks
A centralized API that interacts with and integrates infrastructure components
Authentication or authorization
Persistent attributes

chef-zero : http://www.slideshare.net/mpgoetz/chefzero-local-mode

---
---


## Quoi?
### - Infrastructure 
### - Infrastructure as code
### - Puppet
### - Chef


Chef

* réduit la complexité de la gestion d'une infrastructure par l'abstraction
 * *Organizations, Environments, Roles, Nodes, Run-List, Cookbooks, Recipes, Resource, Data Bags, Search*
 
* permet de persister et manager ces abstractions sous forme de code

* génère les configurations et provoque les installations directement sur les serveurs/ *Nodes* à partir des leur *Run-Lists* 
 

---
---



# Comment
### Comprende Chef 
### -  Panorama


![overview](img/overview_chef.png)

------
presenter's notes:

----


http://docs.opscode.com/chef_overview.html
http://www.slideshare.net/opscode/week-1-overview-of-chef

---
---

## Chef Comment ?
### -  Panorama
### -  Abstractions



* Organisations
 * locataires independants du chef serveur (BU, Département)
 
* Environments
 * modèle votre cycle de release et vos process (dev, test, stage, prod)  
 
* Roles 
 * représente votre type de serveur (lb, JEE serveur, DB Serveur...)
 
* Nodes
 * vos serveurs (physique ou virtuel, sur votre réseau our sur le cloud)
 * sur lequel tourne `chef-client`


------
presenter's notes:

----


manager le complexité, et embrasser les abstraction offertes par Chef


Organization : 

Completely independent tenants of Enterprise Chef
*  Share nothing with other organizations
*  May represent different
*  Companies
*  Business Units
*  Departments

Environments may include data attributes necessary
for configuring your infrastructure
*  The URL of your payment service’s API
*  The location of your package repository
*  The version of the Chef configuration files that
should be used


Roles may include a list of Chef configuration files
that should be applied.
*  We call this list a Run List
*  Roles may include data attributes necessary for
configuring your infrastructure
*  The port that the application server listens on
*  A list of applications that should be deployed

Nodes Adhere to Policy
• An application, the chef-client, runs on each node
• chef-client will
• gather current system configuration
• download the desired system configuration from
the Chef server
• configure the node such that it adheres to the
policy

http://www.slideshare.net/opscode/week-1-overview-of-chef

http://docs.opscode.com/chef_overview.html


---
---

## je n'ai qu'un simple jar
un micro service/site web
c'est auto suffisant

oui mais:
* installation en service
* monitoring de log
* HA 
* apache dispatcher for static content
* security checklist
* elasticité

multiplié par le nombre d'env 


---
---
## je veux protéger mes secrets 

* chef-vault

---
---
## l'enfer des dépendances

* berkshelf

---
---


## Pourquoi?


---
---

## Pourquoi?
### - Transformation d'Adobe IT


- Adobe **Creative Cloud**
 * *'Accelerate, Simplify, Scale'*
 
- décloisonner les équipes, dev, de qualité, de sécurité et d'exploitation
 
- Comme notre infra devient code, elle devient 
 * testable
 * versionable 
 * jetable 
 * repétable, *'cloud-ready'*
 

------
presenter's notes:

----



- Adobe IT
 * *Accelerate, Simplify, Scale*
 
- décloisonner les équipes, dev, de qualité et d'exploitation
 * faciliter, accélérer les changements 
 * mieux garantir stabilité et sécurité 
 * éviter les surprises
 
- Comme votre infra devient code, elle devient 
 * testable
 * versionable 
 * jetable 
 * repétable

* http://sdarchitect.wordpress.com/2012/12/13/infrastructure-as-code/
* http://java.dzone.com/articles/infrastructure-code-key-devops
* http://architects.dzone.com/articles/infrastructure-code


---
---

## Pourquoi?
### - Transformation d'Adobe IT
### - Open Development


[@bdelacretaz](http://www.slideshare.net/bdelacretaz/open-development-in-the-enterprise-apachecon-na-2013) nous donnes 5 clefs:

 * Whatever you're working on, it must be backed by an issue in the tracker.

 * **If it's not in the source code control system, it doesn't exist.**

 * If it's important, it needs a permanent URL.

* If it didn't happen on the dev list, it didn't happen.

* What happened while you were away? Check the activity stream and archives.
]


------
presenter's notes:

----

Who needs secrets?
Who cares if your code is not yet perfect?

* http://www.slideshare.net/bdelacretaz/open-development-in-the-enterprise-apachecon-na-2013

without trust, the tools don't matter

* http://www.slideshare.net/JulianDunn/chef-introduction-princeton-meetup

---
---

## Pourquoi?  



* TBD



---
---