# 02 — Architecture technique

> Ce document tranche la question fondatrice : **sur quoi SERF est-il construit ?**
> Toutes les autres décisions techniques en découlent.

---

## 1. Le mur d'entrée : pourquoi pas un OS de zéro

L'ambition « un OS français indépendant » se heurte à quatre obstacles qui ne se
contournent pas par l'effort ou le talent.

**Les pilotes.** Un téléphone moderne repose sur un SoC (Qualcomm, MediaTek,
Exynos) dont le modem, l'ISP, le GPU et le DSP sont pilotés par des binaires
propriétaires livrés sous NDA au fabricant. Personne hors de ce circuit ne peut
les réécrire. Un OS mobile qui n'utilise pas ces blobs n'a ni réseau, ni appareil
photo, ni accélération graphique.

**La pile radio.** Le baseband est un processeur autonome, avec son propre OS
temps réel, soumis à certification réglementaire (ANFR, ETSI). Le réécrire est
juridiquement interdit sans homologation, et techniquement l'affaire d'un
équipementier télécom.

**L'écosystème applicatif.** Un OS sans applications est un objet mort. Le seul
moyen d'hériter d'un catalogue est d'être compatible Android — donc d'exécuter du
bytecode ART/Dalvik et d'implémenter les API du framework Android. À ce stade,
autant partir d'AOSP.

**L'attestation.** Les applications bancaires, les transports, France Identité,
les services de streaming exigent Play Integrity. Un OS non certifié y échoue.
C'est un problème que SERF affrontera quel que soit son socle — mais partir
d'AOSP est la seule position où une négociation est concevable.

**Conclusion : SERF est un fork d'AOSP.** Ce n'est pas un renoncement à la
souveraineté. La souveraineté se joue sur la couche que l'on contrôle — services,
identité, données, gouvernance — pas sur la réécriture d'un pilote GPU.

---

## 2. Le socle : quel point de départ exactement

Trois candidats, avec des compromis très différents.

| Option | Ce qu'on gagne | Ce qu'on paie |
|---|---|---|
| **AOSP nu** | Contrôle total, dette technique nulle | Support matériel à écrire pour chaque appareil : des mois par modèle |
| **LineageOS** | Support de ~200 appareils déjà fait, communauté active | Durcissement sécurité faible ; il faut le reconstruire |
| **GrapheneOS** | Le durcissement le plus abouti au monde | Support Pixel uniquement ; portage ailleurs = quasi-réécriture |

### Décision rouverte — 3 août 2026

> **La recommandation initiale était LineageOS. La recherche l'a invalidée.**
> Détail et sources : [`11-ETAT-DE-LART.md §4`](11-ETAT-DE-LART.md).

Le raisonnement initial : le support matériel est le coût le plus lourd du projet,
LineageOS l'offre gratuitement sur un large parc d'occasion, et s'enfermer sur du
Pixel — matériel américain — contredirait le récit de souveraineté.

**Trois faits l'ont défait.**

**LineageOS ne peut structurellement pas tenir la promesse.** Les ROM non
officielles échouent à l'attestation matérielle parce qu'elles rompent la chaîne
de certification — donc pas d'applications bancaires, donc pas d'adoption. Et sur
la majorité des appareils concernés, le démarrage vérifié ne peut même pas être
reverrouillé. **Un socle qui n'atteste ni ne verrouille ne porte aucun des trois
piliers.**

**L'objection « Pixel uniquement » est en train de tomber.** GrapheneOS a annoncé
en mars 2026 un partenariat avec Motorola, appareils visés fin 2026 / début 2027.
Notre jalon ROM vient après le jalon scrutin — soit dans plusieurs années. Le
verrou n'existera probablement plus à cette échéance.

**Une voie légitime existe pour l'attestation**, que j'ignorais : l'API
d'attestation matérielle standard d'Android est plus forte que Play Integrity et
sait mettre en liste blanche les clés d'un système alternatif. Ce n'est donc pas
une lutte perdue mais un travail de plaidoyer appuyé sur un standard — et le
résultat est déjà visible, la plupart des banques de détail européennes
fonctionnant sur GrapheneOS en 2026.

**Recommandation révisée : lignée GrapheneOS, appareils issus des partenariats
constructeurs.** On renonce au parc d'occasion large, qui était un argument
écologique et social réel — mais il ne compensait pas l'impossibilité de tenir la
promesse de sécurité.

*À confirmer par Diego : c'est une révision de fond, pas un ajustement.*

---

## 3. Couches du système

