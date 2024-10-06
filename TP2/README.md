# TP2 : Environnement virtuel

## Compte-rendu

☀️ Sur **`node1.lan1.tp2`**

```bash
[et0@node1 ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: enp0s1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 12:a7:85:b8:eb:9c brd ff:ff:ff:ff:ff:ff
    inet 10.1.1.11/24 brd 10.1.1.255 scope global noprefixroute enp0s1
       valid_lft forever preferred_lft forever
    inet6 fe80::10a7:85ff:feb8:eb9c/64 scope link 
       valid_lft forever preferred_lft forever
```
```bash
[et0@node1 ~]$ ip r s
default via 10.1.1.254 dev enp0s1 proto static metric 100 
10.1.1.0/24 dev enp0s1 proto kernel scope link src 10.1.1.11 metric 100 
```
```bash
[et0@node1 ~]$ ping 10.1.2.12
PING 10.1.2.12 (10.1.2.12) 56(84) bytes of data.
64 bytes from 10.1.2.12: icmp_seq=1 ttl=63 time=16.0 ms
64 bytes from 10.1.2.12: icmp_seq=2 ttl=63 time=3.00 ms
64 bytes from 10.1.2.12: icmp_seq=3 ttl=63 time=10.3 ms
64 bytes from 10.1.2.12: icmp_seq=4 ttl=63 time=2.24 ms
^C
--- 10.1.2.12 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3012ms
rtt min/avg/max/mdev = 2.242/7.896/16.046/5.661 ms
```
```bash
[et0@node1 ~]$ traceroute 10.1.2.12
traceroute to 10.1.2.12 (10.1.2.12), 30 hops max, 60 byte packets
 1  _gateway (10.1.1.254)  5.815 ms  5.655 ms  5.626 ms
 2  10.1.2.12 (10.1.2.12)  7.058 ms !X  7.024 ms !X  6.999 ms !X
```

# II. Interlude accès internet

☀️ **Sur `router.tp2`**

```bash
[et0@router ~]$ ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=54 time=24.5 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=54 time=26.5 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=54 time=23.8 ms
64 bytes from 1.1.1.1: icmp_seq=4 ttl=54 time=25.8 ms
^C
--- 1.1.1.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3014ms
rtt min/avg/max/mdev = 23.758/25.119/26.476/1.061 ms
```
```bash
[et0@router ~]$ ping apple.com
PING apple.com (17.253.144.10) 56(84) bytes of data.
64 bytes from www.brkgls.com (17.253.144.10): icmp_seq=1 ttl=53 time=26.7 ms
64 bytes from www.brkgls.com (17.253.144.10): icmp_seq=2 ttl=53 time=28.9 ms
64 bytes from www.brkgls.com (17.253.144.10): icmp_seq=3 ttl=53 time=24.4 ms
64 bytes from www.brkgls.com (17.253.144.10): icmp_seq=4 ttl=53 time=24.6 ms
^C
--- apple.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3010ms
rtt min/avg/max/mdev = 24.415/26.162/28.928/1.832 ms

```

☀️ **Accès internet LAN1 et LAN2**

```bash
[et0@node2 ~]$ ip r s
default via 10.1.1.254 dev enp0s1 proto static metric 100 
10.1.1.0/24 dev enp0s1 proto kernel scope link src 10.1.1.11 metric 100 
```
```bash
[et0@node2 ~]$ sudo cat /etc/sysconfig/network-scripts/ifcfg-enp0s1 | grep DNS1
DNS1=1.1.1.1
```
```bash
[et0@node2 ~]$ ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=53 time=29.7 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=53 time=50.1 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=53 time=25.4 ms
64 bytes from 1.1.1.1: icmp_seq=4 ttl=53 time=40.5 ms
^C
--- 1.1.1.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3005ms
rtt min/avg/max/mdev = 25.361/36.410/50.064/9.630 ms
```
```bash
PING apple.com (17.253.144.10) 56(84) bytes of data.
64 bytes from www.brkgls.com (17.253.144.10): icmp_seq=1 ttl=52 time=27.7 ms
64 bytes from www.brkgls.com (17.253.144.10): icmp_seq=2 ttl=52 time=27.1 ms
64 bytes from www.brkgls.com (17.253.144.10): icmp_seq=3 ttl=52 time=25.8 ms
64 bytes from www.brkgls.com (17.253.144.10): icmp_seq=4 ttl=52 time=25.4 ms
^C
--- apple.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3008ms
rtt min/avg/max/mdev = 25.370/26.492/27.696/0.956 ms
```

# III. Services réseau

**Adresses IP et routage OK, maintenant, il s'agirait d'en faire quelque chose nan ?**

Dans cette partie, on va **monter quelques services orientés réseau** au sein de la topologie, afin de la rendre un peu utile que diable. Des machines qui se `ping` c'est rigolo mais ça sert à rien, des machines qui font des trucs c'est mieux.

## 1. Web web web


```bash
[et0@web ~]$ sudo dnf install nginx
Last metadata expiration check: 0:05:31 ago on Fri Oct  4 19:00:05 2024.
Package nginx-1:1.20.1-16.el9_4.1.aarch64 is already installed.
Dependencies resolved.
Nothing to do.
Complete!
```
```bash
[et0@web ~]$ sudo cat /etc/nginx/nginx.conf | grep listen
        listen       80;
        listen       [::]:80;
#        listen       443 ssl http2;
#        listen       [::]:443 ssl http2;
```
```bash
[et0@web www]$ sudo firewall-cmd --list-all | grep ports
  ports: 80/tcp
  forward-ports: 
  source-ports: 
```
```bash
[et0@web site_nul]$ ls -al
total 4
drwxr-xr-x. 2 nginx nginx  24 Oct  6 16:37 .
drwxr-xr-x. 3 root  root   22 Oct  6 16:37 ..
-rw-r--r--. 1 nginx nginx 192 Oct  4 19:16 index.html
```
```bash
[et0@web conf.d]$ sudo cat site_nul.conf 
    server {
        listen       80;
        listen       [::]:80;
        server_name  site_nul.tp2;
        root         /var/www/site_nul;
	index index.html;

        # Load configuration files for the default server block.
        include /etc/nginx/default.d/*.conf;

        error_page 404 /404.html;
        location = /404.html {
        }

        error_page 500 502 503 504 /50x.html;
        location = /50x.html {
        }
    }
```
```bash
[et0@web conf.d]$ sudo ss -alntp | grep nginx
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=1231,fd=6),("nginx",pid=1230,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=1231,fd=7),("nginx",pid=1230,fd=7))
```

☀️ **Sur `node1.lan1.tp2`**

```bash
[et0@node1 ~]$ sudo cat /etc/hosts
10.1.2.12   site_nul.tp2
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
```
```bash
[et0@node1 ~]$ curl site_nul.tp2
<!DOCTYPE html>
<html lang="fr">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
  <body>
    <h1>Hello</h1>
  </body>
</html>
```