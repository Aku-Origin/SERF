---
name: coherence
description: Contrôle la cohérence interne du dépôt SERF avant tout commit ou après toute insertion dans un document long — renvois croisés, numéros de section et d'article cités ailleurs, compteurs annoncés dans les titres ou les phrases (« les trois X », « sept écrans », « 56 articles »), dérive de vocabulaire, et contradictions entre CLAUDE.md et les documents. À invoquer dès qu'on insère une section au milieu d'un document, qu'on renumérote, qu'on ajoute un article à la Charte, ou qu'on tranche un terme.
---

# Cohérence

Les documents de SERF se citent les uns les autres par **numéro** — `§7`,
`art. 26 sexies`, `Titre VI bis` — et annoncent des **comptes** dans leurs titres.
Ces deux choses se périment silencieusement dès qu'on insère quoi que ce soit au
milieu. C'est la classe d'erreur la plus fréquente du dépôt : elle ne casse rien,
elle ment.

**Aucune de ces vérifications ne se fait de tête. Toutes se mesurent.**

---

## 1. Renvois croisés

Les fichiers cibles existent-ils encore ?

```bash
cd "D:/Claude/SERF" && grep -rhoE '\]\([^)]+\.md[^)]*\)' --include='*.md' . | tr -d '])' | sed 's/.*(//' | sort -u
```

Attention aux profondeurs : les documents de `docs/` se citent en relatif
(`03-REGENCE.md`) et citent la racine avec `../` (`../CHARTE.md`). Les fichiers
de la racine préfixent par `docs/`.

## 2. Numéros de section cités ailleurs

**Le piège le plus fréquent.** Insérer une section décale toutes les suivantes, et
les renvois d'autres fichiers pointent alors sur le mauvais contenu.

```bash
cd "D:/Claude/SERF" && grep -rn '§[0-9]' --include='*.md' .
```

Pour chaque occurrence, **ouvrir la cible et vérifier que le numéro correspond
toujours au sujet annoncé**. Un renvoi qui pointe vers une section existante mais
sur un autre sujet est pire qu'un lien mort : il ne se signale pas.

Même contrôle pour les articles et les titres de la Charte :

```bash
cd "D:/Claude/SERF" && grep -rn 'art\.\|article [0-9]\|Titre [IVX]' --include='*.md' . | grep -v '^./CHARTE.md'
```

## 3. Compteurs annoncés

Un titre ou une phrase qui annonce un nombre devient faux dès qu'on allonge la
liste. Repérer, puis **compter réellement les éléments**.

```bash
cd "D:/Claude/SERF" && grep -rniE '\b(deux|trois|quatre|cinq|six|sept|huit|neuf|dix|onze|douze|treize|[0-9]+) (renversements?|écrans?|articles?|piliers?|cercles?|règles?|modes?|expressions?|surfaces?|corps|sièges?|points?|titres?)' --include='*.md' .
```

Vérifier notamment : les cinq renversements · les onze écrans · les quatre
expressions · les quatre cercles de publication · les quatre modes de résilience ·
les treize sièges · les douze Corps · le nombre d'articles de la Charte · les ~35
surfaces.

**Règle apprise :** ne pas mettre de compte dans un titre de section quand la liste
est vouée à grandir. *« Les règles à ne pas enfreindre »* survit à un ajout ;
*« Les dix règles »*, non.

## 4. Vocabulaire tranché

Termes décidés, à ne jamais laisser dériver :

| Terme | Sens exact | Erreur à traquer |
|---|---|---|
| **Table Ronde** | Les Treize, jamais l'ensemble des porteurs | Employé pour tous les Régents |
| **Les Régents** | Tous les porteurs admis — **toujours au pluriel, jamais une entité** | Appelés « électeurs », « utilisateurs », « citoyens » ; ou ramassés sous un singulier (« l'Assemblée », « le corps ») |
| **L'Amorçage** | Les 36 premiers mois, avant que le corps électoral tienne debout — Titre IX | Appelé « la Régence », qui désigne la couche du produit et ne s'éteint pas |
| **La Régence** | La couche de gouvernance : Table Ronde, Registre, Scrutin. Permanente | Employée pour la période provisoire du Titre IX |
| **L'Enceinte** | La couche d'encapsulation des applications | Décrite comme un « bac à sable » ou un « blocage » |
| **Le Registre** | Le journal de transparence | Appelé « blockchain », terme explicitement écarté |
| **La Parole** | La délibération **publique**, opposable | Confondue avec la messagerie privée |

```bash
cd "D:/Claude/SERF" && grep -rn 'blockchain\|électeur\|utilisateur\|Assemblée\|Régence provisoire' --include='*.md' . | grep -v 'docs/06-REGISTRE.md' | grep -v 'JOURNAL.md'
```

Les occurrences d'analyse — « pourquoi pas une blockchain » — sont légitimes ; les
occurrences normatives ne le sont pas.

## 5. Contradictions avec les décisions

`CLAUDE.md` porte le tableau des décisions actées. Toute affirmation d'un document
qui le contredit est un défaut : l'un des deux doit céder, et le choix se note au
[`JOURNAL.md`](../../../JOURNAL.md).

Points historiquement fragiles : microG (écarté au profit de l'Enceinte) · l'eID
étatique (écartée au profit du parrainage) · la blockchain (écartée au profit du
journal de Merkle) · Signal (écarté au profit d'Olm/Megolm, faute de pouvoir se
passer d'un numéro de téléphone).

## 6. Titre I

Le Titre I de la Charte est **non révisable**. Tout article ajouté ailleurs qui le
restreindrait, le conditionnerait ou y ménagerait une exception est nul — même
formulé prudemment. Relire les six articles avant toute insertion dans la Charte.

---

## Quand invoquer

- **Avant chaque commit** touchant plusieurs documents.
- **Après toute insertion au milieu** d'un document numéroté — c'est le moment
  exact où les renvois d'autres fichiers deviennent faux.
- **Après tout ajout à la Charte**, pour la numérotation `bis`/`ter` et le Titre I.
- **Après avoir tranché un terme**, pour rattraper les emplois antérieurs.

## Rendre compte

Lister ce qui a été **mesuré**, et ce qui reste incertain. Ne jamais annoncer une
vérification non faite. S'il ne reste rien à corriger, le dire en une ligne — sans
détailler les contrôles passés.
