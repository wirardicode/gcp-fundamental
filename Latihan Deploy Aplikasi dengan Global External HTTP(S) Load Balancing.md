# Deploy Aplikasi dengan Global External HTTP(S) Load Balancing

cofiguration firewall rule
--
1. open in gcp console Navigation menu -> VPC network -> Firewall.<br>
2. click over <b>Create Firewall Rule</b>,
3. fill in the:<br>
Name: allow-http <br>
Network: default<br>
Targets: Specified target tags<br>
Target tags: http-server<br>
Source filter: IPv4 ranges<br>
Source IPv4 ranges: `0.0.0.0/0`<br>
Protocols and ports: select Specified protocols and ports, checklist on tcp, fill in `80`.<br>
4. then create
5. create new fire wall again with:<br>
Name: allow-health-check<br>
Network: default<br>
Targets: Specified target tags<br>
Target tags: http-server<br>
Source filter: IPv4 ranges<br>
Source IPv4 ranges: `130.211.0.0/22`, `35.191.0.0/16`<br>
Protocol and ports: select Specified protocols and ports, checklist on `tcp`.<br>

create instance tamplate and instance group
--
- you must open <b>Compute Engine > Instance templates.</b> <br>
- click on <b>create instance template</b><br>
- fill in name of instance tamplate<br>
- let another default<br>
- open advance seting (Network, disk, security, management, and sole-tenancy) then go to Management seting and fill in Startup script <b>with code below</b>: <br>
`sudo apt-get update`<br>
`sudo apt-get install apache2 -y` <br>
`echo '<!doctype html><html><body><h1>Hello from Jakarta!<h1></body></html>' | sudo tee /var/www/html/index.html`<br>
- open networking (still in advance setting)-> Network interfaces
- select <b>Subnetwork</b> then select <<your_region>> on Network tag select `http-server` then create.

create another instance tamplate
--
to make it easy, checklist on first instance then copy then change the name and on the management fill out last line code with `echo '<!doctype html><html><body><h1>Hello from Belgium!<h1></body></html>' | sudo tee /var/www/html/index.html`<br>
, on networking change subnet into <<your_difrent_region>>, and network tag `http-server`

create instance group
--
- find instance group<br>
- fill the form<br>
  Name: "instance name"<br>
  Location: "Multiple zones" or "your own selected"<br>
  Region: "your_region"<br>
  Instance template: "your created instance tamplate before"<br>
  Autoscaling policy:<br>
    1. Metric type = `CPU utilization`<br>
    2. Target CPU utilization= `80`<br>
    3. minimum instance number = `1`<br>
    4. Maximum instance number = `5`<br>
- then create instance<br>

create another instance group
--
how to make it? it <b>it same like above</b> but change the name, region, and instance tamplate follow your second instance tamplate you had made before.

open vm instance
--
open it and copy all external IP then copy at new tap, or just click those.

configure load balancer
--
- Navigation Menu -> Network services -> Load balancing, then klik Create Load Balancer.
- select Start configuration on HTTP(S) Load Balancing. when option showed, let it default within click Continue because we will use external load balancer with global scope
- set load balancer name, <b>eg: "http-lb".</b>
- on Backend configuration, click on Backend services & backend buckets columns, then select <b>Create a Backend Service</b>.
- set name for backend service, <b>eg: http-backend</b>
- add new backend use instance group you create before and fill in `80` at port numbers column
- on balancing mode, use rate mode then fill RPS at `50` or you can seet more or less of 50
- add new backend again and use anoter one of instance group you create before and fill `80` at port numbers, let another set default, then click <b>Done</b>.
- on healt check field, click on <b>create a healt check</b>
- fill healt check name with `http-health-check`, then change protocol into http then save
- then click create on bottom session (it's mean you will create backend after already set all configur).
- Next select frontend, select `IPv4` on IP version, then select `Ephemeral` on ip address then `80` for port. click <b>Done</b>
- click <b>Add Frontend IP and Port</b> select `IPv6`, then select `Ephemeral`, fill port with `80`. click <b>Done</b>
- <b>Optional:</b> for review all set use <b>Review and finalize </b>
- click create button
- when it done copy your IP:Port into new tab, <b>Yeayyy You already in into your website on http protocol, and in nearly server from your location🔥🔥</b>
- try to use vpn for use another server use your IPv4

# Stress Test terhadap Load Balancer
stress test digunakan untuk test pembagian beban kerja pada load balance

install sige on shell
--
`sudo apt-get install siege`

start stress test
--
`siege -c 250 http://<<load_balancer_ip>>`

Don't copy this
--
`** SIEGE 4.0.4`<br>
`** Preparing 250 concurrent users for battle`.<br>
`The server is now under siege...`<br>
<b>This code is result while stress test</b>

- open your load balancing then click monitoring, then you will see the trafic
