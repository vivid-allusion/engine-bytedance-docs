---
title: "Creating a connection endpoint"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/creating_connection_endpoints"
---

This topic describes how to create a custom connection endpoint.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The default endpoint is automatically created at instance creation and does not support manual creation. Only custom endpoints can be manually created.

* You can create 10 custom endpoints at the maximum and 1 custom read/write endpoint at the maximum on an instance.

* You can associate one read\-only node to one read\-only endpoint only, and the associated read\-only node cannot be changed.

* One read\-only node can be associated with multiple read\-only endpoints.

* Once a read\-only node is deleted, the read\-only endpoints associated with it will also be deleted.

* Newly added read\-only nodes will be automatically added to the default endpoint.


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the name of target instance and enter **Summary** page.

4. Click on the **Connectivity** tab. Click **Create endpoint** in the **Instance topology** section to open the **Create endpoint** page.

5. Complete the following settings on the **Create endpoint** page:

   1. Select the read/write mode.

   2. Enter the endpoint name. The rules for the endpoint name are as follows:

      * Can only contain Chinese characters, letters, digits, underscores (_) and hyphens(\-).

      * It cannot start with a digit or hyphen.

      * The name length is limited to 1–64 characters. The endpoint name is optional. If not provided, it will be automatically named "Customized_endpoint".

   3. Select an associated node.

      * If you select "Read/Write" as the endpoint read/write mode, a primary node is automatically selected.

      * If you select "Read\-only" as the endpoint read/write mode, select or check a read\-only node in the **All nodes** column to add the node to the **Selected node** column.

   4. Click **OK** to complete the creation.
