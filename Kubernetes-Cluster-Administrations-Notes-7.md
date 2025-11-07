# Introductions Of Cluster Administraions
## 🧩 What is Cluster Administration in Kubernetes
### Cluster Administration involves managing the overall Kubernetes control plane and nodes, ensuring:
   * Security (access control & policies)
   * Maintenance (upgrades, patches)
   * Extensibility (custom resources)
   * Monitoring and troubleshooting.

## 👤 1. RBAC (Role-Based Access Control)
### RBAC controls who can do what within the cluster.
* It manages access to resources using roles, role bindings, cluster roles, and cluster role bindings.

## 🧠 RBAC Core Concepts
| Component              | Description                                      | Scope     |
| ---------------------- | ------------------------------------------------ | --------- |
| **Role**               | Defines permissions (verbs on resources).        | Namespace |
| **RoleBinding**        | Assigns Role to a user/group/service account.    | Namespace |
| **ClusterRole**        | Same as Role but applies **cluster-wide**.       | Cluster   |
| **ClusterRoleBinding** | Binds ClusterRole to user/group/SA cluster-wide. | Cluster   |

## ⚙️ Example: Role & RoleBinding.
### Role (in a specific namespace):
* apiVersion: rbac.authorization.k8s.io/v1
* kind: Role
* metadata:
  * namespace: dev
  * name: pod-reader
* rules:
* - apiGroups: [""]
  * resources: ["pods"]
  * verbs: ["get", "watch", "list"]

### RoleBinding (binds the Role to a user):
* apiVersion: rbac.authorization.k8s.io/v1
* kind: RoleBinding
* metadata:
  * name: read-pods
  * namespace: dev
* subjects:
* - kind: User
  * name: abhi
  * apiGroup: rbac.authorization.k8s.io
* roleRef:
  * kind: Role
  * name: pod-reader
  * apiGroup: rbac.authorization.k8s.io

## ⚙️ ClusterRole & ClusterRoleBinding.
### Used for permissions across all namespaces (e.g., nodes, namespaces, persistent volumes).
### ClusterRole example:
* apiVersion: rbac.authorization.k8s.io/v1
* kind: ClusterRole
* metadata:
  * name: cluster-admin-role
* rules:
* - apiGroups: ["*"]
  * resources: ["*"]
  * verbs: ["*"]

### ClusterRoleBinding:
* apiVersion: rbac.authorization.k8s.io/v1
* kind: ClusterRoleBinding
* metadata:
  * name: cluster-admin-binding
* subjects:
* - kind: User
  * name: abhi
  * apiGroup: rbac.authorization.k8s.io
* roleRef:
  * kind: ClusterRole
  * name: cluster-admin-role
  * apiGroup: rbac.authorization.k8s.io

### Command Example:
* kubectl create clusterrolebinding abhi-admin --clusterrole=cluster-admin --user=abhi

### ✅ Check Current Permissions
* kubectl auth can-i get pods --namespace=dev


