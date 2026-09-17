Server Message Block protocol.
Allows communication between Windows, Linux and other machines on a network.
Used to share files, printers and serial ports.
First only implemented for Windows, [[Samba]] is the Linux implementation.
# Ports
SMB commonly uses the 139 and 445 ports.
Port 139 dates back to when SMB ran on top of NetBIOS.
Port 445 is the modern replacement, working over TCP.
# Scanning
Enumerate shares and users using [[nmap]].
```bash
nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse <IP>
```