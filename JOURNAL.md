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
