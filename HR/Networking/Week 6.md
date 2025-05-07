# OSI Applicatie Laag (7)
- In een computernetwerk wordt de applicatie laag gebruikt om de protocollen en methoden te benoemen die zijn ontworpen voor proces-tot-procescommunicatie via een Internet Protocol-computernetwerk
- **Maakt gebruik van:**
	- Presentatie laag (laag 6)
	- Sessie laag (laag 5)
	- (laag 4 - 1)
- PDU: **Data (JSON, Text, MP3, MP4, PNG, etc.)**
## URL
- Uniform Resource Locator
## HTTP
- Protocol voor datacommunicatie in het WWW
- Hypertext Transfer Protocol
### HTTP - Methods
- Definiëren welke actie moet worden uitgevoerd op de bron die is geïdentificeerd voor een URL
- **Veel voorkomende:**
	- GET
	- POST
	- PUT
	- DELETE
	- TRACE
	- OPTIONS
	- CONNECT
	- PATCH
- Request / Response
	- Request
		- `GET / HTTP/1.1`
		- `GET [locatie] [protocol versie]`
	- Response
		- `HTTP/1.1 200 OK`
			- `200` is een status code
		- `Content-Type: text/html`
		- `Content-Length: 136`
		- HTML Tekst
## Domeinen
- `hint.hogeschoolrotterdam.nl`
	- Subdomain (`hint`)
		- Zelfde restrictie als SLD
	- Second-Level Domain (`hogeschoolrotterdam`)
		- Kan meerdere subdomains hebben
		- Maximaal 63 karakters + TLD
		- a tot z, 0 tot 9 en streepjes
	- Top Level Domain (`nl`)
		- ccTLD (Landen)
		- gTLD (Generiek: `com`, `org`)
	- Totaal maximaal 253 karakters
## DNS - Domain Name System
- Is verantwoordelijk voor de vertaling van een domeinnaam naar een IP-adres
- Een domeinnaam kan je zien als een **alias** voor een IP-adres
- Bestaat uit verschillende onderdelen
- Eigenschappen
	- Port 53 (standaard)
	- Hiërarchische structuur
	- Model: Client-Server (UDP)
	- Is gewoon software (DNS-server)
	- Vertaling met behulp van **records**
### DNS - Records
- Zijn specifieke instructies binnen het DNS die bepalen hoe een domeinnaam wordt gekoppeld aan bijbehorende resources, zoals IP-adres of mailservers
- **A Record:** Deze wordt omgezet naar een IPv4 adres
- **AAAA Record:** Deze wordt omgezet naar een IPv6 adres
- **CNAME Record:** Deze wordt omgezet naar een ander domein (alias van een alias)
- **MX Record:** Deze wordt omgezet naar een ander adres dat e-mails verwerkt
- **TXT Record:** Een vrij in te vullen veld waar informatie in gezet kan worden
