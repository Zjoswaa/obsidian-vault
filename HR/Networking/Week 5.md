# OSI Transport laag (4)
- Verantwoordelijk voor het afleveren van berichten naar de juiste applicatie

- Twee opties voor het versturen van berichten
	- Connectieloos
		- Direct een bericht via adres sturen
	- Connectie georiënteerd
		- Eerst een connectie maken, dan pas bericht sturen

- Belangrijkste protocollen
	- **Transport Control Protocol** (TCP)
		- Connectie georiënteerd
	- **User Datagram Protocol** (UDP)
		- Connectieloos
# TCP verbinding
- Three-way-handshake
	- SYN (sender > receiver)
	- SYN ACK (receiver > sender)
	- ACK (sender > receiver)
	- Data (sender > receiver)
	- ACK (receiver > sender)
- Dit wordt beide voor openen (syn) en sluiten (fin) van een verbinding gedaan
## TCP - Flow Control
- De ontvanger kan vragen of de verzender de pakketten langzamer kan verzenden. Dit als de ontvanger de berichten niet snel genoeg kan verwerken
	- Dit wordt gecommuniceerd via de TCP packer header (`window`)
		- `window > 0`: Geeft aan de grootte van data wat de ontvanger kan ontvangen
		- `window = 0`: Geeft aan dat de verzender de data verzending moet pauzeren totdat hij een bericht ontvangt
## TCP - Congestion Control
- Berichten die door een host worden verzonden worden doorgestuurd door routers
- De routers plaatsen de berichten in een queue
- Als de wachtrij vol is, worden de berichten genegeerd
- Deze situatie wordt **congestion** genoemd

- Het TCP-Protocol vertraagt de berichtoverdracht om het congestieprobleem op te lossen
# UDP verbinding
- Requests en Responses worden gewoon "at random" gestuurd
# Ports
- Genummerde eindpunten waarmee computers en servers verschillende soorten netwerkverkeer kunnen onderscheiden
- Hoe werken ports
	- Elke verbinding gebruikt een IP-adres en een poortnummer
	- IP-Adres: Identificeert een **apparaat** op het netwerk
	- Port: Welke **applicatie** de data moet verwerken
## Ports - Soorten
- **Well-Known Ports**
	- 0-1023
	- Standaard voor bekende protocollen
		- HTTP (80)
		- HTTPS (443)
		- FTP (21)
		- SSH (22)
- **Registered Ports**
	- Voor specifieke applicaties
		- 1024-49151
			- MySQL (3306)
			- RDP (3389)
			- Minecraft (25565)
- **Dynamic / Private Ports**
	- 49152 - 65535
	- Tijdelijke poorten voor client verbindingen
	- Dynamisch toegewezen door OS
