---
title: "Kubernetes image upgrade"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Kubernetes_image_upgrade"
---

Code Pipeline provides the **Kubernetes image upgrade** task, enabling users to upgrade images for existing applications in the cluster.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background Information

The upgrade strategy for the **Kubernetes image upgrade** task depends on the update strategy you set for the Deployment to be deployed. For example, when upgrading the image of a Deployment in a BytePlus container service cluster, where the Deployment has eight instances, the update strategy in the container service is set to rolling update, with a maximum unavailable of 25 percent and a maximum surge of 25 percent. During image upgrades, a rolling update strategy will be used. Throughout the upgrade process, the number of unavailable instances will not exceed two, and a maximum of ten instances, including both old and new versions, may coexist simultaneously.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Clusters to be deployed have already been connected. For detailed actions, see [Access deployment resources](https://docs.byteplus.com/en/docs/cp/Deploy_resource_management).

* If you use a custom image, please prepare in advance the deployment address of the target image.

* Caution: If the target image is a private image, make sure to set the key or configure a passwordless component before deploying the cluster. When configuring container services, refer to [Configuring the secret dictionary](https://docs.byteplus.com/en/docs/vke/Creating-a-Secret) and [Configuring the passwordless component](https://docs.byteplus.com/en/docs/vke/Pulling-private-images-to-create-workloads-by-using-cr-credential-controller#.5q2l6aqk5LiA77ya5a6J6KOF5YWN5a-G57uE5Lu2).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* Repeated deployment is not supported while the target application is being deployed. For example, while pipeline A is deploying the deployment\-a application, any deployment task for deployment\-a initiated by pipeline B will automatically fail.

* The target image address cannot be exactly the same as the original image address. At a minimum, modify the version number of the target image. The image address is used to distinguish between different images. If the target image address is exactly the same as the original image address, the application's image will not be updated.


<span id=".5re75Yqg5Lu75Yqh"></span>
## Add a task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. Select a task template **Kubernetes image upgrade**.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter descriptions

Configure the Kubernetes image upgrade task as required.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The Kubernetes image upgrade task does not support adding other steps.</div>



|Configuration Item |Descriptions |
|---|---|
|Task name |The default is Kubernetes image upgrade; custom task names are supported. |
|Upstream tasks |Display the names of upstream serial tasks for the current task. Displayed when no upstream tasks exist`-`。 |
|deploy resource |Select clusters that have been connected and are pending deployment. |
|Namespace |Select or enter the namespace for the workload to deploy. |
|Application types |Identify the type and name of the workload to be deployed.<br><br><br>* Select a workload type. The supported workload types are Deployment, StatefulSet, DaemonSet, and CronJob.<br><br>* Select or enter a workload name. If you enter it manually, it must match the name you used when you created the workload. |
|Container name |Select or enter the specific Container name to be deployed, and make sure to upgrade the corresponding image if there are multiple Containers in the Pod. |
|Image |Set the target image address. You can use images generated from upstream artifacts or images you have prepared in advance; please select as needed.<br><br><br>* **Upstream artifact**: Select the output of a previous image packaging task as the target image.<br><br>* **Custom**: Enter the address of a pre\-prepared image to use as the target image. Example of an image address: `xxx.com/ns/nginx:v1`. |
|Timeout duration |Set automatic timeout period. If the task runtime exceeds the specified time, the deployment is considered to have failed, and the system automatically triggers a rollback action, reverting to the version prior to the upgrade. |
|Task outputs |Display the current task's outputs Displayed when there are no products`-`。 |
|Advanced settings |**Webhook notification**: Enables you to receive task notifications via Webhook, helping you stay up to date with task activity. |


<span id=".5Y-R5biD6L-H56iL"></span>
## The release process


* During the image upgrade process, the task card displays the **Rollback now** button, allowing you to revert to the version prior to the upgrade at any time.

* If the image upgrade task fails, the system will automatically trigger a rollback to the previous version.


<span id=".6YOo572y6K-m5oOF"></span>
## Deployment details

The following section describes the details displayed in the pipeline after the preset task is completed.

On the run details page of the current pipeline, click the title of the Kubernetes image upgrade card to view the run log, task configuration, deployment details, and other information.


* Run log: Displays the run log for this task in real time.

* Task configuration: Displays the configuration parameters for this task. For details, refer to the parameter description above.

* Deployment details: Real\-time display of instance list information for both old and new versions, including instance name, running status, and start time. All new version instances being in the Running state indicates that the upgrade was successful.
