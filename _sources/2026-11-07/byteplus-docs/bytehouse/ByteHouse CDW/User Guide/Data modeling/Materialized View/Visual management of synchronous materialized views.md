---
title: "Visual management of synchronous materialized views"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/visually-manage-synchronous-materialized-view"
---

ByteHouse supports managing synchronized materialized views visually, allows users to save common queries in advance, and automatically updates data to accelerate queries, suitable for simpler computational scenarios. This article introduces how to create and delete synchronized materialized views.

<span id="a284fbc9"></span>
## **Usage restrictions**

Before use, ensure your engine is version v2.3 or later. You can check your current engine version on the **Tenant management** \> **Basic Information** page in the ByteHouse console.

<span id="5c84655e"></span>
## Create synchronized materialized views


1. Log in to ByteHouse Console, click the target database under the **Database** tab, click  **+ View**, and click **Create Materialized View**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/653051c7a16f4ac79088f8e8c6966e33~tplv-goo7wpa0wc-image.image) </span>

2. On the create materialized view page, enter the query SQL then click **Next**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8be82f779ffd4ca9a8be0cf5c1df0a7d~tplv-goo7wpa0wc-image.image) </span>

3. Configure materialized view information and click **Next**.

   
   |Parameter |Parameter description |
   |---|---|
   |Materialized view type |Select synchronized materialized view. |
   |Database |Select the Database for creating a materialized view and target table. |
   |Name |Customize the name of the materialized view. The naming rules are as follows:<br><br><br>* The name can only contain letters, numbers, and underscores "_".<br><br>* Up to 128 characters. |
   |Sort Key |The system will recommend suitable sort keys based on the SQL commands you have entered, and you can Confirm from the drop\-down list. Changing the sort key is Not supported after completion. |
   |Partition Key |The system will recommend suitable partition keys based on the SQL commands you have entered, which you can confirm from the dropdown list. Once created, the partition key cannot be changed. |
   

4. Preview the system\-generated creation SQL and confirm if it meets your expectations. If everything is correct, click **Create,**  and the system will automatically create the synchronized materialized view. If you need to modify information, you can click **Previous**.

5. After a successful creation, in the **Materialized views** tab, click on the **materialized view name** to view the detailed information of the materialized view.


<span id="fdb83592"></span>
## Delete synchronous materialized view


1. In the ByteHouse console, under the **Database** tab, click on the target database, click on the materialized view tab, and then click on the **target materialized view name**.

2. Click on the upper right corner of the materialized view interface  **...**  button, click **Delete materialized view**.

3. In the popup window, click **Delete**.
