---
title: "Row privilege"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/row-privilege"
---

ByteHouse CE offers you a graphical row privilege control capability. Once row privileges are activated in the Console, you can create and authorize row privilege strategies. This document introduces the operational key points of ByteHouse row privileges.

<span id="7f0461ea"></span>
# Background information

ByteHouse supports both privileges and row policies on data objects (e.g., databases, tables, columns, indexes, views, projections, etc.).

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/82260e37488242a8a51b6f3059b4600f~tplv-goo7wpa0wc-image.image" width="544px" /></div>



* Previllige: An abstract strategy that expresses whether a user is allowed to perform actions like insert, drop, alter, and select data objects.

* Row Policy: A security strategy used to control data access. Allows conditions to be imposed on the rows in a table to control which rows different users can access. This row\-level security policy can be used to protect sensitive data, ensuring only users who meet specific conditions can access certain rows.


Prerequisites

Only users with the SystemAdmin or ClusterAdmin role can use this feature.

<span id="dc5c15d2"></span>
# Create row **privilege** policy

<span id="a267d6ba"></span>
## Entrants to the row **privilege** page

After logging in and entering the ByteHouse CE console, click on the ad_auth_management tab at the top, and then click row privilege on the left navigation bar to enter the row privilege list page, where you can create row privilege policies and manage authorization.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5c1231c26e644cdeb34c1b913a46669a~tplv-goo7wpa0wc-image.image) </span>

<span id="047b73d6"></span>
## Activate row **privilege**


1. After entering the row privilege list, you can Select the cluster to be configured from the drop\-down box on the upper left.

   If the cluster has not started the row privilege function, you need to follow the screen reminder to activate row privilege for the cluster before you can create privilege policies for the respective cluster.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d2d61aa9be0445018c136c2de5bf4018~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Currently, only clusters version 2.4 and above support activating row privilege features. Lower version clusters require an upgrade before activating the features.   </div>
   

2. You can activate the row privilege toggle in the pop\-up sidebar; the toggle must be turned on and the cluster restarted for the changes to activate.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0eebb56044d4491fa86dd10afe936af8~tplv-goo7wpa0wc-image.image) </span>


<span id="fd7c00fb"></span>
## Create row **privilege** policy


1. Click the **Create row privilege policy** button in the upper left corner of the Page, and configure row privilege policy parameters in the pop\-up Page.

2. Configure basic information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/125db54ad808473099e1558b8367be85~tplv-goo7wpa0wc-image.image) </span>

   * Select the cluster to enforce row\-level security. The cluster must have row\-level security activated.

   * Customize the name and description to identify the row\-level security strategy.

3. Configure the row\-level security strategy.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca0110333f3046e1b506888b303c0e20~tplv-goo7wpa0wc-image.image) </span>

   
   |Param |Description |
   |---|---|
   |Database & Table |Select the database and tables in need of privilege control from the dropdown list. |
   |Row restrictions |Enter the row\-level privilege control strategy in the row restriction input field. The row\-level privilege control strategy is implemented through the **Column** Field Expression of the selected table, for example:<br><br><br>* `city = 'shanghai'`: This row privilege strategy allows viewing data only where the **Column** city has the Valu has the Value shanghai.<br><br>* `city IN ('shanghai', 'beijing')`: This row\-level privilege policy means you can only view data where the **city** column values are **shanghai** or **beijing**.<br><br>* `description LIKE '%sale%'`: This row\-level privilege policy means you can only view data where the **description** column contains the value **sale**.<br><br><br>You can click **View Example** above to see more configuration examples.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The column fields configured here must actually exist in the selected table. Otherwise, users granted this row\-level privilege policy will not be able to query the data; therefore, ensure the configuration is correct and avoid problems such as case sensitivity and spelling errors.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">This configuration only supports specifying a single <strong>column field</strong> expression here and <strong>does not support</strong> configuring multiple column field expressions via commas, Wrap Text, or in other ways.</div><br> |
   |RESTRICTIVE |Select the logic between policies when there are multiple row\-level privileges. By default, the PERMISSIVE strategy is used. You can choose to activate the RESTRICTIVE strategy, which will then be applied.<br><br><br>* PERMISSIVE strategy: The system tries to allow access as much as possible. If any policy allows access, the access request is approved.<br><br>* RESTRICTIVE strategy: The system requires all relevant privilege control policies to allow access. Any single policy's denial results in the entire access request being denied. |
   

4. You can click the Add button in the actions column to keep adding more row restriction strategies.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">A data table only supports adding one row limit strategy.   </div>
   

5. After completing the addition of all row restriction strategies, click the **Create** button below to finish creating the row\-level security strategy.


<span id="c9deb214"></span>
# Authorize to user/role

After the row\-level security strategy is created, you can click the **Grant Authority** button on the row\-level security strategy list page to grant authority to users or roles.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e6e42ffa4f046ffbfdaad45032d29ca~tplv-goo7wpa0wc-image.image) </span>

<span id="ef010c34"></span>
# Edit/Delete row\-level security strategy

You can edit or delete the row\-level privilege policies you have created by clicking the **edit** or **delete** buttons in the row policy list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85bbb9558263466b8dd6a480553812c8~tplv-goo7wpa0wc-image.image) </span>
