# Journal de bord

> Chronologie du projet. Ce que l'on a décidé, quand, et **pourquoi** — y compris
> ce qu'on a changé d'avis.
>
> Le journal n'est pas l'état du projet : cet état vit dans [`CLAUDE.md`](CLAUDE.md)
> et dans la [Charte](CHARTE.md). Le journal dit comment on y est arrivé. C'est ce
> qui permettra à quelqu'un qui n'a connu personne de reprendre le dossier sans
> refaire les mêmes débats.
>
> **Convention** : une entrée par séance de travail, la plus récente en haut.
> Horodatage en heure de Paris. On y écrit aussi les erreurs.

---

## 2026-08-06, 16h — Le mot « Assemblée » tombe, et la mémoire l'emporte sur la sortie

### Le compteur de défiance ne protégeait pas ceux qu'il devait protéger

Diego avait posé trois questions : *combien de fois la Table Ronde est-elle
dissoute, combien de fois est-elle freinée, combien de fois le peuple perd-il ?*
La simulation a répondu, et la réponse est mauvaise.

Sous le quorum de 20 % de l'article 25, **zéro dissolution — jamais**. Pas
rarement : jamais. Et comme l'article 41 traite un échec au quorum comme un rejet,
le compteur retombe à zéro à chaque tentative et la pétition se bloque six mois.
**Essayer coûte plus cher que ne rien faire. L'abstention absout.** La stratégie
optimale d'une Table Ronde qui veut durer devient : maintenir la participation
basse, avec des scrutins fréquents, techniques et ennuyeux.

Diego a demandé d'où sortaient les 12 % de participation. **De moi** — ce sont des
paramètres inventés, comme les « 3 » et « 8 points par an » de conduite. Il fallait
le dire. Ce qui ne dépend pas de mes chiffres, en revanche : le mur à 20 % est
écrit dans l'article 25, et l'effacement est écrit dans l'article 41. Le vrai
défaut est là — **on a écrit un dispositif dont la fonction s'inverse selon un
paramètre qu'on ne connaît pas.** Un garde-fou qui a besoin qu'on devine juste n'en
est pas un.

Trois corrections proposées, non tranchées : un échec au quorum n'efface rien · le
quorum décroît quand le compteur monte · la confirmation de demi-mandat n'est pas
une dissolution. Diego reprend l'architecture des organes — la correction attendra
qu'elle soit posée.

### « Assemblée » : le mot était faux, pas seulement vieux

Diego : *« L'assemblée ? On est dans l'ancien monde ? Puisque tout le peuple mature
a le devoir de vote, c'est débile. »*

Il a doublement raison. *Assembler*, c'est se réunir — or personne ne se réunit :
on vote chacun depuis son appareil, étalé sur 72 heures. L'article 13 avouait
lui-même le problème en précisant « ni présidence, ni bureau, ni siège permanent »,
c'est-à-dire en retirant tout le contenu du mot qu'il venait d'employer.

**Le mot disparaît sans remplacement.** Pas de nouveau nom de corps — sinon on
recrée la même chose sous une étiquette neuve. On écrit *les Régents*, toujours au
pluriel, et *le commun* pour ce qu'ils gouvernent.

Le motif n'est pas esthétique : **un corps constitué peut être saisi, puis ignoré,
puis vidé de sa substance sans que personne ne se sente visé. Des personnes, non.**
C'est écrit dans le nouvel article 13, pour que la règle survive à ceux qui l'ont
posée.

Vingt-sept occurrences reprises dans huit fichiers. J'en avais d'abord raté la
moitié : mon `grep` était sensible à la casse et laissait passer tous les
« assemblée » en minuscule — dont *« l'assemblée est la Table Ronde »* de
l'article 44 quinquies, le plus important. C'est Diego qui l'a vu. La règle du
contrôle de cohérence a été corrigée en conséquence.

### « Régence provisoire » devient **l'Amorçage**

Le mot « Régence » portait trois sens : la couche du produit, la période
transitoire du Titre IX, et la racine de « Régent ». D'où la confusion de Diego :
*« SERF est bien un système d'exploitation Régence français, pourquoi
provisoire ? »*

*Amorçage* dit ce que la chose est. Un système démarre ; le commun aussi. Et une
séquence de démarrage qui ne finit jamais est un plantage — le mot meurt de
lui-même, ce qui est exactement le propos de l'article 55.

### L'Amorçage n'est pas une attente

Je posais les trois fondateurs comme tenant la maison faute de corps électoral.
Diego : *« Sauf si la première année est de l'accumulation — combien de groupes en
France sont prêts à changer mais n'ont pas l'outil ? »*

C'est une période de **recrutement**, pas d'attente. Et le vivier existe :
associations, coopératives, communes, collectifs, syndicats — des gens qui se
gouvernent déjà, mal outillés. **Ça change l'arithmétique de F0** : le calcul des
treize Régents à trente-six mois suppose une entrée individu par individu. Une
association de deux cents membres en apporte deux cents d'un coup.

