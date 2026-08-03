# CLAUDE.md — Espace de travail « SERF — Régence »

Bâtir **SERF** : un système d'exploitation mobile souverain, français, qui porte la **transmission
et la gouvernance d'un pays par le peuple**. L'utilisateur cesse d'être le serf des géants de la
Tech ; il devient le **Régent** qui gouverne sa machine — puis, de proche en proche, le commun qu'il
habite.

**Cadence en deux temps (décidée avec Diego, 3 août 2026) :** *prouver le scrutin d'abord, la ROM
ensuite.* On tient **un jalon à la fois** — chaque jalon finit avant le suivant.

---

## Comprendre SERF — l'architecture (la tenir entière)

SERF est un **fork AOSP** surmonté de deux couches originales. La souveraineté ne se joue pas sur la
réécriture d'un pilote GPU — elle se joue sur la couche où se prennent les décisions.

```
LA RÉGENCE          Table Ronde · Registre · Scrutin       ← original SERF, LE produit
SERVICES SOUVERAINS Identité · Sync · Cartes · Push        ← à construire
APPLICATIONS SYSTÈME Lanceur · Contacts · Messages         ← à habiller
FRAMEWORK ANDROID   API, ART, PackageManager               ← AOSP, durci
HAL + PILOTES       blobs SoC propriétaires                ← hérité, non modifiable
NOYAU LINUX         GPLv2 — modifications publiables       ← hérité, durci
```

- **L'effort porte sur les deux couches du haut.** Le reste est de l'intégration. La dégooglisation
  est un marché déjà bien occupé (/e/OS, iodéOS, GrapheneOS, CalyxOS) : s'y épuiser ne justifierait
  pas l'existence du projet.
- **La Régence est l'unique différenciateur.** Aucun OS au monde ne donne à ses porteurs un pouvoir
  formel sur ses propres règles. C'est aussi le risque n°1 — donc ce qu'on teste en premier.
- Détail : **[docs/02-ARCHITECTURE.md](docs/02-ARCHITECTURE.md)** · gouvernance et modèle de menace :
  **[docs/03-REGENCE.md](docs/03-REGENCE.md)** · texte fondateur : **[CHARTE.md](CHARTE.md)**.

**Le réalisme de l'ambition.** La finalité est la gouvernance d'un pays par le peuple. Le chemin
n'est pas la proclamation, c'est la **subsidiarité montante** : gouverner d'abord de petites choses
réelles, et bien — le dépôt d'applications, la trésorerie, la feuille de route — puis la Charte,
puis des collectivités et coopératives qui s'y adossent par convention, puis un poids civique
constitué par la pratique. Chaque échelon n'est franchi qu'après avoir été tenu à l'échelon
précédent. Une Table Ronde qui a arbitré correctement cinq ans de décisions a une autorité que nulle
proclamation ne confère. **On reprend par le dessous, doucement.**

---

## La doctrine — qui décide quoi (décidée avec Diego, 3 août 2026)

> **La cryptographie garantit. La procédure protège l'assemblée d'elle-même. La Charte borne les deux.**

**Les trois renversements (Diego, 3 août 2026)** — la boussole du projet, à quoi toute décision se
rapporte :

1. **Payer la santé plutôt que la maladie.** Un système qui ne rémunère que la réparation produit
   mécaniquement ce qu'il faut réparer. Traduit dans le commun : maintenance, durcissement,
   accessibilité et documentation passent avant le spectaculaire (Charte, art. 18 quater), et le
   **vote par conviction** fait prévaloir le soutien durable sur l'élan passager.
2. **La souveraineté du peuple plutôt qu'une gouvernance de peu.** Traduit en arithmétique : la
   **pondération quadratique** fait peser le nombre de personnes et non les montants. Mille électeurs
   à une part l'emportent sur un seul à mille parts.
3. **La liberté plutôt que la soumission.** Traduit en architecture : l'**Enceinte** — on n'interdit
   rien, on encercle. L'utilisateur garde ses applications *et* reprend ce qu'elles voient.

Ces trois lignes ne sont pas de l'ornement : chacune a déjà un mécanisme qui la porte. **Une valeur
sans mécanisme est une déclaration ; on n'en écrit pas.**

- **Le secret et la vérifiabilité sont cryptographiques, jamais déclaratifs.** Une garantie qui
  repose sur la bonne foi d'un opérateur n'est pas une garantie. Signature aveugle pour séparer
  l'admission du bulletin ; chiffrement homomorphe pour dépouiller sans déchiffrer ; clé de
  dépouillement éclatée entre plusieurs autorités.
- **La friction délibérative est un dispositif de sécurité, pas une lenteur.** 7 jours minimum entre
  la mise à l'ordre du jour et le vote, non abrégeables même à l'unanimité. C'est la seule défense
  connue contre le vote d'humeur et contre la mobilisation-éclair d'un groupe organisé.
