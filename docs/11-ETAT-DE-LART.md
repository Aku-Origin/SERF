# 11 — État de l'art

> Recherche du 3 août 2026. Ce que d'autres ont déjà tenté, cassé, ou prouvé.
> **Deux conclusions remettent en cause des décisions prises le matin même.**
>
> Toute affirmation ici est sourcée. Ce qui n'est pas sourcé est signalé comme
> hypothèse.

---

## 1. Le vote vérifiable

### Belenios — et la faille qui nous concerne directement

Belenios est un protocole de vote vérifiable développé en France, **déployé dans
plus de 200 élections**. Il vise le secret du vote et la vérifiabilité intégrale,
y compris face à un serveur de vote compromis.

**Mais une analyse formelle a mis au jour une hypothèse de confiance absente de
l'analyse papier :**

> *« Le secret du bulletin ne tient pas si le registrar se comporte mal, alors
> même que son rôle semble se limiter à fournir les garanties d'éligibilité. »*
> — analyse à preuves mécanisées, IEEE CSF
> ([source](https://ieeexplore.ieee.org/document/8429313/))

**C'est notre architecture.** L'organe qui délivre le jeton d'éligibilité signé en
aveugle (Charte, art. 10) *est* ce registrar. Nous avons donc, depuis ce matin, la
même faille latente — et elle est d'autant plus grave que notre article 10 affirme
que la séparation est « cryptographique et non déclarative ».

**Ce qu'il faut corriger :** le registrar ne peut pas être un organe unique. Il
doit être **éclaté en seuil** — k parties sur n, aucune ne détenant seule de quoi
lier un jeton à une personne. Le principe est le même que pour les clés de
dépouillement, et pour la même raison : il doit falloir un complot.

**Leçon de méthode, plus large :** une analyse à la main manque des hypothèses
qu'une preuve mécanisée trouve. Pour un système de vote, **la vérification formelle
n'est pas un luxe académique** — c'est ce qui distingue « nous n'avons pas trouvé
de faille » de « il n'y en a pas dans ce modèle ».

### ElectionGuard, et un précédent français

ElectionGuard (Microsoft Research) a été employé pour des votes civiques à
**Neuilly-sur-Seine en 2021**, puis dans l'Idaho, l'Utah et le Maryland ; les
enseignements de ces déploiements ont nourri une version 2 simplifiée
([USENIX Security 24](https://www.usenix.org/system/files/usenixsecurity24-benaloh.pdf)).

Un précédent français de vote vérifiable en collectivité existe donc déjà. C'est
utile à savoir : SERF n'aurait pas à défricher seul le terrain institutionnel.

### Les codes de retour — la réponse au paradoxe du client

**Le document [`03-REGENCE.md §5`](03-REGENCE.md) affirmait que le paradoxe du
client n'a pas de solution connue. C'est faux, et il faut le corriger.**

Le mécanisme, déployé en Suisse depuis Neuchâtel 2015 puis par La Poste suisse :

> L'électeur reçoit **par courrier**, sur un canal indépendant, une feuille de
> codes personnalisés. Après avoir déposé son bulletin, le client affiche des
> codes. S'ils correspondent à ceux du papier, le bulletin déposé est bien celui
> voulu, avec forte probabilité.
> ([Neuchâtel 2015](https://link.springer.com/chapter/10.1007/978-3-319-22270-7_1) ·
> [mécanisme à codes de retour](https://arxiv.org/pdf/1707.03632))

**Pourquoi ça marche :** les codes n'ont jamais transité par l'ordinateur. Un
logiciel malveillant qui contrôle entièrement le client ne peut pas afficher un
code qu'il n'a aucun moyen de connaître. C'est le seul mécanisme connu qui
contraigne un client compromis **sans lui faire confiance**.

**Le défaut documenté, et sa leçon.** Le protocole suisse a été critiqué parce que
**son mode d'emploi n'est expliqué qu'en ligne**, sur le site de vote :

> *« Le protocole ne vous est pas expliqué sur le papier reçu par courrier. Il ne
> vous est expliqué qu'en ligne, quand vous visitez le site de vote. »*
> — Princeton CITP
> ([source](https://blog.citp.princeton.edu/?p=17334))

Celui qui contrôle le site contrôle donc l'explication, et peut convaincre
l'électeur qu'un code faux est bon. **L'explication doit voyager avec le papier.**

**Ce que ça donne pour SERF.** Le papier est déjà dans notre architecture —
ancrage trimestriel (art. 26 octies), mode dégradé papier (doc. 08). Les codes de
retour s'y insèrent naturellement, et l'exigence d'intelligibilité (art. 14 bis)
impose déjà que l'explication soit sur la feuille, pas seulement à l'écran.

**Réserve :** cela suppose un canal postal, donc une adresse — ce qui heurte le
pseudonymat du corps électoral. À concevoir : codes remis en main propre à
l'admission par les trois parrains, ou déposés hors-ligne. **Point ouvert.**

### Estonie — l'échec dont il faut se souvenir

L'Estonie vote par Internet depuis 2005. En 2014, une équipe conduite par Alex
Halderman et Harri Hursti observe une élection sur place et relève de nombreuses
vulnérabilités ainsi que des pratiques opérationnelles très négligentes
([Verified Voting](https://verifiedvoting.org/international-internet-voting/)).

Plus grave et plus récent :

> L'examen systématique de la phase de traitement des bulletins a révélé des
> vulnérabilités permettant à **un initié malveillant de remplacer la totalité des
> bulletins sans être détecté**.
> ([IEEE](https://ieeexplore.ieee.org/document/10811882/))

**Vingt ans de déploiement national n'ont pas suffi à rendre ce système sûr.**
C'est l'argument le plus fort en faveur de notre discipline : vérifiabilité de
bout en bout, registre public, et surtout **détection par des tiers plutôt que
confiance dans l'exploitant**.

### Retenu pour SERF

| Décision | Fondement |
|---|---|
| **Registrar en seuil, jamais unique** | Faille Belenios — correction de l'art. 10 |
| **Codes de retour, avec explication sur le papier** | Neuchâtel/Suisse — corrige le paradoxe du client |
| **Vérification formelle du protocole** | Ce qui a révélé la faille Belenios |
| **Ne jamais réimplémenter la cryptographie** | Partir de Belenios, décision inchangée |

---

## 2. Les précédents de gouvernance numérique

### vTaiwan — l'échec qui valide notre article 35

vTaiwan est la référence mondiale de la délibération numérique. Son bilan est
sans ambiguïté :

> vTaiwan, née d'un partenariat entre le gouvernement et la société civile, repose
> aujourd'hui **entièrement sur des bénévoles**, ce qui limite sa portée. **Le
> gouvernement n'est pas tenu de prendre en considération** les discussions ni le
> consensus atteint sur la plateforme.
> ([People Powered](https://www.peoplepowered.org/news-content/digital-participation-case-study-taiwan))

**C'est exactement le trou que l'article 35 comble.** Une délibération que
personne n'est tenu de considérer s'éteint — non par désintérêt, mais parce que
participer devient rationnellement absurde. L'obligation de réponse motivée sous
trente jours, et le point de défiance en cas de silence, ne sont donc pas une
élégance : **c'est la différence entre un dispositif vivant et vTaiwan.**

### Pol.is — deux mécanismes à reprendre

Pol.is, l'outil de délibération de vTaiwan :

> Pol.is **interdit les réponses aux commentaires**, ce qui réduit le
> harcèlement, et **regroupe les personnes aux schémas de vote similaires** afin
> de visualiser les zones d'accord et de désaccord.
> ([People Powered](https://www.peoplepowered.org/news-content/digital-participation-case-study-taiwan))

Deux idées à intégrer à **La Parole** ([`09-BRIEF-DESIGN.md §5.4`](09-BRIEF-DESIGN.md)) :

**Pas de fil de réponses.** On dépose une position, on ne réplique pas. C'est
contre-intuitif et cela supprime d'un coup la dynamique d'affrontement qui rend
tout forum inutilisable. Cohérent avec notre refus du classement algorithmique.

**Cartographier l'accord, pas le conflit.** Regrouper les participants par
proximité de vote fait apparaître ce sur quoi des camps opposés s'accordent
déjà — l'inverse exact de ce que produit un fil de discussion. C'est un usage
d'analyse **qui ne classe rien et n'amplifie rien** : il décrit.

### Decidim — l'avertissement

Decidim est la plateforme de démocratie participative la plus déployée
institutionnellement. La critique académique est sévère :

> Un décalage entre les principes technopolitiques de conception démocratique et
> les complexités politico-institutionnelles, **les possibilités de participation
> étant souvent réduites à quelques options de faible qualité**, où les
> participants ne peuvent pas exprimer directement leurs préférences et où **le
> débat ouvert est absent ou très limité**.
> ([SpringerLink](https://link.springer.com/chapter/10.1007/978-3-031-50784-7_5))

**L'avertissement est direct :** une plateforme adoptée par des institutions est
configurée *par* ces institutions, qui réduisent la participation à ce qu'elles
sont prêtes à concéder. L'outil ne protège pas de cela.

**Ce que SERF en tire :** la Charte doit contraindre l'organe, pas seulement
outiller l'assemblée. C'est déjà le cas — art. 35, 37 (la Table Ronde ne peut pas
modifier les seuils qui l'atteignent), 38 (compteur de défiance). **Le succès de
Decidim en déploiement et son échec en qualité démocratique valident ce
verrouillage.**

Son succès réel, en revanche, est la standardisation du **budget participatif** —
ce qui conforte nos scrutins de répartition (art. 21).

### La fracture d'accès

> Les générations plus âgées et les habitants des zones rurales rencontrent
> davantage d'obstacles pour accéder à ces plateformes ou les utiliser.
> ([People Powered](https://www.peoplepowered.org/news-content/digital-participation-case-study-taiwan))

Confirme la portée de l'article 6 et du niveau d'accessibilité visé
([`09-BRIEF-DESIGN.md §6`](09-BRIEF-DESIGN.md)) — et que le mode papier n'est pas
seulement un secours technique : **c'est aussi une voie d'accès.**

---

## 3. Le cadre juridique français

### L'association loi 1901 peut se lier à ses votes

C'est la réponse à l'arbitrage n°1 de la feuille de route, et elle est favorable.

> La loi de 1901 **ne définit pas les organes de gouvernance** d'une association.
> Une association est donc libre de déterminer, dans ses statuts, ses instances
> dirigeantes et leurs attributions. […] **Les statuts ont force de loi pour les
> membres.**
> ([Associathèque](https://www.associatheque.fr/fr/creer-association/statuts-clauses-recommandees.html) ·
> [Associations.gouv.fr](https://associations.gouv.fr/la-loi-1901-et-la-liberte-dassociation))

La liberté contractuelle est quasi totale. **Rien n'empêche des statuts de prévoir
que la structure est liée par les scrutins contraignants de la Charte** —
dissolution de la Table Ronde, révision de la Charte. Cela devient alors une
obligation statutaire, opposable devant le juge civil.

**Conséquence :** l'article 34 peut être tenu pour de bon. Les votes contraignants
le sont réellement, et pas seulement moralement.

**À vérifier avec un juriste**, non par recherche documentaire : l'articulation
avec la responsabilité des dirigeants, la validité d'un vote dématérialisé
pseudonyme au regard du droit associatif, et la rédaction exacte de la clause de
liaison.

### RGPD et registre permanent — notre solution est celle de la CNIL

La CNIL a analysé la contradiction entre immuabilité et droit à l'effacement, et
retient exactement le mécanisme inscrit à l'article 26 quinquies :

> La CNIL a pris connaissance de solutions […] permettant de se rapprocher des
> exigences de conformité du RGPD, notamment **en coupant l'accessibilité de la
> donnée** selon le format choisi : *engagement cryptographique, chiffrement,
> empreinte issue d'une fonction de hachage à clé*.
>
> Avec une empreinte issue d'une fonction de hachage à clé et une clé privée, le
> responsable de traitement peut rendre la donnée **quasi inaccessible**. […] Ce
> n'est pas un effacement au sens strict — il reste une trace — mais retrouver
> l'information inscrite sera irréalisable.
> ([CNIL](https://www.cnil.fr/fr/technologies/blockchain-et-rgpd-quelles-solutions-pour-un-usage-responsable-en-presence-de-donnees-personnelles))

**Notre article 26 quinquies décrit précisément cela** : engagement
cryptographique au Registre, correspondance tenue dehors, destruction à la sortie.
Nous sommes alignés sur la doctrine de l'autorité, ce qui est une position bien
plus solide qu'une interprétation personnelle.

Des lignes directrices européennes sur chaînes de blocs et RGPD (CEPD 02/2025)
prolongent cette analyse
([synthèse](https://silexo.fr/article/149/blockchain-et-rgpd-analyse-des-lignes-directrices-02-2025-du-cepd-et-enjeux-de-souverainete-numerique)) —
**à lire intégralement avant d'écrire le Registre.**

---

## 4. La faisabilité du socle — la décision à rouvrir

### Ce que j'avais recommandé, et pourquoi c'était fragile

[`02-ARCHITECTURE.md §2`](02-ARCHITECTURE.md) recommande **LineageOS** comme base,
en écartant GrapheneOS au motif qu'il enferme sur du matériel Pixel — américain,
contradictoire avec le récit de souveraineté.

Deux faits invalident ce raisonnement.

### Fait 1 — LineageOS ne peut pas tenir la promesse

> Les ROM non officielles telles que LineageOS **échouent à l'attestation
> matérielle**, ce qui empêche l'utilisateur d'employer des applications tierces
> qui reposent sur l'API — principalement les applications bancaires.
> ([Play Integrity API](https://en.wikipedia.org/wiki/Play_Integrity_API))

Ce n'est pas un défaut de configuration : les ROM personnalisées échouent aux
niveaux *Device* et *Strong* parce qu'elles **rompent la chaîne de certification**.
Or la promesse de sécurité de SERF repose sur le démarrage vérifié, que la plupart
des appareils LineageOS ne permettent même pas de reverrouiller.

**Un socle qui ne peut ni reverrouiller le démarrage, ni attester, ne peut porter
aucun des trois piliers.**

### Fait 2 — l'objection « Pixel uniquement » est en train de tomber

> GrapheneOS est passé à un modèle où il prendra en charge d'autres appareils dès
> lors que le matériel et les partenaires constructeurs satisfont ses exigences ;
> en octobre 2025 un partenariat avec un constructeur majeur est annoncé, et en
> **mars 2026 ce partenaire est Motorola**, pour des appareils visés **fin 2026 /
> début 2027**.
> ([Elvion Pulse](https://elvionpulse.com/grapheneos-supported-devices-list/) ·
> [WebProNews](https://www.webpronews.com/motorola-and-grapheneos-team-up-first-non-pixel-phones-set-for-official-privacy-os-support-in-2027/))

Notre jalon 2 (la ROM) vient **après** le jalon 1 (le scrutin prouvé hors OS) —
soit dans plusieurs années. À cette échéance, le verrou Pixel n'existera
probablement plus.

### Fait 3 — et une voie que j'ignorais

> Les applications qui utilisent l'API Play Integrity peuvent prendre en charge
> GrapheneOS **en utilisant l'API d'attestation matérielle standard d'Android et
> en autorisant les clés de signature officielles**. L'attestation matérielle
> d'Android est une forme d'attestation bien plus forte que Play Integrity, avec
> **la capacité de mettre en liste blanche les clés de systèmes alternatifs**.
> ([GrapheneOS](https://grapheneos.org/articles/attestation-compatibility-guide))

**Il existe donc une voie technique légitime** pour qu'une banque prenne en charge
un OS alternatif — sans contournement, avec une attestation plus forte que celle
de Google. Ce n'est pas une lutte perdue d'avance : c'est un travail de plaidoyer
appuyé sur un standard existant.

Et le résultat est déjà là : en 2026, la plupart des grandes applications
bancaires fonctionnent sur GrapheneOS via les services Google déprivilégiés — dont
la plupart des banques de détail européennes
([liste 2026](https://vucense.com/tech-reviews/mobile-gear/grapheneos-banking-apps-2026-complete-compatibility-list/)).
**C'est la validation en production de l'Enceinte.**

### Recommandation révisée

| | Ancienne décision | Décision révisée |
|---|---|---|
| Socle | LineageOS, durcissement inspiré de GrapheneOS | **Lignée GrapheneOS**, appareils issus des partenariats constructeurs |
| Matériel | Liste courte, puis partenariat européen | **Attendre le jalon 2** ; viser les appareils à démarrage vérifié reverrouillable |
| Attestation | « Problème non résolu, risque existentiel » | **Voie existante** : attestation matérielle standard + liste blanche de nos clés. Plaidoyer, pas contournement |

**À trancher par Diego** — c'est une révision de fond, pas un détail. Voir §5.

---

## 5. Ce qui change, et ce qui reste ouvert

### Corrections à porter

1. **Article 10 de la Charte** — le registrar doit être éclaté en seuil. Faille
   Belenios. *Urgent : c'est une faille active dans notre texte.*
2. **[`03-REGENCE.md §5`](03-REGENCE.md)** — le paradoxe du client n'est plus « sans
   solution connue ». Les codes de retour sont une réponse déployée. À réécrire.
3. **[`02-ARCHITECTURE.md §2`](02-ARCHITECTURE.md)** — rouvrir le choix du socle.
4. **[`09-BRIEF-DESIGN.md §5.4`](09-BRIEF-DESIGN.md)** — La Parole : pas de fil de
   réponses, et cartographie des accords à la manière de Pol.is.
5. **[`ROADMAP.md`](../ROADMAP.md)** — l'arbitrage « portée des votes » est
   résolu : une association loi 1901 peut statutairement se lier.

### Restent ouverts

- **La remise des codes de retour** sans adresse postale, donc sans rompre le
  pseudonymat. Piste : remise par les trois parrains à l'admission.
- **La vérification formelle** de notre protocole — qui, quand, à quel coût.
- **Les lignes directrices CEPD 02/2025**, à lire intégralement.
- **La relecture juridique**, qui ne se fait pas par recherche documentaire.

---

## Sources

- [Machine-Checked Proofs for Belenios — IEEE CSF](https://ieeexplore.ieee.org/document/8429313/)
- [Belenios](https://www.belenios.org/)
- [ElectionGuard — USENIX Security 24](https://www.usenix.org/system/files/usenixsecurity24-benaloh.pdf)
- [Neuchâtel 2015 — Cast-as-Intended Verification](https://link.springer.com/chapter/10.1007/978-3-319-22270-7_1)
- [Cast-as-Intended with Return Codes — arXiv](https://arxiv.org/pdf/1707.03632)
- [Switzerland's e-voting implementation blunder — Princeton CITP](https://blog.citp.princeton.edu/?p=17334)
- [Estonian i-voting ballot integrity — IEEE](https://ieeexplore.ieee.org/document/10811882/)
- [International Internet Voting — Verified Voting](https://verifiedvoting.org/international-internet-voting/)
- [vTaiwan case study — People Powered](https://www.peoplepowered.org/news-content/digital-participation-case-study-taiwan)
- [Decidim, a Technopolitical Network — SpringerLink](https://link.springer.com/chapter/10.1007/978-3-031-50784-7_5)
- [Loi 1901 et liberté d'association — Associations.gouv.fr](https://associations.gouv.fr/la-loi-1901-et-la-liberte-dassociation)
- [Statuts, clauses recommandées — Associathèque](https://www.associatheque.fr/fr/creer-association/statuts-clauses-recommandees.html)
- [Blockchain et RGPD — CNIL](https://www.cnil.fr/fr/technologies/blockchain-et-rgpd-quelles-solutions-pour-un-usage-responsable-en-presence-de-donnees-personnelles)
- [Lignes directrices CEPD 02/2025 — analyse](https://silexo.fr/article/149/blockchain-et-rgpd-analyse-des-lignes-directrices-02-2025-du-cepd-et-enjeux-de-souverainete-numerique)
- [Attestation compatibility guide — GrapheneOS](https://grapheneos.org/articles/attestation-compatibility-guide)
- [Play Integrity API — Wikipedia](https://en.wikipedia.org/wiki/Play_Integrity_API)
- [GrapheneOS supported devices 2026 — Elvion Pulse](https://elvionpulse.com/grapheneos-supported-devices-list/)
- [Motorola × GrapheneOS — WebProNews](https://www.webpronews.com/motorola-and-grapheneos-team-up-first-non-pixel-phones-set-for-official-privacy-os-support-in-2027/)
- [Banking apps on GrapheneOS 2026](https://vucense.com/tech-reviews/mobile-gear/grapheneos-banking-apps-2026-complete-compatibility-list/)
