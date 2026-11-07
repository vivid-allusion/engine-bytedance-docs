---
title: "Resource privilege management"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/resource-privilege-management"
---

This section mainly explains how to set resource privileges in ByteHouse, including creating databases, creating external catalogs, data loading, knowledge base management, virtual warehouses, and global audit logs. The authorized objects include roles and users.

<span id="409b23ac"></span>
# Background information

Under the AccountAdmin role, you can click on the "Access Control \> Resource Privileges" page in the top navigation to view all resource libraries and tables under the account.

The general concept of resource privilege types is as follows:


|Privilege |Description |
|---|---|
|Create a database |Create a database, and browse all database lists. |
|Create an external catalog |Create an external catalog, and browse all external catalogs. |
|Data loading management |The function privileges of the Data Import module, including creating, editing, and deleting import tasks, creating, editing, and deleting datasources. |
|Knowledge base management |Create, view, and manage knowledge bases. |
|Virtual warehouses management |Function privileges for Virtual Warehouse Management (supports View, Use, All privileges), and also supports setting the scope of the virtual warehouse control to a specific virtual warehouse or all virtual warehouses.<br><br><br>* VIEW: Can view the virtual warehouse and search history records<br><br>* USE: Can use the virtual warehouse for queries and restore the virtual warehouse when "Automatic Restore" is activated<br><br>* ALL: Grants all privileges to the virtual warehouse. |
|Global audit log |View global audit logs, including log information such as SQL history, running queries, permission audits, virtual warehouse audits, and user activities. After obtaining this privilege, sub\-users can directly view the global audit log information of all sub\-users. |


<span id="07a4776e"></span>
# Caution

Only the main account or the sub\-account with the SystemAdmin or AccountAdmin role and the privilege to access the ByteHouse console can manage resource privileges in the ByteHouse Console.

<span id="89e3b988"></span>
# Prerequisites


1. The log\-in account is **Administrator role (AccountAdmin)** , or has management privileges for creating databases, data loading, virtual warehouses, and data expressways.

2. Confirm that the **User/role** to be authorized exists. For details, refer to [Manage IAM user](https://docs.byteplus.com/docs/bytehouse/docs-user-management) and [Role management](https://docs.byteplus.com/docs/bytehouse/docs-access-control-administration).


<span id="742cc66e"></span>
# Grant resource privileges


1. Click on "ad_auth_management \- Resource privilege" in the top navigation page to view all the database tables under the account.

2. Click the edit button on the right to modify the corresponding resource privileges.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/653ec78dde744e77a96d992f3c264eb8~tplv-goo7wpa0wc-image.image) </span>

3. Select to enable or disable the privileges for the corresponding roles or users, then click "Submit" to confirm the privilege settings. The interface operations for these settings are consistent; for specific displays, refer to the figure below:

   * Edit creating databases privilege

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b31e781d5aa84cdc88dfad14098939a2~tplv-goo7wpa0wc-image.image) </span>

   * Edit creating external catalogs privilege

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ed5c1c2eed3745e898ab8ecb758856f4~tplv-goo7wpa0wc-image.image) </span>

   * Edit data loading management privilege

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/755ad87df45646d38a245173cde36a22~tplv-goo7wpa0wc-image.image) </span>

   * Edit knowledge base management privilege

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/99917492b349454cab49879f38957956~tplv-goo7wpa0wc-image.image) </span>

   * Edit virtual warehouse privilege

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ac95dd460d8f4f04a709766cc989c9e7~tplv-goo7wpa0wc-image.image) </span>

   * Edit global augit log privilege

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8355ebe3f05746c9b514175efe8aa94e~tplv-goo7wpa0wc-image.image) </span>
