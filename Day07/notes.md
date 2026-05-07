

---

Pod in kubernetes|Imperative vs Declarative way
to create pod we have two ways ;imperative and declarative way
in imperative we will provide each commands to do creating pod like kubectl run nginx
in declarative way we will define all the things that are needed to create pod/object in yaml file
we will use kubectl create/apply -f pod.yaml file

---
create a nginx pod through kubectl imperative way
kubectl run nginx-pod --image=nginx:latest 
# name of the pod we gave here nginx-pod
 kubectl get pods
NAME        READY   STATUS    RESTARTS   AGE
nginx-pod   1/1     Running   0          91s
#1/1 ready represents that the pod we have created contains one container out of 1 container 1 is running



---