Reste à écrire comment l'anti-Sybil tient dans ce mode. Une association qui existe
depuis quinze ans se fabrique moins facilement que cinq faux comptes — mais ça
s'écrit, ça ne s'espère pas.

### On scelle, on ne supprime pas

J'avais proposé, pour le contenu illicite, de garder l'engagement cryptographique
et de détruire le contenu. Diego a démoli la proposition : *« Comment tu peux être
sûr que c'est intact si t'en effaces la moitié ? C'est comme dire que l'eau est
verte sans dire que j'ai mis du colorant. »*

Il a raison, et c'est pire que la perte du *pourquoi*. Une empreinte prouve qu'une
chose existait, jamais ce qu'elle était. Marquer « cette entrée était illégale »
puis détruire l'entrée, c'est produire **une accusation que plus personne ne pourra
jamais contrôler** — donc une censure munie d'une preuve d'honnêteté. Règle de
méthode n°6 : une décision de conception qui se retourne en arme.

Retenu : **le contenu est scellé, non supprimé** — chiffré, présent, prouvablement
inchangé, mais non diffusé ; clé éclatée entre cosignataires ; tout descellement
inscrit au Registre. Et Diego ajoute que le scellé s'ouvre **quand la chose est
éprouvée** : c'est un délai, pas un tombeau. Reste à définir ce qui l'ouvre.

### La mémoire l'emporte sur la sortie

*« Je peux pas protéger une personne face aux générations futures. »*

Décision prise. Elle a une conséquence lourde que je dois écrire ici pour qu'elle
ne se perde pas : **l'article 4 promet aujourd'hui l'inverse** — « effacer toute
trace le concernant », sans condition. Il est au **Titre I, non révisable**. La
Charte n'étant pas encore adoptée, la fenêtre pour le corriger est ouverte ; elle
se referme définitivement à l'article 56.

Ce qu'il faudra y mettre : la sortie détruit le lien entre la personne et ce
qu'elle a inscrit ; ce qui fut inscrit comme acte du commun demeure. Et **ça se dit
à l'entrée**. Quelqu'un qui écrit une objection publique doit savoir, au moment où
il l'écrit, qu'elle lui survivra — d'autant qu'un texte libre reste reconnaissable
au style et que « non rattachable » sera toujours une fiction.

### Le droit, et où il s'arrête

J'ai présenté la LCEN et le DSA comme des contraintes de conception. Diego a coupé :
*« Je refais un gouvernement d'en dessous pour pallier au liberticide actuel, on
s'en tape. »* Il a un conseil juridique à lui, qu'il saisira quand il le décidera.

Ce que j'ai maintenu, en une phrase et sans y revenir : le risque n'est pas que le
droit invalide l'idée, c'est qu'une **personne** en réponde devant un tribunal —
la manière la moins chère de faire tomber le projet sans jamais discuter de l'idée.
Dit une fois, c'est son appel.

### Les modalités de scrutin se réduisent

Diego, sur les quatre modalités de l'article 21 : *« C'est les mêmes, y'a juste une
question de fréquence. »* Exact pour répartition et conviction, et presque pour la
préférentielle : l'expression est identique — répartir son soutien entre des
options — seule la **résolution** change, exclusive ou proportionnelle, ponctuelle
ou continue. Condorcet n'est pas une manière de voter mais de dépouiller.

L'article passera de quatre modalités à deux. Bénéfice non cherché : **ça règle
F12.** La conviction n'était sans procédure que parce qu'on en avait fait une
modalité étrangère à la fenêtre de 72 heures.

### L'horodatage : Diego résout F1

*« L'horodatage du partage sur tous les appareils, tu ne falsifies rien, c'est
enregistré. »* Le témoignage réparti **est** l'horloge : l'agrégat des attestations
« j'ai vu cette tête » borne l'existence d'un état sans qu'aucune horloge
individuelle ait à être juste. Les délais s'exprimeront en attestations.

Une nuance que je lui dois : l'OS aide mais ne prouve pas — un appareil seul reste
compromettable, c'est le paradoxe du client. **C'est la répartition qui prouve.**
Et la garantie est faible tant que les témoins sont peu nombreux — soit exactement
pendant l'Amorçage.

### Méthode

Diego : *« Fais une liste pour qu'on se perde pas, le sujet est complexe et aura
tendance à m'emmener de tous les côtés. »* Quinze entrées tenues à jour à chaque
tour. Le reproche du 3 août — *« tu es parti dans tous les sens »* — vaut aussi
dans l'autre sens : c'est à moi de tenir le fil quand la conversation part, et
d'aller au bout de chaque question ouverte.

---

## 2026-08-05, 14h — Bloc 3a, et la simulation qui casse le Titre IX

### « À nuancer » n'était pas ce que j'avais écrit

