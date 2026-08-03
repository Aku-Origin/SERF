# 04 — Système de design

> **Bleu nuit** pour la souveraineté. **Rouge** pour le prestige discret.
> **Blanc** pour la clarté. Trois couleurs, tenues avec discipline.

---

## 1. Principes

**La sobriété est l'argument.** SERF vend le contrôle et la sécurité. Toute
fioriture — dégradé, animation gratuite, glassmorphisme — travaille contre le
message. L'interface doit avoir la tenue d'un document officiel, pas d'une
application de divertissement.

**Le rouge est rare.** Il ne signale que trois choses : une action régalienne
(voter, signer, révoquer), un état critique (permission accordée, chiffrement
désactivé), un sceau institutionnel. S'il apparaît partout, il ne signifie plus
rien.

**Sombre par défaut.** Cohérent avec le récit de souveraineté, économe en OLED,
et c'est le mode dans lequel un OS de sécurité est attendu. Le thème clair est
un premier rôle, pas une réflexion après coup.

**Aucun élément décoratif ne doit ralentir l'information.** L'écran de vote est
le plus important du système : il doit être lisible en trois secondes, sous
stress, en marchant.

---

## 2. Palette

### Nuit — la couleur structurelle

| Jeton | Hex | Usage |
|---|---|---|
| `nuit-950` | `#05090F` | Fond de niveau le plus profond |
| `nuit-900` | `#0A1424` | **Fond principal (thème sombre)** |
| `nuit-800` | `#101F3A` | Surfaces élevées, cartes |
| `nuit-700` | `#182C50` | Bordures, séparateurs |
| `nuit-600` | `#223A66` | Bordures actives |
| `nuit-500` | `#2F4B80` | États désactivés |
| `nuit-400` | `#4C6BA0` | Texte tertiaire |
| `nuit-300` | `#7A93BD` | Texte secondaire (sombre) |
| `nuit-200` | `#B0C0D8` | Icônes |
| `nuit-100` | `#DCE4EF` | Fond principal (thème clair) |

### Régence — le rouge, scindé par usage

| Jeton | Hex | Usage | Contraste sur `nuit-900` |
|---|---|---|---|
| `regence-800` | `#6E1414` | Remplissage d'état pressé | — (fond) |
| `regence-700` | `#8C1A1A` | Remplissage survolé | — (fond) |
| `regence-600` | `#A62121` | **Remplissage principal** (boutons, sceaux) | 3.2:1 — **fonds uniquement** |
| `regence-400` | `#D65A5A` | **Texte et bordures accentués** | 6.1:1 ✓ AA |
| `regence-300` | `#E99494` | Texte accentué sur fond très sombre | 9.4:1 ✓ AAA |

> **Règle stricte :** `regence-600` ne porte **jamais** de texte directement sur
> fond nuit. Il sert de remplissage, avec du blanc dessus (contraste 6.4:1 ✓).
> Pour du texte rouge sur fond sombre, utiliser `regence-400` ou plus clair.

### Clarté — les neutres

| Jeton | Hex | Usage |
|---|---|---|
| `clarte-000` | `#FFFFFF` | Texte principal sur sombre, fond clair pur |
| `clarte-050` | `#F6F7F9` | Fond de page (thème clair) |
| `clarte-100` | `#E9ECF1` | Surfaces (thème clair) |

### Sémantique

| Jeton | Hex | Sens |
|---|---|---|
| `etat-scelle` | `#2E7D5B` | Chiffré, vérifié, protégé |
| `etat-alerte` | `#B8860B` | Attention, permission sensible |
| `etat-peril` | `#C13030` | Danger, fuite de données, non chiffré |

`etat-peril` et `regence-600` sont volontairement proches mais distincts : le
rouge institutionnel ne doit pas être confondu avec le rouge d'alarme. En cas de
doute d'un utilisateur, c'est un défaut de conception à corriger.

---

## 3. Typographie

**Marianne** est le choix évident pour le récit — c'est le caractère officiel de
l'État français, dessiné par Mathieu Réguer. **Vérifier sa licence avant tout
usage** : son emploi est cadré par la charte de l'État, et un projet privé n'y a
pas droit automatiquement.

Solution de repli sans risque : **Inter** (SIL OFL) pour l'interface, **Spectral**
(SIL OFL, dessiné pour l'écran par Production Type, fonderie française) pour les
textes de loi et les propositions — un empattement pour ce qui se lit longuement
et fait autorité, un linéaire pour ce qui s'utilise.

| Rôle | Fonte | Graisse | Taille | Interlignage |
|---|---|---|---|---|
| Titre régalien | Spectral | 600 | 32 | 1.2 |
| Titre de section | Inter | 600 | 22 | 1.3 |
| Corps d'interface | Inter | 400 | 16 | 1.5 |
| Texte de proposition | Spectral | 400 | 17 | 1.65 |
| Étiquette | Inter | 500 | 13 | 1.4 |
| Données techniques | JetBrains Mono | 400 | 14 | 1.5 |

Le texte des propositions soumises au vote se lit en Spectral, à 17 px et
interlignage généreux : c'est le seul endroit du système où l'on optimise pour la
lecture soutenue plutôt que pour le balayage. Un choix typographique qui porte
une intention politique — on veut que les gens *lisent* avant de voter.

---

## 4. Le sceau

L'identité visuelle appelle un **sceau**, pas un logo. Un sceau signifie
l'authentification, l'acte officiel, l'engagement — exactement ce que fait SERF.

Piste : une **couronne renversée devenue table** — le pouvoir descendu du
souverain vers l'assemblée. Le serf qui devient régent, en une forme.
Contrainte : doit rester lisible à 24 px (icône de notification) et en
monochrome.

---

## 5. Accessibilité — non négociable

Un OS qui exclut n'est pas souverain. Exigences minimales :

- Contraste WCAG AA (4.5:1 texte, 3:1 éléments d'interface) sur **tous** les
  thèmes, vérifié automatiquement en intégration continue
- Zones tactiles ≥ 48 dp
- Aucune information portée par la couleur seule — un vote « pour » ne se
  distingue jamais d'un « contre » par la seule teinte
- Fonctionnel à 200 % de taille de police
- L'écran de vote est intégralement navigable au lecteur d'écran, testé

Sur ce dernier point : si une personne aveugle ne peut pas voter seule, la
Régence n'est pas une démocratie.
