---
title: "Add a dataset"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Add_a_dataset"
---

In personalization search scenarios, you need to first add a dataset and import business data into it before proceeding with model development and optimization. This topic describes how to add a dataset.

## Prerequisites

* A personalization search scenario has been created. For more information, see [Create a scenario](https://docs.byteplus.com/en/docs/contextsearch/Create_a_scenario).

* Basic configuration Completed. For more information, see [Basic configuration](https://docs.byteplus.com/en/docs/contextsearch/Basic_configuration).

## Procedure

1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. Click the![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0fa3b8ee25f6f32b1a40b6b6f218982.png)icon in the top\-right corner on the target personalized search and recommendation scenario page, then click **Add dataset**.

5. In the **Add dataset** panel, select **Local import** or **MySQL** from the **Data source** dropdown list. Configure the following parameters, then click **OK**.

   |Parameter |Description |
   |---|---|
   |Dataset name |Set the dataset name. Naming rules are as follows:<br><br><br>* Cannot start with a number or a hyphen (\-).<br><br>* Length must be between 1 and 128 characters.<br><br>* Contain letters, digits, underscores (_), and hyphens (\-). |
   |Description (optional) |Set a description for the dataset. Length cannot exceed 256 characters. |
   |Data source |Select **Local import** or **MySQL**. |
   |Data source |Select a MySQL instance from the dropdown list.<br><br>> **tip**<br><br><br>> This parameter is visible only when **Data source** is set to **MySQL**.<br> |
   |Database |Select MySQL database from the dropdown list.<br><br>> **tip**<br><br><br>> This parameter is visible only when **Data source** is set to **MySQL**.<br> |
   |Item table |Store information about the recommended targets, users' basic information, and item interactions separately. Sub\-parameters are as follows:<br><br><br>* Field name<br><br>* Type<br><br>* Is array<br><br>* Field property<br><br>* Field description<br><br><br>> **tip**<br><br><br><br>* > You can click **Add field** in the corresponding table to add multiple fields.<br><br><br>* > You can click the delete icon in the corresponding table to delete fields.<br><br><br>* > You can click **JSON code** in the corresponding table to preview the added fields in JSON format.<br><br><br>* > The item table must have at least one field with the property `ITEM_ID`.<br><br><br>* > The user table must have at least one field with the property `USER_ID`.<br><br><br>* > The behavior table fields must include the properties `ITEM_ID` and `USER_ID`.<br> |
   |User table ||
   |Behavior table ||

## Related operations

### Configure a dataset

After adding the dataset, you can configure it by following the steps below.

1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. Click the top\-right corner on the target personalized search and recommendation scenario page![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0fa3b8ee25f6f32b1a40b6b6f218982.png)icon, then click **Data Configuration** to the right of the target dataset.

5. On the **Data configuration** tab, click **Configure fields** in each table as needed to modify field information, then click **Save**.

### Delete a dataset

You can delete a dataset following these steps when it is no longer in use.

1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **My Scene** in the left navigation panel, then click the target personalized search push scenario.

4. Click the![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c0fa3b8ee25f6f32b1a40b6b6f218982.png) icon in the top\-right corner on the target personalized search and recommendation scenario page, then select  **... \> Delete** on the right side of the target dataset.

5. In the pop\-up dialog, click **Delete**.

## Subsequent operations

After adding a dataset, you can import data into it. For detailed steps, see [Import data](https://docs.byteplus.com/en/docs/contextsearch/Import_data).
