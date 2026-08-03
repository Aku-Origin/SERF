# 06 — Le Registre : transparence non falsifiable

> **Tout ce qui relève du pouvoir est inscrit. Rien de ce qui est inscrit ne peut
> être réécrit. Chaque citoyen le vérifie lui-même.**
>
> Trois phrases, et tout le reste de ce document sert à les tenir sans jamais
> demander à personne de faire confiance.

---

## 1. Pourquoi pas une blockchain

L'intuition — *« tout enregistré, à l'image d'une blockchain »* — vise les bonnes
propriétés. Mais la blockchain est un outil taillé pour un autre problème, et
l'adopter ici coûterait cher tout en contredisant la Charte.

**Ce qu'une blockchain résout :** se mettre d'accord sur un **ordre** entre des
inconnus mutuellement méfiants, **sans couche d'identité**. Pour empêcher qu'un
acteur se démultiplie, elle rend la participation coûteuse — calcul (preuve de
travail) ou capital immobilisé (preuve d'enjeu).

**Ce que SERF a déjà :** une couche d'identité (le parrainage, art. 8 à 11) et un
rédacteur désigné du registre. Il n'y a pas de double dépense à empêcher, ni
d'ordre à négocier entre anonymes.

**Le vrai problème de SERF est ailleurs :** empêcher que celui qui tient le
registre puisse **réécrire discrètement** ce qui y a été inscrit. C'est de
l'inviolabilité par la preuve, pas du consensus.

Et un argument devrait emporter à lui seul la décision :

> **La preuve d'enjeu pondère le pouvoir par la fortune détenue.** C'est
> littéralement une gouvernance de peu. L'adopter reviendrait à écrire dans
> l'infrastructure l'exact contraire de l'article 22, qui fait peser le nombre de
> personnes et non les montants.

S'y ajoutent le coût énergétique, la latence, la nécessité d'un jeton — donc d'une
spéculation — et l'impossibilité pratique de faire tourner un nœud complet sur un
téléphone. Or c'est précisément sur les téléphones que la vérification doit avoir
lieu.

**Ce qu'on garde de la culture blockchain :** tout est public, tout est
vérifiable, personne n'est cru sur parole. **Ce qu'on jette :** le coût, la
lenteur, le jeton et la ploutocratie.

---

## 2. Ce qu'on utilise à la place : le journal de transparence

Un **journal à arbre de Merkle** — la structure des journaux de transparence des
certificats (Certificate Transparency), en service à l'échelle d'Internet depuis
2013, reprise depuis par Sigstore et par la base de sommes de contrôle de Go.

C'est une technologie **ennuyeuse, éprouvée et auditée**. Pour une infrastructure
de vote, c'est une qualité, pas un défaut.

### Les trois propriétés, et ce qu'elles donnent

**Preuve d'inclusion** — démontrer qu'une entrée précise figure bien dans le
journal coûte environ log₂(n) empreintes. Pour un million d'entrées : vingt
empreintes. Un téléphone le calcule instantanément, hors ligne.

*Ce que ça donne au citoyen :* « mon bulletin est dans l'urne » n'est plus une
affirmation du serveur, c'est un calcul fait sur son appareil.

**Preuve de cohérence** — démontrer que le journal d'aujourd'hui **contient celui
d'hier, inchangé**. Pas « nous n'avons rien modifié », mais une preuve
mathématique qu'aucune modification n'est possible sans être détectée.

*Ce que ça donne :* le caractère non falsifiable, au sens fort. Une réécriture ne
casse pas la sécurité — elle casse la preuve, et devient visible.

**Tête d'arbre signée** — périodiquement, le journal signe : « à cet instant, je
contiens N entrées, ma racine vaut R ». C'est un engagement daté, signé, opposable.

---

## 3. Sécurisé par chaque citoyen : le témoignage

C'est ici que « sécurisé par chaque citoyen » cesse d'être une image.

**Chaque appareil SERF est un témoin du registre.** Sans configuration, sans
effort, sans que son porteur ait à le savoir :

1. Il **conserve** la dernière tête d'arbre signée qu'il a vue.
2. À chaque échange avec le journal, il **exige une preuve de cohérence** entre sa
   tête stockée et la nouvelle. Sans preuve valide, il refuse et alerte.
3. Il **échange ses têtes** avec les autres appareils qu'il croise, et compare.

### Pourquoi c'est décisif

Pour réécrire l'histoire, l'opérateur devrait présenter **deux versions
divergentes** du journal à des appareils différents. Cette attaque — la vue
scindée — est la seule qui reste. Elle échoue dès que deux appareils comparent
leurs têtes.

Avec des centaines de milliers d'appareils qui comparent en permanence, la
divergence est détectée en quelques minutes. Et surtout :

> **La triche produit sa propre preuve.** Deux têtes d'arbre incohérentes, toutes
> deux signées par l'opérateur, constituent une démonstration irréfutable et
> transférable qu'il a triché. **Il signe lui-même sa condamnation.**

Aucune autorité n'a besoin d'arbitrer. N'importe qui peut vérifier les deux
signatures et conclure.

### Les cosignataires

Le témoignage citoyen est renforcé par un collège de **cosignataires** — entités
indépendantes, en juridictions distinctes (Charte, art. 49), qui contresignent les
têtes d'arbre après avoir vérifié la cohérence.

Un appareil n'accepte une tête que si elle porte **k signatures sur n**. On obtient
la résistance aux acteurs malveillants sans aucun mécanisme de consensus, sans
minage, sans jeton, sans latence.

**Candidats naturels :** une association de défense des libertés numériques, un
laboratoire public, un syndicat, une collectivité, une fondation étrangère. La
diversité des motivations vaut mieux que le nombre.

---

## 4. Ce qui s'inscrit

La transparence porte sur **les actes de pouvoir**. Sans exception.

| Catégorie | Inscrit |
|---|---|
| **Délibération** | Propositions, amendements, objections, parrainages de mise à l'ordre du jour |
| **Scrutins** | Bulletins chiffrés, décompte, preuves de dépouillement, résultat |
| **Table Ronde** | Ordres du jour, procès-verbaux, **votes nominatifs de chaque membre** |
| **Redevabilité** | Réponses motivées (art. 35) — **et l'expiration du délai sans réponse** |
| **Défiance** | Chaque point inscrit, son motif, l'état du compteur |
| **Désignations** | Élections des Corps, tirages au sort et leur graine publique |
| **Ressources** | Chaque mouvement, chaque affectation, chaque dérogation motivée à l'art. 23 |
| **Technique** | Images publiées, empreintes de construction reproductible, attributions et révocations de clés |
| **Charge** | Transmission de la charge nommée (art. 52) |

**Le silence est un événement inscrit.** Quand le délai de trente jours de
l'article 35 expire sans réponse, le registre inscrit l'expiration. Ne rien faire
laisse une trace. C'est ce qui empêche l'inaction d'être la stratégie d'évitement
la plus rentable.

**Les tirages au sort sont vérifiables.** La graine est engagée publiquement
*avant* le tirage et révélée après ; chacun recalcule le résultat. Un tirage
invérifiable est une nomination déguisée.

---

## 5. Ce qui ne s'inscrit jamais

**Le lien entre un Régent et son bulletin.** Jamais, sous aucune forme, sous aucun
motif, sous aucune pression.

L'asymétrie est fondatrice et se lit dans toute la Charte :

> **Transparence totale des actes de pouvoir. Secret total du vote individuel.**
> Le secret protège le faible ; la publicité contraint le puissant.

Un registre qui enregistrerait « tout » sans cette réserve ne serait pas une
avancée démocratique : ce serait le meilleur instrument de rétorsion jamais
construit, et il serait offert clés en main à qui s'en emparerait.

---

## 6. Le conflit à résoudre : effacement et registre immuable

**Un journal immuable et un droit à l'effacement sont contradictoires** — et le
projet est pris entre les deux : le RGPD impose l'un, l'article 4 de sa propre
Charte l'impose aussi.

Un registre naïvement conçu — « on inscrit tout pour toujours » — serait en
infraction avec la loi **et** avec le texte fondateur du projet. Il faut le régler
à la conception, car après le premier enregistrement il est trop tard.

**La résolution : le registre inscrit des actes, jamais des personnes.**

- Aucune donnée personnelle n'entre dans le journal. Ni nom, ni adresse, ni
  identifiant d'appareil, ni adresse réseau.
- Ce qui y entre est un **engagement cryptographique** — une empreinte qui ne
  révèle rien mais que l'intéressé peut prouver.
- La correspondance entre une personne et ses engagements vit **hors du journal**,
  dans un registre d'identité effaçable.
- Quand un Régent exerce son droit de sortie, cette correspondance est détruite.
  Le journal demeure intact et vérifiable ; ses entrées deviennent
  **définitivement non rattachables**. La personne a disparu ; l'histoire du
  commun est préservée.

Le graphe des parrainages, public par nécessité (art. 10), suit le même régime :
il relie des **identifiants pseudonymes**, jamais des états civils.

---

## 7. Simple et déclaratif : la complexité vit dans la machine

> **La complexité est dans la preuve, jamais dans le geste.**

Le citoyen voit un texte en langue claire et quatre boutons. Son appareil, en
silence, vérifie la tête d'arbre, exige la preuve de cohérence, calcule la preuve
d'inclusion de son bulletin, et échange ses têtes avec les appareils croisés.

Il n'a rien à comprendre pour être protégé. Il peut tout comprendre s'il le veut.

**Le sceau « vérifié » veut dire quelque chose.** Partout ailleurs, un tel
indicateur signifie « un serveur nous l'a affirmé ». Ici il signifie : **votre
appareil a fait le calcul.** C'est une différence de nature, et c'est la seule
promesse d'interface que le système n'a pas le droit de rompre.

Trois écrans, et rien de plus :

- **Ce qui se décide** — l'ordre du jour, en langue claire.
- **Ce que j'ai dit** — mes expressions passées, chacune avec sa preuve
  d'inclusion vérifiable hors ligne.
- **Ce qu'ils ont fait** — les votes nominatifs des Treize, les réponses motivées,
  les silences, le compteur de défiance.

Le troisième écran est le plus important, et c'est celui qu'aucune institution
n'offre aujourd'hui.

---

## 8. Composants et étapes

| Composant | Rôle |
|---|---|
| `serf-registre` | Journal à arbre de Merkle, têtes signées, service de preuves |
| `serf-temoin` | Le témoin embarqué : conservation des têtes, vérification, échange |
| `serf-cosignataires` | Protocole de contresignature k-sur-n |
| `serf-preuve` | Bibliothèque de vérification hors ligne — **la première brique à écrire** |

**Ordre de construction.** La bibliothèque de vérification d'abord, avant le
journal lui-même : écrire le vérificateur en premier oblige à définir précisément
ce qui doit être prouvé, et évite de concevoir un journal dont les preuves seraient
commodes à produire mais pénibles à contrôler.

**Ne rien réimplémenter.** Trillian et les bibliothèques de journaux de
transparence existent, sont auditées et éprouvées. Réécrire un arbre de Merkle
signé est la façon la plus sûre d'introduire une faille dans la fondation.