Correction de Diego : *« Nuancer va donner des arguments, c'est pas refaire, c'est
oui cependant ou avec tel et tel chose. »*

J'en avais fait un renvoi en délibération — un blocage procédural, avec deux
renvois maximum. C'est une adhésion sous réserve. Elle compte du côté du oui, et
elle **porte du texte** : les réserves, les arguments, ce qui devrait être pris en
compte. Ces écrits appellent une réponse publique (art. 35), et le silence coûte
un point de défiance.

**On ne bloque pas, on oblige à entendre.** Une nuance n'arrête pas une décision ;
elle crée une dette d'explication à la charge de celui qui décide. C'est plus fin
que ma version, et ça donne enfin sa raison d'être au résumeur — ce sont ces
textes-là qu'il faudra rendre lisibles quand il y en aura dix mille.

### Le trou qu'ouvrait « les Treize décident »

Diego : *« Les décisions et applications seront prises par la Table Ronde, que le
peuple adhère ou pas. Ceci dit, si le peuple n'adhère pas, la table se fait à un
moment dissoute. »*

C'est cohérent — une démocratie de révocation. Mais tout le poids de l'édifice
repose alors sur le compteur de défiance, ce qui rend la faille F5 bien plus
grave qu'elle ne paraissait. Et un trou apparaissait, que je n'avais pas vu :
**rien n'obligeait les Treize à consulter.** Le compteur ne s'incrémente que sur ce
qui a été soumis ou sur un avis écarté. Ne rien demander et n'écouter personne
n'accumulait jamais rien. Le silence total était la stratégie parfaite.

Trois fermetures, validées : **obligation de consulter** deux fois l'an et avant
tout engagement majeur (art. 35 bis) · **le silence coûte** un point de défiance
(art. 38.4) · **la saisine est inconditionnelle** (art. 15 bis).

Cette dernière règle du même coup le veto que j'avais découvert en présentant le
bloc : l'article 14 bis interdit de mettre aux voix une proposition sans version
en langue simple, sans dire qui en juge — donc n'importe qui pouvait bloquer
n'importe quoi en déclarant une version trop obscure. Résolu sans créer d'organe :
**l'insuffisance se signale, elle ne s'oppose pas.** Un texte incompréhensible est
déjà sanctionné — on ne le comprend pas, on l'ignore, et l'« Ignorer » majoritaire
coûte à son auteur.

### La simulation — et le défaut le plus grave du texte

Diego : *« Maintenant tu simules ce qui se passe dans cette société avec ce
système. »* J'ai calculé au lieu d'imaginer, et l'arithmétique a tranché.

Trois fondateurs · cinq parrainages par Régent et par an · trois parrains par
admission · douze mois de Porteur avant de voter. Il en résulte :

```
an 3 : 13 Régents     an 9  :   598
an 5 : 47             an 11 : 2 124
an 7 : 168            an 12 : 4 004
```

**À trente-six mois — le terme absolu et non prorogeable de l'article 55 — il y a
treize Régents pour treize sièges.** Tout le corps électoral est délégué ; il ne
reste personne pour aviser ni pour dissoudre. Le quorum de 20 % vaut trois
personnes. Et les sortants n'étant pas rééligibles, **une seconde Table Ronde ne
peut pas être formée.**

Les seuils de dévolution de l'article 54 — 500, 2 000, 10 000 — arrivent
respectivement vers les années 9, 11 et 13. La dévolution progressive que le texte
organise n'a jamais lieu : le terme absolu tombe d'abord, sur treize personnes.

Les règles d'entrée et les seuils avaient été écrits séparément et **jamais
multipliés l'un par l'autre**. Ce n'est pas un cas limite, c'est la trajectoire par
défaut. Inscrit en F0, avant toutes les autres failles.

**Et une chose que la simulation rend visible sans qu'on l'ait cherchée : la
lenteur de la croissance et la résistance au Sybil sont la même propriété.** On ne
peut pas desserrer l'entrée sans perdre la défense. Le ramp de dix ans n'est pas un
mauvais réglage, c'est le mécanisme qui fonctionne.

**Leçon de méthode, et elle vaut pour la suite : un texte de gouvernance doit être
exécuté, pas seulement relu.** Ni la lecture attentive, ni l'audit adversarial
n'avaient vu F0. Une seule simulation l'a sorti en une minute.

---

## 2026-08-04, 15h — Bloc 2 : qui vote

Lecture de la Charte avec Diego, bloc par bloc, à son rythme. Le Titre I a été
clos hier (commit `f6d157e`) ; aujourd'hui le Titre II.

### L'article 12 saute

C'était l'article dont Diego s'était plaint sans savoir ce qu'il contenait, et
l'audit avait raison de le désigner. Deux défauts, et un seul aurait suffi.

