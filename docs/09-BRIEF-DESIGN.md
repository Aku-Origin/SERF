# 09 — Brief de conception

> **Document autoportant.** Il se lit seul, sans le reste du dépôt, et suffit à
> concevoir les écrans de SERF. Il est fait pour être remis tel quel à un
> concepteur — humain ou modèle.

---

## 1. Ce qu'on conçoit

Un système d'exploitation mobile souverain, et surtout **son organe de
gouvernance** : la Table Ronde, où des citoyens délibèrent et votent les règles du
commun qu'ils habitent.

L'utilisateur n'est pas un consommateur. C'est un **Régent** : quelqu'un qui
exerce un pouvoir. Toute l'interface doit être conçue pour cette personne-là.

**Slogan :** *Prenez le contrôle absolu de votre univers numérique.*
**Signature :** Le Sans-Ciel — *rien au-dessus.*

---

## 2. Le ton

**La sobriété est l'argument.** SERF vend le contrôle, la sécurité et la mémoire.
Chaque effet gratuit — dégradé, verre dépoli, animation d'apparition,
micro-interaction festive — travaille contre le message. L'interface doit avoir la
tenue d'un **document officiel**, pas d'une application de divertissement.

**Registre visé :** un acte notarié bien composé. Un bulletin de vote. Une plaque
gravée. Sérieux sans être froid, dense sans être encombré, ancien sans être
pastiche.

**À fuir explicitement :** l'esthétique « tableau de bord de startup », les cartes
flottantes à ombre portée, les illustrations de personnages, les emojis dans
l'interface, les barres de progression ludiques, les félicitations après une
action, le terme « communauté » employé comme argument marketing.

**Deux références de justesse :** la typographie d'un journal officiel bien
imprimé ; la sobriété d'un terminal bancaire suisse. **Une anti-référence :**
toute application qui cherche à vous faire revenir.

---

## 3. Couleurs

Trois familles, tenues avec discipline. **Sombre par défaut** — cohérent avec le
récit de souveraineté, économe en OLED, et attendu d'un système de sécurité. Le
thème clair est un premier rôle, pas un rattrapage.

### Nuit — la structure

`#05090F` · `#0A1424` *(fond principal sombre)* · `#101F3A` *(surfaces)* ·
`#182C50` *(bordures)* · `#223A66` · `#2F4B80` · `#4C6BA0` *(texte tertiaire)* ·
`#7A93BD` *(texte secondaire)* · `#B0C0D8` *(icônes)* · `#DCE4EF` *(fond clair)*

### Régence — le rouge, scindé par usage

| Jeton | Hex | Usage |
|---|---|---|
| `regence-800` | `#6E1414` | Remplissage pressé |
| `regence-700` | `#8C1A1A` | Remplissage survolé |
| `regence-600` | `#A62121` | **Remplissage principal** |
| `regence-400` | `#D65A5A` | **Texte et bordures accentués** |
| `regence-300` | `#E99494` | Texte sur fond très sombre |

> **Règle absolue :** `regence-600` ne porte **jamais** de texte sur fond nuit —
> contraste 3.2:1, échec WCAG AA. Il est un **remplissage**, avec du blanc dessus
> (6.4:1 ✓). Pour du texte rouge sur fond sombre : `regence-400` minimum.

### Clarté et sémantique

`#FFFFFF` · `#F6F7F9` *(fond clair)* · `#E9ECF1` *(surfaces claires)*

`#2E7D5B` **scellé** (chiffré, vérifié) · `#B8860B` **alerte** (permission
sensible) · `#C13030` **péril** (non chiffré, fuite)

**Le rouge est rare.** Il ne signale que trois choses : un acte régalien (voter,
signer, révoquer), un état critique, un sceau. Partout, il ne signifie plus rien.

---

## 4. Typographie

**Marianne** est le choix évident pour le récit — caractère officiel de l'État
français. **Vérifier sa licence avant tout usage** : son emploi est cadré par la
charte de l'État et un projet privé n'y a pas droit automatiquement.

