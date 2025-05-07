# IPv4-Packet
- Definieert **datagram** structuur dat data encapsuleert
- Heeft een **header** (20 bytes)
- Heeft een **payload** (data)
## IP-Packet en Fragmentatie (datalink laag)
Een datalink-frame is kleiner in grootte dan een IP-Packet, Hoe krijg ik dan een IP-Packet in een frame
- **Fragmentation** Opsplitsen van pakketten in kleinere pakketjes
- **Reassemblage** Ontvanger plakt alle losse fragmenten weer aan elkaar
# IP-Packet inpakken in frame
- Wat hebben we nodig?
	- Verzender MAC-adres
	- Ontvanger MAC-adres
- Wie kan ons het MAC-adres van een host vertellen?
	- Alleen de host zelf
	- Dit is een probleem
# ARP - Adres Resolution Protocol
- OSI laag 2
- Een protocol dat wordt gebruikt om het MAC-adres van hosts te achterhalen aan de hand van het IP-adres.
	- ARP Request
		- Broadcast (one > all)
	- ARP Reply
		- Unicast (one > one)
# IP-Adres uitdelen op het netwerk
- Static
	- Verspilling omdat de host het IP-adres niet nodig heeft als deze niet met het netwerk is verbonden
	- Handmatig instellen
- Dynamic
	- DHCP wijst IP-adressen toe aan hosts die ze nodig hebben en eist terug wanneer ze niet langer nodig zijn
	- Automatisch ingesteld
# DHCP - Dynamic Host Configuration Protocol
- OSI laag 3
- Apparaat vraagt om een IP-adres aan de DHCP-server
- Niks meer dan alleen software
- Stappen:
	- Discover (Een host vraagt aan het netwerk wie de DHCP server is en of hij een IP-adres mag hebben)
	- Offer (DHCP server biedt een IP-adres aan)
	- Request (De host vraagt dit IP-adres aan)
	- Acknowledge (De DHCP server confirmed dat de aanvraag gemaakt is)
# ICMP - Internet Control Message Protocol
- OSI laag 3
- Een netwerkprotocol dat wordt gebruikt voor het verzenden van foutmeldingen en operationele informatie over netwerkcommunicatie
- **Wat kan er mis gaan?**
	- Een host is offline
	- Een verkeerde IP-adres gebruikt door de verzender
	- Connectie is verbroken (bijvoorbeeld gebroken kabel, router, etc.)
- **Belangrijke eigenschappen**
	- Niet bedoeld voor Data-overdracht
		- Alleen diagnostiek en foutmeldingen
	- Veelgebruikte tool die ICMP gebruikt: `ping`
	- ICMP pakketten bevatten geen TCP- of UDP-data
- **Veel voorkomende ICMP-berichten**
	- Echo Request en Echo Reply
		- Gebruikt door `ping`
	- Destination Unreachable
		- Geeft aan dat pakket niet afgeleverd kan worden
	- Time Exceeded
		- Wanneer een pakket de TTL bereikt, en dus niet op tijd is aangekomen 
		- Gebruikt bij de `traceroute` tool
	- Redirect Message
		- Wanneer een router een host vertelt dat er een betere route is
# NAT - Network Address Translation
- Een techniek die wordt gebruikt om meerder apparaten in **een** privé-netwerk toegang te geven tot het internet via een publiek IP-adres
- **Toepassing**
	- **Routers** > Bijvoorbeeld `192.168.x.x` omzetten naar een publiek IP van provider
- **Waarom NAT gebruiken?**
	- IP-Adresbesparing
		- IPv4 adressen zijn beperkt
	- Beveiliging
		- Privé apparaten niet direct vanaf internet bereikbaar
	- Flexibiliteit
		- Eigen IP-ranges gebruiken zonder afhankelijkheid van ISP
- **Hoe werkt het?**
	- Wanneer een bericht naar buiten wordt verstuurd wordt de verzender zijn IP vervangen door het publieke IP > **IP Address Translation**
	- De router koppelt een uniek poortnummer (bijvoorbeeld 50001) aan het verzoek. Dit slaat hij op in een NAT-tabel
# IPv6
- Schaarste aan IPv4 adressen
- Snellere routers
	- De router hoeft niet meer packets te fragmenteren
- Ingebouwde beveiliging
- Efficiëntere header
	- IPv6 verwijdert onnodige velden en maakt optionele velden flexibeler
