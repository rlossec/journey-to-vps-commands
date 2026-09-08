← [Retour à la feuille TP](../../tp-sheet.md#cmd-1-tld)

# TLD : « Qui est autoritaire pour `readresolve.tech` ? »

```bash
dig NS readresolve.tech @ns01.trs-dns.com
```

## Sortie attendue raccourcie

```
;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 2, …
;; WARNING: recursion requested but not available

;; AUTHORITY SECTION:
readresolve.tech.       900     IN      NS      ns13.ovh.net.
readresolve.tech.       900     IN      NS      dns13.ovh.net.
```

## Lignes importantes

| Fragment | Lecture |
| --- | --- |
| `@ns01.trs-dns.com` | On interroge **un TLD** `.tech` (étape précédente). |
| `ANSWER: 0` + `AUTHORITY` | Encore une **délégation**, pas la réponse finale. |
| `dns13.ovh.net` / `ns13.ovh.net` | Serveurs **autoritaires** OVH pour le domaine. |

← [Retour à la feuille TP](../../tp-sheet.md#cmd-1-tld)
