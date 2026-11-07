---
title: "Modifying private network address prefix"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_a_private_address_prefix"
---

PostgreSQL provides private network addresses for accessing PostgreSQL instances. To facilitate use, the private network address prefix supports modification.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## **Prerequisites**

An instance is created and in the **Running** state. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

After the new address takes effect, the old address will be closed three minutes later. Modify the connection configuration of the application synchronously, otherwise it may affect the business, so proceed with caution.

<span id=".5pON5L2c5q2l6aqk"></span>
## **Procedure**


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the name of target instance and enter **Summary** page.

4. Click the **Connectivity** tab, point the mouse at the target endpoint card in the **instance topology** area below, and in the pop\-up window click the **Modify endpoint** button to enter the **Modify endpoint** page.

5. On the **Modify endpoint** page, click the right side of the **Private network address**<span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_e9079885405cce281508d428d13e7c89.png) </span>button, enter the new prefix and click **OK**. The prefix should follow these rules:

   * Consist of lowercase letters, numbers, and hyphens (\-).

   * Contain at least 8 characters, with a total length (including the suffix) of no more than 63 characters.

   * Start with a lowercase letter and end with a lowercase letter or number.


<span id=".55u45YWzIEFQSQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[ModifyDBEndpointAddress](https://docs.byteplus.com/en/docs/RDS_for_PG/modifydbendpointaddress) |Call ModifyDBEndpointAddress API to modify the instance address. |
