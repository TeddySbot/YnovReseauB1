<H1>1. Quelques pings </1>

<H2>🌞 Prouvez que votre configuration est effective !</H2>

```powershell

PS C:\Windows\system32> Get-NetIPAddress -InterfaceAlias "Ethernet"


IPAddress         : fe80::72ea:a395:faf8:efcb%7
InterfaceIndex    : 7
InterfaceAlias    : Ethernet
AddressFamily     : IPv6
Type              : Unicast
PrefixLength      : 64
PrefixOrigin      : WellKnown
SuffixOrigin      : Link
AddressState      : Preferred
ValidLifetime     :
PreferredLifetime :
SkipAsSource      : False
PolicyStore       : ActiveStore

IPAddress         : 10.10.10.10
InterfaceIndex    : 7
InterfaceAlias    : Ethernet
AddressFamily     : IPv4
Type              : Unicast
PrefixLength      : 24
PrefixOrigin      : Manual
SuffixOrigin      : Manual
AddressState      : Preferred
ValidLifetime     :
PreferredLifetime :
SkipAsSource      : False
PolicyStore       : ActiveStore

```

<H1>🌞 Tester que votre LAN + votre adressage IP est fonctionnel </H1>

```powershell
PS C:\Windows\system32> ping 10.10.10.54

Envoi d’une requête 'Ping'  10.10.10.54 avec 32 octets de données :
Réponse de 10.10.10.54 : octets=32 temps<1ms TTL=128
Réponse de 10.10.10.54 : octets=32 temps<1ms TTL=128
Réponse de 10.10.10.54 : octets=32 temps<1ms TTL=128
Réponse de 10.10.10.54 : octets=32 temps=1 ms TTL=128

Statistiques Ping pour 10.10.10.54:
    Paquets : envoyés = 4, reçus = 4, perdus = 0 (perte 0%),
Durée approximative des boucles en millisecondes :
    Minimum = 0ms, Maximum = 1ms, Moyenne = 0ms

```

<H1>🌞 Sur le PC client & 🌞 Echangez-vous des messages</H1>



```powershell

PS C:\Users\TeddyS\ cd C:\Users\TeddyS\Downloads\netcat-win32-1.11\netcat-1.11

PS C:\Users\TeddyS\Downloads\netcat-win32-1.11\netcat-1.11> ./nc.exe 10.10.10.54 7777
Coucou mon petit
Fais preuves de politesse
^C

```

<H1>🌞 Sur le PC serveur </H1>

```powershell
PS C:\Users\TeddyS\Downloads\netcat-win32-1.11\netcat-1.11> ./nc -l -p  8888
hugo
c moi
Tes sur ?
```

<H1>🌞 Sur le PC serveur toujours</H1>

```powershell
PS C:\Users\TeddyS\Downloads\netcat-win32-1.11\netcat-1.11> netstat -a -b -n

 TCP    0.0.0.0:8888           0.0.0.0:0              LISTENING
 [nc.exe]
```

<H1>🌞 Utilisez une commande qui permet de voir la connexion en cours </H1>

```powershell

netstat -a -b -n | Select-String :8888
TCP    10.10.10.10:8888       10.10.10.54:6611       ESTABLISHED

```

<H1>🌞 Faites une capture Wireshark complète d'un échange </H1>

Allez voir netcat1.pcap

<H1>🌞 Inversez les rôles </H1>

Allez voir netcat2.pcap


<h1>1. Serveur web </h1>

<h2>🌞 Utilisez Wireshark pour capturer du trafic HTTP</h2>

Allez voir http.pcap

<h1>2. Autres services</h1>

<h2>🌞 Pour les 5 applications</h2>

Avec powershell, on cherche l'ip correspond à ce que l'on cherche et avec Wireshark, on observe les captures correspondantes avec le filtre.

```
ip.addr == xxx.xxx.xxx.xxx
```



```
Discord : 152.199.19.161:443   #service1.pcap
Teams : 52.123.128.14:443      #service2.pcap
Notion : 172.67.72.70:443      #service3.pcap
riot : 162.159.61.3:443        #service4.pcap
Valorant :172.65.252.238:5223  #service5.pcap
```

