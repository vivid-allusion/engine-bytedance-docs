---
title: "Connect to an artifact repository"
product: "Code Pipeline"
product_code: "cp"
source: "https://docs.byteplus.com/en/docs/cp/Connect_to_an_artifact_repository"
---

The pipeline needs to reference artifact repositories, code sources, and other services. You can register these services in advance in the Service Onboarding module of Code Pipeline to facilitate unified management later. This article introduces methods for integrating artifact repository services in Code Pipeline.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [Code Pipeline Console](https://console.byteplus.com/cp).

2. In the left navigation bar, select **Global configurations \> Service connection**.

3. On the Service connection page, click **Create service connection**.

4. On the Create service connection page, fill in the following parameters as specified.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The <strong>Service connection</strong> ID is a unique identifier. Service connection IDs must be unique within the same account and cannot be changed after creation.   </div>
   

   
   |Configuration Item |Descriptions |
   |---|---|
   |Connection Type |Select **artifact repository**. |
   |Registry type |Select `Docker registry`. |
   |Name |Custom service connection name. |
   |ID |Custom service connection ID The unique identifier of a service connection must be unique within the same account and cannot be modified after creation. |
   |Repository URL |Enter the address of the artifact repository to be integrated. |
   |Access Credentials |Enter the username and password for accessing the artifact repository. |
   |Description |Description of custom services |
   |Sharing scope |Select a workspace that can invoke this service |
   

5. Click **OK** to finish creating the service connection.
