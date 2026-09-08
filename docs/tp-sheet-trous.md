# Feuille TP — à remplir

La partie **1. Résolution DNS** se complète **pendant** la présentation, en regardant les sorties. Le reste : commandes à lancer.

2 terminaux :
- un `bash` sur le VPS
- un `PowerShell` sur Windows

Connexion VPS :

```bash
ssh mbr-********@54.36.100.9 -p 64483
```

🐧 = Linux / macOS · 🪟 = Windows

---

## 1. Résolution DNS

### 1.1. Résolution en 1 commande

🐧

```bash
dig +trace readresolve.tech
```

🪟 *pas d’équivalent*

| Server | NOM |
| ----- | ------------- |
| Serveur Root (`.`) | `________________________________` |
| Serveur TLD (`.tech`) | `________________________________` |
| Serveur Autoritaire | `________________________________` |
| IP VPS | `________________________________` |


### 1.2. Étape par étape

#### 1.2.1. Root : « Quel TLD gère `.tech` ? »

🐧

```bash
dig NS tech. @a.root-servers.net
```

🪟

```powershell
nslookup -type=NS tech. a.root-servers.net
```

Serveurs NS de `.tech` : `________________________________`

On interroge un **root** / un **TLD** / un **autoritaire** (entourer).

#### 1.2.2. TLD : « Quel est le serveur autoritaire ? »

🐧

```bash
dig NS readresolve.tech @ns01.trs-dns.com
```

🪟

```powershell
nslookup -type=NS readresolve.tech ns01.trs-dns.com
```

NS autoritaires : `________________________________`

C’est la réponse finale (IP) ? oui / non

#### 1.2.3. Autoritaire : « Quelle est l’IP ? »

🐧

```bash
dig A readresolve.tech @dns13.ovh.net
```

🪟

```powershell
nslookup -type=A readresolve.tech dns13.ovh.net
```


---

## 2. Enregistrement DNS

Objectif : Découvrir les enregistrements sur le VPS

### 2.1. Records A et AAAA

🐧 **Linux / macOS**

```bash
dig A readresolve.tech
```
```bash
dig AAAA readresolve.tech
```

🪟 **Windows**

```powershell
Resolve-DnsName -Name "readresolve.tech" -Type A
```
```powershell
Resolve-DnsName -Name "readresolve.tech" -Type AAAA
```

### 2.2. Records NS

🐧 **Linux / macOS**

```bash
dig NS readresolve.tech
```

🪟 **Windows**

```powershell
Resolve-DnsName -Name "readresolve.tech" -Type NS
```

### 2.3. Record CNAME (`www`)

🐧 **Linux / macOS**

```bash
dig CNAME www.readresolve.tech
```

🪟 **Windows**

```powershell
Resolve-DnsName -Name "www.readresolve.tech" -Type CNAME
```

### 2.4. À creuser

🐧 **Linux / macOS**

```bash
dig MX readresolve.tech
dig TXT readresolve.tech
dig A www.readresolve.tech
```

🪟 **Windows**

```powershell
Resolve-DnsName -Name "readresolve.tech" -Type MX
Resolve-DnsName -Name "readresolve.tech" -Type TXT
Resolve-DnsName -Name "www.readresolve.tech" -Type A
```

🪟 **Windows** — *pas d’équivalent `whois`*

**À reconnaître**

| Type  | Attendu                                                   |
| ----- | --------------------------------------------------------- |
| A     | `54.36.100.9`, TTL 3600                                   |
| AAAA  | absent                                                    |
| NS    | `dns13.ovh.net`, `ns13.ovh.net`                           |
| MX    | `mx4.mail.ovh.net` , `mx3.mail.ovh.net`                   |
| `www` | **A**  vers la même IP                                    |

Zone dans la console OVH : capture / démo formateur.

---

## 3. Routage Internet

Objectif : l’IP est-elle **joignable**, et **par où** ?

### Ping

🐧 **Linux / macOS**

```bash
ping -c 4 54.36.100.9
```

🪟 **Windows**

```powershell
ping 54.36.100.9
```

### Traceroute

🐧 **Linux / macOS**

```bash
traceroute 54.36.100.9
```

🪟 **Windows**

```powershell
tracert 54.36.100.9
```

### Variante sondes / affichage

🐧 **Linux / macOS**

```bash
traceroute -I 54.36.100.9
```

🪟 **Windows**

```powershell
tracert -d 54.36.100.9
```

---

## 4. Infrastructure OVH

**Pas de commande** sur cette partie : on n’a pas la main sur HCAP / VAC / edge FW.

---

## 5. Configuration du VPS

Objectif : **qui écoute** (ports / sockets), et ce que voit l’extérieur.

### 5a. Ports / sockets — VPS

🐧 **Linux (VPS)**

```bash
ss -tlnp
```

🪟 **Windows** — *pas d’équivalent*

### 5b. Ce que voit l’extérieur — Local

🐧 **Linux / macOS**

```bash
nmap -sV -p 22,80,443 54.36.100.9
```

🪟 **Windows** — *pas d’équivalent*

`nmap` uniquement vers **notre** VPS.
