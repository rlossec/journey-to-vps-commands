← [Retour à la feuille TP](../../tp-sheet.md#cmd-2-a-aaaa)

# Records A et AAAA (`readresolve.tech`)

```powershell
Resolve-DnsName -Name "readresolve.tech" -Type A
Resolve-DnsName -Name "readresolve.tech" -Type AAAA
```

## Sortie attendue — A

```
Name                 Type  TTL   Section  IPAddress
----                 ----  ---   -------  ---------
readresolve.tech     A     2863  Answer   54.36.100.9
```

## Sortie attendue — AAAA

```
Name              Type TTL Section   PrimaryServer    NameAdministrator
----              ---- --- -------   -------------    -----------------
readresolve.tech  SOA  300 Authority dns13.ovh.net    tech.ovh.net
```


← [Retour à la feuille TP](../../tp-sheet.md#cmd-2-a-aaaa)
