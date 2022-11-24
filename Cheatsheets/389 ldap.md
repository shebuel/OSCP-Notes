crackmapexec smb 10.129.227.255 -u '' -p '' --continue-on-success### Recon

#### Without creds

```bash
nmap -n -sV --script "ldap* and not brute"
```
ldap with null auth and creds
```bash
ldapsearch -x -h $ip -s base namingcontexts
ldapsearch -x -H ldap://<IP> -D '' -w '' -b "DC=<1_SUBDOMAIN>,DC=<TLD>"
ldapsearch -x -H ldap://<IP> -D '<DOMAIN>\<username>' -w '<password>' -b "DC=<1_SUBDOMAIN>,DC=<TLD>"
```

#### With creds


Windows specific:
```powershell
# Get computers
python3 windapsearch.py --dc-ip 10.10.10.10 -u john@domain.local -p password --computers
# Get groups
python3 windapsearch.py --dc-ip 10.10.10.10 -u john@domain.local -p password --groups
# Get users
python3 windapsearch.py --dc-ip 10.10.10.10 -u john@domain.local -p password --da
# Get Domain Admins
python3 windapsearch.py --dc-ip 10.10.10.10 -u john@domain.local -p password --da
# Get Privileged Users
python3 windapsearch.py --dc-ip 10.10.10.10 -u john@domain.local -p password --privileged-users
```

Filter specific results by using CN alone with DC as base string

https://book.hacktricks.xyz/network-services-pentesting/pentesting-ldap