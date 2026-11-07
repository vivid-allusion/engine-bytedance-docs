---
title: "Disassociating instances and allowlists"
product: "NDB for mysql"
product_code: "NDB_for_MySQL"
source: "https://docs.byteplus.com/en/docs/NDB_for_MySQL/Disassociating_instance_and_allowlist"
---

This article describes how to disassociate instances and allowlists through the console.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

After instances are disassociated from the allowlist, IP addresses in the allowlist can no longer be used to access the instances in the database. Please ensure that the device IP that also requires access to the current instance is added to the other allowlists. To modify allowlist IP addresses, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/NDB_for_MySQL/Modifying_an_allowlist).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

You can choose any of the following methods to associate an instance with an allowlist:

<span id=".5pa55rOV5LiA77ya5bCG5b2T5YmN5a6e5L6L5LuO55m95ZCN5Y2V6Kej57uR"></span>
### Method 1: Disassociating an instance from an allowlist


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the allowlist.

3. Click **Allowlists** in the left\-side navigation bar.

4. On the **Allowlists** page, select the target allowlist **Actions** column for  **...**  \> **Disassociate instance**.

5. On the **Disassociate instance** page, click the **Disassociate instance** of the target Instance **Actions** column. Or check multiple instances, click **Disassociate instance** below the instance list, and disassociate instances and allowlists in batches.

6. Click **OK** in the pop\-up dialog box.


<span id=".5pa55rOV5LqM77ya5bCG55m95ZCN5Y2V5LuO5b2T5YmN5a6e5L6L6Kej57uR"></span>
### Method 2: Disassociating an allowlist from an instance


1. Log on to the [NDB for MySQL console](https://console.byteplus.com/db/vedb-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click **Security**.

5. On the allowlist list, click **Disassociate instance** in the actions column of the target allowlist.

6. Click **OK** in the pop\-up dialog box.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/NDB_for_MySQL/DisassociateAllowList) |Call the DisassociateAllowList to disassociate the instance from the allowlist. |
