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
command: kubectl get pods --show-labels

2) create 5 nginx pods in witch two of them are labeled env=prod and three are labeled env=dev
yaml file containing it 202_nginx_pods.yml
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
to check that the labels are removed - command: kubectl get pods --show-labels
***notice that the pods are running on yaml deployment with fixed labels, so changing the label will cause the deployment to restart the pods so the return to the desired state.

13) Let’s add the label app=nginx for all the pods and verify 
command: kubectl label pods --all app=nginx
to verify all pods have that label - command: kubectl get pods --show-labels

14) Get all the nodes with labels
command: kubectl get nodes --show-labels

15) Label the worker node nodeName=nginxnode
command: kubectl label nodes {"worker node name"} nodeName=nginxnode         

16) Create a Pod that will be deployed on the worker node with the label nodeName=nginxnode
command: kubectl run {"pod name"} --image=nginx --labels nodeName=nginxnode

17) Verify the pod that is scheduled with the node selector is on the right node
command: kubectl describe pods {"pod name"}
check if the pods is on the desired node
or command: kubectl describe nodes {"nodename"}
check if the node has the desired pod in it

18) Verify the pod nginx that we just created has this label
command: kubectl get pods {"pod name"} --show-labels


Deployments

1) Create a deployment called webapp with image nginx with 5 replicas
a) Use the below command to create a yaml file.
i) kubectl create deploy webapp --image=nginx --dry-run -o yaml >
webapp.yaml
ii) Edit it and add 5 replica’s

2) Get the deployment rollout status

3) Get the replicaset that created with this deployment

4) EXPORT the yaml of the replicaset and pods of this deployment

5) Delete the deployment you just created and watch all the pods are also being
deleted

6) Create a deployment of webapp with image nginx:1.17.1 with container port 80 and
verify the image version
a) kubectl create deploy webapp --image=nginx:1.17.1 --dry-run -o yaml >
webapp.yaml
b) add the port section (80) and create the deployment

7) Update the deployment with the image version 1.17.4 and verify

8) Check the rollout history and make sure everything is ok after the update

9) Undo the deployment to the previous version 1.17.1 and verify Image has the
previous version

10) Update the deployment with the wrong image version 1.100 and verify something is
wrong with the deployment
a) Expect: kubectl get pods (ImagePullErr)
b) Undo the deployment with the previous version and verify everything is Ok
c) kubectl rollout history deploy webapp --revision=7
d) Check the history of the specific revision of that deployment
e) update the deployment with the image version latest and check the history
and verify nothing is going on

11) Apply the autoscaling to this deployment with minimum 10 and maximum 20 replicas
and target CPU of 85% and verify hpa is created and replicas are increased to 10
from 1

12.

13) Clean the cluster by deleting deployment and hpa you just created

14) Create a job and make it run 10 times one after one (run > exit > run >exit ..) using
the following configuration:
kubectl create job hello-job --image=busybox --dry-run -o yaml -- echo "Hello I am
from job" > hello-job.yaml”
a) Add to the above job completions: 10 inside the yaml

