---
title: "Description of RBAC permission roles"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/RBAC-roles"
---

This topic mainly describes the names of role\-based access control (RBAC) roles, their corresponding ClusterRole names, and the corresponding permission names in Kubernetes.

<span id=".Y2x1c3RlcnJvbGUt5ZG95ZCN6K-05piO"></span>
## Description of ClusterRole names


|RBAC access permission role |ClusterRole name |Kubernetes permission name |
|---|---|---|
|Cluster administrator |vke:admin |See [vke:admin](https://docs.byteplus.com/en/docs/vke/RBAC-roles#vke-admin). |
|Operation and maintenance administrator |vke:ops |See [vke:ops](https://docs.byteplus.com/en/docs/vke/RBAC-roles#vke-ops). |
|Privileged developer |vke:dev\-promoted |See [vke:dev-promoted](https://docs.byteplus.com/en/docs/vke/RBAC-roles#vke-dev-promoted). |
|Developers |vke:dev |See [vke:dev](https://docs.byteplus.com/en/docs/vke/RBAC-roles#vke-dev). |
|Read\-only user |vke:visitor |See [vke:visitor](https://docs.byteplus.com/en/docs/vke/RBAC-roles#vke-visitor). |


<span id=".a3ViZXJuZXRlcy3mnYPpmZDlkI3np7Dor7TmmI4="></span>
## Description of Kubernetes permission names

<span id="vke-admin"></span>
### vke:admin

Run the following command to view the details of Kubernetes permissions that correspond to `vke:admin`.

```Bash
kubectl get ClusterRole vke:admin --output=yaml
```


Expected output result:

```YAML
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  creationTimestamp: "2023-05-17T04:03:24Z"
  labels:
    app.kubernetes.io/managed-by: Helm
    rbac.vke.volcengine.com/preset-role: "true"
    rbac.vke.volcengine.com/version: 1.0.0
  name: vke:admin
  resourceVersion: "308"
  uid: f79ed7ee-2c92-4074-9b00-359d********
rules:
- apiGroups:
  - '*'
  resources:
  - '*'
  verbs:
  - '*'
- nonResourceURLs:
  - '*'
  verbs:
  - '*'
```


<span id="vke-ops"></span>
### vke:ops

Run the following command to view the details of Kubernetes permissions that correspond to `vke:ops`.

```Bash
kubectl get clusterrole vke:ops --output=yaml
```


Expected output result:

```YAML
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  creationTimestamp: "2023-05-17T04:03:24Z"
  labels:
    app.kubernetes.io/managed-by: Helm
    argocd.argoproj.io/instance: vke-resource-controller
    rbac.vke.volcengine.com/preset-role: "true"
    rbac.vke.volcengine.com/version: 1.0.6
  name: vke:ops
  resourceVersion: "37760530"
  uid: 85d4a166-1acf-4cd0-8ef1-2bf5********
rules:
- apiGroups:
  - ""
  resources:
  - pods
  - pods/attach
  - pods/exec
  - pods/portforward
  - pods/proxy
  - pods/eviction
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - ""
  resources:
  - namespaces
  - nodes
  - persistentvolumes
  - configmaps
  - endpoints
  - persistentvolumeclaims
  - replicationcontrollers
  - replicationcontrollers/scale
  - secrets
  - serviceaccounts
  - services
  - services/proxy
  - limitranges
  - resourcequotas
  - resourcequotas/status
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - ""
  resources:
  - bindings
  - events
  - namespaces/status
  - replicationcontrollers/status
  - pods/log
  - pods/status
  - componentstatuses
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - coordination.k8s.io
  resources:
  - leases
  verbs:
  - get
- apiGroups:
  - apps
  resources:
  - daemonsets
  - daemonsets/status
  - deployments
  - deployments/status
  - deployments/rollback
  - deployments/scale
  - replicasets
  - replicasets/scale
  - statefulsets
  - controllerrevisions
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - autoscaling
  resources:
  - horizontalpodautoscalers
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - batch
  resources:
  - cronjobs
  - jobs
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - extensions
  resources:
  - daemonsets
  - daemonsets/status
  - deployments
  - deployments/status
  - deployments/rollback
  - deployments/scale
  - ingresses
  - replicasets
  - replicasets/scale
  - replicationcontrollers/scale
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - networking.k8s.io
  resources:
  - '*'
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - servicecatalog.k8s.io
  resources:
  - clusterserviceclasses
  - clusterserviceplans
  - clusterservicebrokers
  - serviceinstances
  - servicebindings
  verbs:
  - create
  - delete
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - servicecatalog.k8s.io
  resources:
  - clusterservicebrokers/status
  - clusterserviceclasses/status
  - clusterserviceplans/status
  - serviceinstances/status
  - serviceinstances/reference
  - servicebindings/status
  verbs:
  - update
- apiGroups:
  - storage.k8s.io
  resources:
  - storageclasses
  verbs:
  - create
  - delete
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - apiextensions.k8s.io
  resources:
  - customresourcedefinitions
  verbs:
  - get
  - list
  - create
  - watch
  - patch
  - update
  - delete
  - deletecollection
- apiGroups:
  - vke.volcengine.com
  resources:
  - cronhpas
  verbs:
  - get
  - list
  - create
  - watch
  - patch
  - update
  - delete
  - deletecollection
- apiGroups:
  - appinspect.elkeid.bytedance.com
  resources:
  - secinspectpolicies
  - secinspectreports
  - secinspectrunconfigs
  - secinspectclusterreports
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - loadbalancer.vke.volcengine.com
  resources:
  - albinstances
  verbs:
  - create
  - delete
  - get
  - list
  - patch
  - update
  - watch
```


<span id="vke-dev-promoted"></span>
### vke:dev\-promoted

Run the following command to view the details of Kubernetes permissions that correspond to `vke:dev-promoted`.

```Bash
kubectl get clusterrole vke:dev-promoted --output=yaml
```


Expected output result:

```YAML
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  creationTimestamp: "2023-05-17T04:03:24Z"
  labels:
    app.kubernetes.io/managed-by: Helm
    rbac.vke.volcengine.com/preset-role: "true"
    rbac.vke.volcengine.com/version: 1.0.4
  name: vke:dev-promoted
  resourceVersion: "37760524"
  uid: 7baff690-a3eb-4ab4-b5b2-4ff3********
rules:
- apiGroups:
  - ""
  resources:
  - nodes
  - persistentvolumes
  - limitranges
  - resourcequotas
  verbs:
  - get
  - list
- apiGroups:
  - storage.k8s.io
  resources:
  - storageclasses
  verbs:
  - get
  - list
- apiGroups:
  - loadbalancer.vke.volcengine.com
  resources:
  - albinstances
  verbs:
  - get
  - list
- apiGroups:
  - networking.k8s.io
  resources:
  - ingressclasses
  verbs:
  - get
  - list
```


<span id="vke-dev"></span>
### vke:dev

Run the following command to view the details of Kubernetes permissions that correspond to `vke:dev`.

```Bash
kubectl get clusterrole vke:dev --output=yaml
```


Expected output result:

```YAML
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  creationTimestamp: "2023-05-17T04:03:24Z"
  labels:
    app.kubernetes.io/managed-by: Helm
    argocd.argoproj.io/instance: vke-resource-controller
    rbac.vke.volcengine.com/preset-role: "true"
    rbac.vke.volcengine.com/version: 1.0.5
  name: vke:dev
  resourceVersion: "37760513"
  uid: a6917647-e8c8-429d-abe5-b381********
rules:
- apiGroups:
  - ""
  resources:
  - pods
  - pods/attach
  - pods/exec
  - pods/portforward
  - pods/proxy
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - ""
  resources:
  - configmaps
  - endpoints
  - replicationcontrollers
  - replicationcontrollers/scale
  - secrets
  - serviceaccounts
  - services
  - services/proxy
  - persistentvolumeclaims
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - ""
  resources:
  - events
  - namespaces/status
  - replicationcontrollers/status
  - pods/log
  - pods/status
  - componentstatuses
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - ""
  resources:
  - namespaces
  - nodes
  - persistentvolumes
  - limitranges
  - resourcequotas
  - resourcequotas/status
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - apps
  resources:
  - daemonsets
  - daemonsets/status
  - deployments
  - deployments/status
  - deployments/rollback
  - deployments/scale
  - replicasets
  - replicasets/scale
  - statefulsets
  - controllerrevisions
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - autoscaling
  resources:
  - horizontalpodautoscalers
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - batch
  resources:
  - cronjobs
  - jobs
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - extensions
  resources:
  - daemonsets
  - daemonsets/status
  - deployments
  - deployments/status
  - deployments/rollback
  - deployments/scale
  - ingresses
  - replicasets
  - replicasets/scale
  - replicationcontrollers/scale
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - networking.k8s.io
  resources:
  - '*'
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - servicecatalog.k8s.io
  resources:
  - clusterserviceclasses
  - clusterserviceplans
  - clusterservicebrokers
  - serviceinstances
  - servicebindings
  verbs:
  - create
  - delete
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - servicecatalog.k8s.io
  resources:
  - clusterservicebrokers/status
  - clusterserviceclasses/status
  - clusterserviceplans/status
  - serviceinstances/status
  - serviceinstances/reference
  - servicebindings/status
  verbs:
  - update
- apiGroups:
  - policy
  resources:
  - poddisruptionbudgets
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
- apiGroups:
  - apiextensions.k8s.io
  resources:
  - customresourcedefinitions
  verbs:
  - get
  - list
  - create
  - watch
  - patch
  - update
  - delete
  - deletecollection
- apiGroups:
  - storage.k8s.io
  resources:
  - storageclasses
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - vke.volcengine.com
  resources:
  - cronhpas
  verbs:
  - get
  - list
  - create
  - watch
  - patch
  - update
  - delete
  - deletecollection
- apiGroups:
  - appinspect.elkeid.bytedance.com
  resources:
  - secinspectpolicies
  - secinspectreports
  - secinspectrunconfigs
  - secinspectclusterreports
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - loadbalancer.vke.volcengine.com
  resources:
  - albinstances
  verbs:
  - create
  - delete
  - deletecollection
  - get
  - list
  - patch
  - update
  - watch
```


<span id="vke-visitor"></span>
### vke:visitor

Run the following command to view the details of Kubernetes permissions that correspond to `vke:visitor`.

```Bash
kubectl get clusterrole vke:visitor --output=yaml
```


Expected output result:

```YAML
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  creationTimestamp: "2023-05-17T04:03:24Z"
  labels:
    app.kubernetes.io/managed-by: Helm
    rbac.vke.volcengine.com/preset-role: "true"
    rbac.vke.volcengine.com/version: 1.0.4
  name: vke:visitor
  resourceVersion: "307"
  uid: 0174b6f8-cde5-411d-bb01-b34f********
rules:
- apiGroups:
  - ""
  resources:
  - pods
  - pods/attach
  - pods/exec
  - pods/portforward
  - pods/proxy
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - ""
  resources:
  - endpoints
  - persistentvolumeclaims
  - replicationcontrollers
  - replicationcontrollers/scale
  - serviceaccounts
  - services
  - services/proxy
  - namespaces
  - nodes
  - persistentvolumes
  - limitranges
  - resourcequotas
  - resourcequotas/status
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - ""
  resources:
  - events
  - replicationcontrollers/status
  - pods/log
  - pods/status
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - apps
  resources:
  - daemonsets
  - deployments
  - deployments/rollback
  - deployments/scale
  - replicasets
  - replicasets/scale
  - statefulsets
  - controllerrevisions
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - autoscaling
  resources:
  - horizontalpodautoscalers
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - batch
  resources:
  - cronjobs
  - jobs
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - extensions
  resources:
  - daemonsets
  - deployments
  - deployments/rollback
  - deployments/scale
  - ingresses
  - replicasets
  - replicasets/scale
  - replicationcontrollers/scale
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - networking.k8s.io
  resources:
  - '*'
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - servicecatalog.k8s.io
  resources:
  - clusterserviceclasses
  - clusterserviceplans
  - clusterservicebrokers
  - serviceinstances
  - servicebindings
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - policy
  resources:
  - poddisruptionbudgets
  verbs:
  - get
  - list
- apiGroups:
  - apiextensions.k8s.io
  resources:
  - customresourcedefinitions
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - storage.k8s.io
  resources:
  - storageclasses
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - vke.volcengine.com
  resources:
  - cronhpas
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - appinspect.elkeid.bytedance.com
  resources:
  - secinspectpolicies
  - secinspectreports
  - secinspectrunconfigs
  - secinspectclusterreports
  verbs:
  - get
  - list
  - watch
- apiGroups:
  - loadbalancer.vke.volcengine.com
  resources:
  - albinstances
  verbs:
  - get
  - list
  - watch
```