Repli sans risque, entièrement libre :

| Rôle | Fonte | Graisse | Taille | Interlignage |
|---|---|---|---|---|
| Titre régalien | Spectral | 600 | 32 | 1.2 |
| Titre de section | Inter | 600 | 22 | 1.3 |
| Corps d'interface | Inter | 400 | 16 | 1.5 |
| **Texte de proposition** | **Spectral** | **400** | **17** | **1.65** |
| Étiquette | Inter | 500 | 13 | 1.4 |
| Données techniques | JetBrains Mono | 400 | 14 | 1.5 |

Le texte soumis au vote se lit en **empattement, à 17 px, interligne généreux** :
c'est le seul endroit du système optimisé pour la lecture soutenue plutôt que pour
le balayage. Choix typographique porteur d'une intention politique — **on veut que
les gens lisent avant de voter.**

---

## 5. Les écrans à concevoir

Deux ensembles, qui suivent la césure de la §7 : **neuf écrans pour la Régence**,
qui tournent partout — Android ancien, iPhone, navigateur ; **deux écrans de
plus** qui n'existent que dans le système SERF, parce qu'ils supposent de contrôler
la pile entière.

| | Écran | Ensemble |
|---|---|---|
| 1 | Devenir Régent | Régence |
| 2 | Mes échelons | Régence |
| 3 | L'ordre du jour | Régence |
| 4 | La proposition *(porte le geste des quatre expressions)* | Régence |
| 5 | La parole *(publique, opposable)* | Régence |
| 5 bis | **La messagerie** *(privée, sans trace)* | Régence |
| 6 | Ce que j'ai dit | Régence |
| 7 | Ce qu'ils ont fait | Régence |
| 8 | Le Registre | Régence — **consultable sans compte** |
| 9 | L'état du lien | Régence |
| 10 | Le tableau de souveraineté | Système seulement |
| 11 | L'Enceinte | Système seulement |

### 5.0 — Devenir Régent

Le seul parcours d'entrée. On y demande son admission, on suit ses trois
parrainages, on reçoit son jeton d'éligibilité.

L'écran doit rendre lisible ce qui se passe, parce que c'est contre-intuitif :
**le parrainage est public, le vote ne l'est pas.** Trois personnes attestent que
vous existez distinctement ; aucune ne saura jamais comment vous votez. Le dire en
une phrase, sur cet écran, vaut mieux que dix pages de documentation.

Contrainte : **l'attente est normale et doit être présentée comme telle.** Un
parrainage prend le temps qu'il prend. Aucune barre de progression, aucune
relance, aucune incitation à recruter vite — c'est exactement le comportement
qu'un attaquant voudrait encourager.

### 5.1 — Mes échelons

Les communautés auxquelles on appartient — immeuble, quartier, coopérative,
métier, commune — et ce qui délibère dans chacune.

**Présentation à plat, jamais en arborescence.** Ces appartenances se recoupent
sans hiérarchie : ce ne sont pas des poupées russes, c'est un tissu. Une
présentation en niveaux emboîtés induirait qu'un échelon commande l'autre, ce que
l'article 44 ter interdit.

Depuis cet écran : rejoindre une communauté, en créer une à sept, et **la
quitter** — la sortie doit être aussi visible que l'entrée. Un ensemble qu'on ne
peut pas quitter n'a aucune raison de bien traiter ses membres.

### 5.2 — L'ordre du jour

Ce qui se décide en ce moment. Chronologique, jamais classé par « pertinence ».
Chaque entrée porte : son titre en langue claire, son étape (délibération /
scrutin ouvert / clos), le temps restant, et rien d'autre.

**Aucun compteur de participation visible pendant un scrutin ouvert.** Afficher
« 68 % de Oui » pendant le vote fabrique un effet de ralliement. Les résultats
n'apparaissent qu'à la clôture.

### 5.3 — La proposition *(l'écran le plus important)*

