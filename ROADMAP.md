# Feuille de route

> Principe directeur : **construire d'abord ce qui n'existe nulle part.**
> La ROM dégooglisée emprunte au maximum à l'existant ; la Régence est le produit.

---

## Jalon 0 — Fondations *(en cours)*

Écrire ce qui engage des années de travail en aval.

- [x] Vision et positionnement — [`docs/01-VISION.md`](docs/01-VISION.md)
- [x] Architecture et arbre de décision — [`docs/02-ARCHITECTURE.md`](docs/02-ARCHITECTURE.md)
- [x] Modèle de gouvernance et de scrutin — [`docs/03-REGENCE.md`](docs/03-REGENCE.md)
- [x] Système de design — [`docs/04-DESIGN.md`](docs/04-DESIGN.md)
- [x] **Charte v0** — [`CHARTE.md`](CHARTE.md), soumise à délibération, non adoptée
- [x] **Décision : modèle d'identité** — parrainage (3 parrains, 5/an) + jeton
      d'éligibilité signé en aveugle
- [x] **Décision : stratégie d'adoption** — l'Enceinte, encapsuler et non exclure
- [x] **Décision : gouvernance** — les Régents / la Table Ronde des Treize ;
      consultatif partout sauf dissolution et révision de la Charte ; quatre
      expressions (Oui, Non, À nuancer, Ignorer) ; compteur de défiance
- [x] **Plan de publication et de continuité** —
      [`docs/05-PUBLICATION.md`](docs/05-PUBLICATION.md)

### Jalon 0 bis — Publier, **avant tout développement**

Tant que les miroirs ne sont pas en place, tout le projet tient sur une seule
machine. C'est le point unique de défaillance le plus bête à laisser en place.

- [ ] Arbitrer l'adresse de courriel du projet (domaine propre ou `noreply`)
- [ ] Clé de signature des commits, et publication de la clé publique
- [ ] Premier commit signé, puis `push` sur GitHub
- [ ] Miroir Codeberg + synchronisation automatique à chaque commit sur `main`
- [ ] Archivage Software Heritage (à refaire après chaque jalon)
- [ ] Dépôt Radicle, identifiant noté au README
- [ ] `SUCCESSION.md` — qui détient quelle clé, quels miroirs, ordre de reprise
- [ ] Répartition des trois clés de signature d'image (Charte, art. 47)

### Jalon 0 ter — Cadre juridique

- [ ] Relecture juridique de la Charte (association loi 1901 ou société à mission)
- [ ] Forme juridique de la structure porteuse — clause : elle est mandataire du
      commun, non propriétaire
- [ ] Licence du projet

---

## Jalon 1 — La Régence, prouvée hors de l'OS

**Objectif : démontrer que le scrutin fonctionne, avant d'écrire une ligne de
code système.** Une application web et Android autonome, utilisable par une
association réelle pour ses propres décisions.

C'est délibérément l'inverse de l'ordre intuitif. Raisons :

- Le scrutin est le risque n°1 du projet. Un risque se teste tôt, pas tard.
- Une association qui vote réellement avec l'outil fournit la première preuve
  de légitimité par l'usage.
- Cela ne dépend d'aucun matériel, d'aucun fork, d'aucune certification.

Contenu :

- [ ] **`serf-preuve`** — bibliothèque de vérification hors ligne. **À écrire en
      premier**, avant le journal : écrire le vérificateur d'abord oblige à
      définir ce qui doit être prouvé, et évite un journal dont les preuves
      seraient commodes à produire mais pénibles à contrôler
- [ ] **`serf-transport`** — abstraction des canaux (réseau, maillage, LoRa, QR,
      fichier). **Dès la première ligne du Registre** : ajoutée après coup, elle
      ne fonctionne jamais, mille suppositions de connectivité s'étant glissées
      partout entre-temps
- [ ] `serf-maille` — synchronisation de proche en proche, sans infrastructure
- [ ] `serf-ancre` — feuilles d'ancrage trimestrielles et suivi des dépôts
      (archives, BnF, notaire, presse)
- [ ] `serf-registre` — journal à arbre de Merkle, têtes signées, preuves
      d'inclusion et de cohérence (partir de **Trillian**, ne pas réimplémenter)
- [ ] `serf-temoin` — le témoin embarqué : conservation des têtes, vérification,
      échange entre appareils
