# Kubernetes-Notes
## 🧩 What is Kubernetes (K8s)?
### Ans: 
* Kubernetes is an open-source container orchestration tool used to automate deployment, scaling, and management of containerized applications.
* Kubernetes helps you run and manage many containers (like Docker containers) across multiple servers automatically.

## ⚙️ Why Kubernetes?
### Ans: It helps with:
* Automatic deployment & scaling of containers
* Load balancing between containers
* Self-healing — restarts failed containers automatically
* Rolling updates — deploy new versions without downtime
* Service discovery — assigns IPs and DNS names to containers

## 🧱 Kubernetes Architecture (in short)
### Ans: Components
* Master Node (Control Plane)	>>>>>>>>>Manages the cluster (scheduling, monitoring, etc.)
* Worker Nodes	>>>>>>>>>Run your applications (containers/pods)
* Pod	>>>>>>>>>The smallest deployable unit in Kubernetes (contains 1 or more containers)
* Service	>>>>>>>>>>Exposes pods to the network or internally
* Deployment	>>>>>>>>>Ensures your app runs in the desired number of pods
* Namespace	>>>>>>>>>>>Used to organize resources within the cluster

## 🧰 Basic Kubernetes Commands
### 🔹 Cluster Info:-
* kubectl version
* kubectl cluster-info
* kubectl get nodes
* kubectl describe node <node-name>

### 🔹 Working with Pods:-
* kubectl get pods
* kubectl get pods -o wide
* kubectl describe pod <pod-name>
* kubectl logs <pod-name>
* kubectl exec -it <pod-name> -- /bin/bash   # Access pod shell
* kubectl delete pod <pod-name>

### 🔹 Working with Deployments:-
* kubectl get deployments
* kubectl create deployment myapp --image=nginx
* kubectl scale deployment myapp --replicas=3
* kubectl delete deployment myapp

### 🔹 Working with Services:-
* kubectl get services
* kubectl expose deployment myapp --type=NodePort --port=80
* kubectl describe service myapp

### 🔹 Working with Namespaces:-
* kubectl get namespaces
* kubectl create namespace dev
* kubectl delete namespace dev

### 🔹 Configuration & Files:-
* kubectl apply -f <filename>.yaml     # Create or update from YAML
* kubectl delete -f <filename>.yaml
* kubectl get all                      # Show all resources

### 🧾 Example: Deploy Nginx App:-
* kubectl create deployment nginx-deploy --image=nginx
* kubectl expose deployment nginx-deploy --type=NodePort --port=80
* kubectl get all

















