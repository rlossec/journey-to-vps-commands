← [Retour à la feuille TP](../../tp-sheet.md#cmd-1-root)

# Root : « Qui gère `.tech` ? »

```bash
dig NS tech. @a.root-servers.net
```

## Sortie attendue raccourcie

```
;; flags: qr rd; QUERY: 1, ANSWER: 0, AUTHORITY: 4, …
;; WARNING: recursion requested but not available

;; AUTHORITY SECTION:
tech.                   172800  IN      NS      ns01.trs-dns.com.
tech.                   172800  IN      NS      ns01.trs-dns.net.
tech.                   172800  IN      NS      ns10.trs-dns.org.
tech.                   172800  IN      NS      ns10.trs-dns.info.
```

## Lignes importantes

| Fragment | Lecture |
| --- | --- |
| `@a.root-servers.net` | On interroge **un root**, pas le résolveur local. |
| `tech. IN NS ns*.trs-dns.*` | Les serveurs du TLD **`.tech`**. |

← [Retour à la feuille TP](../../tp-sheet.md#cmd-1-root)
