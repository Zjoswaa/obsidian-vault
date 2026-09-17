Is een [[Bruteforcing Tools|bruteforcing tool]].

> [!warning]
> Krachtig, ook extreem luid. Triggert lockouts/IDS in echte engagements.

Kan dictionary attacks tegen SSH, FTP, HTTP, SMB, SNMP, etc.

```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt ssh://10.10.10.x
```
- `-l` - Login username.
- `-L` - Login username wordlist.
- `-P` - Password wordlist.
[Cheat Sheet](https://github.com/frizb/Hydra-Cheatsheet)
