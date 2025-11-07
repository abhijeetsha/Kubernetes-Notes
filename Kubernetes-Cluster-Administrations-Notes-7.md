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

## 🔁 2. Cluster Upgrade:
### Upgrading ensures your cluster runs the latest stable Kubernetes version, fixing bugs and adding new features.

## ⚙️ Upgrade Process Overview
### 1. Check current version:
* kubectl version

### 2. Plan upgrade
* Backup etcd
* Review Kubernetes release notes
* Verify compatibility (API versions, plugins, CNI, CSI)

### 3. Upgrade Control Plane.
* If using kubeadm, upgrade step-by-step:
  * apt update && apt install -y kubeadm=<version>
  * kubeadm upgrade plan
  * kubeadm upgrade apply v1.30.0

### 4. Upgrade kubelet & kubectl on control plane node.
* Commands:-
  * apt install -y kubelet=<version> kubectl=<version>
  * systemctl daemon-reload
  * systemctl restart kubelet

### 5. Upgrade Worker Nodes.
  * kubeadm upgrade node
  * apt install -y kubelet=<version>
  * systemctl restart kubelet

### Verify upgrade.
  * kubectl get nodes

## 🔒 Best Practices for Cluster Upgrade
### Upgrade one version at a time (e.g., v1.28 → v1.29 → v1.30).
 * Drain nodes before upgrading:
 * kubectl drain <node> --ignore-daemonsets
### Uncordon after upgrade:
 * kubectl uncordon <node>
 * Test workloads post-upgrade.

## 🧱 3. Custom Resource Definitions (CRDs)
### Kubernetes allows you to extend the API by creating Custom Resources (CRs).
🔹 What is a CRD?
* Custom Resource Definition (CRD): Defines a new resource type in Kubernetes.
* Custom Resource (CR): An instance of that type.
* Used by Operators, Custom Controllers, or teams who need domain-specific APIs.

## 🧩 Example: Creating a CRD
### CRD Definition:
* apiVersion: apiextensions.k8s.io/v1
* kind: CustomResourceDefinition
* metadata:
  * name: databases.myorg.com
* spec:
  * group: myorg.com
  * versions:
    * - name: v1
      * served: true
      * storage: true
      * schema:
        * openAPIV3Schema:
          * type: object
          * properties:
            * spec:
              * type: object
              * properties:
                * dbname:
                  * type: string
                * replicas:
                  * type: integer
  * scope: Namespaced
  * names:
    * plural: databases
    * singular: database
    * kind: Database
    * shortNames:
    * - db

## After applying this:
### kubectl apply -f database-crd.yaml
### Kubernetes now recognizes a new kind: Database
* Create a Custom Resource:
* apiVersion: myorg.com/v1
* kind: Database
* metadata:
  * name: mydb
* spec:
  * dbname: "customers"
  * replicas: 3
### Commands:
* kubectl apply -f mydb.yaml
* kubectl get databases

## ⚙️ CRDs Use Cases
* Extend Kubernetes to manage new services (e.g., Databases, ML jobs, etc.)
* Used by Operators like:
   * Prometheus Operator (Prometheus, Alertmanager)
   * Istio Operator
   * ArgoCD Custom Resources