```
┌──────────────────────────────────────────────────────────┐
│  LA RÉGENCE          Table Ronde · Registre · Scrutin    │  ← original SERF
├──────────────────────────────────────────────────────────┤
│  SERVICES SOUVERAINS  Identité · Sync · Cartes · Push    │  ← à construire
├──────────────────────────────────────────────────────────┤
│  APPLICATIONS SYSTÈME Lanceur · Contacts · Messages      │  ← à habiller
├──────────────────────────────────────────────────────────┤
│  FRAMEWORK ANDROID    API, ART, PackageManager           │  ← AOSP, durci
├──────────────────────────────────────────────────────────┤
│  HAL + PILOTES        blobs SoC propriétaires            │  ← hérité, non modifiable
├──────────────────────────────────────────────────────────┤
│  NOYAU LINUX          GPLv2 — modifications publiables    │  ← hérité, durci
└──────────────────────────────────────────────────────────┘
```

L'effort de SERF se concentre sur les **deux couches du haut**. C'est là que
réside la différenciation ; le reste est de l'intégration.

---

## 4. L'Enceinte — encapsuler plutôt qu'exclure

> **Décision structurante : SERF ne retire pas les applications, il les encercle.**
> C'est la condition d'une adoption simple et rapide.

### Le constat d'échec des ROMs alternatives

Toutes les distributions dégooglisées butent sur le même mur : elles demandent à
l'utilisateur de **renoncer** à ses applications. Sa banque, son opérateur de
transport, son application de santé, celle de son employeur. Une fois sur deux
l'application refuse de démarrer, une fois sur deux la fonction essentielle est
absente. L'utilisateur revient à Android en trois semaines, et il a raison : on
lui a vendu une privation, pas une émancipation.

**Le renoncement n'est pas une stratégie d'adoption. L'encapsulation en est une.**

### Le principe

Les applications tierces continuent de fonctionner — **toutes**, y compris celles
qui dépendent des services Google. Elles s'exécutent simplement dans une
**enceinte** qui contrôle intégralement ce qu'elles voient et ce qu'elles
atteignent. L'application ignore qu'elle est encerclée ; l'utilisateur, lui, sait
exactement ce qu'elle peut faire.

### Les quatre murs de l'Enceinte

**1. Services Google déprivilégiés.** Les Play Services sont installés comme une
**application ordinaire, non privilégiée**, soumise au même régime de permissions
que n'importe quelle autre. Elle n'obtient rien qu'on ne lui accorde
explicitement.

C'est le renversement décisif, et il corrige l'approche microG. microG
*réimplémente* les API Google en usurpant la signature de Google, ce qui exige
des privilèges au niveau système : le composant le moins digne de confiance du
téléphone hérite des droits les plus élevés, et la compatibilité reste
approximative puisqu'il s'agit d'une imitation. À l'inverse, exécuter le véritable
code sans aucun privilège donne **une compatibilité supérieure et une
architecture plus saine**. Approche éprouvée en production par GrapheneOS.

**2. Réponses vides plutôt que refus.** C'est le mécanisme d'adoption le plus
important du système. Une permission refusée fait planter l'application ;
l'utilisateur accuse SERF et s'en va. L'Enceinte répond donc **autre chose qu'un
refus** :

| L'application demande | Android répond | SERF répond |
|---|---|---|
| Les contacts | Tout, ou une erreur | Un carnet vide, ou les trois contacts choisis |
| Le stockage | Tout, ou une erreur | Un dossier dédié qu'elle croit être le stockage |
| La position | Précise, ou une erreur | La ville, le département, ou une position fixe |
| Les capteurs | Tout, ou une erreur | Des capteurs présents et silencieux |
| Le réseau | Ouvert | Ouvert, filtré, ou coupé — par application |

L'application fonctionne. Elle n'apprend rien. L'utilisateur n'a rien perdu.

**3. Espaces cloisonnés.** Le profil professionnel, le profil personnel et le
profil « toléré » sont des espaces à chiffrement distinct. Une application d'un
espace ne voit ni les données, ni même l'existence des applications des autres.
Un espace peut être gelé d'un geste : ses applications cessent totalement de
s'exécuter.

**4. Journal d'activité.** L'utilisateur voit ce que chaque application a
réellement tenté : quelles permissions, quels serveurs contactés, quel volume
transmis, à quelle heure. La surveillance des surveillants — et le seul moyen de
transformer une promesse de vie privée en fait vérifiable.

### Ce qui est remplacé, et ce qui reste

