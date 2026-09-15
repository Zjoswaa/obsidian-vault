Voorbeeld van active [[Reconnaisance|reconnaisance]].
```bash
nmap <IP>
```
- `-sS` - Stealth (TCP SYN scan), maakt de 3-way-handshake niet af. Default als `sudo` of root.
- `-sT` - TCP connect scan, maakt de 3-way-handshake af. Default als geen `sudo` en geen root.
- `-sV` - Service version detection.
- `-O` - OS detection.
- `-sC` - Gebruikt default scripts tijdens de scan, zelfde als `--script=default`
- `-A` - Agressive, kort voor `-sV -sC -O --traceroute`.
- `-p 80` - Scan alleen port 80
- `-p 80-443` - Scan port 80 t/m 443.
- `-p-` - Scan alle ports.
- `--top-ports 1000` - Scan de 1000 meest voorkomende ports.
- `-T<0-5>` - Wacht langer tussen twee opeenvolgende scans, `0` wacht het langst, `5` wacht het kortst.
- `-Pn` - Stuur niet eerst een ping packet naar de port om te checken of de port actief is, scan de port sowieso. Handig als een firewall alle ICMP packets dropt waardoor de target offline lijkt.
- `-v` - Verbose, print tussendoor meer messages over scan progressie. `-vv` en `-vvv` zijn nog meer verbose dus nog meer informatie.
# Scripts
`nmap` kan ook bepaalde scripts uitvoeren om bijvoorbeeld op ports vulnerabilities te checken.
```bash
nmap <IP> --script=<script-name>
```
[Documentation](https://nmap.org/nsedoc/scripts/)

Scripts zijn op Kali te vinden in de `/usr/share/nmap/scripts` directory.