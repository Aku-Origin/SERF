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

### 5.1 — L'ordre du jour

Ce qui se décide en ce moment. Chronologique, jamais classé par « pertinence ».
Chaque entrée porte : son titre en langue claire, son étape (délibération /
scrutin ouvert / clos), le temps restant, et rien d'autre.

**Aucun compteur de participation visible pendant un scrutin ouvert.** Afficher
« 68 % de Oui » pendant le vote fabrique un effet de ralliement. Les résultats
n'apparaissent qu'à la clôture.

### 5.2 — La proposition *(l'écran le plus important)*

En haut : **la version FALC** — Facile À Lire et à Comprendre. Phrases courtes,
un sujet par phrase, aucun jargon. **C'est la version par défaut**, pas une
option d'accessibilité reléguée.

En dessous, dépliables : le texte intégral, les objections déposées, les
amendements, et **ce qui a fait changer d'avis** — le cœur de la mémoire du
projet.

### 5.3 — Les quatre expressions

C'est le geste central du système. Quatre boutons, jamais trois, jamais cinq :

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

### 5.4 — Ce que j'ai dit

L'historique personnel de ses expressions. Chacune accompagnée de **sa preuve
d'inclusion, vérifiable hors ligne**.

> Le sceau **« vérifié »** doit signifier ce qu'il dit. Partout ailleurs, un tel
> indicateur veut dire *« un serveur nous l'a affirmé »*. Ici il veut dire
> **« votre appareil a fait le calcul »**. C'est la seule promesse d'interface que
> le système n'a pas le droit de rompre — et elle doit être visuellement
> distincte de toute autre coche de l'écosystème logiciel.

### 5.5 — Ce qu'ils ont fait *(l'écran qui n'existe nulle part)*

La redevabilité des Treize. Pour chaque membre : ses **votes nominatifs**, ses
présences, ses réponses motivées. Pour l'organe : le **compteur de défiance**, son
état sur douze mois glissants, et chaque point avec son motif.

**Les silences y figurent.** Un délai de réponse expiré est affiché comme un
événement, pas comme une absence de ligne.

C'est l'écran que nulle institution n'offre aujourd'hui. Il doit être aussi soigné
que l'écran de vote.

### 5.6 — Le tableau de souveraineté

Ce que chaque application a tenté : permissions demandées, serveurs contactés,
volume transmis, heure. La surveillance des surveillants.

### 5.7 — L'Enceinte

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

## 9. Les dix règles à ne pas enfreindre

1. Aucun classement algorithmique, nulle part. L'ordre est chronologique.
2. Une seule notification système : l'ouverture d'un scrutin.
3. Les quatre expressions ont le même poids visuel.
4. Aucun résultat partiel pendant un scrutin ouvert.
5. Le rouge `regence-600` ne porte jamais de texte.
6. Aucune information portée par la seule couleur.
7. « Vérifié » signifie *calculé sur votre appareil*, jamais *affirmé par un
   serveur*.
8. Version FALC par défaut, texte intégral en second.
9. Aucune célébration, aucune récompense, aucune incitation au retour.
10. Le silence d'un organe est affiché comme un événement, jamais comme un vide.
