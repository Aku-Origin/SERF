# 08 — Résilience : gouverner sans réseau

> **Un outil pour gouverner ensemble doit fonctionner le jour où il n'y a plus de
> réseau — sinon il ne sert précisément pas le jour où l'on en aurait le plus
> besoin.**

---

## 1. Ce qu'on affronte

Quatre situations, de la plus banale à la plus extrême. Les trois premières sont
des problèmes d'ingénierie ; la quatrième est un problème de physique, et il faut
le dire.

| | Situation | Fréquence | Traitable par le logiciel ? |
|---|---|---|---|
| **1** | Panne, saturation, zone blanche | Quotidienne | Oui, entièrement |
| **2** | Coupure ou filtrage volontaire | Occasionnelle | Oui, largement |
| **3** | Brouillage radio local | Rare, en hausse | Oui, en partie |
| **4** | Impulsion électromagnétique | Très rare, catastrophique | **Non — voir §6** |

Concevoir pour la situation 1 traite déjà l'essentiel des situations 2 et 3. C'est
la bonne nouvelle : **il n'y a pas de mode « crise » à construire à part.** Il y a
un système qui n'a jamais supposé le réseau.

---

## 2. La propriété qui rend tout possible

**Un journal à arbre de Merkle se synchronise par différences, et ses preuves
restent valides quel que soit le transport.**

C'est la conséquence la plus utile du choix fait en [`06-REGISTRE.md`](06-REGISTRE.md),
et elle n'était pas cherchée. Une preuve d'inclusion est un calcul sur des
empreintes : elle ne sait pas, et n'a pas à savoir, si les données sont arrivées
par fibre, par radio, sur une clé USB ou par un QR code photographié.

Il en découle qu'aucun canal n'est privilégié :

| Canal | Ce qui passe | Portée |
|---|---|---|
| Internet | Tout | Illimitée |
| Maillage local (Wi-Fi direct, Bluetooth) | Tout | Quelques dizaines de mètres, de proche en proche |
| LoRa / radio sub-GHz | Têtes d'arbre, bulletins, résumés | Plusieurs kilomètres |
| Clé USB, carte SD | Tout | Celle des jambes |
| QR code affiché ou imprimé | Têtes d'arbre, bulletins | Celle du regard |
| Papier, voix, radio amateur | Tête d'arbre (64 caractères) | Celle qu'on veut |

**Une blockchain n'aurait pas cette propriété** : elle exige un réseau vivant pour
que le consensus se forme. Un journal de Merkle n'exige rien du tout — il se
vérifie à l'arrêt.

---

## 3. Le fait décisif : la gouvernance ne pèse rien

On dimensionne les téléphones pour la vidéo, et on en conclut à tort qu'il faut du
débit pour tout.

| Objet | Taille |
|---|---|
| Tête d'arbre signée | ~100 octets |
| Bulletin chiffré | quelques centaines d'octets |
| Preuve d'inclusion (1 million d'entrées) | ~640 octets |
| Texte d'une proposition | quelques kilo-octets |
| **Une seconde de vidéo** | **~200 000 octets** |

**Un scrutin municipal entier tient dans ce que coûte une seconde de vidéo.**

C'est ce qui rend les canaux de secours réellement suffisants, et non symboliques.
On ne peut pas faire passer un service de streaming sur du LoRa ; on peut y faire
passer une délibération, un vote et son dépouillement, sur plusieurs kilomètres,
avec une pile.

---

## 4. Les quatre modes de fonctionnement

Le système ne tombe pas : il **descend**. Chaque mode est complet en lui-même, et
le passage se fait sans intervention ni annonce.

**Mode plein — réseau disponible.** Tout fonctionne : synchronisation continue,
témoignage entre appareils, contresignature des cosignataires.

**Mode maillé — pas d'Internet, des voisins.** Les appareils se synchronisent de
proche en proche par Wi-Fi direct et Bluetooth. Les bulletins sont collectés et
relayés ; les têtes d'arbre circulent et se confrontent. Le témoignage citoyen
fonctionne **mieux** en maillage qu'en étoile, car il repose déjà sur la
confrontation entre pairs.

**Mode différé — ni réseau ni voisins.** Le vote est déposé localement, signé,
horodaté logiquement, et transmis quand un canal réapparaît. La fenêtre de scrutin
de 72 heures (Charte, art. 14) n'a pas été choisie pour cela, mais elle l'autorise.
Le transport peut être une clé USB, un QR code, ou quelqu'un qui se déplace.

**Mode papier — plus rien d'électronique.** Le bulletin s'imprime, se dépose, se
scanne plus tard. Le dépouillement redevient manuel, et **le résultat reste
rattachable au Registre** par l'empreinte imprimée sur le bulletin. C'est dégradé,
c'est lent, et c'est mieux que rien — ce qui est exactement l'objectif.

> **Règle de conception : aucune fonction essentielle ne suppose le réseau.** Une
> fonctionnalité qui exige d'être en ligne pour délibérer ou voter est refusée,
> quelle que soit son élégance.

---

