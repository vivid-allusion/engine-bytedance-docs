---
title: "Create a Flink Python Task"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Create_a_Flink_Python_Task"
---

Flink supports the development of Python\-based tasks. You can write Python programs yourself and upload the Python files to the repository to develop Python tasks on the platform.

<span id="2df2e32a"></span>
## Function Limitations

Currently, only the Flink 1.17\-byted version supports Flink Python tasks.

<span id="41d151be"></span>
## Create a Flink Python Task


1. Log in to [BytePlus Flink Console](https://console.byteplus.com/flink).

2. Select the target region in the top menu bar.

3. Select **Project Management** in the left navigation bar, perform a fuzzy search based on the project name in the search box, and then click on the project block to enter the project.

4. Select **Task Development \> Tasks** in the project's left navigation bar.

5. On the **Tasks** page, click the plus button to create a task.

   You can also select a target folder and create a task directly within it, or simply click on **Flink Python** at the bottom of the introductory page.

6. In the **Create** dialog, set the job name, storage location, engine version, and other key parameters, then click **Create now**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4317cf337a0444df9aa046bcbd070637~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Job Name |Customize the name of the task.<br><br>The character length of the name is limited to 1\-48, supporting numbers, upper and lower case letters, underscores (_), hyphens (\-), and periods (.), and must start and end with a number or letter. |
|Task Type |Select **Task Type \> Flink Python** . |
|Storage Location |Select the target folder from the drop\-down list.<br><br>There is a default **Data Development Folder**, but for more convenient task management, you are free to create folders. For instructions on how to create a task folder, see [Task Folders](https://docs.byteplus.com/docs/flink/Task_Folders) here. |
|Engine Version |Only the Flink 1.17\-byted version supports Flink Python tasks. |



1. In the task configuration area, set the key parameters for the task.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0ba87e7aa9fe439eaf6cfb139b0d7207~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Task Name |Name set when creating the job. |
|Python File URI |Select an uploaded Python file from the drop\-down list. If you have not uploaded a file yet, please refer to [Upload Resource Files](https://docs.byteplus.com/docs/flink/Upload_Resource_Files). |
|Entry Module |The entry class of the program.<br><br><br>* If the Python job file is a `.py` file, this field is not required.<br><br>* If your Python assignment file is a `.zip` file, enter your Entry Module here, for example, kafka_test. |
|Entry Point Main Arguments |Main function args parameter for the business program, not required. Please fill in the information according to the interface prompts. |
|Python Libraries |Third\-party Python packages.<br><br>Third\-party Python packages will be added to the PYTHONPATH of the Python worker process, allowing direct access in Python custom functions. |



2. After developing and configuring the task, click **save**.


<span id="2f3c1c4b"></span>
## Develop Flink Batch Python tasks


1. Log in to the BytePlus Flink console.

2. Select the target region from the top menu bar.

3. In the left navigation bar, select **Project Management**, conduct a fuzzy search by project name in the search box, and then click into the project block to enter the project.

4. In the project’s left navigation bar, select **Task Development \> Tasks**.

5. On the **Task Development** page, click the plus button to create a task.

   You can also select the target folder and create a task directly in that folder, or simply click **Flink Python** on the guide interface below.

6. In the **Create** dialog, set key parameters such as job name, storage location, and engine version, then click **Create now**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb024c6a98dd49f0931c0f366bbbb73a~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Task Name |Customize the task name.<br><br>The name must be 1\-48 characters in length and can include numbers, upper and lower case letters, underscores (_), hyphens (\-), and periods (.). It should start and end with a letter or number. |
|Task type |Choose **Flink task \> Flink Python**. |
|Job Template |Select the relevant template for batch jobs. |
|Associated folder |Select the target folder from the drop\-down list.<br><br>By default, there is a **data development folder**, but for more convenient task management, you can freely create folders. For information on how to create a task folder, please refer to [Task Folders](https://docs.byteplus.com/docs/flink/Task_Folders). |
|Engine version |Only BytePlus Flink 1.17\-byted version supports Flink Python tasks. |



6. In the task configuration area, set the key parameters of the task.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/270ba30d768f49299eeaaf7c86217bf2~tplv-goo7wpa0wc-image.image) </span>


|**Configuration** |**Description** |
|---|---|
|Task Name |Name set when creating the task. |
|Python File URI |Select a previously uploaded Python file from the dropdown list. If you have not uploaded the file yet, see [Upload Resource Files](https://docs.byteplus.com/docs/flink/Upload_Resource_Files). |
|Entry Module |The entry class of the program.<br><br><br>* If the Python job file is a `.py` file, this field is not required.<br><br>* If the Python job file is a`.zip` file, then you need to enter your Entry Module here, such as kafka_test. |
|Entry Point Main Arguments |Main function's `args` parameters of the business program, optional. Please fill in according to the interface prompts. |
|Python Libraries |Third\-party Python packages.<br><br>Third\-party Python packages will be added to the PYTHONPATH of the Python worker process, allowing direct access in Python custom functions. |



7. After developing and configuring the task, click **save**.
