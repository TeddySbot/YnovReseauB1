<H1> I. ARP basics </h1>

<h2> ☀️ Avant de continuer...</h2>

- affichez l'adresse MAC de votre carte WiFi !


```powershell
PS C:\Windows\system32> ipconfig /all

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Killer(R) Wireless-AC 1550i Wireless Network Adapter (9560NGW) 160MHz
   Adresse physique . . . . . . . . . . . : D4-3B-04-FF-44-7A
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui
   Adresse IPv6 de liaison locale. . . . .: fe80::faf0:1a48:6685:e80f%10(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.77.156(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Bail obtenu. . . . . . . . . . . . . . : mardi 8 octobre 2024 08:38:33
   Bail expirant. . . . . . . . . . . . . : mercredi 9 octobre 2024 08:38:33
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
   Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254
   IAID DHCPv6 . . . . . . . . . . . : 97794820
   DUID de client DHCPv6. . . . . . . . : 00-01-00-01-2E-64-27-9B-B4-2E-99-3A-92-0D
   Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
                                       1.1.1.1
   NetBIOS sur Tcpip. . . . . . . . . . . : Activé

```

```powershell
   Adresse physique . . . . . . . . . . : D4-3B-04-FF-44-7A
```

<h2>☀️ Affichez votre table ARP </h2>

- allez vous commencez à devenir grands, je vous donne pas la commande, demande à m'sieur internet !



```powershell
PS C:\Windows\system32> arp -a

Interface : 10.33.77.156 --- 0xa
  Adresse Internet      Adresse physique      Type
  10.33.65.63           44-af-28-c3-6a-9f     dynamique
  10.33.66.78           e4-b3-18-48-36-68     dynamique
  10.33.73.77           98-8d-46-c4-fa-e5     dynamique
  10.33.77.160          c8-94-02-f8-ab-97     dynamique
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
  10.33.79.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
  ```

<h2>☀️ Déterminez l'adresse MAC de la passerelle du réseau de l'école </h2>


-  la passerelle, vous connaissez son adresse IP normalement (cf TP1 ;) )

```powershell 
PS C:\Windows\system32> ipconfig

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::faf0:1a48:6685:e80f%10
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.77.156
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Passerelle par défaut. . . . . . . . . : 10.33.79.254

``` 
```powershell
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
```

- si vous avez un accès internet, votre PC a forcément l'adresse MAC de la passerelle dans sa table ARP
```powershell

PS C:\Windows\system32> arp -a

Interface : 10.33.77.156 --- 0xa
  Adresse Internet      Adresse physique      Type
  10.33.65.63           44-af-28-c3-6a-9f     dynamique
  10.33.66.78           e4-b3-18-48-36-68     dynamique
  10.33.73.77           98-8d-46-c4-fa-e5     dynamique
  10.33.77.160          c8-94-02-f8-ab-97     dynamique
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
  10.33.79.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
  ```

```powershell
7c-5a-1c-d3-d8-76 //  adresse MAC de la passerelle

```

<H2>☀️ Supprimez la ligne qui concerne la passerelle </h2>

- une commande pour supprimer l'adresse MAC de votre table ARP

```powershell

PS C:\Windows\system32> arp -d 10.33.79.254

```

- si vous ré-affichez votre table ARP, y'a des chances que ça revienne presque tout de suite !

```powershell
PS C:\Windows\system32> arp -a

Interface : 10.33.77.156 --- 0xa
  Adresse Internet      Adresse physique      Type
  10.33.65.63           44-af-28-c3-6a-9f     dynamique
  10.33.66.78           e4-b3-18-48-36-68     dynamique
  10.33.73.77           98-8d-46-c4-fa-e5     dynamique
  10.33.77.160          c8-94-02-f8-ab-97     dynamique
  10.33.79.254          7c-5a-1c-d3-d8-76     dynamique
  10.33.79.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```

<h2>☀️ Prouvez que vous avez supprimé la ligne dans la table ARP </h2>

- en affichant la table ARP

```powershell
```powershell

PS C:\Windows\system32> arp -d 10.33.79.254
PS C:\Windows\system32> arp -a

Interface : 10.33.77.156 --- 0xa
  Adresse Internet      Adresse physique      Type
  10.33.65.63           44-af-28-c3-6a-9f     dynamique
  10.33.66.78           e4-b3-18-48-36-68     dynamique
  10.33.73.77           98-8d-46-c4-fa-e5     dynamique
  10.33.77.160          c8-94-02-f8-ab-97     dynamique
  10.33.79.255          ff-ff-ff-ff-ff-ff     statique
  224.0.0.2             01-00-5e-00-00-02     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```

<h2>☀️ Wireshark </h2>

- capture [arp1.pcap](arp1.pcap)
- lancez une capture Wireshark, puis supprimez la ligne de la passerelle dans la table ARP pendant que la capture est en cours
la capture doit contenir uniquement 2 trames :
    - un ARP request que votre PC envoie pour apprendre l'adresse MAC de la passerelle
    - et la réponse

<H1>II. ARP dans un réseau local </H1>

<h2>☀️ Déterminer </h2>

- pour la carte réseau impliquée dans le partage de connexion (carte WiFi ?)
    - son adresse IP au sein du réseau local formé par le partage de co

```powershell
PS C:\Windows\system32> ipconfig

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6. . . . . . . . . . . . . .: 2a02:8440:6300:309e:b2a0:52f3:d37:bd4d
   Adresse IPv6 temporaire . . . . . . . .: 2a02:8440:6300:309e:e448:3fe9:cc9b:84ab
   Adresse IPv6 de liaison locale. . . . .: fe80::faf0:1a48:6685:e80f%10
   Adresse IPv4. . . . . . . . . . . . . .: 172.20.10.7
   Masque de sous-réseau. . . . . . . . . : 255.255.255.240
   Passerelle par défaut. . . . . . . . . : fe80::cdb:eaff:fe5b:1364%10
                                       172.20.10.1
