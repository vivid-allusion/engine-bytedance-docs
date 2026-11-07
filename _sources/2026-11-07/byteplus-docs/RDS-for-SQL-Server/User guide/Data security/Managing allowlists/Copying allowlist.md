---
title: "Copying allowlist"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/copying-allowlist"
---

RDS for SQL Server supports the creation of new allowlists by copying existing allowlists. This article describes the steps to replicate allowlists.

<span id="precautions"></span>
## Precautions

The copied allowlist will contain the IP addresses and associated security groups from the original allowlist, but not any instances.

<span id="operation-steps"></span>
## Operation steps


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the target project and region.

3. Click **Allowlist list** in the left navigation bar.

4. On the **Allowlist list** page, click Copy for the target allowlist action column.

5. In the **Copy allowlist** dialog box, set the **Allowlist name** and **Description**.

   
   |Parameters |Description |
   |---|---|
   |allowlist Name |Required. The naming rules for allowlisted names are as follows:<br><br><br>* names are unique.<br><br>* Begins with Chinese, a letter, or an underscore (_).<br><br>* can only contain Chinese, letters, numbers, underscores (_) and underscores (\-).<br><br>* Length is 1 to 128 characters.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When copying the allowlist, the <code>original allowlist name + copy + operation date</code> is named after the copied allowlist by default.</div><br> |
   |Description |Optional. The description information can be used to search the allowlist in the allowlist, and the description content should not exceed 200 characters in length.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When copying the allowlist, a <code>copy of allowlist name</code> is used as the description information of the copied allowlist by default.</div><br> |
   

6. Click **OK**.
