---
title: "Integrate code source"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Integrate_code_source"
---

The pipeline requires access to services such as artifact repositories and code sources. You can register these services with the service connections in Code Pipeline in advance to facilitate unified management in the future. This article introduces the method for integrating the code source service in Code Pipeline.

<span id=".5Luj56CB5rqQ"></span>
## code source

See [Code source overview](https://docs.byteplus.com/en/docs/cp/An_overview_of_the_code_source) for code sources supported by service connection.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Code Pipeline console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **Global configurations \> Service connection**.

3. On the Service connection page, click **Create service connection**.

4. On the Create service connection page, fill in the following parameters as required.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1"><strong>Service connection</strong> ID is the unique identifier for a service connection. Duplicate IDs are not allowed under the same account, and it cannot be changed after creation.   </div>
   

   
   |Configuration Item |Descriptions |
   |---|---|
   |Connection Type |Select **code repository**. |
   |Code repositories |Select a target code repository. |
   |Name |Name of the custom service connection. |
   |ID |The Custom Service Connection ID. Unique identifier for the service connection; duplication is not allowed within the same account, and it cannot be changed after creation. |
   |Access Credentials |Enter access credentials for the code repository. |
   |Description |Custom service description |
   |Sharing scope |Select workspace(s) that can call this service. |
   

5. Click **OK** to complete the creation of the service connection.
