# 05 — Publication, miroirs et continuité

> **Priorité absolue, avant tout développement.** Un projet non publié n'existe
> pas ; un projet publié sur un seul hébergeur n'existe qu'à sa merci.
> Ce document se lit avant d'écrire une ligne de code.

---

## 1. Le principe : la visibilité est la protection

Il y a une tentation naturelle à commencer discrètement et à publier « quand ce
sera prêt ». Pour SERF, c'est l'erreur exacte.

**La discrétion protège une personne. La visibilité protège le projet.** Un
dépôt cloné par trois cents personnes, miroité sur quatre serveurs et archivé par
une institution publique ne disparaît pas sans que cela se sache. Un dépôt
confidentiel, si — et personne ne s'en apercevrait.

Cela ne veut pas dire tout exposer : les clés de signature, elles, restent
strictement hors du dépôt (cf. §5). Cela veut dire que **le code, la Charte, les
décisions et l'historique sont publics dès le premier jour**, et le restent.

C'est aussi ce qu'exige l'article 3 de la [Charte](../CHARTE.md) : ce qui ne peut
être vérifié ne peut être distribué.

---

## 2. Ce que git offre déjà, et qu'on sous-exploite

**Chaque clone est une sauvegarde intégrale.** Historique complet, signatures
comprises. Ce n'est pas une copie partielle : c'est le dépôt entier, réutilisable
seul, capable de redevenir l'origine.

La continuité ne se pense donc pas comme « sauvegarder le dépôt » mais comme
**multiplier les porteurs**. Chaque personne qui clone devient un point de
restauration. La stratégie qui suit ne fait qu'organiser cette propriété.

---

## 3. Les quatre cercles de publication

### Cercle 1 — La façade : GitHub

`https://github.com/Aku-Origin/SERF.git`

C'est là qu'on est trouvé. Portée, référencement, contributions spontanées, outils
d'intégration. Aucune illusion sur sa nature : hébergeur américain, propriété de
Microsoft, soumis au droit américain, avec un historique de retraits sur
injonction.

**Rôle : la vitrine et le point d'entrée. Jamais l'unique dépositaire.**

### Cercle 2 — Le miroir européen : Codeberg

`https://codeberg.org` — Forgejo, porté par **Codeberg e.V.**, association sans
but lucratif de droit allemand, financée par ses membres.

Le contraste avec le cercle 1 est le point : une association ne se rachète pas,
n'a pas d'actionnaires, et n'a aucun intérêt commercial à céder à une pression.
Juridiction européenne, RGPD applicable de plein droit.

**Rôle : le miroir de référence. Si GitHub tombe, l'adresse à donner.**

### Cercle 3 — L'archive patrimoniale : Software Heritage

`https://softwareheritage.org` — Inria + UNESCO, siège à Paris.

**La pièce maîtresse, et la plus négligée.** Software Heritage n'est pas un
hébergeur : c'est l'archive universelle du code source, mission d'intérêt général,
vocation patrimoniale. Elle moissonne et **conserve définitivement** tout dépôt
git public. On peut déclencher l'archivage soi-même, gratuitement, par une simple
requête.

Ce que ça change : on ne demande pas à une archive patrimoniale de « retirer » un
projet comme on le demande à un hébergeur commercial. Chaque instantané reçoit un
identifiant permanent (SWHID) citable dans un texte, une thèse, un dépôt légal.

Pour un projet de souveraineté française, s'ancrer dans une archive publique
française et onusienne n'est pas seulement prudent — c'est cohérent.

**Rôle : la permanence. Ne sert pas à travailler ; sert à ce que ça survive.**

### Cercle 4 — Le hors-serveur : Radicle

`https://radicle.xyz` — git en pair-à-pair, sans serveur central.

Le dépôt vit dans le réseau des personnes qui le suivent. Il n'y a aucune entité
à qui adresser une demande de retrait, parce qu'il n'y a aucune entité.

Écosystème plus jeune, ergonomie plus rude, audience restreinte. Ce n'est pas un
lieu de travail — c'est **la garantie de dernier recours**, celle qui reste quand
les trois autres cercles ont cédé.

**Rôle : l'assurance. À poser une fois, à vérifier chaque trimestre.**

---

## 4. Ordre d'exécution

Dans cet ordre, sans en sauter.

