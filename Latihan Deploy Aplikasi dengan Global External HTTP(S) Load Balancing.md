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
Source IPv4 ranges: 0.0.0.0/0<br>
Protocols and ports: select Specified protocols and ports, checklist on tcp, fill in 80.<br>
4. then create
5. create new fire wall again with:<br>
Name: allow-health-check<br>
Network: default<br>
Targets: Specified target tags<br>
Target tags: http-server<br>
Source filter: IPv4 ranges<br>
Source IPv4 ranges: 130.211.0.0/22, 35.191.0.0/16<br>
Protocol and ports: select Specified protocols and ports, checklist on tcp.<br>

create instance tamplate and instance group
--
- you must open <b>Compute Engine > Instance templates.</b> <br>
- click on <b>create instance template</b><br>
- fill in region or location<br>
- let another default<br>
- open advance seting (Network, disk, security, management, and sole-tenancy) then go to Management seting and fill in Automation scrip <b>with code below</b>: <br>
sudo apt-get update <br>
sudo apt-get install apache2 -y <br>
echo '<b>(html script without head tag)</b>' | sudo tee /var/www/html/index.html<br>
