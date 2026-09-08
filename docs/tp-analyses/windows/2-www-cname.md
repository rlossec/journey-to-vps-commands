← [Retour à la feuille TP](../../tp-sheet.md#cmd-2-cname)

# Record CNAME (`www.readresolve.tech`)

```powershell
Resolve-DnsName -Name "www.readresolve.tech" -Type CNAME
```

## Sortie attendue

```
Name              Type TTL Section   PrimaryServer
----              ---- --- -------   -------------
readresolve.tech  SOA  300 Authority dns13.ovh.net
```


← [Retour à la feuille TP](../../tp-sheet.md#cmd-2-cname)
