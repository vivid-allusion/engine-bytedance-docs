---
title: "Manage abnormal tables"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/manage-abnormal-tables"
---

ByteHouse supports filtering tables with abnormal statuses such as conflicts and missing definitions through the interface and offers one\-click repair for problematic tables, helping you quickly locate and resolve issues. This article introduces common abnormal table statuses and explains how to fix tables through the interface.

<span id="f727208e"></span>
# Function overview

As a distributed database with an MPP architecture, ByteHouse requires that each table's definition exists and remains consistent across all nodes to ensure balanced data storage and query distribution. ByteHouse displays the status of database tables in the console interface, reflecting their distribution within the cluster, described as follows:


1. **Normal**: The table is properly distributed across the cluster.

2. **Missing**: The table is absent on some nodes in the cluster, which may cause some queries to fail due to missing table definitions and result in data imbalance among nodes.

3. **Conflict**: The table definitions are inconsistent among some nodes in the cluster or between distributed and local tables, potentially causing inconsistent query results.


ByteHouse supports filtering tables with conflict or missing issues, allowing resolution and completion of problems via the interface to quickly fix abnormal table statuses.

<span id="e97a9712"></span>
# View abnormal status tables


1. Log in to the ByteHouse Enterprise Console, click **Data Management** at the top, select the successfully created cluster from the dropdown at the top left, click the **Filter** button, check **Show only conflicts/missing**, then click **Save**. The system will automatically filter and display tables with conflict/missing problems.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3e1b781a32eb420d83efbd6ded62e499~tplv-goo7wpa0wc-image.image) </span>

2. Click the dropdown button before the database name to view tables with abnormal status data. A yellow icon indicates missing problems, and a red icon indicates conflict problems.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c14404dd8724221bfb7d0584335ccb3~tplv-goo7wpa0wc-image.image) </span>


<span id="838ea4be"></span>
# Resolve conflicts


1. Click the table with conflict issues, then click **Conflicting** on the table details page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/852b04119c5a46e1a1c60ac0abb5d58a~tplv-goo7wpa0wc-image.image) </span>

2. View conflict details and DDL comparison details, then perform corresponding fixes.

   ByteHouse provides corresponding solutions for different conflict types. Operate as needed; see the table below for details:

   
   |Conflict subdivision type |Processing method |
   |---|---|
   |DDL differs for the same table on different nodes, but no data |Select the correct DDL from the dropdown list after confirming the field, click **One\-click Fix**, the system will automatically resolve conflicts, overwriting other DDL with the correct DDL you selected.<br><br>The interface example is as follows:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/539a62826e5c4989ada62a1dc4c7bac6~tplv-goo7wpa0wc-image.image) </span> |
   |No DDL for the table on a specific node ||
   |DDL differs for the same table on different nodes, but there is data |Click **View fix documentation** to view [Best practice: Workarounds for table state exceptions](https://docs.byteplus.com/docs/bytehouse/best-practice-workarounds-for-table-state-exceptions) and see the corresponding solution.<br><br>The interface example is as follows:<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22009a0f1692451fabd1f4e81ff58c54~tplv-goo7wpa0wc-image.image) </span> |
   |Columns differ between local table and distributed table ||
   

3. After fixing, the system will report the result of the repair. When repair succeeds, the system will indicate “Node repair successful.”

   If conflict resolution fails, the system will indicate the failed nodes. You can click **Failure** to view the specific reasons and retry according to steps 1 to 2.


<span id="e2b4ffa9"></span>
# Complete missing parts


1. Click a table with missing issues, then click **Missing** on the table details page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4882f6fe6ab7470e96c4827887a073a6~tplv-goo7wpa0wc-image.image) </span>

2. View nodes currently missing DDL. After confirming the completion is needed, click **Complete Nodes**. The system will automatically complete the missing DDL.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/38263f05c8e341aa9f91e77810e8309d~tplv-goo7wpa0wc-image.image) </span>

3. After completion, the system will provide feedback on the result. When the repair succeeds, the system will prompt "Completion success."

   If completion fails, the system will indicate the failed nodes. You can click failure to view the specific reasons and retry according to steps 1 to 2.


<span id="c95bcc6c"></span>
# Reference: Best practice

You can refer to [Best practice: Workarounds for table state exceptions](https://docs.byteplus.com/docs/bytehouse/best-practice-workarounds-for-table-state-exceptions) to learn how to use SQL to resolve table status abnormalities.
