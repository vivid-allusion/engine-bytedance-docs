---
title: "Disabling public network access"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/disabling_internet_access"
---

When devices outside the virtual private cloud no longer require access to the PostgreSQL instance, it is recommended to disable public network access promptly. This topic describes how to disable public network access.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Instances have been created and the instance is in **Running** state, for more details please see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

* For more information, refer to [Enabling public network access](https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_internet_access).


<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Once Internet access is disabled, this public address will be deleted and the elastic public network IP address (EIP) will be disassociated automatically. Disassociated EIPs will be retained and billing will continue.

* Once Internet access is disabled, you will not be able to access the database over the Internet, and any Internet connections already established will be disconnected.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Go to the **Instances** page and click on the target instance name to open the **Summary** page.

4. Click the **Connectivity** tab at the top of the page.

5. Go to the **Connectivity** tab and hover over the target endpoint card in the **Instance topology** section. Click **Close** on the right side of the public address in the pop\-up window.

6. Click **Close** in the pop\-up dialog box.
