# 10 — Les surfaces du système

> Un système d'exploitation n'est pas onze écrans. C'est une trentaine de
> surfaces, dont la plupart n'ont rien à voir avec la gouvernance — et dont
> l'absence d'une seule suffit à rendre le téléphone inutilisable.
>
> Ce document les inventorie, et tranche pour chacune : **écrire, ou adopter.**

---

## 0. Adopter n'est pas maquiller

> **On reprend un socle, on ne le laisse pas tel quel.** Ne pas réécrire n'est pas
> ne pas concevoir.

Ce document tranche, pour chaque surface, s'il faut du **code neuf**. C'est une
question d'économie d'ingénierie, et rien d'autre. Elle ne dit pas ce qui relève
de la **conception**, qui porte sur l'ensemble et n'est déléguée à personne.

Le maquillage, c'est changer les couleurs et poser un logo. La conception, c'est
décider ce que le système fait **par défaut**, ce qu'il **refuse** de faire, et
comment les surfaces se répondent. Rien de cela n'est hérité — quelle que soit
l'origine du code.

Ce qui reste nôtre sur **chaque** surface, y compris adoptée :

| | Ce que nous décidons |
|---|---|
| **Les défauts** | Ce qui est actif au premier démarrage. La plupart des gens ne changeront jamais un réglage : le défaut *est* le produit |
| **Les retraits** | Ce qu'on enlève. Toute fonction contraire au Titre I disparaît, même utile, même attendue |
| **Le comportement des permissions** | Toute application passe par l'Enceinte. Aucune n'accède au réel parce que son auteur l'avait prévu ainsi |
| **Les parcours** | Comment on passe d'une surface à l'autre, ce qui est à un geste et ce qui demande un détour délibéré |
| **L'accessibilité** | Niveau AA minimum, AAA sur le chemin de vote — **et c'est un critère d'adoption** |
| **Le ton** | Vocabulaire, densité, absence de célébration. Une application adoptée est réécrite dans sa langue |

**Le point le plus contraignant est l'accessibilité.** Une application par ailleurs
excellente qui échoue au niveau AA n'est **pas adoptable** : soit on l'adapte, soit
on la remplace, soit on l'écrit. C'est ce qui empêche « adopter » de devenir
« se contenter de » — et c'est mesurable, donc opposable.

**Conséquence sur les chiffres ci-dessous :** ils comptent des lignes de code, pas
de l'intention. *Aucune* surface n'échappe à la conception.

---

## 1. La discipline d'écriture

**On n'écrit que ce qui porte la thèse. On adopte tout le reste.**

Réécrire une galerie photo, une calculatrice ou un lecteur de PDF ne rapproche
d'aucun objectif du projet, et consomme les années qu'il faudrait à la Régence.
L'écosystème libre a déjà tout cela, souvent mieux fait que ce qu'on produirait.

Trois catégories, et une seule justifie du code neuf :

| | Critère | Décision |
|---|---|---|
| **Écrire** | La surface *est* la thèse — elle n'existe nulle part ailleurs | Code neuf |
| **Adapter** | La surface existe, mais porte le ton ou touche à la sécurité | Fork, habillage, durcissement |
| **Adopter** | La surface est banale et bien faite ailleurs | Intégration, zéro code |

---

## 2. Ce que SERF écrit — et rien d'autre

Six surfaces. Ce sont elles, et elles seules, qui justifient l'existence d'un
système nouveau.

| Surface | Pourquoi personne ne l'a |
|---|---|
| **La Table Ronde** | Délibérer et voter depuis le système. Voir [`09-BRIEF-DESIGN.md`](09-BRIEF-DESIGN.md) |
| **Le Registre** | Journal de transparence vérifié sur l'appareil. Voir [`06-REGISTRE.md`](06-REGISTRE.md) |
| **L'Enceinte** | Permissions qui répondent un vide plutôt qu'un refus. Voir [`02-ARCHITECTURE.md`](02-ARCHITECTURE.md) |
| **Le tableau de souveraineté** | Ce que chaque application a tenté, et vers qui |
| **L'état du lien** | Les quatre modes, le maillage, la sauvegarde froide |
| **La messagerie** | La seule où l'identité n'est pas un numéro de téléphone. Voir §4 |

---

## 3. L'inventaire complet

### Cœur du système

