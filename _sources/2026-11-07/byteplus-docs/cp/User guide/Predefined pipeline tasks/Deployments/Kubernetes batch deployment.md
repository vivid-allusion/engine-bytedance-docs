---
title: "Kubernetes batch deployment"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/A_staged_rollout_in_Kubernetes"
---

The Code Pipeline preset Kubernetes batch deployment task allows users to configure deployment strategies, enabling instance\-based batch rolling deployment of applications on Kubernetes clusters and ensuring a more controlled release process.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Clusters awaiting deployment have been connected. For detailed actions, see [Deploy resource](https://docs.byteplus.com/en/docs/cp/Deploy_resource_management).

* Caution: If the target image is private, ensure that credentials are set or passwordless authentication is configured before deploying the cluster. For container service configuration, refer to [Configure a secrets dictionary](https://docs.byteplus.com/en/docs/vke/Creating-a-Secret) and [Configure a passwordless component](https://docs.byteplus.com/en/docs/vke/Pulling-private-images-to-create-workloads-by-using-cr-credential-controller#.5q2l6aqk5LiA77ya5a6J6KOF5YWN5a-G57uE5Lu2).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limit


* Repeated deployment is not supported while the target application is being deployed. For example, if pipeline A is deploying the deployment\-a application, any deployment task for the deployment\-a application initiated by pipeline B will automatically fail.

* The target image address cannot be exactly the same as the original image address. Please modify at least the version number in the target image address. The image address is used to distinguish between different images. If the target image address is exactly the same as the original image address, the application's image will not be updated.


<span id=".5re75Yqg5Lu75Yqh"></span>
## Add a task

When creating or editing a pipeline, go to the **Process Orchestration** tab, click **Add Job**, and the **Add Job** drawer will pop up. Select task template **Deploy \> Kubernetes batch release**.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter descriptions

The following describes the parameters of this preset task.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Kubernetes batch release tasks do not support adding other steps.</div>



|Configuration Item |Descriptions |
|---|---|
|Task name |By default, releases are performed in batches using Kubernetes, and custom task names are supported. |
|Upstream tasks |Display the names of upstream serial tasks for the current task. Shown when there is no upstream task`-`。 |
|deploy resource |Select clusters that have been connected and are pending deployment. |
|Namespace |Select or enter the namespace for the application to be deployed. |
|Service name |Select or enter the target Service for Kubernetes batch release.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is optional. In v1, use Service to associate multiple Deployment versions to ensure a smooth and reliable service release process. The v2 version achieves batch deployment by controlling the ratio of new and old ReplicaSets in a Deployment, and no longer relies on this parameter.</div><br> |
|Application types |Settings for the type and name of the workload to be deployed<br><br><br>* Select a workload type The supported workload types are Deployment, StatefulSet, DaemonSet, and CronJob.<br><br>* Select or enter a workload name. If you enter the name manually, it must match the name you used when you created the workload. |
|Container name |Select or enter the specific Container name to be deployed. If there are multiple Containers in the Pod, make sure to upgrade the corresponding image. |
|Image |Set the target image address to deploy. Images generated from upstream artifacts or images you have prepared in advance are supported; please select as needed.<br><br><br>* **Upstream artifact**: Select the output of a preceding image packaging task as the target image.<br><br>* **Custom**: Enter the image address prepared in advance as the target image. Example image address: `xxx.com/ns/nginx:v1`. |
|Deployment strategies |Configure the deployment strategy for batch release tasks, which includes three parameters: rolling batches, batch ratio, and wait time.<br><br><br>* **Rolling batch**: A batch defined for a staged release strategy. After each batch is released, the workflow enters a waiting state and requires manual confirmation to continue deployment.<br><br>* **Batch release ratio**: Configure the ratio for each batch release. The proportion of the last batch is automatically calculated after the previous batches are adjusted and cannot be modified. The sum of the proportions must be 100%.<br><br>   Number of instances × batch ratio = number of instances upgraded in each batch. If the result is not an integer, round down. Any remaining instances will be upgraded in the final batch.<br><br>   For example, if 10 instances are deployed in 3 batches with batch ratios of 30%, 30%, and 40%, then the number of instances deployed in each batch will be 3, 3, and 4, respectively.<br><br>* **Waiting time**: Set the maximum waiting time for manual confirmation. If the waiting period expires without manual confirmation of whether to continue the deployment or roll back, the deployment is considered failed, and the system automatically triggers rollback actions to the version prior to the upgrade. |
|Task outputs |This preset task does not produce any artifacts. |
|Advanced settings |**Webhook notification**: Supports sending task\-level messages via Webhook to help you stay informed about task updates in a timely manner. |


<span id=".5Y-R5biD6L-H56iL"></span>
## The release process

During the execution of Kubernetes batch release tasks, after each batch is released, the pipeline pauses and requires manual confirmation within the allowed time to confirm whether to continue deployment. If manual confirmation is not received within the waiting period, the deployment is considered failed, and the system automatically triggers a rollback to revert to the version prior to the upgrade.


* Continue: End waiting and continue deploying the next batch according to the user's batch configuration.

* Rollback immediately: End waiting. All instances will be rolled back to the pre\-upgrade version.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If a batch release task fails to run, the system will automatically roll back to the previous version.</div>


<span id=".6YOo572y6K-m5oOF"></span>
## Deployment details

The following section introduces the details displayed in the pipeline after the preset task is completed.

On the current pipeline run details page, click the title of the Kubernetes batch release card to view run logs, task details, task configuration, deployment details, and other information.


* Run log: Displays the run log of the task in real time.

* Task details: Display batch groups and the deployment results for each batch.

* Task configuration: Displays the configuration parameters for this task. For more information, see the parameter descriptions above.

* Deployment details: Real\-time display of the instance lists for both current and previous versions, including instance name, running status, and start time. All new version instances are in the running state, indicating a successful release.