```
```powershell
172.20.10.1
```
- son adresse MAC
```powershell

PS C:\Windows\system32> arp -a

Interface : 172.20.10.7 --- 0xa
  Adresse Internet      Adresse physique      Type
  172.20.10.1           0e-db-ea-5b-13-64     dynamique
  172.20.10.15          ff-ff-ff-ff-ff-ff     statique
  224.0.0.22            01-00-5e-00-00-16     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  224.0.0.252           01-00-5e-00-00-fc     statique
  239.255.255.250       01-00-5e-7f-ff-fa     statique
  255.255.255.255       ff-ff-ff-ff-ff-ff     statique
```
```powershell
0e-db-ea-5b-13-64
```

<h2>☀️ DIY </h2>

- changer d'adresse IP & prouvez que vous avez bien changé d'IP


```powershell

PS C:\Windows\system32> ipconfig

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6. . . . . . . . . . . . . .: 2a02:8440:6300:309e:b2a0:52f3:d37:bd4d
   Adresse IPv6 temporaire . . . . . . . .: 2a02:8440:6300:309e:3424:124d:e52:fe93
   Adresse IPv6 de liaison locale. . . . .: fe80::faf0:1a48:6685:e80f%10
   Adresse IPv4. . . . . . . . . . . . . .: 172.20.10.10
   Masque de sous-réseau. . . . . . . . . : 255.255.0.0
   Passerelle par défaut. . . . . . . . . : fe80::cdb:eaff:fe5b:1364%10
```

```powershell
   Adresse IPv4. . . . . . . . . . . . . .: 172.20.10.10
```
<h2> ☀️ Pingz ! </h2>

- vérifiez que vous pouvez tous vous ping avec ces adresses IP

Victoria 
```powershell
PS C:\Windows\system32> ping 172.20.10.8 -t

Envoi d’une requête 'Ping'  172.20.10.8 avec 32 octets de données :
Réponse de 172.20.10.8 : octets=32 temps=10 ms TTL=128
Réponse de 172.20.10.8 : octets=32 temps=5 ms TTL=128
Réponse de 172.20.10.8 : octets=32 temps=71 ms TTL=128
Réponse de 172.20.10.8 : octets=32 temps=21 ms TTL=128
Réponse de 172.20.10.8 : octets=32 temps=7 ms TTL=128

Statistiques Ping pour 172.20.10.8:
    Paquets : envoyés = 5, reçus = 5, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 5ms, Maximum = 71ms, Moyenne = 22ms
Ctrl+C
```

hugo
```powershell
PS C:\Users\TeddyS\Downloads> ping 172.20.10.11 -t

Envoi d’une requête 'Ping'  172.20.10.11 avec 32 octets de données :
Réponse de 172.20.10.11 : octets=32 temps=133 ms TTL=128
Réponse de 172.20.10.11 : octets=32 temps=3 ms TTL=128
Réponse de 172.20.10.11 : octets=32 temps=4 ms TTL=128
Réponse de 172.20.10.11 : octets=32 temps=5 ms TTL=128
Réponse de 172.20.10.11 : octets=32 temps=3 ms TTL=128
Réponse de 172.20.10.11 : octets=32 temps=4 ms TTL=128
Réponse de 172.20.10.11 : octets=32 temps=81 ms TTL=128

Statistiques Ping pour 172.20.10.11:
    Paquets : envoyés = 7, reçus = 7, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 3ms, Maximum = 133ms, Moyenne = 33ms
Ctrl+C
```

- vérifiez avec une commande ping que vous avez bien un accès internet

```powershell
PS C:\Users\TeddyS\Downloads> ping www.youtube.com

Envoi d’une requête 'ping' sur youtube-ui.l.google.com [2a00:1450:4007:80e::200e] avec 32 octets de données :
Réponse de 2a00:1450:4007:80e::200e : temps=65 ms
Réponse de 2a00:1450:4007:80e::200e : temps=94 ms
Réponse de 2a00:1450:4007:80e::200e : temps=98 ms
Réponse de 2a00:1450:4007:80e::200e : temps=59 ms

Statistiques Ping pour 2a00:1450:4007:80e::200e:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 59ms, Maximum = 98ms, Moyenne = 79ms
```

<h2>☀️ Affichez votre table ARP ! </h2>

```powershell
PS C:\Users\TeddyS\Downloads> arp -a

Interface : 172.20.10.10 --- 0xa
  Adresse Internet      Adresse physique      Type
  172.20.10.1           0e-db-ea-5b-13-64     dynamique
  172.20.10.2           10-63-c8-68-8c-21     dynamique
  172.20.10.6           50-5a-65-50-4a-c9     dynamique
  172.20.10.7           50-5a-65-50-4a-c9     dynamique
  172.20.10.8           10-63-c8-68-8c-21     dynamique
  172.20.10.11          50-5a-65-50-4a-c9     dynamique
  172.20.255.255        ff-ff-ff-ff-ff-ff     statique
  224.0.0.251           01-00-5e-00-00-fb     statique
  ```

<h2>☀️ Capture arp2.pcap </h2>

capture [arp2.pcap](arp2.pcap)

<h2>🪽 Bonus : ARP poisoning </h2>







