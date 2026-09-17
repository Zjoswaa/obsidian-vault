Is een [[Web Traffic Interception|web traffic interception]] tool.
# Setup
Zet eerst in Firefox je proxy aan, dit kan makkelijk met FoxyProxy, of lastiger via de Firefox proxy settings. Proxy `127.0.0.1:8080`.
```bash
mitmproxy --listen-port 8080
```
Terwijl de proxy aan staat, ga naar `http://mitm.it`.
Download daar de certificate, de `.pem` file.
Ga dan naar Firefox settings, View Certificates, Install, selecteer de `.pem` file.
Vink "Trust this CA to identify websites." aan.
# Gebruiken
- Zet je proxy aan, via ProxyFoxy of Firefox settings op `127.0.0.1:8080`.
- Doe daarna weer:
```bash
mitmproxy --listen-port 8080
```
