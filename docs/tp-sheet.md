# Feuille TP — commandes

Version apprenants (à remplir pendant la présentation) : [tp-sheet-trous.md](tp-sheet-trous.md)

On va avoir besoin de 2 terminaux :
- un `bash` sur le VPS
- un `PowerShell` sur Windows (déso Hélène et Amine :broken_heart: )

Donc connectez vous au VPS :

```bash
ssh mbr-********@54.36.100.9 -p 64483
```

Il y a qq fois équivalence mais souvent la nature des commandes différent entre les OS.
Il y a du bon à prendre dans les deux.  

Après chaque commande, un bandeau **🐧 Linux / macOS** et **🪟 Windows** : le lien ouvre l’analyse de **votre** OS.

S’il n’y a pas d’équivalent, c’est indiqué en italique, sans fiche.

Chaque fiche contient :
- un rappel de la commande, 
- un exemple de sortie attendue,
- une analyse des lignes utiles,
- un lien vers cette page 

---

## Introduction

Pas de commandes

---

## 1. Résolution DNS

### 1.1. Résolution en 1 commande

<a id="cmd-1-trace"></a>

🐧 **Linux / macOS** — [Analyse](tp-analyses/linux-macos/1-dig-trace.md)

```bash
dig +trace readresolve.tech
```

🪟 **Windows** — *pas d’équivalent*

Le résultat est abrupt mais tout est là !

### 1.2. Etape par étape

#### 1.2.1. Demander à un root server : "Quel TLD gère .tech ?"

<a id="cmd-1-root"></a>

🐧 **Linux / macOS** — [Analyse](tp-analyses/linux-macos/1-root-ns-tech.md)

```bash
dig NS tech. @a.root-servers.net
```

🪟 **Windows** — [Analyse](tp-analyses/windows/1-root-ns-tech.md)

```powershell
nslookup -type=NS tech. a.root-servers.net
```

#### 1.2.2. Demander à un TLD server : "Quel est le serveur autoritaire ?"

<a id="cmd-1-tld"></a>

🐧 **Linux / macOS** — [Analyse](tp-analyses/linux-macos/1-tld-ns.md)

```bash
dig NS readresolve.tech @ns01.trs-dns.com
```

🪟 **Windows** — [Analyse](tp-analyses/windows/1-tld-ns.md)

```powershell
nslookup -type=NS readresolve.tech ns01.trs-dns.com
```

#### 1.2.3. Demander à un serveur autoritaire : "Quelle est l'IP du serveur final ?"

<a id="cmd-1-auth"></a>

🐧 **Linux / macOS** — [Analyse](tp-analyses/linux-macos/1-auth-a.md)

```bash
dig A readresolve.tech @dns13.ovh.net
```

🪟 **Windows** — [Analyse](tp-analyses/windows/1-auth-a.md)

```powershell
nslookup -type=A readresolve.tech dns13.ovh.net
```

| Server | NOM |
| ----- | ------------- |
| Serveur Root (`.`) | `a.root-servers.net` |
| Serveur TLD (`.tech`) | `ns01.trs-dns.com`, `ns01.trs-dns.net`, `ns10.trs-dns.org`, `ns10.trs-dns.info` |
| Serveur Autoritaire | `dns13.ovh.net`, `ns13.ovh.net` |
| IP VPS | `54.36.100.9` |

---

## 2. Enregistrement DNS

### 2.1. Records A et AAAA

<a id="cmd-2-a-aaaa"></a>

🐧 **Linux / macOS** — [Analyse](tp-analyses/linux-macos/2-a-aaaa.md)

```bash
dig A readresolve.tech
```
```bash
dig AAAA readresolve.tech
```

🪟 **Windows** — [Analyse](tp-analyses/windows/2-a-aaaa.md)

```powershell
Resolve-DnsName -Name "readresolve.tech" -Type A
```
```powershell
Resolve-DnsName -Name "readresolve.tech" -Type AAAA
```

### 2.2. Records NS

<a id="cmd-2-ns"></a>

🐧 **Linux / macOS** — [Analyse](tp-analyses/linux-macos/2-ns.md)

```bash
dig NS readresolve.tech
```

🪟 **Windows** — [Analyse](tp-analyses/windows/2-ns.md)

```powershell
Resolve-DnsName -Name "readresolve.tech" -Type NS
```

### 2.3. Record CNAME (`www`)

<a id="cmd-2-cname"></a>

