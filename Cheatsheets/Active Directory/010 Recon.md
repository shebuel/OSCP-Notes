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


### Basic computer information

Architecture
```cmd
wmic os get osarchitecture || echo %PROCESSOR_ARCHITECTURE% #Get architecture
systeminfo
```
Environment variables
```cmd
set
```

#### User info
```powershell
powershell -ep bypass
import-module .\Powerview.ps1
#Disable ASMI
Get-DomainUser
Get-DomainUser -Name somename #show only that user
Get-DomainUser -SPN #List services?
Get-DomainUser -Properties samaccountname, memberof #list all users with only those columns
Get-DomainUser -Properties samaccountname, Description
```

#### Group Info
```powershell
Get-DomainGroup
Get-DomainGroup -Name "Domain Admins"
Get-DomainGroupMember -Name "Domain Admins" -Recurse #list all members of domain admin
```

#### Enumerate Shares

```powershell
#Enumerate Domain Shares
Find-DomainShare

#Enumerate Domain Shares the current user has access
Find-DomainShare -CheckShareAccess
```

### Defensive Mechanisms

#### App locker policies
```powershell
Get-ApplockerPolicy -Effective -xml

Get-AppLockerPolicy -Effective | select -ExpandProperty RuleCollections

$a = Get-ApplockerPolicy -effective
$a.rulecollections
```

AppLocker rules applied to a host can also be **read from the local registry** at **`HKLM\Software\Policies\Microsoft\Windows\SrpV2`**.

#### Status of Defender
```powershell
Get-MpComputerStatus
```

#### Powershell Language mode

```powershell
$ExecutionContext.SessionState.LanguageMode
#Values could be: FullLanguage or ConstrainedLanguage

#Bypass
Powershell -version 2
```

#### LAPS 

Check for ms-msc-AdmPwd and ms-mcs-AdmPwdExpirationTime in computer object to detect the use of LAPS
Also shows up in result of winPeas.sh

```powershell
#Check if present
reg query "HKLM\Software\Policies\Microsoft Services\AdmPwd" /v AdmPwdEnabled
# Find GPOs that have "LAPS" or some other descriptive term in the name
Get-DomainGPO | ? { $_.DisplayName -like "*laps*" } | select DisplayName, Name, GPCFileSysPath | fl
# Search computer objects where the ms-Mcs-AdmPwdExpirationTime property is not null (any Domain User can read this property)
Get-DomainObject -SearchBase "LDAP://DC=sub,DC=domain,DC=local" | ? { $_."ms-mcs-admpwdexpirationtime" -ne $null } | select DnsHostname

#Checks from payloadallthethings
Get-ChildItem 'c:\program files\LAPS\CSE\Admpwd.dll'
Get-FileHash 'c:\program files\LAPS\CSE\Admpwd.dll'
Get-AuthenticodeSignature 'c:\program files\LAPS\CSE\Admpwd.dll'

#Check who has read access to LAPS
# List who can read LAPS password of the given OU
Find-AdmPwdExtendedRights -Identity Workstations | fl
# Read the password
Get-AdmPwdPassword -ComputerName wkstn-2 | fl

```

### Recycle Bin
```powershell
dir C:\$Recycle.Bin /s /b
```

