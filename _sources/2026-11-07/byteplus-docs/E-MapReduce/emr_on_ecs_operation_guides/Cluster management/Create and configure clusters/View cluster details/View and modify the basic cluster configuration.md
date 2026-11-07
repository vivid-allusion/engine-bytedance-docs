---
title: "View and modify the basic cluster configuration"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/View_and_modify_basic_cluster_configurations"
---

# Cluster overview

In the **cluster list**, click the **cluster name** in the row of the desired cluster to enter the **Cluster overview** page. The page displays the cluster's basic information, including cluster information, software information, payment information, network hardware, and security information. This article introduces the configurations on the **Cluster overview** page that **support modification**.

# Cluster information

|**Parameter** |**Description** |
|---|---|
|Cluster name |The cluster's name |
|Label |Cluster tags and quantity, used for retrieval and classification. Tag management entry: [Tag management](https://console.byteplus.com/resourcemanager/tag/list). |
|Release protection |A protection switch to prevent the cluster from being accidentally released or deleted. The cluster can only be released after this switch is turned off. |

# Payment information

> **注意**

> Pay\-As\-You\-Go clusters do not display payment information.

|**Parameter** |**Description** |
|---|---|
|Payment type |The cluster's payment type |
|Expiration time |Expiration time of the cluster lease (Subscription) |
|Auto\-renewal |Cluster auto\-renewal switch |

# Software information

|**Parameter** |**Description** |
|---|---|
|Cluster type |The type of cluster, for example, Hadoop. |
|Product version |The EMR product version used by the cluster. |
|Version expiration reminder |Displays the service status of the current version:<br><br>• **Version in normal service**: In the GA phase, more than 180 days from EOM.<br><br>• **Version about to enter the EOM phase**: In the GA phase, less than 180 days from EOM.<br><br>• **Version in the EOM phase**: Already in EOM, more than 180 days from EOS.<br><br>• **Version about to enter the EOS phase**: In the EOM phase, less than 180 days from EOS.<br><br>• **Version in the EOS phase**: Already in EOS.<br><br>For information about the GA, EOM, and EOS phases, see [Lifecycle policy](https://docs.byteplus.com/docs/undefined/6a56fd191222100509b0d1c0). |
|Installed services |Installed services and their corresponding versions. |
|Cluster storage root path |The storage root path used by the cluster. |
|Hive metadata |The storage method for Hive metadata, for example, a built\-in database. |
|Hive root path |The storage root path for Hive data. |

# Security information

|**Parameter** |**Description** |
|---|---|
|Security group name |Security group bound to the cluster, which controls network access rules. |
|Cluster role |Role used by the cluster. The cluster assumes a role to access cloud resources, and access permissions are controlled through the role. |
