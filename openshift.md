# Openshift

_Status: Published_
_Created: 2021-03-12 09:51:40_

## Developer perspective

### GUI
add shortcuts in menu for:  
deployments 
services  
routes  
image streams  
pods  
replica sets  


terminal
```oc project demoapp```

```oc config get-contexts```

alles
```oc api-resources```
```oc get pods```
```oc get pods,deploy,svc```
```oc get pods,rs,deploy```

```oc get all```

(refresh at every 2 sec)
```watch oc get pods,deploy,svc```

```oc scale deploy demoapp-name --replicas=7```

```oc delete pod devops-demo-app-git-c8c68f8-8pfcs```