- [ ] `serf-cosignataires` — contresignature k-sur-n, recrutement des entités
- [ ] `serf-scrutin` — chiffrement homomorphe, dépouillement à seuil
      (partir de **Belenios**, éprouvé et audité, plutôt que de réimplémenter)
- [ ] `serf-identite` — jeton d'éligibilité par signature aveugle
- [ ] `serf-forum` — propositions, parrainages, amendements, objections tracées,
      **motifs et changements d'avis** (Charte, art. 26 sexies)
- [ ] `serf-communaute` — créer un échelon, définir son objet, calibrer la
      procédure aux trois paliers (7-30 / 30-500 / 500+)
- [ ] `serf-federation` — cosignature mutuelle des registres, adhésion, retrait
- [ ] `serf-parole` — messagerie fédérée sur **Matrix**, liée au registre des
      objections. **Jamais de fil algorithmique**
- [ ] Interface Table Ronde, aux couleurs du système de design
- [ ] **Audit cryptographique externe** — non négociable avant tout usage réel
- [ ] Premier scrutin réel avec une association pilote

---

## Jalon 2 — La ROM

- [ ] Choix définitif du socle (LineageOS recommandé, cf. architecture §2)
- [ ] Liste courte d'appareils cibles, avec verified boot vérifié modèle par modèle
- [ ] Build reproductible, à l'octet près — **préalable à toute distribution**
- [ ] Substituts souverains par défaut (F-Droid, UnifiedPush, BeaconDB, OSM)
- [ ] **L'Enceinte** — la couche d'adoption, cf. [architecture §4](docs/02-ARCHITECTURE.md) :
  - [ ] Services Google déprivilégiés (application ordinaire, zéro privilège)
  - [ ] **Réponses vides et sous-ensembles** au lieu des refus de permission —
        contacts, stockage, position, capteurs
  - [ ] Espaces cloisonnés à chiffrement distinct, gelables d'un geste
  - [ ] Pare-feu réseau par application
  - [ ] Journal d'activité : ce que chaque application a tenté, et vers qui
- [ ] Durcissement mémoire, permissions granulaires (capteurs, presse-papiers)
- [ ] Chaîne de mise à jour OTA à signature multi-parties
- [ ] Transparence des binaires — journal public infalsifiable des images publiées

---

## Jalon 3 — L'intégration

Ce qui n'est possible qu'en contrôlant la pile entière.

- [ ] `RegenceNotifier` — canal de notification système qu'aucun tiers ne peut
      enterrer. C'est la fonction que seule l'intégration OS rend possible.
- [ ] Table Ronde en application système, liée au verified boot
- [ ] Vérification hors-bande du bulletin depuis un appareil tiers
- [ ] Habillage complet : lanceur, écran de verrouillage, applications système
- [ ] Tableau de bord de souveraineté — que fait chaque application, avec qui elle
      parle, ce qu'elle a envoyé

---

## Arbitrages ouverts

Décisions bloquantes, à trancher avant le jalon 1. Chacune engage des années.

**1. Portée des votes.** Consultatifs, ou statutairement contraignants pour la
structure porteuse ? Le second est la seule version qui tient la promesse — et
exige des statuts rédigés pour cela. Bloquant pour le choix de la forme
juridique.

**2. Calibrage des seuils de la Charte.** 3 parrains, 5 parrainages par an, 7
jours de délibération, 1 % ou 100 soutiens, 36 mois de Régence : ces nombres sont
des propositions argumentées, pas des mesures. Ils doivent être éprouvés sur
l'association pilote du jalon 1 avant d'être figés.

**3. Financement.** Le financement public est le plus accessible et le plus
contradictoire avec le message. À trancher explicitement, pas par défaut.

**4. Licence.** Le noyau impose GPLv2 pour ses modifications. Pour la couche
Régence, une licence copyleft forte (AGPLv3) empêcherait un tiers d'exploiter le
scrutin sans en publier les modifications — ce qui est cohérent avec l'exigence
de vérifiabilité.

---

## Ce qui n'est pas au programme

- **iOS.** Techniquement impossible, cf. architecture §1.
- **Voter la loi de la République.** Juridiquement impossible, cf. Régence §1.
- **Écrire un noyau.** Cf. architecture §1.

Ces trois exclusions sont des choix de crédibilité. Elles doivent figurer dans la
communication publique, pas seulement dans la documentation interne.
