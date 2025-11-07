# Introductions Of Monitoring And Loggings.
## 🧩 1. What is Monitoring and Logging in Kubernetes?
### Both are essential parts of Kubernetes cluster administration.
| Term           | Purpose                                                                                                           |
| -------------- | ----------------------------------------------------------------------------------------------------------------- |
| **Monitoring** | Collects and observes performance data (CPU, memory, network, etc.) to understand cluster and application health. |
| **Logging**    | Captures and stores system and application logs for debugging and auditing.                                       |
### Together, they help in troubleshooting, capacity planning, alerting, and performance optimization.

## ⚙️ 2. Monitoring in Kubernetes
### Monitoring focuses on metrics — measurable values that describe the system’s state.
##🔹 What do we monitor?
| Layer                 | Examples of Metrics                        |
| --------------------- | ------------------------------------------ |
| **Node Level**        | CPU, memory, disk usage, network traffic   |
| **Pod Level**         | Pod health, restart counts, resource usage |
| **Application Level** | Request latency, error rate, throughput    |
| **Cluster Level**     | Control plane health, scheduling latency   |

## 🔹 Types of Metrics
* Resource Metrics (CPU, Memory) — short-term performance data.
* Custom Metrics — app-level data (e.g., requests per second).
* External Metrics — from outside Kubernetes (e.g., cloud service metrics).

## 📊 3. Metrics Server.
### The Metrics Server is a built-in Kubernetes component for resource monitoring.
* It collects CPU and memory usage data from kubelets on each node.
* Data is stored in-memory (not persistent).
* Used by kubectl top, Horizontal Pod Autoscaler (HPA), and dashboards.

### 🔧 Install Metrics Server.
* kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml

### ✅ Verify Installation
* kubectl get deployment metrics-server -n kube-system