- **Une notification système, une seule, à l'ouverture du scrutin.** Un signal qui se répète cesse
  d'être un signal. Ce canal est la seule fonction que *seule* l'intégration OS rend possible : une
  notification qu'aucun algorithme ne peut enterrer.
- **Le socle intangible est le dispositif anti-capture.** Sans Titre I, un adversaire n'a plus besoin
  de casser un chiffrement : il lui suffit de gagner une élection.
- **La Régence expire.** Dévolution automatique par seuils, terme absolu à 36 mois, non prorogeable
  y compris par l'Assemblée. Un pouvoir qui doit voter son abdication ne l'a jamais votée.

---

## Décisions prises (ne pas rouvrir sans raison neuve)

| Sujet | Décision | Pourquoi |
|---|---|---|
| Socle | Fork AOSP, base **LineageOS**, durcissement inspiré GrapheneOS | Le support matériel est le coût le plus lourd et le moins gratifiant ; GrapheneOS enfermerait sur Pixel, matériel américain — contradiction frontale avec le récit |
| iOS | **Hors périmètre**, définitivement | Bootloader verrouillé sans voie de déblocage. Le promettre coûterait toute crédibilité au premier examen technique |
| Identité électorale | **Parrainage (3 parrains, 5/an max) + jeton d'éligibilité signé en aveugle** | Aucune dépendance à l'État, cohérent avec « par le dessous », constructible sans partenaire externe. Montée en charge lente : assumée |
| Ordre des jalons | **Le scrutin avant la ROM** | On teste le risque n°1 tôt. Ne dépend d'aucun matériel, d'aucun fork, d'aucune certification |
| Cryptographie du scrutin | Partir de **Belenios**, ne pas réimplémenter | Éprouvé et audité. Réimplémenter du vote homomorphe est la façon la plus sûre d'introduire une faille |
| Applications tierces | **L'Enceinte : encapsuler, jamais exclure** — toutes les apps tournent, dans un cloisonnement qui contrôle ce qu'elles voient | Le renoncement n'est pas une stratégie d'adoption. On ne demande à personne de perdre ses applications |
| Services Google | **Déprivilégiés** (application ordinaire, zéro privilège) — **et non microG** | microG usurpe la signature Google et exige des privilèges système : le composant le moins fiable obtient les droits les plus élevés, pour une compatibilité approximative. Le vrai code sans privilège fait mieux, sur les deux plans |
| Permissions | **Répondre par un vide ou un sous-ensemble, pas par un refus** | Un refus fait planter l'app ; l'utilisateur accuse SERF et part. Un carnet de contacts vide la laisse fonctionner et ne lui apprend rien |
| Allocation des ressources | Scrutins de **répartition** et de **conviction**, pondération **quadratique** | Le binaire ne sait pas exprimer une priorité. Le quadratique fait peser le nombre de personnes, non les montants — la souveraineté du peuple écrite en arithmétique |
| Couleur | `regence-600` en **remplissage uniquement**, jamais en texte sur fond nuit | 3.2:1 — échoue WCAG AA. Texte accentué : `regence-400` ou plus clair |
| Les deux corps | **Les Régents** (tous les porteurs) délibèrent · **la Table Ronde** (les Treize) décide | « Table Ronde » = les Treize, jamais l'assemblée. Vocabulaire tranché le 3 août, ne pas régresser |
| Portée des votes | **Consultatif partout**, sauf deux scrutins contraignants : dissolution de la Table Ronde, et révision de la Charte | Une assemblée qui tranche tout se paralyse ; une assemblée qui ne peut rien est un décor. Le peuple détient le pouvoir de renvoyer, pas celui de cogérer |
| Expressions de vote | **Oui · Non · À nuancer · Ignorer** | « À nuancer » renvoie en délibération. « Ignorer » récuse la question — ce n'est pas l'abstention, qui est le silence |
| Le reset | Un « Ignorer » majoritaire = 1 point de défiance · **5 points sur 12 mois glissants ouvrent de plein droit le scrutin de dissolution** | C'est le câblage qui empêche « Ignorer » d'être un vote perdu : l'expression répétée arme le seul pouvoir réel de l'Assemblée |
| Composition des Treize | 12 Corps + **le Siège Ouvert** (tiré au sort parmi tous les Régents) · 6 élus / 6 tirés, mode alternant à chaque renouvellement | Aucun Corps ne s'installe ni ne se professionnalise. *Lecture de l'art. 29 à confirmer — deux autres restent ouvertes* |
| Publication | **La visibilité est la protection** — 4 cercles : GitHub, Codeberg, Software Heritage, Radicle | Un dépôt confidentiel disparaît sans que personne s'en aperçoive. Software Heritage archive définitivement et n'est pas un hébergeur : on ne lui demande pas de retirer |
| Signature | **Père Sans-Ciel / Le Sans-Ciel** — une **charge transmissible**, non un masque (Charte art. 52) | Un masque disparaît avec son porteur ; une charge se transmet. Règle par le haut la continuité |
| Cloisonnement | **Une seule identité par dépôt** — règle d'hygiène, révisable avant le premier push | Un dépôt public, miroité et archivé ne se corrige pas : une mention lie deux identités pour toujours, dans tous les clones. Après le push, ça ne se défait plus |
| Questions à Diego | **L'outil à choix multiples est bienvenu** | Contrairement à l'espace Voyage : ici les arbitrages sont des bifurcations nettes, mieux servies par des options tranchées que par de la prose ouverte |

