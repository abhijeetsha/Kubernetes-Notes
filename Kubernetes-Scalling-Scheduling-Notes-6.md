# Understanding Of Scalling And Scheduling.
## 🧩 What is Scaling and Scheduling in Kubernetes..?
### Ans: Kubernetes provides automation for scaling workloads and intelligent scheduling of Pods across cluster nodes.

## ⚙️ 1. Scaling in Kubernetes
### Scaling = Increasing or decreasing the number of running Pods to handle load.
* There are two types of scaling:

🔹 Manual Scaling
* You can scale Pods manually using the command:
* kubectl scale deployment <deployment-name> --replicas=5
* This updates the number of replicas (Pods) for a Deployment.

🔹 Automatic Scaling
* Kubernetes can automatically adjust Pods or resource allocations based on metrics (CPU, memory, etc).
* There are 3 types:
   * HPA (Horizontal Pod Autoscaler)
   * VPA (Vertical Pod Autoscaler)
   * Cluster Autoscaler

## 🧭 2. Horizontal Pod Autoscaler (HPA)
* Purpose: Automatically increases or decreases the number of Pods based on CPU, memory, or custom metrics.
* Example: Scale Pods between 2 and 10 if CPU > 80%.
* kubectl autoscale deployment myapp --min=2 --max=10 --cpu-percent=80

## 🧱 3. Vertical Pod Autoscaler (VPA)
### Purpose: Automatically adjusts CPU and memory requests/limits for Pods (instead of changing Pod count).
* Useful for workloads that always run the same number of Pods but need more or fewer resources.
* Modes:
   * Off: Only gives recommendations.
   * Auto: Applies changes automatically.
   * Initial: Applies recommendations only when Pod starts.

## ⚡ 4. Cluster Autoscaler
### Automatically adds or removes nodes in the cluster (on AWS, GCP, Azure) depending on pending Pods.
   * It works with cloud providers’ auto-scaling groups.

## 🧮 5. Scheduling in Kubernetes
### Scheduling = Deciding which node runs which Pod.
*  The Kube-scheduler decides placement based on:
   * Resource availability (CPU/memory)
   * Node selectors
   * Affinity/anti-affinity
   * Taints and tolerations
   * Resource requests/limits

 ## 🌍 6. Node Affinity
 ### Allows Pods to prefer or require scheduling on specific nodes based on labels.
### Types:
  * requiredDuringSchedulingIgnoredDuringExecution: Must match.
  * preferredDuringSchedulingIgnoredDuringExecution: Prefer to match.

## 🚫 7. Taints and Tolerations
### Ans: Used to control which Pods can be scheduled on which nodes.
   * Taint: Applied on Node (makes it repel Pods).
   * Toleration: Applied on Pod (allows it to “tolerate” the taint).

### Example:
* Taint a node:
* kubectl taint nodes node1 key=value:NoSchedule
### Pod toleration example:
* tolerations:
* - key: "key"
  * operator: "Equal"
  * value: "value"
  * effect: "NoSchedule"

## ⚖️ 8. Resource Requests and Limits
### Defines how much CPU/memory a Pod needs (request) and the maximum it can use (limit).
### Example: 
* resources:
  * requests:
    * cpu: "250m"
    * memory: "256Mi"
  * limits:
    * cpu: "500m"
    * memory: "512Mi"
* Requests = Scheduler uses this to place Pods.
* Limits = Maximum resources the container can use.

## 📦 9. Resource Quotas
### Restrict total resource usage per namespace.
* Example:
* apiVersion: v1
* kind: ResourceQuota
* metadata:
  * name: compute-quota
  * namespace: dev
* spec:
  * hard:
    * pods: "10"
    * requests.cpu: "4"
    * limits.memory: "8Gi"

## 🩺 10. Probes
### Probes monitor Pod health.
🔹 Liveness Probe
* Checks if the container is running properly.
* If it fails → Pod restarts.
   * livenessProbe:
  * httpGet:
     * path: /healthz
     * port: 8080
   * initialDelaySeconds: 10
   * periodSeconds: 5

## 🔹 Readiness Probe
### Checks if the Pod is ready to receive traffic.
* If fails → Pod is removed from Service load balancer.
* readinessProbe:
  * tcpSocket:
    * port: 8080

## 🔹 Startup Probe
### Checks if the app has started successfully before liveness checks begin.
* startupProbe:
  * exec:
    * command: ["cat", "/tmp/healthy"]
  * failureThreshold: 30
  * periodSeconds: 10

## 🧠 Summary Table
| Concept            | Purpose                            | Applies To            |
| ------------------ | ---------------------------------- | --------------------- |
| HPA                | Scale Pods horizontally            | Deployment/ReplicaSet |
| VPA                | Adjust Pod resource limits         | Deployment/Pod        |
| Node Affinity      | Schedule Pods on specific nodes    | Pod                   |
| Taints/Tolerations | Restrict Pod placement             | Node + Pod            |
| Resource Quota     | Limit total resources in namespace | Namespace             |
| Limits/Requests    | Define Pod resource usage          | Pod                   |
| Probes             | Monitor Pod health                 | Pod                   |
