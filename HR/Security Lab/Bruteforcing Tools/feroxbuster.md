Is een [[Bruteforcing Tools|bruteforcing tool]]. Vergelijkbaar met [[gobuster]]. Geschreven in Rust, dus snel.

```bash
feroxbuster -u http://10.10.10.x -w /usr/share/wordlists/dirb/common.txt -d 2 -s 200
```
```bash
feroxbuster -u http://10.10.10.x -C 404 -t 4
```
- `-d` - Recursion depth.
- `-s` - Selecteer op status code.
- `-C` - Filter op status code.
- `-t` - Multithread count.
- `--auto-tune` - Als er responses terug komen zoals `403 (Forbidden)`, `429 (Too many requests)`, of als er te veel timeouts zijn, gaat de tool langzamer requests sturen.
- `--auto-bail` - Als er responses terug komen zoals 403 (Forbidden), 429 (Too many requests), of als er te veel timeouts zijn, stopt de tool met individuele directory scans.