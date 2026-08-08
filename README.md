# SERF — Régence

> **Un système d'exploitation mobile où les porteurs détiennent les règles.**

Là où Android et iOS font de vous un serf — locataire d'une machine que vous avez
payée, dont les règles sont écrites ailleurs — SERF vise l'inverse : le contrôle du
matériel, le contrôle des données, et **le contrôle des règles elles-mêmes**, par
un scrutin vérifiable et un registre que personne ne peut réécrire.

> ### Rien n'est adopté. Rien n'est en production. Aucune ligne de code n'existe.
>
> Ce dépôt contient un corpus de conception, une Charte soumise à délibération, et
> un **registre public de ses propres défauts**. Il est publié pour être attaqué.
>
> **[→ Catalogue des travaux](site/index.html)** — la présentation complète du
> projet en une page : ce qu'il est, ce que nous refusons de promettre, ce qui est
> cassé, et où en est chaque document. Téléchargez le fichier et ouvrez-le dans un
> navigateur ; il ne fait aucune requête réseau.

---

## Les cinq renversements

| | Le renversement | Le mécanisme qui le porte |
|---|---|---|
| **Amont** | La santé plutôt que la maladie · l'élévation plutôt que l'éducation | Priorité d'affectation à ce qui augmente une capacité (art. 23) |
| **Souveraineté** | La souveraineté du peuple plutôt qu'une gouvernance de peu | Pondération quadratique : le nombre de personnes décide, pas les montants (art. 22) |
| **Liberté** | La liberté plutôt que la soumission | L'Enceinte : aucune application n'est interdite, toutes sont encerclées |
| **Proximité** | L'échelon proche plutôt que le sommet | Fédération à attestation mutuelle : les communautés cosignent leurs registres |
| **Mémoire** | La mémoire plutôt que l'amnésie | Le *pourquoi* inscrit avec le *quoi* — motifs, objections, et ce qui a fait changer d'avis (art. 26 sexies) |

*Une valeur sans mécanisme n'est qu'une déclaration, et on n'en écrit pas.*

---

## Ce que nous ne promettons pas

Un projet de souveraineté meurt de la première promesse démentie. Ces limites sont
publiques dès maintenant, et développées dans le
[catalogue](site/index.html).

- **iOS, jamais.** Un iPhone vérifie son démarrage contre des clés fondues dans le
  silicium ; il n'existe aucun chemin pour y inscrire la nôtre. Ce n'est pas un
  manque de moyens, c'est le matériel qui refuse.
- **Voter suppose d'avoir installé SERF.** Sur un appareil qu'on ne contrôle pas,
  on peut offrir la vérifiabilité, jamais l'intégrité — un téléphone compromis peut
  afficher un écran qui mente. *La vérification, elle, ne suppose rien : le
  Registre se contrôle depuis n'importe quoi, hors ligne, jusque sur papier.*
- **Les votes de SERF n'ont pas force de loi.** La force viendra de la pratique
  accumulée et de conventions signées — plus lent, infiniment plus solide.
- **Aucun noyau écrit de zéro.** Le projet part d'AOSP et emprunte partout où c'est
  possible. Le temps d'ingénierie va à la couche que personne d'autre ne construit.
- **Le paradoxe du client n'a pas de solution parfaite**, et la coercition est
  irréductible en vote à distance. On empile des défenses, et on le dit.
- **Un composant soudé ne se garantit pas par du logiciel.** On neutralise beaucoup
  — jusqu'à ne pas charger le micrologiciel qu'il attend — mais on ne peut pas
  prouver l'absence de ce qu'on ignore.

---

## Comment on décide, en bref

**Les Régents** — tous les porteurs admis au corps électoral, toujours au pluriel,
jamais une entité. On y entre par **parrainage** : trois Régents répondent de votre
existence distincte. Le vote est secret, séparé de l'admission par cryptographie et
non par promesse.

