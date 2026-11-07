---
title: "Enabling public network access"
product: "RDS for SQL Server"
product_code: "RDS-for-SQL-Server"
source: "https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/enabling-public-network-access"
---

RDS for SQL Server supports both private and public network access. If you need to access through the public network, you need to apply for a public network address. This article describes the steps to enable public network access.

<span id="fee-description"></span>
## fee description


* The public network address will be bound to the [public network IP ](https://docs.byteplus.com/en/docs/eip/What-is-EIP)(Elastic IP Address, referred to as EIP), and the use of EIP will be billed according to the EIP billing standard. For more information on public network IP billing, please refer to the [Public Network IP Billing Overview](https://docs.byteplus.com/en/docs/eip/Billing-overview).

* The EIP billed by the amount will enter the **shutdown** state after 2 hours of arrears to stop providing services, and automatically unbind the bound resources. If your SQL Server instance is bound to a volume\-based EIP, it is recommended that you pay close attention to the account balance and recharge it in time when the balance is insufficient to avoid the instance's public network access address being unavailable due to account arrears. For more details, see [Public IP Arrears Description](https://docs.byteplus.com/en/docs/eip/Arrears).


<span id="precautions"></span>
## Precautions

Read\-only instances also support access to data through both public and private networks. When you need to read data from the public network, you need to enable public network access for the read\-only instance on the **connection management** tab of the read\-only instance.

<span id="prerequisite"></span>
## **prerequisite**

An instance has been created and is **in the running** state. For details, see [Creating an instance](https://docs.byteplus.com/en/docs/RDS-for-SQL-Server/creating-instance-for-user-guide).

<span id="operation-steps"></span>
## **Operation steps**


1. Log in to [RDS for SQL Server console](https://console.byteplus.com/db/sql-server).

2. In the upper left corner of the top menu bar, select the project and region to which the instance belongs.

3. On the **instance list** page, click the target instance name to go to the **instance information** page.

4. Click on the **connection management** tab, in the **connection management** page signed **connection topology** area, the mouse points to the master node end point card, in the pop\-up window click to **open public network access** , enter the **open public network access** page.

5. On the **Open Public Network Access** page, select the EIP that needs to be bound.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If there is no available EIP, you can click <strong>Apply for Public IP</strong> to enter the <strong>Apply for Public IP</strong> page, apply for a new EIP and then bind. For more information about applying for EIP, see <a href="https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP">Applying for Public IP</a>.   </div>
   

6. After selecting the target EIP, click **OK** .
