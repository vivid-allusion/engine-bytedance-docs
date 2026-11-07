---
title: "Copying an allowlist"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/Copying_an_allowlist"
---

RDS for PostgreSQL supports the creation of new allowlist by copying existing allowlists. This article describes the operation steps of copying allowlist.

<span id="RbATJ5NB"></span>
## Precautions

The replicated allowlist will contain the IP addresses and associated security groups from the original allowlist, but not any instances.

<span id="sfsk1vyb"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper left corner of the top menu bar, select the region to which the allowlist belongs.

3. Click on **Allowlists** in the left navigation bar.

4. On the **Allowlists** page, click **Copy** for the target allowlist **Actions** column.

5. In the pop\-up **Copy allowlist** window, after setting the name and description information for the copied allowlist, click **OK**.

   
   |Parameters |Note |
   |---|---|
   |Allowlist name |Required The naming convention for allowlist names is as follows:<br><br><br>* The name is unique.<br><br>* Begin with Chinese, a letter, or an underscore (_).<br><br>* Can only contain Chinese characters, letters, digits, underscores (_) and hyphens(\-).<br><br>* The name length is limited to 1~128 characters.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When copying an allowlist, the default name is <code>original allowlist name + replica + operation date</code>.</div><br> |
   |Description |Optional The description information can be used to search the whitelist in the allowlist, and the description content should not exceed 200 characters in length.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">When copying an allowlist, <code>original allowlist name+[space]+replica</code> is used as the description information of the copied allowlist by default.</div><br> |
   


&nbsp;
