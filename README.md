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

2) create 5 nginx pods in witch two of them are labeled env=prod and three are labeled env=dev
yaml file containing it 2.02_nginx_pods.yml
or run this command: kubectl run {"pod name"} --image=nginx --labels env={"env(X2)/prod(X3)"}

3) Verify all pods are created with correct labels
command: kubectl describe pods {"pod name"}
then you go and check that all the labels are correct in the Labels section

4) Get the pods with label env=dev
command: kubectl get pods -l env=dev

5) Get the pods with label env=dev and also output the label
command: kubectl get pods -l env=dev -L env

6) Get the pods with label env=prod
command: kubectl get pods -l env=prod

7) Get the pods with label env=prod and also output the labels
command: kubectl get pods -l env=prod -L env

8) Get the pods with label env
command: kubectl get pods -l env

9) Get the pods with labels env=dev and env=prod
command: kubectl get pods -L env | egrep 'prod|dev'

10) Get the pods with labels env=dev and env=prod and output the labels as well
command: kubectl get pods -L env | egrep 'prod|dev'

11) Change the label for one of the pod to env=uat and list all the pods to verify
command: kubectl label --overwrite pods {"desired pod"} env=uat

12) Remove the labels for the pods that we created now and verify all the labels are removed
for single pod - command: kubectl label pods {"desired pod"} env-
for multiple pods with label env - command: kubectl label pods -l env env-
to check that the labels are removed - command: kubectl get pods -l env
***notice that the pods are running on yaml deployment with fixed labels, so changing the label will cause the deployment to restart the pods so the return to the desired state.

13) Let’s add the label app=nginx for all the pods and verify (using kubectl)
command: kubectl label pods --all app=nginx

14) Get all the nodes with labels (if using minikube you would get only master node)

15) Label the worker node nodeName=nginxnode

16) Create a Pod that will be deployed on the worker node with the label nodeName=nginxnode








