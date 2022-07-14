---
title: OSINT
permalink: /OSINT
---

## Get info about domain name or ip
```whois $IP```

## google hacking

site:megacorpone.com
filetype:php
#The ext operator could also be helpful to discern what programming languages might be used on a web site. Searches like 
ext:jsp, ext:cfm, ext:pl 
#will find indexed Java Server Pages, Coldfusion, and Perl pages respectively.
#exclude html result
-filetype:html

#directory listing
intitle:“index of” “parent directory”

#info on technology used
https://searchdns.netcraft.com

#or use econ-ng

#search code on github if one github account has leaked
#Use gitrob or gitleaks to exploit large repositories

#search on shodan hostname:megacorpone.com. Would crawl any device connected to the internet
#search on pastebin

#find emails
theharvester -d megacorpone.com -b google

#scan twitter
Twofi

#scan linkedin
linkedin2username

#search on stackoverflow
#for large information searching, have a look at maltego

Active
#zonetransfer
kali@kali:~$ host -l megacorpone.com ns1.megacorpone.com
Bash script to automate the process of identifying the relevant nameservers and attempting a zone transfer from each:
#!/bin/bash
# Simple Zone Transfer Bash Script
# $1 is the first argument given after the bash script # Check if argument was given, if not, print usage
if [ -z "$1" ]; then
echo "[*] Simple Zone transfer script" echo "[*] Usage : $0 <domain name> " exit 0
fi
# if argument was given, identify the DNS servers for the domain
for server in $(host -t ns $1 | cut -d " " -f4); do
# For each of these servers, attempt a zone transfer host -l $1 $server |grep "has address"
done

#dnsenumeration
kali@kali:~$ dnsrecon -d megacorpone.com -t axfr
kali@kali:~$ dnsenum zonetransfer.me 

Utiliser le Google mais russe pour éviter les bâtiments floutés 
Et open street cam ou Mapillary
Tiktok et snapchat 
Voir les badges pour les imiter
Regarder zonedinteret.blogspot
Regarder les ventes aux enchères du matériel informatique
Papers.fr : informations sur la société et les associés, signature du patron
www.bellingcat.fr
Tester l'existence des mails sur have i been pawned
Et sur EPEIOS
