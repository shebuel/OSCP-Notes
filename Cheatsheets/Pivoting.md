#### SSH

SSH port forward from local box
```bash
ssh -i key -L<local port>:<host to forward to>:<port to forward to> <pivot box ip>
```
SSH dynamic port forward sock5 proxy
```bash
ssh -D<localport> <ip>

# Add to porxychains
vi /etc/proxychains.conf
socks5 127.0.0.1 <localport>

# add proxychains b4 command to send it thro proxy
```
