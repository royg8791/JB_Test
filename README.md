# JB_Test
the README file is built in a structure of:
num) explanation
\<execution code\>


1) Deploy a pod based on nginx:alpine image
kubectl apply -f 01_nginx_pod.yml

2) Deploy a messaging pod based on redis:alpine image
kubectl apply -f 02_messaging_pod.yml

3) Create namespace called apx-x998-roy
kubectl apply -f 03_namespace.yml

4) json file containing nodes configurations up to this step
kubectl get nodes -o json > 04_tmp_nodes.json

5) = 6) created messaging service that listens on port 6379
kubectl apply -f 05_messaging_service.yml

7) created a deployment with 2 replicas based on kodekloud/webapp-color image
kubectl apply -f 07_deploy_rep.yml

8) 

9) created pod with a namespace temp-bus based on redis:alpine image
kubectl apply -f 09_pod_namespace.yml

10) created persistent volume named pv-analytics
kubectl apply -f 10_persistant_volume.yml

11) created pod with a volume of type emptyDir
kubectl apply -f 11_redis_storage.yml

12) created pod an dattached it on a persistant volume called pv-1
kubectl apply -f 12_pod_pv.yml

13) 

14) 

15) 

16) 

Pod Design Questions

1) Get pods with label info
kubectl describe pods

2) 





