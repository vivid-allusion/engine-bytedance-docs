---
title: "Modifying private network access port"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_private_ports"
---

RDS for PostgreSQL provides private addresses by default for accessing PostgreSQL instances. The private network ports are modifiable to facilitate service access.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance is created and in the **Running** state. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the name of target instance and enter **Summary** page.

4. Click on the **Connectivity** tab and hover over the target endpoint card in the **Instance topology** section. Click **Modify endpoint** in the pop\-up window to open the **Modify endpoint** page.

5. On the **Modify endpoint** page, click the button to the right of the **Private network port**<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_068f4429a1225b2f428c9c61f92d58b3.png) </span>Enter the new port number and click **OK**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Port number range: 1000 to 65534.</div>


* <div data-tips="true" data-tips-type="tip">After you modify the private network port, please manually refresh the page to confirm that the modification is in effect.</div>


* <div data-tips="true" data-tips-type="tip">After the new port takes effect, the old port will be closed immediately. Modify the connection configuration of the application synchronously, otherwise it may affect the business. Proceed with caution.</div>
