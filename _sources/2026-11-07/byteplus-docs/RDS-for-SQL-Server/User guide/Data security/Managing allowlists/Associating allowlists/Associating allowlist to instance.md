---
title: "Associating allowlist to instance"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/associating-allowlist-to-instance"
---

After adding the IP address to the allowlist, you also need to bind the allowlist to the instance in order for the IP address to successfully access the SQL Server instance. Since allowlists and instances have a "many\-to\-many" correspondence, you can bind allowlists from instances, or you can bind instances from allowlists. This article describes how to bind the allowlist to an instance.

<span id="prerequisite"></span>
## **prerequisite**

The [instance was created ](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide)and is **in the running** state.

<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the target project and region.

3. Click **Instance list** in the left navigation bar.

4. On the **Instance list** page, click the target instance name.

5. At the top of the page, click the **Data security** tab.

6. Under **Data security** Page, click **Associate instance** to enter the **Associate instance** page. Under this page, you can choose **Existing allowlist** or a **New allowlist** to bind the allowlist in two ways. The rules are as follows:

   * **Associate Existing allowlist**

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">the allowlist has been created. For more details, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-allowlist">Creating allowlist</a>.      </div>
      

      * On the **Associate instance** page, click **Existing allowlist** to enter the **Existing allowlist** list.

      * In the **Existing allowlist** list, after checking the allowlist that needs to be bound to the current instance, click **OK**. Successfully bound allowlists appear in the **List of associated allowlist**.

   * **Associate new allowlist**

      * On the **Associate instance** page, click **New allowlist** to enter the **New allowlist** page.

      * On the **New allowlist** page, add the **Allowlist name**, **Description** and **IP address**, and click **OK**.

      
      |parameter |explain |
      |---|---|
      |allowlist name |Required. The naming convention is as follows:<br><br><br>* The name is unique.<br><br>* Start with Chinese, a letter, or an underscore.<br><br>* Only Chinese, letters, numbers, underscores and underscores can be included.<br><br>* The length is 1 to 128 characters. |
      |describe |Optional. The description information can be used to search the allowlist in the allowlist, and the description content should not exceed 200 characters in length. |
      |Internet Protocol Address |Required. Only IP addresses added to the allowlist can access the instance. Support pasting IP addresses or address segments, separated by Chinese and English commas, spaces or newline characters. |
