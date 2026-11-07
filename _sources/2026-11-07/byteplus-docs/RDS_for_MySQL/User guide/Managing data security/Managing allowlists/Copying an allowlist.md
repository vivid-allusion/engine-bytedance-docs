---
title: "Copying an allowlist"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/copying_an_allowlist"
---

RDS for MySQL supports the creation of new allowlist by copying existing allowlists. This article describes the operation steps of copying allowlist.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* The replicated allowlist will contain the IP addresses and associated security groups from the original allowlist, but not any instances.

* To enhance the security of RDS for MySQL, optimize privilege management, and provide more granular and secure resource management services, RDS for MySQL has upgraded its allowlist feature to support project authentication. After the project authentication feature is launched, historical allowlists are automatically assigned to the "Global resources" project. To view the allowlists in the "Global resources" project, you must select "All resources" in the top navigation bar.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper left corner of the top menu bar, select the region to which the allowlist belongs.

3. Click on **Allowlists** in the left navigation bar.

4. On the **Allowlists** page, click **Copy** for the target allowlist **Actions** column.

5. In the pop\-up **Copy allowlist** window, after setting the name and description information for the copied allowlist, click **OK**.

   
   |Parameter |Description |
   |---|---|
   |Allowlist name |Required The naming convention for allowlist names is as follows:<br><br><br>* The name is unique.<br><br>* Begin with Chinese, a letter, or an underscore (_).<br><br>* It can contain only Chinese characters, letters, digits, underscores (_), and hyphens (\-).<br><br>* The name length is limited to 1~128 characters.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When copying an allowlist, the default name is <code>original allowlist name + replica + operation date</code>.</div><br> |
   |Description |Optional The description information can be used to search the whitelist in the allowlist, and the description content should not exceed 200 characters in length.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When copying an allowlist, <code>original allowlist name+[space]+replica</code> is used as the description information of the copied allowlist by default.</div><br> |
