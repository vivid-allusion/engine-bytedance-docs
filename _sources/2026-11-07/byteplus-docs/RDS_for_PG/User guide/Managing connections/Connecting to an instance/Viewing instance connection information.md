---
title: "Viewing instance connection information"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/viewing_access_address_and_port"
---

RDS for PostgreSQL supports both private network (default) and Internet access to PostgreSQL instances. This topic describes how to view the private or public address and port information.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

If you need the connection information related to the default terminal, you can directly view it in the instance list. In the instance list, the domain names, IP addresses, and port information of the instance's default terminal for both private and public networks are displayed. If you need the connection information for other connection terminals of the instance, please refer to the Procedure provided in this topic.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Instances have been created and the instance is in **Running** state, for more details please see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

* If you need to view the public network address and port information of the instance, public access must be enabled. For more information, refer to [Enabling public network access](https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_internet_access).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. On the **Instances** page, click the name of target instance and enter **Summary** page.

4. Click on the **Connectivity** tab and hover over the target endpoint card in the **Instance topology** section to view or copy the public and private address and port information in the pop\-up window.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[Enabling public network access](https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_internet_access)
