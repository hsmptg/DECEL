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