---
title: "How do I modify the specification of the CLB instance associated with the API server during cluster creation?"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/How-do-I-change-the-instance-type-of-the-CLB-instance-automatically-created-during-cluster-creation"
---

To modify the specification of the CLB instance associated with the API server during cluster creation, go to the [CLB console](https://console.byteplus.com/clb).

<span id=".5p-l55yLLWFwaS1zZXJ2ZXIt5YWz6IGU5Yib5bu655qELWNsYg=="></span>
## Viewing the CLB instance associated with the API server


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Cluster**. On the page that appears, find the target cluster and click the name of the cluster.

3. On the **Overview** tab of the **Overview** page for the cluster, view the CLB instance associated with the API server in the **Cluster API Server configuration** section.

4. Click the name of the CLB instance that corresponds to the **Load balancer** parameter to go to the details page of the CLB instance in the [CLB console](https://console.byteplus.com/clb).


<span id=".5L-u5pS5LWFwaS1zZXJ2ZXIt5YWz6IGU5Yib5bu655qELWNsYi3op4TmoLw="></span>
## Modifying the instance type of the CLB instance associated with the API server

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This method applies only to CLB instances associated with API servers. However, it does not apply to CLB instances associated with Ingresses and Services.</div>



1. On the **Overview** tab of the details page for the CLB instance, disable **Modification Protection** in the **Instance property configuration** section.

2. In the upper\-right corner of the instance details page, click the `...` icon and click **Manage instance configuration** \> **Change Instance Configuration** to change the CLB instance type. For detailed operations and parameter descriptions, see [Changing instance types](https://docs.byteplus.com/en/docs/clb/CLB-instances-03).
