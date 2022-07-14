---
title: Forensics
permalink: /Forensics
---

#create username login based from a list of names
/username-anarchy --input-file fullnames.txt --select-format first,flast,first.last,firstl > unames.txt
#Linux searching for recent files
find -type f -newermt '2022-01-01' -ls
