# Problem

The Nautilus DevOps team is testing applications containerization, which is supposed to be migrated on docker container-based environments soon. In today's stand-up meeting one of the team members has been assigned a task to create and test a docker container with certain requirements. Below are more details:

a. On App Server 2 in Stratos DC pull ubuntu image (preferably latest tag but others should work too).

b. Create a new container with name cluster from the image you just pulled.

c. Map the host volume /opt/data with container volume /tmp. There is an sample.txt file present on same server under /tmp; copy that file to /opt/data. Also please keep the container in running state.

# Solution
ssh steve@stapp02

## Task A
```
sudo docker pull ubuntu:latest
```
## Task B and C
```
cat /tmp/sample.txt
sudo cp /tmp/sample.txt /opt/data
sudo docker create -v /opt/data:/tmp --name cluster ubuntu sleep infinity
sudo docker ps -a
sudo docker start <container ID from above command>
```

## To Check
```
sudo docker exec -it cluster bash
ls /tmp
cat /tmp/sample.txt
```
Or 
```
sudo docker exec -ti cluster cat /tmp/sample.txt
```