**Étape 1 — Régler l'identité de signature.** Avant le premier commit, pas après :
réécrire l'auteur d'un historique déjà poussé est pénible et laisse des traces
dans les miroirs.

```bash
git -C "D:/Claude/SERF" config user.name "Père Sans-Ciel"
```

L'adresse de courriel doit être une adresse dédiée au projet — jamais une adresse
personnelle, qui serait inscrite à jamais dans chaque commit de chaque clone :

```bash
git -C "D:/Claude/SERF" config user.email "sans-ciel@aku-origin.org"
```

> **À arbitrer avant de commiter.** Soit une adresse `@users.noreply.github.com`
> fournie par GitHub (aucune boîte à gérer, mais elle lie l'identité au compte
> GitHub), soit une adresse sur un domaine du projet (indépendante des
> hébergeurs, mais il faut le domaine). La seconde vaut mieux pour un projet qui
> se veut souverain.

**Étape 2 — Premier commit signé.** Voir §5 pour la clé.

**Étape 3 — Pousser sur GitHub.** Le dépôt existe et est vide.

```bash
git -C "D:/Claude/SERF" push -u origin main
```

**Étape 4 — Créer et pousser le miroir Codeberg**, puis déclarer les deux dépôts
l'un dans l'autre : chaque README pointe vers tous les miroirs, pour qu'aucun
point d'entrée ne soit un cul-de-sac.

**Étape 5 — Déclencher l'archivage Software Heritage.** Une requête suffit ; à
refaire après chaque jalon.

```bash
curl -X POST "https://archive.softwareheritage.org/api/1/origin/save/git/url/https://github.com/Aku-Origin/SERF/"
```

**Étape 6 — Poser Radicle**, une fois, et noter l'identifiant du dépôt dans le
README.

**Étape 7 — Automatiser la synchronisation des miroirs.** Une action
d'intégration continue qui pousse vers Codeberg à chaque commit sur `main`. Un
miroir qu'il faut penser à mettre à jour est un miroir périmé.

---

## 5. Les clés — le seul secret du projet

Tout est public dans SERF **sauf les clés privées**. Elles sont la racine de
confiance : leur fuite permet de forger une version de SERF que les appareils
accepteraient au démarrage vérifié. Le `.gitignore` les couvre ; le vérifier
avant chaque commit reste un réflexe, pas une confiance.

**Trois usages, trois clés distinctes** — ne jamais réutiliser :

| Clé | Rôle | Détention |
|---|---|---|
| Signature des commits | Prouver qui a écrit quoi | L'auteur |
| Signature des étiquettes de version | Marquer un état comme officiel | Multipartite |
| Signature des images système | Racine de confiance du démarrage vérifié | **3 porteurs distincts** (Charte, art. 25) |

La règle des trois porteurs de l'article 25 a un objet précis, qui vaut d'être
redit ici : **il doit falloir un complot, pas une trahison** — ni une contrainte
exercée sur une seule personne, ni une seule négligence.

**Publier les clés publiques dans le dépôt** (`keys/*.pub`, jamais les privées).
C'est ce qui permettra, plus tard, à quiconque de distinguer un commit authentique
d'un commit forgé — y compris si l'auteur d'origine n'est plus là pour le dire.

---

## 6. Continuité — le jour où le porteur n'est plus là

Écrit sans dramatiser. C'est de la planification de succession, la même que
tout projet libre sérieux devrait faire et que presque aucun ne fait.

**La vraie réponse est déjà écrite, et ce n'est pas un dispositif : c'est la
documentation.** Un inconnu qui clone ce dépôt trouve la vision, l'architecture,
les décisions *avec leur pourquoi*, la Charte et la feuille de route. Il peut
reprendre sans avoir connu personne. C'est cela, et rien d'autre, qui fait qu'un
projet survit à quelqu'un.

Ce que la Charte prévoit déjà : le registre répliqué en juridictions distinctes
(art. 27), l'interdiction de dépendre d'une personne morale unique (art. 28), la
continuité malgré la disparition de la structure porteuse (art. 29), et le droit
de bifurquer opposable à tous (art. 5).

Ce qu'il reste à poser :

**Un document de succession** — `SUCCESSION.md`, public, nommant : qui détient
quelle clé, quels miroirs existent, quel est l'ordre de reprise, et ce que
l'auteur souhaite qu'il advienne du projet. Un texte qu'un tiers peut appliquer
seul.

