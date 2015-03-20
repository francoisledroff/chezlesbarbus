`Talklet 3` Threat Model
--------

`FLD` ce qui compte c'est du comprendre les menaces qui pèsent sur notre système.

Microsoft
https://www.owasp.org/index.php/Threat_Risk_Modeling


`FLD` pas le temps ici pour faire un cours sur les concepts de STRIDE et DREAD, voici juste un slide

STRIDE is a classification scheme for characterizing known threats according to the kinds of exploit that are used (or motivation of the attacker).

* Spoofing Identity : ensure a single execution context at the application and database level.
* Tampering with Data : data validation
* Repudiation: audit trails at each tier
* Information Disclosure: persist/cache as little info as possible
* Denial of Service, do not allow anonymous, or do as little as possible for anonymous
* Elevation of Privilege : proper ACL in place

DREAD is a classification scheme for quantifying, comparing and prioritizing the amount of risk presented by each evaluated threat.

* Damage Potential
* Reproducibility
* Exploitability
* Affected Users
* Discoverability
