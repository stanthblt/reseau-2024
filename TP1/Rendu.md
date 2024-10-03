# TP1 : Maîtrise réseau du votre poste

- [TP1 : Maîtrise réseau du votre poste](#tp1--maîtrise-réseau-du-votre-poste)
- [I. Basics](#i-basics)
- [II. Go further](#ii-go-further)
- [III. Le requin](#iii-le-requin)

# I. Basics

> Tout est à faire en ligne de commande, sauf si précision contraire.

☀️ **Carte réseau WiFi**

```bash
Adresse mac : 02:0b:97:22:17:c2
Adresse IP : 10.33.73.228
Masque de sous réseau : 
- 255.255.240.0
- /20
```

☀️ **Déso pas déso**

```bash
Adresse de réseau : 10.33.64.0
Adresse de broadcast : 10.33.79.255
Nombre adresses IP disponible : 4094
```
---

☀️ **Hostname**

```bash
stan@Stanislass-MacBook-Pro-2 ~ % hostname
Stanislass-MacBook-Pro-2.local
```

---

☀️ **Passerelle du réseau**

Déterminer...

```bash
Adresse IP passerelle réseau : 10.33.79.254
Adresse MAC passerelle réseau : 7c:5a:1c:d3:d8:76
```

---

☀️ **Serveur DHCP et DNS**

Déterminer...

```bash
stan@Stanislass-MacBook-Pro-2 ~ % ipconfig getpacket en0 | grep server_identifier
server_identifier (ip): 10.33.79.254

stan@Stanislass-MacBook-Pro-2 ~ % ipconfig getpacket en0 | grep domain_name_server
domain_name_server (ip_mult): {8.8.8.8, 1.1.1.1}
```

---

☀️ **Table de routage**

Déterminer...

```bash
stan@Stanislass-MacBook-Pro-2 ~ % route -n get default
   route to: default
destination: default
       mask: default
    gateway: 10.33.79.254
  interface: en0
      flags: <UP,GATEWAY,DONE,STATIC,PRCLONING,GLOBAL>
 recvpipe  sendpipe  ssthresh  rtt,msec    rttvar  hopcount      mtu     expire
       0         0         0         0         0         0      1500         0 

```

---

# II. Go further

> Toujours tout en ligne de commande.

---

☀️ **Hosts ?**

```bash
stan@Stanislass-MacBook-Pro-2 ~ % ping b2.hello.vous
PING b2.hello.vous (1.1.1.1): 56 data bytes
64 bytes from 1.1.1.1: icmp_seq=0 ttl=55 time=18.154 ms
64 bytes from 1.1.1.1: icmp_seq=1 ttl=55 time=16.588 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=55 time=21.832 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=55 time=16.265 ms
^C
--- b2.hello.vous ping statistics ---
4 packets transmitted, 4 packets received, 0.0% packet loss
round-trip min/avg/max/stddev = 16.265/18.210/21.832/2.210 ms
```

---

☀️ **Go mater une vidéo youtube et déterminer, pendant qu'elle tourne...**

```bash
Adresse IP du serveur : 91.68.245.14
Port du serveur : 443
port que votre PC a ouvert en local : 54437
```

---

☀️ **Requêtes DNS**

Déterminer...

```bash
stan@Stanislass-MacBook-Pro-2 ~ % nslookup www.thinkerview.com
Server:		8.8.8.8
Address:	8.8.8.8#53

Non-authoritative answer:
Name:	www.thinkerview.com
Address: 188.114.96.7
Name:	www.thinkerview.com
Address: 188.114.97.7
```

```bash
stan@Stanislass-MacBook-Pro-2 ~ % nslookup 143.90.88.12
Server:		8.8.8.8
Address:	8.8.8.8#53

Non-authoritative answer:
12.88.90.143.in-addr.arpa	name = EAOcf-140p12.ppp15.odn.ne.jp.
```

---

☀️ **Hop hop hop**

Déterminer...

```bash
stan@Stanislass-MacBook-Pro-2 ~ % traceroute www.ynov.com
traceroute: Warning: www.ynov.com has multiple addresses; using 172.67.74.226
traceroute to www.ynov.com (172.67.74.226), 64 hops max, 40 byte packets
 1  10.33.79.254 (10.33.79.254)  7.720 ms  4.281 ms  4.538 ms
 2  145.117.7.195.rev.sfr.net (195.7.117.145)  5.845 ms  5.821 ms  6.195 ms
 3  * * *
 4  196.224.65.86.rev.sfr.net (86.65.224.196)  9.853 ms  13.266 ms  3.751 ms
 5  164.147.6.194.rev.sfr.net (194.6.147.164)  16.743 ms  11.135 ms  13.672 ms
 6  162.158.20.24 (162.158.20.24)  70.778 ms *  48.016 ms
 7  162.158.20.31 (162.158.20.31)  18.158 ms * *
 8  172.67.74.226 (172.67.74.226)  21.338 ms  16.617 ms  15.616 ms
```
`Par 8 machines`

---

☀️ **IP publique**

Déterminer...

```bash
Adresse IP publique : 195.7.117.146
```

# III. Le requin

Faites chauffer Wireshark. Pour chaque point, je veux que vous me livrez une capture Wireshark, format `.pcap` donc.

Faites *clean* 🧹, vous êtes des grands now :

- livrez moi des captures réseau avec uniquement ce que je demande et pas 40000 autres paquets autour
  - vous pouvez sélectionner seulement certains paquets quand vous enregistrez la capture dans Wireshark
- stockez les fichiers `.pcap` dans le dépôt git et côté rendu Markdown, vous me faites un lien vers le fichier, c'est cette syntaxe :

```markdown
[Lien vers capture ARP](./captures/arp.pcap)
```

---

☀️ **Capture ARP**

- 📁 fichier `arp.pcap`

---

☀️ **Capture DNS**

- 📁 fichier `dns.pcap`

---

☀️ **Capture TCP**

- 📁 fichier `tcp.pcap`

---