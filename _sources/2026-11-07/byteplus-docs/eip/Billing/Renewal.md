---
title: "Renewal"
product: "Elastic IP Address"
product_code: "eip"
source: "https://docs.byteplus.com/en/docs/eip/Renewal"
---

For Subscription Elastic IP Addresses (EIPs), BytePlus VeManager platform sends SMS, email, or internal message reminders based on your reminder settings 7 days, 3 days, 1 day before expiration and on the expiration date to notify you of the impending expiration. To avoid disrupting your business, renew promptly after receiving the expiration notice.


* You cannot modify the bandwidth limit of the EIP during renewal. If needed, make any changes after renewal.

* If you renew before suspension at expiration (within 12 hours after expiration), the renewal period starts from the original expiration time; if renewed after suspension but before resource reclamation, the renewal starts from the actual renewal time.


<span id=".5omL5Yqo57ut6LS5"></span>
## Manual renewal

You can manually renew the EIP at any time before resource reclamation after expiration.

<span id="IV9yMNNc"></span>
### Procedure


1. Log in [to the EIP console](https://console.byteplus.com/eip/eips). 

2. In the top menu bar, select the region and project.

3. In the EIP list, click  **··· \> Renew** to the right of the target EIP.

4. Confirm the details of the EIP to be renewed. When you renew the EIP, the subscription Elastic Compute Service (ECS) instance associated with the EIP can be renewed as needed.

   > When renewing a Subscription ECS instance, the mounted Subscription Volumes are renewed accordingly.   
   

5. Select the renewal period, read and confirm the related agreement, then click **Pay**.

6. Click **Next**, select the payment method, then click **Pay**.

7. Make the payment by the selected method. After submitting the payment information, complete the payment within the specified time. Otherwise, the order will be canceled.


<span id=".6Ieq5Yqo57ut6LS5"></span>
## Automatic renewal

You can select the **Automatic renewal** option when applying for a Subscription EIP. You can also enable automatic renewal before the Subscription EIP expires. For detailed actions, refer to Automatic renewal.

After enabling automatic renewal, if you have available vouchers in your account, the system will prioritize using them for renewal.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For resources with automatic renewal enabled, you can manually renew them at any time. Manual renewal does not invalidate automatic renewal. The system will charge 7 days before the resource's new expiration date.</div>


* <div data-tips="true" data-tips-type="tip">You cannot enable or modify automatic renewal for expired EIPs.</div>
