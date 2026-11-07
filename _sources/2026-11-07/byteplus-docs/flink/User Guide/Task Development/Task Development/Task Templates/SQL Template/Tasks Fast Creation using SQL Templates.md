---
title: "Tasks Fast Creation using SQL Templates"
product: "BytePlus Flink"
product_code: "flink"
source: "https://docs.byteplus.com/en/docs/flink/Tasks_Fast_Creation_using_SQL_Templates"
---

The console offers a rich selection of foundational SQL and Change Data Capture templates ready for immediate task creation; you can also use pre\-created custom templates. Creating tasks with SQL modules can greatly reduce development time.

<span id="80a04ce1"></span>
## Develop tasks using templates


1. Log in to [BytePlus Flink Console](https://console.volcengine.com/flink).

2. Select the target region from the top menu bar.

3. In the left navigation bar, select **Project Management**, then click on the project block to enter the project.

4. In the left navigation bar of the project, select **Task Development \> Jupyter lab**.

5. On the **Template Management** page, choose **SQL templates**.

6. Select the desired template, confirm the engine version, and then click **Use Template**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c17732968f2f4f6cac73dcecde767a77~tplv-goo7wpa0wc-image.image) </span>

7. In the **create task** dialog, set the task name, folder, and other parameters, then click **OK**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41e6e05aadbe468fb1ee352710d33c5e~tplv-goo7wpa0wc-image.image) </span>

   
   |**Configuration** |**Explanation** |
   |---|---|
   |Apply template |Display the currently selected SQL template. |
   |Task name |Customize the name of the task.<br><br>The name can be 1~48 characters long and support numbers, uppercase and lowercase letters, underscores (_), hyphens (\-), and periods (.), with the first and last characters being letters or numbers. |
   |Task type |The task types supported by the template.<br><br>The SQL templates preset in the system are only used for creating BytePlus Flink Stream SQL tasks; however, custom\-created templates support both Stream and Batch types of tasks. |
   |Applicable versions |The engine version that the current template supports. |
   |Located folder |Select the target folder from the dropdown list.<br><br>The system automatically includes a **data development folder**, but for more convenient task management, you may freely create folders. For instructions on how to create a task folder, see [管理任务文件夹](https://docs.byteplus.com/docs/undefined/655468147c29cc0301edefb3). |
   |Task Description |Enter a description statement for the task, generally outlining the functionality implemented by the task. |
   


<span id="e26c916e"></span>
## Subsequent operations

After creating a task using a template, the task will be stored in the designated folder. You can go to the task development page and continue to edit the code based on SQL templates for rapid task development.

For operations related to task development, please refer to[创建 Flink SQL 任务](https://docs.byteplus.com/docs/undefined/655468147c29cc0301edef40).
