# Wat is een netwerk?
Een groep van 2 of meer apparaten die met elkaar zijn verbonden en informatie delen. Elk apparaat dat toegang heeft tot het netwerk heet een ==**host**==.
## Netwerk types:
- LAN (Local Area Network)
- WLAN (Wireless LAN)
	- Wi-Fi
	- Bluetooth
- WAN (Wide Area Network)
	- Netwerk van KPN, Odido, etc.
# Wat kan je delen op een netwerk?
- Data
- Hardware resources
	- Printer
	- Disk
	- GPU
# Netwerktopologieën
- Topologieën
	- Ster - Een centraal punt met andere hosts eromheen
	- Bus - Een lijn die van begin tot eind aftakkingen heeft naar hosts
	- Ring - Alle hosts zijn opvolgend met elkaar verbonden
- Waarom meerdere soorten?
	- Kosten
	- Redundantie - Als 1 punt niet werkt, werkt de rest dan wel nog? Foutgevoeligheid
	- Gemak
# Broadcast & Point-to-Point netwerken
- **Broadcast**
	- Een bericht verzend een bericht naar alle luisteraars
		- Sommige hosts negeren het bericht, als het niet voor hun bedoeld was
	- Niet efficiënt bij grote netwerken
	- Slecht schaalbaar
		- Je kan niet meerdere berichten tegelijk sturen : ==**collision problem**==
	- Vaak gebruikt in bus- en ster -topologieën
	- Ethernet (LAN), Wi-Fi
	- Geschikt voor kleine netwerken met weinig verkeer
- **Point-to-Point**
	- Bericht wordt via een specifiek pad naar de ontvanger gestuurd
		- Het beste pad moet wel gevonden worden
	- Efficiënter
	- Goed schaalbaar
	- Gebruikt in ster-, ring- en mesh-topologieën
	- Internet, WAN-verbindingen
	- Geschikt voor grote netwerken met veel verkeer

- Kleine netwerken gebruiken een broadcast netwerk intern
	- Elk kleine netwerk is verbonden met een point-to-point netwerk door een speciaal device, de ==**gateway**==.

![[Gateway Network.png]]
# Bericht van source naar destination
- Het bericht is **gebroadcast** in het **source** netwerk
- De **gateway** van het **source** netwerk krijgt dit bericht binnen en forward het via het point-to-point netwerk naar het **destination** netwerk
- De **gateway** van het **destination** netwerk ontvangt het bericht en **broadcast** het in het **destination** netwerk
# Apparaten in een netwerk
- Switch
	- Verbinden van hosts (binnen een LAN netwerk)
	- Pakketten sturen naar apparaten
	- Maakt gebruik van MAC-Adressen
- Router
	- Verbinden van diverse netwerken
	- IP-Adressen uitdelen (DHCP)
	- Doorsturen van pakketten
	- Heeft een **default gateway**
- Hubs / Repeaters
	- Signaal gaat erin en wordt gedupliceerd naar elke uitgang
- Bridges
	- Een brug tussen 2 netwerken
	- Wordt niet veel meer gebruikt
- Kabels
	- Glasvezel
	- Koper
- Draadloos
	- Wi-Fi
	- Satelliet
# Wat is het internet
- Allemaal netwerken met elkaar verbonden
# Addressering
- Welke informatie heb je nodig om een pakketje van punt A naar punt B te krijgen?
	- (Continent)
	- Land
	- (Provincie)
	- Plaats
	- Straat
	- Huisnummer
	- (Toevoegingen, etage, etc.)
- Addressering voor netwerken zijn IP-Adres
- Achter elke host zit een IP-Adres, het identificeert een apparaat op een netwerk
- **I**nternet **P**rotocol

- IPv4
	- bijvoorbeeld 192.168.1.1
	- In totaal 4,3 miljard addressen totaal.
	- 4 octeten
	- 32 bits
- IPv6
	- IPv4 was vol, er moeten meer addressen zijn
	- 128 bits
- **Public** vs **Private**
	- Private
		- 10.x.x.x (Class A)
		- 172.16.x.x (Class B)
		- 192.168.x.x (Class C)
		- Kan je niet gebruiken op het internet (WAN)
	- Public
		- Alle andere addressen
# Network software
- **Network software** is de set regels die definieërt hoe berichten worden gemaakt, gebruikt en ontvangen
- Deze regels zijn gedefinieërd als ==**protocols**==
# Protocols
- Heeft dezelfde rol als een ==**grammatica**== in een taal
- Het geeft je de regels om een kloppende zin te vormen en dingen correct te communiceren
- Network protocols verbergen hardware details van een gebruiker
	- Protocols zijn ontworpen in meerdere ==**lagen**==
	- Elke laag heeft zijn eigen taken
	- Als een laag is vervangen, worden andere lagen hier niet door aangetast
	- Een gebruiker hoeft bijvoorbeeld niet te weten wat voor soort kabels zijn gebruikt, hoe berichten worden gemaakt en hoe errors worden afgehandeld
