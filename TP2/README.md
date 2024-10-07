<H1>🌞 Prouvez que votre configuration est effective !</H1>

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

