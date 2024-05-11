## Server
- select ```server``` folder and choose ```Open in integrated Terminal```
- create ```.gitignore``` file and add ```node_modules``` to it
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
- test going to http://localhost:3000

## Docker
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
- run Docker Desktop
- create and push an image to Docker Hub, or do it using cli
    - ```docker build . -t decel_server:latest```
    - ```docker image tag decel_server hsmptg/decel_server```
    - ```docker image push docker.io/hsmptg/decel_server:latest```

## Portainer
- create stack decel_server with
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
- test going to http://10.0.5.111:3001

## Postman
Install Postman extension