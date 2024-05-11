## Setup

First steps:
- create ```app``` and ```server``` folders
- create ```README.md``` file
- create [README.md](app/README.md) file inside app folder
- create [README.md](server/README.md) file inside server folder

## Server
- select ```server``` folder and choose ```Open in integrated Terminal```
- execute ```npm init -y```
- edit packages.json replacing ```index.js``` by ```server.js```
- install nodemon running ```npm install --save-dev nodemon```
- also replace the test script, by: ```"dev": "nodemon server.js"```
- install express by running: ```npm install express```
- create ```server.js``` file and add the following to it:
```
const express = require('express');
const app = express();
const port = 3000;

app.get("/", (req, res) => {
	res.send('Hello World!!!');
});

app.listen(port, () => {
  console.log(`Server is running on port ${port}`);
});
```
- run the server using nodemon: ```npm run dev```
- create ```.gitignore``` file and add ```node_modules``` to it
- create ```.dockerignore``` file and add ```node_modules``` to it
- create ```Dockerfile``` file
```
FROM node:18-alpine
WORKDIR /server
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD [ "npm", "start" ]
```
- run Docker Desktop or do it from de CLI
- create image running ```docker build . -t decel_server:latest```
- ```docker image tag decel_server hsmptg/decel_server```
- ```docker image push docker.io/hsmptg/decel_server:latest```
- at Portainer create stack decel_server with
```
version: '3'
services:
  server:
    container_name: decel_server
    image: docker.io/hsmptg/decel_server:latest
    restart: always
    ports:
      - 3001:3000
```
- test goint to http://10.0.5.111:3001

## App
- select ```app``` folder and choose ```Open in integrated Terminal```
- execute ```npm init -y```
- edit packages.json replacing ```index.js``` by ```server.js```
- install nodemon running ```npm install --save-dev nodemon```
- also replace the test script, by: ```"dev": "nodemon server.js"```
- install express by running: ```npm install express```
- create ```server.js``` file and add the following to it:

## Docker Desktop installation on Windows
Installation steps:
- WSL
- Docker Desktop

### WSL
- open Powershell in Admin mode and run ```wsl --install```
- check version: ```wsl -v```
- if asked enter "Enter new UNIX username" (helio) and password
- when recommended, install 'WSL' extension from Microsoft

### Docker Desktop
- download [Docker Desktop Installer.exe (v4.29.0)](https://docs.docker.com/desktop/install/windows-install/)
- run the executable and check "Use WSL 2 instead of Hyper-V"
- check version: ```docker -v``` (Docker version 26.0.0, build 2ae903e)

### Registry
To store the containers images we need a Registry:
- GitHub is not supported by Portainer Community Edition
- Docker Hub only support 1 private image
- It is possible to self host a registry with https://joxit.dev/docker-registry-ui/