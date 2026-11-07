---
title: "Before Use"
product: "Cloud Search"
product_code: "cloudsearch"
source: "https://docs.byteplus.com/en/docs/cloudsearch/Before-Use"
---

Before using the Cloud Search service, it is recommended that you first understand what you need to pay attention to in the production environment to avoid problems.

<span id="e7c83f24"></span>
## Single\-node instances are prohibited in production environments

Single\-node instance is only suitable for testing scenarios.

Single\-node instance for testing scenarios, if you need to use it for production, it is recommended to upgrade to 3 nodes or more. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/cloudsearch/upgrading).

<span id="7385d918"></span>
## Two\-nodes instances are prohibited in production environments

The risk of split brain exists in the case of using two nodes, and the cloud search service prohibits the opening of such instances.

<span id="384c4ca4"></span>
## 1C4GiB nodes are prohibited in production environments

1C4GiB nodes are suitable for testing scenarios.

Instances in the production environment are prohibited from using 1C4GiB nodes. Such small\-sized instances are prone to CPU overload or OOM. If such a small\-sized test instance needs to be converted to formal production use, it is recommended to upgrade the node to a 2C4GiB or above specification. For more information, refer to [Upgrading instance specifications](https://docs.byteplus.com/en/docs/cloudsearch/upgrading).

<span id="f86d6465"></span>
## 0 replica index is not recommended in production environments

Index setting 0 replica, if there is a node offline, the index will turn red, and the index query data will be incomplete and the write will be blocked until the offline node is reconnected to the cluster and the cluster turns green again.

0 replica index is generally only suitable for testing scenarios. If the 0 replica index in the test environment needs to be converted to formal production use, it is recommended to modify the replica number of the index to 1 or more, that is, 1 master and N slaves (N≥1).

<span id="de404fed"></span>
## Disk capacity exceeds 80% is not recommended in production environments, and recommended to configure alarm rules

Disk capacity in production environment needs to reserve a certain capacity safety threshold, it is recommended that the total disk capacity of single\-node and cluster should not exceed 80%, and it is recommended to keep it below 50%.

In addition, it is recommended that you configure alarms for disk capacity to avoid data write failures caused by disk capacity thresholds. How to configure alarms, please refer to [Configuring alarm rules](https://docs.byteplus.com/en/docs/cloudsearch/alarm-rules).
