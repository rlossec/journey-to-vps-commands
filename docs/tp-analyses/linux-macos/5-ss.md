← [Retour à la feuille TP](../../tp-sheet.md#cmd-5-ss)

# Qui écoute mes sockets ?

```bash
ss -tlnp
```

## Sortie attendue (VPS)

```
State   Recv-Q Send-Q  Local Address:Port   Process
LISTEN  0      4096          0.0.0.0:64483  …
LISTEN  0      511         127.0.0.1:9030   …
LISTEN  0      511         127.0.0.1:9050   …
… (autres 127.0.0.1:90xx)
LISTEN  0      511                 *:80     …
LISTEN  0      511                 *:443    …
```

← [Retour à la feuille TP](../../tp-sheet.md#cmd-5-ss)
