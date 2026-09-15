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
- `-H` - Spoof request Host header.
