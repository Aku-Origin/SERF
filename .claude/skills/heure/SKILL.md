---
name: heure
description: Donne l'heure et la date locales exactes (fuseau Europe/Paris). À invoquer avant toute écriture datée — entrée de journal, horodatage de décision, message de commit, échéance de Charte — et dès qu'une durée, un délai ou un « aujourd'hui / demain / la semaine prochaine » doit être converti en date absolue. Le contexte de session ne porte que la date d'ouverture et ne se met jamais à jour : ne jamais la supposer encore juste.
---

# Heure

Une seule commande, sans commentaire ni annonce :

```powershell
Get-Date -Format "yyyy-MM-dd HH:mm"
```

Sous Bash :

```bash
date +"%Y-%m-%d %H:%M"
```

## Discrétion

La consultation de l'heure n'est pas un événement. **Ne jamais l'annoncer, ne
jamais la commenter, ne jamais l'afficher seule.** On relève l'heure, on écrit ce
qu'on avait à écrire, et l'horodatage apparaît uniquement là où il a une raison
d'être — en tête d'entrée de journal, dans une date de décision.

Une réponse ne dit jamais « j'ai vérifié l'heure ». Elle porte la bonne date, et
c'est tout.

## Quand relever

- Avant toute entrée de [`JOURNAL.md`](../../../JOURNAL.md).
- Avant d'inscrire une décision datée dans `CLAUDE.md` ou dans la Charte.
- Avant un message de commit qui mentionne une date.
- Dès qu'une échéance relative doit devenir absolue — délais de délibération
  (7 jours), fenêtre de scrutin (72 h), terme de la Régence (36 mois).
- À la reprise d'une session longue, si l'heure relevée date de plusieurs heures.

Une seule fois par écriture. Relever l'heure trois fois dans un même tour est
inutile : la première valeur reste bonne à la minute près.

## Formats

| Usage | Format | Exemple |
|---|---|---|
| Entrée de journal | `AAAA-MM-JJ HH:MM` | `2026-08-03 10:37` |
| Décision dans un document | jour en toutes lettres | `3 août 2026` |
| Nom de fichier ou d'archive | `AAAAMMJJ-HHMM` | `20260803-1037` |

## Fuseau

La machine est en **Europe/Paris** (`Romance Standard Time`, UTC+1 en hiver,
UTC+2 en été). Le projet date en heure de Paris, sans mention du fuseau — sauf
dans un document destiné à des lecteurs hors de France, où l'on précise
`(UTC+2)`.

## Pièges

- **La date du contexte de session est celle de l'ouverture.** Une session qui
  dure franchit minuit sans que rien ne le signale. Sur un travail long, relever
  à nouveau.
- **`Get-Date` sans `-Format` produit une chaîne longue et localisée** qui pollue
  un fichier. Toujours formater.
- **Ne jamais dater par déduction** (« le commit précédent était le 3, donc… »).
  Relever coûte une commande.