**La Table Ronde** — treize personnes qui instruisent, décident et exécutent, et qui
rendent compte. *Composition en cours de refonte : six pôles à deux sièges — l'un
élu, l'autre tiré au sort — plus un siège du peuple tiré au sort, qui fait la
balance.*

**Quatre expressions** : **Oui** · **Non** · **À nuancer** — *j'adhère, avec les
réserves déjà au dossier* · **Ignorer** — *je récuse la question elle-même*.
L'abstention n'y est pas : elle est le silence, et le silence ne se compte pas.

**Consultatif partout, contraignant sur la révocation.** Les Régents ne cogèrent pas
le quotidien — un commun où tout se vote se paralyse. Ils détiennent le seul pouvoir
qui ne se contourne pas : **renvoyer ceux qui décident.** Chaque « Ignorer »
majoritaire, chaque avis écarté sans réponse motivée inscrit un point de défiance.
**Cinq points, et le scrutin de dissolution s'ouvre de plein droit.**

**On argumente en délibération** — sept jours, signé, public, opposable. **On vote
au scrutin** — soixante-douze heures, secret, aucun texte joint. Les deux régimes ne
se mélangent jamais.

Détail : [`CHARTE.md`](CHARTE.md) · [`docs/03-REGENCE.md`](docs/03-REGENCE.md).

---

## Le Registre — vérifier, plutôt que croire

**Un journal de transparence à arbre de Merkle. Pas une chaîne de blocs** — celle-ci
ordonne des transactions entre inconnus sans identité, au prix d'une pondération par
le capital ou le calcul, ce qui serait écrire l'inverse de l'article 22 dans
l'infrastructure.

Le Registre ne *promet* pas qu'il n'a rien réécrit : il le **prouve**, à chaque
publication. **Chaque appareil sous SERF en est témoin** — il garde le dernier état
signé, exige la preuve, et le confronte à celui des appareils qu'il croise, sans
réglage et sans que son porteur ait à le savoir. Il en découle que **la
falsification produit sa propre preuve**.

Et ce qui ne s'y inscrit jamais : le lien entre une personne et son bulletin.

Détail : [`docs/06-REGISTRE.md`](docs/06-REGISTRE.md).

---

## Les communautés — gouverner à l'échelon proche

Le dispositif est **reproductible**. Un immeuble, un village, une école, une
coopérative, un syndicat — chacun peut tenir ses Régents, son registre et sa Table
Ronde. Sans autorisation, sans adhésion, sans redevance. **Sept personnes
suffisent**, et la procédure s'allège avec la taille : jusqu'à trente membres, *tous
les Régents sont* la Table Ronde.

Chaque communauté cosigne le registre de ses voisines. La protection vient du
voisinage, pas d'une autorité de contrôle. *Réserve à connaître : la cosignature
prouve qu'une chaîne n'a pas été réécrite — elle ne dit rien de la véracité de ce
qui y est inscrit.*

**On ne conquiert pas un sommet : on rend inutile qu'il y en ait un.**

Détail : [`docs/07-SUBSIDIARITE.md`](docs/07-SUBSIDIARITE.md).

---

## Documentation

