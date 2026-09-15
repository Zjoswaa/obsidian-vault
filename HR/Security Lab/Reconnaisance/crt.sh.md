Voorbeeld van passive [[Reconnaisance|reconnaisance]].

Zoeken naar certificaten die op dit domein staan.
Is ook een website: [https://crt.sh](https://crt.sh)

Kan ook met `curl` in de terminal.
```bash
curl -s "https://crt.sh/?q=<domain>&output=json" | jq -r '.[].name_value' | sort -u
```
