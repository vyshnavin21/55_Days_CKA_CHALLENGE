What is a Namespace in Kubernetes
--
Provides isolation of resources 
-
Avoid accidental deletion/modification
-
Separated by resource type or environment or domain and so on
-
Resources can access each other in the same namespace with their first name by the DNS name for other namespaces
---

<img width="1281" height="553" alt="image" src="https://github.com/user-attachments/assets/bedbf2c0-4ffe-48e1-a005-7daf8fa9da50" />

---
kubectl get ns # provides all namespaces in the system
---
kubectl get all --namespace=kube-system or kubectl get all -n kube-system
which provides what and all components are there in kube system namespace,etcd,apiserver,coredns all control plane components 
you can see under kube-system namespace
---