Déchoir quelqu'un après vingt-quatre mois d'inactivité **oblige à tenir, par
personne, la trace de qui a participé**. Croisé au graphe de parrainage public,
cela rendait calculable la liste de ceux qui ne votent pas — dans un commun où
voter est un devoir. C'est l'instrument de pression que l'article 24 existe pour
empêcher. Et cela contredisait l'article 7 bis : un droit qu'on perd faute d'en
avoir usé est un droit conditionné.

Ne restent que la renonciation volontaire et la cascade de l'article 11.
**L'inactivité ne coûte rien.**

### Les trois statuts — l'idée de Diego

*« L'OS ne doit pas bloquer le nouvel utilisateur, il doit bloquer uniquement le
droit de vote, comme pour les plus jeunes. »*

D'où **Porteur · Régent · Suspendu**. Porter SERF n'est pas être Régent. Le
Porteur a l'appareil entier, lit le Registre, délibère, parle — il ne vote pas.
C'est l'état du jeune, du nouveau venu, de la personne en cours de récupération.

Ce qui en fait un principe et pas une commodité : **on ne coupe jamais l'appareil
de quelqu'un.** La sanction touche le pouvoir, jamais l'usage.

### Seize pour entrer, dix-sept pour voter — et un bénéfice imprévu

Diego : seize ans, puis un an d'attente. J'ai objecté qu'un âge exigerait une
pièce d'identité, donc l'état civil, donc l'anéantissement du jeton aveugle — et
il a répondu par la seule question qui comptait : *« donc tu laisses un gamin de
treize ans voter ? »* J'avais recommandé le parrainage seul en glissant sur ce
cas. C'était malhonnête.

Retenu : **âge attesté par les parrains, jamais prouvé par pièce**, sous leur
responsabilité (art. 11). Solution déclarative, donc imparfaite, et c'est écrit
comme tel. Cible affichée : la **preuve d'âge anonyme** — même technique que
l'article 10, appliquée à un autre attribut. L'émetteur ignore l'usage, le
vérificateur n'apprend que le seuil. Dès qu'un émetteur existe.

**Et l'année de présence vaut bien plus que ce que Diego lui demandait.** Il l'a
posée pour la maturité des jeunes. Appliquée à tous, elle devient la meilleure
défense anti-Sybil du texte : un attaquant doit désormais *entretenir* ses fausses
identités pendant un an avant qu'elles ne vaillent une voix. L'attaque devient
chère, et surtout visible longtemps avant d'être décisive. Le vide de la première
année est exactement ce que la Régence provisoire couvre — les deux mécanismes
s'emboîtent sans qu'on ait rien forcé.

### La protection de l'inexpérience — ma version était mauvaise

J'avais traduit « protection innocence » par : occulter les expressions des
jeunes, les inscrire par engagement cryptographique plutôt qu'en clair. Diego a
refusé, et sa version est meilleure :

> *« Tout ce qu'il fait est aussi clair que pour les autres, la différence c'est
> qu'aucun jugement ne peut s'y appliquer. Il a aucune expérience donc il est
> innocent, ses erreurs ne sont pas de sa faute, en partie de sa responsabilité
> mais pas complètement. »*

Ma version créait une zone d'ombre. La sienne garde tout en pleine lumière et
retire seulement le droit de condamner. Jusqu'à vingt-et-un ans : visibilité
identique, aucune sanction, et rien qui puisse entrer en négatif dans une future
mesure de mérite — c'est là que ça se serait joué sans qu'on le voie venir.

**Et la part qu'il ne porte pas incombe à ses parrains.** Conséquence : on ne
parraine plus un jeune à la légère. Ça règle sans quota le recrutement de masse
que je proposais de plafonner — le coût est sur celui qui recrute, pas sur celui
qui est recruté.

Limite écrite noir sur blanc : le commun peut s'interdire de juger, il ne peut pas
interdire aux autres de lire. La seule chose opposable est le contexte — le
Registre porte le statut de l'auteur au moment de l'acte.

### Récupération d'accès

Mécanisme de Diego, corrigé par lui : *l'appareil actif est le veto*. S'il répond,
il tranche ; s'il ne répond plus de tout le délai, la clé est réputée perdue.
Acte public au Registre, délai annoncé, deux demandes concurrentes se gèlent et le
nombre arbitre.

### Le désaccord de la séance

Diego voulait **pondérer les bulletins selon l'appareil** — moins de poids pour
les appareils à risque. J'ai tenu contre, et il n'a pas insisté : pondérer selon
le matériel fait mécaniquement compter les pauvres moins que les autres, ce qui
est l'exact contraire de l'article 22. Retenu à la place : **on ne pondère jamais,
on publie toujours** la composition du scrutin.

### Rappel de méthode, encore

Le relevé d'heure a montré que la session avait franchi minuit — les décisions
d'hier sont datées du 3, celles-ci du 4. C'est exactement le piège que la
compétence `heure` décrit, et il s'est produit dès le deuxième jour.

---

## 2026-08-03, 11h30 — Publication, et une recherche qui corrige deux décisions

