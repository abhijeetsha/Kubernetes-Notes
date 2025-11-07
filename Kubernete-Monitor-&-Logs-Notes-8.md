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

##@ 🔍 View Metrics
* kubectl top nodes
* kubectl top pods
* Example Output:
* NAME        CPU(cores)   MEMORY(bytes)
* node1       200m         800Mi

## 🪵 4. Logging in Kubernetes
* Logs are text output from applications, system components, and containers.
* Kubernetes itself doesn’t manage log storage — you must configure a logging pipeline.

## 🔹 Types of Logs
| Source               | Example                                        |
| -------------------- | ---------------------------------------------- |
| **Application Logs** | `stdout` and `stderr` from containers          |
| **System Logs**      | Logs from `kubelet`, `container runtime`, etc. |
| **Audit Logs**       | Security-related events (API access, changes)  |

## 🔹 Access Logs
* View container logs:---> kubectl logs <pod-name>
* If multiple containers in one Pod:----> kubectl logs <pod-name> -c <container-name>

## 🔹 Centralized Logging
### To manage logs across many Pods and Nodes, use a logging stack:

## 🧱 Common Logging Stack:
### EFK Stack (Elasticsearch + Fluentd + Kibana)
| Component         | Function                     |
| ----------------- | ---------------------------- |
| **Fluentd**       | Collects & forwards logs     |
| **Elasticsearch** | Stores and indexes logs      |
| **Kibana**        | Visualizes and searches logs |
### Alternative: Loki + Promtail + Grafana (lightweight and efficient).

## 📈 5. Monitoring & Logging Tools.
* Let’s look at the most popular and widely used tools:-

## 🧠 Monitoring Tools:-
| Tool                    | Description                                       | Usage                             |
| ----------------------- | ------------------------------------------------- | --------------------------------- |
| **Metrics Server**      | Resource metrics (CPU, memory) for short-term use | Built-in, lightweight             |
| **Prometheus**          | Open-source monitoring & alerting toolkit         | Collects metrics using pull model |
| **Grafana**             | Visualization & dashboard tool                    | Works with Prometheus, Loki, etc. |
| **Kube-state-metrics**  | Exposes cluster state metrics                     | Used by Prometheus                |
| **cAdvisor**            | Provides container-level metrics to kubelet       | Node-level monitoring             |
| **Datadog / New Relic** | SaaS-based monitoring tools                       | Commercial, full-stack visibility |

## 🪵 Logging Tools
| Tool                                                      | Description                                   | Key Feature                       |
| --------------------------------------------------------- | --------------------------------------------- | --------------------------------- |
| **Fluentd / Fluent Bit**                                  | Log collectors and forwarders                 | Collect logs to external storage  |
| **Elasticsearch**                                         | Stores and indexes logs                       | Part of EFK Stack                 |
| **Kibana**                                                | Visualizes Elasticsearch data                 | Log dashboards and searches       |
| **Loki**                                                  | Lightweight log aggregation system by Grafana | Works with Promtail               |
| **Promtail**                                              | Collects logs for Loki                        | Kubernetes-native                 |
| **Cloud Logging (e.g., AWS CloudWatch, GCP Stackdriver)** | Cloud-managed log storage                     | Easy integration with managed K8s |