**Une preuve de vie sobre.** Un commit signé au moins tous les 90 jours. Passé ce
délai sans signe, les porteurs de clés appliquent le document de succession. Pas
d'automatisme : un dispositif qui se déclenche seul se déclenche surtout à
tort — une panne, un voyage, une hospitalisation. Un délai long, constaté par des
humains, vaut mieux qu'un interrupteur nerveux.

**Le legs des accès.** Comptes d'hébergement, domaine, boîte du projet : consignés
dans un gestionnaire de secrets dont l'accès est réparti entre les mêmes trois
porteurs. **Ces éléments ne figurent jamais dans le dépôt.**

**La clause à écrire dans les statuts.** La structure porteuse ne possède pas le
commun ; elle en est mandataire. Sa disparition n'emporte rien. À faire figurer
noir sur blanc lors de la rédaction juridique.

---

## 7. La signature — une charge, non un masque

Le projet est signé **Père Sans-Ciel**, ou **Le Sans-Ciel** — *rien au-dessus* :
ni plafond, ni seigneur. Le sens du nom est développé dans
[la vision](01-VISION.md).

**Ce n'est pas un pseudonyme au sens ordinaire : c'est une charge, et une charge
se transmet.** La distinction n'est pas de vocabulaire, elle règle le problème du
§6 par le haut. Un masque protège une personne et disparaît avec elle ; une
charge survit à celui qui la porte. Le jour où le porteur s'arrête, la signature
ne s'éteint pas — elle passe.

Conséquences à câbler :

- **La signature n'atteste pas d'une personne, mais d'une fonction.** « Le
  Sans-Ciel » engage celui qui exerce la charge au moment où il signe. Les textes
  fondateurs restent signés sans avoir à être réattribués.
- **La transmission est un acte documenté**, inscrit au registre et contresigné
  par les porteurs de clés (§5) : sans quoi n'importe qui pourrait revendiquer la
  charge. C'est la clé qui authentifie, jamais le nom seul.
- **Le pseudonymat devient secondaire à la sécurité du projet.** Si la signature
  n'est pas une personne, la démasquer n'ouvre rien : elle ne donne aucun pouvoir
  sur le dépôt, dont l'autorité tient aux clés réparties et aux miroirs.

C'est la réponse la plus solide à la question du §6 : la continuité ne repose ni
sur un dispositif automatique, ni sur la longévité de quelqu'un, mais sur le fait
que **la charge est déjà conçue pour changer de mains**.

### Cloisonnement

**Aucune autre identité, aucun autre pseudonyme du porteur ne figure dans ce
dépôt.** Un dépôt public, miroité et archivé de façon permanente ne se corrige
pas : une seule mention lie deux identités pour toujours, dans tous les clones.

La règle retenue : **une seule identité par dépôt.** Compte dédié, adresse de
courriel dédiée, aucune réutilisation d'un compte existant, aucune mention croisée
dans un commentaire, un message de commit ou un fichier de configuration.

C'est une règle d'hygiène, pas un interdit : le porteur peut décider de signer
sous plusieurs noms. Mais la décision se prend **avant** le premier push, parce
qu'elle ne se défait pas après.

### Ce que la charge ne protège pas

Même transmissible, la signature laisse des traces qui, elles, désignent une
personne :

- Les métadonnées de commit — horodatage, fuseau, cadence de travail — dessinent
  un emploi du temps.
- L'adresse de courriel du commit est **inscrite à jamais** dans chaque clone. Une
  seule occurrence d'une adresse personnelle suffit, et elle ne se retire plus.
- Le compte qui pousse, le domaine qui héberge, le paiement qui l'a acheté sont
  autant de liens.
- Le style d'écriture est identifiant, et le corpus s'allonge à chaque document.

**Règles de tenue :** aucune donnée personnelle dans le dépôt, jamais, y compris
dans un fichier de configuration ou un commentaire ; une adresse dédiée au
projet ; ne pas mélanger ce compte avec un compte personnel existant.

Le pseudonymat tient contre la lecture distraite. Il ne tient pas contre un examen
déterminé. Ce qui protège, à ce niveau-là, c'est la §1 : que le projet soit trop
public et trop reproduit pour qu'il serve à quoi que ce soit de s'en prendre à une
personne.
