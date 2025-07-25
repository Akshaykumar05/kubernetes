# kubernetes
![image](https://github.com/user-attachments/assets/b14960cc-ec47-4b73-8cc6-f65bd7e12c7c)

In this repo I'm documenting the K8s learning from **Kubesimplify K8s Bootcamp** by **Saiyam Pathak** on his Youtube channel.

Kubernetes (K8s) is an open-source container orchestration platform that automates many of the manual processes involved in deploying, managing, and scaling containerized applications. It essentially allows you to orchestrate clusters of virtual machines and schedule containers to run on those virtual machines. 

------------------------
## K8s Architecture
![image](https://miro.medium.com/v2/resize:fit:1400/format:webp/1*NbfqFvRvZnofYn2-T4SAuw.png)

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
<img width="551" alt="image" src="https://github.com/user-attachments/assets/5ef4bba1-b477-4cc9-a056-e9527dd6fe72" />

* Now here we can see all the namespace of this PID.

---------------------------------------
```
kubectl config view
```
 This command shows the configuration stored in your kubeconfig file (typically located at ~/.kube/config) and tells kubectl how to connect to your Kubernetes cluster.

* Now create CSR (Certificate Signing Requests) : We are generating a key using openssl
  ```
  openssl genrsa -out akshay.key 2048
  ```
  ```
  openssl req -new -key akshay.key -out akshay.csr -subj "/CN=akshay/O=group1"
  ```
#### Sign CSE with k8s CA
  ```
  cat akshay.csr | base64 | tr -d '\n'
  ```
* Create csr
  ```
  vim csr.yaml
  ```

* Add following description
```
apiVersion: certificates.k8s.io/v1
kind: CertificateSigningRequest
metadata:
   name: akshay
spec:
   request: BASE64_CSR      #use your generated key in place of BASE64_CSR
   signerName: kubernetes.io/kube-apiserver-client
   usages:
   - client auth
 ```

   ```
   kubectl apply -f csr.yml
   ```
   ```
   kubectl certificate approve akshay
   ```

   <img width="542" alt="image" src="https://github.com/user-attachments/assets/22f3cfbd-5f35-4458-bae0-09178d0ce009" />

  * Now take the certificate from jsonpath using below command
   ```
   kubectl get csr akshay -o jsonpath='{.status.certificate}' | base64 --decode > akshay.crt
   ```
  * check using **ls** you will get the **.crt** file

  <img width="644" alt="image" src="https://github.com/user-attachments/assets/bc470c1c-2ae9-4e44-bd1f-9e614a246348" />

### Now we will reate role binding
  ```
  vim role.yaml
  ```
```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: read-pods
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "watch", "list"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods-binding
  namespace: default
subjects:
- kind: User
  name: akshay
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: read-pods
  apiGroup: rbac.authorization.k8s.io
```
* In the above file we created a user named **akshay** and gave the role **pod-reader** who can do the **get, watch & list** the pod.
* Apply the changes

```
kubectl apply -f role.yaml
```
<img width="620" alt="image" src="https://github.com/user-attachments/assets/440d3969-11c8-48a9-91a1-a97cadc78cb1" />

### Setup kubeconfig file
 ```
 kubectl config set-credentials akshay --client-certificate=akshay.crt --client-key=saiyam.key
 ```
 ```
 kubectl config get-contexts
 ```
 ```
 kubectl config set-context akshay-context --cluster=kubernetes --namespace=default --user=akshay
 ```
 ```
 kubectl config use-context akshay-context
 ```
 <img width="653" alt="image" src="https://github.com/user-attachments/assets/a98cc8d3-4ae1-41f5-8a35-f72d4c9e5b44" />

 ```
 cat ~/.kube/config
 ```

 ```
 kubectl config get-contexts
 ```

 ```
 kubectl config use-context kubernetes-admin@kubernetes
 ```

 ```
 kubectl get pods
 ```

 ```
 cat ~/.kube/c
 ```

 ```
 ls ~/.kube/config
 ```
 ```
 kubectl get nodes --kubeconfig ~/.kube/config
 ```

 
 ### Merging multiple Kubeconfig files
 ```
 export KUBECONFIG=/path/to/first/config:/path/to/second/config:/path /to/third/config
 ```
### local HTTP proxy
```kubectl proxy``` is a command used in Kubernetes to create a local HTTP proxy that allows you to access the Kubernetes API server securely without needing to manually handle authentication or certificates.

```
kubectl proxy
```
It starts a proxy server on your local machine (default: ```http://localhost:8001```) and forwards HTTP requests to the Kubernetes API server, using your current kubeconfig credentials.

```
curl localhost:8001/apis
```