**Poussé sur GitHub** : https://github.com/Aku-Origin/SERF — public, cinq commits.
Compétence `coherence` ajoutée, après m'être fait prendre deux fois dans la même
séance par des renvois périmés (`§6` devenu faux après insertion, « sept écrans »
resté dans un titre après changement de la liste).

### Ce que la recherche a corrigé

**Une faille active dans notre propre texte.** L'analyse à preuves mécanisées de
Belenios a établi que **le secret du bulletin ne tient pas si l'organe
d'éligibilité se comporte mal** — alors même que son rôle paraît étranger au
scrutin. Or notre émetteur de jetons aveugles *est* cet organe. La faille était
chez nous depuis le matin, sous une phrase qui affirmait que la séparation était
« cryptographique et non déclarative ». Corrigé : article 10, émetteur éclaté en
seuil, trois sur cinq.

Leçon de méthode, plus large que le cas : **une analyse à la main manque les
hypothèses qu'une preuve mécanisée trouve.** Pour un système de vote, la
vérification formelle n'est pas un luxe académique.

**Le paradoxe du client n'était pas insoluble.** J'avais écrit qu'il n'avait « pas
de solution parfaite connue ». Les **codes de retour** — feuille papier reçue hors
appareil, comparée après le vote — sont déployés en Suisse depuis 2015. C'est la
seule défense qui contraigne un client compromis *sur-le-champ* plutôt qu'a
posteriori : il ne peut pas afficher un code qu'il n'a jamais vu. Et le défaut
documenté de la mise en œuvre suisse est la vraie leçon : **le protocole n'y est
expliqué qu'en ligne**, donc celui qui contrôle le site contrôle l'explication.
L'explication doit voyager avec le papier.

Point ouvert : la remise suppose un canal indépendant, classiquement postal, ce
qui heurte le pseudonymat. Piste — remise en main propre par les trois parrains à
l'admission.

**Le socle : j'avais tort.** J'avais écarté GrapheneOS parce qu'il enfermait sur
du Pixel. Mais LineageOS **échoue structurellement à l'attestation matérielle** et
ne reverrouille pas le démarrage sur la plupart des appareils — donc pas
d'applications bancaires, donc pas d'adoption, donc aucun des trois piliers. Et
mon objection tombe : partenariat GrapheneOS–Motorola annoncé en mars 2026,
appareils fin 2026/début 2027, soit avant notre jalon ROM.

Troisième fait que j'ignorais : l'**API d'attestation matérielle standard**
d'Android est plus forte que Play Integrity et sait mettre en liste blanche les
clés d'un système alternatif. L'attestation n'est donc pas une lutte perdue mais
un plaidoyer appuyé sur un standard — et la plupart des banques de détail
européennes fonctionnent déjà sur GrapheneOS en 2026, ce qui valide l'Enceinte en
production.

### Ce que la recherche a validé

**vTaiwan valide l'article 35 par son échec.** La référence mondiale de la
délibération numérique repose aujourd'hui sur des bénévoles et voit sa portée
limitée parce que **le gouvernement n'est pas tenu de considérer ses conclusions**.
C'est exactement le trou que comble l'obligation de réponse motivée. Une
délibération que personne n'est tenu d'examiner s'éteint — non par désintérêt,
mais parce que participer devient rationnellement absurde.

**Decidim avertit.** Plateforme la plus déployée institutionnellement, et critique
académique sévère : la participation y est réduite à quelques options de faible
qualité, le débat ouvert absent ou très limité. L'outil ne protège pas d'une
institution qui le configure. D'où l'intérêt de nos articles 35, 37 et 38, qui
contraignent l'organe et non seulement l'assemblée.

**Pol.is offre deux mécanismes à reprendre** : interdire les réponses — ce qui
supprime la dynamique d'affrontement — et regrouper les participants par proximité
de position pour faire apparaître les accords que des camps opposés ignorent
avoir. Le second décrit sans hiérarchiser : seule exception admise à notre refus
du traitement algorithmique.

**Le droit français est favorable.** La loi de 1901 ne définit pas les organes de
gouvernance ; la liberté statutaire est quasi totale et **les statuts ont force de
loi pour les membres**. Des statuts peuvent donc lier la structure à ses scrutins
contraignants, opposables devant le juge civil. L'arbitrage n°1 est résolu.

**Et le RGPD ne s'oppose pas au Registre.** La CNIL retient exactement le
mécanisme de notre article 26 quinquies — engagement cryptographique, empreinte à
clé, destruction de la clé rendant l'information irretrouvable. Nous sommes
alignés sur la doctrine de l'autorité plutôt que sur une interprétation
personnelle.

---

## 2026-08-03, 11h02 — Registre, communautés, résilience

**Premier commit poussé dans l'histoire du projet : `f24c512`**, signé
`Père Sans-Ciel <sans-ciel@aku-origin.org>`. Douze fichiers, 2 426 lignes. Adresse
sur domaine propre, non sur un `noreply` d'hébergeur : elle s'inscrit à jamais dans
chaque clone, autant qu'elle ne dépende de personne.

