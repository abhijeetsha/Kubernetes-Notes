# Kubernetes In One-Shots Explanations:-
## 🔹 Core Concepts:-

## 🧱 1. Monolithic vs Microservices
### 🧩 Monolithic Architecture
* The entire application is built as one single unit.
* All components (UI, business logic, database access) are tightly coupled.
* 👉 Example:-
* A shopping app where product listing, cart, and payment are all in one big codebase.
### Pros:
* Simple to develop, test, and deploy initially.
* Easier for small applications.
### Cons:
* Hard to scale (you must scale the entire app even if one part needs more resources).
* Difficult to update — one small change can require redeploying the entire app.
* Slower development when the app grows.

### ⚙️ Microservices Architecture
* Application is divided into small independent services, each focusing on a specific function (e.g., User Service, Payment Service, Order Service).
* Each service runs in its own container or pod, often managed by Kubernetes.
### Pros:
* Independent deployment and scaling.
* Easier fault isolation — one service failing doesn’t crash the whole app.
* Better suited for cloud-native and DevOps environments.
### Cons:
* More complex networking and monitoring.
* Requires orchestration (like Kubernetes) to manage services.

## ☸️ 2. Kubernetes Architecture
🧠 Control Plane (Master Node)
* Responsible for managing and controlling the cluster.
### Components:
* API Server – The main entry point; all commands go through it (kubectl communicates here).
* etcd – Key-value store that holds cluster state and configuration.
* Controller Manager – Ensures the desired state matches the actual state.
* Scheduler – Assigns pods to available nodes.
* Cloud Controller Manager – Integrates with cloud providers (AWS, Azure, etc.).

## 🖥️ Worker Node (Minion Node)
*Runs your actual workloads (pods).
### Components:
* Kubelet – Communicates with the master; ensures pods are running.
* Kube-proxy – Handles network routing and service discovery.
* Container Runtime – Runs containers (Docker, containerd, etc.).

## 💻 3. Kubernetes Setup
### 🧩 A. Local Setup (using Minikube or Kind)
🔹 Minikube
####  Install Minikube and kubectl
* minikube start --driver=docker

#### Check cluster status
* kubectl get nodes





