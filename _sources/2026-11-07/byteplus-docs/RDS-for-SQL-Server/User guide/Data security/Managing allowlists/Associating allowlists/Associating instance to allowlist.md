---
title: "Associating instance to allowlist"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/associating-instance-to-allowlist"
---

After adding an IP to the allowlist, you also need to bind the allowlist to the instance in order for the device to which the IP address belongs to successfully access the SQL Server instance. Since allowlists and instances have a "many\-to\-many" correspondence, you can bind allowlists from instances, or you can bind instances from allowlists. This article describes how to bind an instance to the allowlist.

<span id="background-information"></span>
## **Background information**


* Whether accessing an instance through a VPC intranet or a public network connection, you need to configure the allowlist of the instance first to ensure that the instance can be connected.

* Please maintain the allowlist regularly to clear the IP addresses of devices that do not require access to SQL Server instances to ensure the security of database connections.


<span id="precautions"></span>
## **Precautions**


* A single instance can bind up to 100 IP allowlists, with each allowlist supporting up to 300 IPs or IP segments. When there are many IP addresses, it is recommended to merge the fragmented IP into IP segments, such as `10.10.10.0/24`.

* Each allowlist can be bound to up to 500 instances.

* Setting up the allowlist does not affect the normal operation of your SQL Server instance.


<span id="prerequisite"></span>
## **prerequisite**

The [instance was created ](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide)and is **in the running** state.

<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the target project and region.

3. Click **Allowlist list** in the left navigation bar.

4. Click on the target allowlisted **Associate instance** to go to the **Associate instance** page.

5. On the **Associate instance** page, in the Instances list, check the target instance and click **OK** to complete the binding.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can quickly locate the target instance by searching for the instance name or instance ID.</div>
