---
title: "Enabling public network access"
product: "RDS for PostgreSQL"
product_code: "RDS_for_PG"
source: "https://docs.byteplus.com/en/docs/RDS_for_PG/enabling_internet_access"
---

PostgreSQL supports two types of address: private network and public network. To access via the public network, you need to apply for a public network address. This topic describes the procedure to enable public network access.

<span id=".6LS555So6K-05piO"></span>
## Fee description


* The public network address is associated with an [Elastic IP Address (EIP)](https://docs.byteplus.com/en/docs/eip/What-is-EIP) . Using an EIP is billed according to EIP billing standards. For more billing information about public network IPs, refer to [Elastic IP Address](https://docs.byteplus.com/en/docs/eip/Billing-overview).

* A pay\-as\-you\-go EIP enters the **Closed** status after it falls into arrears for two hours and is automatically disassociated from resources. If your PostgreSQL instance is associated with a pay\-as\-you\-go EIP, you are recommended to pay close attention to the account balance and top it up in good time to avoid unavailability of the instance public address due to arrears. For more information about public IP address billing, refer to [Elastic IP Address](https://docs.byteplus.com/en/docs/eip/Arrears).

* An instance enters the closed status when the account is in arrears for 2 hours. During this period, if you recharge the account and after settling the outstanding fee bill and the available quota is greater than 0, the instance status will automatically be restored to **Running**. However, the EIP that has been released will not be re\-associated with the instance. You need to re\-enable public network access for the instance and associate the EIP again.


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

An instance is created and in the **Running** state. For more details, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_PG/creating_an_instance).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Login to the [RDS for PostgreSQL console](https://console.byteplus.com/db/rds-pg).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If the project of the instance has not been set, the project should be selected as <strong>All resources</strong>.   </div>
   

3. Go to the **Instances** page and click on the target instance name to open the **Summary** page.

4. Click the **Connectivity** tab at the top of the page.

5. Go to the **Connectivity** tab and hover over the target endpoint card in the **Instance topology** section. Click **Enable public network access** in the pop\-up window to open the **Enable public network access** page.

6. Select an existing EIP on the **Enable public network access** page.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you haven't applied for any EIPs, click <strong>Apply for public IP</strong> at the top of the list. For more information about public IP address billing, refer to <a href="https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP">Elastic IP Address</a>.   </div>
   

7. After selecting the target EIP, click **OK**.
