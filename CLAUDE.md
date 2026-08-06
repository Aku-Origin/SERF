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

> **La cryptographie garantit. La procédure protège les Régents d'eux-mêmes. La Charte borne les deux.**

**Les cinq renversements (Diego, 3 août 2026)** — la boussole du projet, à quoi toute décision se
rapporte :

1. **La santé plutôt que la maladie · l'élévation plutôt que l'éducation.** Deux faces d'un seul
   principe : **financer l'amont, pas l'aval** (art. 23). L'éducation comble un manque, l'élévation
   augmente une capacité. Mécanisme d'appoint : le **vote par conviction**, où le financement
   s'accumule avec la durée du soutien et non son intensité.
2. **La souveraineté du peuple plutôt qu'une gouvernance de peu.** **Pondération quadratique**
   (art. 22) : le nombre de personnes pèse, pas les montants.
3. **La liberté plutôt que la soumission.** L'**Enceinte** — on n'interdit rien, on encercle.
4. **L'échelon proche plutôt que le sommet.** **Fédération à attestation mutuelle** (Titre VI bis) :
   les communautés cosignent les registres les unes des autres. La protection vient du voisinage,
   pas d'une autorité.
5. **La mémoire plutôt que l'amnésie.** Le **pourquoi inscrit avec le quoi** (art. 26 sexies) —
   motifs, objections, et ce qui a fait changer d'avis. Le Registre est écrit pour ceux qui devront
   reprendre le commun sans avoir connu personne.

**Une valeur sans mécanisme est une déclaration ; on n'en écrit pas.** Quand Diego formule un
renversement, lui trouver son mécanisme dans la même séance.

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
  y compris par les Régents. Un pouvoir qui doit voter son abdication ne l'a jamais votée.

---

## Décisions prises (ne pas rouvrir sans raison neuve)