En haut : **la version FALC** — Facile À Lire et à Comprendre. Phrases courtes,
un sujet par phrase, aucun jargon. **C'est la version par défaut**, pas une
option d'accessibilité reléguée. Une proposition qui n'en a pas ne peut pas être
mise aux voix (Charte, art. 14 bis).

En dessous, dépliables : le texte intégral, les objections déposées, les
amendements, et **ce qui a fait changer d'avis** — le cœur de la mémoire du
projet.

En bas, le geste central : **les quatre expressions.**

#### Le geste — quatre boutons, jamais trois, jamais cinq

| | Ce que ça dit |
|---|---|
| **Oui** | J'adhère au texte tel qu'il est. |
| **Non** | Je le refuse. |
| **À nuancer** | Le principe tient, pas ce texte-ci. Reprenez-le. |
| **Ignorer** | Je récuse la question elle-même. |

Contraintes de conception :

- **Les quatre ont exactement le même poids visuel.** Aucune n'est le choix par
  défaut, aucune n'est mise en avant, aucune n'est plus grande.
- **Jamais distinguées par la seule couleur.** Chacune porte un libellé, et une
  forme ou un pictogramme distinct.
- **« Ignorer » n'est pas grisé ni traité comme un abandon.** C'est un acte fort —
  il arme le compteur de défiance. Le concevoir comme un renoncement trahirait
  tout le dispositif.
- **Modifiable jusqu'à la clôture**, affiché comme tel. C'est la protection contre
  la coercition : voter sous pression, puis revoter seul.
- **Aucune confirmation festive.** Pas d'animation de succès, pas de « merci ».
  Un vote est un acte ordinaire de citoyen, pas une performance.

### 5.4 — La parole

Là où l'on délibère : objections, amendements, contre-propositions. Adossé à
**Matrix**, protocole fédéré déjà retenu par l'État français.

Trois contraintes qui le distinguent de tout ce qui existe :

- **Ordre chronologique, point.** Aucun classement par pertinence, popularité ou
  réaction. Ce qui remonte à l'ordre du jour, c'est ce qui a recueilli des
  parrainages — jamais ce qui a provoqué des réactions.
- **La parole peut devenir opposable.** Une objection déposée s'inscrit au
  Registre : il faudra y répondre. C'est ce qui distingue une délibération d'un
  fil de commentaires — la parole cesse de se dissiper.
- **Aucune mesure d'engagement affichée.** Ni compteur de vues, ni approbations,
  ni badges. **On ne construit pas un réseau social** : un flux optimisé pour
  l'engagement produit l'exact inverse de l'élévation. Ligne rouge, pas
  préférence.

### 5.4 bis — La messagerie *(privée)*

Se parler. Chiffré de bout en bout, sans numéro de téléphone, sans trace.

**Contrainte majeure de conception — la plus grave du système :** cet écran et
celui de la Parole (5.4) doivent être **visuellement irréconciliables**. Fond,
typographie, densité, iconographie : rien de commun. Aucun passage de l'un à
l'autre sans rupture explicite et nommée. Aucune fonction de partage ne fait
glisser un message privé vers le public sans un acte délibéré.

> **Quelqu'un qui croit chuchoter alors qu'il dépose au Registre, c'est une vie
> abîmée.** Toute ambiguïté visuelle entre les deux paroles est un défaut
> bloquant, au même titre qu'une faille cryptographique.

L'écran affiche en permanence, sans emphase, ce qu'il est : *privé, chiffré, aucune
trace au Registre*. Détail technique en [`10-SURFACES.md §4`](10-SURFACES.md).

### 5.5 — Ce que j'ai dit

L'historique personnel de ses expressions. Chacune accompagnée de **sa preuve
d'inclusion, vérifiable hors ligne**.

> Le sceau **« vérifié »** doit signifier ce qu'il dit. Partout ailleurs, un tel
> indicateur veut dire *« un serveur nous l'a affirmé »*. Ici il veut dire
> **« votre appareil a fait le calcul »**. C'est la seule promesse d'interface que
> le système n'a pas le droit de rompre — et elle doit être visuellement
> distincte de toute autre coche de l'écosystème logiciel.

