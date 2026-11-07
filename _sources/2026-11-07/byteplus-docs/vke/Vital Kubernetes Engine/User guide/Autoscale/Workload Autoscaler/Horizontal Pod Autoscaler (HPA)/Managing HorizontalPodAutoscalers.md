---
title: "Managing HorizontalPodAutoscalers"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing-Horizontal-Pod-Autoscalers"
---

You can manage an existing HorizontalPodAutoscaler (HPA) on the HPA page in the VKE console. This topic describes the scenarios, impacts, and procedures of HPA\-related operations.

<span id=".5pu05paw5oyH5qCH5Ly457yp"></span>
## Updating HPA

You can update the configuration of an HPA. After an update is complete, the new HPA configuration takes effect. To do so, follow the steps below:


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Cluster**.

3. Click the name of the target cluster. In the left navigation bar, click **Autoscaling** \> **HPA**.

4. In the HPA list, select the HPA to be updated, and in the **Actions** column, click `...` \> **Update**.

5. Modify the configuration items of the HPA as needed. For details, see [Creating HPAs](https://docs.byteplus.com/en/docs/vke/Creating-a-Horizontal-Pod-Autoscaler).

6. Click **Confirm** to finish configuration.


<span id=".57yW6L6R5Ly457yp5oyH5qCHLXlhbWw="></span>
## Editing HPA YAML

You can modify an HPA by editing its YAML content. To do so, follow the steps below:


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Cluster**.

3. Click the name of the target cluster. In the left navigation bar, click **Autoscaling** \> **HPA**.

4. In the HPA list, select the HPA to be modified, and in the **Actions** column, click `...` \> **Edit Yaml**.

5. In the pop\-up window, edit the YAML file.

6. Click **Confirm** to finish configuration.


<span id=".5a-85Ye65Ly457yp5oyH5qCH"></span>
## Exporting an HPA configuration

You can export the YAML file of an HPA by following the steps below:


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Cluster**.

3. Click the name of the target cluster. In the left navigation bar, click **Autoscaling** \> **HPA**.

4. In the HPA list, select the HPA to be exported, and in the **Actions** column, click `...` \> **Export**.

5. The file will be downloaded to your computer.


<span id=".5Yig6Zmk5Ly457yp5oyH5qCH"></span>
## Deleting HPA

You can delete an HPA. To do so, follow the steps below:


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. In the left navigation bar, click **Cluster**.

3. Click the name of the target cluster. In the left navigation bar, click **Autoscaling** \> **HPA**.

4. In the HPA list, select the HPA to be deleted, and in the **Actions** column, click `...` \> **Delete**.

5. Click **Delete** in the confirmation dialog box.
