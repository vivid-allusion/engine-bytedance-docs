---
title: "Enabling global read-only"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_global_read-only"
---

You can enable database global read\-only to ensure the PostgreSQL instance allows read\-only access and prohibits write operations. This topic describes the procedure for enabling database global read\-only.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance is created and in the **Running** state. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

Once you set a database to read\-only mode, the database supports query operations only and does not support update, write, delete, and other modification operations. Please proceed with caution.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the name of target instance and enter **Summary** page.

4. Click the **Connectivity** tab at the top of the page.

5. Under the **Connectivity** tab in the **Connectivity** area, click<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_6d26697ff1f797c8cba3185f51e20cdf.png) </span>button.

6. Click **Enable** and then click **OK** in the pop\-up dialog box.
