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
