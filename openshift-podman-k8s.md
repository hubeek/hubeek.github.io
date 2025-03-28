# Openshift Podman K8s

_Status: Published_
_Created: 2021-07-02 08:57:18_

containerized applications shares host os, hardware, trad os, isolates resources, network, libs namespace
advantage not vulnerable or need to be stopped for updates base system, lower hardware footprint, env iso, quick deploy, multiple env deploy, reusability
OCI open container initiative (specs)
Rocket Drawbridge Docker Podman

containers: namespaces, controlgroups cgroups, Seccomp, SELinux

k8s
is helmsman/orchestrator => simplyfy deployment, managment, scaling containers
service discovery and load balancing
horizontal scaling
self healing
automated rollout
secrets and config management
operators

openshift is set of modular components and services on top of kubernetes

openshift
integrates dev workflow (ci/cd pipelines, s2i)
routes
metrics & logging
unified ui

https://registry.redhat.io 
https://quay.io

registries
redhat container images
trusted source
original deps
vulnerability-free
runtime protection
red hat enterprise linux
red hat support

configuring in podman
</code>
/etc/containers/registries.conf
[registries.search]
registries = ["registry.access.redhat.com", "quay.io"]
</code>
to support insecure connections:
<code>
[registries.insecure]
registries = ['localhost:5000']
</code>




PODMAN
<code>
sudo podman search rhel
sudo podman pull [OPTIONS] [REGISTRY[:PORT]/]NAME[:TAG] 
sudo podman push [OPTIONS] IMAGE [DESTINATION]
sudo podman commit [OPTIONS] CONTAINER \ > [REPOSITORY[:PORT]/]IMAGE_NAME[:TAG] 
sudo podman diff mysql-basic 
sudo podman save [-o FILE_NAME] IMAGE_NAME[:TAG] 
sudo podman tag [OPTIONS] IMAGE[:TAG] \ > [REGISTRYHOST/][USERNAME/]NAME[:TAG] 
sudo podman images
sudo podman ps
sudo podman ps -a
sudo podman run REPO/IMG CMD
sudo podman run ubi7/ubi7:7 echo ‘hello’
sudo podman run -it ubi7/ubi:7.7 /bin/bash 
sudo podman run -e GREET=Hello -e NAME=RedHat \ > rhel7:7.5 printenv GREET NAME # env vars!
sudo podman run --name mysql-custom -e MYSQL_USER=redhat -e MYSQL_PASSWORD=r3dh4t -d rhmap47/mysql:5.5 
sudo podman exec -it mysql-basic /bin/bash  # run bash in running container
sudo podman inspect -l -f "{{.NetworkSettings.IPAddress}}" 
sudo podman inspect \ > -f "{{range .Mounts}}{{println .Destination}}{{end}}" CONTAINER_NAME/ID 
sudo podman ps --format "{{.ID}} {{.Image}} {{.Names}}"
sudo podman ps --format="{{.ID}} {{.Names}} {{.Status}}" 
sudo podman ps -a
sudo podman stop containername/ID
sudo podman kill container
sudo podman kill -s SIGKKILL container
sudo podman restart container
sudo podman rm container
sudo podman rm -f container
sudo podman rmi [OPTIONS] IMAGE [IMAGE...] 
sudo podman rmi -a
sudo podman rmi container

login with quay or docker:
sudo podman login -u username \ > -p password registry.access.redhat.com 

</code>
persistant storage:
<code>
sudo mkdir /var/dbfiles
sudo chown -R 27:27 /var/dbfiles
sudo semanage fcontext -a -t container_file_t '/var/dbfiles(/.*)?' 
sudo restorecon -Rv /var/dbfiles
sudo podman run -v /var/dbfiles:/var/lib/mysql rhmap47/mysql 
</code>
===
<code>
sudo podman run --name mysqldb-port -d -v /var/local/mysql:/var/lib/mysql/data -p 13306:3306 -e MYSQL_USER=user1 -e MYSQL_PASSWORD=mypa55 -e MYSQL_DATABASE=items -e MYSQL_ROOT_PASSWORD=r00tpa55  rhscl/mysql-57-rhel7 sudo podman ps --format="{{.ID}} {{.Names}} {{.Ports}}" 
mysql -uuser1 -h 127.0.0.1 -pmypa55 -P13306 items < /home/student/DO180/labs/manage-networking/db.sql 
sudo podman exec -it mysqldb-port  /opt/rh/rh-mysql57/root/usr/bin/mysql -uroot items -e "SELECT * FROM Item" 
</code>
===
<code>
sudo mkdir -pv /var/local/mysql 
sudo semanage fcontext -a \ > -t container_file_t '/var/local/mysql(/.*)?' 
sudo restorecon -R /var/local/mysql sudo chown -Rv 27:27 /var/local/mysql 
sudo podman run --name mysql-1 \ > -d -v /var/local/mysql:/var/lib/mysql/data \ > -e MYSQL_USER=user1 -e MYSQL_PASSWORD=mypa55 \ > -e MYSQL_DATABASE=items -e MYSQL_ROOT_PASSWORD=r00tpa55 \ > rhscl/mysql-57-rhel7 
sudo podman ps --format="{{.ID}} {{.Names}}" 
sudo podman inspect \ > -f '{{ .NetworkSettings.IPAddress }}' mysql-1 
mysql -uuser1 -h CONTAINER_IP \ > -pmypa55 items < /home/student/DO180/labs/manage-review/db.sql 
mysql -uuser1 -h CONTAINER_IP -pmypa55 items \ > -e "SELECT * FROM Item" sudo podman stop mysql-1 



</code>