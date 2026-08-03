# 12 — Failles ouvertes

> **À lire avant d'écrire la première ligne de code.**
>
> Registre des défauts **connus et non corrigés**. Issu d'un audit adversarial du
> dépôt, 3 août 2026. Rien ici n'est réglé ; ce qui l'a été figure au §4.
>
> Ce document existe parce que la doctrine du projet l'impose : *ne jamais
> annoncer une vérification non faite*. Un projet de gouvernance qui cacherait ses
> propres défauts n'aurait aucun titre à en demander la transparence à d'autres.

---

## 1. Bloquantes — à trancher **avant** `serf-registre` et `serf-scrutin`

Ces quatre-là coûtent très cher après la première ligne écrite.

### F1 — Le Registre ne peut pas porter les délais de la Charte

L'article 26 septies pose que **l'ordre du Registre est intrinsèque** et qu'« un
horodatage est une indication de confort, jamais une preuve ». Or toute la
procédure est en temps horloge : 7 jours de délibération, 72 h de scrutin, **30
jours de réponse motivée** (art. 35), compteur **glissant sur 12 mois** (art. 38),
36 mois de Régence (art. 55).

Le seul pouvoir réel de l'Assemblée — le point de défiance pour silence — dépend
donc d'une durée que la Charte déclare non probante. Comment prouve-t-on au
Registre que le délai de l'article 35 a expiré, si rien de temporel n'y fait
preuve ?

**À trancher :** exprimer les délais en **événements du Registre** (nombre
d'entrées, publications de têtes d'arbre, ancrages trimestriels), ou assumer une
horloge de confiance faible et l'écrire. **Pas les deux.**

### F2 — La liste des non-votants est dérivable

L'article 10 rend le graphe de parrainage public. L'article 12 fait perdre la
qualité de Régent après « une absence **totale de participation** pendant
vingt-quatre mois » — ce qui **exige de tenir, par personne, la trace de qui a
participé**.

Croisé avec un graphe d'identifiants publics, cela rend dérivable **la liste de
qui n'a pas voté**, dans un système où voter est un devoir (art. 7 bis). C'est
exactement l'instrument de pression sociale que l'article 24 prétend neutraliser.

La règle de méthode n°6 du projet — *« une décision de conception peut se
retourner en arme ; vérifier ce qu'on ouvre »* — énonce précisément ce risque, et
n'a pas été appliquée à l'article 12.

**À trancher :** supprimer la déchéance pour inactivité, ou remplacer la preuve de
participation par un jeton de renouvellement non lié au graphe public.

### F3 — Les codes de retour : la piste retenue est morte

`03-REGENCE.md §5` et `11-ETAT-DE-LART.md §1` proposent, comme voie unique pour
remettre les codes sans adresse postale, la **remise en main propre par les trois
parrains à l'admission**. Elle ne tient pas, pour deux raisons dirimantes :

1. **Chronologiquement impossible.** Un code de retour est calculé *par scrutin et
   par option*. À l'admission, aucun scrutin futur n'existe et aucune option n'est
   connue.
2. **Elle donnerait le vote aux parrains.** Quiconque détient la feuille peut
   vérifier après coup comment la personne a voté. Cela transformerait le parrain
   — statistiquement un proche, un employeur, un membre de la famille — en
   vérificateur de vote. C'est le contraire exact de l'objet de l'article 24.

**Et une tension non résolue s'y ajoute :** un code de retour **est** un accusé de
réception. L'article 24 en interdit tout « opposable à un tiers ». Le dépôt affirme
aujourd'hui les deux exigences.

**À trancher :** retrait anonyme en point physique, mécanisme de codes non
transférable (le code ne prouve rien à un tiers sans le secret du votant), ou
renoncement assumé aux codes de retour au profit de la seule vérification
hors-bande.

### F4 — Le tirage au sort n'est pas vérifiable

L'article 26 bis prévoit que « la graine est engagée publiquement avant le tirage
et révélée après ». **Un engagement-révélation à un seul engageant ne protège de
rien** : l'attaque n'est pas de changer la graine après coup, c'est d'en essayer
des milliers hors ligne et d'engager celle dont le résultat convient. La fonction
graine → gagnant est publique et calculable à l'avance.

Le dispositif ne garantit donc pas mieux qu'une nomination — ce que l'article
lui-même déclare inacceptable. **Sept des treize sièges en dépendent** (six tirés
plus le Siège Ouvert).

