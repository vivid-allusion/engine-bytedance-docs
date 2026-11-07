---
title: "Deleting a connection endpoint"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/deleting_connection_endpoints"
---

RDS for PostgreSQL supports deleting connection endpoints. This topic introduces the procedure for deleting connection endpoints.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

<span id=".5rOo5oSP5LqL6aG5"></span>
## **Precautions**


* Deleting an endpoint will interrupt all database connections accessed through this endpoint, operate carefully.

* Only the custom endpoints manually created can be deleted, while the default endpoint cannot be deleted.

* Once a connection endpoint is deleted, all the private addresses, public addresses, and inner service zone addresses associated with the endpoint will be released.


<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Choose **PostgreSQL** \> **Instances** in the left\-side navigation bar.

4. Go to the **Instances** page and click on the target instance name to access the instance.

5. Go to the **Connectivity** tab and hover over the target endpoint card in the **Instance topology** section. Click ** Delete endpoint** in the pop\-up window and then click **OK** in the pop\-up dialog box.
