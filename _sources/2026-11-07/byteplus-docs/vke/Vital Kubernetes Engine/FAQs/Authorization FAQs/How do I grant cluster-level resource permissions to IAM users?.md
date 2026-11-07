---
title: "How do I grant cluster-level resource permissions to IAM users?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-grant-an-IAM-user-permissions-on-cluster-level-resources"
---

This topic describes how to grant cluster\-level resource access to IAM users.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For more information about authorization, see <a href="https://docs.byteplus.com/en/docs/vke/Configuring-RBAC-permissions">Configuring RBAC permissions</a>.</div>


<span id=".5pON5L2c6K-05piO"></span>
## Procedure

VKE supports controlling cluster resource access by customizing Role and ClusterRole objects in Kubernetes authorization policies. For more information about Role and ClusterRole, see [Role and ClusterRole](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#role-and-clusterrole).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Create a ClusterRole to define a cluster\-level role.

   ```yaml
   apiVersion: rbac.authorization.k8s.io/v1
   kind: ClusterRole
   metadata:
     name: demo-role  # ClusterRole object name.
   rules:
     - apiGroups:
         - ""
       resources:
         - nodes     # get/list permission for node resources.
         - persistentvolumes   # get/list permission for PersistentVolume resources.
         - limitranges      # get/list permission for LimitRange resources.
         - resourcequotas   # get/list permission for ResourceQuota resources.
       verbs:
         - get
         - list
     - apiGroups:
         - storage.k8s.io
       resources:
         - storageclasses   # get/list permission for StorageClass resources.
       verbs:
         - get
         - list
   ```
   

2. Create a ClusterRoleBinding to grant the permissions defined in the ClusterRole to one or more IAM users.

   ```yaml
   apiVersion: rbac.authorization.k8s.io/v1
   kind: ClusterRoleBinding
   metadata:
     labels:
       rbac.vke.volcengine.com/user: "100****"    # Account ID of the authorized IAM user.
     name: demo-rolebending       # ClusterRoleBinding object name.
   roleRef:
     apiGroup: rbac.authorization.k8s.io
     kind: ClusterRole
     name: demo-role  # ClusterRole object name.
   subjects:
   - apiGroup: rbac.authorization.k8s.io
     kind: User
     name: "xxxx"    # Account ID of the authorized IAM user.
   ```
   

3. Use the authorized IAM user to connect to the cluster. If you can successfully query cluster\-level resources (such as PV), the permission configuration is valid. For details on connecting to clusters, see [Connecting to clusters](https://docs.byteplus.com/en/docs/vke/Connecting-to-a-cluster).

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3466ab265aa1558d6499f91c3f38e888.png) </span>
