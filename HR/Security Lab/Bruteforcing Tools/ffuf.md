Is een [[Bruteforcing Tools|bruteforcing tool]].

```bash
ffuf -w /usr/share/wordlists/dirb/common.txt -u http://testasp.vulnweb.com/FUZZ -fc 404
```
```bash
ffuf -w subs.txt -u http://FUZZ.hr.nl -fs 1234
```
```bash
ffuf -u http://10.10.10.1 -H "Host: FUZZ.hr.nl"
```
- `-fc` - Filter op response status code.
- `-fs` - Filter op response size.
- `-mc` - Match codes.
- `-H` - Spoof request header.
```bash
ffuf -w /usr/share/wordlists/seclists/Usernames/Names/names.txt -X POST -d "username=FUZZ&email=x&password=x&cpassword=x" -H "Content-Type: application/x-www-form-urlencoded" -u http://<IP>/signup -mr "username already exists"
```
- `-X` - Request method.
- `-mr` - Match regular expression.
- `-d` - POST data.
```bash
ffuf -w valid_usernames.txt:W1,/usr/share/wordlists/seclists/Passwords/Common-Credentials/10k-most-common.txt:W2 -X POST -d "username=W1&password=W2" -H "Content-Type: application/x-www-form-urlencoded" -u http://<IP>/login -fc 200
```
Multiple wordlists can be used and given a name, `W1` and `W2` in this example.