---
title: "Disassociating instance and allowlist"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Disassociating_instance_and_allowlist"
---

You can disassociate an instance from an allowlist if you no longer need the devices in that list to access the instance. This article describes how to disassociate instances and allowlists in the console.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

After disassociating an instance from an allowlist, all devices in that allowlist can no longer access the instance. Ensure that the IP addresses of devices that still need to access the current instance are added to other allowlists. To modify allowlist IP addresses, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/HBase/Modifying_an_allowlist).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

You can use any of the following methods to disassociate an instance from an allowlist.

<span id=".5pa55rOV5LiA77ya5bCG5b2T5YmN5a6e5L6L5LuO55m95ZCN5Y2V6Kej57uR"></span>
### Method 1: Disassociating an instance from an allowlist


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. Click **Allowlists** in the left\-side navigation bar.

4. On the **Allowlists** page, select the target allowlist Actions column for  **...**  \> **Disassociate instance**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">You can also click on the target allowlist name, and in the pop\-up control panel, in the <strong>List of associated instances</strong> area, click <strong>Disassociate instance</strong>.   </div>
   

5. On the **Disassociate instance** page, click the **Disassociate instance** of the target Instance **Actions** column. Or check multiple instances, click **Disassociate instance** below the instance list, and disassociate instances and allowlists in batches.

6. In the dialog box that appears, click **OK**.


<span id=".5pa55rOV5LqM77ya5bCG55m95ZCN5Y2V5LuO5b2T5YmN5a6e5L6L6Kej57uR"></span>
### Method 2: Disassociating an allowlist from an instance


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. On the **Instances** page, click the name of the target instance.

4. At the top of the page, click the **Security** tab.

5. On the **Security** tab, click **Disassociate instance** from the target allowlist in the **Actions** column.

6. In the dialog box that appears, click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/HBase/DescribeAllowLists) |Call the DescribeAllowLists API to query all IP allowlists in a specified region for the current account. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/HBase/DescribeAllowListDetail) |Call the DescribeAllowListDetail API to view the details of a specified allowlist, including its IP addresses and associate instances. |
|[DisassociateAllowList](https://docs.byteplus.com/en/docs/HBase/DisassociateAllowList) |Call the DisassociateAllowList interface to disassociate the target instance from the specified allowlist. |
