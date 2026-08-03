# 03 — La Régence : gouvernance, Table Ronde et scrutin

> C'est ici que se joue l'originalité de SERF — et sa difficulté.
> Un OS dégooglisé, d'autres l'ont fait. Un OS qui se gouverne lui-même, personne.

---

## 1. Que gouverne-t-on, exactement ?

Question préalable à toute autre. Trois périmètres possibles, de plus en plus
ambitieux, et de moins en moins crédibles.

### A. Gouverner le commun SERF — **recommandé**

Le corps électoral décide de ce qui lui appartient réellement :

- **La Charte** — les droits inaliénables de l'utilisateur, opposables à
  l'éditeur lui-même
- **La feuille de route** — quelles fonctions sont développées, dans quel ordre
- **Les admissions au dépôt** — quelles applications entrent dans le magasin
  officiel, lesquelles en sont exclues et pourquoi
- **La trésorerie** — allocation des dons et subventions, rémunération des
  contributeurs
- **Les partenariats** — accepte-t-on un constructeur, un financement, un État ?
- **Les révocations** — destitution d'un mainteneur, retrait d'une clé de
  signature

Ce pouvoir est **réel, immédiat, et juridiquement propre**. Une association loi
1901 ou une société à mission peut statutairement se lier à ses propres votes.
C'est bien plus radical qu'il n'y paraît : aucune plateforme numérique au monde
n'accorde cela à ses utilisateurs.

### B. Consultation civique

SERF sert d'infrastructure de consultation pour des collectivités, associations,
syndicats, copropriétés, coopératives — qui *choisissent* de s'y lier. Le vote
tire sa force du contrat qui l'adosse, pas de l'OS. Extension naturelle de (A),
et modèle économique plausible.

### C. Le poids civique — l'horizon, non le point de départ

La finalité du projet est la transmission et la gouvernance d'un pays par le
peuple. Il faut être exact sur l'état du droit : la Constitution confie le vote
de la loi au Parlement (art. 24) et au référendum encadré (art. 11 et 89). Un
scrutin émis par SERF **n'a aujourd'hui aucune valeur juridique**.

Ce n'est pas un renoncement, c'est un point de départ. Ce qui est immédiatement
possible :