### Le Registre — et pourquoi ce n'est pas une blockchain

Diego demande la transparence maximale, l'infalsifiabilité, tout enregistré « à
l'image d'une blockchain », et sécurisé par chaque citoyen. Les propriétés visées
sont les bonnes. L'outil ne l'était pas.

Une blockchain résout **l'ordre entre inconnus sans couche d'identité**, en rendant
la participation coûteuse. SERF a déjà une identité — le parrainage — et un
rédacteur désigné. Son problème est autre : **empêcher la réécriture discrète**.
C'est de l'inviolabilité par la preuve, pas du consensus.

Et un argument aurait suffi seul : **la preuve d'enjeu pondère le pouvoir par la
fortune détenue.** C'est littéralement une gouvernance de peu — l'exact contraire
de l'article 22. L'adopter aurait écrit l'inverse de la Charte dans
l'infrastructure.

Retenu : **journal de transparence à arbre de Merkle**, la technologie qui
surveille les certificats de tout l'Internet depuis 2013. Ennuyeuse, éprouvée,
auditée — des qualités, pour une infrastructure de vote.

**Ce qui donne corps à « sécurisé par chaque citoyen » :** chaque appareil est
témoin. Il garde la dernière tête signée, exige la preuve de cohérence, et
confronte avec les appareils croisés. La seule attaque restante — la vue
scindée — échoue dès que deux appareils comparent. Et **la triche produit sa propre
preuve** : deux têtes incohérentes signées par l'opérateur le condamnent sans
qu'aucune autorité n'arbitre.

**Un conflit rattrapé à temps :** un journal immuable et le droit à l'effacement
sont contradictoires — le RGPD l'impose, et l'article 4 de notre propre Charte
aussi. Résolu à la conception : le Registre inscrit des **actes**, jamais des
personnes ; la correspondance personne/engagements vit dehors et se détruit à la
sortie. Après la première inscription, il aurait été trop tard.

### Le pourquoi, et la transmission

Diego : garder trace du pourquoi, du comment et du quoi, pour transmettre aux
générations futures.

Ça change la finalité du Registre. Presque toutes les institutions conservent le
*quoi* et perdent le *pourquoi* — c'est pour cela que chaque génération refait les
mêmes débats et retombe dans les mêmes erreurs. **Article 26 sexies** : motif,
objections, et *ce qui a fait changer d'avis*, en langue claire et formats ouverts.
Le Registre est un instrument de transmission avant d'être un instrument de
contrôle.

### Deux renversements de plus — cinq au total

« L'élévation plutôt que l'éducation » n'appelait pas un article nouveau : c'est la
même chose que « la santé plutôt que la maladie ». **Financer l'amont, pas
l'aval.** L'éducation comble un manque, l'élévation augmente une capacité.
L'article 23 a été généralisé plutôt que dédoublé.

S'y ajoutent **l'échelon proche plutôt que le sommet** et **la mémoire plutôt que
l'amnésie**. Cinq renversements, cinq mécanismes.

### Les communautés fédérées — le changement d'échelle

Jusqu'ici on gouvernait *un logiciel*. Diego : donner à toutes les petites
communautés le moyen de communiquer et de gouverner.

Le dispositif est **reproductible** : sept personnes, un registre, un objet écrit.
La procédure s'allège avec la taille — jusqu'à trente membres, l'assemblée *est*
la Table Ronde. Imposer treize délégués à un village de quarante tuerait le
dispositif par la procédure, ce qui est la façon dont meurent les outils
démocratiques.

**Une propriété que je n'attendais pas :** si les communautés cosignent les
registres les unes des autres, falsifier un registre local exige de falsifier tous
ceux qui l'attestent. **La protection vient du voisinage, pas d'une autorité.**
C'est « sécurisé par chaque citoyen » passé à l'échelle du pays, sans centre.

Messagerie : **Matrix**, ne rien réinventer — protocole fédéré déjà retenu par
l'État français pour son administration. **Jamais de fil algorithmique** : un flux
optimisé pour l'engagement produit l'exact inverse de l'élévation. Ligne rouge de
conception.

### Résilience — brouillage et IEM

Bonne nouvelle : elle était déjà là. **Les preuves de Merkle restent valides quel
que soit le transport** — clé USB, QR code, LoRa, papier. Et le témoignage entre
appareils *est déjà* un protocole de proximité, qui fonctionne mieux en maillage
qu'en étoile.

Le fait qui rend les canaux de secours suffisants plutôt que symboliques : **un
scrutin municipal entier pèse moins qu'une seconde de vidéo.** On ne peut pas faire
passer du streaming sur du LoRa ; une délibération et son dépouillement, si, sur
plusieurs kilomètres, avec une pile.