| Sujet | Décision | Pourquoi |
|---|---|---|
| Socle | ~~LineageOS~~ → **lignée GrapheneOS**, appareils des partenariats constructeurs. **Rouvert le 3 août, à confirmer** | Les ROM non officielles échouent à l'attestation et ne reverrouillent pas le démarrage : pas de banques, pas d'adoption, aucun des trois piliers. Et le verrou Pixel tombe — partenariat Motorola annoncé en mars 2026 |
| Registrar du scrutin | **Éclaté en seuil : 3 émetteurs sur 5, jamais unique** (art. 10) | Une preuve mécanisée sur Belenios a établi que le secret du bulletin ne tient pas si l'organe d'éligibilité triche — alors que son rôle paraît étranger au scrutin. Faille latente chez nous jusqu'au 3 août |
| Paradoxe du client | **Les codes de retour** — feuille papier remise hors appareil, comparée après le vote | Seule défense qui contraigne un client compromis *sur-le-champ* : il ne peut afficher un code qu'il n'a jamais vu. **L'explication doit voyager avec le papier** — la faille de la mise en œuvre suisse est de l'expliquer en ligne |
| Portée des votes | **Résolu** : une association loi 1901 peut statutairement se lier à ses scrutins | Liberté statutaire quasi totale, et les statuts ont force de loi pour les membres. L'obligation devient opposable devant le juge civil |
| La Parole | **Aucun fil de réponses** · cartographier l'accord à la manière de Pol.is | vTaiwan l'a éprouvé : interdire la réplique supprime la dynamique d'affrontement. Le regroupement par proximité de position décrit, il ne hiérarchise pas — seule exception admise au refus de l'algorithmique |
| iOS | **Hors périmètre**, définitivement | Bootloader verrouillé sans voie de déblocage. Le promettre coûterait toute crédibilité au premier examen technique |
| Les trois statuts | **Porteur · Régent · Suspendu** (art. 7 quater) | Porter SERF n'est pas être Régent. **On ne coupe jamais l'appareil de quelqu'un** — la sanction touche le pouvoir, jamais l'usage |
| Âge et ancienneté | **16 ans révolus pour entrer, 12 mois de Porteur pour voter** → on vote au plus tôt à 17 ans (art. 8, 8 bis) | L'âge est *attesté par les parrains*, jamais prouvé par pièce : l'exiger imposerait l'état civil et anéantirait le jeton aveugle. Cible : **preuve d'âge anonyme** dès qu'un émetteur existe |
| L'année de présence | **Vaut pour tous, pas seulement les jeunes** | Bénéfice non cherché : c'est la meilleure défense anti-Sybil du texte. L'attaquant doit *entretenir* ses faux comptes un an — coûteux, et visible longtemps avant d'être décisif. Le vide de la première année est ce que couvre l'Amorçage |
| Article 12 | **L'inactivité ne coûte rien** — ne restent que la renonciation et la cascade de l'art. 11 | Déchoir pour inactivité obligeait à tracer qui a participé ; croisé au graphe public, ça rendait calculable la liste des non-votants. Et un droit qu'on perd faute d'en avoir usé est un droit conditionné — contraire à l'art. 7 bis |
| Protection de l'inexpérience | **Jusqu'à 21 ans : tout est visible, aucun jugement ne s'applique** (art. 12 bis) | Diego : *« il a aucune expérience donc il est innocent »*. On n'occulte rien — on retire le droit de condamner. **La part qu'il ne porte pas incombe à ses parrains**, ce qui règle le recrutement de masse sans quota |
| Récupération d'accès | **Acte public au Registre, délai annoncé, veto instantané du détenteur, deux demandes se gèlent** (art. 12 ter) | Le délai transforme une prise silencieuse en acte annoncé. L'appareil actif est le meilleur témoin : s'il ne répond plus de tout le délai, la clé est réputée perdue |
| Identité électorale | **Parrainage (3 parrains, 5/an max) + jeton d'éligibilité signé en aveugle** | Aucune dépendance à l'État, cohérent avec « par le dessous », constructible sans partenaire externe. Montée en charge lente : assumée |
| Ordre des jalons | **Le scrutin avant la ROM** | On teste le risque n°1 tôt. Ne dépend d'aucun matériel, d'aucun fork, d'aucune certification |
| Cryptographie du scrutin | Partir de **Belenios**, ne pas réimplémenter | Éprouvé et audité. Réimplémenter du vote homomorphe est la façon la plus sûre d'introduire une faille |
| Applications tierces | **L'Enceinte : encapsuler, jamais exclure** — toutes les apps tournent, dans un cloisonnement qui contrôle ce qu'elles voient | Le renoncement n'est pas une stratégie d'adoption. On ne demande à personne de perdre ses applications |
| Services Google | **Déprivilégiés** (application ordinaire, zéro privilège) — **et non microG** | microG usurpe la signature Google et exige des privilèges système : le composant le moins fiable obtient les droits les plus élevés, pour une compatibilité approximative. Le vrai code sans privilège fait mieux, sur les deux plans |
| Permissions | **Répondre par un vide ou un sous-ensemble, pas par un refus** | Un refus fait planter l'app ; l'utilisateur accuse SERF et part. Un carnet de contacts vide la laisse fonctionner et ne lui apprend rien |
| Allocation des ressources | Scrutins de **répartition** et de **conviction**, pondération **quadratique** | Le binaire ne sait pas exprimer une priorité. Le quadratique fait peser le nombre de personnes, non les montants — la souveraineté du peuple écrite en arithmétique |
| Couleur | `regence-600` = `#C62828`, **remplissage uniquement**. Texte accentué : `regence-400` (AA) ou `regence-300` (chemin de vote) | **Tout contraste s'écrit calculé, jamais estimé.** Les quatre valeurs publiées jusqu'au 3 août étaient fausses, et l'ancien `#A62121` (2.51:1 réel) échouait même au seuil de 3:1 des composants. Contrôle automatisé en CI, non négociable |
| Les deux corps | **Les Régents** (tous les porteurs) délibèrent · **la Table Ronde** (les Treize) décide | « Table Ronde » = les Treize, jamais l'ensemble des porteurs. Vocabulaire tranché le 3 août, ne pas régresser |
| Le mot « Assemblée » | **Supprimé, sans remplacement** (6 août). On écrit *les Régents* (toujours au pluriel) et *le commun* | Le mot est faux — personne ne s'assemble, on vote chacun depuis son appareil — et il réimporte la chambre parlementaire par la grammaire. Surtout : **un corps constitué se saisit, s'ignore, puis se vide sans que personne ne se sente visé ; des personnes, non** |
| « Régence provisoire » | **Devient l'Amorçage** (Titre IX) | Le mot « Régence » portait trois sens : la couche du produit, la période transitoire, et la racine de « Régent ». L'*Amorçage* dit ce que la chose est — un système démarre, il ne démarre pas indéfiniment — et meurt de lui-même |
| L'Amorçage n'est pas une attente | **C'est la période de recrutement** (Diego, 6 août) : les communautés qui se gouvernent déjà y entrent avec les leurs | *« Combien de groupes en France sont prêts à changer mais n'ont pas l'outil ? »* Change l'arithmétique de F0 : l'entrée par communauté constituée n'a rien à voir avec l'entrée individu par individu. **Reste à écrire comment on tient l'anti-Sybil dans ce mode** |
| Mémoire et sortie | **La mémoire l'emporte** (Diego, 6 août) : la sortie détruit le lien, pas ce qui fut inscrit comme acte du commun. **Écrit à l'art. 26 quinquies** | *« Je peux pas protéger une personne face aux générations futures. »* **Article 4 réécrit le 6 août**, avant l'adoption — il promettait d'« effacer toute trace », promesse intenable au Titre I non révisable. **Et l'objection n'est pas un résidu** (Diego : *« une objection peut être bonne, arrête de centrer dessus comme si c'était le problème »*) : ce qui reste au Registre est une **contribution**, pas une trace qu'on refuse d'effacer |
| Les deux paroles, dans les articles | **Le texte quitte le bulletin.** On argumente en délibération (7 j, signé, public) · on vote au scrutin (72 h, secret, **aucun texte joint**) — art. 14, 18, 26 bis | Trouvé par Diego : *« si le Régent est secret, il n'est donc jamais lié à son objection. »* La raison est arithmétique — trois textes signés en face de trois bulletins révèlent trois votes — et le style défait tout anonymat promis. **Corrige F9.** Prix assumé : on ne nuance plus au dernier moment, et le délai de 7 jours devient le seul moment où l'on pèse |
| Contenu illicite au Registre | **On scelle, on ne supprime pas** — et le scellé s'ouvre quand la chose est éprouvée | L'engagement-sans-contenu était pire que le mal : une accusation invérifiable, donc une censure munie d'une preuve d'honnêteté. Sous scellé, l'accusation reste falsifiable et le *pourquoi* est la chose elle-même. *Reste à définir ce qui ouvre : terme, scrutin, ou les deux* |
| Portée des votes | **Consultatif partout**, sauf deux scrutins contraignants : dissolution de la Table Ronde, et révision de la Charte | Un commun où tout se vote se paralyse ; un commun où rien ne se vote est un décor. Le peuple détient le pouvoir de renvoyer, pas celui de cogérer |
| Expressions de vote | **Oui · Non · À nuancer · Ignorer** | « À nuancer » est un **oui conditionnel qui porte ses arguments** — elle compte du côté de l'adhésion et crée une dette d'explication, elle ne bloque pas. « Ignorer » récuse la question — ce n'est pas l'abstention, qui est le silence |
| Le silence des Treize | **Obligation de consulter** 2×/an et avant tout engagement majeur (art. 35 bis) · **le silence coûte** un point (art. 38.4) · **saisine inconditionnelle** (art. 15 bis) | Sans ça, ne rien demander et n'écouter personne n'accumulait aucune défiance : le silence était la stratégie parfaite. La saisine inconditionnelle règle aussi le veto caché de l'art. 14 bis — l'insuffisance d'une version FALC se signale, elle ne s'oppose pas |
| Simuler avant de graver | **Un texte de gouvernance s'exécute, il ne se relit pas seulement** | La simulation du 5 août a sorti en une minute le défaut le plus grave du texte (F0) — que ni la lecture ni l'audit adversarial n'avaient vu : à 36 mois, 13 Régents pour 13 sièges |
| Le reset | Un « Ignorer » majoritaire = 1 point de défiance · **5 points sur 12 mois glissants ouvrent de plein droit le scrutin de dissolution** | C'est le câblage qui empêche « Ignorer » d'être un vote perdu : l'expression répétée arme le seul pouvoir réel des Régents |
| Composition des Treize | 12 Corps + **le Siège Ouvert** (tiré au sort parmi tous les Régents) · 6 élus / 6 tirés, mode alternant à chaque renouvellement | Aucun Corps ne s'installe ni ne se professionnalise. *Lecture de l'art. 29 à confirmer — deux autres restent ouvertes* |
| Codes de retour papier | **Écartés (Diego, 3 août)** — pousser le sans-confiance à la place | L'enveloppe s'ouvre en transit, la logistique est absurde, et une vérification post-hoc constate le dégât sans l'empêcher. Limite exacte à tenir : la cryptographie rend sans confiance tout ce qui suit le départ du bulletin, **jamais l'appareil lui-même** — c'est une frontière, pas un trou. Sur SERF elle est petite et auditable (démarrage vérifié, build reproductible, attestation) ; ailleurs on le dit |
| Financement | **Sujet non ouvert par Diego** — retiré des besoins | C'est moi qui l'avais listé. À ne pas remettre tant qu'il ne le soulève pas |
| Structure juridique | **Pas urgent, et pas une source de légitimité** | Elle sert à trois choses prosaïques : détenir de l'argent qui ne soit pas celui de Diego, éviter qu'il réponde personnellement, rendre un vote opposable entre membres. Utile quand il y aura de l'argent ou des membres |
| Audit | **Revue de sécurité par Fable en première passe.** Audit crypto externe plus tard — piste : Quarkslab (français, qualification ANSSI) | Décidé le 3 août |
| Le Registre | **Journal de transparence à arbre de Merkle — PAS une blockchain** | Une blockchain résout l'ordre entre inconnus sans identité ; on a déjà une identité. Notre problème est de détecter la *réécriture* — c'est de l'inviolabilité par la preuve, pas du consensus. Et la preuve d'enjeu pondère par la fortune : ce serait écrire l'inverse de l'art. 22 dans l'infrastructure |
| Sécurisé par chaque citoyen | **Chaque appareil est témoin** : conserve la dernière tête signée, exige la preuve de cohérence, échange avec les appareils croisés | C'est la seule défense contre la vue scindée. Et la triche produit sa propre preuve : deux têtes incohérentes signées par l'opérateur le condamnent sans qu'aucune autorité n'arbitre |
| Vote | **Droit et devoir**, sans sanction | Tenable seulement grâce aux quatre expressions : le silence n'est jamais nécessaire. Réciproquement le commun doit *rendre le vote votable* — sinon le devoir est un piège |
| Échelle | **Le dispositif est reproductible à tout échelon** — 7 membres minimum, procédure allégée en dessous de 500 | Imposer treize délégués à un village de quarante tue le dispositif par la procédure. `7-30` : *tous les Régents sont* la Table Ronde · `30-500` : cinq sièges · `500+` : les Treize |
| Fédération | **Les communautés cosignent les registres les unes des autres** | Falsifier un registre local exigerait de falsifier tous ceux qui l'attestent. La protection vient du voisinage — aucune autorité de contrôle nécessaire |
| Messagerie | **Matrix**, ne rien réinventer — et **jamais de fil algorithmique** | Protocole fédéré déjà retenu par l'État français. Un fil optimisé pour l'engagement produit l'inverse de l'élévation : ligne rouge de conception |
| Surfaces de l'OS | **~35 surfaces. On n'écrit que ce qui porte la thèse (9), on adapte (10), on adopte le reste (16)** | Réécrire une galerie photo ne rapproche d'aucun objectif et consomme les années qu'il faut à la Régence |
| Adopter ≠ maquiller | **On reprend un socle, on ne le laisse pas tel quel.** Les défauts, les retraits, les permissions, les parcours, le ton et l'accessibilité restent nôtres sur *chaque* surface | Ne pas réécrire n'est pas ne pas concevoir. Le compte « écrire/adapter/adopter » mesure des lignes de code, pas de l'intention. Levier dur : **l'accessibilité AA est un critère d'adoption** — une app qui échoue n'est pas adoptable, on l'adapte ou on la remplace |
| Adoption d'apps tierces | **Construire depuis les sources, épingler, relire les diffs, surveiller les rachats** | Simple Mobile Tools racheté en 2023 par un publicitaire → fork Fossify. Une app adoptée qui change de mains devient une porte dérobée — voie de compromission la plus probable du projet |
| Messagerie | **Le protocole de Signal, sans Signal** — Olm/Megolm sur Matrix | Signal exige un numéro de téléphone, donc l'état civil : ça annulerait le jeton aveugle. Réserve à dire : Matrix protège moins bien les métadonnées — recommander Signal/Briar en complément pour les usages à haut risque |
| Les deux paroles | **Publique (opposable, au Registre) et privée (sans trace) — visuellement irréconciliables** | Le risque de conception le plus grave du système. Croire chuchoter alors qu'on dépose au Registre : défaut bloquant au même titre qu'une faille crypto |
| Périmètres | **La Régence est universelle, l'OS est ciblé** (art. 7 ter) | L'app Table Ronde tourne sur tout — iPhone compris. Le système reste sur la liste où le démarrage vérifié est possible. *La Régence recrute, l'OS convertit* : personne n'a à changer de téléphone pour commencer à gouverner |
| Accessibilité | **WCAG 2.2 AAA sur le chemin de vote**, AA ailleurs · **version FALC obligatoire** (art. 14 bis) | Une proposition sans version intelligible ne peut être mise aux voix. Si voter est un devoir, le commun doit rendre le vote votable — un texte incompréhensible est un texte auquel on ne peut pas consentir |
| Matériel opaque | **Zéro confiance matérielle** : isoler le modem, interrupteurs physiques, tout rendre visible | On ne désactive pas un modem par logiciel, et un mouchard soudé ne se retire pas par du code. Le levier manquant est réglementaire — le prétendre résolu par du code serait se raconter une histoire |
| Résilience | **Aucune fonction essentielle ne suppose le réseau.** Quatre modes : plein, maillé, différé, papier | Les preuves de Merkle sont valides quel que soit le transport — clé USB, QR, LoRa. Un scrutin municipal entier pèse moins qu'une seconde de vidéo |
| Horloge et position | **Ne jamais dépendre du GPS.** L'ordre du Registre est intrinsèque | Le signal le plus facile à brouiller et à falsifier. Un horodatage est du confort, jamais une preuve |
| IEM | **Aucun logiciel n'en protège** — c'est de la physique. On protège les *données* : sauvegarde froide, dispersion, **ancrage papier trimestriel** (BnF, notaire, archives, presse) | 64 caractères imprimés suffisent à revérifier tout le Registre depuis une seule copie survivante, sans réseau ni autorité |
| Publication | **La visibilité est la protection** — 4 cercles : GitHub, Codeberg, Software Heritage, Radicle | Un dépôt confidentiel disparaît sans que personne s'en aperçoive. Software Heritage archive définitivement et n'est pas un hébergeur : on ne lui demande pas de retirer |
| Signature | **Père Sans-Ciel / Le Sans-Ciel** — une **charge transmissible**, non un masque (Charte art. 52) | Un masque disparaît avec son porteur ; une charge se transmet. Règle par le haut la continuité |
| Cloisonnement | **Une seule identité par dépôt** — règle d'hygiène, révisable avant le premier push | Un dépôt public, miroité et archivé ne se corrige pas : une mention lie deux identités pour toujours, dans tous les clones. Après le push, ça ne se défait plus |
| Questions à Diego | **L'outil à choix multiples est bienvenu** | Contrairement à l'espace Voyage : ici les arbitrages sont des bifurcations nettes, mieux servies par des options tranchées que par de la prose ouverte |

---

## Décidé avec Diego, pas encore écrit dans les documents techniques

Ces mécanismes sont **tranchés** ; il leur manque leur place. Ne pas les rouvrir, les écrire.

- **Code vocal à correspondance tournante.** Pour voter à la voix : « dis *Jul* pour oui, *Leon*
  pour non », correspondance régénérée toutes les trente secondes. Celui qui écoute n'apprend rien,
  un enregistrement ne prouve rien. **Délivrée à l'oreille, jamais à l'écran** ; reconnaissance
  vocale **entièrement locale** (art. 1). *Résout la coercition, pas le paradoxe du client* — un
  logiciel compromis tient les deux bouts. → `09-BRIEF-DESIGN`, `03-REGENCE`.
- **Signalement d'une conversation.** Toute discussion doit pouvoir être signalée — chantage,
  harcèlement — pour que la personne soit protégée et entendue. *Tension à trancher : un
  destinataire qui peut prouver ce qui a été dit détruit le déni plausible que le chiffrement
  offre. On ne peut pas avoir les deux.* → `10-SURFACES §4`.
- **Attestation : publier, jamais pondérer.** Chaque résultat porte sa composition (« 71 % des
  bulletins venaient d'appareils attestés »). Pondérer selon l'appareil ferait compter les pauvres
  moins que les autres — l'exact contraire de l'art. 22. → `06-REGISTRE`, `09-BRIEF-DESIGN`.
- **Mérite.** À concevoir. **Ligne rouge : le mérite ne pondère jamais un vote.** Il peut valoir
  reconnaissance et ressources, jamais pouvoir. Et on récompense qui trouve une faille *technique*,
  jamais qui dénonce une *personne* — sinon on paie la fabrication d'accusations.
- **Résumeur des « À nuancer », sur le modèle d'OASIS** (`D:\Claude\OASIS`) : *le SLM est une
  cognition louée, cosmétique ; la rigueur vient du harnais, pas du prompt.* Protocole de Diego :
  **trois exécutions par scrutin, convergence → ça passe, divergence → lecture humaine bloc par
  bloc.** Modèle, poids et consigne publics et versionnés au Registre ; déterministe ; ne remplace
  jamais les originaux ; l'arithmétique façon Pol.is passe avant le résumé. → `06-REGISTRE`,
  `09-BRIEF-DESIGN`.
- **Formats visés** : téléphone, tablette, montre (notifie et vérifie, ne porte pas la Parole),
  poste de travail — **un second projet, pas un portage**. Déjà écrit en `02-ARCHITECTURE §5`.

### Pistes ouvertes, non tranchées

- **« L'IA de l'autonomie »** (Diego, 4 août 2026) — application autonome, distribuable
  immédiatement : encyclopédie complète **hors ligne** (Kiwix) + SLM local en RAG, pour apprendre à
  penser par soi-même. C'est le renversement « l'élévation plutôt que l'éducation » en produit, et
  la chose la plus vite livrable du projet — elle ne dépend ni de l'OS, ni du scrutin, ni d'un
  partenaire. **Contradiction à résoudre avant d'écrire :** une IA qui pense à ta place ne t'apprend
  pas à penser. Donc — elle conduit à la source au lieu de répondre, n'affirme jamais sans montrer
  d'où ça vient, « je ne sais pas » est une sortie normale, et elle enseigne la méthode plus que le
  contenu. **Le seul bon indicateur : l'usage doit décroître** quand les gens savent chercher
  seuls. *Statut : proposée, ni cadrée ni décidée — projet distinct ou compagnon de SERF, à
  trancher.*
- **Le crédit social chinois est le contre-modèle à citer publiquement.** Même diagnostic que le
  nôtre — le collectif est à refonder — et mécanisme inverse : la confiance y est produite par le
  contrôle au lieu d'être éprouvée par le vote. C'est ce qui donne sa portée à la ligne rouge du
  mérite : **il ne pondère jamais un vote.** On nous fera la comparaison ; autant l'avoir déjà
  tranchée.

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

### Le rythme — règle apprise le 3 août 2026, à ses dépens

**Diego n'a pas lu le dépôt.** En une séance, j'ai produit cinq mille lignes sur douze sujets, dont
une Charte de cinquante-six articles écrite en son nom. Il s'est retrouvé avec « un article 12
mauvais sans savoir ce que c'est ». Son diagnostic : *« tu es parti dans tous les sens. »* Il a
raison, et c'est un défaut de méthode, pas de volume.

1. **Expliquer avant d'écrire.** Un mécanisme se présente en prose, on en discute, *ensuite* il entre
   dans un document. Jamais l'inverse. Un texte que Diego n'a pas compris n'engage rien — et une
   Charte qu'il n'a pas lue ne le représente pas.
2. **Un sujet à la fois, fini avant le suivant.** Pas six documents dans un tour.
3. **Ne jamais déduire un accord.** Le 3 août, « on reprend un OS et on le conçoit » a été transformé
   en validation du socle GrapheneOS. C'était faux. Une décision n'est actée que si Diego l'a
   énoncée sur ce point précis.
4. **Inline plutôt que workflow.** Un fan-out produit plus de texte plus vite : c'est la maladie, pas
   le remède. Todo séquentiel + agent de contrôle en fin d'étape.
5. **Agent de contrôle adversarial en fin d'étape.** Celui du 3 août a trouvé quatre contrastes faux,
   une contradiction entre les art. 24 et 32, et un tirage au sort non vérifiable. Rien de cela
   n'était visible de l'intérieur.

### Cadence

- **Un jalon à la fois** ; le jalon courant est le *goal*. Jalon 0 (fondations) → 1 (Régence hors
  OS) → 2 (ROM) → 3 (intégration). Voir **[ROADMAP.md](ROADMAP.md)**.
- **Dire ce qui est impossible, tôt et sans détour.** iOS, la force de loi, le noyau écrit de zéro.
  Les trois exclusions sont des choix de crédibilité et doivent figurer dans la communication
  publique, pas seulement en interne. Un projet de souveraineté meurt de la première promesse
  démentie.
- **Cite la source avant d'affirmer**, ou dis « je ne sais pas — à vérifier dans X ». Vaut
  particulièrement pour le juridique (Constitution, RGPD, DMA) et pour l'état de l'art du vote
  électronique.
- **Emprunter avant d'écrire.** Belenios pour le scrutin, Trillian pour le journal, la lignée
  GrapheneOS pour le socle, F-Droid pour le dépôt, UnifiedPush pour les notifications, Matrix pour
  la parole. Le temps d'ingénierie va à la Régence.
- **Faire contrôler.** Un agent de contrôle adversarial sur le dépôt, régulièrement. Celui du
  3 août a trouvé quatre contrastes faux, une contradiction entre l'art. 24 et l'art. 32 aux petits
  échelons, et un tirage au sort non vérifiable. Aucun de ces défauts n'aurait été vu de l'intérieur.
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
│   ├── 01-VISION.md           ← les cinq renversements, cibles, modèle économique
│   ├── 02-ARCHITECTURE.md     ← socle AOSP, l'Enceinte, risques structurants
│   ├── 03-REGENCE.md          ← gouvernance, scrutin, modèle de menace, résilience
│   ├── 04-DESIGN.md           ← couleurs, typographie, accessibilité
│   ├── 05-PUBLICATION.md      ← miroirs, clés, continuité, cloisonnement — PRIORITÉ
│   ├── 06-REGISTRE.md         ← transparence non falsifiable, témoignage citoyen
│   ├── 07-SUBSIDIARITE.md     ← les communautés fédérées — l'échelle d'un pays
│   ├── 08-RESILIENCE.md       ← gouverner sans réseau : maillage, LoRa, papier, IEM
│   ├── 09-BRIEF-DESIGN.md     ← brief autoportant : écrans, accessibilité, règles
│   ├── 10-SURFACES.md         ← les ~35 surfaces d'un OS : écrire / adapter / adopter
│   ├── 11-ETAT-DE-LART.md     ← recherche sourcée : vote, gouvernance, droit, socle
│   └── 12-FAILLES-OUVERTES.md ← les défauts connus et non corrigés — À LIRE
└── .claude/skills/
    ├── heure/                 ← relever l'heure, sans l'annoncer
    └── coherence/             ← renvois, compteurs, vocabulaire, avant chaque commit
```

**Distinction à tenir : `CLAUDE.md` dit *où on en est*, `JOURNAL.md` dit *comment on y est
arrivé*.** Le second contient les erreurs et les revirements — c'est ce qui évite à un
repreneur de refaire les mêmes débats. Ne jamais fondre l'un dans l'autre.

**À venir (jalon 1)** : `serf-registre`, `serf-scrutin`, `serf-identite`, `serf-forum`,
`serf-table-ronde`.

---

## Repères

- **[docs/12-FAILLES-OUVERTES.md](docs/12-FAILLES-OUVERTES.md)** — **à lire avant d'écrire du
  code.** Les défauts connus et non corrigés, par gravité.
- **[CHARTE.md](CHARTE.md)** — le texte qui borne tout le reste. Titre I non révisable ; **Titre IX**
  fait expirer la Régence.
- **[docs/03-REGENCE.md](docs/03-REGENCE.md)** — le cœur intellectuel : périmètre, corps électoral,
  secret/vérifiabilité/coercition, paradoxe du client, résilience.
- **[ROADMAP.md](ROADMAP.md) § Arbitrages ouverts** — ce qui reste à trancher : confirmation du
  socle, calibrage des seuils, financement, licence.
- **[docs/05-PUBLICATION.md](docs/05-PUBLICATION.md)** — les quatre cercles, l'ordre d'exécution du
  premier push, les clés, la continuité, le cloisonnement des identités.
- **[JOURNAL.md](JOURNAL.md)** — la chronologie et les revirements.
- Dépôt distant : `https://github.com/Aku-Origin/SERF.git` — **public, poussé**. Miroirs Codeberg,
  Software Heritage et Radicle : **pas encore en place**, priorité du jalon 0 bis.

**Références externes** : Belenios (vote vérifiable, Inria) · GrapheneOS (durcissement) ·
LineageOS (support matériel) · /e/OS et iodéOS (précédents français dégooglisés) · F-Droid ·
UnifiedPush · OpenStreetMap.

## Environnement

- Windows 11, shell PowerShell principal (Bash POSIX dispo).
- Dépôt git initialisé le 3 août 2026, branche `main`, signé `Père Sans-Ciel <sans-ciel@aku-origin.org>`.
  **Poussé sur GitHub.** *Le domaine `aku-origin.org` reste à enregistrer — il figure dans chaque
  commit et s'usurpe en attendant.*
- Console Python : forcer `PYTHONIOENCODING=utf-8` (cp932 bloque l'Unicode).
