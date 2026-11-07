---
title: "Deleting allowlist"
product: "Document Database for MongoDB"
product_code: "mongodb"
source: "https://docs.byteplus.com/en/docs/mongodb/delete-allowlist"
---

You can delete allowlists that are no longer needed. This article describes how to delete allowlist via the console.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisite

All instances in the allowlist are disassociated from that allowlist. For specific procedures on how to disassociate instances from allowlists, refer to [Disassociating instances from allowlists](https://docs.byteplus.com/en/docs/mongodb/disassociate-allowlist).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [MongoDB console](https://console.byteplus.com/db/mongodb).

2. In the upper\-left corner of the top menu bar, select the project and region for instance.

3. In the left navigation bar, choose **NoSQL Database \> MongoDB \> Allowlists**.

4. On the **Allowlists** page, click **Delete** in the **Actions** column on the right side of the target allowlist.

5. In the pop\-up dialog box, click **OK**.


<span id=".55u45YWzLWFwaQ=="></span>
## Relevant APIs


|API |Description |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/mongodb/describeallowlists) |Call the DescribeAllowLists API to query all IP allowlists for the account in the specified region. |
|[DescribeAllowListDetail](https://docs.byteplus.com/en/docs/mongodb/describeallowlistdetail) |Call the DescribeAllowListDetail API to query the details of the target allowlist group, including the IP addresses and the details of associated instances. |
|[DeleteAllowList](https://docs.byteplus.com/en/docs/mongodb/deleteallowlist) |Call the DeleteAllowList API to delete the target allowlist. |
