---
title: "Public network resolution management"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/public-network-resolution-management"
---

The cloud database SQL Server version provides a public network resolution function that enables private network addresses. Through this function, the private network domain name address can be resolved into a private network IP address in a public network environment. This article describes how to enable or disable public network resolution for private network addresses.

<span id="background-information"></span>
## Background information

RDS for SQL Server provides access points for various protocols for your connection. When accessing a private network VPC type access point, the private network domain name needs to be resolved, but the private network domain name must be successfully resolved to the private network IP address in the Byteplus private network environment by default. You can enable the public network resolution function for the instance. After opening, you can successfully convert the private network domain name resolution to the private network IP address even in the public network environment. Public network resolution is suitable for non\-production environment scenarios such as testing environment, such as testing environment directly connecting to cloud database SQL Server version instances, personal devices accessing private network domain names, etc.

<span id="precautions"></span>
## Precautions


* After the private network domain name is resolved by the public network, the Byteplus private network IP address is obtained. Your local environment needs to open the Byteplus private network through VPN and other means, otherwise the private network IP address cannot be successfully accessed.

* Due to the complexity of the public network environment, the accuracy and timeliness of domain name resolution cannot be guaranteed, so this function is recommended for non\-production environments.

* If your primary instance contains a read\-only instance, enable or disable the public network resolution function of the private network address of the read\-only instance, which helps you resolve the private domain name address of the read\-only instance to the private IP address in the public network environment.


<span id="prerequisite"></span>
## prerequisite


* Registered Byteplus account and completed real\-name authentication. For details, see [How to perform account registration](https://docs.byteplus.com/en/docs/byteplus-platform/docs-signing-up-your-account#create-byteplus-account) and [real-name authentication](https://docs.byteplus.com/en/docs/byteplus-platform/docs-getting-started).

* An instance has been created and the instance state is **running** . For more details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).


<span id="operation-steps"></span>
## Operation steps


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. In the left navigation bar, click **Instance List** .

4. On the **instance list** page, click the target instance name.

5. On the **Instance Information** page, click **Connection Management** .

6. In the connection topology area of the connection tab, hover the cursor on the **master node end point** card to turn on or off the public network analysis. The specific operations are as follows:

   * Open public network analysis

      1. In the dialog box that pops up, click **Open Public Network Resolution** .

      2. In the **Open Public Network Resolution** dialog box, click **OK** to open .

   * Disable public network analysis

      1. In the dialog box that pops up, click **Close Public Network Resolution** .

      2. Are you **sure to turn off public network resolution?**  Dialog box, click **OK** to close .
