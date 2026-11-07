---
title: "Add instance to project"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_instance_to_a_project"
---

You can add created instances to projects to manage instance resources at the project level. This topic introduces the procedure of adding an instance to a project.

<span id=".5paw5a6e5L6L"></span>
## New instances

For new instances, you can select a project during the instance creation. For more information, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/create_instance).

<span id=".5bey5pyJ5a6e5L6L"></span>
## Existing instance

For existing instances not belonging to any project, add them by [Directly move in](https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_instance_to_a_project#.55u05o6l56e75YWl).

For existing instances, if the instance has been attributed to a project, you can use [Directly move in](https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_instance_to_a_project#.55u05o6l56e75YWl) or [Move in from other projects](https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_instance_to_a_project#.55Sx5YW25LuW6aG555uu56e75YWl) ways to join the new project.

<span id=".55u05o6l56e75YWl"></span>
### Directly moving in

<span id=".5YmN5o-Q5p2h5Lu2"></span>
#### Prerequisites


* The instance ID is available.

* The instance region is available.

* is the resource account ID.


<span id=".5pON5L2c5q2l6aqk"></span>
#### Procedure


1. Log in to the [Project console](https://console.byteplus.com/iam/resourcemanage/project).

2. Go to the project list page and click on the target project name to go to the project details page.

3. Select the resource tab and click **Move in**.

4. Go to the pop\-up **Move in resource** window and choose **Move in directly** \> **Resource TRN**.

5. Enter the resource TRN in **Resource TRN** textbox and click **OK**. Enter the resource TRNs of RDS for PostgreSQL instances in the format of `trn:rds_postgresql:{region}:{account}:instance/{id}`.

   1. `trn` is a fixed prefix.

   2. `{region}` is the resource region. RDS for PostgreSQL service is now available in the following regions as shown in the table below.

      
      |Region |Region |
      |---|---|
      |China (Beijing) |cn\-beijing |
      |East China 2 (Shanghai) |cn\-shanghai |
      |South China 1 (Guangzhou) |cn\-guangzhou |
      

   3. `{account}` is the account ID of the resource.

   4. `{id}` is the instance ID of the PostgreSQL instance.


<span id=".55Sx5YW25LuW6aG555uu56e75YWl"></span>
### **Move in from other projects**

<span id=".5YmN5o-Q5p2h5Lu2"></span>
#### Prerequisites

The instance ID is available.

<span id=".5pON5L2c5q2l6aqk"></span>
#### Procedure


1. Log in to the [Project console](https://console.byteplus.com/iam/resourcemanage/project).

2. Go to the project list page and click on the target project name to go to the project details page.

3. Select the resource tab and click **Move in**.

4. Complete the following actions in the **Move in resource** pop\-up window and click **OK**.

   1. Select **Move in from other projects**.

   2. Select a source (source project).

   3. Enter the instance ID to search for resources.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[Project Resource Management](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Resource_Management)
