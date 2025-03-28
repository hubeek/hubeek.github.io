# Minikube

_Status: Published_
_Created: 2021-06-08 17:46:21_
_Tags: minikube, docker, angular_

#Minikube

run an Angular app in local kubernetes Minikube env with image from Docker.io  


create angular app  
in angular.ts custom output path:
```...
"options": {
  "outputPath": "dist/pw",
  ...```

create nginx file:  

```
events{}
http {
    include /etc/nginx/mime.types;
    server {
        listen 80;
        server_name localhost;
        root /usr/share/nginx/html;
        index index.html;
        location / {
            try_files $uri $uri/ /index.html;
        }
    }
}
```
  
create Dockerfile  
  
##Dockerfile
```
FROM nginx
COPY nginx.conf /etc/nginx/nginx.conf
COPY ./dist/pw /usr/share/nginx/html 
```

##Minikube  
On mac: install via brew minikube and hyperkit.  
brew install hyperkit  
brew install minikube  
brew install kubectl  

```
minikube start --vm-driver=hyperkit
```
in other terminal window  
```
minikube dashboard
```

back to the first window:  
(after a *ng build --prod*)
```
docker build -t DOCKER_ACCOUNTNAME/pw-app:latest .

docker push docker.io/DOCKER_ACCOUNTNAME/pw-app:latest

kubectl create deployment pw-app --image=docker.io/DOCKER_ACCOUNTNAME/pw-app:latest

kubectl expose deployment pw-app --type=NodePort --port=80
minikube service pw-app
```