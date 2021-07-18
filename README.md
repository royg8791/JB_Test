# JB_Test
the README file is built in a structure of:
num) explanation
\<execution code\>


1) Deploy a pod based on nginx:alpine image
<!-- 
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl apply -f 01_nginx_pod.yml
pod/nginx-pod-roy created
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get pods
NAME            READY   STATUS    RESTARTS   AGE
nginx-pod-roy   1/1     Running   0          11s 
 -->

2) Deploy a messaging pod based on redis:alpine image
<!-- 
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl apply -f 02_messaging_pod.yml
pod/messaging created 
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get pods
NAME            READY   STATUS    RESTARTS   AGE
messaging       1/1     Running   0          7s    
 -->

3) Create namespace called apx-x998-roy
<!-- 
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl apply -f 03_namespace.yml
namespace/apx-x998-roy created
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get ns
NAME              STATUS   AGE
apx-x998-roy      Active   5s  
 -->

4) json file containing nodes configurations up to this step
<!-- 
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get nodes -o json > 04_tmp_nodes.json
 -->

5) created messaging service that listens on port 6379
<!-- 
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl apply -f 05_messaging_service.yml
service/messaging-service created
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get svc
NAME                TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)    AGE
messaging-service   ClusterIP   100.70.60.189   <none>        6379/TCP   5s    
 -->
6) = 5

7) created a deployment with 2 replicas based on kodekloud/webapp-color image
<!-- 
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl apply -f 07_deploy_2_rep.yml
deployment.apps/hr-web-app created
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get deployments.apps hr-web-app
NAME         READY   UP-TO-DATE   AVAILABLE   AGE
hr-web-app   2/2     2            2           16s 
 -->

8) Create a static pod named static-busybox on the master node that uses the busybox
image and the command sleep 1000





9) created pod with a namespace temp-bus based on redis:alpine image
<!-- 
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl apply -f 09_pod_namespace.yml
namespace/finance-roy created
pod/temp-bus created
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get ns
NAME              STATUS   AGE
finance-roy       Active   15s
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get pods --namespace=finance-roy
NAME       READY   STATUS    RESTARTS   AGE
temp-bus   1/1     Running   0          2m
 -->

10) created persistent volume named pv-analytics
<!-- 
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl apply -f 10_persistant_volume.yml
persistentvolume/pv-analytics created
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get pv
NAME           CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   REASON   AGE
pv-analytics   100Mi      RWX            Retain           Available                                   72s
 -->

11) created pod with a volume of type emptyDir
<!-- 
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl apply -f 11_redis_storage.yml
pod/redis-storage-roy created
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get pods
NAME                          READY   STATUS    RESTARTS   AGE
redis-storage-roy             1/1     Running   0          23s
 -->

12) created pod an dattached it on a persistant volume called pv-1
<!-- 
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl apply -f 12_pod_pv.yml
persistentvolume/pv-1 created
persistentvolumeclaim/pv-1 created
pod/use-pv-roy created
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get pv pv-1
NAME   CAPACITY   ACCESS MODES   RECLAIM POLICY   STATUS      CLAIM   STORAGECLASS   REASON   AGE
pv-1   100Mi      RWO            Retain           Available                                   13s
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get pvc pv-1
NAME   STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS    AGE
pv-1   Bound    pvc-f9245503-487e-4249-913b-52b4f2eac960   1Gi        RWO            kops-ssd-1-17   21s
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get pods use-pv-roy
NAME         READY   STATUS    RESTARTS   AGE
use-pv-roy   1/1     Running   0          43s
 -->

13) Create a new deployment called nginx-deploy, with image nginx:1.16 and 1 replica. Record the version. Next upgrade the deployment to version 1.17 using rolling update. Make sure that the version upgrade is recorded in the resource annotation.
command: \<kubectl apply -f 13_nginx_deploy_record.yml\>
<!-- 
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl apply -f 13_nginx_deploy_record.yml
deployment.apps/nginx-deploy created
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get deployments nginx-deploy
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deploy   1/1     1            1           17s
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl set image deployments nginx-deploy nginx=nginx:1.17 --record
deployment.apps/nginx-deploy image updated
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl describe deployments nginx-deploy
Name:                   nginx-deploy
...
Annotations:            deployment.kubernetes.io/revision: 2
                        kubernetes.io/change-cause: kubectl set image deployments nginx-deploy nginx=nginx:1.17 --record=true
