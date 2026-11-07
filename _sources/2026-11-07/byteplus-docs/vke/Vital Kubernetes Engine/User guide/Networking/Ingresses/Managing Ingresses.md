---
title: "Managing Ingresses"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing-Ingresses"
---

If Ingresses have already been created or added to the cluster, you can manage them on the cluster's Ingress page. This topic describes the scenarios, impacts, and steps for managing Ingresses.

<span id=".5pu05paw6Lev55Sx6KeE5YiZ"></span>
## Updating Ingresses

VKE allows you to update Ingresses. After you update an Ingress, the new Ingress settings take effect. To do so, follow the steps below:


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview) **,**  and in the left navigation bar, select **Cluster**.

2. Click the target cluster that you want to configure. In the left\-side navigation bar, click **Services and Ingresses** \> **Ingress**.

3. In the Ingress list, select the Ingress you want to update, click `...` in the **Actions** column, and select **Update** from the dropdown menu.

4. Modify the specific configuration of the Ingress. For details, see the configuration documentation for the corresponding Ingress type.


<span id=".57yW6L6R6Lev55Sx6KeE5YiZLXlhbWw="></span>
## Editing Ingress YAML

You can modify the Ingress configuration by editing the YAML file. Procedure:


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview), and in the left navigation bar, select **Cluster**.

2. Click the target cluster that you want to configure. In the left\-side navigation bar, click **Services and Ingresses** \> **Ingress**.

3. In the Ingress list, select the Ingress you want to edit, click `...` in the **Actions** column, then select **Edit Yaml** from the drop\-down menu.

4. In the pop\-up window, edit the YAML file. Click **Confirm**.


<span id=".5a-85Ye66Lev55Sx6KeE5YiZ"></span>
## Exporting Ingresses

You can export the YAML file of an Ingress to save the Ingress configuration locally. Procedure:


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview) **,**  and in the left navigation bar, select **Cluster**.

2. Click the target cluster that you want to configure. In the left\-side navigation bar, click **Services and Ingresses** \> **Ingress**.

3. In the Ingress list, select the Ingress you want to export, click `...` in the **Actions** column, then select **Export** from the drop\-down menu.

4. The YAML file is downloaded to your computer.


<span id=".5Yig6Zmk6Lev55Sx6KeE5YiZ"></span>
## Deleting Ingresses

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>



* <div data-tips="true" data-tips-type="danger">Deleting an Ingress will also delete all configurations under this Ingress.  This action cannot be undone. Please proceed with caution.</div>


* <div data-tips="true" data-tips-type="danger">Deleting a CLB Ingress will also delete the associated CLB instance.</div>



You can delete an Ingress. Procedure:


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview), and in the left navigation bar, select **Cluster**.

2. Click the target cluster that you want to configure. In the left\-side navigation bar, click **Services and Ingresses** \> **Ingress**.

3. In the Ingress list, select the Ingress you want to delete, click `...` in the **Actions** column, then select **Delete** from the drop\-down menu.

4. A confirmation dialog appears. Click **Delete** to delete the Ingress.
