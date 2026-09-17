Privilege Escalation Awesome Scripts SUITE
Te vinden op [GitHub](https://github.com/peass-ng/PEASS-ng)

Versies voor Windows en Linux.

Wanneer je ingebroken bent op een systeem, kan je proberen om het script op het systeem te krijgen, in de documentatie staat welke opties je daarvoor hebt.

Een voorbeeld als je de private SSH key hebt van iemand:
```bash
scp -i id_rsa ~/Downloads/linpeas.sh <user>@<IP>:<dir>
```

Deze script kan vervolgens worden uitgevoerd op het systeem en gaat daar zoeken naar allerlei dingen die potentieel nuttig kunnen zijn voor privilege escalation.