- **Outiller** le RIP (référendum d'initiative partagée) et les pétitions
  officielles, en abaissant d'un ordre de grandeur le coût de mobilisation d'un
  seuil de signatures.
- **Constituer une pratique** — un corps électoral rodé, un registre de décisions
  vérifiable, des années de scrutins réguliers et incontestés. Un instrument dont
  la fiabilité est démontrée par l'usage n'a plus le même statut dans un débat
  public qu'une proposition théorique.
- **Faire adopter par convention** — collectivités, coopératives, syndicats,
  partis. Chaque adoption est un précédent, et les précédents s'additionnent.

> **Position retenue : (A) est le cœur et le premier échelon, (B) l'extension
> naturelle, (C) la direction.** Ce qui est écarté n'est pas l'ambition — c'est
> la **proclamation**. Annoncer une force de loi qu'on n'a pas offrirait une
> disqualification gratuite à quiconque veut abattre le projet dans sa première
> année. On monte échelon par échelon, et chacun est tenu avant que le suivant
> soit revendiqué.

---

## 2. Le piège du « vote instantané »

L'intuition fondatrice — *« la Table Ronde propose un changement ? Vote poussé
instantanément à tous les porteurs de l'OS »* — est le bon geste, mais elle
contient trois pièges connus.

**La fatigue.** Une notification par décision, sur un système utilisé par des
centaines de milliers de personnes, produit en quelques semaines un réflexe de
rejet. La participation s'effondre, et le pouvoir échoit mécaniquement à la
minorité qui vote encore.

**Le plébiscite.** Voter *immédiatement* sur un texte que l'on découvre, c'est
voter sur son titre. Sans délibération préalable, un scrutin instantané ne mesure
pas une volonté collective : il mesure une réaction émotionnelle et la qualité de
la formulation. C'est exactement le mécanisme qu'exploitent les campagnes de
manipulation.

**La capture par mobilisation.** Qui mobilise vite gagne. Un groupe organisé de
2 000 personnes bat structurellement 200 000 utilisateurs distraits.

**Correctif de conception — la friction délibérative.** Le cycle proposé :

```
  PROPOSITION      →  DÉLIBÉRATION      →  MISE À L'ORDRE   →  SCRUTIN
  seuil de           7 jours minimum,      annonce ferme       48–72 h
  parrainages        amendements,          de la date          fenêtre
  atteint            objections tracées                        de vote
```

La notification système n'intervient qu'à l'ouverture du scrutin — un seul
signal, attendu, jamais noyé. Le caractère « intégré à l'OS » sert alors sa vraie
fonction : **une notification qu'aucun algorithme ne peut enterrer**, ce qui est
précisément ce que les réseaux sociaux rendent impossible.

---

## 3. Le corps électoral : qui a le droit de voter

Le problème dur : **une personne, une voix**, sans registre d'identité
centralisé — car un tel registre trahirait la promesse de vie privée.

| Modèle | Résistance au Sybil | Vie privée | Friction |
|---|---|---|---|
| Un appareil = une voix | **Nulle** — inutilisable | Excellente | Nulle |
| Compte + vérification téléphone | Faible (cartes prépayées) | Médiocre | Faible |
| Toile de confiance (parrainage) | Bonne | Bonne | Élevée |
| eID étatique (France Identité) | Excellente | **Dépendance à l'État** | Moyenne |
| Preuve de personnalité biométrique | Bonne | Très mauvaise | Élevée |

Aucune ligne n'est satisfaisante seule.

### Décision : parrainage + jeton signé en aveugle *(3 août 2026)*

**L'admission** s'opère par toile de confiance : trois électeurs déjà inscrits
présentent le candidat et répondent de son existence distincte. Chacun ne peut
parrainer que cinq admissions par an — ce plafond borne mécaniquement la vitesse
à laquelle un acteur hostile peut peupler l'assemblée d'identités fictives, et
rend l'entreprise visible avant d'être décisive. Le graphe des parrainages est
public : c'est le seul rempart, il doit être auditable.

**Le scrutin** en est séparé cryptographiquement. L'électeur admis obtient un
**jeton d'éligibilité signé en aveugle** : l'organe émetteur certifie « cette
personne a droit à une voix » sans jamais voir quel bulletin elle déposera ;
l'urne vérifie la signature sans savoir qui l'a obtenue. Le graphe de parrainage
est public, mais il ne porte **aucune** information de vote. La séparation ne
repose pas sur la bonne foi d'un opérateur — elle est mathématique.

**Pourquoi pas l'eID étatique**, malgré sa résistance au Sybil supérieure : elle
crée une dépendance à l'État, contradictoire avec un projet qui se construit par
le bas ; et son intégration bute de toute façon sur l'attestation Play Integrity
(cf. [architecture §6](02-ARCHITECTURE.md)), donc elle n'est même pas
prototypable aujourd'hui. Elle reste ouverte comme **second collège optionnel**
si la Table Ronde le décide un jour.

**Le coût assumé** : la montée en charge est lente. C'est cohérent — « par le
dessous, doucement » n'est pas une figure de style, c'est le régime de croissance
choisi. Un corps électoral qui grandit par confiance interpersonnelle est plus
lent et beaucoup plus difficile à noyauter qu'un corps qui grandit par
inscription libre.

---

## 4. Secret, vérifiabilité, coercition

Trois exigences dont deux seulement peuvent être fortes simultanément — c'est un
résultat établi de la recherche en vote électronique, pas une limite d'ingénierie.

**Secret** — nul ne doit pouvoir lier un bulletin à un électeur.
**Vérifiabilité** — chacun doit pouvoir vérifier que sa voix est comptée, et que
le total est juste.
**Résistance à la coercition** — nul ne doit pouvoir *prouver* à un tiers comment
il a voté (sinon : achat de voix, pression familiale ou patronale).

L'état de l'art (Helios, Belenios, ElectionGuard) : chiffrement homomorphe +
bulletin board public. Chaque bulletin est chiffré, publié, vérifiable
individuellement ; le total est calculé sans jamais déchiffrer un bulletin
individuel ; la clé de déchiffrement est éclatée entre plusieurs autorités qui
doivent coopérer.

La coercition reste **le point faible irréductible du vote à distance**. Un
téléphone se vote sous le regard de quelqu'un. Atténuations partielles :
re-vote autorisé pendant toute la fenêtre (seul le dernier compte), et jamais
d'accusé de réception opposable. Cela n'élimine pas le risque — l'isoloir n'a pas
d'équivalent numérique.

---

## 5. Le paradoxe du client — le problème central

> **Si l'éditeur de l'OS écrit le client de vote, il contrôle le scrutin.**

Toute la cryptographie du monde est vaine si le logiciel qui affiche « votre vote
POUR a bien été enregistré » a en réalité chiffré CONTRE. C'est la faille que ni
Helios ni ElectionGuard ne résolvent — ils supposent un client honnête.

SERF aggrave le problème : l'urne est *dans* le système. Mais SERF est aussi le
seul projet en position de l'attaquer sérieusement, parce qu'il contrôle la pile
entière.

Défenses cumulables, aucune suffisante seule :

- **Builds reproductibles** — n'importe qui recompile les sources et obtient
  l'octet près la même image. Sans cela, le code source publié ne prouve rien.
- **Verified boot** — l'appareil refuse de démarrer une image non signée. Rend le
  contournement local détectable.
- **Signature multi-parties des versions** — aucune personne, aucune entité seule
  ne peut publier une image. Il faut un complot, pas une trahison.
- **Transparence des binaires** — journal public et infalsifiable de chaque image
  publiée, à la manière du Certificate Transparency. Une image ciblée sur un seul
  utilisateur devient impossible à cacher.
- **Vérification hors-bande** — possibilité de vérifier son bulletin depuis un
  appareil tiers, sur un serveur indépendant.

**À dire publiquement, sans détour :** la Régence ne peut pas offrir les
garanties du vote papier en isoloir. Elle offre autre chose — une gouvernance
continue, vérifiable, à coût de participation quasi nul, sur un objet qui
n'était jusqu'ici gouverné par personne. Prétendre l'inverse détruirait la
confiance à la première contestation sérieuse.

---

## 6. Constitution : ce qui ne se vote pas

Une démocratie sans droits inaliénables est une tyrannie de la majorité. Certains
articles de la Charte doivent être hors d'atteinte du scrutin ordinaire —
révisables uniquement à majorité qualifiée très élevée, voire jamais :

- Aucune télémétrie non consentie, quel qu'en soit le prétexte
- Aucune porte dérobée, quelle qu'en soit l'autorité demandeuse
- Le code source reste publiable et vérifiable
- Nul ne peut être privé du droit de désinstaller, de bifurquer, de partir avec
  ses données

Sans ce socle, un vote suffirait à démanteler la raison d'être du projet — et un
adversaire n'aurait qu'à gagner une élection au lieu de casser un chiffrement.

---

## 7. Légitimité par le bas, et résilience

La Régence ne se décrète pas légitime — elle le devient. La stratégie est la
**subsidiarité montante** : gouverner d'abord de petites choses réelles, et bien.

```
  le dépôt d'applications  →  la trésorerie  →  la feuille de route
        →  la Charte  →  des collectivités et coopératives s'y adossent
              →  un poids civique constitué par la pratique
```

Chaque échelon n'est franchi qu'après avoir été tenu à l'échelon précédent. Une
Table Ronde qui a arbitré correctement cinq ans de décisions techniques et
budgétaires a une autorité que nulle proclamation ne confère.

**Conséquence architecturale : le commun doit survivre à sa structure porteuse.**
Un projet qui monte par le bas ne peut pas dépendre d'une entité unique — une
association se dissout, une société se rachète, un dirigeant se retourne.

- **Registre répliqué.** Le journal des propositions et décisions est signé et
  miroité par plusieurs entités indépendantes, de juridictions différentes. Sa
  disparition doit exiger une action coordonnée, pas une lettre recommandée.
- **Droit de bifurquer, inscrit dans la Charte.** Le corps électoral peut à tout
  moment emporter le registre, les clés publiques et le code vers une autre
  structure. C'est la garantie ultime contre la capture — et c'est aussi ce qui
  discipline l'éditeur.
- **Aucun point unique de défaillance juridique.** Ni les clés de signature, ni
  l'infrastructure de mise à jour, ni le registre ne doivent tenir à une seule
  personne morale.
- **Aucun séquestre.** Pas de registre central d'identité, pas de copie des clés,
  métadonnées réduites au strict nécessaire. Ce qui n'est pas collecté ne peut
  être ni saisi, ni fuité, ni retourné.

Ce dernier point relève de l'ingénierie de vie privée standard — celle de Signal,
de Tor, de GrapheneOS. Il protège l'utilisateur contre la collecte de masse et
l'abus, ce qui est l'objet même du projet.

---

## 8. Composants à construire

| Composant | Rôle | Couche |
|---|---|---|
| `serf-registre` | Journal public et vérifiable des propositions et décisions | Service |
| `serf-scrutin` | Chiffrement des bulletins, dépôt, dépouillement homomorphe | Service |
| `serf-identite` | Jeton d'éligibilité par signature aveugle | Service |
| `serf-forum` | Délibération, amendements, parrainages | Application |
| `serf-table-ronde` | Interface citoyenne : ordre du jour, vote, résultats | Application système |
| `RegenceNotifier` | Canal de notification système non désactivable par un tiers | Framework |
