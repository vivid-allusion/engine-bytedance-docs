---
title: "Mounting with access points and FSX"
product: "FileNAS"
product_code: "nas"
source: "https://docs.byteplus.com/en/docs/nas/Mounting_with_access_points_and_FSX"
---

This topic explains how to mount a file system to an Elastic Compute Service (ECS) instance via an access point when using FSX. This can be done via the EFS console.

<span id="3eH5qdBb"></span>
## Restrictions

The following restrictions apply when mounting a file system to an ECS instance via the EFS console using FSX:


|Category |Description |
|---|---|
|FSX |FSX is only compatible with certain operating systems. For a list of supported operating systems, see [Operating environment](https://docs.byteplus.com/en/docs/nas/Choosing_the_right_client#GJtg9kNe). |
|ECS instance |* Both the ECS instance and the access point must be located within the same virtual private cloud (VPC).<br><br>* The ECS instance must have at least 4 vCPUs and 8 GiB of memory.<br><br>* The ECS instance must not be managed by the Vital Kubernetes Engine (VKE).<br><br>* The cloud assistant agent must be installed on the ECS instance and be in the **Running** state.<br><br>   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div><br>   <br><br>   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">The cloud assistant is a native BytePlus tool for automatic O&M. With the cloud assistant, you can execute O&M commands on one or multiple objects. You do not need to input passwords, log in, or use a jump server. For more information, see <a href="https://docs.byteplus.com/en/docs/ecs/Overview-of-cloud-assistant?lang=zh">Cloud assistant overview</a>.   </div><br>    |


<span id="3wV1mkPc"></span>
## Mounting with access points

<span id="0MnX5EUB"></span>
### Prerequisites


* You have created a file system. For instructions, see [Creating file systems](https://docs.byteplus.com/en/docs/nas/efs_Creating_file_systems).

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">For optimal performance, deploy your file system and ECS instance in the same availability zone.   </div>
   

* You have created an access point. For instructions, see [Creating an access point](https://docs.byteplus.com/en/docs/nas/efs_managing_access_points#8DplUcqW).

* You have installed FSX. For instructions, see [Installing FSX](https://docs.byteplus.com/en/docs/nas/efs_Installing_FSX).

* You have created an ECS instance within the same VPC as the access point. For instructions, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).

* You have installed the cloud assistant agent on the ECS instance. For instructions, see [Installing cloud assistant agent](https://docs.byteplus.com/en/docs/ecs/Install-the-Cloud-Assistant-client?lang=zh).


<span id="xQJzhNNg"></span>
### Steps


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Access point**.

6. On the **Access point** page, click **mount** in the **Actions** column of the access point you want to manage.

7. Under **Select ECS instance**, check the box for the ECS instance you want to use. Then, click **Next step**.

8. Under **Configuration IAM authentication**, configure the following parameters and click **Next step**.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">You need to complete this step if an <strong>IAM policy</strong> is enabled for the access point.   </div>
   

   * <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If no <strong>IAM policy</strong> is enabled for the access point, skip to Step 9.   </div>
   

   * **Access point access policy**

      You can either **create** a new access policy or **reuse** an existing one. The parameters are described below.

      
      <Tabs>
      <Tab zoneid="UcyieMsR" title="Create">
      <TabTitle>Create</TabTitle>
      
      
      |Parameter |Description |
      |---|---|
      |Permission scope |Define the scope of permissions for the access point policy:<br><br><br>* **Read/write**<br><br>* **Read\-only** |
      |Root access |Define root user permissions for the access point policy:<br><br><br>* **Allow root access**<br><br>* **Map to nobody** |
      |Other permissions |**Validation of access point IAM permissions** is selected by default and cannot be deselected. |
      |IAM policy name |IAM policy names are automatically generated and cannot be modified. |
      
      
      
      
      
      </Tab>
      <Tab zoneid="0tpu71wU" title="Reuse">
      <TabTitle>Reuse</TabTitle>
      
      
      |Parameter |Description |
      |---|---|
      |IAM policy name |Enter the name of an existing IAM policy to reuse it.<br><br><br>* Once a policy has been selected, its contents will be displayed on the page.<br><br>* The system will verify that the permissions granted by the selected policy include the ID of the access point. You can only proceed once the policy has been confirmed as valid. |
      |Go to view IAM policy |Click **Go to view IAM policy** to navigate to the **Permission policy** page, where you can view all permission policies. |
      
      
      
      
      
      </Tab>
      </Tabs>
      

   * **ECS default role**

      * If the selected ECS instance is already bound to an IAM role, this parameter will not appear on the page and the current access policy will automatically be assigned to the IAM role.

      * If the selected ECS instance does not have an IAM role attached, you must either **create** a new one or **reuse** an existing one. The parameters are described as follows.

         
         |Parameter |Description |
         |---|---|
         |IAM role name |Enter or select an IAM role name.<br><br><br>* To **create** a new role, the name must:<br><br>   * Contain only uppercase and lowercase letters, numbers, underscores (_), hyphens (\-) and periods (.).<br><br>   * Be no more than 64 characters long.<br><br>* To **reuse** an existing role, click **Go to view IAM roles** to navigate to the **Role Management** page, where you can view all available roles. |
         |Current access policy authorization for IAM roles |This option is selected by default and cannot be deselected. |
         

   * **Allow authorization**

      
      |Parameter |Description |
      |---|---|
      |ECS instances of unbound IAM roles: Allow binding of ECS default roles |These options are selected by default and cannot be deselected. |
      |ECS instances of bound IAM roles: Allows authorization of the current access policy for bound IAM roles ||
      

9. Under **Configuration mount parameters**, configure the following parameters.

   
   |Parameter |Description |
   |---|---|
   |Local mount path |Enter the mount path. The path must start and end with a forward slash (/).<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">We recommend selecting an empty directory for the path. If you select a local directory containing files, these files will be temporarily inaccessible after mounting and the EFS data will be visible instead.</div><br> |
   |Directory does not exist automatically created |Select whether to automatically create the directory path if the specified **local mount path** does not exist. This option is enabled by default. |
   |Skip non\-empty directory |Select whether to skip mounting if the directory is not empty. This option is disabled by default. |
   |Read/write permission |Select whether to mount the file system with **read/write** (default) or **read\-only** permissions. |
   |Turn on xattr |Select whether to enable extended attributes (xattr). This option is disabled by default.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Enabling xattr reduces performance by around 30%. Choose the option that best suits your needs.</div><br> |
   |Auto mount |Select whether to automatically mount the file system on reboot. This option is enabled by default. |
   |Operation |Click **Delete** to remove this local mount path configuration. |
   

10. Click **Start mounting**.


<span id="FvV8OGD8"></span>
## Viewing a list of ECS instances associated with an access point

<span id="2gbHsIXe"></span>
### Steps


1. Log in to the [EFS console](https://console.byteplus.com/efs).

2. In the top menu bar, select the region of the file system you want to manage.

3. In the left navigation pane, select **File System**.

4. On the **File System** page, click the file system you want to manage.

5. In the left navigation pane, select **Access point**.

6. On the **Access point** page, click **Client side list** in the **Actions** column of the access point you want to check.

7. On the **client side list** page, view the list of ECS instances where the file system is mounted through this access point, along with related information. The parameters are described as follows.

   
   |Parameter |Description |
   |---|---|
   |ECS instance name/ID |Displays the name and ID of the ECS instance where the file system is mounted through this access point.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">Clicking the instance name takes you to its <strong>Overview</strong> page.</div><br> |
   |ECS status |Displays the current status of the ECS instance. |
   |FSX status |Displays the running status of FSX.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">If the status shows <strong>Installation failed</strong>, click <strong>Retry</strong> to attempt reinstallation.</div><br> |
   |Mount status |Displays the current mount status. |
   |The mounted directory |Displays the number of successfully mounted directories out of the total mount directories. |
   |FSX version |Displays the version number of the current FSX client.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">Note</div><br><br><br><div data-tips="true" data-tips-type="default">To upgrade FSX, click <strong>…</strong> \> <strong>Upgrade FSX</strong> in the operation column. Then, follow the instructions in the <strong>Upgrade FSX client side</strong> panel to complete the upgrade.</div><br> |
   |IAM role |Displays the name of the IAM role authorized to mount through this access point. |
   


<span id="m4XO0TaL"></span>
### Related operations


|Operation |Description |
|---|---|
|View mount details |To view mount details, click **Mount details** in the **operation** column of the ECS instance you want to check. |
|Upgrade FSX |Follow these steps to upgrade FSX:<br><br><br>1. Click  **…**  \> **Upgrade FSX** in the operation column.<br><br>2. In the **Upgrade FSX client side** panel, view the FSX target upgrade version.<br><br>3. Click **OK** to upgrade immediately. |
|Unmount |Unmount file systems that are mounted through this access point. For instructions, see [Unmounting file systems](https://docs.byteplus.com/en/docs/nas/efs_Unmounting_file_systems). |
