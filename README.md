## Setup

First steps:
- create ```app``` and ```server``` folders
- create ```README.md``` file
- create [README.md](app/README.md) file inside ```app``` folder
- create [README.md](server/README.md) file inside ```server``` folder

## Git
- make an "initial commit"
- create a repository at GitHub:
```
git remote add origin https://github.com/hsmptg/DECEL.git
git branch -M main
git push -u origin main
```

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