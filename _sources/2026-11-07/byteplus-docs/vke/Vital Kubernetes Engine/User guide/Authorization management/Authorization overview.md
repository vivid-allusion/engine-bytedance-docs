---
title: "Authorization overview"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Authorization-overview"
---

Authorization management of VKE includes Identity and Access Management (IAM) authorization, Role\-Based Access Control (RBAC) authorization, and IAM Role for Service Account (IRSA) permission isolation.

<span id="4s3gASh8"></span>
## Terms


|Category |IAM permissions |RBAC permissions |IRSA mechanism |
|---|---|---|---|
|Introduction |IAM controls whether IAM users can access VKE and related cloud services, which is a form of external access control. |RBAC manages the operation permissions of IAM users or roles on internal resources of the Kubernetes cluster. |IRSA maps IAM role permissions to Kubernetes service accounts, which enables Pods to securely access cloud resources. This is a Pod\-level permission isolation mechanism. |
|Implementation methods |Implemented through system preset or custom IAM policies. |Implemented through RoleBinding/ClusterRoleBinding. |Implemented by binding Kubernetes service accounts with IAM roles through the OIDC protocol. |
|Application scenarios |Used for managing user access permissions on cloud resources. In most cases, IAM needs to be used with RBAC permissions to manage resources in clusters. |Used for managing user operation permissions within Kubernetes clusters. |Applicable to fine\-grained permission isolation in multi\-tenant scenarios, which enables container applications to securely access cloud resources. |
|Action |[Granting IAM permissions](https://docs.byteplus.com/en/docs/vke/Configuring-IAM-user-permissions) |[Granting RBAC permissions](https://docs.byteplus.com/en/docs/vke/Configuring-RBAC-permissions) |[Using IRSA in clusters](https://docs.byteplus.com/en/docs/vke/Using_IRSA_in_clusters) |


<span id=".aWFtLeaOiOadgw=="></span>
## IAM permissions

IAM is a permission management system provided by BytePlus for users. It is used to manage the access permissions on cloud resources to different IAM identities, including IAM users, user groups, and roles. Identities created through IAM are not granted access permissions on cloud resources by default. IAM provides predefined permissions for each cloud service. You can grant these permissions to identities based on your business requirements. You can also configure custom permission policies for fine\-grained permission management.

IAM supports the following two types of permission policies:


* System\-preset policies: The policies are created by the BytePlus in a centralized manner. You can only use but cannot modify them, and the version updates of these policies are maintained by the BytePlus.

* User\-defined policies: You can create, update, and delete the policies. The version updates of these policies are maintained by yourself.


<span id=".57O757uf6aKE6K6-562W55Wl"></span>
### System\-preset policies

VKE provides the following preset system policies, which can be directly attached to IAM users. For detailed configuration instructions, see [Attaching system-preset policies](https://docs.byteplus.com/en/docs/vke/Configuring-IAM-user-permissions#.5YWz6IGU57O757uf6aKE6K6-562W55Wl).


|Policy |Policy description |
|---|---|
|VKEFullAccess |This policy allows full read and write access to VKE, including Elastic Compute Service (ECS), LoadBalancer, VPC, and NAT Gateway. |
|VKEInnerFullAccess |This policy allows internal read and write access to VKE. |
|VKEReadOnlyAccess |This policy allows read\-only access to VKE. |
|VKEInnerReadOnlyAccess |This policy grants read\-only permissions in VKE. |
|BillingCenterPayOrderAccess |This policy grants payment permissions for the Billing Center and PayOrder permissions for OpenAPI access. |


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Starting from August 31, 2025, all IAM users (even those with <strong>FullAccess</strong> permission) must have <strong>BillingCenterPayOrderAccess</strong> permission to apply for prepaid resources. Otherwise, order payment cannot be completed. </div>


<span id=".55So5oi36Ieq5a6a5LmJ562W55Wl"></span>
### User\-defined policies

VKE allows you to create custom policies and grant permissions. For detailed configuration instructions, see [Attach user-defined policies](https://docs.byteplus.com/en/docs/vke/Configuring-IAM-user-permissions#.5YWz6IGU55So5oi36Ieq5a6a5LmJ562W55Wl).

The following table describes authorization actions (Action) and resources (Resource) supported in VKE.  For more information, see [Policy syntax](https://docs.byteplus.com/en/docs/byteplus-platform/docs-what-is-the-policy-syntax).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Resources are configured in the form of TRN, which is a unique identifier for BytePlus cloud resources. The format is <code>trn:{service}:{region}:{account}:{resourceType}/{id}</code>.</div>



|Category |Action |Resource |Description |
|---|---|---|---|
|cluster |CreateCluster |No |Create a cluster. |
||ListClusters |No |Obtain the list and details of clusters. |
||UpdateClusterConfig |trn:vke:{region}:{account}:cluster/ |Update cluster configurations. |
||DeleteCluster |trn:vke:{region}:{account}:cluster/ |Delete a cluster. |
||ListSupportedResourceTypes |No |Obtain the resource types supported by a cluster. |
||CreateKubeconfig |trn:vke:{region}:{account}:cluster/ |Generate the Kubeconfig credentials for a cluster. |
||ListKubeconfigs |No |Query the list of Kubeconfig details for clusters that meet the specified criteria. |
||DeleteKubeconfigs |trn:vke:{region}:{account}:cluster/ |Revoke the Kubeconfig credentials of a cluster. |
|Node pool management |CreateNodePool |trn:vke:{region}:{account}:cluster/ |Create a node pool. |
||CreateDefaultNodePool |trn:vke:{region}:{account}:cluster/ |Create a default node pool. |
||UpdateNodePoolConfig |trn:vke:{region}:{account}:cluster/ |Update node pool configurations. |
||ListNodePools |No |Query the list and details of node pools. |
||DeleteNodePool |trn:vke:{region}:{account}:cluster/ |Delete a node pool. |
|Nodes |CreateNodes |trn:vke:{region}:{account}:cluster/ |Add a node. |
||ListNodes |No |Obtain the list and details of nodes. |
||DeleteNodes |trn:vke:{region}:{account}:cluster/ |Remove a node. |
|Tag |TagResources |No |Add a label to a specified resource. |
||UntagResources |No |Remove a label from a resource. |
||ListTagsForResources |No |Query all label information for resources that meet the criteria. |
|Add\-ons |ListSupportedAddons |trn:vke:{region}:{account}:cluster/ |View the details of add\-ons that are supported by VKE. |
||CreateAddon |trn:vke:{region}:{account}:cluster/ |Install add\-ons for a specified cluster. |
||UpdateAddonConfig |trn:vke:{region}:{account}:cluster/ |Update the configurations of a specified add\-on in a specified cluster. |
||UpdateAddonVersion |trn:vke:{region}:{account}:cluster/ |Update the version of a specified add\-on in a specified cluster. |
||DeleteAddon |trn:vke:{region}:{account}:cluster/ |Remove a specified add\-on from a specified cluster. |
||ListAddons |No |Query the details of installed add\-ons that meet the criteria. |
|Access policy |GrantPermission |No |Granting RBAC access permission to an IAM user or role. |
||ListPermissions |No |Making queries to find RBAC access policy resources that meet the conditions. |
||RevokePermission |No |Revoke the RBAC permission granted to an IAM user or role by specifying the resource ID of the permission policy. |


<span id=".cmJhY-aOiOadgw=="></span>
## RBAC permissions

RBAC is a permission control system based on roles. VKE provides the cluster RBAC authorization feature to meet the requirement for fine\-grained resource access control of enterprises.


* Preset RBAC roles

   VKE provides the following preset RBAC roles, which can be directly assigned to IAM users or roles.

   
   |Role |Role description |
   |---|---|
   |Cluster administrator |Has read and write permissions on all resources in clusters and all namespaces, such as cluster nodes, StorageClasses, PVs, namespaces, ResourceQuotas, and LimitRanges. |
   |Operation and maintenance administrator |Has read and write permissions on visible Kubernetes resources in all namespaces in the console, such as cluster nodes, StorageClasses, PVs, namespaces, ResourceQuotas, and LimitRanges. |
   |Privileged developer |Has read\-only permissions on Kubernetes cluster\-level resources such as nodes, StorageClasses, PVs, namespaces, ResourceQuotas, and LimitRanges. |
   |Developers |Has read and write permissions on visible Kubernetes resources in all namespaces or in specified namespaces in the console, and has read\-only permissions on cluster nodes, StorageClasses, PersistentVolumes (PVs), namespaces, ResourceQuotas, and LimitRanges. |
   |Read\-only user |Has read\-only permissions on visible Kubernetes resources in all namespaces or in specified namespaces in the console, such as cluster nodes, StorageClasses, PVs, namespaces, ResourceQuotas, and LimitRanges, and cannot view configuration items and Secrets. |
   

* Custom RBAC roles

   VKE provides various custom finer\-grained RBAC permissions, which allow you to manage and control access permissions on various resources at the cluster level.


<span id="hrLTwTP9"></span>
## IRSA mechanism

The IRSA mechanism is a security isolation mechanism jointly provided by VKE and IAM. It is mainly used to allow Pods in Kubernetes clusters to be associated with IAM roles and use IAM role permissions by using Kubernetes ServiceAccount. This enables the Pods to securely access various cloud product resources. For more information, see [IRSA overview](https://docs.byteplus.com/en/docs/vke/IRSA-overview).
