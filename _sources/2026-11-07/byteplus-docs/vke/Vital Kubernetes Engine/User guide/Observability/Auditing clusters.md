---
title: "Auditing clusters"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Cluster-auditing"
---

VKE supports recording operations performed within clusters through API Server audit logs, helping cluster administrators perform security audits of cluster actions to ensure that clusters run securely and stably. This topic describes how to configure the cluster audit feature.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* TLS has been activated. To activate this service, log in to the [TLS console](https://console.byteplus.com/tls) and activate the service based on the on\-screen prompts.

* (Optional) A log project has been created. For details, see [Log projects](https://docs.byteplus.com/en/docs/tls/Managing_projects).


<span id=".5byA5ZCv6ZuG576k5a6h6K6h"></span>
## Enable cluster audit


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**.

3. On the Cluster page, click the name of the target cluster.

4. In the left navigation bar of the cluster management page, click **Cluster audit**.

5. Click **Enable cluster audit**. In the dialog box, configure logging settings.

   
   |Parameter |Description |
   |---|---|
   |Log usage type |Select the method for saving cluster audit logs, including:<br><br><br>* **Use existing log projects**: Use an existing log project to save cluster audit logs.<br><br>* **Automatically create new log projects**: Create a new log project for saving cluster audit logs. |
   |Project |Specify the log project to which logs belong. The log project allows you to manage operation and maintenance, authorization, and other actions on cluster resources at the project level. By default, the **default** project is selected. For more details, see [Project management](https://docs.byteplus.com/en/docs/vke/Project-management). |
   |Log project |If you set **Log usage type** to **Use existing log projects**, select a log project where you want to save audit logs.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The VKE cluster automatically creates a log topic within the specified log project. You do not need to manually create one.</div><br> |
   

6. Click **Confirm**.


<span id=".5p-l55yL5a6h6K6h5pel5b-X"></span>
## View audit logs

After the cluster audit feature is configured, you can view its logs on the **Cluster audit** page.

<span id=".5pu05o2i5pel5b-X6aG555uu"></span>
## Change the log project

You can change the log project specified in your cluster inspection configuration. To do so, follow the steps below:


1. On the cluster inspection page, click **Change log project** in the upper\-right corner.

2. In the **Log project** drop\-down menu, select the new log project.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Changing the log project for cluster inspection will also change the log project for control plane add\-ons (such as kube\-apiserver and kube\-scheduler). Exercise caution when you perform this operation. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Collecting-control-plane-add-on-logs">Control plane add\-on logging</a>.   </div>
   

3. Click **Confirm**.


<span id=".5YWz6Zet6ZuG576k5a6h6K6h"></span>
## Disable cluster audit

You can disable the cluster inspection feature. To do so, follow the steps below:


1. On the cluster inspection page, click **Disable cluster audit** in the upper\-right corner.

2. In the confirmation dialog box, click **Confirm**.
