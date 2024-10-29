<h1>TP7 : On dit chiffrer pas crypter</h1>
<h2>Serveur Web </h2>
<h3>🌞 Lister les ports en écoute sur la machine</h3>

```powershell
[user@web conf.d]$ sudo ss -lnpt | grep 80
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=1484,fd=6),("nginx",pid=1483,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=1484,fd=7),("nginx",pid=1483,fd=7))
```

<h3>🌞 Ouvrir le port dans le firewall de la machine </h3>
```powershell
[user@web conf.d]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3
  sources:
  services: ssh
  ports: 80/tcp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

<h3>🌞 Vérifier que ça a pris effet</h3>

- faites un ping vers sitedefou.tp7.b1

```powershell
teddy@teddy-VirtualBox:~$ ping sitedefou.tp7.b1
PING sitedefou.tp7.b1 (10.7.1.11) 56(84) bytes of data.
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=1 ttl=64 time=1.12 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=2 ttl=64 time=0.731 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=3 ttl=64 time=0.396 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=4 ttl=64 time=0.902 ms
64 bytes from sitedefou.tp7.b1 (10.7.1.11): icmp_seq=5 ttl=64 time=0.442 ms
^C
--- sitedefou.tp7.b1 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4031ms
rtt min/avg/max/mdev = 0.396/0.718/1.123/0.274 ms
```
- vous devriez avoir la page "meow !" quand vous visitez le site

```powershell
teddy@teddy-VirtualBox:~$ curl http://sitedefou.tp7.b1
meow !
```

<h3>🌞 Capture tcp_http.pcap</h3>

voici la capture demandé [tcp_http.pcap](tcp_http.pcap)

<h3>🌞 Voir la connexion établie</h3>

```powershell
teddy@teddy-VirtualBox:~$ sudo ss -npt | grep 80
ESTAB 0      0               10.7.1.101:40248         10.7.1.11:80    users:(("firefox",pid=5006,fd=109))
```

<h2>2. On rajoute un S</h2>

<h3>🌞 Lister les ports en écoute sur la machine </h3>

```powershell
[user@web ~]$ sudo ss -lnpt | grep 443
LISTEN 0      511        10.7.1.11:443       0.0.0.0:*    users:(("nginx",pid=1426,fd=6),("nginx",pid=1425,fd=6))
```

<h3>🌞 Gérer le firewall 0</h3>

```powershell
[user@web ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3
  sources:
  services: ssh
  ports: 443/tcp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

<h3>🌞 Capture tcp_https.pcap </h3>

- capture [tcp_https.pcap](tcp_https.pcap)

<h2>III. Serveur VPN</h2>

<h3>🌞 Prouvez que vous avez bien une nouvelle carte réseau wg0</h3>

```powershell
[user@vpn ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:89:e6:ba brd ff:ff:ff:ff:ff:ff
    inet 10.7.1.111/24 brd 10.7.1.255 scope global noprefixroute enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe89:e6ba/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:e2:20:18 brd ff:ff:ff:ff:ff:ff
    inet 10.7.2.111/24 brd 10.7.2.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fee2:2018/64 scope link
       valid_lft forever preferred_lft forever
4: wg0: <POINTOPOINT,NOARP,UP,LOWER_UP> mtu 1420 qdisc noqueue state UNKNOWN group default qlen 1000
    link/none
    inet 10.7.200.1/24 scope global wg0
       valid_lft forever preferred_lft forever
```

<h3>🌞 Déterminer sur quel port écoute Wireguard </h3>

```powershell
[user@vpn ~]$ sudo ss -lnpu | grep 51820
UNCONN 0      0            0.0.0.0:51820      0.0.0.0:*
UNCONN 0      0               [::]:51820         [::]:*
```

<h3>🌞 Ouvrez ce port dans le firewall </h3>

```powershell
[user@vpn ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3 enp0s8 wg0
  sources:
  services: cockpit dhcpv6-client ssh
  ports: 51820/udp
  protocols:
  forward: yes
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

<h2>2. Ajout d'un client VPN </h2>

<h3>🌞 Ping ping ping ! </h3>

```powershell
teddy@teddy-VirtualBox:~$ ping 10.7.200.1
PING 10.7.200.1 (10.7.200.1) 56(84) bytes of data.
64 bytes from 10.7.200.1: icmp_seq=1 ttl=64 time=0.732 ms
64 bytes from 10.7.200.1: icmp_seq=2 ttl=64 time=1.02 ms
64 bytes from 10.7.200.1: icmp_seq=3 ttl=64 time=1.20 ms
64 bytes from 10.7.200.1: icmp_seq=4 ttl=64 time=0.596 ms
64 bytes from 10.7.200.1: icmp_seq=5 ttl=64 time=0.727 ms
64 bytes from 10.7.200.1: icmp_seq=6 ttl=64 time=0.632 ms
^C
--- 10.7.200.1 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 5092ms
rtt min/avg/max/mdev = 0.596/0.816/1.198/0.217 ms
```

<h3>🌞 Capture ping1_vpn.pcap </h3>

```powershell
teddy@teddy-VirtualBox:~$ ping 10.7.200.1
PING 10.7.200.1 (10.7.200.1) 56(84) bytes of data.
64 bytes from 10.7.200.1: icmp_seq=1 ttl=64 time=0.677 ms
64 bytes from 10.7.200.1: icmp_seq=2 ttl=64 time=1.77 ms
64 bytes from 10.7.200.1: icmp_seq=3 ttl=64 time=1.01 ms
64 bytes from 10.7.200.1: icmp_seq=4 ttl=64 time=1.93 ms
64 bytes from 10.7.200.1: icmp_seq=5 ttl=64 time=1.69 ms
64 bytes from 10.7.200.1: icmp_seq=6 ttl=64 time=1.78 ms
^C
--- 10.7.200.1 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 5051ms
rtt min/avg/max/mdev = 0.677/1.476/1.933/0.464 ms
```

<h3>🌞 Capture ping1_vpn.pcap </h3>

- capture [ping1_vpn.pcap](ping1_vpn.pcap)


<h3>🌞 Capture ping2_vpn.pcap </h3>

- capture [ping2_vpn.pcap](ping2_vpn.pcap)


<h3>🌞 Prouvez que vous avez toujours un accès internet </h3>

```powershell
teddy@teddy-VirtualBox:/etc$ traceroute 1.1.1.1
traceroute to 1.1.1.1 (1.1.1.1), 64 hops max
  1   10.7.200.1  0.921ms  0.886ms  0.480ms
  2   10.7.1.254  2.092ms  1.759ms  2.619ms
  3   10.0.3.2  1.911ms  1.968ms  2.589ms
```

<h2>4. Private service </h2>

<h3>🌞 Visitez le service Web à travers le VPN </h3>

```powerpoint
teddy@teddy-VirtualBox:~$ traceroute 10.7.200.37
traceroute to 10.7.200.37 (10.7.200.37), 64 hops max
  1   10.7.200.1  0.712ms  0.352ms  0.516ms
  2   10.7.200.37  0.894ms !X  1.052ms !X  0.819ms !X
```