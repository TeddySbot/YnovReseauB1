<h1>I. Le setup

</H1>

<h2>☀️ Prouvez que...</h2>

- une machine du LAN1 peut joindre internet (ping un nom de domaine)

```powershell
[user@dhcp ~]$ ping ynov.com
PING ynov.com (104.26.10.233) 56(84) bytes of data.
64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=1 ttl=53 time=17.2 ms
64 bytes from 104.26.10.233 (104.26.10.233): icmp_seq=2 ttl=53 time=18.1 ms
^C
--- ynov.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 17.249/17.668/18.087/0.419 ms
```

- une machine du LAN2 peut joindre internet (ping nom de domaine)

```powershell
[user@web ~]$ ping ynov.com
PING ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=1 ttl=53 time=16.8 ms
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=2 ttl=53 time=18.9 ms
^C
--- ynov.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1001ms
rtt min/avg/max/mdev = 16.792/17.841/18.890/1.049 ms
```

- une machine du LAN1 peut joindre une machine du LAN2 (ping une adresse IP)

```powershell
[user@web ~]$ ping 10.6.1.253
PING 10.6.1.253 (10.6.1.253) 56(84) bytes of data.
64 bytes from 10.6.1.253: icmp_seq=1 ttl=63 time=1.15 ms
64 bytes from 10.6.1.253: icmp_seq=2 ttl=63 time=1.60 ms
64 bytes from 10.6.1.253: icmp_seq=3 ttl=63 time=1.92 ms
64 bytes from 10.6.1.253: icmp_seq=4 ttl=63 time=1.39 ms
64 bytes from 10.6.1.253: icmp_seq=5 ttl=63 time=2.08 ms
^C
--- 10.6.1.253 ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4007ms
rtt min/avg/max/mdev = 1.152/1.626/2.078/0.337 ms
```



<h1>II. LAN clients</h1>

<h2>☀️ Prouvez que...</h2>

- le client a bien récupéré une adresse IP en DHCP

```powershell
teddy@teddy-VirtualBox:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:57:07:b4 brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.37/24 brd 10.6.1.255 scope global dynamic noprefixroute enp0s3
       valid_lft 43022sec preferred_lft 43022sec
    inet6 fe80::a00:27ff:fe57:7b4/64 scope link
       valid_lft forever preferred_lft forever
```

- vous avez bien 1.1.1.1 en DNS

```powershell
teddy@teddy-VirtualBox:~$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s3)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 1.1.1.1
       DNS Servers: 1.1.1.1
```

- vous avez bien la bonne passerelle indiquée

```powershell
teddy@teddy-VirtualBox:~$ ip r s
default via 10.6.1.254 dev enp0s3 proto dhcp src 10.6.1.37 metric 100
10.6.1.0/24 dev enp0s3 proto kernel scope link src 10.6.1.37 metric 100
```

- que ça ping un nom de domaine public sans problème magueule

```powershell
teddy@teddy-VirtualBox:~$ ping ynov.com
PING ynov.com (172.67.74.226) 56(84) bytes of data.
64 bytes from 172.67.74.226: icmp_seq=1 ttl=53 time=17.0 ms
64 bytes from 172.67.74.226: icmp_seq=2 ttl=53 time=17.8 ms
^C
--- ynov.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 17.034/17.409/17.785/0.375 ms
```
<h1>III. LAN serveurzzzz
</h1>
<h2>☀️ Déterminer sur quel port écoute le serveur NGINX

</h2>

```powershell
[user@web ~]$ sudo ss -lnpt | grep 80
LISTEN 0      511          0.0.0.0:80        0.0.0.0:*    users:(("nginx",pid=1504,fd=6),("nginx",pid=1503,fd=6))
LISTEN 0      511             [::]:80           [::]:*    users:(("nginx",pid=1504,fd=7),("nginx",pid=1503,fd=7))
```

<h2>☀️ Ouvrir ce port dans le firewall</h2>


```powershell
Error: INVALID_PROTOCOL: 'HTTP' not in {'tcp'|'udp'|'sctp'|'dccp'}
[user@web ~]$ sudo firewall-cmd --permanent --add-port=80/tcp
success
[user@web ~]$ sudo firewall-cmd --reload
success

# Whoaaaaa la page est magnifique
```

```powershell
teddy@teddy-VirtualBox:~$ curl http://10.6.2.11
```

```http
teddy@teddy-VirtualBox:~$ curl http://10.6.2.11
<!doctype html>
<html>
  <head>
    <meta charset='utf-8'>
    <meta name='viewport' content='width=device-width, initial-scale=1'>
    <title>HTTP Server Test Page powered by: Rocky Linux</title>
    <style type="text/css">
      /*<![CDATA[*/
```


<h1>III. 2. Serveur DNS</h1>
<h2>☀️ Déterminer sur quel(s) port(s) écoute le service BIND9 </h2>

```powershell
[user@dns ~]$ sudo ss -lnpt | grep 53
LISTEN 0      4096       127.0.0.1:953       0.0.0.0:*    users:(("named",pid=2117,fd=28))
LISTEN 0      10         10.6.2.12:53        0.0.0.0:*    users:(("named",pid=2117,fd=25))
LISTEN 0      10         127.0.0.1:53        0.0.0.0:*    users:(("named",pid=2117,fd=22))
LISTEN 0      10             [::1]:53           [::]:*    users:(("named",pid=2117,fd=27))
LISTEN 0      4096           [::1]:953          [::]:*    users:(("named",pid=2117,fd=29))
```

