---
title: "Managing pods"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Managing-pods"
---

You can perform operations on created pods based on your business requirements, such as updating and deleting pods. This topic describes how to manage pods.

<span id=".5pu05paw5a655Zmo57uE"></span>
## Updating a Pod

You can modify the configurations of a created pod by using the console or a YAML file.


1. Go to the pod management page.

   1. Log in to the [VKE console](https://console.byteplus.com/vke).

   2. In the left navigation bar, click **Cluster**.

   3. On the Cluster page, click the name of the target cluster.

   4. In the left navigation bar of the cluster management page, click **Workload** \> **Pod**.

2. In the **Actions** column that corresponds to the target pod, click `...` \> **Edit Yaml**.

   For details about configuration information in the YAML file, see [Creating pods](https://docs.byteplus.com/en/docs/vke/Creating-a-pod).

3. After the configurations are updated, click **Confirm**.


<span id=".5p-l55yL55uR5o6n"></span>
## Viewing monitoring data

You can be quickly redirected to the Cloud Monitor console in VKE console to view the monitoring data of pods.


1. Go to the pod management page.

   1. Log in to the [VKE console](https://console.byteplus.com/vke).

   2. In the left navigation bar, click **Cluster**.

   3. On the Cluster page, click the name of the target cluster.

   4. In the left navigation bar of the cluster management page, click **Workload** \> **Pod**.

2. In the **Actions** column that corresponds to the target pod, click `...` \> **View monitoring**.

3. View pod monitoring data on the monitoring page. For a description of container\-related metrics, see [Cloud service metrics](https://docs.byteplus.com/en/docs/cloudmonitor/Cloud-service-metrics).

4. After the configurations are updated, click **Confirm**.


<span id=".5a-85Ye65paH5Lu2"></span>
## Exporting files

You can quickly export the YAML file of a pod in the console.


1. Go to the pod management page.

   1. Log in to the [VKE console](https://console.byteplus.com/vke).

   2. In the left navigation bar, click **Cluster**.

   3. On the Cluster page, click the name of the target cluster.

   4. In the left navigation bar of the cluster management page, click **Workload** \> **Pod**.

2. In the **Actions** column that corresponds to the target pod, click `...` \> **Export** to export the YAML file to your on\-premises computer.


<span id=".5Yig6Zmk5a655Zmo57uE"></span>
## Deleting pods

You can delete pods based on your business requirements.

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">After you delete a pod, the service may become unavailable. Proceed with caution.</div>



1. Go to the pod management page.

   1. Log in to the [VKE console](https://console.byteplus.com/vke).

   2. In the left navigation bar, click **Cluster**.

   3. On the Cluster page, click the name of the target cluster.

   4. In the left navigation bar of the cluster management page, click **Workload** \> **Pod**.

2. Delete a pod or multiple pods at the same time.

   * **Delete a pod**

      After you select a namespace on the **Pod** page, find the pod that you want to delete and click `...` \> **Delete** in the Actions column.

   * **Delete multiple pods at the same time**

      After you select a namespace on the **Pod** page, select the names of multiple pods, and click **Delete** below the pod list.

3. In the message that appears, click **Delete** to delete the pod.


<span id=".5pWF6Zqc6K-K5pat"></span>
## Diagnostics Pod

Pod diagnostics can help users identify potential risks in pods within the VKE cluster, such as high pod load and abnormal pod status.


1. Go to the pod management page.

   1. Log in to the [VKE console](https://console.byteplus.com/vke).

   2. In the left navigation bar, click **Cluster**.

   3. On the Cluster page, click the name of the target cluster.

   4. In the left navigation bar of the cluster management page, click **Workload** \> **Pod**.

2. In the **Actions** column that corresponds to the target pod, click `...` \> **Diagnosis**.

3. You are redirected to the **Diagnosis** page to configure the diagnostics task for the pod. For details, see [Pod diagnostics](https://docs.byteplus.com/en/docs/vke/Pod-diagnosis).


<span id=".55m75b2V5a655Zmo57uE"></span>
## Logging in to pods

You can quickly log in to a pod to perform interactive operations in a container.


1. Go to the pod management page.

   1. Log in to the [VKE console](https://console.byteplus.com/vke).

   2. In the left navigation bar, click **Cluster**.

   3. On the Cluster page, click the name of the target cluster.

   4. In the left navigation bar of the cluster management page, click **Workload** \> **Pod**.

2. Click the name of the target pod to go to the **pod details page**.

3. In the upper right corner of the **pod details page**, click **Console** to log in to the container for interactive operations.

   You can also execute the `kubectl exec -it {your_container_name} -- /bin/bash` command in the cluster to perform interactive operations.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">To precisely control the access permissions of users or roles on the pods, you can use the Identity and Access Management (IAM) service to define access control policies to prohibit unauthorized access. For details, see <a href="https://docs.byteplus.com/en/docs/vke/Access_control_based_on_IAM_for_VKE_console">Access control based on IAM for VKE console</a>.   </div>
