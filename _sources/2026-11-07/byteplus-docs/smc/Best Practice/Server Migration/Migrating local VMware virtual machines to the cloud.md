---
title: "Migrating local VMware virtual machines to the cloud"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Migrate-VMware-to-the-cloud"
---

Due to the hardware resource constraints of your local physical hosts, virtual machines created via VMware have low availability and scalability. You can use SMC to quickly migrate local virtual machines to the BytePlus platform without downtime. This leverages cloud services with high availability and elasticity.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* A virtual machine has been created via VMware.

   > This practice uses a CentOS 7.9 image to create a virtual machine, which has a graphical user interface (GUI) pre\-installed. To install a GUI manually, refer to [Installing graphical interface on Linux](https://docs.byteplus.com/en/docs/ecs/Install-a-GUI-in-Linux).   
   

* Your BytePlus platform account and migration source must meet the requirements in the [Limits](https://docs.byteplus.com/en/docs/smc/Limits).

* You have completed [preparations](https://docs.byteplus.com/en/docs/smc/Preparations). It is recommended to [install a password plugin](https://docs.byteplus.com/en/docs/ecs/Installing-the-password-plug-in) on the virtual machine.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

<span id=".5q2l6aqk5LiA77ya5L2_55SoQWdlbnTlr7zlhaXov4Hnp7vmupA="></span>
### Step 1: Use Agent to import the migration source


1. Log in to the VMware virtual machine.

2. Select "Applications \> System Tools" and click "Terminal" to start the command line tool.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_29c64a4db0f652c217fafd8eec6dff1e.png) </span>

   1. Confirm whether the network, SELinux, and rsync of the virtual machine meet the migration requirements. For migration requirement details, refer to [Preparations](https://docs.byteplus.com/en/docs/smc/Preparations).

      * Execute the following command to check the rsync version. The version must be 3.1.0 or above.

         ```Plain Text
         rsync -version
         ```
         

         Example:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea7b8611f69561410b86071b3d1a76ec.png) </span>

      * Execute the following command to view the SELinux status. It must be in `disabled` status. If SELinux is not disabled, refer to [Disabling SELinux](https://docs.byteplus.com/en/docs/smc/Disable_SELinux) to complete the disabling process.

         ```Plain Text
         sestatus
         ```
         

         Example:

         <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_74e9bf6122c188bfb6c7758a69076835.png) </span>

      * Execute the following command to verify whether the virtual machine can connect to SMC over the public network.

         If the connection fails, check the public network configuration of the migration source, or configure a proxy server as follows to enable proxy\-based access. For detailed operations, see [Creating and starting migration jobs](https://docs.byteplus.com/en/docs/smc/Server-Migration-Task).

         ```Plain Text
         ping smc.byteplusapi.com
         ```
         

      * Make sure that the virtual machine has the Virtio driver installed according to the guidance in the [solution](https://docs.byteplus.com/en/docs/smc/checkVirtioInstall-failed-or-Check-initramfs-failed).

   2. Execute the following commands to download the migration tool Agent.

      ```Plain Text
      sudo wget -O smc-agent_Linux_amd64.tar.gz https://smc.tos-ap-southeast-1.bytepluses.com/smc-agent_Linux_amd64.tar.gz
      sudo tar -zxvf smc-agent_Linux_amd64.tar.gz
      ```
      

   3.  **(Optional)**  Exclude files that do not need to be migrated.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">You can exclude files or folders that do not need to be migrated only when performing "File replication" migrations.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Enter the relative path of the file relative to the mount point of its parent directory in the excludes.txt file. For example, if the absolute path of a file is /etc/test.txt, enter test_file.txt.      </div>
      

   4. Execute the following command, enter the access key AK/SK as instructed, and run the migration tool Agent.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">For instructions on obtaining an access key (AK), refer to <a href="https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-an-accesskey">Managing an access key</a>.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the Access Key ID and Secret Access Key you entered are incorrect or you need to update the key configuration, delete the AK and SK values in the user_cfg.json file and rerun the migration tool Agent.      </div>
      

      ```Plain Text
      sudo ./smc_manage start
      ```
      

   5. Execute the `tail -f smc.log` command to view the `SourceId` (migration source ID) and Agent running logs.


<span id=".5q2l6aqk5LqM77ya6L-B56e75LiK5LqR"></span>
### Step 2: Migrate to the cloud


1. Log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

2. In the top menu bar, select the region where the target instance is located, and in the left directory tree, select "Server Migration Center \> Migration Source".

3. Use the `SourceId` (migration source ID) obtained from the Agent logs to query the target migration source.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_aae0a94daf6ea3a9657440d2cdd84bff.png) </span>

4. Click the "Create migration task" button in the "Actions" column and enter the task information.

   > In this practice, data will be migrated to a BytePlus ECS instance via block\-based replication over the public network. Additionally, automated incremental data synchronization will be executed every 24 hours. For more migration configuration instructions, see [Creating and starting migration tasks](https://docs.byteplus.com/en/docs/smc/Server-Migration-Task).   
   

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Do not disable the migration Agent before the migration task is completed. Otherwise, the migration source will lose connectivity to the SMC console, preventing the migration from finishing.   </div>
   

5. Click "Confirm" to complete the creation.

6. Once the task is created, it will start immediately. You can view the task progress and log information in the ECS console or virtual machine.


<span id=".5q2l6aqk5LiJ77ya5p-l55yL6L-B56e757uT5p6c"></span>
### Step 3: View migration result


1. After migration starts, log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance).

2. In the top menu bar, select the region where the target instance is located, and in the left directory tree, select "Server Migration Center \> Migration Job" to view the task progress and result.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8aa3d2b6f2075f7262955fa7324591c5.png) </span>

3. After migration, you can log in to the [ECS console](https://console.byteplus.com/ecs/region:ecs+cn-beijing/instance) and use the login password/key pair of the VMware virtual machine to log in to the destination ECS instance.
