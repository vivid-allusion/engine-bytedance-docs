---
title: "[Announcements] Patch version upgrade for VKE clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Patch-version-upgrade-for-VKE-clusters"
---

<span id="tFJ2vfSc"></span>
## Background information

In a Kubernetes cluster, when kube\-apiserver starts, a self\-signed certificate is automatically generated. In some earlier Kubernetes versions, the self\-signed certificate is valid for only **one year**. Therefore, when the certificate expires, kube\-apiserver becomes unavailable.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">For more details, see the <a href="https://github.com/kubernetes/kubernetes/issues/86552">community documentation</a>.</div>


To address the preceding issue and ensure the normal operation of your cluster, BytePlus provides a dedicated cluster patch version to reissue the certificate. To help you get the best experience with minimal effort, we strongly recommend that you upgrade your cluster to the latest patch version.


* After the upgrade is complete, the apiserver self\-signed certificate will be valid for **99 ** years.

* The upgrade is fully backward compatible and does not introduce disruptive changes.

* You only need to perform simple operations in the BytePlus console.

* During the upgrade, running workloads and the control plane (such as apiserver and etcd) are not affected.

* During the upgrade, the apiserver restarts in a rolling manner. Long\-lived connections may be briefly interrupted for a few seconds and can be restored by retrying.


<span id="iYgXJMhJ"></span>
## Version description

Select an appropriate patch version for upgrade based on the current version of your cluster.


|**Current version** |**Patch version** |
|---|---|
|v1.20.15\-vke.xx |v1.20.15\-vke.36 and later |
|v1.24.xx\-vke.xx |v1.24.17\-vke.17 and later |
|v1.26.xx\-vke.xx |v1.26.15\-vke.32 and later |


<span id="1O2niJly"></span>
## Procedure


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster to go to the cluster management page.

4. In the left navigation bar, click **Overview**. On the **Overview** tab, find the **Kubernetes version** parameter and move the pointer over the **Upgradable** label.

5. In the pop\-up message, click **Upgrade** to upgrade the current cluster version. This topic takes the upgrade of v1.26 as an example.

6. Select **Patch version v1.26.15\-vke.32** for the **Upgrade target version** parameter. Read **Upgrade check warning**, then select the check box. Click **Confirm upgrade** to perform a pre\-upgrade check on the cluster.


&nbsp;

<div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Note</div>


* <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Make sure that you select the patch version.</div>


   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Upgrading the patch version will not affect running services. However, we recommend that you upgrade the version during off\-peak hours to ensure the secure running of the services.   </div>
   

7. In the left navigation bar of the cluster management page, click **Cluster upgrade**. Click the **Kubernetes upgrade check** tab to check whether the cluster passes the pre\-upgrade check.

   * If the cluster passes the pre\-upgrade check, the cluster will be automatically upgraded.

   * If the cluster fails to pass the pre\-upgrade check, click **View details** in the **Actions** column, then fix the failed items according to the on\-screen instructions. After you address the check items, perform the **control plane upgrade check** again. Ensure **Pass** appears in the **Check status** column before upgrading. For check item descriptions and fixes, see [Cluster upgrade check items](https://docs.byteplus.com/en/docs/vke/Cluster_upgrade_checks).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For more operations and considerations during cluster upgrade, see <a href="https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster">Upgrading clusters</a>.   </div>