**À trancher :** graine multipartite (chaque Corps engage une part, combinaison
des révélations), dérivation depuis une tête d'arbre à une hauteur annoncée
d'avance, ou fonction aléatoire vérifiable à seuil. **Dans l'article, pas en
annexe.**

*Point ouvert connexe :* l'article 29 tire au sort « parmi les volontaires du
Corps ». **Rien ne définit comment on établit l'appartenance à un Corps.** Un
groupe coordonné peut se déclarer volontaire d'un Corps peu peuplé et faire
basculer une désignation.

---

## 2. Graves — à trancher avant tout scrutin réel

### F5 — Le compteur de défiance est neutralisable, par trois voies

- **L'effacement est calendaire.** Un scrutin de dissolution s'ouvre « de droit » à
  chaque demi-mandat (art. 39.3), et un scrutin rejeté remet le compteur à zéro
  (art. 41). La Table Ronde bénéficie donc d'une remise à zéro garantie tous les
  douze mois, indépendante de sa conduite — alors que le compteur est déjà
  glissant sur douze mois.
- **L'effacement s'achète.** Dix pour cent de Régents complaisants déclenchent un
  scrutin au moment le plus favorable, le perdent volontairement, effacent les
  points accumulés — et **bloquent six mois** la voie de la pétition pour
  l'opposition réelle. Le garde-fou anti-harcèlement se retourne contre ceux
  qu'il protège.
- **Le premier motif s'évite gratuitement.** Un point ne s'inscrit que si la
  proposition a été « portée » par la Table Ronde. Il suffit de la faire déposer
  par un Régent allié.

*S'y ajoute :* l'article 38(3) ne dit pas **qui constate l'identité d'objet** entre
trois avis écartés. Modifier l'intitulé remet le compte à zéro.

**À trancher :** dissocier la confirmation de demi-mandat du scrutin de
dissolution et n'attacher la remise à zéro qu'au second ; supprimer ou conditionner
la remise à zéro par pétition ; définir « portée » et « même objet ».

### F6 — La fédération atteste la cohérence, pas la véracité

`07-SUBSIDIARITE.md` et le `README` affirment que « falsifier un registre local
exigerait de falsifier tous ceux qui l'attestent ». **C'est surestimé.**

- Une cosignature atteste que la chaîne est en ajout seul. Elle ne dit rien de la
  réalité des délibérations inscrites. Une communauté malveillante écrit une
  histoire **fausse mais cohérente**, et l'obtient cosignée par des honnêtes. La
  fédération protège de la **réécriture**, jamais du **mensonge d'origine**.
- **Sybil au niveau des communautés.** Sept membres suffisent (art. 44 quater),
  sans autorisation (art. 44 bis). Vingt communautés fictives se cosignent entre
  elles et portent plus d'attestations qu'un village honnête. **Il n'existe aucune
  couche d'identité entre communautés**, et rien ne dit comment on choisit qui
  l'on cosigne ni comment un observateur pondère les attestations.
- **Sortie sans mémoire.** L'article 44 septies permet de partir « sans
  condition ». Une communauté prise en faute sort et se refédère ailleurs. Aucune
  révocation, aucune propagation d'alerte.

**Correction minimale immédiate :** cesser d'affirmer que la fédération empêche la
falsification. Elle rend la **réécriture** détectable. C'est déjà beaucoup, et
c'est autre chose.

### F7 — Aucune remédiation après fraude constatée

`06-REGISTRE.md` : « la triche produit sa propre preuve… aucune autorité n'a besoin
d'arbitrer ». Vrai **pour constater**. Mais aucun article ne dit qui annule un
scrutin faussé, qui le rejoue, ce qu'il advient du registre corrompu.

Et le compteur de défiance ne s'incrémente que pour mépris de l'Assemblée
(art. 38) — **jamais pour excès de compétence ni pour atteinte au Titre I**.

**Détection sans remédiation n'est pas un dispositif de sécurité.**

### F8 — Aux petits échelons, le vote doit être secret et public à la fois

De 7 à 30 membres, « l'assemblée **est** la Table Ronde » (art. 44 quinquies). Or
le vote des Régents est secret (art. 24) et celui des membres de la Table Ronde
est « nominatif et publié » (art. 32). **Le même corps est les deux.**

