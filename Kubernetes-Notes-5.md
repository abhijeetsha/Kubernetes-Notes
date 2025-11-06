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
### 🧾 Example PV:
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-volume
spec:
  capacity:
    storage: 5Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  hostPath:
    path: "/data/pv1"
