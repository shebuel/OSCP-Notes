## Port

### Autorecon
```bash
sudo $(which autorecon) <OPTIONS>
```
```bash
sudo $(which autorecon) -t <target_file> -o <output_dir> -vv
```

### Nmap Automator
```bash
./nmapAutomator.sh -H academy.htb -t Recon #<-- Basic Recon
./nmapAutomator.sh -H 10.1.1.1 -t Port #<-- Full port scan
```

## SMB

### Null User
```bash
smbclient --no-pass -L //<IP> # Null user
smbmap -H <IP> [-P <PORT>] #Null user
crackmapexec smb <IP> -u '' -p '' --shares #Null user
```

### Enumerate Shares
```bash
smbclient --no-pass //<IP>/<Folder>
smbmap [-u "username" -p "password"] -R [Folder] -H <IP> [-P <PORT>] # Recursive list
```

### Enumerate Users
#### Null auth
```bash
crackmapexec smb 10.129.227.255 -u '' -p '' --continue-on-success
```
#### With creds
```bash
crackmapexec smb 10.129.227.255 -u <username/users_list.txt> -p <password/password_list.txt> --continue-on-success
```

### Download Share Folder
```bash
#Download all
smbclient //<IP>/<share>
> mask ""
> recurse
> prompt
> mget *
#Download everything to current directory
```

