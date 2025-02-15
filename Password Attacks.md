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

However, a few more files belong to the user management system of Linux. The other two files are `/etc/passwd` and `/etc/group` 
**Note!** : only be read by root. 