| Document | Contenu |
|---|---|
| **[`docs/12-FAILLES-OUVERTES.md`](docs/12-FAILLES-OUVERTES.md)** | **Les défauts connus et non corrigés, par gravité. À lire avant tout le reste.** |
| [`CHARTE.md`](CHARTE.md) | Le texte fondateur — Titre I intangible, corps électoral, Table Ronde, fin de l'Amorçage |
| [`JOURNAL.md`](JOURNAL.md) | La chronologie : les décisions datées, leur pourquoi, et ce qu'on a changé d'avis |
| [`ROADMAP.md`](ROADMAP.md) | Les jalons et les arbitrages encore ouverts |
| [`docs/01-VISION.md`](docs/01-VISION.md) | Les cinq renversements, cibles, modèle économique |
| [`docs/02-ARCHITECTURE.md`](docs/02-ARCHITECTURE.md) | Socle AOSP, l'Enceinte, périmètre matériel, confiance matérielle |
| [`docs/03-REGENCE.md`](docs/03-REGENCE.md) | Gouvernance, scrutin, modèle de menace, résilience |
| [`docs/04-DESIGN.md`](docs/04-DESIGN.md) | Jetons de couleur, typographie, accessibilité — contrastes calculés |
| [`docs/05-PUBLICATION.md`](docs/05-PUBLICATION.md) | Miroirs, clés, continuité, cloisonnement des identités |
| [`docs/06-REGISTRE.md`](docs/06-REGISTRE.md) | Transparence non falsifiable, témoignage citoyen, ancrage papier |
| [`docs/07-SUBSIDIARITE.md`](docs/07-SUBSIDIARITE.md) | Les communautés fédérées, les trois paliers d'échelle |
| [`docs/08-RESILIENCE.md`](docs/08-RESILIENCE.md) | Gouverner sans réseau : maillage, radio, papier, impulsion électromagnétique |
| [`docs/09-BRIEF-DESIGN.md`](docs/09-BRIEF-DESIGN.md) | Brief autoportant : écrans, accessibilité, règles à ne pas enfreindre |
| [`docs/10-SURFACES.md`](docs/10-SURFACES.md) | Les ~35 surfaces d'un système : écrire / adapter / adopter |
| [`docs/11-ETAT-DE-LART.md`](docs/11-ETAT-DE-LART.md) | Recherche sourcée : vote vérifiable, précédents, droit français, socle |

---

## État du projet

**Jalon 0 — Fondations.** Aucun code n'est écrit. Les documents fondateurs le sont,
et une [Charte](CHARTE.md) en version 0.2 est soumise à délibération sans être
adoptée. C'est le préalable : les décisions prises ici engagent des années de
travail en aval.

**Décidé à ce jour** — fork AOSP · socle de lignée GrapheneOS, *à confirmer sur
sources primaires* · iOS hors périmètre · corps électoral par parrainage et jeton
signé en aveugle · l'Enceinte comme stratégie d'adoption · le scrutin prouvé
**avant** la ROM · pas d'application sur les systèmes des autres, un installateur en
un clic à la place.

**Ouvert** — la composition de la Table Ronde · les seuils de l'Amorçage · le quorum
du scrutin de dissolution · le calibrage général des seuils · la licence. Et
**seize failles connues**, dont deux qui doivent être tranchées avant l'adoption de
la Charte, parce que le Titre I n'est pas révisable une fois adopté.

Voir [`ROADMAP.md`](ROADMAP.md) et
[`docs/12-FAILLES-OUVERTES.md`](docs/12-FAILLES-OUVERTES.md).

---

## Contribuer

La manière la plus utile de contribuer aujourd'hui n'est pas d'écrire du code — il
n'y en a pas — mais de **casser un raisonnement** : une règle qui se retourne contre
ceux qu'elle protège, une contradiction entre deux articles, un seuil dont
l'arithmétique ne tient pas, une affirmation que nous n'avons pas étayée.

Les défauts les plus graves de ce dépôt ont été trouvés comme ça.

---

## Licence

À déterminer. Contrainte structurante : AOSP est sous Apache 2.0, le noyau Linux
sous GPLv2. Toute distribution de SERF **doit** publier ses modifications du noyau.
Ce n'est pas une gêne — c'est cohérent avec la promesse de vérifiabilité. Voir la
discussion dans [`ROADMAP.md`](ROADMAP.md).

---

*Signé `Le Sans-Ciel`. Dépôt public :
[github.com/Aku-Origin/SERF](https://github.com/Aku-Origin/SERF). Les miroirs
Codeberg, Software Heritage et Radicle ne sont pas encore en place.*
