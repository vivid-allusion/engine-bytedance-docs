---
title: "Editing connection endpoints"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/editing_connection_endpoints"
---

RDS for PostgreSQL supports modifying the connection information, endpoint information, and read/write separation settings of connection endpoints. This topic describes how to edit connection endpoints.

## **Prerequisites**

An instance is created and in the **Running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

## **Procedure**

1. Login to the [RDS for PostgreSQL](https://console.byteplus.com/db/rds-pg) console.

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   > **tip**

   > If the project of the instance has not been set, the project should be selected as **All resources**.

3. On the **Instances** page, click the name of target instance and enter **Summary** page.

4. Click on the **Connectivity** tab and hover over the target endpoint card in the **Instance topology** section. Click **Modify endpoint** in the pop\-up window to open the **Modify endpoint** page.

5. At the **Modify endpoint** page, you can modify the private address prefix, private network port, enable or disable Internet access, enable or disable inner service zone access, and other settings following the procedure below.

   |**Actions** |**Note** |
   |---|---|
   |Modify private network access port |For more information, refer to [Modify private network port](https://docs.byteplus.com/en/docs/RDS_for_PG/modifying_private_ports). |
   |Enable public network access |For more information, refer to [Enabling public network access](https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_internet_access). |
   |Disable public network access |For more information, refer to [Disabling public network access](https://docs.byteplus.com/en/docs/RDS_for_PG/disabling_internet_access). |
   |Enable public service area access |For more information, refer to [Enabling public service area access](https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_access_to_an_inner_service_zone). |
   |Disable public service area access |For more information, refer to [Disable public service area access](https://docs.byteplus.com/en/docs/RDS_for_PG/disabling_access_to_an_inner_service_zone). |
   |Change the name of a connection endpoint |The rules for the endpoint name are as follows:<br><br><br>* The name only supports Chinese characters, letters, digits, underscores ( _ ), and hyphens ( \- ).<br><br>* Cannot start with digits or hyphens.<br><br>* Length must be 1 to 64 characters. Modification fails if left empty, and the original endpoint name remains. |

6. Complete the above settings and click **OK.**
