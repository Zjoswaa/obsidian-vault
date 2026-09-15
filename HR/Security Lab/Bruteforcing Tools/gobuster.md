Is een [[Bruteforcing Tools|bruteforcing tool]] om bereikbare subdomeinen van een domein te vinden.

```bash
gobuster dir -u http://10.10.10.x -w /usr/share/wordlists/dirb/common.txt -t 8
```
```bash
gobuster vhost -u http://hr.nl -w subs.txt --append-domain
```
- `-u` - URL om te bruteforcen.
- `-w` - Wordlist om te gebruiken.
- `-t` - Multithread count.

Goede wordlist voor virtual hosts:
- `seclists` package op Kali.
	- `/usr/share/wordlists/seclists/Discovery/DNS/fierce-hostlist.txt`
- Of op [GitHub](https://github.com/danielmiessler/seclists)