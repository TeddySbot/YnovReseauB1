<H1> 🌞 Adresses IP de ta machine </H1>

```powershell 
PS C:\Users\TeddyS> ipconfig

Configuration IP de Windows

Carte Ethernet Ethernet :

   Statut du média. . . . . . . . . . . . : Média déconnecté
   Suffixe DNS propre à la connexion. . . :

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Adresse IPv6 de liaison locale. . . . .: fe80::faf0:1a48:6685:e80f%10
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.77.156
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
```

<br>
<H1>🌞 Si t'as un accès internet normal, d'autres infos sont forcément dispos...</H1>

```powershell
PS C:\Users\TeddyS> ipconfig /all


Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . :
   Description. . . . . . . . . . . . . . : Killer(R) Wireless-AC 1550i Wireless Network Adapter (9560NGW) 160MHz
   Adresse physique . . . . . . . . . . . : D4-3B-04-FF-44-7A
   DHCP activé. . . . . . . . . . . . . . : Oui
   Configuration automatique activée. . . : Oui
   Adresse IPv6 de liaison locale. . . . .: fe80::faf0:1a48:6685:e80f%10(préféré)
   Adresse IPv4. . . . . . . . . . . . . .: 10.33.77.156(préféré)
   Masque de sous-réseau. . . . . . . . . : 255.255.240.0
   Bail obtenu. . . . . . . . . . . . . . : vendredi 27 septembre 2024 08:54:27
   Bail expirant. . . . . . . . . . . . . : samedi 28 septembre 2024 08:54:27
   Passerelle par défaut. . . . . . . . . : 10.33.79.254
   Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254
   IAID DHCPv6 . . . . . . . . . . . : 97794820
   DUID de client DHCPv6. . . . . . . . : 00-01-00-01-2E-64-27-9B-B4-2E-99-3A-92-0D
   Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
                                       1.1.1.1
   NetBIOS sur Tcpip. . . . . . . . . . . : Activé
```
Voici un petit zoom sur les réponses.
```
 Passerelle par défaut. . . . . . . . . : 10.33.79.254
 Serveurs DNS. . .  . . . . . . . . . . : 8.8.8.8
 Serveur DHCP . . . . . . . . . . . . . : 10.33.79.254
```

<br>

<H1>🌟 BONUS : Détermine s'il y a un pare-feu actif sur ta machine </H1>

```powershell
PS C:\Users\TeddyS> Get-NetFirewallProfile | ft Name,Enabled

Name    Enabled
----    -------
Domain     True
Private    True
Public     True
```

```powershell 
PS C:\Users\TeddyS> Get-NetFirewallRule

Name                          : WFDPRINT-SPOOL-Out-Active
DisplayName                   : Utilisation de spouleur Wi-Fi Direct (Sortie)
Description                   : Règle de trafic sortant relative à l’utilisation d’imprimantes WSD sur des réseaux Wi-Fi Direct.
DisplayGroup                  : Découverte de réseau Wi-Fi Direct
Group                         : @FirewallAPI.dll,-36851
Enabled                       : True
Profile                       : Public
Platform                      : {}
Direction                     : Outbound
Action                        : Allow
EdgeTraversalPolicy           : Block
LooseSourceMapping            : False
LocalOnlyMapping              : False
Owner                         :
PrimaryStatus                 : OK
Status                        : La règle a été analysée à partir de la banque. (65536)
EnforcementStatus             : NotApplicable
PolicyStoreSource             : PersistentStore
PolicyStoreSourceType         : Local
RemoteDynamicKeywordAddresses : {}
PolicyAppId                   :
```
<br>

<H1>🌞 Envoie un ping vers toi même ! </H1>

```powershell
PS C:\Users\TeddyS> ping 10.33.77.156

Envoi d’une requête 'Ping'  10.33.77.156 avec 32 octets de données :
Réponse de 10.33.77.156 : octets=32 temps<1ms TTL=128
Réponse de 10.33.77.156 : octets=32 temps<1ms TTL=128
Réponse de 10.33.77.156 : octets=32 temps<1ms TTL=128
Réponse de 10.33.77.156 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 10.33.77.156:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```
<br>
<H1>🌞 Envoie un ping vers l'adresse IP 127.0.0.1 ! </H1>

```powershell
PS C:\Users\TeddyS> ping 127.0.0.1

Envoi d’une requête 'Ping'  127.0.0.1 avec 32 octets de données :
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128
Réponse de 127.0.0.1 : octets=32 temps<1ms TTL=128

Statistiques Ping pour 127.0.0.1:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 0ms, Moyenne = 0ms
```
<br>
<H1> 🌞 On continue avec ping. Envoie un ping vers ta passerelle ! </H1>

```powershell
PS C:\Users\TeddyS\Desktop> ping 10.33.79.254

Envoi d’une requête 'Ping'  10.33.79.254 avec 32 octets de données :
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.
Délai d’attente de la demande dépassé.

Statistiques Ping pour 10.33.79.254:
    Paquets : envoyés = 4, reçus = 0, perdus = 4 (perte 100%),
```

<H1> 🌞 On continue avec ping. Envoie un ping vers un(e) pote sur le réseau ! </H1>

```powershell
PS C:\Users\TeddyS\Desktop> ping 10.33.77.170

Envoi d’une requête 'Ping'  10.33.77.170 avec 32 octets de données :
Réponse de 10.33.77.170 : octets=32 temps=8 ms TTL=128
Réponse de 10.33.77.170 : octets=32 temps=7 ms TTL=128
Réponse de 10.33.77.170 : octets=32 temps=51 ms TTL=128
Réponse de 10.33.77.170 : octets=32 temps=63 ms TTL=128

Statistiques Ping pour 10.33.77.170:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 7ms, Maximum = 63ms, Moyenne = 32ms
```