Quatre modes — plein, maillé, différé, papier — et le système descend au lieu de
tomber. Règle : **aucune fonction essentielle ne suppose le réseau.**

Sur le brouillage : **ne jamais dépendre du GPS**, ni pour l'heure ni pour rien.
L'ordre du Registre est intrinsèque. Un horodatage est du confort, jamais une
preuve.

**Sur l'IEM, dit franchement : aucun logiciel n'en protège.** C'est de la physique.
Ce qui est atteignable, c'est la survie des *données* — et la réponse rejoint la
transmission : **l'ancrage papier.** Soixante-quatre caractères imprimés
trimestriellement aux archives, au dépôt légal de la BnF, chez un notaire, dans la
presse. Quelques feuilles par trimestre, et une seule copie survivante du Registre
suffit ensuite à tout revérifier — sans réseau, sans autorité, sans qu'aucun témoin
d'origine soit vivant.

### Ce qui reste vrai

Rien de tout cela n'attend une technologie à inventer. Merkle, Wi-Fi direct,
Bluetooth, LoRa, QR, clés USB, imprimantes, dépôt légal : tout existe, tout est
éprouvé, tout est légal, tout est bon marché. **Il n'y a qu'à le construire.**

---

## 2026-08-03 — Fondations

**Point de départ.** Dépôt local vide, dépôt distant `Aku-Origin/SERF.git` sans
aucune référence. Rien n'existait. Dépôt git initialisé sur `main`, aucun commit
poussé à ce jour.

### Ce qui a été posé

Sept documents fondateurs : vision, architecture, gouvernance, design,
publication, feuille de route, et la Charte. Plus la mémoire de travail
(`CLAUDE.md`), une compétence `heure`, et ce journal.

### Décisions

**Fork AOSP sur base LineageOS.** Écrire un OS mobile de zéro se heurte aux
pilotes SoC propriétaires, à la certification du baseband et à l'absence
d'écosystème applicatif. GrapheneOS aurait donné un meilleur durcissement, mais
enfermerait sur du Pixel — matériel américain, en contradiction frontale avec le
récit. Le support matériel est le coût le plus lourd du projet : on l'emprunte.

**iOS hors périmètre, définitivement.** Le bootloader d'un iPhone ne s'ouvre pas.
Le promettre coûterait toute crédibilité au premier examen technique.

**Corps électoral par parrainage.** Trois parrains, cinq parrainages par personne
et par an, jeton d'éligibilité signé en aveugle pour séparer l'admission du
bulletin. L'eID étatique offrait une meilleure résistance au Sybil, mais crée une
dépendance à l'État — contradictoire avec un projet qui se construit par le bas —
et bute de toute façon sur l'attestation Play Integrity, donc n'est même pas
prototypable aujourd'hui. Coût assumé : la croissance est lente. C'est cohérent
avec le régime choisi.

**Le scrutin avant la ROM.** Ordre contre-intuitif, assumé : le scrutin est le
risque n°1 et ne dépend d'aucun matériel. On teste tôt ce qui peut tuer le projet.

**Belenios plutôt que réimplémenter la cryptographie de vote.** Réécrire du
dépouillement homomorphe est la façon la plus sûre d'introduire une faille.

### Correction en cours de route — microG écarté

J'avais d'abord recommandé **microG** pour restituer les fonctions Google. C'était
le mauvais choix, et Diego a posé la bonne question : garder l'accès aux
applications actuelles, mais **encapsulées**.

microG réimplémente les API Google en usurpant la signature de Google, ce qui
exige des privilèges système : le composant le moins digne de confiance du
téléphone hérite des droits les plus élevés, pour une compatibilité qui reste
approximative puisqu'il s'agit d'une imitation.

**L'Enceinte** inverse le rapport : les services Google tournent comme une
application ordinaire, **sans aucun privilège**. Compatibilité supérieure *et*
architecture plus saine. Éprouvé en production par GrapheneOS.

Le levier d'adoption qui en découle est le vrai gain : **répondre par un vide
plutôt que par un refus.** Une permission refusée fait planter l'application ;
l'utilisateur accuse SERF et s'en va — c'est ce qui a tué toutes les alternatives
précédentes. Un carnet de contacts vide la laisse fonctionner et ne lui apprend
rien.

Limite dite franchement : l'Enceinte ne contourne pas l'attestation matérielle
forte. Banques et France Identité refuseront. C'est de la régulation, pas de
l'ingénierie.

### Les trois renversements

Formulés par Diego, adoptés comme boussole. Chacun a reçu son mécanisme le jour
même, parce qu'une valeur sans mécanisme n'est qu'une déclaration :

| Renversement | Mécanisme |
|---|---|
| Payer la santé plutôt que la maladie | Vote par conviction ; priorité d'affectation à la prévention (Charte, art. 23) |
| La souveraineté du peuple plutôt qu'une gouvernance de peu | Pondération quadratique (art. 22) |
| La liberté plutôt que la soumission | L'Enceinte |

