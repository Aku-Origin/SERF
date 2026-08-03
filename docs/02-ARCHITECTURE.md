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

**Recommandation : LineageOS comme base, durcissement inspiré de GrapheneOS.**

Le raisonnement : le support matériel est le coût le plus lourd et le moins
gratifiant du projet. LineageOS l'offre gratuitement sur un large parc, y compris
du matériel d'occasion — ce qui sert directement l'argument de souveraineté
(prolonger la vie des appareils plutôt que dépendre d'achats neufs). Le
durcissement, lui, est du code que l'on peut porter incrémentalement, jalon par
jalon.

Le contre-argument mérite d'être entendu : GrapheneOS offre une sécurité
supérieure *tout de suite*, et « sécurité » est un des trois piliers annoncés.
Mais s'enfermer sur Pixel — matériel américain, non disponible en France par
canal souverain — est en contradiction frontale avec le récit du projet.

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
| **Attestation forte** | **Aucun** | **Aucun — voir §6** |

La colonne du milieu est le défaut ; celle de droite est la porte de sortie qui
évite l'abandon. L'utilisateur choisit, application par application, et voit ce
que son choix coûte.

### La limite, dite franchement

L'Enceinte résout la grande majorité des cas — tout ce qui échouait par **absence
des services Google**. Elle ne résout **pas** l'attestation matérielle forte
(Play Integrity en niveau matériel) : les applications bancaires, France Identité
et certains DRM vérifient que l'appareil exécute un système certifié par Google,
et refusent quoi qu'il arrive. Aucune ingénierie honnête n'en vient à bout ;
c'est un problème de régulation (DMA), traité en §6.

**Ne jamais laisser croire le contraire.** Un utilisateur qui migre en croyant
garder son application bancaire est un utilisateur perdu, et un détracteur créé.

---

## 5. Périmètre matériel

Un OS sans appareil cible est un exercice de style. Trois stratégies :

1. **Parc d'occasion large** (via LineageOS) — accessible, écologique, mais
   qualité inégale et verified boot souvent impossible (bootloader non
   reverrouillable sur la majorité des modèles).
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

## 6. Risques structurants

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
