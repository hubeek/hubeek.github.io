# Grafana

_Status: Published_
_Created: 2021-07-17 03:43:05_

with local data
```
  docker run -d -p 3000:3000 --name grafana --volume "$PWD/data:/var/lib/grafana" grafana/grafana  
  docker container ls -a  
  docker container stop <tagname>  
  docker container rm <tagname> 
```
##hub.docker.com
```
docker run -d -p 3000:3000 --name grafana --user 472 --volume "$PWD/data:/var/lib/grafana" -e "GF_INSTALL_PLUGINS=grafana-clock-panel,grafana-simple-json-datasource" grafana/grafana

docker stop grafana
docker commit grafana
docker tag grafana yoyohu/grafana-tuinhok
docker push yoyohu/grafana-tuinhok:latest
```
## Query time correction
```
SELECT
  UNIX_TIMESTAMP(created) AS "time",
  temperature
FROM temperatures
WHERE
  $__timeFilter(created)
ORDER BY created
```