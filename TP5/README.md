<h1> I. Setup </h1>

<h2>☀️ Uniquement avec des commandes, prouvez-que : </h2>

- vous avez bien configuré les adresses IP demandées (un ip a suffit hein)

```powershell

teddy@teddy12:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:55:fe:9a brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.12/24 brd 10.5.1.255 scope global enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe55:fe9a/64 scope link
       valid_lft forever preferred_lft forever


teddy@teddy11:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:fb:eb:df brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.11/24 brd 10.5.1.255 scope global enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fefb:ebdf/64 scope link
       valid_lft forever preferred_lft forever


PS C:\Users\TeddyS> ipconfig
Carte Ethernet Ethernet 3 :
   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::562:98ac:3c50:6f67%13
   Adresse IPv4. . . . . . . . . . . . . .: 10.5.1.1
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . :

[user@teddyroot ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:1f:e0:07 brd ff:ff:ff:ff:ff:ff
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic noprefixroute enp0s3
       valid_lft 86365sec preferred_lft 86365sec
    inet6 fe80::a00:27ff:fe1f:e007/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:02:65:4f brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.254/24 brd 10.5.1.255 scope global noprefixroute enp0s8
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe02:654f/64 scope link
       valid_lft forever preferred_lft forever

```
- vous avez bien configuré les hostnames demandés
```powershell
teddy@teddy12:~$ sudo hostnamectl
[sudo] password for teddy:
 Static hostname: teddy12
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: 2dcb28693e7745c6869238c4cbfb642f
         Boot ID: a722fa469c014f9ab68cf3a6f40cc4b6
  Virtualization: oracle
Operating System: Ubuntu 24.04.1 LTS
          Kernel: Linux 6.8.0-45-generic
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Firmware Version: VirtualBox
   Firmware Date: Fri 2006-12-01
    Firmware Age: 17y 10month 2w


teddy@teddy11:~$ sudo hostnamectl
[sudo] password for teddy:
 Static hostname: teddy11
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: 2dcb28693e7745c6869238c4cbfb642f
         Boot ID: 794844b48027431f80a6fb9856a243e3
  Virtualization: oracle
Operating System: Ubuntu 24.04.1 LTS
          Kernel: Linux 6.8.0-45-generic
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Firmware Version: VirtualBox
   Firmware Date: Fri 2006-12-01
    Firmware Age: 17y 10month 2w


[user@teddyroot ~]$ sudo hostnamectl
[sudo] password for user:
 Static hostname: teddyroot
       Icon name: computer-vm
         Chassis: vm 🖴
      Machine ID: d8c6949e8f8a478ba0b9f1c2a22248fb
         Boot ID: a7d6650edf2a4fd3b5fa7b715e7a45ed
  Virtualization: oracle
Operating System: Rocky Linux 9.4 (Blue Onyx)
     CPE OS Name: cpe:/o:rocky:rocky:9::baseos
          Kernel: Linux 5.14.0-427.13.1.el9_4.x86_64
    Architecture: x86-64
 Hardware Vendor: innotek GmbH
  Hardware Model: VirtualBox
Firmware Version: VirtualBox

```

- tout le monde peut se ping au sein du réseau 10.5.1.0/24



```powershell

PS C:\Users\TeddyS> ping 10.5.1.11

Envoi d’une requête 'Ping'  10.5.1.11 avec 32 octets de données :
Réponse de 10.5.1.11 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.11 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.11 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.11 : octets=32 temps<1ms TTL=64

Statistiques Ping pour 10.5.1.11:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms

____________________________________________________

PS C:\Users\TeddyS> ping 10.5.1.12

Envoi d’une requête 'Ping'  10.5.1.12 avec 32 octets de données :
Réponse de 10.5.1.12 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.12 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.12 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.12 : octets=32 temps<1ms TTL=64

Statistiques Ping pour 10.5.1.12:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms

____________________________________________________

PS C:\Users\TeddyS> ping 10.5.1.254

Envoi d’une requête 'Ping'  10.5.1.254 avec 32 octets de données :
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64
Réponse de 10.5.1.254 : octets=32 temps<1ms TTL=64

Statistiques Ping pour 10.5.1.254:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```

<h1>II. Accès internet pour tous !</h1>

<h2>☀️ Déjà, prouvez que le routeur a un accès internet </h2>

```powershell
[user@teddyroot ~]$ ping ynov.com
PING ynov.com (104.26.11.233) 56(84) bytes of data.
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=1 ttl=51 time=47.4 ms
64 bytes from 104.26.11.233 (104.26.11.233): icmp_seq=2 ttl=51 time=104 ms
^C
--- ynov.com ping statistics ---
2 packets transmitted, 2 received, 0% packet loss, time 1002ms
rtt min/avg/max/mdev = 47.366/75.442/103.519/28.076 ms
```

<h2>☀️ Activez le routage </h2>

```powershell
[user@teddyroot ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3 enp0s8
  sources:
  services: cockpit dhcpv6-client ssh
  ports:
  protocols:
  forward: yes
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```
<h2>☀️ Prouvez que les clients ont un accès internet </h2>

