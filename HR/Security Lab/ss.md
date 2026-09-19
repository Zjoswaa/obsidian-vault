Investigate sockets running on a host.
```bash
ss -tulpn
```
- `-t` - Display TCP sockets.
- `-u` - Display UDP sockets.
- `-l` - Display listening sockets only.
- `-p` - Show the process using the socket.
- `-n` - Dont resolve service names.