## 5. Brouillage : ne pas offrir de prise

Le brouillage radio est local, coûteux à maintenir sur une zone, et illégal — mais
réel, et en augmentation. Trois règles suffisent à ne pas lui donner de prise.

**Ne jamais dépendre du GPS.** Ni pour l'heure, ni pour la position, ni pour
départager deux versions. Le GPS est le signal le plus facile à brouiller et à
falsifier qui soit. **L'ordre du Registre est intrinsèque** : il découle de la
structure de l'arbre, pas d'une horloge extérieure. Un horodatage est une
indication de confort, jamais un élément de preuve.

**Multiplier les bandes.** Wi-Fi (2,4 et 5 GHz), Bluetooth, LoRa (868 MHz en
Europe, bande libre), et le hors-onde. Brouiller une bande est facile ; brouiller
toutes celles d'un territoire pendant 72 heures ne l'est pas.

**Garder le hors-onde comme chemin normal, pas comme exception.** Une clé USB qui
traverse une zone brouillée transporte un Registre parfaitement vérifiable. Si ce
chemin n'est utilisé qu'en catastrophe, il ne fonctionnera pas en catastrophe : il
doit être un mode ordinaire, testé, documenté, banal.

---

## 6. IEM : dire ce qui est vrai

**Aucun logiciel ne protège d'une impulsion électromagnétique.** C'est de la
physique — des courants induits qui détruisent des jonctions. Prétendre le
contraire serait exactement le genre de promesse qui déshonore un projet
sérieux.

Ce qui est atteignable n'est pas la survie des appareils. C'est **la survie des
données et la capacité à repartir.**

**Sauvegarde froide.** Une copie du Registre sur un support hors tension, dans un
contenant conducteur clos — une cage de Faraday improvisée suffit — n'est pas
affectée. C'est une pratique à quelques euros, que chaque communauté peut tenir
elle-même. Un appareil de rechange, éteint, dans le même contenant, redonne un
point de départ.

**Dispersion géographique.** Une IEM a une empreinte étendue mais finie. Des
communautés fédérées sur un territaire large ne perdent jamais toutes leurs copies
à la fois — c'est un bénéfice supplémentaire, non prévu, de l'attestation mutuelle
du [`07-SUBSIDIARITE.md`](07-SUBSIDIARITE.md).

**Et surtout : l'ancrage papier.**

---

## 7. L'ancrage papier

**Une tête d'arbre tient en 64 caractères hexadécimaux.** Elle s'imprime,
s'affiche, se lit à voix haute, se recopie à la main, se grave.

Conséquence : si une seule copie du Registre survit, **n'importe qui peut la
recalculer et la comparer à une empreinte imprimée**. Si elles concordent, le
Registre est authentique — sans serveur, sans réseau, sans autorité, et sans
qu'aucun des témoins d'origine soit encore en vie.

**Périodiquement — trimestriellement — la tête d'arbre est imprimée et
déposée :**

- Aux **archives municipales** de chaque communauté fédérée.
- Au **dépôt légal** de la Bibliothèque nationale de France : une obligation de
  conservation portée par l'État, gratuite, pluriséculaire — le pendant papier de
  Software Heritage.
- Chez un **notaire**, où la date certaine est opposable.
- Dans la **presse locale**, où elle devient publique et impossible à retirer.

Ces dépôts sont dérisoires en coût — quelques feuilles par trimestre — et
constituent l'ancrage le plus durable du dispositif entier. Ils traversent une
panne, une saisie, une IEM, et une génération.

**C'est aussi la réponse à la transmission.** L'article 26 sexies de la Charte
exige que le Registre reste lisible sans l'outil qui l'a produit. L'ancrage papier
en est la forme extrême : la preuve d'intégrité survit à la disparition de toute
l'informatique qui l'a créée.

---

## 8. Ce qui reste vrai, et qu'il faut redire

Il n'y a **pas besoin d'autorité centrale** — ni pour décider, ni pour attester,
ni pour rétablir après une coupure. Le Registre s'atteste par ses pairs, les
communautés se cosignent, et le papier ancre le tout.

Et **rien de ce document n'attend une technologie à inventer.** Merkle, Wi-Fi
direct, Bluetooth, LoRa, QR codes, clés USB, imprimantes, dépôt légal : tout
existe, tout est éprouvé, tout est légal, tout est bon marché.

**Il n'y a qu'à le construire.**

---

## 9. Composants

| Composant | Rôle |
|---|---|
| `serf-transport` | Abstraction des canaux — réseau, maillage, LoRa, QR, fichier |
| `serf-maille` | Synchronisation de proche en proche, sans infrastructure |
| `serf-froid` | Export de sauvegarde froide, restauration, jeu de secours |
| `serf-ancre` | Génération des feuilles d'ancrage trimestrielles, suivi des dépôts |

**Ordre de construction :** `serf-transport` **dès la première ligne du Registre**.
Une abstraction de transport ajoutée après coup ne fonctionne jamais, parce que
mille suppositions de connectivité se seront glissées partout entre-temps.
