SHELL=/bin/bash script -q /dev/null
Ctrl-Z
stty raw -echo
fg
reset
xterm

python -c 'import pty;pty.spawn("bash")'
Ctrl-Z
[1]+  Stopped                 nc -lnvp 443
root@kali# stty raw -echo
root@kali# nc -lnvp 443


#webshell list
https://github.com/tennc/webshell
