---
title: "Managing applications"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing-applications"
---

This topic describes how to manage Helm applications, including viewing application details, updating applications, deleting applications, and rolling back application versions.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A Helm application has been created. For details, see [Creating Helm applications](https://docs.byteplus.com/en/docs/vke/Creating-a-Helm-application).

<span id=".5p-l55yL5bqU55So5L-h5oGv"></span>
## Viewing application information

After you create a Helm application, you can view the basic information about the application and associated workloads, services, and other resources. You can also view historical versions and parameter configuration information.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Application center \> Helm**.

3. On the **Helm** page, select the project, cluster, and namespace where the application is located to find the target application. Then, click the name of the application.

4. On the **Helm details page**, click the corresponding button in the upper\-right corner to update or delete the application.

   
   |Actions |Description |
   |---|---|
   |Update |You can update only the Chart and Parameter configuration parameters of the Helm application. You cannot update other parameters. For detailed operations, see the [Updating applications](https://docs.byteplus.com/en/docs/vke/Managing-applications#.5pu05paw5bqU55So) section of this topic. |
   |Delete |<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">After you delete the application, related services will be affected and cannot be restored. Proceed with caution.</div><br><br><br>Delete the application and its associated resources. For detailed operations, see the [Deleting applications](https://docs.byteplus.com/en/docs/vke/Managing-applications#.5Yig6Zmk5bqU55So) section of this topic. |
   

5. On the **Helm details page**, click the corresponding tab to view and manage other resources of the Helm application.

   
   |Tab |Description |
   |---|---|
   |Overview |Displays the basic information of the application, as well as the detailed configurations and YAML files of associated workloads, services, and other resources.<br><br>Click the name of the corresponding resource to go to its details page and view more information. |
   |Historical version |Displays all historical versions of the application. In the **Actions** column that corresponds to the version number, click the `...` icon to view the parameter configuration of the version or roll back the application to the version.<br><br>For detailed operations on rolling back applications, see the [Rolling back applications](https://docs.byteplus.com/en/docs/vke/Managing-applications#.5Zue5rua5bqU55So) section of this topic. |
   |Parameter configuration |Displays the parameter configuration of the current version for the application. |
   


<span id=".5pu05paw5bqU55So"></span>
## Updating applications


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Application center \> Helm**.

3. On the **Helm** page, select the project, cluster, and namespace where the application is located to find the target application. Then, click the name of the application.

4. On the **Helm details page**, after you view the application information and confirm the changes, click **Update** in the upper\-right corner.

5. On the **Update Helm** page, update parameters based on the on\-screen prompts.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When you update Helm applications that are deployed through application templates, you can only update <strong>Chart</strong> parameters and the <strong>values.yaml</strong> file. For parameter configuration descriptions, see the parameter descriptions in <a href="https://docs.byteplus.com/en/docs/vke/Creating-a-Helm-application">Creating Helm applications</a>.   </div>
   

6. Click **Confirm** to update the application.


<span id=".5Zue5rua5bqU55So"></span>
## Rolling back applications

After you update the application, you can roll it back to a historical version.


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Application center \> Helm**.

3. On the **Helm** page, select the project, cluster, and namespace where the application is located to find the target application. Then, click the name of the application.

4. On the **Helm details page**, click the **Historical version** tab.

5. In the **Version list** section, find the version to which you want to roll back, and in the **Actions** column, click `...` \> **Roll back**.

6. In the pop\-up message, click **Confirm** to roll back the application to the selected historical version.


<span id=".5Yig6Zmk5bqU55So"></span>
## Deleting applications

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After you delete the application, all associated services will stop and cannot be restored. Proceed with caution.</div>



1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation bar, click **Application center \> Helm**.

3. On the **Helm** page, select the project, cluster, and namespace where the application is located to find the target application. Then, in the **Actions** column that corresponds to the application, click `...` \> **Delete**.

4. In the pop\-up dialog box, select whether to delete resources associated with the application based on your business requirements, and then click **Confirm** to delete the application.