<br>
<H1> 🌞 On continue avec ping. Envoie un ping vers un site internet ! </H1>

```powershell

PS C:\Users\TeddyS\Desktop> ping www.youtube.com

Envoi d’une requête 'ping' sur youtube-ui.l.google.com [216.58.214.174] avec 32 octets de données :
Réponse de 216.58.214.174 : octets=32 temps=18 ms TTL=117
Réponse de 216.58.214.174 : octets=32 temps=19 ms TTL=117
Réponse de 216.58.214.174 : octets=32 temps=16 ms TTL=117
Réponse de 216.58.214.174 : octets=32 temps=18 ms TTL=117

Statistiques Ping pour 216.58.214.174:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 16ms, Maximum = 19ms, Moyenne = 17ms

```
<br>

<H1>  🌞 Faire une requête DNS à la main  </H1>

```powershell
PS C:\Users\TeddyS\Desktop> Resolve-DnsName www.torproject.org

Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
www.torproject.org                             AAAA   134   Answer     2620:7:6002:0:466:39ff:fe32:e3dd
www.torproject.org                             AAAA   134   Answer     2a01:4f8:fff0:4f:266:37ff:feae:3bbc
www.torproject.org                             AAAA   134   Answer     2a01:4f8:fff0:4f:266:37ff:fe2c:5d19
www.torproject.org                             AAAA   134   Answer     2a01:4f9:c010:19eb::1
www.torproject.org                             AAAA   134   Answer     2620:7:6002:0:466:39ff:fe7f:1826
www.torproject.org                             A      88    Answer     204.8.99.144
www.torproject.org                             A      88    Answer     116.202.120.166
www.torproject.org                             A      88    Answer     116.202.120.165
www.torproject.org                             A      88    Answer     204.8.99.146
www.torproject.org                             A      88    Answer     95.216.163.36


PS C:\Users\TeddyS\Desktop> Resolve-DnsName www.wikileaks.org

Name                           Type   TTL   Section    NameHost
----                           ----   ---   -------    --------
www.wikileaks.org              CNAME  1348  Answer     wikileaks.org

Name       : wikileaks.org
QueryType  : A
TTL        : 60
Section    : Answer
IP4Address : 80.81.248.21


Name       : wikileaks.org
QueryType  : A
TTL        : 60
Section    : Answer
IP4Address : 51.159.197.136


Name                   : wikileaks.org
QueryType              : SOA
TTL                    : 1800
Section                : Authority
NameAdministrator      : root.wlinfra.org
SerialNumber           : 2022082502
TimeToZoneRefresh      : 21600
TimeToZoneFailureRetry : 3600
TimeToExpiration       : 604800
DefaultTTL             : 1800



PS C:\Users\TeddyS\Desktop> Resolve-DnsName www.thinkerview.com

Name                                           Type   TTL   Section    IPAddress
----                                           ----   ---   -------    ---------
www.thinkerview.com                            AAAA   300   Answer     2a06:98c1:3120::7
www.thinkerview.com                            AAAA   300   Answer     2a06:98c1:3121::7
www.thinkerview.com                            A      202   Answer     188.114.96.7
www.thinkerview.com                            A      202   Answer     188.114.97.7

```
<br>

<H1>🌞 Effectue un scan du réseau auquel tu es connecté !</H1>


Command sur Nmap-Zenmap GUI
```
nmap -sn -PR 192.168.1.0/24

[résultat dans Scan.pcap]
```

<H2>🌞 Changer d'adresse IP</h2>

On commmence par lancer le powershell en tant que administrateur.

Grace au scan effectuer avant nous utilison un filtre pour permettre de filtrer les ip permettant de voir qu'elles sont les adresses utilisable quand celle-ci marque no-request.

Nous utilisons par la suite la commande suivant qui permet de recuperer le noms de l'interface correspond dans notre cas à la carte wi-fi.

```
PS C:\Windows\system32> Get-NetAdapter

Name                      InterfaceDescription                    ifIndex Status       MacAddress             LinkSpeed
----                      --------------------                    ------- ------       ----------             ---------
Wi-Fi                     Killer(R) Wireless-AC 1550i Wireless...      10 Up           D4-3B-04-FF-44-7A     866.7 Mbps
Ethernet                  Killer E2500 Gigabit Ethernet Contro...       7 Disconnected B4-2E-99-3A-92-0D          0 bps
Ethernet 2                VirtualBox Host-Only Ethernet Adapter         6 Up           0A-00-27-00-00-06         1 Gbps

```

Ensuite, nous utilisons une autre command permettant de modifier les ip de notre carte Wi-Fi.



```powershell
New-NetIPAddress -interfaceAlias "Wi-Fi" -IPAddress "192.168.1.38" -PrefixLength 24 -DefaultGateway "192.168.1.1"
#                               Nom du réseau        ip disponile                                    passerelle

ipconfig

Carte réseau sans fil Wi-Fi :

   Suffixe DNS propre à la connexion. . . : home
   Adresse IPv6. . . . . . . . . . . . . .: 2a01:cb19:b08:8600:b5e:db11:955:b668
   Adresse IPv6 temporaire . . . . . . . .: 2a01:cb19:b08:8600:e4c8:9752:19dd:f51d
   Adresse IPv6 de liaison locale. . . . .: fe80::faf0:1a48:6685:e80f%10
   Adresse IPv4. . . . . . . . . . . . . .: 192.168.1.38
   Masque de sous-réseau. . . . . . . . . : 255.255.255.0
   Passerelle par défaut. . . . . . . . . : fe80::12e9:92ff:fe8c:2f10%10
                                       192.168.1.1

```

