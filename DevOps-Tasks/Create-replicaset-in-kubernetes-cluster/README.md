# Problem
The Nautilus DevOps team is going to deploy some applications on kubernetes cluster as they are planning to migrate some of their applications there. Recently one of the team members has been assigned a task to write a template as per details mentioned below:
	• Create a ReplicaSet using httpd image with latest tag only and remember to mention tag i.e httpd:latest and name it as httpd-replicaset.

	• Labels app should be httpd_app, labels type should be front-end. The container should be named as httpd-container; also make sure replicas counts are 4.

	• Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

# Solution
vi replicaset-definition.yml

apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: httpd-replicaset
  labels:
    app: httpd_app
    type: front-end
spec:
  template:
    metadata:
      name: httpd-replicaset
      labels:
        app: httpd_app
        type: front-end
    spec:
      containers:
      - name: httpd-container
        image: httpd:latest


  replicas: 4
  selector:
    matchLabels:
      type: front-end


Selector is what makes replicaset different from replicationController
We give it a label so that replicaset knows what to monitor

kubectl create -f replicaset-definition.yml

# To Check
kubectl get replicaset
kubectl describe replicaset-definition.yml

