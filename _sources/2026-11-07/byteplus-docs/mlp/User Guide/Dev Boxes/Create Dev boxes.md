---
title: "Create Dev boxes"
product: "Machine Learning Platform"
product_code: "mlp"
source: "https://docs.byteplus.com/en/docs/mlp/Create_Dev_boxes"
---

[Dev boxes] is a module provided by the Machine Learning Platform for online compilation, debugging code and model development for machine learning developers. Dev boxes support online development using WebIDE or remote development via SSH connection to Dev boxes, and also provide persistent cloud storage services and shared file systems for storing data in development. After the Dev boxes are shut down, the platform will release the computing power of the Dev boxes, save the previous operation, downloaded data and configuration environment, etc

<span id="相关概念"></span>
## Related concepts


* Queue

* Mirror image

* Shared file system mount

* Cloud disk


<span id="使用前提"></span>
## Premise of use


* Have 1 or more Dev box queues with a cloud disk capacity of more than 20 GiB


<span id="操作步骤"></span>
## Procedure


1. Log in to the Machine Learning Platform and click [Dev boxes] in the left navigation bar to enter the list page

2. Click [+ Create Dev boxes] at the top left of the list page to enter the creation page.

3. Fill in the relevant parameters on the creation page, the specific parameters are as follows



|Parameter |Parameter Description |
|---|---|
|Task name |* Fill in the name of the Dev boxes, **required** .<br><br>* Supports 1 to 64\-bit visible characters, and only includes uppercase and lowercase letters, Chinese, numbers, dashes, and underscores. |
|Description |* Fill in the appropriate description of the Dev boxes, **optional** .<br><br>* Supports 1 to 200 visible characters. |
|mirror image |* Select the mirror of the Dev boxes, **required** .<br><br>* Supports `preset images`, `custom images`, `BytePlus images`and `public images`(private Container Registry requires a username and key). |
|queue |* Select the queue to create the Dev boxes, **required**.<br><br>* Support `prepaid queues`and `postpaid queues`. |
| | |
| |* Select the appropriate instance specification based on the selected queue, **required**.<br><br>* One type of GPU corresponds to a layer of rich CPU and memory specifications to choose from, providing users with the highest possible flexibility while improving resource utilization. |
|Cloud disk capacity |* The cloud disk capacity required to fill in the Dev boxes is at least 20 GiB. The cloud disk type is Extreme Speed SSD FlexPL, **required**.<br><br>   * Used to store development environment, code, data files that do not need to be shared, etc., the content in the cloud disk will not be lost due to the shutdown and restart of Dev boxes.<br><br>   * When deleting the Dev boxes, the data in the cloud disk will be wiped together and cannot be restored. Please pay attention to the backup of important data.<br><br>   * After creating Dev boxes, it also supports expanding the cloud disk capacity. If the cloud disk capacity in the queue is insufficient, please contact the queue administrator to expand the capacity.<br><br>* For cloud disk performance, please refer to . |
|access configuration |* Select the way to log in to the Dev boxes. If you don't need to log in through SSH, you don't need to fill in the SSH public key. Currently, there are two ways to log in, namely public network login and private network login, **optional** .<br><br>   * Public network login: On any machine connected to the public network, you can use the SSH public network command to log in to the Dev boxes.<br><br>   * Private network login: When you need to log in to the Dev boxes through the SSH private network command, please ensure that the machine entering the login command is in the corresponding private network.<br><br>* Precautions<br><br>   * For security reasons, Dev boxes SSH login only supports public key authentication, not username + password authentication.<br><br>   * Usually fill in the contents of the `~/.ssh/id_rsa.pub`file on the machine that initiates the SSH login. If the file does not exist, it can be generated with the `ssh-keygen`command. When initiating an SSH login, be sure to check whether the private keys are paired.<br><br>   * If you need to initiate SSH login from multiple machines, you can fill in multiple public keys, or you can directly edit the list of public keys in the Dev boxes `~/.ssh/authorized_keys`file. |
|Shared file system mount |* Fill in the file system that needs to be mounted, up to 10 file systems can be mounted, **optional** .<br><br>   * Data in a shared file system will not be lost due to Dev box restarts, shutdowns, or deletions. File system selection and mount method see [Overview](https://docs.byteplus.com/docs/undefined/67e296ece1665f050fa76a8f) |


calculation specification


4. After completing the configuration of the above form, click [Confirm Creation]. The creation process of the Dev boxes will be completed according to the submitted form configuration

5. Dev boxes mainly contain the following states



|Status |Description information |
|---|---|
|Creating |* Dev boxes are creating configuration information |
|Queueing |* Dev boxes are in the queuing process. If the selected queue resources are relatively small, it is recommended to contact the queue administrator to expand the capacity. |
|Deploying |* Dev boxes are in the deployment process, including the following two processes<br><br>   * Create cloud disks and compute instances<br><br>   * Creating a development environment |
|Running |* Dev boxes have been created and are running. Dev boxes can be connected via WebIDE (new version) or SSH |
|Shutdown |* Dev boxes are in the process of shutting down |
|turned off |* Dev boxes turned off<br><br>* The previous operation and environment will not be lost after shutdown, and configuration information such as instance, access, and file system can be modified by editing |
|Deleting |* Dev boxes are being deleted |
|Failed to create |* Dev boxes failed to create<br><br>* When resources are insufficient, the creation will fail. You can try to boot manually or replace a smaller instance. If it still cannot run after many attempts, please contact the platform administrator to deal with it at this time. |
|abnormal |* Dev boxes abnormal |



6. You can switch between [All] and [I created] on the Dev boxes list page to view Dev boxes.

7. After the Dev boxes are created, you can edit the configuration items of the Dev boxes. The configuration can be modified as follows

   * Concept

   * Description

   * Cloud disk capacity (or increase cloud disk capacity through expansion)

   * access configuration

   * Shared file system mount
