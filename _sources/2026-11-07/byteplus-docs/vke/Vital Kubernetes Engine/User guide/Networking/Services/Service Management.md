---
title: "Service Management"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing-Services"
---

The service management page provides a series of options for the management of existing services. The following content will introduce these options in detail.

<span id=".5pu05paw5pyN5Yqh"></span>
## Updating a service

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">Warning</div>


<div data-tips="true" data-tips-type="warning">It is recommended that you update services by <strong>editing YAML</strong> files if you need to convert a LoadBalancer service to another type. Doing it in another way will lead to unreclaimed CLB resources left in the system.</div>


The new Service settings will take effect as soon as they are confirmed on the page. Follow the steps below to update the Service:


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. Select **Cluster** in the left navigation bar, and click the name of the desired cluster.

3. Click **Services and Ingresses** \> **Service** in the left navigation bar.

4. Locate the service you want to update and click `...` in the **Actions** column, then select **Update** from the drop\-down menu.

5. Now make changes as needed to the configurations. For details about the configurations, see [ClusterIP](https://docs.byteplus.com/en/docs/vke/ClusterIP), [NodePort](https://docs.byteplus.com/en/docs/vke/NodePort), and [LoadBalancer](https://docs.byteplus.com/en/docs/vke/Creating-a-LoadBalancer-Service-in-the-console).


<span id=".57yW6L6R5pyN5YqhLXlhbWw="></span>
## Editing the YAML file of a service

Services can be configured by editing YAML files correspondingly. Follow the steps below to edit YAML file of a service:


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. Select **Cluster** in the left navigation bar, and click the name of the desired cluster.

3. Click **Services and Ingresses** \> **Service** in the left navigation bar.

4. Locate the service you want and click `...` in the **Actions** column, and then select **Edit Yaml** from the drop\-down menu.

5. Now make changes as needed to the YAML file in the pop\-up window. Click **Confirm** when you finish.


<span id=".5a-85Ye65pyN5Yqh"></span>
## Exporting a service

The configurations of a service can be saved by exporting it to a YAML file. Follow the steps below to export a service to a YAML file:


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. Select **Cluster** in the left navigation bar, and click the name of the desired cluster.

3. Click **Services and Ingresses** \> **Service** in the left navigation bar.

4. Locate the service you want and click `...` in the **Actions** column, and then select **Export** from the drop\-down menu.

5. The file will be downloaded to your computer.


<span id=".5Yig6Zmk5pyN5Yqh"></span>
## Deleting a service

Services can be deleted anytime if necessary. Follow the steps below to delete a service:


1. Log in to the [VKE console](https://console.byteplus.com/vke/overview).

2. Select **Cluster** in the left navigation bar, and click the name of the desired cluster.

3. Click **Services and Ingresses** \> **Service** in the left navigation bar.

4. Locate the service you want and click `...` in the **Actions** column, and then select **Delete** from the drop\-down menu.

5. Click **Confirm** in the pop\-up window to delete the service.
