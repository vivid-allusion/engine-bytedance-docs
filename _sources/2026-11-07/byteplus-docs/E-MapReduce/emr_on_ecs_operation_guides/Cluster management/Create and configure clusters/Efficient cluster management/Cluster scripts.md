---
title: "Cluster scripts"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Cluster_scripts"
---

After a Volcano Engine E\-MapReduce (EMR) cluster is created, you can use the **cluster scripts** feature to batch select nodes and run specified scripts to meet personalized requirements. For example, installing third\-party software and modifying the cluster runtime environment.

<span id="_1-使用限制"></span>
## Limits


1. Only one cluster script can be executed at a time in the same cluster. If a cluster script is currently running, you cannot submit and execute a new cluster script.

2. The maximum number of cluster scripts that can be added is 20. If you add more than 20 scripts, you cannot add new cluster scripts. You must delete previously added scripts before adding new ones.

3. This feature is only available for clusters that have already been created and are running normally. To run cluster scripts during cluster creation, refer to [Guided operations](https://docs.byteplus.com/docs/E-MapReduce/105420).

4. Ensure that you have enabled the Object Storage Service (TOS) and uploaded the script to TOS. For instructions on enabling TOS, see [TOS Quick Start](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1).

5. User role permission check:

   1. The logged\-in user clicks the user avatar in the upper right corner of the interface to enter the **Access Control \> Roles** page.

   2. Enter **VEECSforEMRRole** in the search box to search for the role. If the role does not exist, click the **Create Role** button to complete role creation.

   3. Click the **VEECSforEMRRole** role name and check whether the role includes permission policies related to ECS and TOS to ensure that EMR can properly read the scripts you uploaded to TOS.

6. Once a cluster script has been executed, it cannot be executed again. Please add a new script.


<span id="_2-注意事项"></span>
## important notes


1. Cluster scripts may fail to run on some nodes, for example, if a node restarts and causes the script to fail. After resolving the exception, you can specify the failed nodes individually to run the script again. After the cluster is expanded, you can also specify the expanded nodes to run the cluster script individually.

2. The cluster scripts will be downloaded from TOS to the specified nodes and executed. If the execution fails, you can log in to each node and check the execution log at `/var/log/clusterscript/<node_name_IP>`. If the cluster is configured with a TOS log directory, the execution log will also be uploaded to the `tos-path/emr/clusterid/log/clusterscript/<node_name_IP>` directory.


<span id="_3-使用集群脚本"></span>
## Using cluster scripts

<span id="_3-1-添加集群脚本"></span>
### Add cluster scripts


1. Log in to the ([E-MapReduce Console](https://console.byteplus.com/emr/region:emr_fe+ap-southeast-1/home?)).

2. In the left navigation bar, click **Resource Management \> on ECS \> Cluster Name** to enter the cluster details page where you need to configure cluster scripts.

3. On the cluster details page, click the **Cluster Script** tab to enter the cluster script configuration page.

4. Click **Add cluster script** on the right side. In the pop\-up window, add the cluster script configuration:

   
   |Parameter |Note |
   |---|---|
   |Script name |Enter a custom script name for easier subsequent management. |
   |Script location |Use the dropdown to select the TOS path where the script is stored. Only Shell execution scripts under the Bucket are displayed here. |
   |Script parameter |Enter the value of the script parameter variable that needs to be referenced in the script. |
   |Execute now |Depending on the actual scenario, you can choose whether to execute the script immediately, or you can click the **Execute** button when needed for your business. |
   |Execution range |Use the dropdown to select the scope for script execution. You can choose the execution scope from the following dimensions: cluster, node group, node instance (single node), or node instance (instance range). |
   

5. After completing the above parameter configuration, click the **Confirm** button to finish adding the cluster script.


<span id="_3-2-集群脚本管理"></span>
### Cluster script management

After the cluster script is created, it will appear in the cluster script list. You can perform the following management operations:


* For cluster scripts that have not been executed, you can click the **Operation** column and then the **Execute** button to manually execute the added cluster script.

* For cluster scripts that are being executed, you can click the **Operation** column and then the **Details** button to view the script's execution status on each node.

* Click the **Operation** column and then the **Delete** button to delete the created cluster script.


<span id="_3-3-脚本示例"></span>
### Script example

You can write the following content in the uploaded script to create folders, decompress archives, install software packages, and perform a series of operations.

```plaintext
#!/bin/bash
mkdir dir
tar -zxvf <myfile>.tar.gz -C /<yourdir>
yum install -y ld-linux.so.2
```


<span id="_4-常见问题"></span>
## FAQs


* **Q1: The EMR bootstrap script execution is interrupted, but there is no error message in the log.** 

   A1: It is recommended to add logging statements at key points in the script to help troubleshoot script execution by reviewing the execution log. The most common causes of cluster script errors currently include the following:

   * Network connectivity issues. The ECS instance and the corresponding TOS must be in the same region. For example, an ECS instance in the Beijing region cannot connect to a TOS outside the Beijing region.

   * ECS failed to obtain AccessKey information. This is usually caused by the ECS instance not being bound to VEECSForEMRRole.

   * The script uses nohup without redirecting output, which will cause the Task to remain unable to exit for an extended period. The correct usage is `nohup ...` `>*** 2>&1`。

   * If the script is edited in a Windows environment, it will contain Windows line break characters, resulting in errors when running the script in a Linux environment. You can check the operation history error log to see if there is a `^M` character. If so, it is recommended to re\-edit the script in a Linux environment and upload it to TOS.

   * Timeout occurred when using the wget command to download the package. Please check whether the ECS node is connected to the public network.

   * The command used was not found. Please check whether the ECS node has installed this command.

* **Q2: EMR bootstrap script execution does not include YARN,HDFS and other commands.** 

   A2: Currently, when EMR management executes cluster scripts, no profile information is included by default. To use YARN, HDFS, and related commands, add `.` `/etc/profile` at the beginning of the script to load it, so you can use the above commands.

* **Q3: The script parameters entered did not take effect.** 

   A3: The parameters entered are separated by spaces. We will sequentially replace the patterns $1, $2, and so on in your script with the parameters you entered. Caution: If your script contains custom functions and the function parameters include patterns such as $1 or $2, these will also be replaced, which may render the function unusable.
