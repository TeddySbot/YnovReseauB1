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

