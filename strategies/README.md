# ws-8AM CRT — V1 à V4 en une seule stratégie

`ws-8am-crt-v1-v4.pine` réunit les deux scripts d'origine (V1/V2 et V3/V4) dans une
seule stratégie Pine v6, à lancer **en 5 minutes**.

## Les quatre modèles

| Modèle | Déclencheur | TP/SL par défaut (ticks) |
|---|---|---|
| **V1** | bougie 5m de 08:55 NY : corps haussier → long, baissier → short (repli sur la bougie de 08:50 si 08:55 est plate) | 300 / 200 |
| **V2** | reprise après un stop de V1, **au premier close confirmant** (filtre doji) | 300 / 200 |
| **V3** | range 08:00–09:00 NY : première cassure (sweep), puis entrée sur la cassure inverse | 450 / 450 |
| **V4** | reprise après un stop de V3, **immédiate**, sans confirmation | 300 / 200 |

`Primary model` choisit le trade principal : `V1`, `V3` ou `V1 + V3`.
`enableV2` / `enableV4` activent les reprises.

## Règles communes

- **Une seule position ouverte** à la fois : aucun modèle n'entre pendant qu'un
  trade tourne, ni pendant qu'une confirmation V2 est attendue.
- **Une seule reprise par jour**, V2 et V4 confondues, et jamais après le cutoff
  (11:00 NY par défaut) — c'est la contrainte du V2 d'origine, désormais appliquée
  aussi à V4.
- **Pas d'enchaînement** : seule la sortie au stop d'un trade *principal* (V1/V3)
  arme une reprise. Un V2 ou un V4 stoppé n'arme rien.
- La clôture horaire optionnelle sort avec le commentaire `EOD` (jamais `SL`), donc
  elle n'arme jamais de reprise.

## Différences avec les scripts d'origine

- V4 ne peut plus boucler ni partir après le cutoff (c'était le cas avant).
- Le changement de jour est détecté sur la date NY réelle. L'ancien
  `time("D", sessionTZ)` passait le fuseau dans le paramètre `session` de `time()`,
  donc les remises à zéro quotidiennes du script V3/V4 n'étaient pas fiables.
- V2 et V4 sont activés par défaut ; les ordres portent le nom du modèle
  (`V1 Long`, `V4 Short`, …), visible dans la liste des trades et sur les labels.
