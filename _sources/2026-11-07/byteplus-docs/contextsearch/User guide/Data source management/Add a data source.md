---
title: "Add a data source"
product: "ContextSearch"
product_code: "contextsearch"
source: "https://docs.byteplus.com/en/docs/contextsearch/Add_a_data_source_new"
---

A data source is a reusable knowledge resource in ContextSearch. After adding a data source, you can reference it in different scenarios to reduce repeated configuration and improve data management efficiency. This topic describes how to add a data source.

## Procedure

1. Log on to the [ContextSearch console](https://console.byteplus.com/context-search).

2. In the top navigation bar, select the target project and region.

3. Select **Data source** in the left navigation bar, then click **Add data source**.

4. In the **Add data source** panel, configure the following parameters, then click **OK**.

   |**Parameter** |**Description** |
   |---|---|
   |Data source Name |Set the name of the data source, up to 64 characters. |
   |Data source type |Select the type of data source. Currently supports **BytePlus DataBase** and **Lark Docs**. |
   |Database type |Currently, **OpenSearch** and **MySQL** are supported. This parameter is visible only when the **Data source type** is set to **BytePlus DataBase**. |
   |Instance |Select the OpenSearch instance to use from the dropdown list. This parameter is visible only when **Data source type** is set to **Volcengine database** and **Database type** is set to **OpenSearch**. |
   |Instance ID |Select the OpenSearch instance to use from the dropdown list. This parameter is visible only when **Data source type** is set to **Volcengine database** and **Database type** is set to **MySQL**. |
   |Account |Enter the Username of the OpenSearch instance. This parameter is only visible when the **Data source type** is set to **BytePlus DataBase**. |
   |Password |Enter the password for the OpenSearch instance. This parameter is only visible when the **Data source type** is set **BytePlus DataBase**. |
   |App ID |Enter the ID of the Feishu application. For creating a custom Feishu application, refer to the [Cloud Documentation Overview](https://open.larkoffice.com/document/server-docs/docs/docs-overview). This parameter is only visible when the **Data source type** is set to **Lark Docs**. |
   |APP Secret |Enter the Password of the Lark application. This parameter is only visible when the **Data source type** is set to **Lark Docs**. |
   |Address (optional) |Enter the Feishu application's address. This parameter is only visible when the **Data source type** is set to **Lark Docs**. |
   |Affiliated project |Project to which the data source belongs. Cannot switch when adding a data source. To switch, close the panel and modify it from the top navigation bar. |