La contradiction est totale et frappe l'échelon que le projet présente comme le
plus important. **À trancher dans l'article 44 quinquies**, dans un sens ou dans
l'autre, explicitement.

### F9 — La parole publique est une donnée personnelle inaltérable

L'article 26 bis inscrit au Registre les objections et amendements. L'article 26
quinquies affirme qu'« aucune donnée personnelle n'y figure ».

Une objection est **du texte libre écrit par une personne** — opinion politique,
donc donnée sensible au sens de l'article 9 du RGPD. Le mécanisme d'engagement
cryptographique fonctionne pour un bulletin ; il ne fonctionne pas pour un
paragraphe d'argumentation, lisible et attribuable par son style. La doctrine CNIL
citée en `11 §3` **valide l'engagement cryptographique, pas l'inscription de texte
libre.**

**À trancher :** distinguer à l'article 26 bis ce qui est inscrit **en clair** (les
actes de l'organe) et **par engagement** (les expressions des personnes), et dire
ce qu'il advient d'une objection à la sortie de son auteur.

### F10 — Un seul Régent peut saturer l'Assemblée

Le seuil de mise à l'ordre du jour est « 1 % ou cent Régents, le plus bas des
deux » (art. 15) — soit **cinq personnes** au seuil de 500, **une seule** pendant
la Régence à faible effectif. Rien ne borne le **nombre de propositions
simultanées**.

Le devoir de vote devient impraticable, et l'article 16 se retourne : dix scrutins
ouverts, dix notifications, et le principe « un signal qui se répète cesse d'être
un signal » tombe de lui-même.

**À trancher :** plafond de scrutins simultanés, quota de dépôts par Régent.

### F11 — L'arithmétique anti-Sybil n'est écrite nulle part

L'article 9 plafonne à cinq parrainages par an, et la Charte affirme que cela
« borne mécaniquement la vitesse ». **C'est vrai contre un attaquant à effectif
fixe, faux contre un attaquant qui réinvestit** : chaque identité fictive admise
acquiert à son tour cinq droits de parrainage. La croissance est **exponentielle**.

La vraie défense est l'annulation en cascade (art. 11), qui suppose une
**détection** — laquelle repose sur un collège « sans aucun pouvoir de décision »
(art. 46) et sans moyens d'enquête définis.

**À écrire et à chiffrer**, avant de prétendre que le dispositif tient.

### F12 — Le vote par conviction n'a pas de procédure

La modalité « conviction » est définie comme un financement **continu, sans date de
clôture** (art. 21). L'article 14 impose que toute question passe par un scrutin
de **72 heures**. Une modalité sans clôture ne rentre pas dans une fenêtre fermée.

**Le mécanisme qui porte le premier renversement — financer l'amont — n'a pas de
procédure.**

### F13 — Deux autres lacunes de texte

- **Préséance art. 18 / art. 19.** Si « À nuancer » atteint un tiers *et*
  « Ignorer » la majorité absolue, les deux effets se déclenchent. Le texte ne dit
  pas lequel l'emporte.
- **Article 55 à faible effectif.** À 36 mois, la Régence prend fin « quel que soit
  l'effectif ». Avec quarante Régents on ne peut pourvoir treize sièges sur douze
  Corps, l'article 44 quinquies en prescrirait cinq, et le quorum de 20 % ferait
  décider la dissolution par huit personnes. **L'article prescrit une
  configuration impossible.**

### F14 — Le mode différé peut perdre un vote

`08-RESILIENCE.md` dit que le bulletin part « quand un canal réapparaît ». Rien ne
dit ce qu'il advient s'il réapparaît **après la clôture**. Et la notification
unique n'atteint pas un appareil hors ligne : une personne déconnectée pendant
toute la fenêtre n'apprend jamais qu'un scrutin a eu lieu — dans un système où
voter est un devoir.

### F15 — Une pile unique pour deux paroles qu'on veut irréconciliables

`10-SURFACES.md` compte comme un bénéfice « un seul protocole pour les deux
paroles, donc une seule pile à durcir ». `09-BRIEF-DESIGN.md` exige qu'elles soient
« visuellement irréconciliables » et qualifie leur confusion de défaut bloquant.
**Une pile unique est précisément l'architecture qui produit le glissement
redouté.** À arbitrer.

