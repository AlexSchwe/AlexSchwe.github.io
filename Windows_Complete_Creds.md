---
title: Exploit_Creds_Windows
permalink: /Windows/Exploit_Creds
---

## Use bloodhound ##
```/home/kali/.local/bin/bloodhound-python -u $USER -p $PASSWORD -d $DC -ns $IP -c All````
```zip info.zip *.json```

```ldapdomaindump <IP> [-r <IP>] -u '<domain>\<username>' -p '<password>'```
## To interpretoutput
```ldd2pretty --directory .```

##To find Contrained Delegation

```grep "DELEGATION" *.grep```` 

Then, extract the hash of managed services with https://github.com/micahvandeusen/gMSADumper
