# Outil de prise de RdV auprès d'un gendarme

> Programme EIG2018 
> Défi : Brigade Numérique
> Décembre 2018
> Par Jean-Baptiste Le Dévéhat

> Possibilité de reprendre ce [caneva pour synthétiser/cadrer son projet](https://pad.etalab.studio/s/Ska9D-Q9N#)
> * Opportunité projet
> * Expression des besoins
>    * Cas d'utilisation
>    * Maquettes / Prototype
> * *Spécifications métiers (optionnelles)*
> 

> [**Evolution du document de cadrage pour les décideurs**](https://pad.numerique-en-commun.fr/s/B1ikrpahQ#)

## Opportunité du projet

### Contexte

Le projet de développement d'un outil de prise de rendez-vous a été lancé fin 2017 par la Mission Numérique de la Gendarmerie Nationale et appuyé par deux entrepreneurs du programme [Entrepreneur.e d’Intérêt Général](https://entrepreneur-interet-general.etalab.gouv.fr/defis/2018/brigadenumerique.html) porté par Etalab.

### Objectif

Proposer au citoyen une application de prise de rendez-vous en ligne avec un gendarme, liée à l’outil de planification de l’activité de la gendarmerie.

### Périmètre de l'étude

Face à la multiplication des services en ligne de prise de rendez-vous pour les citoyens, la gendarmerie nationale souhaite s'équiper de ce service de contact numérique. 

Ce projet s'inscrit également dans la nouvelle doctrine d'emploi de [Police de sécurité du quotidien](https://fr.wikipedia.org/wiki/Police_de_s%C3%A9curit%C3%A9_du_quotidien).

### Analyse des besoins

Pour les gendarmes, il faut que le service aide la planification des missions sans ajouter de contrainte. Le commandement de la brigade doit pouvoir planifier des heures de rendez-vous et pouvoir annuler ces rendez-vous (pris ou non). Le choix a donc été fait de proposer des rendez-vous sur deux semaines à partir du surlendemain.

Pour les citoyens, il faut un service qu’on découvre rapidement, facile à utiliser, qui donne plus d’autonomie dans la gestion de son emploi du temps. 

De part et d’autre, il faut bâtir une relation de confiance : garantir le sérieux d’une demande de rendez-vous, garantir la fiabilité du service.

### Scénario d'implémentation

Au commencement du projet, plusieurs scénarii ont été proposés. Finalement, il a été jugé intéressant de déployé cet outil au sein du site internet [service-public.fr](https://www.service-public.fr) pour le potentiel et l'affordance déjà acquis par l'internaute dans l'usage de ce site web. Potentiellement, cet outil pourra être réutilisé par d'autres administrations (pré-requis avoir un back-office interopérable - avec API). 

Il sera donc nécessaire d’inter-opérer la gestion/administration des rendez-vous à travers l'outil de planification de la gendarmerie avec le site web [service-public.fr](https://www.service-public.fr).

### Contraintes & exigences

* La mission des deux EIG se termine mi-novembre 2018.
* L'outil doit permettre de réorienter l'utilisateur vers un service en ligne existant ou vers les informations nécessaires répondant à son besoin de rendez-vous.
* Il est nécessaire d’expérimenter un tel outil plusieurs mois sur un périmètre resteint afin de recueillir les ajustements des utilisateurs (gendarmes et citoyens)

### Calendrier projet

* Développer l'API / interface de programmation et de gestion des rendez-vous (gestion interne à la gendarmerie) : 
    * Environnement Dev : Fait
    * En prod < 15/01/2018
* Définir les cas d'utilisation pour prendre rendez-vous ou être réorienté vers les (télé-)services en ligne adéquats. : Fait
* Maquetter/prototyper les cas d'utilisation : En cours
    * Validation des maquettes : Fait
    * Validation du débruitage (par la DOE/DPJ et la DILA) : Fait
    * Validation du process de prise de RdV (par la DOE/DPJ et la DILA) : Fait
    * Validation du prototype 
        * Quelques modifications à faire suite à réunion DOE/DPJ : Fait
        * Présentation à la DIAM (le 23/11 à la DILA) : Valider 
        * Validation des textes pour chaque cas (production 06/12 avec DOE/DPJ) : Fait (voir chapitre [Spécifications](https://pad.etalab.studio/s/Bk7Vz-Q94#Sp%C3%A9cifications-m%C3%A9tiers-d%C3%A9taill%C3%A9es))
* Développer l'interface de prise de rendez-vous par le citoyen
    * Attente DILA pour planning (estimations de 4 cycles de 2 semaines)
* Lancer en production et communiquer sur cette expérimentation
* Expérimenter cette expérimentation sur 2 départements français
* Lancer en production à l'échelle nationale et communiquer sur ce nouveau service


----

## Expression des besoins

### Profils utilisateurs

Les (profils) utilisateurs sont donc les suivants : 
* Le commandant de brigade
* Le gendarme
* Le citoyen

### Cas d'utilisation

#### Gestion/administration du rendez-vous

* Le commandant de brigade planifie des plages de rendez-vous dans son outil de planification.
* Le commandant de brigade peut supprimer des plages de rendez-vous.
* La plage de rendez-vous peut-être de plusieurs heures, par exemple de 8h à 12h.
* Une plage de rendez-vous est uniquement en heure pleine afin d'être découpée en créneau d'une heure.
* Un créneau peut être :
    * planifié
    * réservé par un citoyen
    * terminé
    * annulé par le citoyen
    * annulé par le commandant 
* La création de plage de rendez-vous créé des créneaux planifiés
* Le citoyen reserve un créneau
* Le commandant de brigade valide un creneau réservé par un citoyen
* Le commandant de brigade peut annuler un creneau réservé par un citoyen, il est annulé par le commandant 
* Le citoyen peut annuler son rendez-vous (créneau reservé), il est annulé par le citoyen
* Une fois le rendez-vous passé (temporellement) il est terminé

#### Annuaire Service Public

Le point d'entrée sera l'[annuaire service-public.fr](https://lannuaire.service-public.fr/) et la fiche du lieu, de la gendarmerie, où le rendez-vous sera pris.

#### Débruitage

Comme décrit dans les [contraintes et exigences de l'opportunité projet](https://pad.etalab.studio/s/Bk7Vz-Q94#Contraintes-amp-exigences), tous les motifs et besoins du citoyen ne nécéssitent pas un rendez-vous. Il est donc nécéssaire de ré-orienter le citoyen vers un service en ligne ou vers les informations présentes sur internet selon son besoin.

Pour définir le besoin du citoyen nous avons construit l'arbre décisionnel, aussi nommé débruitage, suivant :

----

![Débruitage pour prendre un rendez-vous](https://pad.numerique-en-commun.fr/uploads/upload_95eaca80ec932540eda59a806a3f642e.png)


----


### Maquettes & Prototypes

Par exemple, sur la [fiche de la Gendarmerie de Lizy-sur-Ourcq](https://lannuaire.service-public.fr/ile-de-france/seine-et-marne/gendarmerie-77257-01), nous pourrions avoir sous l'adresse postale un bloc nommé "Besoin de nous contacter ?", comme ci-dessous  : 

----
![](https://pad.numerique-en-commun.fr/uploads/upload_ad1cd1ff60a99710efceb11eba605ef0.png)

----
#### Prototype en ligne

Le prototype est actuelement accessible au lien suivant : [Prototype (en construction) de l'outil de prise de rendez-vous sur l'annuaire service-public.fr](https://launchpad.animaapp.com/UseCase01/rdv0)

Sur ce prototype, nous avons décrit les 3 cas d'utilisation suivants :

#### Prendre un rendez-vous

Exemple de cas d'usage :
![](https://pad.numerique-en-commun.fr/uploads/upload_0f69c0a825036f14f93c65a29ed5c29a.png)

<div style="padding:59% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/302275556?title=0&byline=0&portrait=0" style="position:absolute;top:0;left:0;width:100%;height:100%;" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div>

#### Être réorienté vers un appel au 17 (cas d'urgence)

Exemple de cas d'usage :
![](https://pad.numerique-en-commun.fr/uploads/upload_00d58e04a93d3e3e6b96db9bc0a9349a.png)


<div style="padding:62.5% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/302275586?title=0&byline=0&portrait=0" style="position:absolute;top:0;left:0;width:100%;height:100%;" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div>

#### Être réorienté vers un service en ligne

Exemple de cas d'usage :
![](https://pad.numerique-en-commun.fr/uploads/upload_0b719bc4893d4dc174d5929ccc287804.png)

<div style="padding:58.16% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/302276558?title=0&byline=0&portrait=0" style="position:absolute;top:0;left:0;width:100%;height:100%;" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div>


----

## Spécifications métiers (détaillées) 
> non-exaustif car agile... 
> WIP
> bloc note/mémoire pour prochaines réunions

### Prise de RDV : OTV
Cas concerné pour ce texte : OTV (particulier) 1ère fois et renouvellement + OTV (pro) 1ère fois et renouvellement.
 
> **Votre demande de prise de rendez-vous a été réalisée avec succès, et vous sera confirmée dans les meilleurs délais.**
> 
> Pièces à présenter lors de votre rendez-vous : 
> 	• 	Une pièce d’identité (carte nationale d'identité, passeport...)
> 	• 	Le formulaire d'inscription complété
> 	 	 	
>(bouton) 	ACCEDER AU FORMULAIRE D'INSCRIPTION

### Prise de RDV : Autres demandes > Signaler une radicalisation

> **Votre demande de prise de rendez-vous a été réalisée avec succès, et vous sera confirmée dans les meilleurs délais.**
> 
> Pièces à présenter lors de votre rendez-vous : 
> 	• 	Une pièce d’identité (carte nationale d'identité, passeport...)
> 	• 	L'ensemble des élements qui vous laisse à penser qu'un individu est, ou en cours de radicalisation 
> 	
> *(bouton)* [EN SAVOIR PLUS SUR STOP-DJIHADISME.GOUV.FR](http://www.stop-djihadisme.gouv.fr/)
 
### Prise de RDV :  Autres demandes > Abandonner une arme à l'Etat

> **Votre demande de prise de rendez-vous a été réalisée avec succès, et vous sera confirmée dans les meilleurs délais.**
> 
> Pièces à présenter lors de votre rendez-vous : 
> 	• 	Une pièce d’identité (carte nationale d'identité, passeport...)
> 	• 	Votre arme sécurisée et démontée
> 	• 	Tous documents relatifs à votre arme
	
### Autres cas de réorientation vers un siteweb
#### Autres demandes > Dépot de candidature

> (bouton) ACCEDER AU SERVICES DE RECRUTEMENT EN LIGNE

#### Autres demandes > Lien vers procuration

> (bouton) ACCEDER AU FORMULAIRE DE PROCURATION

#### Autres demandes > Info acte cyber

> (bouton) ACCEDER AU SITE D'INFORMATIONS CYBERMALVEILLANCE
 
#### Autres demandes > Conseil de sécurité

> (bouton)ACCEDER AUX CONSEILS DE SECURITE
 
#### Autres demandes > BNUM
 
> *(bouton)* [ECHANGER AVEC UN GENDARME EN LIGNE](https://www.gendarmerie.interieur.gouv.fr/Brigade-numerique)
 

# Amélioration du cas d'utilisation d'un rendez-vous avec réorientation vers PPEL

## Design Review

### Cas d'utilisation actuel

<div style="padding:58.16% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/303071626?title=0&byline=0&portrait=0" style="position:absolute;top:0;left:0;width:100%;height:100%;" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div>

### Amélioriation du cas d'utilisation 

Etant actuellement sur un fiche de Gendarmerie (Annuaire Service Public), il est incohérent et inenvisageable pour le citoyen de devoir refaire une recherche d'unité de Gendarmerie dans PPEL. Il est donc nécéssaire d'être réorienter directement vers la fiche de renseignement (voir cas d'utilisation et prototype)

![](https://pad.numerique-en-commun.fr/uploads/upload_6d2386fb756f86c65b2a9030246908d7.jpg)

<div style="padding:58.16% 0 0 0;position:relative;"><iframe src="https://player.vimeo.com/video/303071584?title=0&byline=0&portrait=0" style="position:absolute;top:0;left:0;width:100%;height:100%;" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe></div>

## Besoin technique 

Il faut donc pour chaque fiche de gendarmerie (Annuaire Service Public) obtenir une correspondance avec l'unité gendarmerie pour le choix du lieu de la PPEL, afin de ne pas réitérer la recherche préalable du lieu (voir ci-dessus).


> fin document

