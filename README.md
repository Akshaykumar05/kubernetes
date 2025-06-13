# kubernetes
![image](https://github.com/user-attachments/assets/b14960cc-ec47-4b73-8cc6-f65bd7e12c7c)


Kubernetes (K8s) is an open-source container orchestration platform that automates many of the manual processes involved in deploying, managing, and scaling containerized applications. It essentially allows you to orchestrate clusters of virtual machines and schedule containers to run on those virtual machines. 
------------------------
* The **kubectl get nodes** command is used in Kubernetes to list all the nodes in your cluster. Each node represents a worker machine (either a VM or a physical machine) where Kubernetes can run pods.
```
kubectl get nodes
```
<img width="551" alt="image" src="https://github.com/user-attachments/assets/ff0779c0-c75f-4503-b027-7ac38e202fbb" />

```
cat ~/.kube/config
```
<img width="655" alt="image" src="https://github.com/user-attachments/assets/610dfbce-04df-4819-b736-3671bd618668" />

* Command to shows all the pods in all namespaces in your Kubernetes cluster.
```
kubectl get pod -A
```
<img width="650" alt="image" src="https://github.com/user-attachments/assets/84d4c644-6b67-47f4-8383-a3ee498b70a6" />

```
kubectl get pods
```
```
kubectl run nginx --image=nginx
```
```
kubectl get pods
```
<img width="570" alt="image" src="https://github.com/user-attachments/assets/709ebbde-345b-4e09-83e5-69009dbb2fa8" />

```
kubectl describe pod
```
<img width="652" alt="image" src="https://github.com/user-attachments/assets/6b05575d-19b4-42fc-92b3-c9810dd07f3f" />
<img width="780" alt="image" src="https://github.com/user-attachments/assets/3ddcb269-e805-47e6-9389-e201c1e1b540" />

* Deployment manifest file
```
kubectl create deploy demo --image=mginx --dry-run=client -oyaml
```
<img width="755" alt="image" src="https://github.com/user-attachments/assets/83803cb2-f26e-4723-ad5c-d9ec7da98814" />

* Now let's create three replocas of pod
```
kubectl create deploy demo --image=nginx --replicas=3
```
```
kubectl get rs
```
* Check total no of pods
```
kubectl get pods
```
* Now let's delete one pod and it will create one more automatically
```
kubectl delete pod pod_id --force
```
```
kubectl get pods
```
<img width="784" alt="k8s 10" src="https://github.com/user-attachments/assets/546e157c-1f04-4c4c-98e5-f8ab46e5d33f" />

* Command to show detailed information about one or more Deployments in the default namespace.
```
kubectl describe deploy
```
<img width="780" alt="image" src="https://github.com/user-attachments/assets/491a7417-b8eb-4159-aa7a-638fe0160459" />
<img width="771" alt="image" src="https://github.com/user-attachments/assets/c8be0923-b1f5-4bda-b1f1-a6576bf5267a" />


 
