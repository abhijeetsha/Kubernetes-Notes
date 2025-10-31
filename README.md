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
