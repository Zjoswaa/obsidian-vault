Onderdeel van [[Metasploit]].

Open de console.
```bash
msfconsole
```
- `-q` - Print niet de ASCII art tijdens startup.
---
Zoek voor een exploit. Geeft een lijst terug met ID's.
```bash
msf > search <term>
```
Info over bepaalde ID.
```bash
msf > info <ID>
```
Selecteer een bepaalde ID voor gebruik.
```bash
msf > use <ID>
```
Toon de opties over de geselecteerde ID.
```bash
msf > show options
```
Vul een optie in van de geselecteerde ID.
```bash
msf > set <option> <value>
```
Toon de mogelijke payloads.
```bash
msf > show payloads
```
Selecteer een payload om te gebruiken.
```bash
msf > set payload <path>
```
Vul een optie in van de payload.
```bash
msf > set <option> <value>
```
Test of de target vulnerable is, stuurt nog geen payload.
```bash
msf > check
```
Start de exploit met de ingevulde opties.
```bash
msf > exploit
```
Stop de console.
```bash
msf > quit
```

Als de exploit lukt, krijg je een `meterpreter` sessie shell.
Deze sessie kan je in de background zetten met `Ctrl + Z` of `background` command.

Laat sessions zien.
```bash
msf > sessions
```
Terug naar specifieke session, op ID.
```bash
msf > sessions -i <ID>
```
Stop sessie, op ID
```bash
msf > sessions -k <ID>
```
Stop alle sessies.
```bash
msf > sessions -K
```
