---
title: Windows Recon
permalink: /Enumeration/Windows
---


<title>{{ page.title }}</title>

### With windows, add dc.$BOX to /etc/hosts ###

### Port 80 ### 
To enumerate on a web page with iis
download iisfinal.txt on https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/iis-internet-information-services

```ffuf -w /home/kali/Downloads/iisfinal.txt -u http://$IP_BOX/FUZZ -recursion```

### Alternative ####

```dirsearch.py -u https://$IP_BOX/ -e aspx,txt```
## If Password requested, you can brute force using  
```hydra `$IP http-form-post "/form/frontpage.php:user=admin&pass=^PAS S^:INVALID LOGIN" -l admin -P /usr/share/wordlists/rockyou.txt -vV -f```
```medusa -h 10.11.0.22 -u admin -P /usr/share/wordlists/rockyou.txt -M http -m DIR:/admin```
### Grab passwords from website
```cewl -d 7 -m 8 -w --with-numbers cewl.out http://$page_to_crawl```
## Check when a page appears
atch -n "curl http://$page"

### Port 445 ###

```crackmapexec smb $BOX```  
```crackmapexec smb $BOX --shares```

```crackmapexec smb $BOX --shares -u '' -p ''```

```smbmap -H $BOX -u ''```

```smbmap -u anonymous -H $IP_BOX```

```smbmap -u anonymous -H $IP_BOX -R $open_share```

```smbclient -U 'anonymous' -N $BOX```` 
```enum4linux```


### RPC
```rpcclient $BOX```  
```rpcclient -U '' -N $BOX  
>enumdomusers
>querydispinfo
>querydispinfo2
>querydispinfo3```` 
#### S'il y a des drivers ou printers dans les comptes
```>enumprinters` 
>enumdrivers```  
##To clean usernames  
```rpcclient -U '' -N $BOX -c "enumdomusers"  | cut -d "[" -f2 | cut -d ']' -f1 > users.txt```


## Ldap,445

#### To get naming context
```ldapsearch -x -h $BOX -s base namingcontexts```` 
#### Then copy the DC  
```ldapsearch -x -h $BOX -b '$DC;'```

```./windapsearch.py -d $DC.local --dc-ip $IP_BOX -U --full  
GetADUsers.py `$DC.local/ -dc-ip $IP_BOX -debug```



## NFS
```showmount -e $IP```

