# Problem
There is an application that needs to be deployed on Kubernetes cluster under Apache web server. The Nautilus application development team has asked the DevOps team to deploy it. We need to develop a template as per requirements mentioned below:

	1. Create a namespace named as httpd-namespace-datacenter.
	2. Create a service named as httpd-service-datacenter under same namespace, targetPort should be 80 and nodePort should be 30004.
	3. Create a deployment named as httpd-deployment-datacenter under the same namespace as mentioned above. Use image httpd with latest tag only and remember to mention tag i.e httpd:latest, and container name should be httpd-container-datacenter. And make sure replicas counts are 4.
	4. Set labels app to httpd_app_datacenter.

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

# Solution

sudo yum install -y bash-completion

echo "source <(kubectl completion bash)" >> ~/.bashrc
su  - thor



## Task 1

kubectl create namespace httpd-namespace-datacenter

## Task 2

kubectl create service nodeport httpd-service-datacenter --namespace=httpd-namespace-datacenter --node-port=30004 --tcp=80 --dry-run=client -o yaml > httpd-service-datacenter.yaml


## Task 3

kubectl create deployment --image=httpd:latest httpd-deployment-datacenter --namespace=httpd-namespace-datacenter --replicas=4 --dry-run=client -o yaml > httpd-deployment-datacenter.yaml

kubectl create deployment --image=httpd:latest httpd-deployment-nautilus --namespace=httpd-namespace-nautilus --replicas=4 --dry-run=client -o yaml >httpd-deployment-nautilus.yaml

## Task 4

vi into the yaml files we created to do the following:
    For the service file:
    - change apps label in two places to httpd_app_datacenter
    For the deployment file: 
    - change app label in three places to httpd_app_datacenter
    - change container name to httpd-container-datacenter

## To Check
kubectl get pods -A --selector=app=httpd_app_datacenter
kubectl get service -A --selector=app=httpd_app_datacenter
