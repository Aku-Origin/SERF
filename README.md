# SERF — Régence

> **Prenez le contrôle absolu de votre univers numérique.**

SERF est un système d'exploitation mobile souverain, français, conçu autour d'un
principe unique : **l'utilisateur n'est plus le produit ; il est le Régent.**

Là où Android et iOS font de vous un serf — locataire d'une machine que vous avez
payée, dont les règles sont écrites ailleurs — SERF vous rend la couronne : le
contrôle du matériel, le contrôle des données, et le contrôle des règles
elles-mêmes.

---

## Les trois renversements

| | Le renversement | Le mécanisme qui le porte |
|---|---|---|
| **Santé** | Payer la santé plutôt que la maladie | Vote par conviction ; priorité d'affectation à la prévention, à la maintenance et à l'accessibilité |
| **Souveraineté** | La souveraineté du peuple plutôt qu'une gouvernance de peu | Pondération quadratique : le nombre de personnes décide, pas les montants |
| **Liberté** | La liberté plutôt que la soumission | L'Enceinte : aucune application n'est interdite, toutes sont encerclées |

*Une valeur sans mécanisme n'est qu'une déclaration.* Chacune de ces trois lignes
est adossée à un dispositif écrit dans la [Charte](CHARTE.md) ou dans
l'[architecture](docs/02-ARCHITECTURE.md).

---

## Vous ne perdez aucune application

L'erreur qui a fait échouer toutes les alternatives précédentes : demander à
l'utilisateur de **renoncer**. Sa banque, son opérateur de transport, son
application professionnelle. Trois semaines plus tard, il est revenu sur Android
— et il a eu raison, on lui avait vendu une privation.

SERF **encapsule au lieu d'exclure**. Vos applications continuent de fonctionner,
dans une *Enceinte* qui contrôle intégralement ce qu'elles voient :

- Les services Google tournent **sans aucun privilège**, comme une application
  ordinaire soumise à vos permissions.
- Une application réclame vos contacts ? Elle reçoit **un carnet vide** — et
  fonctionne normalement. Un refus la ferait planter ; un vide ne lui apprend
  rien.
- Réseau coupé par application, espaces cloisonnés à chiffrement distinct,
  journal de tout ce que chaque application a tenté et vers qui.

Réserve honnête : cela ne contourne **pas** l'attestation matérielle forte. Les
applications bancaires et France Identité exigent un système certifié par Google
et refuseront. C'est un problème de régulation, pas d'ingénierie — voir
[architecture §6](docs/02-ARCHITECTURE.md).

---

## Ce que SERF est — et ce qu'il n'est pas

**SERF est** un fork AOSP durci, où les services Google sont **déprivilégiés**
plutôt que supprimés, surmonté d'une couche système de gouvernance collective.

**SERF n'est pas** un noyau écrit de zéro. Écrire un OS mobile complet — noyau,
pilotes, pile radio, pile graphique — est hors d'atteinte de toute structure
n'ayant pas les moyens d'un État ou d'un GAFAM, et se heurterait de toute façon
au mur des pilotes propriétaires SoC. Le chemin réaliste est le fork AOSP.
Voir [`docs/02-ARCHITECTURE.md`](docs/02-ARCHITECTURE.md).

**SERF ne tournera pas sur iPhone.** Apple ne permet aucun système alternatif :
le bootloader est verrouillé sans voie de déblocage. Sur iOS, le maximum
atteignable est une application compagnon — ce qui n'est pas un OS souverain.

**Les votes de SERF n'ont pas encore de portée juridique.** La finalité du projet
est la transmission et la gouvernance d'un pays par le peuple ; le chemin est la
**subsidiarité montante**. On gouverne d'abord **le commun SERF** lui-même — sa
feuille de route, son dépôt, sa trésorerie, sa charte — puis les structures qui
s'y adossent par convention. Chaque échelon se franchit après avoir été tenu au
précédent. C'est un pouvoir réel, exercé sur un objet réel, et c'est ainsi que se
construit une légitimité qui ne s'effondre pas au premier examen.

