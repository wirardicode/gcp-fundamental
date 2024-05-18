# Create VM Instance use cloud shell and run VM

# create vm us shell

open Cloud shell
--
first you must open cloud shell

copy this command to create instance
--
gcloud compute instances create <<VM_name>>

chek your VM
--
ping <<external_IP>>

delete your vm
--
gcloud compute instances delete <<VM_name>>

# use console

step 1
--
fine compute engine on nav bar

step 2
--
configur your
1. name = "your instance name"
2. region & zone = "choose region use dropdown"
3. machine configuration = "eg: E2"
4. machine type = "eg: e2 micro"
5. boot disk = "choose your os"
6. identity and api access = "let it default or set it like you want"
7. firewall = " checklist on allow HTTP Trafic"
8. advance option = "let it default or set it like you want"

# run your server

use ssh
--
open ssh by console on right vm list table or use this command : gcloud compute ssh <<vm_name>> zone <<zone>>

install nginix server
--
sudo apt-get install nginx

check if server already run
--
click on vm external IP

open editor use this command
--
sudo nano /var/www/html/index.nginx-debian.html

change html code or let it default
--
you can change it or let it default<br>
if you done to change it you can press ctrl+X key then press y key
