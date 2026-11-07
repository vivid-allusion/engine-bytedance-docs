---
title: "Notice of minor kernel version upgrade for Milvus for VectorDB"
product: "Milvus for VectorDB"
product_code: "Milvus_for_VectorDB"
source: "https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Notice_of_minor_kernel_version_upgrade_for_Milvus_for_VectorDB"
---

To continuously improve the security, stability, and service reliability of Milvus for VectorDB, we recently enhanced the Milvus kernel with security reinforcements and minor version optimizations. To ensure your instances consistently benefit from the latest security features and stability improvements, we recommend completing the corresponding Milvus major version kernel minor version upgrade as soon as possible.

<span id="gsyHYs4p"></span>
## Upgrade scope

This upgrade applies to the following Milvus instance versions:


* Instances currently using **Milvus version 2.5**: please upgrade to the **latest minor version in the Milvus 2.5 series**.

* Instances currently using **Milvus version 2.6**: please upgrade to the **latest minor version in the Milvus 2.6 series**.


This upgrade involves a minor version update within the same major version and does not include cross\-major version upgrades.

<span id="Mt1puevX"></span>
## Upgrade background

This upgrade mainly addresses security reinforcement requirements and includes kernel stability and performance optimizations. After the upgrade, the instance will receive the latest security enhancements and issue fixes within the version series, helping reduce potential security risks and improve the stability of online service operation.

<span id="0vjg6A0Y"></span>
## Upgrade impact

The upgrade operation triggers a rolling restart of the instance. During the upgrade, the instance can continue read and write access, but a few requests may time out or fail. To minimize business impact, it is recommended that you:


* Perform the upgrade during off\-peak traffic periods;

* Complete data backup before the upgrade;

* Assess the retry mechanism and fault tolerance strategy on the business side in advance;

* Avoid making other instance changes during the upgrade.


<span id="5ZgT74Gv"></span>
## Upgrade procedure

Log on to the [Milvus for VectorDB console](https://console.byteplus.com/milvus) and initiate the version upgrade at the "Kernel version" field on the instance details page. For the procedure, see [Upgrade instance kernel version](https://docs.byteplus.com/en/docs/Milvus_for_VectorDB/Upgrade_kernel_version?lang=en).

If the "Version upgrade" entry does not appear after the instance kernel version, it means the current instance is already at the latest minor version of the corresponding version series, and no action is needed.

<span id="hIN9lbiz"></span>
## Precautions


* Only Dedicated instances support kernel version upgrades.

* The upgrade process cannot be canceled once started.

* You can continue read and write operations during the upgrade, but other changes cannot be made.

* Manually backup data before upgrading.

* The upgrade duration depends on factors such as instance specification and number of nodes, with each node generally requiring a short time.

* During the upgrade, a small number of requests may time out or fail; make sure your business systems are prepared for retries and fault tolerance.


Thank you for supporting Milvus for VectorDB. If you encounter any issues during the upgrade process, contact [technical support](https://console.byteplus.com/workorder/create?step=1) or your account manager promptly for assistance.
