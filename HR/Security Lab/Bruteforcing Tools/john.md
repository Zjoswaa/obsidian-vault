Password hash cracking
```bash
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt --format=Raw-SHA256
```
- `--format` - Specificeer het hash algoritme, `john --list=format` voor alle mogelijke formats.

SSH key passphrase cracking
```bash
ssh2john <ssh_key_file> > key_hash.txt
```
```bash
john key_hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```