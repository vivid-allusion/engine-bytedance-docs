---
title: "Viewing instance list"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_instance_list"
---

This topic describes the information displayed in the Instance list of RDS for PostgreSQL and the procedure to view the instance list.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs, and you can view the instance list under the current project and region.

   The instance list provides multiple pieces of information about the instance, which are displayed as list items. Different list items support different display and viewing methods. The detailed information is shown in the following table. Different list items support different display methods and viewing methods, detailed information is shown in the table below.

   
   |List items |Whether custom display is supported |Whether filtering and viewing is supported |Related Actions |
   |---|---|---|---|
   |Instance name/ID |No |No |None |
   |Operational status |Yes |Yes |None |
   |Availability zone |Yes |Yes |[Migrating availability zones](https://docs.byteplus.com/en/docs/RDS_for_PG/availability_zone_migration) |
   |Private network address |Yes |No |[Modifying private network address prefix](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_a_private_address_prefix) |
   |Private network port |Yes |No |[Modifying private network access port](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_private_ports) |
   |Public network address |Yes |No |[Enabling public network access](https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_internet_access) |
   |Port |Yes |No |[Enabling public network access](https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_internet_access) |
   |IP address |Yes |No |None |
   |Virtual private cloud |Yes |No |None |
   |Instance types |Yes |Yes |None |
   |Tag |Yes |Yes |[Label Management](https://docs.byteplus.com/en/docs/RDS_for_PG/managing_tags) |
   |Primary node specifications |Yes |No |[Change Instance Configuration](https://docs.byteplus.com/en/docs/RDS_for_PG/standard_instance_specification_modification) |
   |Number of Nodes |Yes |No |[Change Instance Configuration](https://docs.byteplus.com/en/docs/RDS_for_PG/standard_instance_specification_modification) |
   |Database version |Yes |Yes |None |
   |Billing method |Yes |Yes |[Switch to Subscription](https://docs.byteplus.com/en/docs/RDS_for_PG/switching_to_subscription) |
   |Creation time |Yes |No |None |
   |Project |No |No |[Add instance to project](https://docs.byteplus.com/en/docs/RDS_for_PG/adding_an_instance_to_a_project) |
   |Actions |No |No |Different instances support different Actions.<br><br><br>* For pay\-as\-you\-go instances, support includes:<br><br>   * [Login DBW](https://docs.byteplus.com/en/docs/RDS_for_PG/managing_data#.55m75b2V5bel5L2c5Y-w)<br><br>   * [Change Instance Configuration](https://docs.byteplus.com/en/docs/RDS_for_PG/standard_instance_specification_modification)<br><br>   * [Add read-only node](https://docs.byteplus.com/en/docs/RDS_for_PG/standard_instance_specification_modification)<br><br>   * [Switch to Subscription](https://docs.byteplus.com/en/docs/RDS_for_PG/switching_to_subscription)<br><br>   * [Restart instance](https://docs.byteplus.com/en/docs/RDS_for_PG/restarting_an_instance)<br><br>   * [Deleting an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/deleting_or_unsubscribing_an_instance)<br><br>* \- For year and month subscription instances, support includes:<br><br>   * [Login DBW](https://docs.byteplus.com/en/docs/RDS_for_PG/managing_data#.55m75b2V5bel5L2c5Y-w)<br><br>   * [Renewal](https://docs.byteplus.com/en/docs/RDS_for_PG/renewal_management)<br><br>   * [Change Instance Configuration](https://docs.byteplus.com/en/docs/RDS_for_PG/standard_instance_specification_modification)<br><br>   * [Add read-only node](https://docs.byteplus.com/en/docs/RDS_for_PG/standard_instance_specification_modification)<br><br>   * [Restart instance](https://docs.byteplus.com/en/docs/RDS_for_PG/restarting_an_instance)<br><br>   * [Unsubscribe instance](https://docs.byteplus.com/en/docs/RDS_for_PG/deleting_or_unsubscribing_an_instance#.6YCA6K6i5a6e5L6L) |
   


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">In the instance list page, the displayed private network address, private port, public network address, public port, and IP address are all the connection information of the default terminal of the instance. If you need connection information for other terminals, you can refer to <a href="https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_access_address_and_port">Viewing instance connection information</a> to obtain it.</div>


* <div data-tips="true" data-tips-type="tip">On the instance list page, you can search for instances by instance ID, instance name, read\-only node ID, or VPC ID. A search category of instance ID/instance name is also provided. It also provides a search category for instance ID/instance name; when selecting this category, searches will be conducted based on the entered content for both instance ID and instance name, and the union of both search results will be displayed as the final result.</div>



<span id=".5ZCO57ut5q2l6aqk"></span>
## Next steps

<span id=".6Ieq5a6a5LmJ5a6e5L6L5YiX6KGo55qE5a2X5q61"></span>
### Customize the Instance List Fields

The instance list displays information such as instance name, instance ID, running state, availability zone, private network address, private network port, public network address, public network port, IP address, private network, instance type, tags, master node specification, number of nodes, database version, billing type, creation time, and affiliated project. You can customize the columns of the instance list by clicking the **Customize list fields** button at the upper right corner of the instance list. Except for the **Instance name/ID** and **Actions** fields, all other fields can be customized for display.


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs, and you can view the instance list under the current project and region.

3. On the upper right corner of the instance list page, Click the **Customize list fields** button and check the fields you want to display.


<span id=".55u45YWz6ZO-5o6l"></span>
## Related Links


* [Modify configuration](https://docs.byteplus.com/en/docs/RDS_for_PG/standard_instance_specification_modification)

* [Switch to Subscription](https://docs.byteplus.com/en/docs/RDS_for_PG/switching_to_subscription)

* [Restart instance](https://docs.byteplus.com/en/docs/RDS_for_PG/restarting_an_instance)

* [Deleting an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/deleting_or_unsubscribing_an_instance)
