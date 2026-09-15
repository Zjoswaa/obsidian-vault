Voorbeeld van passive [[Reconnaisance|reconnaisance]].

Vind de `A` records van het domein.
```bash
dig <domain> A
```
Vind de `AAAA` records van het domein.
```bash
dig <domain> AAAA
```
Vind de `MX` records van het domein.
```bash
dig <domain> MX
```
Vind de `TXT`records van het domein.
```bash
dig <domain> TXT
```
Vind zone transfer informatie van de DNS server, staat vaak uit.
```bash
dig <domain> AXFR
```
Vind de nameservers van het domein.
```dig
dig ns <domain>
```
- `@<server>` - Gebruik een andere DNS server om de resultaten te vinden. Bijvoorbeeld `@8.8.8.8`.
- `+short` - Laat resultaten in het kort zien.
- `+dnssec` - Laat ook dnssec informatie zien.
- `+recurse` - Query ook recursief andere DNS servers.