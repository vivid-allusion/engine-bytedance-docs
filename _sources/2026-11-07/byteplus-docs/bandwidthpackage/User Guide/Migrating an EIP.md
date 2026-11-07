---
title: "Migrating an EIP"
product: "Bandwidth Package"
product_code: "bandwidthpackage"
source: "https://docs.byteplus.com/en/docs/bandwidthpackage/Migrating_an_EIP"
---

When you need to adjust resource allocation in a Bandwidth Package due to business changes, you can use the migration feature for Elastic IP Address (EIP) to transfer EIPs from one Bandwidth Package to another. This allows you to optimize bandwidth resource allocation, reduce bandwidth management costs, and ensure stable and flexible business network connectivity.

<span id="tSLFnUMq"></span>
## Instructions


* The EIP migration feature is currently in the beta stage. If you need a trial, please contact your account manager.

* You can migrate up to 100 EIPs​ in a single batch request.

* After an EIP is successfully migrated from Bandwidth Package A to Bandwidth Package B, traffic generated will be billed to Bandwidth Package B. Traffic generated before the migration remains billed to Bandwidth Package A.


<span id="nhQtfl01"></span>
## Limits


* You cannot migrate an EIP to a Bandwidth Package that has been suspended.

* Migration is only allowed between Bandwidth Packages that are in the **same region** and have the **same protection type** and **same ISP**. For EIPs using static single\-ISP and preferential, migration is only allowed between Bandwidth Packages with the **same line operator** and **same EIP egress**.

* You can only migrate an EIP to a Bandwidth Package that supports its protocol type. For details, see [Limits on adding cloud resources to Bandwidth Package](https://docs.byteplus.com/en/docs/bandwidthpackage/Limits?lang=zh#.5YW25LuW6ZmQ5Yi2).

* You cannot migrate an EIP with independent bandwidth configured within a Bandwidth Package. To migrate such an EIP, first disable its independent bandwidth configuration on the Bandwidth Package details page.

   > The dedicated bandwidth configuration for EIP in Bandwidth Packages is currently in the beta stage. If you need a trial, please contact your account manager.   
   

<span id="yyWbUpNy"></span>
## Procedure


1. Log in to [the Bandwidth Package console](https://console.byteplus.com/eip/cbwps).

2. In the top menu bar, select the region and project of your target Bandwidth Package.

3. Click **Manage EIP** to the right of the Bandwidth Package associated with the target EIP.

4. Click  **··· \> Migrate** to the right of the target EIP.

5. Select the target Shared Bandwidth Package for migration.

6. Click **Migrate** to complete the action.
