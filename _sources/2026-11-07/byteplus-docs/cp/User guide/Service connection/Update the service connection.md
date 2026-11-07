---
title: "Update the service connection"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Update_the_service_connection"
---

Supports modifying the connection information for connected artifact repositories or code sources.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

After updating the service connection information, you must manually update the information for any tasks associated with the service connection to prevent task failures.

<span id=".5Y-v57yW6L6R6YWN572u"></span>
## An editable configuration

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The type of integration service (for example, Codebase code repository) and the service ID <strong>cannot be updated</strong>.</div>



|Configuration Item |Descriptions |
|---|---|
|Name |Custom service connection name. |
|Repository URL |Enter the service access address. |
|Access Credentials |The entered access credentials for the target service. |
|Description |Description of the custom service. |
|Sharing scope |Select the workspace that can call this service. |


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **Global configurations \> Service connection**.

3. On the Service connection page, under the **actions** column for the target Service connection, click **edit**.

4. On the edit page, modify configuration information.

5. After making modifications, click **confirm**.
