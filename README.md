# Yael-JB-TEST
1. Deploy a pod na,ed nginx-pod...
משתמשים בפקודה:
kubectl apply -f 1.nginx_pod.yml 
kubectl get pods

2. Deploy a messaging pod using the redis:alpine...
kubectl apply -f 2.messaging_pod.yml 
kubectl get pods

3. Create a namespace named apx-x998-yael
kubectl apply -f 3.namespace.yml 
kubectl get ns

4. Get the list of nodes in JSON format...
 kubectl get nodes -o json > 4.tmp_nodes.json

5+6. Create a service messaging-service to expose...
 kubectl apply -f 5+6.messaging_service.yml 
  kubectl get svc
 
7. Create a deployment named hr-web-app...
kubectl apply -f 7.deploy_2_rep.yml 
kubectl get deployments.apps hr-web-app

8. Create a static pod named static-busybox...
kubectl run-restart-never-image=busybox static-busybox-dry-run- o yaml-command-sleep 1000 > /etc/kubernetes/manifests/static-busybox.yaml

9. Create a pod in the finance-yael...
kubectl apply -f 9.pod_namespace.yml 
kubectl get ns
kubectl get pods --namespace=finance-yael

10. Create a persistent volume with the given specification
kubectl apply -f 10.persistant_volume.yml 
kubectl get pv

11. Create a pod called  redis-storage-yael...
kubectl apply -f 11.redis_storage.yml 
kubectl get pods

12. Create this pod and attached it a persistent...
kubectl apply -f 12.pod_pv.yml
kubectl get pv pv-1
kubectl get pvc pv-1
kubectl get pods use-pv-yael

13. Create a new deployment called nginx-deploy...
kubectl apply -f 13.nginx_deploy_record.yml
kubectl get deployments nginx-deploy
kubectl set image deployments nginx-deploy nginx=nginx:1.17 --record
kubectl describe deployments nginx-deploy

14. Create an nginx pod called ngnix-resolver using image ngnix...
kubectl apply -f 14.deploy_and_service.yml
kubectl get svc nginx-resolver-service
kubectl get pods nginx-resolver
kubectl run test-nslookup --image=busybox:1.28 -- nslookup nginx-resolver-service
kubectl logs test-nslookup

15. Create a static pod on node01 called nginx-critical with image nginx...
kubectl run --generator=run-pod/v1 nginx-critical --image=nginx --dry-run -o yaml > nginx-critical.yaml
cat nginx-critical.yaml

16. Create a pod called multi-pod wite two containers...
kubectl apply -f 16.pod_2 containers.yml
kubectl get pods
kubectl describe pods multi-pod

Pod Design Questions:
1. Get pods with label information
 kubectl get pods --show-labels
 
 2. Create 5 nginx pods in which two of them is labeled...
 kubectl apply -f 2.2.nginx_pods.yml
 kubectl get deployments.apps
 
 3. verify all the pods are created with correct labels
 kubectl describe pods {"pod name"}
 
 4. Get the pods with label env=dev
 kubectl get pods -l env=dev
 
 5. Get the pods with label env=dev and also output the label
 kubectl get pods -l env=dev -L env
 
 6. Get the pods withe label env=prod 
 kubectl get pods -l env=prod
 
 7. Get the pod with label...
 kubectl get pods -l env=prod -L env
 
 8. Get the pods with label env
 kubectl get pods -l env
 
 9. Get the pods with label...
 kubectl get pods -L env | egrep 'prod|dev
 
 10. Get the pods with labels env=dev...
 kubectl get pods -L env | egrep 'prod|dev
 
 11. Change the label for one of the pod...
 kubectl label --overwrite pods {"desired pod"} env=uat
 
 12. Remove the labels for the pods that we created now...
 kubectl label pods {"desired pod"} env-
 kubectl label pods -l env env-
 kubectl get pods --show-labels
 
 13. lets add the label app-nginx for all the pods...
 kubectl label pods --all app=nginx
 kubectl get pods --show-labels
 
 14. Get all the nodes with labels...
 kubectl get nodes --show-labels
 
 15. label the worker node nodename=ngnixnode
 kubectl label nodes {"worker node name"} nodeName=nginxnode
 
 16. Create a pod that will be deployed...
 kubectl run {"pod name"} --image=nginx --labels nodeName=nginxnode
 
 17. Verify the pod that it is acheduled with the node selector...
 kubectl describe pods {"pod name"}
 kubectl describe nodes {"nodename"}
 
 18. Verify the pod ngnix that we just created has this label
 kubectl get pods {"pod name"} --show-labels
 
 Deployments:
 1. Create a deployment called webapp...
 kubectl apply -f 3.1.deploy_5 rep.yml
 
 2. Get the deployment rollout status
 kubectl rollout status deployments {"deployment name"}
 
 3. Get the replicaset that created with this deployment
 kubectl get replicasets {"replicaset name"
 
 4. EXPORT the yaml of the replicaset...
 file containing pods export > 3.4. pods export.yml
 file containing replicaset export > 3.4. rs_export.yml
 
 5. Delete the deployment you just created...
 kubectl delete -f 3.1. deploy_5 rep.yml
 
 6. Create a deployment of webapp...
 kubectl apply -f 3.6 deploy port 80.yml
 ונאשר ngenix:1.17.1 נבדוק בגיט שקיימים
 
 7. Update the deployment with the image version 1.17.14 and verify
 kubectl set image deployments {"deployment name"} nginx=nginx:1.17.4
 kubectl describe deployments {"deployment name"}  כדי לאשר נריץ
 
 8. Check the rollout history and make sure...
 kubectl rollout history deployments {"deployment name"}
 
 9. Undo the deployment to the previous version 1.17.1...
 kubectl rollout undo deployments {"deployment name"}
 kubectl describe deployments {"deployment name"} כדי לאשר נריץ
 
 10. Update the deployment with the wrong image version 1.100...
 kubectl set image deployments {"deployment name"} nginx=nginx:1.100
 kubectl get pods\> you'll see under STATUS "ErrImagePull כדי לאשר נריץ
 -kubectl rollout undo deployments {"deployment name"
 -kubectl get pods {"pods name"} כדי לאשר נריץ
 Update image:
 kubectl set image deployments {"deployment name"} nginx=nginx:latest
 history check:
 kubectl rollout history deployments {"deployment name"}
 kubectl get pods כדי לבדוק שהכל רץ תקין
 
 11. Apply the autoscaling to this deployment with minimum 10 and maximum 20 replicas...
 kubectl autoscale deployments {"deployment name"} --max=20 --min=10 --cpu-percent=85
 kubectl get horizontalpodautoscalers {"deployment name לאישור 
 kubectl get deployments {"deployment name לאישור 
 
12. 
 
13. Clean the cluster by deleting deployment...
kubectl delete deployments {"deployment name
kubectl delete horizontalpodautoscalers {"deployment name

14. Create a job and make it run 10 times one after one...
3.14 hello job קובץ

Config Map:
1. Create a file called config.txt with two values...
cat >> config.txt << EOF
key1=value1
key2=value2
EOF
cat config.txt

2. create a configmap named keyvalcfgmap and read data from the file config.txt...
kubectl create cm keyvalcfgmap --from-file=config.txt
kubectl get cm keyvalcfgmap -o yaml

3. Create an nginx pod and load environment value from the above configmap keyvalcfgmap...
kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml &gt; nginx-pod.yml
kubectl create -f nginx-pod.yml
Verify:
kubectl exec -it nginx -- env
kubectl delete po nginx