```powershell
teddy@teddy11:~$ ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=50 time=82.3 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=50 time=69.2 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=50 time=82.8 ms
64 bytes from 1.1.1.1: icmp_seq=4 ttl=50 time=70.3 ms
64 bytes from 1.1.1.1: icmp_seq=5 ttl=50 time=115 ms
64 bytes from 1.1.1.1: icmp_seq=6 ttl=50 time=81.2 ms
^C
--- 1.1.1.1 ping statistics ---
6 packets transmitted, 6 received, 0% packet loss, time 5004ms
rtt min/avg/max/mdev = 69.159/83.376/114.540/15.003 ms

_______________________________________________________

teddy@teddy12:~$ ping 1.1.1.1
PING 1.1.1.1 (1.1.1.1) 56(84) bytes of data.
64 bytes from 1.1.1.1: icmp_seq=1 ttl=50 time=69.3 ms
64 bytes from 1.1.1.1: icmp_seq=2 ttl=50 time=59.9 ms
64 bytes from 1.1.1.1: icmp_seq=3 ttl=50 time=76.8 ms
64 bytes from 1.1.1.1: icmp_seq=4 ttl=50 time=68.2 ms
^C
--- 1.1.1.1 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3001ms
rtt min/avg/max/mdev = 59.920/68.566/76.819/5.989 ms
```

<h2>☀️ Montrez-moi le contenu final du fichier de configuration de l'interface réseau </h2>

```powershell
teddy@teddy12:~$ cat /etc/netplan/01-netcfg.yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [10.5.1.12/24]
      gateway4: 10.5.1.254
```

<h1>III. Serveur SSH </h1>

<h2>☀️ Sur routeur.tp5.b1, déterminer sur quel port écoute le serveur SSH </h2>

```powershell
[user@teddyroot ~]$ sudo ss -lnpt
State      Recv-Q     Send-Q         Local Address:Port         Peer Address:Port    Process
LISTEN     0          128                  0.0.0.0:22                0.0.0.0:*        users:(("sshd",pid=707,fd=3))
LISTEN     0          128                     [::]:22                   [::]:*        users:(("sshd",pid=707,fd=4))
```

<h2>☀️ Sur routeur.tp5.b1, vérifier que ce port est bien ouvert</h2>

```powershell
[user@teddyroot ~]$ sudo firewall-cmd --list-all
public (active)
  target: default
  icmp-block-inversion: no
  interfaces: enp0s3 enp0s8
  sources:
  services: ssh
  ports: 22/tcp
  protocols:
  forward: yes
  masquerade: yes
  forward-ports:
  source-ports:
  icmp-blocks:
  rich rules:
```

<h1>IV. Serveur DHCP </h1>

<h2> ☀️ Installez et configurez un serveur DHCP sur la machine routeur.tp5.b1</h2>

```powershell
dnf -y install dhcp-server

sudo nano /etc/dhcp/dhcpd.conf

((La configuration du fichier))

sudo systemctl enable --now dhcpd
```

Voici la configuration :
```powershell
option domain-name-servers     1.1.1.1;
authoritative;
subnet 10.5.1.0 netmask 255.255.255.0 {
    range dynamic-bootp 10.5.1.137 10.5.1.237;
    option broadcast-address 10.5.1.255;
    option routers 10.5.1.254;
}
```

<h2>☀️ Créez une nouvelle machine client client3.tp5.b1 </h2>

```powershell
teddy@teddy13:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel ``state`` UP group default qlen 1000
    link/ether 08:00:27:0e:36:ff brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.138/24 brd 10.5.1.255 scope global dynamic enp0s3
       valid_lft 451sec preferred_lft 451sec

_____________________________________________________________

teddy@teddy13:~$ ping ynov.com
PING ynov.com (104.26.10.233) 56(84) bytes of data.
64 bytes from 104.26.10.233: icmp_seq=1 ttl=50 time=89.8 ms
64 bytes from 104.26.10.233: icmp_seq=2 ttl=50 time=61.3 ms
64 bytes from 104.26.10.233: icmp_seq=3 ttl=50 time=140 ms
64 bytes from 104.26.10.233: icmp_seq=4 ttl=50 time=60.4 ms

--- ynov.com ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3002ms
rtt min/avg/max/mdev = 60.414/87.982/140.430/32.501 ms
```

<h2>☀️ Consultez le bail DHCP qui a été créé pour notre client

</h2>

```powershell
[user@teddyroot dhcpd]$ cat dhcpd.leases
[....]
[....]
lease 10.5.1.137 {
  starts 2 2024/10/15 11:24:57;
  ends 2 2024/10/15 11:34:57;
  cltt 2 2024/10/15 11:24:57;
  binding state active;
  next binding state free;
  rewind binding state free;
  hardware ethernet 08:00:27:0e:36:ff;
  uid "\377\3424?>\000\002\000\000\253\021\037\335\242\363\2212\251\267";
  client-hostname "teddy13";
}
[....]
```

<h2>☀️ Confirmez qu'il s'agit bien de la bonne adresse MAC

</h2>

```powershell
teddy@teddy13:/var/lib$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host noprefixroute
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:0e:36:ff brd ff:ff:ff:ff:ff:ff
    inet 10.5.1.137/24 metric 100 brd 10.5.1.255 scope global dynamic enp0s3
       valid_lft 380sec preferred_lft 380sec
    inet 10.5.1.138/24 brd 10.5.1.255 scope global secondary dynamic enp0s3
       valid_lft 374sec preferred_lft 374sec
```