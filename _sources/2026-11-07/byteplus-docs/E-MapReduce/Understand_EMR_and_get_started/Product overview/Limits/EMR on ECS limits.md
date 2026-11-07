---
title: "EMR on ECS limits"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_on_ECS_limits"
---

When using E\-MapReduce on ECS (EMR on ECS), certain operations that are not intended by the product may cause cluster instability or even make the cluster unavailable. To avoid such issues, carefully read this document and understand the following limits.

<span id="53c123f3"></span>
# Limits


1. EMR recommends using supported browser versions

   * Google Chrome: version 36.0 or later

2. EMR cluster creation/management operation limits

   * Upgrading a non\-HA cluster to an HA cluster is not supported. It is recommended to enable high availability when creating production clusters.

   * Upgrading the service version of an existing cluster is not supported. Select the appropriate version when creating the cluster.


<span id="90d5afed"></span>
# High\-risk operation note

Do not perform the following operations arbitrarily to avoid abnormal cluster states and impact on EMR cluster usage:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">When the cluster is in an abnormal state, you can contact Volcano Engine technical support by <a href="https://console.volcengine.com/workorder/create/">submitting a ticket</a>. After obtaining your authorization, technical support personnel will log in to the EMR cluster for troubleshooting. Fees will continue to be charged during the abnormal period of the EMR cluster.</div>



|High\-risk operation |Possible consequences |Recommendation |
|---|---|---|
|During cluster initialization or after creation, **using non\-EMR consoles** (such as ECS management, EBS management, or OpenAPI) to perform unmounting, capacity expansion, or configuration changes on cloud disks attached to EMR cluster nodes. |The cluster is unavailable. |It is recommended to perform operations only in the EMR console. |
|During the cluster payment process, initialization process, or after creation, actions such as deleting, stopping, restarting, unsubscribing, or changing instance specifications on EMR cluster nodes **through channels other than the EMR console** (for example: ECS management/OpenAPI) may be performed. |* Modifying the Master node may cause the cluster to become unavailable.<br><br>* Modifying Core nodes or Task nodes may result in the loss of data replicas on the relevant nodes or failure of computing tasks. |It is recommended to perform operations only in the EMR console. |
|Deleting existing processes, installed applications, and files on cluster nodes. |The cluster is unavailable. |It is recommended to perform operations only in the EMR console. |
|Do not set an overly simple password for the EMR cluster Master node. |Malicious attacks by other users. |It is recommended to use a key pair. |
|Directly modifying parameters of EMR component configuration files on ECS nodes. |After the service restarts, the modified parameters may be overwritten. |It is recommended to modify parameters only in the EMR console. |
|Modifying or deleting files or directories that are not related to business operations. |Running jobs fail. |This operation is not recommended. If necessary, you can [submit a ticket](https://console.volcengine.com/workorder/create/) to contact Volcano Engine technical support personnel. |
|Binding, unbinding, releasing, or unsubscribing newly created public IPs of the cluster during the cluster creation process. |Cluster creation failed. |It is recommended to operate only on public IPs that you have created yourself. |
|Deleting or modifying the hosts file under the etc/hosts directory. |This causes the cluster to become unavailable. |This operation is not recommended. If necessary, you can [submit a ticket](https://console.volcengine.com/workorder/create/) to contact Volcano Engine technical support personnel. |
|Stopping the MySQL service of the Master node. |This causes the cluster to become unavailable, and services cannot access the database. |This operation is not recommended. If necessary, you can [submit a ticket](https://console.volcengine.com/workorder/create/) to contact Volcano Engine technical support personnel. |
|Modifying the pre\-installed MySQL root password on the emr\-master node. |This causes certain components on the cluster to fail abnormally. |This operation is not recommended. If necessary, you can [submit a ticket](https://console.volcengine.com/workorder/create/) to contact Volcano Engine technical support personnel. |
|Unbinding or changing the security group and VPC information bound to ECS nodes while the cluster is running. |The cluster is unavailable. |This operation is not recommended. If necessary, you can [submit a ticket](https://console.volcengine.com/workorder/create/) to contact Volcano Engine technical support. |
|Modify the relevant data used by Ambari. |The cluster is unavailable. |This operation is not recommended. If necessary, you can [submit a ticket](https://console.volcengine.com/workorder/create/) to contact Volcano Engine technical support. |
|When creating cluster metadata and selecting "Independent RDS MySQL", multiple clusters share the same RDS MySQL. |Cluster creation failed. |It is recommended that each RDS MySQL database be associated with only one cluster. |
|Use the ECS console or the OpenAPI provided by ECS to perform operations such as changing the billing method or renewing EMR nodes. |This results in being unable to revert to the original billing method. |To change the billing method in the EMR console, see [Convert Pay-As-You-Go to Subscription](https://docs.byteplus.com/docs/undefined/6a1d54568c7845050f5e4157).<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">EMR does not support converting from Subscription to Pay\-As\-You\-Go billing.</div><br> |
|Perform operations such as modifying basic environment information or upgrading the software stack version on ECS nodes. |Cluster status, engine basic features, and integration capabilities are unavailable due to exceptions. |This operation is not recommended. If necessary, you can [submit a ticket](https://console.volcengine.com/workorder/create/) to contact Volcano Engine technical support. |


<span id="2430ef34"></span>
# Data recovery and accidental deletion prevention note

When using TOS object storage in the EMR environment, to mitigate the irreversible risk caused by unintended deletions, you must enable the corresponding security protection feature based on the bucket type.


* Flat Bucket: You must enable [version control](https://www.volcengine.com/docs/6349/261963). After enabling, delete operations will only generate a "Delete Marker"; historical version data will still be retained, ensuring that version rollback is possible after accidental deletion.

* Hierarchical Bucket: You must enable the [Recycle Bin](https://www.volcengine.com/docs/6349/1458171). After enabling, files or directories deleted via the FileSystem delete method or commands such as hadoop rm will be moved to the Recycle Bin, providing an undo window within the configured retention period. If not enabled, data will be physically deleted immediately.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is recommended to configure according to the above content. If protection is not enabled, any deletion operation will result in permanent data loss.</div>
