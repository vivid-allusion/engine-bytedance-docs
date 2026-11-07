---
title: "Baseline inspection"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Baseline-inspection"
---

Baseline inspection is based on industry security standards and requirements, primarily targeting worker nodes in Kubernetes clusters. It provides security inspection for cluster nodes, enabling timely detection of insecure configurations in cluster nodes and advising users to remediate them to prevent exploitation by attacks. This helps ensure stability and security of applications.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The security\-scan add\-on for application inspection has been installed in the cluster. This add\-on enables application baseline inspection within the cluster. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

<span id=".6YWN572u56uL5Y2z5beh5qOA"></span>
## Configuring immediate inspections

Manually trigger a baseline inspection immediately. You can use the following steps to perform an immediate inspection:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar, choose **Security** \> **Baseline inspection**. Then, click **Immediate inspection**.

5. In the **Immediate inspection** dialog box, confirm the relevant information for the inspection task.

6. Click **Confirm** to start the inspection.


<span id=".6YWN572u5ZGo5pyf5beh5qOA"></span>
## Configuring periodic inspections

Configure baseline inspection tasks to periodically run at a fixed time every month or week. You can use the following steps to configure periodic inspection:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar, choose **Security** \> **Baseline inspection**. Then, click **Periodic inspection settings**.

5. In the **Periodic inspection settings** dialog box, read the inspection configuration tips and enable **Periodic inspection**.

   The inspection cycle can be **Weekly** or **Monthly**. You also need to configure a specific point of time.

6. Click **Confirm** to save the periodic inspection configuration.


<span id=".5p-l55yL5beh5qOA6K-m5oOF"></span>
## Viewing inspection details


1. In the left navigation bar, choose **Security** \> **Baseline inspection**.

2. On the **Baseline inspection** page, click the name of a completed baseline inspection to view inspection details.

3. On the **Node list** page, view the inspection status of all nodes in the cluster.

   * Click **Inspection Details** to view inspection details for a single node.

   * Click **Re\-inspection** to perform a re\-inspection on a single node.

4. To view detailed information about the inspection items for a node, click **Details** in the **Actions** column.
