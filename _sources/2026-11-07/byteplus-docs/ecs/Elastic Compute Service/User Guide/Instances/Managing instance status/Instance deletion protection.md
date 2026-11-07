---
title: "Instance deletion protection"
product: "Elastic Compute Service"
product_code: "ecs"
source: "https://docs.byteplus.com/en/docs/ecs/Instance_delete_protection"
---

<span id="LrOzBAuy"></span>
## Applicable scenarios

If your Pay\-as\-you\-go instance carries critical services, you can enable instance deletion protection for it. After being enabled, this function prevents accidental deletion of instances through the console or API, effectively avoiding irreparable consequences due to operational negligence or untimely communication among team members. This topic describes how to set instance deletion protection in the Elastic Compute Service (ECS) console and view the protection status of an instance.

<span id="Qob1yE9F"></span>
## Precautions


* Only [regular Pay-as-you-go instances](https://docs.byteplus.com/en/docs/ecs/Pay-as-you-go) support enabling instance deletion protection.

* Instance deletion protection does not prevent automatic deletions performed by the system for justifiable reasons, including but not limited to:

   * Instances being automatically released due to Account Overdue.

   * Instances that are identified as having security or compliance risks may be stopped or released.


<span id="MZpBuF4e"></span>
## Procedure


<Tabs>
<Tab zoneid="Ax7nLctO7W" title="Enable deletion protection when creating an instance">
<TabTitle>Enable deletion protection when creating an instance</TabTitle>

The following section describes the configurations related to instance deletion protection. For more parameter configurations, see [Purchasing an instance by following the wizard](https://docs.byteplus.com/en/docs/ecs/Using-the-wizard-to-buy-ECS-instances).


1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. Click the "Create instance" button to purchase an ECS instance.

4. On the **Custom configuration** page, check "Prevent accidental deletion through the console or API" (disabled by default).

5. Configure remaining parameters to complete the purchase.


</Tab>
<Tab zoneid="JF1i4BRFBd" title="Change instance deletion protection status">
<TabTitle>Change instance deletion protection status</TabTitle>

1. Log in to the [ECS console](https://console.byteplus.com/ecs/instance). 

2. In the left\-side navigation pane, select "Instances & Images \> Instances".

3. Click the "··· \> Instance settings \> Modify instance delete protection" button in the "Actions" column to the right of the target instance.

4. In the pop\-up dialog box, select "Open" or "Close" to enable or disable instance deletion protection.

5. Click "Confirm" to complete the operation.


</Tab>
</Tabs>


<span id="LNzN4bE5"></span>
## View the status of instance deletion protection

You can click the target instance to enter the instance Overview page, and view the status of instance deletion protection in the **Basic information** section. Instances with deletion protection enabled cannot be directly deleted through the console or API; you need to disable this feature before performing the delete operation.
