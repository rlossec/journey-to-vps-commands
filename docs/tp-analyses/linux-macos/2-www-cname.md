← [Retour à la feuille TP](../../tp-sheet.md#cmd-2-cname)

# Record CNAME (`www.readresolve.tech`)

```bash
dig CNAME www.readresolve.tech
```

## Sortie attendue

```
;; flags: … ANSWER: 0, AUTHORITY: 1, …

;; QUESTION SECTION:
;www.readresolve.tech.          IN      CNAME

;; AUTHORITY SECTION:
readresolve.tech.       300     IN      SOA     dns13.ovh.net. …
```

## Lignes importantes

| Fragment | Lecture |
| --- | --- |
| Conclusion | `www` est un **A** vers `54.36.100.9` |

← [Retour à la feuille TP](../../tp-sheet.md#cmd-2-cname)
