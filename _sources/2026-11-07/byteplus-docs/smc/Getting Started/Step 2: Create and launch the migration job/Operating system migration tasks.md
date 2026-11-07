---
title: "Operating system migration tasks"
product: "Server Migration Center"
product_code: "smc"
source: "https://docs.byteplus.com/en/docs/smc/Operating-System-Migration-Task"
---

After the migration source information is imported, the SMC console will automatically generate a migration source record. You can create and start an operating system migration task for the migration source in the console to migrate the operating system of your BytePlus instance to veLinux 1.0/2.0 CentOS Compatible while retaining all system volume data.

This topic describes how to create and start a migration task.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The migration source has been imported. For details, see [Importing migration source](https://docs.byteplus.com/en/docs/smc/Step-1-Import-Migration-Sources).

* Make sure that the BytePlus instance with the operating system to be migrated complies with the [operating system migration](https://docs.byteplus.com/en/docs/smc/Preparations#.5pON5L2c57O757uf6L-B56e7) specifications.


<span id=".5rOo5oSP5LqL6aG5"></span>
## Usage notes


* Currently, only the following operating systems are supported for migration.

   
   |Source operating system |<div style="text-align: center"><br>Target OS</div><br> ||
   |---|---|---|
   ||<div style="text-align: center"><br>veLinux 1.0 CentOS Compatible</div><br> |<div style="text-align: center"><br>veLinux 2.0 CentOS Compatible</div><br> |
   |CentOS Stream 8 |<div style="text-align: center"><br>×</div><br> |<div style="text-align: center"><br>✓</div><br> |
   |CentOS 7 |<div style="text-align: center"><br>✓</div><br> |<div style="text-align: center"><br>✓</div><br> |
   

* The 5.x kernel used by veLinux is incompatible with the 3.10 kernel used by CentOS 7. If your instance runs workloads that depend on kernel interface programming, such as kernel out\-of\-tree (OOT) module development and hardware enablement, evaluate compatibility in advance to avoid service malfunctions after operating system migration.

* Before the operating system of the ECS instance is migrated, SMC will automatically create a whole image (naming format: `SMC_Backup_Image__$Migration task ID$`) and a snapshot consistency group (naming format: `create from $Target resource ID$`) for data backup, facilitating subsequent data recovery. The image and snapshots will not be automatically deleted by the resource cleanup feature after the migration. You can delete them manually based on your needs. For details, refer to [Clearing tasks resources](https://docs.byteplus.com/en/docs/smc/Clean-up-task-resources).

* During the migration process, do not perform operations on the source ECS instance. For example, do not stop or restart the source ECS instance.

* Do not shut down the migration Agent during the migration. Doing so will cause migration failure and may even damage the operating system of the source ECS instance. In case of unexpected incidents, restore the system using the whole image automatically created by SMC before the migration. For details, refer to [Purchasing ECS instances with whole images](https://docs.byteplus.com/en/docs/ecs/Using-whole-images-to-buy-ECS).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

After you import the migration source information using the migration Agent, the ECS console will display the corresponding migration source information. You can create a migration task to migrate the source to BytePlus.


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).

2. In the left directory tree under any region, select "Server Migration Center \> Migration source" to enter the migration source list page.

3.  **(Optional)**  If you have already enabled the snapshot service, skip this step. Otherwise, hover the mouse over the "Create migration task" button. In the pop\-up window, check the box next to "Click to activate, indicating that you are aware and agree Service\-Specific Terms for BytePlus Elastic Compute Service", and then click the "Confirm" button.

4. After the snapshot service is enabled, click the "Create migration task" button in the "Actions" column of the target migration source.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7957bb93fa1f9dd5be3d8d5b7ac36af8.png) </span>

5. On the "Create migration task" page, enter the following information based on the page instructions.

   
   |Parameter​ |Description |Sample value |
   |---|---|---|
   |Migration type |Select the migration task type. In this topic, "OS migration" is selected. |OS migration |
   |Task name |Enter the name of the current migration task. |Migration task 1 |
   |Current OS |By default, the source server operating system version is displayed. You cannot modify this parameter. |CentOS 7 |
   |Target OS |Select the new operating system version for the source server after migration. |veLinux 1.0 CentOS Compatible |
   |Project name (optional) |Select the project to which the migration task belongs.<br><br><br>* After a project is selected, the migration task can only be viewed and used by users with permissions for that project.<br><br>* To adjust the project to which the migration task belongs, see [Project resource management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management).<br><br>* If no project is available in the drop\-down list, you can follow the guidelines to create a project. For more information, see [Creating projects](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Management#creating-project).<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">A project is a collection of resources. You can add migration tasks to a project, categorize and manage them by project, and control user and role permissions for migration tasks within the project. For more details, refer to <a href="https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview">Project overview</a>.</div><br> |project\-1 |
   |Tag (optional) |A tag is a key\-value pair used to identify cloud resources. Tags help you categorize cloud resources with similar attributes based on different dimensions, such as purpose, owner, or environment. This allows you to search and aggregate your cloud resources for easy management.<br><br>Click the " **+**  Add tag" button, and enter the tag key and tag value to add a tag to the migration task. For more information, see [Tag overview](https://docs.byteplus.com/en/docs/ecs/Tag-overview). |Key:Value |
   

6. After you configure the parameters, click the "Confirm" button.

7. Once the task is created, it will start immediately.

   * You can view the execution progress, result, and logs of the migration task. You can also modify the auto incremental synchronization rules. For details, see [Managing migration tasks](https://docs.byteplus.com/en/docs/smc/Managing-Migration-Jobs).

   * You can go to the "Event monitoring" page in the ECS console or the "Event Center" in the Cloud Monitor console to query migration task event information. For details, see [Querying and handling ECS events](https://docs.byteplus.com/en/docs/ecs/Querying-and-handling-events). For the complete list of Server Migration Center event types, see [Status change event](https://docs.byteplus.com/en/docs/ecs/Event-type-overview#.54q25oCB5Y-Y5YyW5LqL5Lu2).

8. After the migration is completed, you can go to the ECS console or log in to the source server to check whether the operating system is migrated.

   
   <Tabs>
   <Tab zoneid="B5zNbOt98a" title="ECS console">
   <TabTitle>ECS console</TabTitle>
   
   1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).
   
   2. In the top menu bar, select the region and project where the target instance resides.
   
   3. If the image column of the target instance is updated to veLinux, the migration is successful.
   
   
   </Tab>
   <Tab zoneid="GY3bXgZ3BM" title="Inside the instance">
   <TabTitle>Inside the instance</TabTitle>
   
   1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance).
   
   2. Execute the following command to view veLinux operating system information.
   
      ```Plain Text
      cat /etc/velinux-release
      ```
      
   
      If the following output is displayed, the migration is successful.
   
      <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_eaa03fa0a1e77b6fd8d67200d2a92926.png) </span>
   
   
   </Tab>
   </Tabs>
