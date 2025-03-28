# Kubernetes

_Status: Published_
_Created: 2021-07-06 12:33:44_
_Tags: kubernetes, k8s, digital ocean, Ingress, docker_

# Kubernetes on Digital Ocean with Ingress

- Create Kubernetes with Create-Button
- Install One-click app Ingress
- Make sure DNS is routed to the ip address of the kubernetes-stack
- Add pods, create from form and choose INTERNAL service.
- When removing pod double check you have removed all the services and routes etc etc.

## Add Ingres yaml
```
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: web
  namespace: default
spec:
  rules:
  - host: nginx01-test.webaddress.com
    http:
      paths:
      - backend:
          serviceName: nginx01
          servicePort: 80
  - host: nginx02-test.yourwebaddress.com
    http:
      paths:
      - backend:
          serviceName: nginx02
          servicePort: 80
```
