---
title: "Guided operations"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Guided_operations"
---

Adding bootstrap actions to a Volcano Engine E\-MapReduce (EMR) cluster allows you to install third\-party software you require or modify the cluster runtime environment. This article describes how to add, edit, clone, and delete bootstrap actions.

<span id="_1-使用限制"></span>
## Limits


1. You can add up to 10 bootstrap actions. Bootstrap actions are executed starting from the most recently added one.

2. By default, they are executed using the root account.


<span id="_2-添加引导操作"></span>
## Add bootstrap actions

<span id="_2-1-方式一：在创建集群时添加引导操作"></span>
### Method 1: Add bootstrap actions when creating a cluster


1. When creating a cluster, select the Custom creation option. In Step 3**Other settings \> Advanced settings**, click the "Select **Add script**" button. In the **Add script** dialog box, fill in the following relevant configuration items. For cluster creation steps, refer to [Create clusters (version 3.18.0 and earlier)](https://docs.byteplus.com/docs/E-MapReduce/105456).



|Parameter |Description |
|---|---|
|Script name |Name of the bootstrap operation. |
|Script location |Select the location of the script in TOS. If you have not enabled TOS\-related services, please authorize them first.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>1. <div data-tips="true" data-tips-type="tip">The logged\-in user clicks the user avatar in the upper right corner of the interface to enter the <strong>Access Control \> Roles</strong> page.</div><br><br><br>2. <div data-tips="true" data-tips-type="tip">Enter <strong>VEECSforEMRRole</strong> in the search box to search for the role. If the role does not exist, you need to click the <strong>Create Role</strong> button to complete role creation. For role creation, please refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-roles">Role Management</a>.</div><br><br><br>3. <div data-tips="true" data-tips-type="tip">Click the <strong>VEECSforEMRRole</strong> role name and check whether the role already includes ECS and TOS\-related permission policies to ensure that EMR can properly read the scripts you uploaded to TOS.</div><br><br><br><br>The script path format must be tos://\*\*/\*.sh. |
|Execution parameters |Parameters for the bootstrap operation script, specifying the values of variables referenced in the script. |
|Execution range |* **Cluster**: This bootstrap operation applies to the entire cluster.<br><br>* **Node group**: This bootstrap operation applies to the node group you select. You can choose the names of the MasterGroup, CoreGroup, and TaskGroup (if available) node groups. |
|Execution time |* **Before component deployment**: Execute this script before component deployment.<br><br>* **After component deployment**: Execute this script after component deployment. |
|Failure policy |* **Continue execution**: If this script fails to execute, continue with the next script.<br><br>* **Stop execution**: If this script fails to execute, stop the current script. |


If you add bootstrap actions when creating a cluster, you can view the corresponding steps in the cluster initialization operation log or view the execution status of each bootstrap action individually in the **Cluster Details \>**  **Guided operation** tab.

You can log in to the primary node and check the execution log at `/var/log/bootstap/<node_name_IP>`. If the cluster is configured with a TOS log directory, the operation log will also be uploaded to `tos-path/emr/clusterid/log/bootstrap/<node_name_IP>`.

<span id="_2-2-方式二：创建集群后添加引导操作。"></span>
### Method 2: Add bootstrap actions after creating a cluster.


1. Log in to the [EMR console](https://console.volcengine.com/emr/).

2. In the left navigation bar, click **Cluster Management \> Cluster List \> Cluster Name** to enter the cluster details page where you need to configure bootstrap actions.

3. On the cluster details page, click the **Guided operation** tab to enter the bootstrap action configuration page.

4. On the right, click **AddGuided operation**. In the pop\-up window, fill in the parameters as described in Method 1 above to configure the bootstrap action.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you add bootstrap operations using method two, these bootstrap operations will only be executed on nodes newly created during the scaling operation!</div>


<span id="_3-引导操作脚本管理"></span>
## **Guided operation**Script management

<span id="_3-1-编辑引导操作"></span>
### **Edit bootstrap actions**


1. On the **Guided operation** page, in the row of the bootstrap action to be edited, click the **Operation** column's **Edit** button.

2. In the **EditGuided operation** dialog box, you can modify all configuration items as needed.


<span id="_3-2-克隆引导操作"></span>
### **Clone bootstrap actions**


1. On the **Guided operation** page, in the row of the bootstrap action to be cloned, click the **Operation** column's **Clone** button.

2. In the pop\-up Add **bootstrap operation** dialog box, you can modify all configuration items as needed.


<span id="_3-3-删除引导操作"></span>
### Delete a bootstrap operation


1. On the **Guided operation** page, in the row containing the bootstrap operation to be deleted, click the Delete button in the Operation column (**Operation** column's **Delete** button).

2. In the secondary confirmation dialog, select whether to delete as needed, and click the **Confirm** button to complete the deletion.


<span id="_4-示例"></span>
## Example

You can write the following content in the uploaded TOS script to perform a series of operations such as creating folders, extracting compressed packages, and installing software packages.

```Plain
#!/bin/bash
mkdir dir
tar -zxvf <myfile>.tar.gz -C /<yourdir>
yum install -y ld-linux.so.2
```


<span id="_5-常见问题"></span>
## FAQs


* **Q1: EMR bootstrap script execution is interrupted, but there is no error information in the log.** 

   A1: It is recommended to add logging statements at key points in the script to help you troubleshoot script execution through the runtime logs. The most common causes of errors in cluster scripts currently include the following types:

   * Network connectivity issues. ECS instances and the corresponding TOS must be in the same region. For example, ECS instances in the Beijing region cannot connect to TOS outside the Beijing region.

   * Failure to obtain AccessKey information for ECS. This is usually caused by the ECS instance not being bound to VEECSForEMRRole.

   * The script uses nohup but does not redirect output, causing the task to be unable to exit for a long time. The correct usage is `nohup ...` `>*** 2>&1`。

   * If the script is edited in a Windows environment, it will contain Windows line break symbols, which will cause errors when running the script in a Linux environment. You can check the operation history error log to see if there is a `^M` character. If so, it is recommended to re\-edit the script in a Linux environment and upload it to TOS.

   * If the wget command times out when downloading the package, please check whether the ECS node is connected to the public network.

   * If the command used is not found, please check whether the ECS node has installed this command.

* **Q2: EMR bootstrap script execution does not include YARN, HDFS, and other commands.** 

   A: Currently, when EMR management executes cluster scripts, no profile information is included by default. To use YARN, HDFS, and related commands, add "`. /etc/profile`" at the beginning of the script. Once `/etc/profile` is loaded, you can use the above commands.

* **Q3: The script parameters entered did not take effect.** 

   A3: The input parameters are separated by spaces. We will sequentially replace occurrences in your script with $1, $2, and so on, corresponding to the parameters you provide. Caution, if your script contains custom functions and the parameters within those functions include $1, $2, and similar patterns, these will also be replaced, which may render the function unusable.
