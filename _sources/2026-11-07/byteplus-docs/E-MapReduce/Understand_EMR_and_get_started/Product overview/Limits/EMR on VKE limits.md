---
title: "EMR on VKE limits"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/EMR_on_VKE_limits"
---

When using E\-MapReduce on VKE (EMR on VKE), certain operations that are not intended by the product may cause cluster instability or even make the cluster unavailable. To avoid such issues, please read this document carefully and understand the following limits.

<span id="99b634b2"></span>
# Limits


1. Recommended browsers and versions for accessing the EMR console.

   * Google Chrome: version 36.0 or later.

2. EMR cluster creation and management operation limits.

   * Upgrading components of a running cluster is not supported. Please select the correct component versions when creating the cluster.


<span id="9da770c8"></span>
# High\-risk operation note

Exercise caution when performing the following operations to avoid abnormal cluster states and impact on EMR cluster usage:


|High\-risk operation |Possible outcomes |Recommendation |
|---|---|---|
|Do not modify namespace information, network configuration, cluster configuration, and more for the VKE cluster |Abnormal cluster state, abnormal job execution |None |
|Do not uninstall components already installed in the VKE cluster |Some cluster functions may become unavailable, such as monitoring, access links, and many other |None |
|The specifications of ECS nodes and attached EBS disks used by EMR cannot be changed outside of EMR (such as specification adjustment, capacity expansion, and more) |Abnormal job execution |It is recommended to operate only in the EMR console |
|Performing shutdown, restart, deletion, or specification modification operations on cluster nodes within the VKE cluster |Abnormal cluster state |It is recommended to operate only in the EMR console |
|Do not delete Pods that come with the EMR system on VKE cluster nodes, such as emr\-agent, job\-agent, emr\-controller, promethous, and other service processes used by EMR to manage big data components |Cluster services may become unavailable or billing features may malfunction |It is recommended to operate only in the EMR console |
|Do not set the EMR cluster Master node password too simply |It may be vulnerable to malicious attacks from other users |It is recommended to use a key pair |
|Do not directly modify component configuration file parameters on VKE cluster nodes |After the service restarts, the modified parameters may be overwritten |Please log in to the EMR console to make modifications |
|Do not arbitrarily modify or delete files or directories not related to business operations |This may cause running jobs to fail |None |
|Do not unbind or replace the security group bound to ECS nodes while the cluster is running |Cluster unavailable |None |
|Do not delete the TOS bucket used by the EMR cluster |Some cluster features may become unavailable, such as access links |None |
|Do not delete the public IP associated with VKE used by the EMR cluster |Some cluster features may become unavailable, such as access links not opening |None |
|When creating a cluster and selecting the Hive service, if metadata is set to "Volcano RDS", each cluster must select a separate RDS MySQL database. Do not allow multiple clusters to share the same RDS MySQL |None |It is recommended to use different RDS MySQL databases |
|When the cluster is in an abnormal state, you can contact Volcano Engine technical support personnel by [submitting a ticket](https://console.volcengine.com/workorder/create/). After obtaining your authorization, technical support personnel will log in to the EMR cluster for troubleshooting. Fees will still be charged during the EMR cluster's abnormal period. |None |None |
|Do not perform operations such as modifying basic environment information or upgrading the software stack version on VKE cluster nodes |Cluster status, engine basic features, and integration capabilities may become abnormal and unavailable |None |


<span id="5af00bfb"></span>
# Data recovery and accidental deletion prevention configuration note

When using TOS object storage in the EMR environment, to mitigate irreversible risks caused by unintended deletion, you must enable the corresponding security protection features based on the bucket type.


* Flat Bucket: You must enable [version control](https://www.volcengine.com/docs/6349/261963). After enabling, delete operations will only generate a "Delete Marker," and historical version data will remain, ensuring version rollback is possible after accidental deletion.

* Hierarchical Bucket: You must enable [Recycle Bin](https://www.volcengine.com/docs/6349/1458171). After enabling, files or directories deleted via the FileSystem delete method or commands such as hadoop rm will be moved to the Recycle Bin and provide a grace period within the configured retention period. If not enabled, data will be physically deleted directly.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">It is recommended to configure according to the above content. If protection is not enabled, any deletion operation will result in permanent data loss.</div>
