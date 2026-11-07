---
title: "Best practices of cluster upgrade "
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cluster-upgrade-best-practices"
---

This article mainly introduces recommendations for actions and precautions at each stage when upgrading a cluster.

<span id=".5Zy65pmv5LuL57uN"></span>
## scenario introduction

Kubernetes is a powerful container orchestration platform, widely used for the deployment and management of cloud\-native applications. With the rapid development of Kubernetes, new versions are continuously released, bringing more features and performance improvements. Vital Kubernetes Engine (VKE) ensures the stable operation of the three most recent minor Kubernetes versions. Clusters running outdated versions may be exposed to security and stability risks. Therefore, to maintain the continuity of your business, it is recommended to upgrade your cluster version in a timely manner. This documentation provides recommendations for actions, precautions, and more related to upgrading the Kubernetes version, helping you upgrade the Kubernetes version of the cluster or node pool to the latest version safely and efficiently. For more information about upgrade policies and the principles of cluster upgrades, refer to [Kubernetes version support policy](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-support-policy), [Cluster upgrade](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The cluster is in **running** status, and an upgradable Kubernetes version is available.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Considerations


* During the process of upgrading the Kubernetes version of the cluster control plane, applications on the cluster will not be interrupted; however, if applications strongly depend on the API Server, there may be a brief impact.

* Upgrading the node Kubernetes version will impact business Pods running on the node. During the upgrade process, it may cause Pod Prober and Lifecycle Hook failures, and in\-place Pod restarts may also occur. Therefore, before the upgrade, you need to check whether the cluster is in a healthy state and whether its business operations are performed during off\-peak hours. This helps you determine whether to start upgrading nodes.

* Cluster upgrade does not support rollback, please proceed with caution.

* To validate the upgrade feature, start with the test environment if you have multiple environments (for example, test environment, pre\-release environment, and production environment). After successful validation in multiple environments, upgrade the cluster in the production environment as the final step.

* When you consecutively upgrade the minor version of Kubernetes for the same cluster, we recommend that you perform an upgrade at an interval of more than 24 hours to ensure stable cluster operation. For example, after you upgrade the cluster control plane from Kubernetes v1.20 to v1.24 and the cluster has stably run for 24 hours, upgrade the cluster to v1.26.


For more precautions when upgrading a cluster, refer to [Upgrade cluster](https://docs.byteplus.com/en/docs/vke/Upgrading-a-cluster).

<span id=".5YmN572u5YeG5aSH"></span>
## Preparation

<span id=".56Gu5a6a5Y2H57qn5pe26Ze056qX5Y-j"></span>
### Confirm upgrade time window

Select the off\-peak period based on the cluster size and business characteristics, and determine the upgrade time window by referring to the following explanation:


* First perform a control plane upgrade, then perform a node upgrade as needed.

* Control plane upgrade takes 5–10 minutes.

* When upgrading multiple nodes simultaneously, the system automatically upgrades the selected nodes in batches according to the number of parallel upgrades. Upgrading a single node or a single batch of nodes takes approximately 3 minutes.

* After verifying that the upgrade is successful in the test/pre\-release environment, reserve a 2\-hour time window for the cluster upgrade in the production environment, including 1 hour for the upgrade and 1 hour for monitoring.


<span id=".56Gu5L-d5Lia5Yqh6LSf6L295omT5pWj"></span>
### Ensure business workloads are distributed

Since the containerd and kubelet components are restarted during node upgrade, workloads in the cluster that are configured with readiness probes (Readiness Probe) and liveness probes (Liveness Probe) may have containers in a NotReady state during this period. It is recommended to configure multiple replicas for the workload and set Pod topology spread constraints or Pod anti\-affinity so that the replicas are distributed across different nodes. When performing a node upgrade, upgrade these nodes in separate batches.

This article uses the ingress\-nginx add\-on as an example. After installing this add\-on, it will be deployed in the cluster's **kube\-system** namespace as a Deployment named **ingress\-nginx\-controller**. For instructions on installing addons, refer to [Install addons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

Configure topology spread constraints in the `spec.template.spec` field of the corresponding YAML file for **ingress\-nginx\-controller**, so that when the number of nodes meets the requirements, Pods are distributed across nodes in different availability zones as much as possible. The following is a sample code snippet:

```yaml
  topologySpreadConstraints:
  - labelSelector:
      matchLabels:
        app.kubernetes.io/name: ingress-nginx
    maxSkew: 1
    topologyKey: kubernetes.io/hostname
    whenUnsatisfiable: ScheduleAnyway
  - labelSelector:
      matchLabels:
        app.kubernetes.io/name: ingress-nginx
    maxSkew: 1
    topologyKey: topology.kubernetes.io/zone
    whenUnsatisfiable: ScheduleAnyway
```


<span id=".6YWN572u55uR5o6n5ZGK6K2m"></span>
### Configure alerts and monitoring

Deploy monitoring and alerting addons within the cluster, for example, install the [Prometheus-agent](https://docs.byteplus.com/en/docs/vke/prometheus-agent) monitoring addon and configure the workspace, to promptly monitor whether key metrics become abnormal during the addon upgrade process. For more information about cluster monitoring, refer to [Cluster monitoring](https://docs.byteplus.com/en/docs/vke/Monitoring-overview).

<span id=".5byA5ZCv6ZuG576k5a6h6K6h"></span>
### Enable cluster audit

Enable the cluster audit feature in the [Vital Kubernetes Engine Console](https://console.byteplus.com/vke) to record users' daily actions in the cluster through API Server audit logs, helping cluster administrators perform security audits of users' actions in the cluster and ensuring the cluster operates safely and stably. For more information about cluster audit, refer to [the Cluster audit](https://docs.byteplus.com/en/docs/vke/Cluster-auditing).

<span id=".5o6n5Yi26Z2i5Y2H57qn"></span>
## Upgrade the control plane

This document uses the example of upgrading the cluster's current Kubernetes version from v1.24 to v1.26 to introduce the procedures for upgrading the cluster control plane and nodes, as well as the precautions to be observed during the upgrade process.

<span id=".5q2l6aqk5LiA77ya5piO56Gu6ZuG576k54mI5pys"></span>
### Step 1: Specify cluster version


1. Log in to [Vital Kubernetes Engine (VKE) console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the cluster list page, click the target cluster.

4. On the **Overview** page of the target cluster, confirm that the cluster's current Kubernetes version (control plane version) is `v1.24.15-vke.21`.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_dcebda4f6296b41ffe2ba5cbd55c824b.png) </span>


<span id=".5q2l6aqk5LqM77ya5o6n5Yi26Z2i5Y2H57qn5qOA5p-l"></span>
### Step 2: Control plane upgrade check


1. In the left navigation bar of the cluster management page, click **Cluster upgrade**.

2. On the **Cluster upgrade** page, click the **Kubernetes upgrade check** tab to run the pre\-upgrade check.

3. Click **Control plane upgrade check**, and confirm that the target version is the minor version  and `v1.26.10-vke.18`.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_3d1b5a55dcf7827affd6d42ff05008b7.png) </span>

4. Click **Confirm** to start the control plane Kubernetes upgrade pre\-check.

5. According to the results of the control plane upgrade check, fix the check items that did not pass, and for warning items, choose to fix or skip them based on the actual situation. For more explanations and fix suggestions regarding upgrade check items, please refer to [Cluster upgrade check items](https://docs.byteplus.com/en/docs/vke/Cluster_upgrade_checks).

   The abnormal **check items** in the control plane inspection report for this example are as follows:

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_da406d74b6f3281a069f0ba1c9d552e9.png) </span>

   * **Addon component compatibility check**: Indicates that the ingress\-nginx addon version in the cluster is too low, and the addon must be upgraded before upgrading the cluster. This item is a **failed** check item, and must be handled to ensure the check item passes.

   * **Audit log removal of k8s API check**: Indicates that there are deprecated Kubernetes API resources in the cluster, so these resources need to be processed. This item is a **Warning** check item. Based on your actual business situation and judgment, you may choose to skip the **Warning** during the official upgrade.

6. Address any issues found in the upgrade check results. Once processing is complete, perform the control plane upgrade check again until all upgrade check results pass.

   1. Upgrade ingress\-nginx Addon to the latest version. For detailed operations, refer to [Upgrading add-on](https://docs.byteplus.com/en/docs/vke/Upgrading-an-add-on).

   2. Confirm which services in the cluster have used deprecated Kubernetes API resources, and independently assess the impact on the cluster and workloads. To ignore this warning if there is no impact; to upgrade the Kubernetes resources in the Service to the new Version if there is an impact. For detailed descriptions of resource changes and deprecations, see [Kubernetes version release notes](https://docs.byteplus.com/en/docs/vke/Kubernetes-version-release-notes).

   3. Click **Control plane upgrade check** again, confirm the upgrade version details, then click **Confirm** to perform the control plane upgrade check.


<span id=".5q2l6aqk5LiJ77ya5o6n5Yi26Z2i5Y2H57qn5pON5L2c"></span>
### Step 3: Control plane upgrade actions


1. On the **Cluster upgrade** page, click the **Kubernetes upgrade** tab. Then, click **Control plane upgrade**.

2. In the **Control plane Kubernetes upgrade** dialog box, check the upgrade information.

3. Click **Confirm upgrade** to upgrade the control plane.

   During the upgrade process, please do not perform any actions on the cluster. Click **actions** in the right column, then **view details** to view the control plane Kubernetes upgrade progress. At the same time, observe business monitoring and check for any unexpected abnormal conditions among Pods within the cluster.

4. When the job status on the cluster upgrade page is observed as **Pass**, check the cluster **Overview** page to confirm that the cluster status is **Running** and the Kubernetes version is the target versions  and v1.26.10\-vke.18. The node Kubernetes version has not yet been upgraded and remains at the old versions  and v1.24.15\-vke.21. At this time, the cluster control plane upgrade is complete.


<span id=".6IqC54K55Y2H57qn"></span>
## Upgrade nodes

<span id=".5q2l6aqk5LiA77ya6YCJ5oup5Y2H57qn6IqC54K5"></span>
### Step 1: Select node to be upgraded


1. When selecting nodes to upgrade, ensure that the nodes hosting traffic\-sensitive business Pods are placed in different upgrade batches.

   In this example, the Pods of **ingress\-nginx\-controller** have been distributed across different nodes. Therefore, when selecting nodes for upgrade, the two nodes hosting these Pods are divided into two batches for upgrade, with `192.168.4.7` corresponding to **node\-xptzps**, which is included in the first batch to be upgraded.

2. The remaining nodes are designated as the second batch for upgrade.


<span id=".5q2l6aqk5LqM77ya6IqC54K55Y2H57qn5qOA5p-l"></span>
### Step 2: Node upgrade check


1. On the **Cluster upgrade** page, select the **Kubernetes upgrade check** tab. Click **Node upgrade check**.

2. On the **Node upgrade check** page, select the upgrade target version, check the nodes or node pools to be upgraded, and then click **Confirm** to start the node upgrade pre\-check.

   In this example, at the node level, the node **node\-xptzps** corresponding to Node IP `192.168.4.7` is individually selected to perform a node upgrade check.

3. Confirm that the node upgrade check for **node\-xptzps** has passed, then select the remaining nodes in batch to perform node upgrade checks.

4. After all remaining nodes have passed the node upgrade check, prepare to perform the node upgrade.

   If there are check items with **Fail** or **Warning** status, please click **View details** on the right and handle the failed check items as prompted by the system. After you address the check items, perform the **node upgrade check** again. Make sure that **Pass** is displayed in the **Check status** column before you start upgrading. For more explanations and fix suggestions regarding upgrade check items, please refer to [Cluster upgrade check items](https://docs.byteplus.com/en/docs/vke/Cluster_upgrade_checks).


<span id=".5q2l6aqk5LiJ77ya6IqC54K55Y2H57qn5pON5L2c"></span>
### Step 3: Node upgrade actions


1. On the **Cluster upgrade** page, click the **Kubernetes upgrade** tab.

2. Click **Node upgrade**. On the **Node upgrade** page, check the upgradable nodes. Then click **Confirm** to start the node upgrade.

   In this example, first select **node\-xptzps**, which corresponds to Node IP `192.168.4.7`, to perform a node upgrade.

3. Click **Confirm upgrade**, and then start upgrading the **node\-xptzps** node.

   During the upgrade process, please do not perform any actions on the cluster and node. Click **View details** under the **Actions** column on the right to check the Node Kubernetes upgrade progress, while also monitoring business monitoring and observing whether there are any unexpected abnormal situations with Pods in the cluster.

4. When the upgrade status is shown as Pass on the **Node Kubernetes upgrade progress** page, check the corresponding **Node details page** to confirm that the node status is **Running**, the node's Kubelet version has been upgraded to the target version v1.26.10\-vke.18, and there are no abnormal existing Pods; then the current node upgrade is complete.

5. According to the planned node upgrade schedule, select the remaining nodes in batches for upgrade.

6. On the **Kubernetes upgrade** tab, click **View details** in the **Actions** column to the right of the corresponding upgrade job. In the upgrade details, you can observe that the selected nodes are being upgraded in batches. When the upgrade status of all nodes displays **Pass**, it indicates that all nodes have been upgraded.


<span id=".5Y2H57qn5ZCO5qOA5p-l"></span>
## Post\-upgrade check


1. In the navigation bar on the left side of the Cluster management page, click **Overview**.

2. In the **cluster information** region, check that the cluster status is **Running**, and both the Kubernetes version and node version match the target versions v1.26.10\-vke.18.

3. Check for any obvious abnormalities in business workload monitoring in the cluster. For more details, please refer to [Monitoring Management](https://docs.byteplus.com/en/docs/vke/Cloud-native-observability).

4. Create and delete test Pods. If the Pods can be scheduled and terminated normally, it indicates that the cluster and node upgrade was successful, and that all services within the cluster are operating normally.

5. (Optional) To resolve a business exception that cannot be fixed through monitoring, observability tips, events, logs, or related explanations, you can submit a [support ticket](https://console.byteplus.com/workorder/create) to obtain technical support.