---

## La Régence — comment on décide

Deux corps, et un seul point de contact qui compte.

**Les Régents** — tous les porteurs de SERF admis au corps électoral. On y entre
par **parrainage** : trois Régents répondent de votre existence distincte. Le vote
est secret, séparé de l'admission par cryptographie et non par promesse.

**La Table Ronde** — **treize** personnes issues des Corps qui font vivre la
nation : Soigner, Nourrir, La Nature, Défendre, Transmettre, Bâtir, Produire,
Mouvoir, Relier, Juger, Créer, Accompagner. Six sièges élus, six tirés au sort, le
mode alternant à chaque renouvellement pour qu'aucun ne se professionnalise. Le
treizième est le **Siège Ouvert**, tiré au sort parmi tous les Régents, sans
condition de métier — une voix au moins qui ne doit rien à une carrière.

**Quatre expressions**, et non deux : **Oui**, **Non**, **À nuancer** — le
principe tient, pas ce texte-ci — et **Ignorer** : *je récuse la question
elle-même*. « Ignorer » n'est pas l'abstention, qui est le silence. C'est un acte,
il est compté, et il porte conséquence.

**Consultatif partout, contraignant sur la révocation.** Les Régents ne cogèrent
pas le quotidien — une assemblée qui tranche tout se paralyse. Ils détiennent le
seul pouvoir qui ne se contourne pas : **renvoyer ceux qui décident.** La Table
Ronde peut passer outre un avis ; elle ne peut pas le faire en silence. Et chaque
« Ignorer » majoritaire, chaque avis écarté sans réponse motivée, inscrit un point
de défiance. **Cinq points, et le scrutin de dissolution s'ouvre de plein droit.**

Détail complet : [`CHARTE.md`](CHARTE.md) et
[`docs/03-REGENCE.md`](docs/03-REGENCE.md).

---

## Documentation

| Document | Contenu |
|---|---|
| [`CHARTE.md`](CHARTE.md) | **Le texte fondateur** — droits intangibles, corps électoral, Table Ronde, fin de la Régence |
| [`docs/01-VISION.md`](docs/01-VISION.md) | Positionnement, récit, identité de marque |
| [`docs/02-ARCHITECTURE.md`](docs/02-ARCHITECTURE.md) | Socle technique, arbre de décision, périmètre matériel |
| [`docs/03-REGENCE.md`](docs/03-REGENCE.md) | La Table Ronde : gouvernance, scrutin, modèle de menace |
| [`docs/04-DESIGN.md`](docs/04-DESIGN.md) | Système de design : couleurs, typographie, principes |
| [`docs/05-PUBLICATION.md`](docs/05-PUBLICATION.md) | Miroirs, clés, continuité du projet |
| [`ROADMAP.md`](ROADMAP.md) | Jalons, du prototype à la première image flashable |
| [`JOURNAL.md`](JOURNAL.md) | Journal de bord — les décisions datées, avec leur pourquoi |

---

## État du projet

**Phase 0 — Fondations.** Aucun code n'est encore écrit. Les documents
fondateurs le sont : vision, architecture, gouvernance, design, et une
[Charte v0](CHARTE.md) soumise à délibération. C'est le préalable indispensable —
les décisions prises ici engagent des années de travail en aval.

Décidé à ce jour : fork AOSP sur base LineageOS · iOS hors périmètre · corps
électoral par parrainage et jeton signé en aveugle · l'Enceinte comme stratégie
d'adoption · le scrutin prouvé **avant** la ROM.

Reste ouvert : portée statutaire des votes, calibrage des seuils, financement,
licence. Voir [`ROADMAP.md`](ROADMAP.md).

---

## Licence

À déterminer. Contrainte structurante : AOSP est sous Apache 2.0, le noyau Linux
sous GPLv2. Toute distribution de SERF **doit** publier ses modifications du
noyau. Ce n'est pas une gêne — c'est cohérent avec la promesse de
vérifiabilité. Voir la discussion dans [`ROADMAP.md`](ROADMAP.md).
