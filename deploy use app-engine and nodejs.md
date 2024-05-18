# deploy use app-engine and node.js

create app engine
--
open app engine and click <b>create application</b><br>
configur zone and service account<br>
clcick <b>next</b><br>
after that choose <b>I'll do this later</b> for program language

code
--
make your own code or use this repo<br>
git clone -b gae-lab https://github.com/dicodingacademy/a133-gcp-labs.git

change directory
--
cd a133-gcp-labs/ 

run in local
--
npm start<br>
then use <b>preview</b> and change port into 8000

create file
--
create file name <b>app.yaml</b><br>
then copy this code<br>
runtime: nodejs20
service: "service_name" or "default"

deploy it
--
gcloud app deploy