# Informatie over een netwerk
Als software op hosts binnen een netwerk informatie met elkaar willen uitwisselen, moeten er afspraken gemaakt worden
- Wat voor berichten gaan we uitwisselen?
- Hoe gaan we met elkaar die berichten uitwisselen?
# OSI-Model
- Open Systems Interconnection Model
- Een model met ==**7 lagen**==
	- Beginnen **onderaan** met tellen
	
	- 7 Applicatie
	- 6 Presentatie
	- 5 Sessie
	- 4 Transport
	- 3 Netwerk
	- 2 Datalink
	- 1 Fysiek
- Op elke laag wordt data toegevoegd: ==**Encapsulatie**==
- Bij zenden gaat de data van laag 7 naar 1
- Bij ontvangen gaat de data van laag 1 naar 7

- **7: Application Layer**
	- Bevat protocollen die door de applicaties worden gebruikt
	- Bepaalt **hoe** we gaan communiceren
	- HTTP
	- FTP
	- SMTP
	- DNS
- **6: Presentation Layer**
	- Zorgt voor vertaling van data tussen de applicatielaag en het netwerk
	- Verantwoordelijk voor hoe de data eruit ziet (data format)
	- Bepaalt **wat** we gaan communiceren
	- SSL/TLS (Encryptie)
	- JPEG
	- GIF
- **5: Session Layer**
	- Zorgt ervoor dat verbindingen worden opgezet, onderhouden en beëindigd
	- NetBIOS
	- RPC (Remote Procedure Call)
- **4: Transport Layer**
	- Zorgt voor end-to-end communicatie en betrouwbaarheid, bijvoorbeeld door datastromen in kleinere pakketten te verdelen en deze opnieuw samen te stellen
	- TCP (Transmission Control Protocol)
		- Handshake protocol
	- UDP (User Datagram Protocol)
		- Veel bij broadcasten gebruikt
		- Send and forget
- **3: Network layer**
	- Verantwoordelijk voor de routering van data tussen verschillende netwerken, en gebruikt IP-adressen
	- Verantwoordelijk voor het zoeken van het **optimale pad**
	- IP (Internet Protocol)
- **2: Datalink Layer**
	- Zorgt voor betrouwbare communicatie binnen een lokaal netwerk door foutdetectie, foutcorrectie en framing van de data. Het behandelt ook MAC-adressering.
	- Verantwoordelijk om data op te splitsen in **frames** als het volledige pakket te groot is
	- Ethernet
	- Wi-Fi (802.11)
- **1: Physical Layer**
	- Dit is de laag die zich bezighoudt met de fysieke aspecten van netwerkverbinding
	- Bekabeling
	- USB
	- Bluetooth kaart
	- Netwerkkaarten

- Ezelsbruggetjes:
	- All People Seem To Need Data Processing
	- Anton Piek Schildert Tieten Naast Dikke Fazanten
# Packets & Frames
- **Packets**
	- Netwerklaag 3 in OSI-Model
	- De eenheid van data dat wordt verzonden of ontvangen door computers. Meestal over een groot netwerk zoals het internet
	- Genavigeerd door IP-Adressen
	- Inhoud:
		- Header
			- Bron
			- Bestemming
			- TCP/UDP en routinginformatie
		- Payload
			- De data
		- Footer
			- Controle of foutinformatie (optioneel)
- **Frame**
	- Datalink laag 2 in OSI-Model
	- Een eenheid van data die wordt gebruikt voor communicatie binnen een lokaal netwerk
	- genavigeerd door MAC-Adressen
	- Inhoud:
		- Header
			- Bron
			- Bestemming
			- Frame-type (bijv. ethernet)
			- Volgnummerinformatie (soms)
		- Payload
			- Bevat een packet
		- Trailer / Footer
			- Foutdetectie-informatie
			- Controleren of een frame is aangekomen

- **Een Frame is groter dan een Packet**

- Applicatie laag krijgt data
- Transport laag split data up in kleinere blokjes en voegt informatie toe, bijvoorbeeld een ID van het stukje dat het is, het splitst het in segments
- Netwerk laag voegt nog meer informatie toe, naar welk IP-adres het moet
- Datalink laag voegt weer informatie toe, ethernet of Wi-Fi protocol, naar welk MAC-adres het moet, uniek per computer. Pas na de datalink laag heet het een frame

# MAC-Adres
- Een unieke identifier per fysiek apparaat
# TCP / IP Model
- Een praktisch model met 4 lagen, gebruikt voor de implementatie van netwerken zoals het internet
	- 4: Application Layer (OSI 7, 6, 5)
		- HTTP
		- TLS
		- DNS
	- 3: Transport Layer (OSI 4)
		- TCP
		- UDP
	- 2: Internet Layer (OSI 3)
		- IP
	- 1: Network Access Layer (OSI 2, 1)
		- Ethernet
		- Wireless LAN