...                        
    Image:        nginx:1.17
 -->

14) Create an nginx pod called nginx-resolver using image nginx, expose it internally with a service called nginx-resolver-service. Test that you are able to look up the 8363 service and pod names from within the cluster. Use the image: busybox:1.28 for dns lookup. Record results in /root/nginx-yourname.svc and /root/nginx-yourname.pod
<!-- 
ubuntu@ip-172-31-15-28:~/JB_Test$ kubectl apply -f 14_deploy_and_service.yml
service/nginx-resolver-service created
pod/nginx-resolver created
ubuntu@ip-172-31-15-28:~/JB_Test$ kubectl get svc nginx-resolver-service
NAME                     TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)   AGE
nginx-resolver-service   ClusterIP   100.66.254.0   <none>        80/TCP    10s
ubuntu@ip-172-31-15-28:~/JB_Test$ kubectl get pods nginx-resolver
NAME             READY   STATUS    RESTARTS   AGE
nginx-resolver   1/1     Running   0          20s
ubuntu@ip-172-31-15-28:~/JB_Test$ kubectl run test-nslookup --image=busybox:1.28 -- nslookup nginx-resolver-service
pod/test-nslookup created
ubuntu@ip-172-31-15-28:~/JB_Test$ kubectl logs test-nslookup
Server:    100.64.0.10
Address 1: 100.64.0.10 kube-dns.kube-system.svc.cluster.local

Name:      nginx-resolver-service
Address 1: 100.66.254.0 nginx-resolver-service.default.svc.cluster.local
 -->


15) Create a static pod on node01 called nginx-critical with image nginx. Create this pod
on node01 and make sure that it is recreated/restarted automatically in case of a
failure.


16) Create a pod called multi-pod with two containers.
Container 1, name: alpha, image: nginx
Container 2: beta, image: busybox, command sleep 4800.
<!-- 
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl apply -f 16_pod_2_containers.yml
pod/multi-pod created
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get pods
NAME                           READY   STATUS    RESTARTS   AGE
multi-pod                      2/2     Running   0          46s
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl describe pods multi-pod
Name:         multi-pod
...
Containers:
  alpha:
...
  beta:
...
    Command:
      sleep
    Args:
      4800
 -->


Pod Design Questions

1) Get pods with label info
<!-- 
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get pods --show-labels
NAME                           READY   STATUS    RESTARTS   AGE     LABELS
messaging                      1/1     Running   0          45m     tier=msg
multi-pod                      2/2     Running   0          3m43s   <none>
use-pv-roy                     1/1     Running   0          15m     run=use-pv-roy
 -->

2) create 5 nginx pods in witch two of them are labeled env=prod and three are labeled env=dev
or run this command: kubectl run {"pod name"} --image=nginx --labels env={"dev(X2)/prod(X3)"}
<!-- 
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl apply -f 202_nginx_pods.yml
deployment.apps/deploy-dev created
deployment.apps/deploy-prod created
ubuntu@ip-172-31-10-80:~/JB_Test$ kubectl get deployments.apps
NAME           READY   UP-TO-DATE   AVAILABLE   AGE
deploy-dev     3/3     3            3           2m49s
deploy-prod    2/2     2            2           2m49s
 -->
or










3) Verify all pods are created with correct labels
command: \<kubectl describe pods {"pod name"}\>
then you go and check that all the labels are correct in the Labels section





4) Get the pods with label env=dev
command: \<kubectl get pods -l env=dev\>





5) Get the pods with label env=dev and also output the label
command: \<kubectl get pods -l env=dev -L env\>

6) Get the pods with label env=prod
command: \<kubectl get pods -l env=prod\>

7) Get the pods with label env=prod and also output the labels
command: \<kubectl get pods -l env=prod -L env\>

8) Get the pods with label env
command: \<kubectl get pods -l env\>

9) Get the pods with labels env=dev and env=prod
command: \<kubectl get pods -L env | egrep 'prod|dev'\>

10) Get the pods with labels env=dev and env=prod and output the labels as well
command: \<kubectl get pods -L env | egrep 'prod|dev'\>

11) Change the label for one of the pod to env=uat and list all the pods to verify
command: \<kubectl label --overwrite pods {"desired pod"} env=uat\>

