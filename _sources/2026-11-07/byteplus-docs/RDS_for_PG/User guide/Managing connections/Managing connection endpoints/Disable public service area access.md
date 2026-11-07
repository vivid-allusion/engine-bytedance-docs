---
title: "Disable public service area access"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/disabling_access_to_an_inner_service_zone"
---

This topic describes the procedure for disabling public service area access.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**


* An instance is created and in the **Running** state. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

* Public service area access is enabled for the instance. For more details, refer to [Enabling public service area access](https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_access_to_an_inner_service_zone).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

After disabling public service area access, you cannot access the database through the public service area, and all established public service area connections will be interrupted. Handle with care.

<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the name of target instance and enter **Summary** page.

4. Click the **Connectivity** tab at the top of the page.

5. Under the **Connectivity** tab in the **instance topology** area, hover over the default endpoint. In the pop\-up window, in the **Public service area**, click the **Disable** button.
