# OSI Fysieke laag
- De fysieke laag is verantwoordelijk voor et omzetten van de data naar **signalen** en deze over het medium (kabel / radio) te versturen.
- Protocol Data Unit (PDU): **Bit / Symbol**

## Analoog & Digitaal
- Een analoog signaal
	- Is continu en kan oneindig veel waarden aannemen
	- Geluidsgolven
	- Dimbare lamp
	- Sine wave

- Een digitaal signaal
	- Heeft een discrete waarde
	- 0 of 1
	- Schakelaar
	- Square wave

- Signalen kunnen analoog of digitaal zijn
## Hoe maken we van data een signaal
- Data
	- Digitale informatie
	- Analoge informatie
- Door een encoder vervormd tot golven
- Om data om te zetten in een signaal hebben we een golf nodig
	- Meestal een simpele sinus golf
- Om data toe te voegen, moeten we het signaal moduleren
	- Amplitude modulatie
	- Frequentie modulatie
	- Fase modulatie
		- De golf verder of terug 
		- De hoek moduleren
## Problemen bij het verzenden van een signaal
- Energieverlies (Attenuation)
	- Weerstand in een koperen kabel
- Vorm verandering (Distortion)
	- Samenvoegen van signalen
- Ruis (Noise)
- Dit alles samen heet **transmission impairments**
## Oplossingen
- Energieverlies
	- Een versterker
- Vorm verandering
	- Lagere bitrate
- Ruis
	- Sterker beginsignaal (carrier wave)
	- SNR (Signal To Noise Ratio)
## Soorten medium
- Begeleid
	- Fysieke verbinding tussen A en B
	- Twisted pair
	- Coaxial cable
	- Fibre optics cable
- Onbegeleid
	- Onzichtbare verbinding tussen A en B
	- Radio (Wi-Fi, Bluetooth)
# OSI Datalink laag
- De datalink laag zorgt voor een betrouwbare gegevensoverdracht tussen direct verbonden apparaten door middel van framing, fysieke adressering en foutdetectie (vanuit de fysieke laag).
- Protocol Data Unit (PDU): **Frames**
## Datalink laag error detectie
- Data vanuit de fysieke laag is niet altijd error vrij
	- Als er een fout is gedetecteerd: Vragen of het bericht opnieuw verzonden kan worden (als dat mogelijk is)
- Error detectie algoritmes:
	- Parity bit
	- Cyclic Redundancy Check (CRC)
### Parity bit
- Deze methode kan enkelvoudige bitfouten opsporen, maar niet corrigeren of meerdere fouten detecteren.
- Aantal 1'tjes in het signaal tellen, als oneven aantal dan heb je **Even Parity**, anders **Odd Parity**
- Voorbeeld:
	- 1011 -> oneven -> Even Parity
	- 0000 -> even -> Odd Parity
### CRC
- Lastig polynoom errordetectie algoritme
- Is "slimmer" dan Parity Bit, het kan meer soorten errors detecteren en ook corrigeren
# Frames
- Data wordt opgesplitst in korte segmenten voor verzending
- Elk segment bevat extra informatie (metadata):
	- Afzender en ontvanger
	- Lengte van het segment
	- Type bericht (normaal, foutmelding, controlebericht)
	- Foutdetectiecodes (Parity Bit, CRC)
## Soorten Frames
- Ethernet frames
	- Bedrade netwerken
	- Maakt gebruik van **MAC-Adressen** (6-byte integers) om apparaten de identificeren
	- Ethernet frame bevat:
		- Ontvanger MAC
		- Zender MAC
		- Type / Grootte
		- Data
		- Padding (als nodig)
		- CRC
- Wi-Fi frames
	- Draadloze netwerken
	- Wi-Fi frame bevat:
		- Frame Control
			- Type frame
		- Duration / ID
			- Timing informatie en identificatie
		- Adres 1, 2, 3 (MAC-adressen van afzender, ontvanger en router / access point)
			- Het signaal moet via de access point verbinden met de ontvanger, deze vertaalt het signaal van draadloos naar bedraad
		- Sequence Controle
			- Helpt met het ordenen van de fragmenten
		- Data
		- FCS (Frame Check Sequence)
			- Errordetectie, vergelijkbaar met CRC