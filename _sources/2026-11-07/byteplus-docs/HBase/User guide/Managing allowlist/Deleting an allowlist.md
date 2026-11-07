---
title: "Deleting an allowlist"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Deleting_an_allowlist"
---

You can delete allowlists that you no longer need. This article describes how to delete an allowlist from the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

The target allowlist is a standard allowlist, and all instances have been disassociated from it. For instructions on disassociating instances and allowlists, see [Disassociating instance and allowlist](https://docs.byteplus.com/en/docs/HBase/Disassociating_instance_and_allowlist).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The default allowlist cannot be deleted. To delete the default allowlist, first change it to a normal allowlist and disassociate all instances from it. For instructions on how to modify an allowlist, see [Modifying an allowlist](https://docs.byteplus.com/en/docs/HBase/Modifying_an_allowlist).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. Click **Allowlists** in the left\-side navigation bar.

4. On the **Allowlists** page, select the target allowlist **Actions** column for  **...**  \> **Delete**.

5. In the dialog box that appears, click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/HBase/DescribeAllowLists) |Call the DescribeAllowLists API to query all IP allowlists in a specified region for the current account. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/HBase/DescribeAllowListDetail) |Call the DescribeAllowListDetail API to query the details of a specified allowlist, including IP addresses and details of associated instances. |
|[DeleteAllowList](https://docs.byteplus.com/en/docs/HBase/DeleteAllowList) |Call the DeleteAllowList API to delete a specified allowlist. |
