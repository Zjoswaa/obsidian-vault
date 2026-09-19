Is een [[Bruteforcing Tools|bruteforcing tool]].

```bash
ffuf -w /usr/share/wordlists/dirb/common.txt -u http://testasp.vulnweb.com/FUZZ -fc 404
```
```bash
ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -u http://FUZZ.hr.nl -fs 1234
```
```bash
ffuf -u http://hr.nl -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -H "Host: FUZZ.hr.nl" -fs 0
```
- `-fc` - Filter response status code.
- `-mc` - Match response status code.
- `-fs` - Filter response size.
- `-fw` - Filter aantal woorden in de response.
- `-H` - Spoof request header.
# Valide username vinden
```bash
ffuf -w /usr/share/wordlists/seclists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://<IP>/signup -mr "username already exists"
```
- `-X` - Request method.
- `-mr` - Match regular expression.
- `-d` - POST data.
# Wachtwoord van valide username vinden
```bash
ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/seclists/Passwords/Common-Credentials/10k-most-common.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://<IP>/login -fc 200
```
Er kunnen meerdere wordlists tegelijk worden gebruikt, je kan ze namen geven. `W1` en `W2` in dit voorbeeld.