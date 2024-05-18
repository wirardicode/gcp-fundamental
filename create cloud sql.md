# create sql use shell
open your shell

copy this command
--
gcloud sql instances create instance_name --tier=machine_type --region=location
<br>
gcloud sql users set-password root --host=% --instance=instance_name --password=password

# create sql use console

Navigate to sql
--
navigate to sql in cloud navbar

choose database engine
--
you can choose one of three (mysql, postgresql, sql server) *I use mysql

configuration
--
1. instance ID= "create your own"<br>
2. password= "create your own"<br>
3. database version = choose mysql 5.7 or up to you<br>
4. cloud sql edition = Enterprise<br>
5. Region= choose one of all<br>
6. zone = single zone or up to you<br>

Show Configuration Options
--
1. Machine configuration= share core or up to you<br>
2. Storage= HDD or SSD<br>
3. Connections= set default or make your own<br>

then click <b>Create Instance</b>

set network
--
1. to connetion menu on left
2. add network on authorized networks
3. set name = "public" or your own
4. network range = 0.0.0.0/0 or yours
