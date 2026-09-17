SSH key passphrase cracking
```bash
ssh2john <ssh_key_file> > key_hash.txt
```
```bash
john --wordlist=/usr/share/wordlists/rockyou.txt key_hash.txt
```