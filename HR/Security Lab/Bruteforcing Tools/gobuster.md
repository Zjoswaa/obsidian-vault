Is een [[Bruteforcing Tools|bruteforcing tool]] om bereikbare subdomeinen van een domein te vinden.
# dir mode
```bash
gobuster dir -u http://<IP> -w /usr/share/wordlists/dirb/common.txt -t 8
```
- `-u` - URL om te bruteforcen.
- `-w` - Wordlist om te gebruiken.
- `-t` - Multithread count.
- `-x` - Zoek voor file extensions (`-x .php,.txt,.js`).
- `-r` - Volg redirects.
- `-k` - Doe geen TLS certificaat verificatie.
- `-s` - Laat alleen specifieke status codes zien (`-s 200,301`).
# dns mode (subdomains)
Doet DNS lookups om voor subdomeinen te zoeken.
```bash
gobuster dns --domain example.com -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt --wildcard
```
- `--resolver` - Gebruik een eigen DNS resolver voor lookups.
# vhost mode
Doet geen DNS lookups, het past per request de `Host:` header aan.
```bash
gobuster vhost -u http://<IP> --domain example.com -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt --append-domain
```
- `--domain` - Nodig wanneer je op IP zoekt, zorg dat de host in `/etc/hosts` staat.