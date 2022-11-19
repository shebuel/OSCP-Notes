https://wadcoms.github.io/#


Enumeration done using Native Executables and .NET classes

### Quick Win

Where current user has local Admin
```powershell #PowerView
Find-LocalAdminAccess -Verbose
```
Find local admins on all machines
```powershell #PowerView
Invoke-EnumerateLocalAdmin -Verbose
```
Find machines which have domain admin session/token
```ps
Invoke-UserHunter
Invoke-UserHunter -CheckAccess # Ensures Admin access
```
dol