### Réécriture de la Charte — v0.1 → v0.2

Les décisions de gouvernance de Diego ont imposé une refonte plutôt qu'un
rapiéçage : « Table Ronde » désignait chez moi l'assemblée entière, alors qu'il
s'agit des Treize. Vocabulaire tranché — les porteurs de l'OS sont **les
Régents**, ce qui colle au nom du projet ; la **Table Ronde** est le collège des
Treize.

**Consultatif partout, contraignant sur la révocation.** Choix constitutionnel
rare et cohérent : le peuple ne cogère pas le quotidien — ce qui produit toujours
la paralysie et la fatigue — il détient le seul pouvoir qui ne se contourne pas,
celui de renvoyer.

**Les quatre expressions : Oui, Non, À nuancer, Ignorer.** « À nuancer » renvoie
le texte en délibération (deux fois au plus). « Ignorer » récuse la question
elle-même — ce n'est pas l'abstention, qui est le silence, mais un acte compté.

**Le câblage central de la séance.** « Ignorer » n'est pas un vote perdu : un
« Ignorer » majoritaire inscrit un **point de défiance**, et cinq points sur douze
mois glissants **ouvrent de plein droit le scrutin contraignant de dissolution**.
L'expression répétée arme le seul pouvoir réel de l'Assemblée. C'est ce qui donne
sa consistance au « reset » demandé par Diego.

**L'obligation de réponse motivée (art. 35).** Sans elle, « consultatif » veut
dire « ignoré ». Passer outre un avis est permis ; le faire en silence ne l'est
pas — et le silence coûte un point de défiance.

**Un second vote contraignant, que j'ai ajouté et signalé : la révision de la
Charte.** Si les Treize pouvaient l'amender seuls, ils pourraient supprimer le
scrutin qui les révoque. L'édifice se dévissait en un tour.

**La Table Ronde des Treize.** Douze Corps — Soigner, Nourrir, La Nature,
Défendre, Transmettre, Bâtir, Produire, Mouvoir, Relier, Juger, Créer,
Accompagner — plus le **Siège Ouvert**, tiré au sort parmi tous les Régents sans
condition de métier. Six sièges élus, six tirés au sort, le mode alternant à
chaque renouvellement pour qu'aucun Corps ne s'installe ni ne se professionnalise.

*Reste à confirmer* : la lecture de « un élu, l'autre au hasard ». Trois lectures
possibles, notées à l'article 29 ; celle qui est câblée conserve treize personnes
et fait coexister les deux modes en permanence.

**Une asymétrie assumée (art. 32) :** les Régents votent à bulletin secret, les
Treize votent à découvert. **Le secret protège le faible, la publicité contraint
le puissant.**

### Publication et continuité — priorité posée avant tout code

**La visibilité est la protection.** La tentation de commencer discrètement est
l'erreur exacte : un dépôt confidentiel disparaît sans que personne ne s'en
aperçoive. Quatre cercles retenus : GitHub (vitrine), Codeberg (miroir associatif
européen), **Software Heritage** (archive Inria/UNESCO, permanence patrimoniale —
la pièce la plus négligée et la plus solide), Radicle (hors-serveur, dernier
recours).

**La signature est une charge, non un masque.** Objection de Diego : un pseudonyme
peut être repris. Elle est juste et elle change la nature du dispositif — un
masque disparaît avec son porteur, une charge se transmet. Inscrit à l'article 52.
Ça règle par le haut la question de la continuité : la charge est déjà conçue pour
changer de mains, ce qui vaut mieux que n'importe quel dispositif automatique.

**Le sens du nom.** *Sans ciel* : rien au-dessus — ni plafond, ni voûte, ni
seigneur. C'est la thèse du projet en un mot, et le contraire exact du serf, qui a
toujours quelqu'un au-dessus de lui. Ce n'est pas l'absence de règle, mais
l'absence d'un étage supérieur qui l'écrit à votre place ; la Charte, elle, est
écrite en bas. Inscrit dans la vision.

**Cloisonnement.** Une seule identité par dépôt — règle d'hygiène retenue, non
une consigne, et révisable **avant** le premier push. Un dépôt public, miroité et
archivé de façon permanente ne se corrige pas : une mention croisée lierait deux
identités pour toujours, dans tous les clones. Après le push, ça ne se défait
plus.

*(Correction de séance : j'avais d'abord lu « ce n'est pas la même » comme une
consigne de séparation d'identités. Il s'agissait du sens des noms.)*

### État à la clôture

Rien n'est commité. Aucun code écrit.

**Ouvert :** portée statutaire des votes hors Charte et dissolution · calibrage
des seuils (13 nombres à éprouver) · lecture définitive de l'article 29 ·
financement · licence · adresse de courriel du projet.

**Prochain pas :** le premier commit et la mise en place des miroirs, avant tout
développement.

*Le Sans-Ciel*