12) Remove the labels for the pods that we created now and verify all the labels are removed
for single pod - command: \<kubectl label pods {"desired pod"} env-\>
for multiple pods with label env - command: \<kubectl label pods -l env env-\>
to check that the labels are removed - command: \<kubectl get pods --show-labels\>
***notice that the pods are running on yaml deployment with fixed labels, so changing the label will cause the deployment to restart the pods so the return to the desired state.

13) Let’s add the label app=nginx for all the pods and verify 
command: \<kubectl label pods --all app=nginx\>
to verify all pods have that label - command: \<kubectl get pods --show-labels\>

14) Get all the nodes with labels
command: \<kubectl get nodes --show-labels\>

15) Label the worker node nodeName=nginxnode
command: \<kubectl label nodes {"worker node name"} nodeName=nginxnode\>     

16) Create a Pod that will be deployed on the worker node with the label nodeName=nginxnode
command: \<kubectl run {"pod name"} --image=nginx --labels nodeName=nginxnode\>

17) Verify the pod that is scheduled with the node selector is on the right node
command: \<kubectl describe pods {"pod name"}\>
check if the pods is on the desired node
or command: \<kubectl describe nodes {"nodename"}
check if the node has the desired pod in it

18) Verify the pod nginx that we just created has this label
command: \<kubectl get pods {"pod name"} --show-labels\>


Deployments

1) Create a deployment called webapp with image nginx with 5 replicas
command: \<kubectl apply -f 301_deploy_5_rep.yml\>

2) Get the deployment rollout status
command: \<kubectl rollout status deployments {"deployment name"}\>

3) Get the replicaset that created with this deployment
command: \<kubectl get replicasets {"replicaset name"}\>
*** you can get replicaset name from desired deployment by doing command: \<kubectl describe deployment {"deployment name"}\> and looking under "NewReplicaSet" category

4) EXPORT the yaml of the replicaset and pods of this deployment
file containing replicaset export > 304_rs_export.yml
file containing pods export > 304_pods_export.yml

5) Delete the deployment you just created and watch all the pods are also being deleted
command: \<kubectl delete -f 301_deploy_5_rep.yml\>

6) Create a deployment of webapp with image nginx:1.17.1 with container port 80 and verify the image version
command: \<kubectl apply -f 306_deploy_port_80.yml\>
to verify the image - go to github and check if nginx:1.17.1 exists

7) Update the deployment with the image version 1.17.4 and verify
command: \<kubectl set image deployments {"deployment name"} nginx=nginx:1.17.4\>
to verify - command: \<kubectl describe deployments {"deployment name"}\> and verify image category

8) Check the rollout history and make sure everything is ok after the update
command: \<kubectl rollout history deployments {"deployment name"}\>

9) Undo the deployment to the previous version 1.17.1 and verify Image has the previous version
command: \<kubectl rollout undo deployments {"deployment name"}\>
to verify - command: \<kubectl describe deployments {"deployment name"}\> and verify image category

10) Update the deployment with the wrong image version 1.100 and verify something is wrong with the deployment
command: \<kubectl set image deployments {"deployment name"} nginx=nginx:1.100\>
to verify - command: \<kubectl get pods\> you'll see under STATUS "ErrImagePull" and under READY 0/1
command: \<kubectl rollout undo deployments {"deployment name"}\>
to verify - command: \<kubectl get pods {"pods name"}\> you'll see under STATUS "Running" and under READY 1/1
to check specific revision - command: \<kubectl rollout history deployments {"deployment name"} --revision={"revision number"}\>
update image to latest - command: \<kubectl set image deployments {"deployment name"} nginx=nginx:latest\>
history check - command: \<kubectl rollout history deployments {"deployment name"}\> you'll see a new revision
to verify everything is running ok - command: \<kubectl get pods\>

11) Apply the autoscaling to this deployment with minimum 10 and maximum 20 replicas and target CPU of 85% and verify hpa is created and replicas are increased to 10 from 1
command: \<kubectl autoscale deployments {"deployment name"} --max=20 --min=10 --cpu-percent=85\>
to verify hpa is created - command: \<kubectl get horizontalpodautoscalers {"deployment name"}\>
to verify replicas are increased - command: \<kubectl get deployments {"deployment name"}\>

12)

13) Clean the cluster by deleting deployment and hpa you just created
deployment - command: \<kubectl delete deployments {"deployment name"}\>
hpa - command: \<kubectl delete horizontalpodautoscalers {"deployment name"}\>


14) Create a job and make it run 10 times one after one (run > exit > run >exit ..) using the following configuration:
file - 314_hello_job.yml
