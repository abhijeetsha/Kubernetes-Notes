# 🌐 Kubernetes Networking:-

## 🌐 1. Networking in Kubernetes – Overview
### Kubernetes networking ensures that:
* Pods can communicate with each other (across nodes).
* Pods can communicate with Services.
* External users can access applications inside the cluster.
* Network traffic can be controlled and secured.

## Kubernetes defines four main networking areas:
| Networking Type            | Description                                           |
| -------------------------- | ----------------------------------------------------- |
| **Container-to-Container** | Within the same Pod (localhost).                      |
| **Pod-to-Pod**             | Communication between Pods (on same/different nodes). |
| **Pod-to-Service**         | Accessing a Service (stable IP for Pods).             |
| **External-to-Service**    | Accessing apps from outside the cluster.              |

## 🧩 2. Cluster Networking
###🧠 What it means:
* Every Pod in Kubernetes gets its own IP address and can communicate with other Pods without NAT (Network Address Translation).
* This is enabled by a CNI (Container Network Interface) plugin.
### 🔹 Common CNI Plugins:
  * Flannel
  * Calico
  * Weave
  * Cilium

3## ⚙️ Example:-
* Pod-A (10.244.1.5)  --->  Pod-B (10.244.2.10)
* 🔹 Both can talk directly using IPs, even if they are on different nodes.
* Key Rule: All Pods in a cluster can reach each other directly via IP.

### 🕸️ 3. Kubernetes Services
* Pods are temporary — they can die or restart, changing their IPs.
* So Kubernetes uses Services to provide a stable network endpoint.

### 🧱 Types of Services
| Service Type            | Description                                    | Use Case                       |
| ----------------------- | ---------------------------------------------- | ------------------------------ |
| **ClusterIP (default)** | Internal access within the cluster             | Microservices inside cluster   |
| **NodePort**            | Exposes app on a port on each node             | Testing or internal dev access |
| **LoadBalancer**        | Exposes app externally via cloud load balancer | Production access              |
| **ExternalName**        | Maps Service to an external DNS name           | External APIs or DBs           |

### 🚪 4. Ingress
### 🧠 What is Ingress?
 * Ingress manages HTTP and HTTPS access to services from outside the cluster using rules (like a smart router or reverse proxy).
 * It reduces the need for multiple LoadBalancers.

### ⚙️ Ingress Controller
 * Ingress rules only work when an Ingress Controller is installed (like NGINX Ingress Controller, Traefik, HAProxy).

### 🧭 Ingress Flow Example
* User → Ingress Controller → Service → Pods
* Instead of giving every Service its own LoadBalancer,
* Ingress combines them under one external IP and routes based on host/path rules.

## 🔒 5. Network Policies
### 🧠 What are Network Policies?
* By default, all Pods can talk to all other Pods — open communication.
* Network Policies restrict traffic between Pods (like a firewall).
* They define which Pods can communicate with which other Pods.

## ⚙️ Requirements:
### Your cluster must use a CNI plugin that supports Network Policies (like Calico, Cilium, or Weave).

## 🧭 6. Kubernetes Networking Diagram
                +---------------------+
                |   External Clients  |
                +----------+----------+
                           |
                      [ Ingress Controller ]
                           |
            +--------------+--------------+
            |                             |
       [Service: web-app]           [Service: api]
            |                             |
       +----+----+                  +-----+-----+
       |  Pod A  | <----> Network <-> |   Pod B   |
       +---------+                  +-------------+

## 🧩 7. Summary Table
| Concept                    | Purpose                           | Key Use Case                |
| -------------------------- | --------------------------------- | --------------------------- |
| **Cluster Networking**     | Allows Pods to talk to each other | Pod-to-Pod communication    |
| **Service (ClusterIP)**    | Internal stable access            | Microservices communication |
| **Service (NodePort)**     | Exposes app on each node port     | Testing                     |
| **Service (LoadBalancer)** | Exposes app externally            | Production traffic          |
| **Ingress**                | Routes HTTP/S traffic to services | Web traffic routing         |
| **Network Policy**         | Controls Pod traffic (firewall)   | Security and isolation      |

## ✅ Quick Recap
* Pods → Have unique IPs, talk directly.
* Services → Provide stable endpoints.
* Ingress → Routes external HTTP traffic.
* Network Policies → Secure and control communications.
* CNI → Manages Pod networking (Flannel, Calico, etc.)