### F16 — Rien sur la modération ni sur le contenu illégal

La Parole interdit les fils, les métriques et le classement. **Rien ne dit qui
retire un contenu illégal d'un Registre en ajout seul, ni sous quelle procédure** —
alors que l'article 26 ter le rend techniquement irretirable et que la
responsabilité d'hébergeur s'appliquera.

---

## 3. Affirmations à étayer

Le projet s'interdit d'annoncer une vérification non faite. Ces quatre-là
l'enfreignent.

**La décision de socle repose sur des fermes de contenu.** Le renversement
LineageOS → lignée GrapheneOS s'appuie, pour ses prémisses factuelles — partenariat
Motorola de mars 2026, appareils fin 2026, « la plupart des banques de détail
européennes » — sur trois sites d'agrégation, aucun primaire. Seule la référence
technique de GrapheneOS est primaire, et elle n'établit qu'une possibilité, pas une
pratique. **À réétayer avant confirmation.**

**« Deux exigences sur trois » n'est pas un théorème identifié.** `03-REGENCE.md §4`
présente comme « un résultat établi de la recherche » le triangle secret /
vérifiabilité / coercition. Des résultats d'incompatibilité existent, mais pas sous
cette forme. **À citer précisément ou à reformuler.**

**Le dépôt légal et la date notariale sont affirmés sans réserve.** L'ancrage
papier (art. 26 octies) tient pour acquis que le dépôt légal BnF couvre une feuille
d'empreinte — alors qu'il porte sur les documents *mis à disposition d'un public* —
et que le dépôt chez un notaire confère date certaine, ce qui suppose des
conditions précises. **Une des quatre voies d'ancrage pourrait ne pas exister.**

**L'arbitrage juridique est déclaré résolu sur de la vulgarisation.** La portée
statutaire des votes est marquée « Résolu » dans `CLAUDE.md` et la `ROADMAP` sur la
foi de deux pages d'information générale — alors que `11 §3` écrit lui-même « à
vérifier avec un juriste, non par recherche documentaire ». *Doute de fond non
soulevé :* une clause statutaire déléguant la décision à un corps extérieur et
**pseudonyme** est d'une validité douteuse, et le pseudonymat interdit d'attribuer
la décision.

---

## 4. Corrigé le 3 août 2026

- **Les quatre contrastes annoncés étaient faux**, surestimés jusqu'à 27 %.
  L'ancien `regence-600` `#A62121` mesurait **2.51:1** contre 3.2 annoncé, et
  échouait même au seuil de 3:1 des composants d'interface — le jeton de l'action
  régalienne n'était pas conforme. Palette recalculée, `regence-600` = `#C62828`.
- **Quatre jetons échouaient au niveau AA sans que ce soit vu**, dont
  `etat-peril` : le jeton qui signale le danger était celui qui se voyait le moins.
- **Rouge institutionnel et rouge d'alarme étaient à 1.30:1** l'un de l'autre,
  indiscernables, et l'écart reposait sur la teinte — effacé chez une personne
  protanope. La distinction est désormais non chromatique.
- **Le `README` public annonçait encore LineageOS** après la révision du socle.
- **`CLAUDE.md` affirmait que rien n'était commité ni poussé**, sept commits après.
- Renvois faux : Titre VII pour Titre IX ; « trois renversements » pour cinq ;
  compétence `coherence` absente de la carte.

**Restent mécaniques et non faits :** cinq renvois d'articles périmés dans
`05-PUBLICATION.md` (art. 25→47, 27→49, 28→50, 29→51), deux dans la Charte
(art. 33 cite 41 pour 42 ; art. 31 cite 45 pour 47), `.gitignore` qui exclut les
clés publiques que `05` prescrit de publier, la fenêtre de scrutin donnée 48–72 h
dans `03` contre 72 h dans la Charte, et plusieurs compteurs de surfaces et
d'écrans devenus faux.

---

## 5. Ordre de traitement

1. **F1** et **F2** — choix de conception, très coûteux après `serf-registre`.
2. **F3** — retirer la piste « parrains » avant qu'elle ne se sédimente comme acquise.
3. **F4**, **F5**, **F8** — trois corrections d'articles, localisées.
4. **§3** — réétayer le socle sur sources primaires avant de confirmer la décision.
5. Le reste des corrections mécaniques du §4, en une passe `coherence`.
