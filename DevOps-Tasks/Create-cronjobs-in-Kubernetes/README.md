#Problem
There are some jobs/tasks that need to be run regularly on different schedules. Currently the Nautilus DevOps team is working on developing some scripts that will be executed on different schedules, but for the time being the team is creating some cron jobs in Kubernetes cluster with some dummy commands (which will be replaced by original scripts later). Create a cronjob as per details given below:
	1. Create a cronjob named datacenter.
	2. Set schedule to */8 * * * *.
	3. Container name should be cron-datacenter.
	4. Use httpd image with latest tag only and remember to mention tag i.e httpd:latest.
	5. Run a dummy command echo Welcome to xfusioncorp.
	6. Ensure restart policy is OnFailure.


#Solution
vi task.yaml

apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: datacenter
spec:
  schedule: "*/8 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: cron-datacenter
            image: httpd:latest
            args:
            - /bin/sh
            - -c
            - date; echo Welcome to xfusioncorp
          restartPolicy: OnFailure

kubectl create -f task.yaml

#To Check
kubectl get task datacenter

kubectl get jobs --watch
NAME                    COMPLETIONS   DURATION   AGE
datacenter-1612408560   1/1           7s         65s

pods=$(kubectl get pods --selector=job-name=datacenter-1612408560 --output=jsonpath={.items[*].metadata.name})
kubectl logs $pods

Ref: https://kubernetes.io/docs/tasks/job/automated-tasks-with-cron-jobs/
