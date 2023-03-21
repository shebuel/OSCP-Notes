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

#PowerUP 
To include the powerup module
```powershell
. .\PowerUp.ps1
```
or
Drop all of the files in the default powershell module path
	The default per-user module path is: 
```ps
"$Env:HomeDrive$Env:HOMEPATH\Documents\WindowsPowerShell\Modules"
```
	The default computer-level module path is:
```ps
"$Env:windir\System32\WindowsPowerShell\v1.0\Modules"
```

### Run All checks

#PowerUP :
```powershell
Invoke-AllChekcs
```
BeRoot:
```powershell
.\beRoot.exe
```
Privesc:
```powershell
Invoke-PrivEsc
```

### Misconfigured Services

- Services with unquoted paths and space in name #PowerUP 
```powershell
Get-ServiceUnquoted -Verbose
```
	Make sure that the service has a higher priv than ur current priv and the service can be restarted
- Services where current user can write to the binary path
```powershell
Get-ModifiableServiceFile -Verbose
```
- Services whose config current user can modify
```powershell
Get-ModifiableService -Verbose
```
 