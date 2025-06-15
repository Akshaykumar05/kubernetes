# kubernetes
![image](https://github.com/user-attachments/assets/b14960cc-ec47-4b73-8cc6-f65bd7e12c7c)


Kubernetes (K8s) is an open-source container orchestration platform that automates many of the manual processes involved in deploying, managing, and scaling containerized applications. It essentially allows you to orchestrate clusters of virtual machines and schedule containers to run on those virtual machines. 
------------------------
* The **kubectl get nodes** command is used in Kubernetes to list all the nodes in your cluster. Each node represents a worker machine (either a VM or a physical machine) where Kubernetes can run pods.
```
kubectl get nodes
```
<img width="551" alt="image" src="https://github.com/user-attachments/assets/ff0779c0-c75f-4503-b027-7ac38e202fbb" />

* ```~/.kube/config``` this file is known as the Kubeconfig file, and it is used by the kubectl command to connect and authenticate to a Kubernetes cluster.

```
cat ~/.kube/config
```
<img width="655" alt="image" src="https://github.com/user-attachments/assets/610dfbce-04df-4819-b736-3671bd618668" />

* Command to shows all the pods in all namespaces in your Kubernetes cluster.
```
kubectl get nodes
```
```
kubectl run nginx --image=nginx
```
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
kubectl create deploy demo --image=nginx --dry-run=client -oyaml
```
<img width="755" alt="image" src="https://github.com/user-attachments/assets/83803cb2-f26e-4723-ad5c-d9ec7da98814" />

* Now let's create three replocas of pod
```
kubectl create deploy demo --image=nginx --replicas=3
```
```
kubectl get rs
```
<img width="562" alt="image" src="https://github.com/user-attachments/assets/4ac2d74a-f2ef-4429-b755-88d61404295a" />

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


 * Go on the ubuntu terminal, we'll create a nginx container there.
```
docker run -d --name my-nginx_container --memory 512m --cpus 1 nginx
```
```
docker ps
```
```
docker logs my-nginx_container
```
<img width="653" alt="image" src="https://github.com/user-attachments/assets/e26e18f6-b327-4668-afff-638c87002e19" />

```
ps aux | grep '[n]ginx' | sort -n -k 2 | head -n 1 | awk '{print $2}'
```
```
ps aux | grep '[n]ginx'
```
```
lsns -p PID
```
<img width="633" alt="image" src="https://github.com/user-attachments/assets/f3afaba3-7e55-4212-aa5e-9f4952e9397a" />
* We can see in above example that we created a container and that container created its processes IDs.
  
* Now let's see the cgroup
```
cd /sys/fs/cgroup/
```
<img width="653" alt="image" src="https://github.com/user-attachments/assets/33a77c2b-ef80-4891-b1b1-8914d3b0650a" />

```
cd system.slice/docker_id
```
```
cat memory.stat
```
<img width="653" alt="image" src="https://github.com/user-attachments/assets/1ae6b5c6-8de4-4ee8-b949-e6de87ee6003" />

#### Now back on the K8s playground
* Well run the workload inside k8s, and that workload is running on node 1
```
kubectl get nodes
```
```
kubectl run nginx --images=nginx
```
```
kubectl get pods -owide
```
```
ssh node 01
```
```
ls
```
* We can see the workload, where it is working

```
crictl ps
```
<img width="655" alt="image" src="https://github.com/user-attachments/assets/f51771a5-c951-4a27-a14a-7e37f3254cec" />

```
ps aux | grep '[n]ginx' | sort -n -k 2 | head -n 1 | awk '{print $2}'
```
```
lsnp -p PID
```
