---
title: "Viewing allowlist"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Viewing_allowlist"
---

The allowlist displays detailed information about all allowlists under the primary account. By viewing the allowlist, you can gain a preliminary understanding of all allowlist information. This article describes how to view the allowlist.

<span id=".6IOM5pmv5L-h5oGv"></span>
## Background

The allowlists page displays information such as allowlist name, allowlist ID, number of IP addresses in the allowlist, number of associated instances, allowlist description, and supported operations. The allowlist provides quick access to the following operations:


* [Creating an allowlist](https://docs.byteplus.com/en/docs/HBase/Creating_an_allowlist)

* [Associating allowlist and instance](https://docs.byteplus.com/en/docs/HBase/Associating_allowlist_and_instance)

* [Disassociating instance and allowlist](https://docs.byteplus.com/en/docs/HBase/Disassociating_instance_and_allowlist)

* [Deleting an allowlist](https://docs.byteplus.com/en/docs/HBase/Deleting_an_allowlist)

* [Copying an allowlist](https://docs.byteplus.com/en/docs/HBase/Copying_an_allowlist)


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Click the number displayed in the <strong>Number of IP addresses</strong> column of the target allowlist to view information about all IP addresses included in the allowlist.</div>


* <div data-tips="true" data-tips-type="tip">Place the mouse over the target allowlist name and click the <img src="https://lf3-volc-editor.volccdn.com/obj/volcfe/sop-public/upload_1f593c2f1753114728d247ea44bcbe09.png" width="15px" /> icon to modify the name of the allowlist.</div>



<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. In the left navigation pane, click **Allowlists** to view all allowlists for the target account.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In the upper\-left corner, you can search for a target allowlist by <strong>Allowlist name</strong>, <strong>Allowlist ID</strong>, or <strong>Description</strong>. Allowlist name and Description support fuzzy matching.   </div>
   

<span id=".55u45YWzLWFwaQ=="></span>
## Related APIs


|API |Description |
|---|---|
|[DescribeAllowLists](https://docs.byteplus.com/en/docs/HBase/DescribeAllowLists) |Call the DescribeAllowLists API to query all IP allowlists in a specified region for the current account. |
