← [Retour à la feuille TP](../../tp-sheet.md#cmd-2-ns)

# Records NS (`readresolve.tech`)

**But :** qui est autoritaire pour la zone (vue « zone », pas délégation TLD).

```bash
dig NS readresolve.tech
```

## Sortie attendue

```
;; ANSWER SECTION:
readresolve.tech.       3600    IN      NS      ns13.ovh.net.
readresolve.tech.       3600    IN      NS      dns13.ovh.net.
```

## Lignes importantes

| Fragment | Lecture |
| --- | --- |
| `dns13.ovh.net` / `ns13.ovh.net` | Paire de serveur autoritaire d'**OVH** |

← [Retour à la feuille TP](../../tp-sheet.md#cmd-2-ns)
