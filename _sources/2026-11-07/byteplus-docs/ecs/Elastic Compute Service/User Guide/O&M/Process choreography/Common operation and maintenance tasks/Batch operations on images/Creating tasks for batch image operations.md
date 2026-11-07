---
title: "Creating tasks for batch image operations"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Creating_a_batch_actions_image_tasks"
---

You can use Orchestration to batch create custom images or batch distribute images for multiple existing instances (copy images and share images). For more information about image definition, fees, and limits, see [Image overview](https://docs.byteplus.com/en/docs/ecs/Image-overview).

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have completed [preparations](https://docs.byteplus.com/en/docs/ecs/Preparation).

* If you want to create Linux images, you have already [cleared the Cloud-Init configuration](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Linux-instance#.5q2l6aqk5LqM77ya5riF6ZmkQ2xvdWQtSW5pdOmFjee9rg==).

* If you want to create Windows images, you have already [cleared the network interface information](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Windows-instance#.5q2l6aqk5LqM77ya5riF55CG572R5Y2h5L-h5oGv).


<span id=".5L2_55So6ZmQ5Yi2"></span>
## Limits


|Feature/Parameter |Limit |
|---|---|
|Send a remote command (**optional**) |Send remote commands only to instances with the cloud assistant Agent installed. For more information, see [Installing cloud assistant Agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client). |
|Share an image (**optional**)<br><br> |* You can share custom images with main accounts only. <br><br>* Do not include data that is not suitable for public disclosure in an image. After an image is shared, the receiving account can access the data stored in the image. |
|Copy an image (**optional**)<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">This feature is in Beta. If you need a trial, contact your account manager.</div><br> |You can copy a custom image in the following regions:<br><br><br>* China (Shanghai)(cn\-shanghai)<br><br>* China (Beijing)(cn\-beijing)<br><br>* China (Guangzhou)(cn\-guangzhou)<br><br>* China (Hong Kong) (cn\-hongkong) |


<span id=".5pON5L2c6K-05piO"></span>
## Usage note


* When you create custom images, the system automatically creates the relevant snapshots. Before you delete the snapshots, you need to first delete the associated images.

* When you create custom images from instances running the Linux system, make sure that the '/etc/fstab' configuration file does not contain any data volume configuration information. Otherwise, instances created by using the custom images cannot start as expected. For more information, see [fstab configuration of Linux instances](https://docs.byteplus.com/en/docs/ecs/Linux_instance_fstab_configuration_repair_solution).

* The region of a new image is the same as the region of the instance for which the image is created. For more information, see [Operation instructions](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Windows-instance#.5pON5L2c6K-05piO).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure 


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left\-side navigation pane, click "Maintenance & Monitoring \> Orchestration".

3. In the top menu bar, select the region where your business is located.

4. On the "CloudOps Orchestration" page, click the "Common tasks" tab.

5. Click the "Batch operations on images" menu.

6. Click the "Create task" button and configure the parameters described in the following table.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |**Select task type** |||
   |Type |Select the type of O&M command that you want to execute. The default type is "Create image". |Creating images |
   |**Select instances** |||
   |Select instances<br><br> |Determine target instances that meet batch operation requirements based on information such as instance name or ID, running status, and instance type. You can select multiple instances.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">You can select up to 100 instances at the same time.</div><br> |\-<br><br> |
   |**Fill in the image information** |||
   |Edit<br><br> |After you select an instance, the "Image Name", "Image type", and ["Project"](https://docs.byteplus.com/en/docs/ecs/Managing-projects) parameters are automatically generated. You can modify the parameters based on your business requirements. You can also add a description and [tag](https://docs.byteplus.com/en/docs/ecs/Tag-overview) to the image.<br><br>Image type:<br><br><br>* System volume image: A custom image that contains only the data from the system volume.<br><br>* Whole Image: A custom image that contains data from both the system volume and data volumes. For more information, see [Whole image operation instructions](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Linux-instance#.5pON5L2c6K-05piO). |\-<br><br> |
   |Copy All<br><br> |Use a parameter of an instance as a template to modify this parameter for all selected intances at the same time. All parameters except for the "Instance name/ID" parameter support "Copy All". The modification procedure is the same across parameters. For example, to copy the image tag, perform the following steps:<br><br><br>1. After you select an instance, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_350f608bd5e35fb599c1fde9ed4a0679.png) </span> icon in the "Image tag" column of the instance.<br><br>2. Click the "Copy All" button to save your modification. ||
   |Copy up/Copy down<br><br> |Use a parameter of an instance as a template to modify this parameter for all instances above or below this instance at the same time. All parameters except for the "Instance name/ID" parameter support "Copy up" and "Copy down". The modification procedure is the same across parameters. For example, to copy the image type, perform the following steps:<br><br><br>1. After you select the target instance, click the <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e8fcf56bfe662685db5f3a0b19997403.png) </span> icon in the "Image type" column of the instance.<br><br>2. Click the "Copy up" or "Copy down" button to save your modification. ||
   |**Send a remote command (optional)**  |||
   |Remote command setup<br><br> |Execute relevant commands inside the instance by delivering scripts. For example, you can execute a specific command to view the IP address. Supported:<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Commands can only be sent to instances running the same type of operating system. For example, Linux commands must be sent to Linux instances. Otherwise, the task will fail as the commands cannot be executed.</div><br><br><br><br>* **Enable**: If you select "Enable remote command sending", you can send remote commands by using "Linux Shell", "Python", "Windows Bat", or "Windows PowerShell". For detailed instructions, see [Batch operations on instances](https://docs.byteplus.com/en/docs/ecs/Creating_a_batch_actions_instance_task#.5pON5L2c5q2l6aqk).<br><br>* **Do not enable (default)** : If you do not select "Enable remote command sending", remote commands will not be sent. |\-<br><br> |
   |**Image distribution (optional)**  |||
   |Target region<br><br> |Select the target region. This parameter is required when you want to copy the images (source custom images) and their configurations to another region, for purposes such as cross\-region deployment of ECS instances and cross\-region backup of data.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The target region must be different from the source region.</div><br> |China (Beijing)<br><br> |
   |Image sharing account<br><br> |Enter the IDs of the receiving accounts. Separate multiple account IDs with Enter keys.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Each image can be shared with up to 50 main ,Byteplus accounts.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you no longer want to share an image with an account, you can <a href="https://docs.byteplus.com/en/docs/ecs/Sharing-or-canceling-sharing-image#.5Y-W5raI5YWx5Lqr6ZWc5YOP">cancel image sharing</a> on the image list page.</div><br> |210005\*\*\*\*<br><br> |
   |**Concurrency control** |||
   |Concurrency rate |* Specify the number of concurrent executions for a batch instance task, which refers to the maximum number of instances that can undergo operations or receive requests at the same time. For example, if you have 50 instances and set this parameter to 10, the task will be executed in 5 batches, and commands will be sent to 10 instances simultaneously in each batch.<br><br>* Value range: 1\-100. |10 |
   |Maximum error count |When specifying batch image tasks to execute within a particular operation or range, the maximum allowable number or percentage of errors is set.<br><br><br>* **Error count:**  Generally applicable to scenarios focusing on error count, with a range of 0\-100.<br><br>   * If the error count is set to 0, no errors are allowed. That is, if an error occurs even once while performing a task, the entire task will stop (fail).<br><br>   * If the error count is set to 100, a maximum of 100 errors is allowed. That is, as long as the number of errors during the execution of a task does not exceed 100, the task will succeed, but if errors exceed 100 before the task is completed, the entire task will stop (fail).<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The next step is allowed to proceed only when the actual number of failures across all batches of the task is less than or equal to the maximum number of errors you specify.      </div><br>      <br><br>* **Percent: ** Applicable to scenarios where the impact of errors on the entire task needs attention. Value range: 0\-100%.<br><br>   * If the maximum error percent is set to 0%, no errors are allowed. That is, if an error occurs even once while performing a task, the entire task will stop (fail).<br><br>   * If the maximum error percent is set to 100%, the task will succeed regardless of the number of errors.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The next step is allowed to proceed only when the actual failure rate (percentage of failed instances) across all batches of the task is less than or equal to the maximum error rate (percentage) you specify.      </div><br>       |Error quantity: 1<br><br> |
   |**Relevant Information** |||
   |Project |You can add the Cloud assistant to a project and manage it uniformly by project dimension, conducive to maintaining resource independence and ensuring data security. For more information about projects, see [Project management](https://docs.byteplus.com/en/docs/ecs/Managing-projects). |default |
   |Tag |A tag is a key\-value pair used to identify cloud resources. Tags help you categorize resources based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your resources. For more information about tags, see [Tags](https://docs.byteplus.com/en/docs/ecs/Tag-overview). |Key1:Value1 |
   

7. Click the "Create" button.

8. After you confirm that the configuration information is correct, click the "Confirm" button to start task execution.

   > * The selected task is executed on the selected instances, which has a wide\-ranging impact. Confirm that all information is correct before you submit the request.

   > * The time required to create custom images depends on the actual sizes of the system volumes. Be patient.


<span id=".5ZCO57ut5q2l6aqk"></span>
### Subsequent steps

After the task is **successfully executed**, you can perform the following operations:


* You can view the image status in the custom image list. If the status of a custom image is **Available**, the custom image is created. For more information, see [Viewing image creation results](https://docs.byteplus.com/en/docs/ecs/Creating-custom-images-from-a-Linux-instance#.5pON5L2c57uT5p6c).

* (**Optional**) If an image you create has been shared with other accounts, you can view the shared image with the "Shared" tag in the custom image list.

* (**Optional**) If an image you create has been copied to another region, you can view information about the image copy task in the target region. For example, if you copy a custom image from the China (Guangzhou) region to the China (Beijing) region, you need to go to the China (Beijing) region to view the task information.
