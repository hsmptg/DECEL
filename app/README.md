## App
Initial steps:
- select ```app``` folder and choose ```Open in integrated Terminal```
- execute ```npm create vite@latest```
    - Project name: .
    - Current directory is not empty: Ignore files and continue
    - React
    - Javascript

- edit ```App.jsx``` with just:
```
import './App.css'

function App() {
  return (
    <h1>DECEL</h1>
  )
}

export default App
```
- edit ```index.html``` from "Vite + React" to "DECEL"
- delete assets folder
- empty index.css and App.css
- ```npm install```
- run the server: ```npm run dev```

- http://localhost:5173/ 
- create ```.gitignore``` file and add ```node_modules``` to it

## Docker
- create ```.dockerignore``` file and add ```node_modules``` to it
- create ```Dockerfile``` file
```
FROM node:18-alpine as build
WORKDIR /app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
FROM nginx:alpine
COPY --from=build /app/dist /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]
```
- run Docker Desktop or do it from de CLI
- create image running ```docker build . -t decel_app:latest```
- ```docker image tag decel_app hsmptg/decel_app```
- ```docker image push docker.io/hsmptg/decel_app:latest```
- at Portainer create stack decel_app with
```
version: '3'
services:
  server:
    container_name: decel_app
    image: docker.io/hsmptg/decel_app:latest
    restart: always
    ports:
      - 8123:80
```
- test goint to http://10.0.5.111:8123

## To see
- [Axios](https://axios-http.com/)
- [Understanding the File Upload Process in React](https://www.filestack.com/fileschool/react/react-file-upload/)
- [How To Implement React MUI File Upload in Your Applications: An Essential Guide](https://www.dhiwise.com/post/how-to-implement-react-mui-file-upload-in-your-applications)
- [The complete guide to WebSockets with React](https://ably.com/blog/websockets-react-tutorial)
- [How to Use MQTT in The React Project](https://www.emqx.com/en/blog/how-to-use-mqtt-in-react)
- [react-chartjs-2](https://react-chartjs-2.js.org/)
- [How to Upload Files in Node.js Using Express and Multer](https://www.youtube.com/watch?v=i8yxx6V9UdM)
- [Open file select dialogue using React JS](https://codepen.io/rkotze/pen/zjRXYr)
- [Opening File Dialog Programmatically](https://react-dropzone.js.org/#!/Opening%20File%20Dialog%20Programmatically)
- [react-dropzone](https://react-dropzone.js.org/)
- [Dockerize React applications with Nginx](https://medium.com/@alinaseri/dockerize-react-applications-with-nginx-17f752deb54)
https://vitejs.dev/guide/static-deploy.html
- [Dockerizing React Application Built with Vite: A Simple Guide](https://thedkpatel.medium.com/dockerizing-react-application-built-with-vite-a-simple-guide-4c41eb09defa)

Install multer:
```
npm install express multer
```

Install axios:
```
npm i axios
```

Install Material UI
```
npm install @mui/material @emotion/react @emotion/styled
npm install @mui/icons-material
```

[Material Icons](https://fonts.google.com/icons?icon.set=Material+Icons)

FROM nginx:alpine
COPY nginx.conf /etc/nginx/conf.d/default.conf

nginx.conf

server {
  listen 80;
  location / {
    root /usr/share/nginx/html;
    index index.html index.htm;
    try_files $uri $uri/ /index.html =404;
  }
}
