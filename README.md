Getting started with Docker and Openshift
==========================================

###### Build docker image
docker build . -t caddy

###### Create a new openshift project
oc new-project andrea

###### Tag and push your new docker image
docker tag caddy registry_hostname/andrea/caddy
docker push registry_hostname/andrea/caddy

###### Check the reference for the pushed image
oc get is

###### Run the new image
oc run caddy-andrea --image=registry_hostname/andrea/caddy

###### Check that a new Deployment Configuration is created
oc get dc

###### And the pod will get ready in a few seconds
oc get po

###### Rsh into the pod to check if the service is working as expected
oc rsh pod_name

> wget -qO- 127.0.0.1:3000

###### Create a service and a route to reach the service from outside
oc expose dc/caddy-andrea --port=3000 --name=caddy-andrea-service

oc create route edge caddy-andrea-route --service=caddy-andrea-service --insecure-policy='Redirect'

###### Apply the deployments from file

oc create -f filename.yaml
oc apply -f filename.yaml