---
title: "Copying an allowlist"
product: "Table Storage for HBase"
product_code: "HBase"
source: "https://docs.byteplus.com/en/docs/HBase/Copying_an_allowlist"
---

Support creating a new allowlist by copying an existing one. This topic describes the procedure for copying an allowlist.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions

The copied allowlist will contain the IP addresses and associated security groups in the original allowlist, but it will not be associated with any instances.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [HBase console](https://console.byteplus.com/db/hbase).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

3. Click **Allowlists** in the left\-side navigation bar.

4. On the **Allowlists** page, click **Copy** in the allowlist **Actions** column.

5. In the dialog box that pops up, set the copied **Allowlist name** and **Description**.

   
   |Parameter |Description |
   |---|---|
   |Allowlist name |Enter the allowlist name, which must also meet the following requirements:<br><br><br>* Cannot start with digits or hyphen (\-).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The length is 1~32 characters.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When copying an allowlist, the default name of the copied allowlist will be <code>original allowlist name-replica-operation date</code>.</div><br> |
   |Description |Enter the comment information for the allowlist, and the length should not exceed 200 characters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you copy an allowlist, the default description of the copied allowlist is <code>original allowlist name replica</code>.</div><br> |
   

6. Click **OK**.
