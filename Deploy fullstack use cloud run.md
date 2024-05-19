# deploy use cloud run
first you must have two code folder, first one is for frontend and last one is backend<br>
I have two directory: Notes App directory for frontend, and Notes API directory for backend

# back-end

Clone backend file
--
use cloud shell then copy this command:<br>
`git clone -b notes-api https://github.com/dicodingacademy/a133-gcp-labs.git notes-api`

change directory
--
`cd notes-api/`

create file name dockerfile
--
`nano Dockerfile`

copy this code and paste to dockerfile
--
`FROM node:14.21.2-alpine`
`WORKDIR /app`
`ENV PORT 5000`
`copy . .`
`RUN npm install`
`EXPOSE 5000`
`CMD["nmp", "run", "start"]`

Active API articat registry, cloud run, cloud build active
--
`gcloud services enable artifactregistry.googleapis.com`
`cloudbuild.googleapis.com`
`run.googleapis.com`

create artifac registry repo
--
`gcloud artifacts repositories create <<new_repo_name>> --repository-format=docker --location=<<region>> --async`

create container image
--
`gcloud builds submit --tag <<region>>-docker.pkg.dev/${GOOGLE_CLOUD_PROJECT}/<<repo_name>>/notes-api:1.0.0`

deploy backend
--
`gcloud run deploy --image <<region>>-docker.pkg.dev/${GOOGLE_CLOUD_PROJECT}/<<repo_name>>/notes-api:1.0.0`

get your service URL
--
copy and paste your backend service url in some place because it will useful

# frontend

change to root directory
--
`cd..`

clone frontend repo
--
`git clone -b notes-app https://github.com/dicodingacademy/a133-gcp-labs.git notes-app`

change directory
--
`cd notes-app/`

create Dockerfile
--
`nano Dockerfile`

copy this code
--
`FROM node:14.21.2-alpine`
`WORKDIR /app`
`COPY . .`
`RUN npm install`
`RUN npm run build`
`EXPOSE 8080`
`CMD [ "npm", "run", "start"]`

make repo to save frontend
--
`gcloud artifacts repositories create <<new_repo_name>> --repository-format=docker --<<region>> --async`

create container image
--
`gcloud builds submit --tag <<region>>-docker.pkg.dev/${GOOGLE_CLOUD_PROJECT}/<<repo_name>>/notes-app:1.0.0`

deploy frontend
--
`gcloud run deploy --image <<region>>-docker.pkg.dev/${GOOGLE_CLOUD_PROJECT}/<<repo_name>>/notes-app:1.0.0`

change url
--
back to console find frontend or notes app then click <b>Change URL</b> after that fill the text box use backend service url
