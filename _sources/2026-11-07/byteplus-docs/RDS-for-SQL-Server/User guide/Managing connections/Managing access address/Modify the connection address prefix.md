---
title: "Modify the connection address prefix"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/modify-the-connection-address-prefix"
---

RDS for SQL Server supports modifying the prefix of the instance connection address. This article describes how to modify the prefix of an instance connection address in the SQL Server Edition console of a cloud database.

<span id="prerequisite"></span>
## prerequisite

An instance has been created and is **in the running** state. For details, see [Create an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide) or [Create a read-only instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-read-only-instance).

<span id="precautions"></span>
## Precautions


* Modifying the prefix of the connection address is supported only. Private network addresses can only end with `. rds-mssql.ivolces.com` suffix, and public network addresses can only end with `. rds-mssql.volces.com` suffix.

* After modifying the connection address, after the new connection address takes effect, the old connection address will expire after 3 minutes. Please modify the connection configuration of the application synchronously before the connection address expires, otherwise it may affect the normal operation of your business.

* If the prefix of the domain name starts with `xn--`, then the prefix of the domain name must comply with the Punycode encoding specification.

* If the instance has SSL encryption enabled, modifying the connection address prefix is not supported. If you need to modify it, please turn off the SSL encryption function of the instance first. For more information about SSL encryption, see [Setting up SSL encryption](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/setting-ssl-encryption).


<span id="operation-steps"></span>
## Operation steps


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the target instance name.

4. On the **Instance Information** tab, click **Connection Management** .

5. In the Connection Topology area of the Connection tab, mouse over the destination connection end point and click the brush icon after the connection address.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you need to modify the connection address of the public network address, you need to apply for the corresponding connection address first. For how to apply for a public network address, see <a href="https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/enabling-public-network-access">Enabling Public Network Access</a>.   </div>
   

6. In the dialog box that pops up, modify the prefix of the connection address. The rules for connection address prefixes are as follows:

   * The prefix should contain at least 8 characters, and the total length of the connection address (including the suffix) should not exceed 63 characters.

   * Begin with a lowercase letter and end with a lowercase letter or number.

   * Consists of lowercase letters, numbers, and a dash (\-).

   * If the prefix of the domain name starts with `xn--`, then the prefix of the domain name must comply with the Punycode encoding specification.

7. Click **OK** .
