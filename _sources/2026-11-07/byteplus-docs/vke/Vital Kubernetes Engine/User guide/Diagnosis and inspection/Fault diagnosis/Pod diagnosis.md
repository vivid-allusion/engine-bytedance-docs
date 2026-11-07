---
title: "Pod diagnosis"
product: " Vital Kubernetes Engine"
product_code: "vke"
source: "https://docs.byteplus.com/en/docs/vke/Pod-diagnosis"
---

Cluster diagnosis helps you identify risks in various resources within VKE clusters, such as node pools, nodes, and pods. This topic describes how to configure the pod diagnosis feature.

<span id=".6YWN572u6K-K5pat"></span>
## Configuring diagnosis


1. Log in to the [VKE console](https://console.byteplus.com/vke).

2. In the left navigation pane, click **Cluster**. Click the target cluster name to go to the management page of this cluster.

3. In the left navigation pane, click **Diagnosis**. On the page that appears, click **Create diagnosis task** to configure a Pod diagnostic task.

   
   |Parameter |Description |
   |---|---|
   |Diagnosis type |Specify the type of resource to be diagnosed. For this example, select **Container group**. |
   |Namespace |Select the namespace where the pod is located. |
   |Pods |In the **All container groups** list on the left side, select the pods on which you need to perform diagnosis, and add them to the **Select container groups** list on the right side. |
   

4. Click **Confirm** to complete the configuration. The system will start the diagnosis and generate a diagnostic report.


<span id=".5p-l55yL6K-K5pat57uT5p6c"></span>
## Viewing diagnostic results

After the diagnostic task is complete, if it is in the **Anomaly** state, it indicates that risks exist in the pod. You can click **View details** in the **Actions** column that corresponds to the target diagnostic task to view the diagnostic report.

The diagnostic result will display all diagnostic items, including successful, failed, and warning ones. You need to view these items on the **Pending** tab and resolve the issues.

<span id=".5LiL6L296K-K5pat5oql5ZGK"></span>
## Downloading diagnostic reports

After the diagnostic task is complete, you can download the diagnostic report in PDF format.


1. After the diagnostic task is complete, click **View details** in the **Actions** column that corresponds to the target diagnostic task to view the diagnostic result.

2. Click **Download the report** in the upper\-right corner to download the diagnostic report in PDF format.


<span id=".6K-K5pat6aG56K-05piO5ZKM5L-u5aSN5bu66K6u"></span>
## Diagnostic item descriptions and Fix suggestions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The diagnostic items slightly vary based on different pod types, such as pods and elastic pods. The diagnostic items displayed in the console shall prevail.</div>


<span id=".cG9kLei0n-i9vQ=="></span>
### Pod load


|Diagnostic item |Check content |Fix suggestions |Reference |
|---|---|---|---|
|Pod memory utilization |Check whether the pod memory utilization is greater than 85%. Excessive memory load may cause OOM errors, which affect normal business operations. |Increase the number of pod instances or configure autoscaling. |* [Managing workloads](https://docs.byteplus.com/en/docs/vke/Managing-Deployments)<br><br>* [Creating HPA](https://docs.byteplus.com/en/docs/vke/Creating-a-Horizontal-Pod-Autoscaler) |
|Pod CPU utilization |Check whether the Pod CPU utilization is greater than 80%. Excessive CPU load may cause CPU preemption, which affects normal business operations. |||


<span id=".cG9kLeeKtuaAgQ=="></span>
### Pod status


|Diagnostic item |Check content |Fix suggestions |Reference |
|---|---|---|---|
|Pod container image download failures |Check whether the pod image is downloaded. |Check the status and logs of the pod. |* [Viewing pod information](https://docs.byteplus.com/en/docs/vke/Viewing-pod-details)<br><br>* [Workload image download failures](https://docs.byteplus.com/en/docs/vke/Why-is-the-pod-status-always-displayed-as-ContainerCreating-after-a-workload-is-created) |
|Pod initialization status |Check whether the pod is initialized as expected. |Check the status and logs of the pod. |[Viewing pod information](https://docs.byteplus.com/en/docs/vke/Viewing-pod-details) |
|Pod scheduling status |Check whether the pod can be scheduled as expected. |Determine the reason why the pod cannot be scheduled, such as insufficient resources and node affinity. |[Viewing pod information](https://docs.byteplus.com/en/docs/vke/Viewing-pod-details) |
|Pod container restart statistics |Check the number of times that the pod restarts. Frequent restarts indicate abnormal pod operation. |Check the status and logs of the pod. |[Viewing pod information](https://docs.byteplus.com/en/docs/vke/Viewing-pod-details) |
|Whether the image cache is available |Enable the image cache feature and check whether it is ready. It can be in the following abnormal status:<br><br><br>* **Warning**: Image cache is not used.<br><br>* **Abnormal**: Image cache is used, and all image caches are unavailable. |Check whether the image cache is in a normal status. If you encounter an issue, [submit a ticket](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000210) for processing. |[Image cache](https://docs.byteplus.com/en/docs/vke/VCI-Image-Cache) |
|Validity of pod container image Secrets |Check whether the Secret that is configured when the pod pulls images by using the password\-free add\-on is valid. If the Secret is invalid, the pod will be unable to pull images by using the secret\-free add\-on. |Check the status and logs of the pod. |[Creating workloads by pulling private images with the secret-free add-on](https://docs.byteplus.com/en/docs/vke/Pulling-private-images-to-create-workloads-by-using-cr-credential-controller) |