| Service Google | Substitut souverain | Repli dans l'Enceinte |
|---|---|---|
| Play Store | F-Droid + Aurora Store | Play Store déprivilégié |
| Notifications push | UnifiedPush + relais souverain | Push Google, sans privilège |
| Localisation réseau | BeaconDB (communautaire) | — |
| Cartographie | OpenStreetMap | — |
| Sauvegarde | Chiffrée E2E, hébergeur au choix | — |
| **Attestation forte** | **Aucun** | **Aucun — voir §7** |

La colonne du milieu est le défaut ; celle de droite est la porte de sortie qui
évite l'abandon. L'utilisateur choisit, application par application, et voit ce
que son choix coûte.

### La limite, dite franchement

L'Enceinte résout la grande majorité des cas — tout ce qui échouait par **absence
des services Google**. Elle ne résout **pas** l'attestation matérielle forte
(Play Integrity en niveau matériel) : les applications bancaires, France Identité
et certains DRM vérifient que l'appareil exécute un système certifié par Google,
et refusent quoi qu'il arrive. Aucune ingénierie honnête n'en vient à bout ;
c'est un problème de régulation (DMA), traité en §7.

**Ne jamais laisser croire le contraire.** Un utilisateur qui migre en croyant
garder son application bancaire est un utilisateur perdu, et un détracteur créé.

---

## 5. Périmètre matériel

### Deux périmètres, à ne jamais confondre

**La Régence est universelle. Le système est ciblé.**

L'application Table Ronde — délibérer, voter, vérifier le Registre — fonctionne
sur **tout** : Android ancien, iPhone, navigateur web, matériel d'entrée de gamme,
connexion faible ou absente. **Nul n'est exclu de la gouvernance pour une raison
de matériel.** Ce serait fatal : écarter la moitié de la population parce qu'elle
porte le mauvais téléphone reviendrait à reproduire ce qu'on prétend défaire.

SERF, le système d'exploitation, s'installe sur une liste plus étroite — celle où
le démarrage vérifié est réellement possible, condition de la promesse de sécurité.

**Conséquence stratégique : la Régence recrute, l'OS convertit.** On entre par
l'application, sur le téléphone qu'on a déjà. On migre quand on veut, ou jamais.
Personne n'a à changer d'appareil pour commencer à gouverner.

**Réserve à dire, et à afficher :** un bulletin déposé depuis un appareil non
vérifié offre de moindres garanties d'intégrité du client — le paradoxe du client
([`03-REGENCE.md §5`](03-REGENCE.md)) y est plus aigu. La vérification d'inclusion et le témoignage fonctionnent toujours ;
l'équivalence, non. On l'affiche sobrement, sans faire de la peur un argument de
conversion.

### Les formats visés — et ce qu'ils coûtent vraiment

L'horizon n'est pas le téléphone seul : **téléphone, tablette, montre, poste de
travail.** Tous ne relèvent pas du même chantier, et il faut le dire avant de le
promettre.

| Format | Faisabilité | Ce que ça suppose |
|---|---|---|
| **Téléphone** | Le socle | C'est le chantier décrit ici |
| **Tablette** | Quasi gratuite | Même socle, même code, adaptation d'affichage |
| **Montre** | Plausible, même lignée | Wear OS dérive d'AOSP : le fork est de même nature. Le vrai coût est ailleurs — une montre n'a ni écran ni saisie pour délibérer. Elle peut **notifier et vérifier**, pas porter la Parole |
| **Poste de travail** | **Un second projet, pas un portage** | AOSP n'est pas un système de bureau. Ce serait un Linux durci partageant la Charte, le Registre et la Régence — mais pas le code du téléphone |

**Ce qui se partage entre tous les formats**, et qui est l'essentiel : la Charte,
le Registre, l'identité, le protocole de scrutin, le témoignage. **Ce qui ne se
partage pas** : le socle système.

Dire « SERF tournera sur PC » sans préciser que c'est un second chantier serait
précisément la promesse démentie qui tue un projet de souveraineté au premier
examen technique.

### Le périmètre du système

Un OS sans appareil cible est un exercice de style. Trois stratégies :

1. ~~**Parc d'occasion large**~~ — **écartée.** C'était l'option accessible et
   écologique, et elle tombe pour deux raisons cumulées : le démarrage vérifié y
   est le plus souvent impossible à reverrouiller, et surtout un appareil que son
   constructeur n'alimente plus **ne peut pas rester à jour** sous la couche
   système, ce qu'exige l'article 7 ter. Le renoncement est réel et il faut le
   nommer : on perd l'argument du prolongement de la vie des appareils.
2. **Une liste courte certifiée** — 3 à 5 modèles testés, verified boot garanti.
   Crédible en sécurité, restreint en diffusion.
