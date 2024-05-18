# connect your own slq
you must have sql first, then save your sql Public IP

run this command
--
udo apt-get update

install sql client
--
sudo apt-get install mysql-client

connect your sql
--
mysql -h <<sql_public_IP>> -u root -p
<br>
now you can make dabase, make table and anything use sql command
<br>
for exit from sql command use <b>exit</b>
