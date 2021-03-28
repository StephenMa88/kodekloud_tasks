# Problem
The Nautilus DevOps team is working to deploy some tools in Kubernetes cluster. Some of the tools are licence based so that license information needs to be stored securely within Kubernetes cluster. Therefore, the team wants to utilize Kubernetes secrets to store those secrets. Below you can find more details about the requirements:

* We already have a secret key file media.txt under /opt location on jump host. Create a secret named as media and it should contain the password/license-number present in media.txt file.

* Also create a pod named secret-devops.

* Configure pod's spec as container name should be secret-container-devops, image should be fedora preferably with latest tag (remember to mention the tag with image). Use command '/bin/bash', '-c' and 'sleep 10000' for container. Mount a volume named as secret-volume-devops. The mount path should be /opt/apps and mode should be readOnly.

* Mount the secret within this volume.

* To verify you can exec into the container secret-container-devops, to check the secret key under the mounted path /opt/apps.

* Secret type should be generic.

# Solution
```
sudo yum install -y bash-completion
echo "source <(kubectl completion bash)" >> ~/.bashrc
su  - thor
```
## Create secret file
Ref: https://kubectl.docs.kubernetes.io/references/kubectl/create/secret/
```
kubectl create secret generic media --from-file=/opt/media.txt --dry-run=client -o yaml > /opt/media.yaml
```

## Create a pod yaml file
```
kubectl run secret-devops --image=fedora:latest --command '/bin/bash','-c','sleep 10000' --dry-run=client -o yaml > secret-container-devops.yaml
```

## Add these to include secrets under container
Ref: https://kubernetes.io/docs/concepts/configuration/secret/
```
    volumeMounts:
    - name: secret-volume-devops
      mountPath: "/opt/apps"
      readOnly: true
  volumes:
  - name: secret-volume-devops
    secret:
      secretName: media
```

## Pod output after modification
```
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: secret-devops
  name: secret-devops
spec:
  containers:
  - command: ['/bin/bash']
    args: ['-c','sleep 10000']
    image: fedora:latest
    name: secret-container-devops
    volumeMounts:
    - name: secret-volume-devops
      mountPath: "/opt/apps"
      readOnly: true
  volumes:
  - name: secret-volume-devops
    secret:
      secretName: media
```

## To create the secret and pod
```
kubectl apply -f media.yaml; kubectl apply -f secret-container-devops.yaml
```

## To check
```
kubectl get pods; kubectl get secrets
kubectl exec secret-devops -- cat /opt/apps/media.txt
kubectl exec --stdin --tty secret-devops -- /bin/bash
```