| Surface | Décision | Base |
|---|---|---|
| Premier démarrage | **Adapter** | Porte le ton du projet — première impression de souveraineté |
| Lanceur | **Adapter** | Lawnchair, ou Launcher3 d'AOSP réhabillé |
| Écran de verrouillage | Adopter | AOSP durci |
| Volet de notifications | **Adapter** | Doit distinguer la notification de scrutin de toutes les autres |
| Réglages | **Adapter** | La plus grosse surface du système ; réorganisée autour de la souveraineté |
| Gestionnaire de permissions | **Écrire** | C'est l'Enceinte |
| Mise à jour du système | **Écrire** | Signature multipartite, construction reproductible (Charte, art. 47) |
| Récupération | Adopter | LineageOS Recovery |
| Sauvegarde et restauration | **Adapter** | Chiffrement de bout en bout, hébergeur au choix |
| Services d'accessibilité | Adopter | AOSP — **jamais dégradés**, c'est constitutionnel (art. 6) |
| **Clavier** | **Adapter** | HeliBoard ou FlorisBoard. **Voie d'exfiltration n°1** : hors ligne obligatoire, aucun réseau, aucune correction dans le nuage |
| Gestionnaire de fichiers | Adopter | Material Files, ou DocumentsUI |
| Client de dépôt | **Adapter** | F-Droid + Aurora Store, sous contrôle de la Table Ronde |

### Communication

| Surface | Décision | Base |
|---|---|---|
| Téléphone | Adopter | Fossify Phone |
| Contacts | **Adapter** | Fossify Contacts + gestion des sous-ensembles de l'Enceinte |
| SMS / MMS | Adopter | Fossify SMS |
| **Messagerie chiffrée** | **Écrire** | Voir §4 — la seule sans numéro de téléphone |
| Courriel | Adopter | Thunderbird Android (ex-K-9 Mail) |
| Agenda | Adopter | Etar, ou Fossify Calendar |

### Média

| Surface | Décision | Base |
|---|---|---|
| Appareil photo | Adopter | GrapheneOS Camera — **retire les métadonnées par défaut** |
| Galerie | Adopter | Fossify Gallery |
| Musique et vidéo | Adopter | VLC, Fossify Music |
| Enregistreur d'écran et dictaphone | Adopter | Fossify |

### Utilitaires

| Surface | Décision | Base |
|---|---|---|
| Navigateur | **Adapter** | Vanadium (Chromium durci) ou Mull. Surface d'attaque la plus large du système |
| Cartes | Adopter | Organic Maps ou OsmAnd — hors ligne par défaut |
| Horloge, calculatrice, notes | Adopter | Fossify |
| Lecteur de PDF | Adopter | GrapheneOS PDF Viewer — isolé, sans réseau |

### Souveraineté

| Surface | Décision |
|---|---|
| Tableau de souveraineté | **Écrire** |
| Pare-feu par application | **Écrire** — intégré à l'Enceinte, non un module tiers |
| Espaces cloisonnés | **Adapter** — profils AOSP, gelables d'un geste |
| Transport et maillage | **Écrire** — voir [`08-RESILIENCE.md`](08-RESILIENCE.md) |
| Table Ronde, Registre, état du lien | **Écrire** |

**Bilan : environ trente-cinq surfaces, dont neuf écrites et dix adaptées.** Les
seize restantes sont de l'intégration. C'est ce rapport qui rend le projet
faisable.

---

## 4. La messagerie chiffrée

### Deux paroles, jamais confondues

SERF porte **deux** formes de parole, et les mélanger est le risque de conception
le plus grave du système.

| | **La parole publique** | **La parole privée** |
|---|---|---|
| Où | La Parole — délibération | La Messagerie |
| Qui lit | Tout le monde, pour toujours | Les destinataires, et personne d'autre |
| Trace | **Opposable, inscrite au Registre** | **Aucune** |
| Protocole | Matrix, salons ouverts | Matrix chiffré de bout en bout |
| Sert à | Délibérer, objecter, amender | Se parler |

> **Quelqu'un qui croit chuchoter alors qu'il dépose au Registre, c'est une vie
> abîmée.** Les deux surfaces doivent être visuellement irréconciliables : jamais
> le même écran, jamais la même couleur, jamais la même typographie, jamais un
> passage de l'une à l'autre sans rupture explicite. Aucune fonction de « partage »
> ne fait glisser un message privé vers le public sans un acte délibéré et nommé.

### Pourquoi pas Signal, malgré tout son mérite

Signal est la référence du chiffrement de messagerie, et son protocole est le bon.
Mais **Signal exige un numéro de téléphone comme identité.**

En France, un numéro est rattaché à une pièce d'identité. Adopter Signal
reviendrait donc à rattacher chaque Régent à son état civil — exactement ce que le
parrainage à jeton aveugle a été conçu pour éviter (Charte, art. 10). Le reste de
l'édifice cryptographique deviendrait décoratif.

S'y ajoutent : un serveur central en juridiction américaine, et un annuaire de
contacts fondé sur les numéros du carnet d'adresses.

### Ce qu'on retient : le protocole de Signal, sans Signal

Le chiffrement de Matrix — **Olm et Megolm** — est une implémentation du **double
cliquet** de Signal, avec confidentialité persistante et sécurité future. On
obtient donc les garanties cryptographiques de Signal, mais :