---

## Invariants (toujours tenir)

- **Le Titre I de la Charte engage dès le premier jour**, avant tout corps électoral, avant tout
  code. Pas de collecte non consentie, pas de porte dérobée, vérifiabilité, droit de sortie, droit
  de bifurcation, accessibilité. Une version qui y contrevient n'est pas SERF.
- **Ne jamais prétendre que les votes SERF ont force de loi.** C'est faux aujourd'hui, et le laisser
  croire offrirait une disqualification gratuite à quiconque veut abattre le projet. La force vient
  de la pratique accumulée et des conventions signées — c'est plus lent et infiniment plus solide.
- **Rien ne se distribue qui ne soit reproductible à l'octet près.** Sans build reproductible, le
  code source publié ne prouve strictement rien.
- **Aucune image publiée par une signature unique.** Trois détenteurs de clés distincts minimum. On
  veut qu'il faille un complot, pas une trahison.
- **Aucun secret de signature dans le dépôt.** Les clés sont la racine de confiance de SERF ; leur
  fuite permet de forger une image que les appareils accepteraient au verified boot. `.gitignore`
  les couvre — vérifier avant chaque commit.
- **L'accessibilité de l'écran de vote n'est pas négociable.** Si une personne aveugle ne peut pas
  voter seule, la Régence n'est pas une démocratie.
- **Aucune information portée par la couleur seule.** Un « pour » ne se distingue jamais d'un
  « contre » par la seule teinte.
- **Écrire en français**, registre sobre et documentaire. L'interface doit avoir la tenue d'un
  document officiel, pas d'une application de divertissement — la sobriété *est* l'argument.

---

## Façon de travailler

- **Un jalon à la fois** ; le jalon courant est le *goal*. Jalon 0 (fondations) → 1 (Régence hors
  OS) → 2 (ROM) → 3 (intégration). Voir **[ROADMAP.md](ROADMAP.md)**.
- **Dire ce qui est impossible, tôt et sans détour.** iOS, la force de loi, le noyau écrit de zéro.
  Les trois exclusions sont des choix de crédibilité et doivent figurer dans la communication
  publique, pas seulement en interne. Un projet de souveraineté meurt de la première promesse
  démentie.
- **Cite la source avant d'affirmer**, ou dis « je ne sais pas — à vérifier dans X ». Vaut
  particulièrement pour le juridique (Constitution, RGPD, DMA) et pour l'état de l'art du vote
  électronique.
- **Emprunter avant d'écrire.** Belenios pour le scrutin, LineageOS pour le matériel, F-Droid pour
  le dépôt, UnifiedPush pour les notifications. Le temps d'ingénierie va à la Régence.
- **Audit externe avant tout usage réel du scrutin.** Non négociable. Un vote cassé découvert en
  production tue le projet définitivement — la confiance ne se reconstruit pas.
- **Todo :** une tâche = un objectif de jalon.

### Conventions de l'espace

- **Tutoyer Diego.**
- **Relever l'heure avant toute écriture datée** — compétence `heure`, sans jamais l'annoncer ni la
  commenter. La date du contexte de session est celle de l'ouverture et ne se met pas à jour.
- **Tenir le journal.** Une entrée par séance dans [`JOURNAL.md`](JOURNAL.md), la plus récente en
  haut : ce qui a été décidé, **pourquoi**, et ce qu'on a changé d'avis. Les erreurs s'y écrivent —
  c'est leur seul intérêt.
- **Signer `Le Sans-Ciel`** les documents fondateurs et les messages de commit.
- **Ne jamais écrire dans le dépôt** : une autre identité du porteur, une adresse personnelle, une
  clé privée. Ces trois-là sont irréversibles une fois poussées et miroitées.
- **Publier avant de développer.** Tant que les miroirs ne sont pas en place, tout travail est un
  point unique de défaillance posé sur une seule machine.

