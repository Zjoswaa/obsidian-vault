# Wi-Fi Netwerk
## Accesspoint (AP)
- Vormt de brug tussen apparaten en een groter netwerk.

## BSS Basic Service Set
- Een roep draadloze apparaten die met elkaar communiceren binnen een netwerk
- Infrastructuurnetwerk
	- Alle communicatie gaat via een centraal punt
- Independent Basic Service Set
	- Alle communicatie gaat via de hosts die direct met elkaar communiceren.
# OSI Netwerk Laag
- Is verantwoordelijk voor het bepalen van het kortste (beste) pad naar de eindbestemming
	- Door addressing en routing
- Protocol Data Unit (PDU): **Packet**
## Packet
- Source Address
- Destination Address
- Allemaal meer informatie
	- Version
	- Length
	- Time To Live
	- Protocol
	- Checksum
	- etc.
## Routing
- Het vinden van de kortste weg van A naar B en het bericht te forwarden over die weg
### Moeilijkheden bij routing
- Structuur kan veranderen (**Topologie verandering**)
	- Nieuwe hosts worden verbonden
	- Hosts worden weggehaald
	- Lengte tussen hosts kan veranderen
		- Tijd, niet afstand

- De **host** voert basisnetwerkfuncties uit zoals adressering, fragmentatie en pakketvorming, maar de echte routering en netwerkbeheer gebeurt op **routers en switches**
## Router
- Een apparaat dat deel uitmaakt van meerdere netwerken en verantwoordelijk is voor het routeren van de pakketten van en naar andere netwerken
- Maakt deel uit van **meerdere** netwerken
	- Elke heeft zijn eigen **IP-Adres**
- Elke verbinding is identificeerbaar via een
	- Interface
	- Label
	- Adres
- Houdt een **routing table** bij
## Routing table
- Wordt gebruikt om het volgende punt naar de eindbestemming op te slaan
- Wat staat er meestal in de routing tabel
	- Bestemmingsnetwerk
		- Geeft aan voor welk netwerk of welke IP-adressen de route geldt
	- Subnet mask
		- Helpt met het bepalen van de grootte van het netwerk
	- Gateway
		- Next hop
	- Interface
	- Kosten / Metric
	- Type route
- `route print` command op Windows laat je computers routing table zien
	- `ip route show` Linux
- Niet elke host op het internet kan worden opgeslagen, dat zouden er te veel zijn
	- We slaan dus alleen mogelijke **bestemmingsnetwerken** op in plaats van host-adressen
	- Dit levert een kleinere tabel op
	- Het adres moet de volgende informatie hebben
		- Netwerk: 192.168.1.0/24
		- Host: 192.168.1.42
## Forwarding
- Verzend de informatie van punt naar punt volgens de tabel
- Router ontvangt een pakket
	- aal het destination adres eruit
	- Haal het netwerk ID uit het destination adres
	- Zoek netwerk ID in routing tabel
		- Gevonden: Gebruik pad in tabel naar de eindbestemming
		- Niet gevonden: Gebruikt default path (meestal 0.0.0.0/0) naar volgende router
## Netwerk ID
- Voordat we het netwerk ID kunnen achterhalen moeten we eerst de netmask weten
- **Netmask**: Binair nummer dat laat zien welke digits het netwerk ID zijn
## IP-Adres
- **Privé** adressen kan je niet gebruiken om fysiek aan het internet verbonden te zijn
- **Class A**
	- **192**.168.1.10/8
	- Groot netwerk
	- Eerste octet geeft netwerk ID aan
	- 16.777.214 hosts
- **Class B**
	- **192.168**.1.10/16
	- Middelgroot netwerk
	- Eerste twee octetten geven netwerk ID aan
	- 65.534 hosts
- **Class C**
	- **192.168.1**.10/24
	- Klein netwerk
	- Eerste drie octetten geven netwerk ID aan
	- 254 hosts
## Localhost
- 127.0.0.0/8
- Binnen een host zelf een netwerk opbouwen