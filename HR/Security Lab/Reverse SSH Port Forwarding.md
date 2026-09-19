Reverse SSH port forwarding specifies that the given port on the remote server host is to be forwarded to the given host and port on the local side.

`-L` is a local tunnel (YOU <-- CLIENT). If a site was blocked, you can forward the traffic to a server you own and view it. For example, if imgur was blocked at work, you can do `ssh -L 9000:imgur.com:80 <user>@<IP>` Going to localhost:9000 on your machine, will load imgur traffic using your other server.

`-R` is a remote tunnel (YOU --> CLIENT). You forward your traffic to the other server for others to view. Similar to the example above, but in reverse.
# Example
If SSH'd to a host and [[ss]] shows a port 10000 that is blocked from outside with a firewall, you can set up a tunnel from your local machine:
```
ssh -L 10000:localhost:10000 <user>@<ip>
```
Afterwards you can visit `localhost:10000` on your machine  to view the page.