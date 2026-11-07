---
title: "Create Flink JAR Jobs"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Create_Flink_JAR_Jobs"
---

Flink supports the development of JAR type jobs. You can write your own business application and build a JAR package. Just upload the application JAR package and configure the key parameters to complete the development of the JAR job, which is very simple.

<span id="74ba4e74"></span>
## Prerequisites

Before developing a JAR job, you should complete the following preparations:


* The project leader or project administrator has already created a Flink resource pool within the project, please see [Create VCI resource pool](https://docs.byteplus.com/docs/flink/Create_VCI_resource_pool).

* Project developers (Project_Dev role) have already uploaded the business JAR package to the repository in advance, please see [Upload Resource Files](https://docs.byteplus.com/docs/flink/Upload_Resource_Files).

* Generally, the developers (Project_Dev) are responsible for developing the tasks. Please ensure that the operator has been added as a project member and associated with their role, please see [Add project members](https://docs.byteplus.com/docs/flink/Member_Management#a45bfca3).


<span id="bbac4320"></span>
## Develop Flink JAR Streaming Jobs


1. Login to the [BytePlus Flink Console](https://console.byteplus.com/flink).

2. Select the target region from the top menu bar.

3. In the left navigation bar, select **Project Management**, perform a fuzzy search by project name in the search box, then click the project block to enter the project.

4. Select **Task Development** in the left navigation bar of the project.

5. On the **Task Development** page, click the plus button to create a task.

   You can also choose the target folder and create a task directly in that folder; you can also directly click **Create** under **Flink Jar**.

6. In the **Create Job** dialog, set the task name, affiliated folder, engine version, and other key parameters, then click **Create now**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db64e5a5ce054f75a2f7e77af719d7a4~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Task Name |Customize the Task Name.<br><br>The name's character length is limited to 1\-48, supporting numbers, uppercase and lowercase English letters, underscores (_), hyphens (\-), and periods (.), and must start and end with a number or letter. |
|Job Type |Select **BytePlus Flink Task \> BytePlus Flink JAR**. |
|Belonging Folder |Select the target folder from the dropdown list.<br><br>The system defaults to having a **Default Folder**, but for easier task management, you are free to create folders. For instructions on how to create a task folder, see [Task Folders](https://docs.byteplus.com/docs/flink/Task_Folders). |
|Engine Version |Currently supports BytePlus Flink 1.11\-byted, BytePlus Flink 1.16\-byted, BytePlus Flink 1.17\-byted versions; please choose as needed. |
|Task Description |Enter the task description, which generally describes the functionality the task implements. |



6. Set the key parameters in the task configuration area.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/feef6bfe30e545cca50482077595a943~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Explanation** |
|---|---|
|Task Name |The name set when creating the task. |
|Jar URI |Select uploaded JAR packages from the drop\-down list. If you have not uploaded a JAR package yet, please refer to [Upload Resource Files](https://docs.byteplus.com/docs/flink/Upload_Resource_Files). |
|Entrypoint Class |Main class of the business JAR package, please complete the form as instructed on the interface. |
|Entrypoint main args |Main function's `args[]` parameters for the business program, optional. Please complete the form as instructed on the interface. |



7. After job development and configuration are completed, click **Save**.


<span id="c4872d77"></span>
## Develop Flink Batch JAR task.


1. Log in to BytePlus Flink Console.

2. Select the target region from the top menu bar.

3. In the left navigation bar, select **Project Management**, perform a fuzzy search by project name in the search box, and then click on the project block to enter the project.

4. In the project's left navigation bar, select **Task Development \> Tasks**.

5. On the **Task Development** page, click the plus button to create a task.

   You can also select the target folder and create a task directly within that folder; alternatively, you can click on **Create** on the **Flink Batch Jar**.

6. In the **Create** dialogue, set the task name, parent folder, engine version, and other key parameters, then click **Create now**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf1a831729734a8e81a2b5618f5f0816~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Task Name |Customize the task's name.<br><br>The name length is restricted to 1\-48 characters. It supports numbers, uppercase and lowercase letters, underscores (_), hyphens (\-), and periods (.), and must start and end with a number or letter. |
|Task Type |Select **Flink Task \> Flink Batch \> Jar**. |
|Associated Folder |Select the target folder from the dropdown list.<br><br>The system has a default **Data Development Folder**, but for more convenient task management, you can freely create folders. For how to create a task folder, see [Task Folders](https://docs.byteplus.com/docs/flink/Task_Folders). |
|Engine Version |Currently supports BytePlus Flink 1.11\-byted, BytePlus Flink 1.16\-byted, and BytePlus Flink 1.17\-byted versions, please choose as needed. |
|Task Description |Enter the task description statement, which generally describes the functionality of the task. |



7. In the task configuration area, set the key parameters for the task.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2437378a5e6346c293ded2845f870545~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Instructions** |
|---|---|
|Task Name |The name set when creating the task. |
|Jar URI |Select the uploaded JAR package resource from the dropdown list. If you have not yet uploaded a JAR package, refer to [Upload Resource Files](https://docs.byteplus.com/docs/flink/Upload_Resource_Files). |
|Entrypoint Class |The main class of the business JAR package program, please fill in as prompted by the interface. |
|Entrypoint main args |The parameter `args[]` of the main function in the business program is optional. Please fill in according to the interface prompts. |



8. After task development and configuration are complete, click **Save**.
