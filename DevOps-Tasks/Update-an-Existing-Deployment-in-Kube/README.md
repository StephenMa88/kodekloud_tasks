# Problem

There is an application deployed on Kubernetes cluster. Recently the Nautilus application development team developed a new version of the application that needs to be deployed now. As per new updates some new changes need to be made in this existing setup. So update the deployment and service as per details mentioned below:

We already have a deployment named nginx-deployment and service named nginx-service. Some changes need to be made in this deployment and service, make sure not to delete the deployment and service.

1.) Change the service nodeport from 30008 to 32165

2.) Change replicas count from 1 to 5

3.) Add a command: ["sh","-c","while true; do apt update; apt install -y vim php ; sleep 3; done"]

4.) Change the image from nginx:1.17 to nginx:latest

Note: The kubectl utility on jump_host has been configured to work with the kubernetes cluster.

# Solution
```
sudo yum install -y bash-completion
echo "source <(kubectl completion bash)" >> ~/.bashrc
su  - thor
```

## Task 1
Use command to open up service edit
```
kubectl edit services nginx-service
```
Change the annotation and nodePort to 32165
Type :wq to save and close file

## Task 2
Use command to open up deployment edit
```
kubectl edit deployments.apps nginx-deployment
```
Change the annotation, replicas under spec > replicas under status to 5
Type :wq to save and close file

## Task 3
Use command to open up deployment edit
```
kubectl edit deployments.apps nginx-deployment
```
Under Spec > template > spec > containers > 
Add the last two lines as seen in the picture below.

Type :wq to save and close file


## Task 4
Use command to open up deployment edit
```
kubectl edit deployments.apps nginx-deployment
```
Replace 1.17 with latest
Under spec > template > spec > containers > image
and in the annotations
Type :wq to save and close file

## To Check
Two methods.
	1) When you run the command, you were able to save and exit and not get called back into the file to fix it :)
Or here are commands you can use to confirm.
```
kubectl describe service nginx-service |grep -i nodePort
```

```
kubectl describe deployments.apps |grep -i replicas:
```

```
kubectl describe deployments.apps |grep -i command -A 5
```

```
kubectl describe deployments.apps |grep -i image
```


