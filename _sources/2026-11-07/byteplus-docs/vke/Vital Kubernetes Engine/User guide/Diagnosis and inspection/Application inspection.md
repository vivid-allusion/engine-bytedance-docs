---
title: "Application inspection"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Application-inspection"
---

Application inspection is based on industry security standards and incorporates container security best practices to provide application security inspection capabilities. Application inspection can promptly detect and block unsafe configurations and prompt you to fix these issues to prevent applications from being attacked or exploited. This helps ensure application security and stability.

Application inspection supplements baseline inspection by covering security scanning checks for Kubernetes\-native resources such as Workload, Pod, and ConfigMap, which are not included in baseline inspection. The inspection system helps you identify potential security risks in Kubernetes\-native resources and provides remedy suggestions, effectively enhancing the security of cloud\-native applications in clusters.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Kubernetes resources, such as Workload, Pod, and ConfigMap, have been created in the cluster. For details, see [Workloads](https://docs.byteplus.com/en/docs/vke/Workloads) and [Creating ConfigMaps](https://docs.byteplus.com/en/docs/vke/Creating-a-ConfigMap).

* The application\-inspector add\-on has been installed. For details, see [Installing add-ons](https://docs.byteplus.com/en/docs/vke/Installing-an-add-on).

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you uninstall the add\-on, the system will automatically delete all application inspection data.   </div>
   

<span id=".6YWN572u5beh5qOA562W55Wl"></span>
## Configuring inspection policies

Before performing an inspection, you need to configure an inspection policy.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar, choose **Security** \> **Application inspection**. Then, click **Policy configuration**.

5. In the **Policy configuration** dialog box, configure parameters as needed.

   
   |Parameters |Description |
   |---|---|
   |Periodic inspection |Turn on the switch to perform application inspection at a fixed cycle. For details, see [Configuring periodic inspections](https://docs.byteplus.com/en/docs/vke/Application-inspection). |
   |Inspection item |VKE provides three inspection categories: **Baseline policy**, **Reinforcement policy**, and **Vulnerability mitigation policy**. Each category contains different inspection items. Select inspection items as needed.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The configured inspection items take effect for both <strong>immediate inspection</strong> and <strong>periodic inspection</strong>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When you hover the mouse over a specific inspection item, you can view the policy statement for that inspection item.</div><br> |
   


<span id=".6YWN572u56uL5Y2z5beh5qOA"></span>
## Configuring immediate inspections

Manually trigger an application inspection immediately. You can use the following steps to perform an immediate inspection:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar, choose ** Security** \> **Application inspection**. Then, click **Immediate inspection**.

5. In the pop\-up box, confirm the relevant information for the inspection task.

6. Click **Confirm** to start the inspection.


<span id=".6YWN572u5ZGo5pyf5beh5qOA"></span>
## Configuring periodic inspections

Configure application inspection tasks to periodically run at a fixed time on a specific day of each month or week. You can use the following steps to configure periodic inspection:


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar, choose **Security** \> **Application inspection**. Then, click **Policy configuration**.

5. In the **Policy configuration** dialog box, enable **Periodic inspection** and configure the inspection cycle.

   The inspection cycle can be **Weekly** or **Monthly**. You also need to configure a specific point of time. For information about how to configure **inspection items**, see [Configuring inspection policies](https://docs.byteplus.com/en/docs/vke/Application-inspection).

6. Click **Confirm** to save the periodic inspection configuration.

   After configuration is complete, the system will automatically trigger inspection tasks and generate reports in each inspection cycle. Only the most recent inspection report is retained for application inspection. Remember to view inspection reports before they are removed.


<span id=".5p-l55yL5beh5qOA5oql5ZGK"></span>
## Viewing inspection reports

After an inspection finishes and the inspection report is generated, you can filter results by risk type, resource level or other items.


1. In the left navigation bar, choose **Security** \> **Application inspection**.

2. Filter results by **Risk type** or **Resource level** to view inspection information.

   * To view the result of each inspection item for a resource, find the resource and click **Details** in the **Actions** column.

   * Click **Details** next to the inspection item to view the **policy statement**, **security risk statement**, **fix suggestion**, and **remarks**.