- **sans numéro de téléphone** — l'identité est le jeton de parrainage ;
- **fédéré** — chaque communauté héberge le sien, aucun centre à saisir ;
- **un seul protocole pour les deux paroles**, donc une seule pile à durcir et à
  auditer plutôt que deux.

### La réserve, dite franchement

**Matrix protège moins bien les métadonnées que Signal.** Le serveur voit qui
appartient à quel salon, qui écrit quand, et à quel rythme. Signal a investi des
années sur ce point précis — expéditeur scellé, découverte privée des contacts —
et Matrix n'a pas d'équivalent aussi abouti.

Atténuations, aucune parfaite :

- **Héberger par communauté.** Les métadonnées d'un village restent chez lui.
- **Aucun identifiant réutilisé** entre le Registre et la messagerie.
- **Acheminement par le maillage** quand il est disponible : de proche en proche,
  aucun serveur ne voit rien.

Et une recommandation honnête : **pour un usage à risque élevé — journalisme,
lanceur d'alerte, opposition politique — recommander Signal ou Briar en
complément**, plutôt que de prétendre à une parité qui n'existe pas. Un projet qui
surestime sa propre protection met en danger ceux qui le croient.

### Faire évoluer le protocole

Le protocole n'est pas un plafond : Matrix est une **spécification ouverte**, dont
les évolutions passent par un processus public de propositions. Rien n'interdit à
SERF d'y porter ce qui lui manque — et le manque est identifié : la protection des
métadonnées.

Trois voies, par coût croissant. **Prendre la moins chère qui suffise.**

**1. Ajouter par-dessus, sans toucher au protocole.** Enveloppe masquant
l'expéditeur, trafic de couverture pour noyer les rythmes, acheminement par le
maillage. L'essentiel du gain de métadonnées s'obtient ainsi, sans rien casser.
**À épuiser avant tout le reste.**

**2. Proposer une extension en amont.** Une proposition publique, discutée,
adoptée : le gain profite à tout l'écosystème, et le coût de maintenance est
partagé. Lent, mais c'est la voie propre — et un projet de souveraineté a intérêt
à ce que son protocole vive au-delà de lui.

**3. Bifurquer.** Toujours possible, jamais gratuit : on perd la compatibilité
avec la fédération existante, et **on devient responsable d'un protocole** —
spécification, sécurité, clients, montées de version, à perpétuité. C'est le coût
que sous-estiment tous ceux qui l'ont fait.

> La perte de fédération n'est pas seulement un coût : ce peut être un choix
> légitime — on ne veut pas nécessairement que les salons d'une commune fédèrent
> avec des serveurs inconnus. Mais alors **c'est un cloisonnement à décider, pas
> un dommage à subir**, et il doit être voulu pour lui-même.

**Ce qu'on ne fait jamais : modifier la cryptographie.** Le double cliquet, Olm et
Megolm sont audités et éprouvés. On peut changer ce qui les entoure — transport,
identité, métadonnées, fédération. On ne touche pas au cœur, sous peine
d'introduire précisément la faille qu'on prétendait corriger.

### Fonctionner sans réseau

La messagerie suit les quatre modes de [`08-RESILIENCE.md`](08-RESILIENCE.md).
Matrix ne fait pas de maillage nativement : une couche de report et transfert, sur
le modèle de **Briar**, achemine les messages de proche en proche quand
l'infrastructure manque. Le chiffrement est inchangé — seul le transport diffère.

---

## 5. Adopter n'est pas déléguer

Chaque application adoptée devient une partie de la surface d'attaque de SERF, et
son éditeur devient un maillon de la chaîne de confiance.

**Le précédent à retenir :** Simple Mobile Tools, suite d'utilitaires libres
largement recommandée, a été rachetée en 2023 par une société de publicité. La
communauté a dû la bifurquer en urgence — d'où **Fossify**, cité plus haut. Un
projet qui se serait contenté de suivre les mises à jour de l'éditeur aurait
distribué le rachat à ses utilisateurs.

D'où une politique, non négociable :

1. **Construire depuis les sources**, dans notre propre chaîne d'intégration.
   Jamais un binaire fourni par un tiers.
2. **Épingler les versions.** Aucune montée automatique. Chaque montée est un
   acte examiné.
3. **Relire les différences** à chaque montée, en priorité sur ce qui touche au
   réseau, aux permissions et à la cryptographie.
4. **Surveiller les changements de main.** Un rachat, un transfert de dépôt, un
   nouveau mainteneur inconnu : signal d'alerte, gel immédiat de la version.
5. **Prévoir la bifurcation.** Pour chaque application adoptée, savoir d'avance ce
   qu'on ferait si elle changeait de propriétaire. Ne pas adopter ce qu'on ne
   saurait pas reprendre.

**Une application adoptée qui change de mains devient une porte dérobée.** C'est
la voie de compromission la plus probable du projet — plus que la cryptographie,
plus que le noyau.
