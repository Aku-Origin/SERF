# 04 — Système de design

> **Pour concevoir des écrans, lire plutôt [`09-BRIEF-DESIGN.md`](09-BRIEF-DESIGN.md)** —
> brief autoportant, avec les écrans, le niveau d'accessibilité visé et les dix
> règles à ne pas enfreindre. Le présent document est la référence des jetons.

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
| `nuit-400` | `#4C6BA0` | Bordures actives, éléments **non textuels** — **3.44:1**, échoue AA en texte |
| `nuit-350` | `#96AACB` | Texte tertiaire — **7.83:1** ✓ AAA |
| `nuit-300` | `#7A93BD` | Texte secondaire, contextes **AA** — **5.92:1** ✓ AA · ✗ AAA |
| `nuit-200` | `#B0C0D8` | Icônes, texte secondaire sur chemin de vote — **9.99:1** ✓ AAA |
| `nuit-100` | `#DCE4EF` | Fond principal (thème clair) — **14.39:1** en texte sur nuit |

*Corrigé le 3 août : `nuit-400` était donné comme « texte tertiaire » alors qu'il
échoue au seuil AA de 4.5:1. Jeton `nuit-350` introduit pour ce rôle.*

### Régence — le rouge, scindé par usage

> **Palette corrigée le 3 août 2026.** Les quatre contrastes précédemment annoncés
> étaient faux — surestimés jusqu'à 27 %, et l'ancien `regence-600` (`#A62121`,
> **2.51:1** réel contre 3.2 annoncé) échouait même au seuil de 3:1 des composants
> d'interface. Toutes les valeurs ci-dessous sont **calculées**, formule WCAG 2.x
> sur `nuit-900` `#0A1424`.

| Jeton | Hex | Usage | Contraste mesuré |
|---|---|---|---|
| `regence-800` | `#7A1C1C` | Remplissage pressé | — (fond) |
| `regence-700` | `#A32222` | Remplissage survolé | — (fond) |
| `regence-600` | `#C62828` | **Remplissage principal** (boutons, sceaux) | **3.28:1** ✓ composants · blanc dessus **5.62:1** ✓ AA |
| `regence-400` | `#D65A5A` | Texte accentué — contextes **AA** | **4.80:1** ✓ AA · ✗ AAA |
| `regence-300` | `#E99494` | Texte accentué — **obligatoire sur le chemin de vote** | **8.02:1** ✓ AAA |

> **Règles strictes.**
> `regence-600` ne porte **jamais** de texte sur fond nuit : c'est un remplissage,
> avec du blanc dessus. Pour du texte rouge sur fond sombre, `regence-400`
> minimum — et `regence-300` dès qu'on est sur le chemin de vote, où la cible est
> 7:1.
>
> **Le double contrainte du remplissage est étroite :** le fond doit atteindre 3:1
> contre la nuit *et* porter du blanc à 4.5:1. Ces deux exigences tirent en sens
> inverse. La fenêtre utile va d'environ `#C62828` à `#D23B3B` — au-delà, le blanc
> décroche. Tout changement de ce jeton se recalcule.

### Clarté — les neutres

| Jeton | Hex | Usage |
|---|---|---|
| `clarte-000` | `#FFFFFF` | Texte principal sur sombre, fond clair pur |
| `clarte-050` | `#F6F7F9` | Fond de page (thème clair) |
| `clarte-100` | `#E9ECF1` | Surfaces (thème clair) |

### Sémantique

| Jeton | Hex | Sens | Contraste mesuré |
|---|---|---|---|
| `etat-scelle` | `#3E9E75` | Chiffré, vérifié, protégé | **5.58:1** ✓ AA |
| `etat-alerte` | `#D4A017` | Attention, permission sensible | **7.77:1** ✓ AAA |
| `etat-peril` | `#E05252` | Danger, fuite, non chiffré | **4.83:1** ✓ AA |

*Corrigés le 3 août : les valeurs précédentes (`#2E7D5B` 3.69:1, `#B8860B`,
`#C13030` 3.28:1) échouaient toutes au niveau AA en texte. **Le jeton qui signale
le danger était celui qui se voyait le moins.***

> **Le rouge institutionnel et le rouge d'alarme ne se distinguent pas par la
> teinte, et il faut cesser de prétendre le contraire.** Les anciennes valeurs
> étaient à **1.30:1** l'une de l'autre — indiscernables, et l'écart reposait
> presque entièrement sur la teinte, donc effacé chez une personne protanope ou
> deutéranope.
>
> La distinction ne peut donc pas être chromatique. **Un état de péril porte
> toujours un pictogramme et un libellé** ; la couleur ne fait que le renforcer.
> C'est l'application de la règle générale — aucune information par la seule
> couleur — au cas où elle était le plus tentante à contourner.

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
souverain vers les Régents. Le serf qui devient régent, en une forme.
Contrainte : doit rester lisible à 24 px (icône de notification) et en
monochrome.

---

## 5. Accessibilité — non négociable

Un OS qui exclut n'est pas souverain. Exigences minimales :

- **WCAG 2.2 AAA sur le chemin de vote** (7:1 texte), **AA partout ailleurs**
  (4.5:1 texte, 3:1 éléments d'interface), sur **tous** les thèmes. Cible
  détaillée en [`09-BRIEF-DESIGN.md §6`](09-BRIEF-DESIGN.md)
- **Vérification automatique en intégration continue, non négociable.** Les
  quatre contrastes annoncés dans ce document jusqu'au 3 août 2026 étaient tous
  faux : ils avaient été estimés, pas calculés. Un contrôle automatisé les aurait
  arrêtés le jour même
- Zones tactiles ≥ 48 dp
- Aucune information portée par la couleur seule — un vote « pour » ne se
  distingue jamais d'un « contre » par la seule teinte
- Fonctionnel à 200 % de taille de police
- L'écran de vote est intégralement navigable au lecteur d'écran, testé

Sur ce dernier point : si une personne aveugle ne peut pas voter seule, la
Régence n'est pas une démocratie.
