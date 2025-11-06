# Storage In Kubernetes
## 🧱 1. What is Storage in Kubernetes?
### Ans: 
* By default, Pods are ephemeral — when a Pod is deleted or recreated, its data is lost.
To store data persistently, Kubernetes provides a storage system that connects Pods to durable storage backends (like EBS, NFS, etc.).
* Kubernetes separates how storage is provided (Persistent Volume) from how storage is used (Persistent Volume Claim).

## 💽 2. Persistent Volume (PV)
### 📘 Definition:
* A Persistent Volume (PV) is a piece of storage in the cluster that an administrator has provisioned (or dynamically created using a storage class).
* It’s a cluster resource, just like a node.

###🧠 Key Points:
* Created by admin or dynamically via StorageClass.
* Can use different backends: EBS (AWS), NFS, GCE Disk, Azure Disk, Ceph, iSCSI, etc.
* Lifecycle is independent of any Pod.

### Explanation:
* capacity: 5 GB of space
* accessModes:
    * ReadWriteOnce (RWO): Mounted by one node read-write
    * ReadOnlyMany (ROX): Read-only by many nodes
    * ReadWriteMany (RWX): Read-write by many nodes
* persistentVolumeReclaimPolicy: What happens when the claim is released (Retain/Delete/Reclaim)

## 📦 3. Persistent Volume Claim (PVC)
### 📘 Definition: A Persistent Volume Claim (PVC) is a request for storage by a user (like how a Pod requests CPU/memory).
* Pods use PVCs to mount storage.

## 4. StorageClass
📘 Definition:
* A StorageClass defines how to dynamically create PVs.
* Instead of manually creating PVs, you can let Kubernetes create them automatically when a PVC requests storage.
* Each cloud provider or storage system offers a provisioner (like kubernetes.io/aws-ebs).

## ⚙️ 5. ConfigMaps
### A ConfigMap is used to store configuration data (like environment variables, config files, or command-line args).

## 🔐 7. Secrets
### 📘 Definition:
* A Secret is like a ConfigMap, but used for sensitive data (like passwords, tokens, SSH keys).
* Kubernetes stores Secrets base64-encoded, not encrypted (you can use external encryption for extra security).

## 🧭 8. Summary Table
### Ans:-
| Concept                           | Purpose                         | Example Use                     |
| --------------------------------- | ------------------------------- | ------------------------------- |
| **Persistent Volume (PV)**        | Actual storage resource         | EBS, NFS, Disk                  |
| **Persistent Volume Claim (PVC)** | Request for PV by user          | Pod data storage                |
| **StorageClass**                  | Defines dynamic volume creation | Cloud volumes (AWS, GCP)        |
| **ConfigMap**                     | Non-sensitive config data       | App environment variables       |
| **Secret**                        | Sensitive config data           | Passwords, tokens, certificates |


## 🧩 9. Visual Summary
   +----------------------------+
   |     StorageClass           |
   |  (Dynamic Provisioner)     |
   +------------+---------------+
                |
         Creates PV dynamically
                ↓
   +----------------------------+
   |  Persistent Volume (PV)    |
   |  (e.g., AWS EBS, NFS)      |
   +------------+---------------+
                |
         Bound to claim
                ↓
   +----------------------------+
   |  Persistent Volume Claim   |
   |  (User Request for PV)     |
   +------------+---------------+
                |
         Mounted into Pod
                ↓
   +----------------------------+
   |           Pod              |
   +----------------------------+

## ✅ Quick Recap
### Ans: | Component        | Description                        |
| ---------------- | ---------------------------------- |
| **PV**           | Actual storage (admin-level)       |
| **PVC**          | User’s request for storage         |
| **StorageClass** | Template for automatic PV creation |
| **ConfigMap**    | Non-secret app configuration       |
| **Secret**       | Encrypted/sensitive configuration  |

