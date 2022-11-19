The hunt for local Admin Access

Methods:
- Missing patches
- Automated deployment and AutoLogon passwords in clear text
- AlwaysInstallElevated (any user can run MSI as SYSTEM)
- Misconfigured Services
- DLL Hijacking
- More?

Tools:
- PowerUP
- BeRoot
- Privesc (enjoiz)

### Misconfigured Services

- Services with unquoted paths and space in name #PowerUP 
```powershell
Get-ServiceUnquoted -Verbose
```
- Services where current user can write to the binary path
```powershell
Get-ModifiableServiceFile -Verbose
```
- Services whose config current user can modify
```powershell
Get-ModifiableService -Verbose
```
 