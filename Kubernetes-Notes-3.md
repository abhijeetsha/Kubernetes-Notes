# 🔹 Workloads Of Kubernetes:
## ☸️ Kubernetes Workloads Overview:
### In Kubernetes, a Workload is an object that defines how your application runs — how many Pods, how they update, how they store data, and how they recover if something fails

## All workloads manage Pods.

## 🚀 1. Deployment Workloads:-
### Ans:-
### 📘 Purpose:
* The most common workload.
* Manages stateless applications (apps that don’t need to remember data between restarts).
* Uses ReplicaSets behind the scenes to ensure desired Pod count.

### 🧠 Features:
* Rolling updates and rollbacks.
* Scaling (up/down replicas easily).
* Self-healing (recreates failed Pods).
* 🔹 Use Case: Web servers, APIs, frontend apps — anything stateless.

## 🧱 2. StatefulSet Workloads:-
### 📘 Purpose:
* Used for stateful applications that require:
* Stable network identity (same Pod name).
* Persistent storage.
* Ordered deployment & scaling.

### 🧠 Features:
* Pods are created with unique, consistent names (e.g., db-0, db-1, db-2).
* Each Pod keeps its own persistent volume.
* 🔹 Use Case: Databases (MySQL, MongoDB), message queues (Kafka, RabbitMQ).

## ⚙️ 3. DaemonSet Workloads:-
### 📘 Purpose:
* Ensures a copy of a Pod runs on every (or selected) Node.
* Commonly used for background system tasks.

### 🧠 Features:
* Automatically runs one Pod per Node.
* When a new Node is added, a Pod is automatically scheduled.
* 🔹 Use Case:
  * Node monitoring agents (Prometheus Node Exporter)
  * Logging (Fluentd, Filebeat)
  * Security agents.

## 🧮 4. ReplicaSet Workloads
### 📘 Purpose:
* Ensures a specified number of identical Pods are running at any time.
* Deployments use ReplicaSets internally — you rarely create them directly now.

### 🧠 Features:
* Self-healing: replaces crashed Pods.
* Doesn’t handle updates or rollbacks (that’s Deployment’s job).
* 🔹 Use Case: Ensuring a fixed number of identical stateless Pods — but most teams use Deployments instead.

## 🧰 5. Job Workloads:-
### 📘 Purpose:
* Runs a task to completion (not long-running).
* Once the Pod finishes successfully, it doesn’t restart.

### 🧠 Features:
* Good for one-time batch jobs or short-lived scripts.
* 🔹 Use Case: Data backup, file processing, batch tasks, migration scripts.

### ⏰ 6. CronJob Workloads
## 📘 Purpose:
* Runs Jobs on a schedule, like a Linux cron job.
* Example: “Run a backup every day at midnight.”

### 🧠 Features:
* Uses cron syntax (*/5 * * * *) for scheduling.
* Each run creates a Job, which in turn creates Pods.
* 🔹 Use Case: Regular backups, data cleanup, scheduled notifications, etc.