🐧 **Linux / macOS** — [Analyse](tp-analyses/linux-macos/2-www-cname.md)

```bash
dig CNAME www.readresolve.tech
```

🪟 **Windows** — [Analyse](tp-analyses/windows/2-www-cname.md)

```powershell
Resolve-DnsName -Name "www.readresolve.tech" -Type CNAME
```

### 2.4. Autres

🐧 **Linux / macOS**

```bash
dig MX readresolve.tech
dig TXT readresolve.tech
dig A www.readresolve.tech
whois readresolve.tech
```

🪟 **Windows**

```powershell
Resolve-DnsName -Name "readresolve.tech" -Type MX
Resolve-DnsName -Name "readresolve.tech" -Type TXT
Resolve-DnsName -Name "www.readresolve.tech" -Type A
```

**Bilan**

| Type  | Attendu                                                   |
| ----- | --------------------------------------------------------- |
| A     | `54.36.100.9`, TTL 3600                                   |
| AAAA  | absent                                                    |
| NS    | `dns13.ovh.net`, `ns13.ovh.net`                           |
| MX    | `mx4.mail.ovh.net`, `mx3.mail.ovh.net`                    |
| TXT   | SPF OVH                                                   |
| `www` | **A**   vers la même IP                                   |

---

## 3. Routage Internet

Objectif : l’IP est-elle **joignable**, et **par où** ?

### Ping

<a id="cmd-3-ping"></a>

🐧 **Linux / macOS** — [Analyse](tp-analyses/linux-macos/3-ping.md)

```bash
ping -c 4 54.36.100.9
```

🪟 **Windows** — [Analyse](tp-analyses/windows/3-ping.md)

```powershell
ping 54.36.100.9
```

### Traceroute

<a id="cmd-3-traceroute"></a>

🐧 **Linux / macOS** — [Analyse](tp-analyses/linux-macos/3-traceroute.md)

```bash
traceroute 54.36.100.9
```

🪟 **Windows** — [Analyse](tp-analyses/windows/3-traceroute.md)

```powershell
tracert 54.36.100.9
```

### Variante sondes / affichage

<a id="cmd-3-traceroute-icmp"></a>

🐧 **Linux / macOS** — [Analyse](tp-analyses/linux-macos/3-traceroute-icmp.md)

```bash
traceroute -I 54.36.100.9
```

🪟 **Windows** — [Analyse](tp-analyses/windows/3-traceroute-icmp.md)

```powershell
tracert -d 54.36.100.9
```

---

## 4. Infrastructure OVH

**Pas de commande** sur cette partie : on n’a pas la main sur HCAP / VAC / edge FW. Observation sur captures console OVH.

---

## 5. Configuration du VPS

Objectif : **qui écoute** (ports / sockets), et ce que voit l’extérieur.

Commandes **VPS** = bash Linux (même depuis un PC Windows, via SSH).

### 5a. Ports / sockets — VPS

<a id="cmd-5-ss"></a>

🐧 **Linux (VPS)** — [Analyse](tp-analyses/linux-macos/5-ss.md)

```bash
ss -tlnp
```

🪟 **Windows** — *pas d’équivalent*

### 5b. Ce que voit l’extérieur — Local

<a id="cmd-5-nmap"></a>

🐧 **Linux / macOS** — [Analyse](tp-analyses/linux-macos/5-nmap.md)

```bash
nmap -sV -p 22,80,443 54.36.100.9
```

🪟 **Windows** — *pas d’équivalent*

`nmap` uniquement vers **notre** VPS.

---

## Mémo rapide

| Partie               | 🐧 Linux / macOS                                   | 🪟 Windows                                           |
| -------------------- | -------------------------------------------------- | ---------------------------------------------------- |
| 1 Résolution DNS     | `dig +trace` · `dig @` (root → TLD → autoritaire)  | `nslookup` (root → TLD → autoritaire)                |
| 2 Enregistrement DNS | `dig A/AAAA` · `NS` · `CNAME`                      | `Resolve-DnsName` A/AAAA · NS · CNAME                |
| 3 Routage            | `ping` · `traceroute` · `traceroute -I`            | `ping` · `tracert` · `tracert -d`                    |
| 4 Infra OVH          | captures formateur (pas de CLI)                    | captures formateur (pas de CLI)                      |
| 5 VPS                | `ss` · `nmap`                                      | *pas d’équivalent*                                   |