### 5.6 — Ce qu'ils ont fait *(l'écran qui n'existe nulle part)*

La redevabilité des Treize. Pour chaque membre : ses **votes nominatifs**, ses
présences, ses réponses motivées. Pour l'organe : le **compteur de défiance**, son
état sur douze mois glissants, et chaque point avec son motif.

**Les silences y figurent.** Un délai de réponse expiré est affiché comme un
événement, pas comme une absence de ligne.

C'est l'écran que nulle institution n'offre aujourd'hui. Il doit être aussi soigné
que l'écran de vote.

### 5.7 — Le Registre

La consultation publique de la mémoire du commun : décisions, motifs, objections,
et ce qui a fait changer d'avis.

**Accessible sans compte, sans identification, sans installation.** Lire ce que
décide un commun ne doit jamais exiger d'en faire partie — c'est ce qui permet à
un journaliste, un chercheur, un élu ou un curieux de vérifier par lui-même. Un
registre qu'il faut mériter n'est pas public.

Chaque entrée porte son empreinte, copiable, et **l'état d'ancrage** : la feuille
trimestrielle qui la couvre, où elle a été déposée.

### 5.8 — L'état du lien

Le mode de fonctionnement en cours : **plein**, **maillé**, **différé**,
**papier**.

Contrainte de ton : ce n'est **jamais une erreur**. Le système descend, il ne
tombe pas. « Différé — votre bulletin partira au prochain contact » n'est pas une
panne à signaler en rouge, c'est un fonctionnement nominal à énoncer calmement.
Traiter le hors-ligne comme une anomalie apprendrait aux gens qu'ils dépendent du
réseau, ce qui est précisément ce qu'on défait.

On y trouve aussi : les bulletins en attente d'envoi, l'export en sauvegarde
froide, et le partage de proche en proche pour aider un voisin à se synchroniser.

### 5.9 — Le tableau de souveraineté *(système seulement)*

Ce que chaque application a tenté : permissions demandées, serveurs contactés,
volume transmis, heure. La surveillance des surveillants.

### 5.10 — L'Enceinte *(système seulement)*

Par application : réseau ouvert / filtré / coupé, et pour chaque permission le
choix entre **réel**, **vide** et **sous-ensemble**. Le vocabulaire doit rendre
évident qu'on ne « refuse » pas — **on répond autre chose**, et l'application
continue de fonctionner.

---

## 6. Accessibilité — le niveau visé

**Un système qui exclut n'est pas souverain.** L'accessibilité n'est pas une
option de conformité : c'est une obligation constitutionnelle du projet
(Charte, art. 6, non révisable).

**Cible : WCAG 2.2 niveau AAA sur le chemin de vote**, AA partout ailleurs. Le
chemin de vote est : ordre du jour → proposition → expression → confirmation.

| Besoin | Exigence |
|---|---|
| **Vue** | Contraste ≥ 7:1 sur le chemin de vote. Fonctionnel à 200 % de police. Aucune information par la seule couleur. Lecteur d'écran complet, testé avec des personnes aveugles — pas simulé. |
| **Motricité** | Cibles ≥ 48 dp. Navigation complète au balayage et au clavier. **Aucun geste requis** — pas de glissement, pas d'appui long obligatoire. Aucune contrainte de temps sur un geste. |
| **Cognition** | **Version FALC obligatoire de toute proposition.** Une phrase, une idée. Aucun jargon non défini sur place. Aucun compte à rebours anxiogène. |
| **Audition** | Aucune information portée par le son seul. Sous-titres systématiques. Interprétation LSF pour les textes fondateurs. |
| **Lecture** | Le Registre est **consultable sans compte**. Lire ne demande jamais de s'identifier. |
| **Matériel** | Fonctionne sur un appareil de six ans, 2 Go de RAM, écran de 4,5 pouces. |
| **Réseau** | Fonctionne hors ligne — voir [`08-RESILIENCE.md`](08-RESILIENCE.md). |

