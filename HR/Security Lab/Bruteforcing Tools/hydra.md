Is een [[Bruteforcing Tools|bruteforcing tool]].

> [!warning]
> Krachtig, ook extreem luid. Triggert lockouts/IDS in echte engagements.

Kan dictionary attacks tegen SSH, FTP, HTTP, SMB, SNMP, etc.

```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt ssh://<IP> -V
```
- `-l` - Login username.
- `-L` - Login username wordlist.
- `-P` - Password wordlist.
- `-V` - Verbose mode.
[Cheat Sheet](https://github.com/frizb/Hydra-Cheatsheet)
# Brute force HTTP login form
```bash
hydra -l admin -P /usr/share/wordlists/rockyou.txt <IP> http-post-form "/login.php:username=^USER^&password=^PASS^:F=Wrong" -V
```
The string na `http-post-form` heeft 3 waardes gesplitst met een `:`.
- De eerste is de pagina op de web server om GET of POST naar te doen.
- De tweede zijn de GET of POST variabeles, de `^USER^` en `^PASS^` macro's worden door Hydra ingevuld.
- De laatste is de string waar Hydra voor succes of falen mee checkt. Invalide conditie aangegeven met `F=`, valide conditie aangegeven met `S=`.