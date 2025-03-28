# Raspberry pi Docker Portainer

_Status: Published_
_Created: 2022-03-05 04:20:35_

apt update -y && apt upgrade -y  
apt install git

create downloads folder
get:
https://github.com/novaspirit/pi-hosted

## install docker
installdocker.sh
```
#!/bin/bash

function error {
  echo -e "\\e[91m$1\\e[39m"
  exit 1
}

function check_internet() {
  printf "Checking if you are online..."
  wget -q --spider http://github.com
  if [ $? -eq 0 ]; then
    echo "Online. Continuing."
  else
    error "Offline. Go connect to the internet then run the script again."
  fi
}

check_internet

curl -sSL https://get.docker.com | sh || error "Failed to install Docker."
sudo usermod -aG docker $USER || error "Failed to add user to the Docker usergroup."
echo "Remember to logoff/reboot for the changes to take effect."
```
check if docker in groups. 
```
groups
```
apt install docker 

## install portainer

```
#!/bin/bash

function error {
  echo -e "\\e[91m$1\\e[39m"
  exit 1
}

function check_internet() {
  printf "Checking if you are online..."
  wget -q --spider http://github.com
  if [ $? -eq 0 ]; then
    echo "Online. Continuing."
  else
    error "Offline. Go connect to the internet then run the script again."
  fi
}

check_internet

sudo docker pull portainer/portainer-ce:latest || error "Failed to pull latest Portainer docker image!"
sudo docker run -d -p 9000:9000 -p 9443:9443 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce:latest || error "Failed to run Portainer docker image!"

```
check in browser if portainer is working. 

list templates for portainer:
```
templates
https://raw.githubusercontent.com/SelfhostedPro/selfhosted_templates/master/Template/portainer-v2.json

default:
https://raw.githubusercontent.com/portainer/templates/master/templates-2.0.json

nog 1:
https://raw.githubusercontent.com/dnburgess/self-hosted-template/master/template.json

redditpost:
https://raw.githubusercontent.com/dnburgess/self-hosted-template/master/template.json

https://raw.githubusercontent.com/Qballjos/portainer_templates/master/Template/template.json

https://raw.githubusercontent.com/SelfhostedPro/selfhosted_templates/portainer-2.0/Template/template.json

https://raw.githubusercontent.com/technorabilia/portainer-templates/main/lsio/templates/templates-2.0.json

https://raw.githubusercontent.com/mikestraney/portainer-templates/master/templates.json

https://raw.githubusercontent.com/mycroftwilde/portainer_templates/master/Template/template.json

```