---
title: "Comparing instance parameters"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/Comparing_parameter_between_instances"
---

RDS for MySQL allows you to compare the parameter configuration of an instance with that of other MySQL instances to better understand its operational status before migration. This topic describes how to compare instance parameters.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.   </div>
   

3. Click **Instances** in the left\-side navigation bar.

4. On the **Instances** page, click the target instance name.

5. At the top of the page, click **Parameters**.

6. On the **MySQL parameter** sub\-tab, click **Compare parameter**.

7. On the **Compare parameter** page, complete the following steps and click **Compare**.

   * **MySQL instance**: In the drop\-down list, select the MySQL instance to compare in the current region.

   * **Node type**: Select the node for parameter comparison. You can select **Primary node** or **Read\-only node**.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If the selected MySQL instance type is Multiple node or Single node, you can only select <strong>Primary node</strong> as the node type.      </div>
      

   * **Read\-only node**: When the **Node type** is set to Read\-only node, you need to specify the read\-only node of the instance to be compared.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">During parameter comparison, the parameter configuration of the primary node of the source instance is compared with the parameter configuration of the primary node or read\-only node of the comparator instance.   </div>
   

8. On the **Parameter comparison** page, two types of comparison results are displayed: you can choose to view only the differences, or view all comparison items. Click **OK** to close the **Parameter comparison** page.