### Les règles de méthode

1. **Toute garantie doit tenir sans supposer la bonne foi de qui que ce soit** — y compris la nôtre.
   Si la protection repose sur « l'éditeur ne le fera pas », ce n'est pas une protection, c'est une
   promesse.
2. **Le paradoxe du client n'a pas de solution parfaite.** Si l'éditeur écrit le client de vote, il
   contrôle le scrutin — aucune cryptographie n'y remédie. On empile des défenses partielles (build
   reproductible, verified boot, signature multipartite, transparence des binaires, vérification
   hors-bande) et **on le dit publiquement**. Prétendre l'inverse détruirait la confiance à la
   première contestation sérieuse.
3. **La coercition est irréductible en vote à distance.** L'isoloir n'a pas d'équivalent numérique.
   Re-vote pendant toute la fenêtre et absence d'accusé opposable atténuent — n'éliminent pas.
4. **Un quorum général transforme l'abstention en veto.** D'où : pas de quorum sur l'ordinaire,
   quorum réel sur le lourd.
5. **Ne jamais annoncer une vérification non faite.** Ni un contraste calculé, ni un build testé, ni
   un texte de loi lu. Dire ce qui a été mesuré, et ce qui reste à mesurer.
6. **Une décision de conception peut se retourner en arme.** Le graphe de parrainage est public
   parce que c'est le seul rempart anti-Sybil — il ne doit donc porter *aucune* information de vote.
   Vérifier ce qu'on ouvre, pas seulement ce qu'on protège.

---

## Carte de l'espace de travail

```
SERF/
├── CLAUDE.md                  ← ce fichier — l'ÉTAT du projet + la méthode
├── JOURNAL.md                 ← la CHRONOLOGIE — décisions datées, avec leur pourquoi
├── CHARTE.md                  ← le texte fondateur (v0.2, non adopté) — Titre I intangible
├── README.md                  ← porte d'entrée publique
├── ROADMAP.md                 ← jalons + arbitrages ouverts
├── docs/
│   ├── 01-VISION.md           ← les trois renversements, cibles, modèle économique
│   ├── 02-ARCHITECTURE.md     ← socle AOSP, l'Enceinte, risques structurants
│   ├── 03-REGENCE.md          ← gouvernance, scrutin, modèle de menace, résilience
│   ├── 04-DESIGN.md           ← couleurs, typographie, accessibilité
│   └── 05-PUBLICATION.md      ← miroirs, clés, continuité, cloisonnement — PRIORITÉ
└── .claude/skills/heure/      ← relever l'heure, sans l'annoncer
```

**Distinction à tenir : `CLAUDE.md` dit *où on en est*, `JOURNAL.md` dit *comment on y est
arrivé*.** Le second contient les erreurs et les revirements — c'est ce qui évite à un
repreneur de refaire les mêmes débats. Ne jamais fondre l'un dans l'autre.

**À venir (jalon 1)** : `serf-registre`, `serf-scrutin`, `serf-identite`, `serf-forum`,
`serf-table-ronde`.

---

## Repères

- **[CHARTE.md](CHARTE.md)** — le texte qui borne tout le reste. Titre I non révisable ; Titre VII
  fait expirer la Régence.
- **[docs/03-REGENCE.md](docs/03-REGENCE.md)** — le cœur intellectuel : périmètre, corps électoral,
  secret/vérifiabilité/coercition, paradoxe du client, résilience.
- **[ROADMAP.md](ROADMAP.md) § Arbitrages ouverts** — ce qui reste à trancher : portée statutaire
  des votes, microG, financement, licence.
- **[docs/05-PUBLICATION.md](docs/05-PUBLICATION.md)** — les quatre cercles, l'ordre d'exécution du
  premier push, les clés, la continuité, le cloisonnement des identités.
- **[JOURNAL.md](JOURNAL.md)** — la chronologie et les revirements.
- Dépôt distant : `https://github.com/Aku-Origin/SERF.git` — **vide à ce jour**, aucun commit poussé.
- Mémoire projet : `C:\Users\dcssa\.claude\projects\D--Claude-SERF\memory\` (`MEMORY.md` = index).

**Références externes** : Belenios (vote vérifiable, Inria) · GrapheneOS (durcissement) ·
LineageOS (support matériel) · /e/OS et iodéOS (précédents français dégooglisés) · F-Droid ·
UnifiedPush · OpenStreetMap.

## Environnement

- Windows 11, shell PowerShell principal (Bash POSIX dispo).
- Dépôt git initialisé le 3 août 2026, branche `main`. **Rien n'est encore commité ni poussé.**
- Console Python : forcer `PYTHONIOENCODING=utf-8` (cp932 bloque l'Unicode).