<h2>☀️ Ouvrir ce(s) port(s) dans le firewall

</h2>

```powershell
[user@dns ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3
  sources:
  services: ssh
  ports: 53/tcp
  protocols:
  forward: yes
  masquerade: no
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

<h2>☀️ Effectuez des requêtes DNS manuellement depuis le serveur DNS lui-même dans un premier temps </h2>

- dig web.tp6.b1 @10.6.2.12
```powershell
[user@dns ~]$ dig web.tp6.b1 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> web.tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 55287
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 2047344a7282056d01000000670fa08ac8d7ce30f6d59a11 (good)
;; QUESTION SECTION:
;web.tp6.b1.                    IN      A

;; ANSWER SECTION:
web.tp6.b1.             86400   IN      A       10.6.2.11

;; Query time: 0 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Wed Oct 16 13:16:26 CEST 2024
;; MSG SIZE  rcvd: 83
```

- dig dns.tp6.b1 @10.6.2.12

```powerhsell
[user@dns ~]$ dig dns.tp6.b1 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> dns.tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 39131
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 3fa4a7b3eb75709c01000000670fa0aed302340cdd35a170 (good)
;; QUESTION SECTION:
;dns.tp6.b1.                    IN      A

;; ANSWER SECTION:
dns.tp6.b1.             86400   IN      A       10.6.2.12

;; Query time: 0 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Wed Oct 16 13:17:02 CEST 2024
;; MSG SIZE  rcvd: 83
```

- dig ynov.com @10.6.2.12

```powerhsell
[user@dns ~]$ dig ynov.com @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> ynov.com @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 7224
;; flags: qr rd ra; QUERY: 1, ANSWER: 3, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: babbd51064eb769301000000670fa0d57e15cfd70869dae3 (good)
;; QUESTION SECTION:
;ynov.com.                      IN      A

;; ANSWER SECTION:
ynov.com.               300     IN      A       104.26.10.233
ynov.com.               300     IN      A       172.67.74.226
ynov.com.               300     IN      A       104.26.11.233

;; Query time: 266 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Wed Oct 16 13:17:41 CEST 2024
;; MSG SIZE  rcvd: 113
```

- dig -x 10.6.2.11 @10.6.2.12

```powershell
[user@dns ~]$ dig -x 10.6.2.11 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> -x 10.6.2.11 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 9479
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: 0d76897f4865e7e301000000670fa0fa1eedfbdbfde7ca02 (good)
;; QUESTION SECTION:
;11.2.6.10.in-addr.arpa.                IN      PTR

;; ANSWER SECTION:
11.2.6.10.in-addr.arpa. 86400   IN      PTR     web.tp6.b1.

;; Query time: 0 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Wed Oct 16 13:18:18 CEST 2024
;; MSG SIZE  rcvd: 103
```

- dig -x 10.6.2.12 @10.6.2.12

```powershell
[user@dns ~]$ dig -x 10.6.2.12 @10.6.2.12

; <<>> DiG 9.16.23-RH <<>> -x 10.6.2.12 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 39436
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: ccc994470c4a9e0a01000000670fa11a4b40e3fb9730907a (good)
;; QUESTION SECTION:
;12.2.6.10.in-addr.arpa.                IN      PTR

;; ANSWER SECTION:
12.2.6.10.in-addr.arpa. 86400   IN      PTR     dns.tp6.b1.

;; Query time: 0 msec
;; SERVER: 10.6.2.12#53(10.6.2.12)
;; WHEN: Wed Oct 16 13:18:50 CEST 2024
;; MSG SIZE  rcvd: 103
```

<h2>☀️ Effectuez une requête DNS manuellement depuis client1.tp6.b1
</h2>

```powershell
teddy@teddy-VirtualBox:~$ dig web.tp6.b1 @10.6.2.12

; <<>> DiG 9.18.28-0ubuntu0.24.04.1-Ubuntu <<>> web.tp6.b1 @10.6.2.12
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 51359
;; flags: qr aa rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 1

;; OPT PSEUDOSECTION:
; EDNS: version: 0, flags:; udp: 1232
; COOKIE: a87202747bdc6e4f01000000671601be316fe680fb6d66ee (good)
;; QUESTION SECTION:
;web.tp6.b1.                    IN      A

;; ANSWER SECTION:
web.tp6.b1.             86400   IN      A       10.6.2.11

;; Query time: 7 msec
;; SERVER: 10.6.2.12#53(10.6.2.12) (UDP)
;; WHEN: Mon Oct 21 09:24:49 CEST 2024
;; MSG SIZE  rcvd: 83
```

<h2>☀️ Capturez une requête DNS et la réponse de votre serveur </h2>

Voici la capture [capture.pcap](capture.pcap) demandé.

<h1>3. Serveur DHCP </h1>

```powershell
teddy@teddy-VirtualBox:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:64:09:69 brd ff:ff:ff:ff:ff:ff
    inet 10.6.1.38/24 brd 10.6.1.255 scope global dynamic noprefixroute enp0s3
       valid_lft 42293sec preferred_lft 42293sec
    inet6 fe80::a00:27ff:fe64:969/64 scope link
       valid_lft forever preferred_lft forever
```

```powershell
teddy@teddy-VirtualBox:~$ resolvectl
Global
         Protocols: -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
  resolv.conf mode: stub

Link 2 (enp0s3)
    Current Scopes: DNS
         Protocols: +DefaultRoute -LLMNR -mDNS -DNSOverTLS DNSSEC=no/unsupported
Current DNS Server: 10.6.2.12
       DNS Servers: 10.6.2.12
```