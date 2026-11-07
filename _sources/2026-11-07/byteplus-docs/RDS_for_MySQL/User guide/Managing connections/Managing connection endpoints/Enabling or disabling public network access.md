---
title: "Enabling or disabling public network access"
product: "RDS for MySQL"
product_code: "RDS_for_MySQL"
source: "https://docs.byteplus.com/en/docs/RDS_for_MySQL/enabling_internet_access"
---

MySQL supports accessing MySQL instances through the public network. This topic describes the steps to enable public network access.

<span id=".6LS555So6K-05piO"></span>
## Billing

A public network address is associated with an [Elastic IP Address (EIP)](https://docs.byteplus.com/en/docs/eip/What-is-EIP). You will be charged for the EIP based on its billing standards. For more information on public IP billing, refer to [Public IP billing overview](https://docs.byteplus.com/en/docs/eip/Billing-overview).

<span id=".5rOo5oSP5LqL6aG5"></span>
## Precautions


* Since new and old public IPs cannot coexist, for an endpoint with carrier\-provided public network access enabled, you must release the carrier's public IP before associating an EIP. To do this: on the target endpoint, first disable the carrier\-provided public network access, and then re\-enable public network access and associate an EIP.

* After you disable public network access, the public network address is deleted and the associated Elastic IP Address (EIP) is automatically disassociated. Disassociated EIPs will be retained and billing will continue.

* After disabling public network access, you will not be able to access the database through the public network, and the established public network connection will also be disrupted, proceed with caution.

* A pay\-as\-you\-go EIP enters the **Closed** status and stops providing services after 2 hours of arrears. If your MySQL instance is associated with a pay\-as\-you\-go EIP, monitor your account balance and top it up promptly when it is low. RDS for MySQL triggers an "EIP status abnormal" event when the EIP status is abnormal. You can configure an event policy for this event to receive timely notifications. For more information about configuring event policies, refer to [Creating event policy](https://docs.byteplus.com/en/docs/RDS_for_MySQL/Creating_event_policy).


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* The instance has been created and is in the **Running** status. For specific operations, refer to [Creating an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_an_instance_1).

* A database and an account have been created. For details, refer to [Creating a database](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_a_database) and [Creating an account](https://docs.byteplus.com/en/docs/RDS_for_MySQL/creating_and_managing_an_account#创建账号).

* An allowlist has been configured. For details, refer to [Associating an allowlist with an instance](https://docs.byteplus.com/en/docs/RDS_for_MySQL/associating_allowlists_to_instances).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log on to the [RDS for MySQL console](https://console.byteplus.com/db/rds-mysql).

2. In the upper\-left corner of the top menu bar, select the project and region for the instance.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If the project to which the instance belongs is not set, this operation should select the project as <strong>All resources</strong>.</div>



3. Click **Instances** in the left\-side navigation bar.

4. Click the name of the target instance on the **Instances** page to go to the **Summary** page.

5. On the **Connectivity** tab, under **Endpoints**, click **Edit** in the **Actions** column of the target connection endpoint. In the **Modify endpoint** dialog box that appears, complete the following steps to enable or disable public network access.

   * **Enable public network access**

      1. On the **Modify endpoint** page, click the **Enable public network access** button to go to the **Enable public network access** page.

      2. On the **Enable public network access** page, you can select and associate an available EIP. If no EIP is available, click **Apply for public IP** to go to the **Apply for public IP** page to apply for a new EIP, and then associate it. For more information about applying for an EIP, refer to [Applying for public IP](https://docs.byteplus.com/en/docs/eip/Applying-for-an-EIP).

      3. After selecting the target EIP, click **OK**.

   * **Disable public network access**

      1. On the **Modify endpoint** page, click the **Disable public network access** button.

      2. In the pop\-up **Are you sure to disbale public network access?**  **In the dialog box, after confirming the impact of disabling public network access, click Disable** button.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After modifying public network access, the instance state changes to <strong>Network changing</strong>. After public network access is enabled or disabled, the instance state changes to <strong>Running</strong>.</div>


<span id=".55u45YWzLWFwaQ=="></span>
## Related API


|API |Description |
|---|---|
|[CreateDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/RDS_for_MySQL/createdbendpointpublicaddress) |Call the CreateDBEndpointPublicAddress API to create a public network address. |
|[DeleteDBEndpointPublicAddress](https://docs.byteplus.com/en/docs/RDS_for_MySQL/deletedbendpointpublicaddress) |Call the DeleteDBEndpointPublicAddress API to delete a public endpoint address. |