**Le FALC mérite d'être souligné**, parce qu'il découle directement de la Charte :
l'article 7 bis fait du vote un devoir, et impose en retour au commun de **rendre
le vote votable**. Un texte qu'on ne peut pas comprendre est un texte auquel on ne
peut pas consentir. Une version FALC n'est donc pas une faveur faite à quelques-uns
— c'est la condition de validité du scrutin.

**Vérification, et non intention :** contrastes contrôlés automatiquement en
intégration continue ; parcours de vote testé au lecteur d'écran à chaque version ;
et un test avec des personnes concernées avant tout scrutin réel. **Si une
personne aveugle ne peut pas voter seule, la Régence n'est pas une démocratie.**

---

## 7. Universalité des appareils

Deux périmètres, à ne jamais confondre :

**La Régence est universelle.** L'application Table Ronde — délibérer, voter,
vérifier — fonctionne sur **tout** : Android ancien, iPhone, navigateur web,
matériel d'entrée de gamme, connexion faible. **Nul n'est exclu de la gouvernance
pour une raison de matériel.**

**SERF, le système, est ciblé.** Il s'installe sur une liste d'appareils où le
démarrage vérifié est réellement possible — condition de la promesse de sécurité.

Conséquence stratégique : **la Régence recrute, l'OS convertit.** On entre par
l'application, sur le téléphone qu'on a déjà. On migre quand on veut, ou jamais.

**Réserve à afficher honnêtement dans l'interface :** un bulletin déposé depuis un
appareil non vérifié offre de moindres garanties d'intégrité du client. La
vérification d'inclusion et le témoignage fonctionnent toujours ; l'équivalence,
non. L'interface le dit — sobrement, sans culpabiliser, sans faire de la peur un
argument de conversion.

---

## 8. Le sceau

L'identité appelle un **sceau**, non un logo. Un sceau signifie l'authentification
et l'acte officiel — exactement ce que fait SERF.

**Piste :** une couronne renversée devenue table. Le pouvoir descendu du souverain
vers l'assemblée ; le serf devenu régent, en une forme.

**Contraintes :** lisible à 24 px en icône de notification · fonctionnel en
monochrome · gravable · reconnaissable imprimé en noir et blanc sur une feuille
d'ancrage trimestrielle.

---

## 9. Les règles à ne pas enfreindre

*(Sans numéro d'ensemble : une liste qui annonce son propre compte devient fausse
dès qu'on l'allonge.)*

- **Aucun classement algorithmique, nulle part.** L'ordre est chronologique. Ce
  qui monte à l'ordre du jour a recueilli des parrainages, jamais des réactions.
- **Une seule notification système** : l'ouverture d'un scrutin.
- **Les quatre expressions ont le même poids visuel.** Aucune par défaut, aucune
  mise en avant, « Ignorer » jamais traité comme un renoncement.
- **Aucun résultat partiel pendant un scrutin ouvert.**
- **Aucune mesure d'engagement affichée** : ni vues, ni approbations, ni badges,
  ni séries. On ne construit pas un réseau social.
- **Le rouge `regence-600` ne porte jamais de texte.**
- **Aucune information portée par la seule couleur.**
- **« Vérifié » signifie *calculé sur votre appareil***, jamais *affirmé par un
  serveur*.
- **Version FALC par défaut**, texte intégral en second.
- **Le Registre se lit sans compte.** Lire ce que décide un commun n'exige jamais
  d'en faire partie.
- **Les échelons se présentent à plat**, jamais en arborescence : aucun échelon ne
  commande un autre.
- **Le hors-ligne n'est jamais une erreur.** Le système descend, il ne tombe pas.
  Rien en rouge, rien à réparer.
- **Aucune célébration, aucune récompense, aucune incitation au retour.**
- **Le silence d'un organe s'affiche comme un événement**, jamais comme un vide.