3. **Partenariat constructeur européen** (Fairphone, Murena, HMD) — la voie
   royale : matériel réparable, bootloader ouvert, image préinstallée. Coûteux
   et lent en négociation.

**Recommandation : (2) pour le premier jalon, (3) comme horizon.** Une liste
courte permet de tenir la promesse de sécurité sans mentir. Le verified boot est
non négociable : sans lui, la Régence n'a aucune garantie que le client de vote
qui s'exécute est bien celui qui a été audité.

---

## 6. La confiance matérielle : mouchards et composants opaques

Tout téléphone contient des composants que son porteur ne contrôle pas et ne peut
pas auditer. Il faut le regarder en face, parce que la promesse de souveraineté s'y
joue autant que dans le logiciel.

**Le modem est un ordinateur autonome.** Il exécute son propre système temps réel,
sous firmware propriétaire signé, certifié par le régulateur. Personne hors du
circuit constructeur ne peut le lire. S'y ajoutent, selon les appareils, un
processeur sécurisé, un contrôleur de capteurs toujours actif, et le firmware de
la carte SIM.

### Ce qui n'est pas vrai

**On ne « désactive » pas un modem par logiciel** si l'on veut du réseau
cellulaire. Le mode avion logiciel est une *requête adressée au modem* — pas une
garantie sur son comportement. Prétendre le contraire serait mentir.

**Et un mouchard imposé au niveau matériel ne se retire pas par du code.** Si un
composant de traçage est soudé et alimenté indépendamment, aucun système
d'exploitation ne l'éteint. C'est une question de matériel et de droit, pas
d'ingénierie logicielle.

### Ce qui est vrai, et faisable

**Principe : zéro confiance matérielle.** On ne cherche pas à faire confiance aux
composants opaques — on les traite comme hostiles et on organise le système en
conséquence.

| Défense | Ce qu'elle obtient |
|---|---|
| **Traiter le modem comme un réseau hostile** | Aucun accès direct à la mémoire, isolation par IOMMU, chiffrement de bout en bout au-dessus de lui. Il achemine des octets qu'il ne peut pas lire |
| **Interrupteurs matériels** | Une coupure physique de l'alimentation du modem, du micro, de la caméra. **Le seul « éteint » qui en soit un.** Existant : Purism Librem 5, MNT Reform |
| **Sélection du matériel** | Privilégier les appareils au démarrage documenté, sans coprocesseur de gestion opaque, et dont le constructeur publie ses sources |
| **Journal d'activité** | Rendre visible ce qui parle, à qui, quand, et combien. On ne peut rien contre ce qu'on ne voit pas |
| **Ne dépendre d'aucun signal externe** | Ni GPS pour l'heure, ni réseau pour délibérer (voir [`08-RESILIENCE.md`](08-RESILIENCE.md)) |

**Le levier qui manque est réglementaire.** L'interdiction d'un traçage matériel
imposé relève du droit européen — RGPD, DMA, directive équipements radio. C'est à
porter politiquement, avec le reste. Un projet de souveraineté qui prétendrait
résoudre cela par du code se raconterait une histoire.

**Ce que SERF peut promettre honnêtement :** aucun mouchard *logiciel*, aucune
télémétrie, aucune porte dérobée (Charte, art. 1 et 2, non révisables) ; et pour
le matériel, l'isolement, la coupure physique quand elle existe, et **la
visibilité de tout le reste**.

---

## 7. Risques structurants

**Play Integrity — risque existentiel.** Si les applications bancaires et
France Identité refusent de s'exécuter, SERF reste un objet militant sans
adoption de masse. Aucune solution technique propre n'existe : c'est un problème
de rapport de force et de régulation (DMA européen). À porter politiquement, pas
techniquement.

**Sécurité de la chaîne de mise à jour.** L'infrastructure OTA de SERF devient
une cible d'État. Une image compromise signée par nos clés atteint tous les
appareils. Exigences : builds reproductibles, signature multi-parties (aucune
personne seule ne peut publier), transparence des binaires.

**Le paradoxe du client de vote.** L'OS est l'urne. Si l'éditeur de l'OS contrôle
le client, il contrôle le scrutin. Ce paradoxe est traité en profondeur dans
[`03-REGENCE.md`](03-REGENCE.md) — c'est le problème le plus difficile du projet,
et il n'a pas de solution parfaite connue.

**Charge de maintenance.** Chaque bulletin de sécurité Android mensuel doit être
fusionné, sur chaque appareil supporté. C'est un travail permanent,
incompressible, qui a tué plus de ROMs alternatives que tout obstacle technique.
