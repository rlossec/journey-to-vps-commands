← [Retour à la feuille TP](../../tp-sheet.md#cmd-1-auth)

# Autoritaire : « Quelle est l’IP ? »

```bash
dig A readresolve.tech @dns13.ovh.net
```

## Sortie attendue raccourcie

```
;; flags: qr aa rd; QUERY: 1, ANSWER: 1, …

;; ANSWER SECTION:
readresolve.tech.       3600    IN      A       54.36.100.9
```

## Lignes importantes

| Fragment                   | Lecture                                     |
| -------------------------- | ------------------------------------------- |
| `@dns13.ovh.net`           | Serveur **autoritaire** (étape précédente). |
| `ANSWER` + `A 54.36.100.9` | **IP publique du VPS.** Fin de chaîne.      |

← [Retour à la feuille TP](../../tp-sheet.md#cmd-1-auth)
