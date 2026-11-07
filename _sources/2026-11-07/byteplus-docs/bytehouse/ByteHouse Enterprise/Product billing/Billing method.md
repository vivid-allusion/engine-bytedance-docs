---
title: "Billing method"
product: "ByteHouse"
product_code: "bytehouse"
source: "https://docs.byteplus.com/en/docs/bytehouse/billing-method"
---

ByteHouse Enterprise edition's billing units include **clusters** and **cold storage**.

<span id="af745b82"></span>
# Cluster billing

A ByteHouse cluster provides a complete set of data management, data import, and data query services. Between different clusters, data is isolated (cluster A cannot access data of cluster B), and the performance of queries and imports are also isolated (queries and imports of cluster A do not affect the performance of cluster B).

The billing method for ByteHouse clusters is **annual and monthly subscription**.

Annual and monthly subscription is a pay\-first, use\-later billing method, helping you save more money, suitable for long\-term usage scenarios.

By purchasing the annual and monthly subscription model of ByteHouse Enterprise clusters, you can enjoy a more favorable price compared to the pay\-as\-you\-go model (the pay\-as\-you\-go model will be supported in the future, stay tuned). On the BytePlus platform, when you purchase cloud servers for more than a year, you can enjoy the annual discount given by the platform, which makes annual and monthly subscription cloud servers your best choice for long\-term stable operations.

After activating the annual or monthly subscription service, if there is an unpaid balance in your account, you can still use the purchased annual or monthly clusters as usual. However, when you buy a new cluster and settle the bill, you will need to pay off the due amount in your account.

<span id="计费介绍"></span>
## Billing introduction

Annual and monthly clusters support monthly purchasing options (ranging from 1 to 9 months) and annual purchasing options (1 to 3 years). Please refer to the actual order settlement page for specific discounts. Once the fees are paid, you can begin using the annual or monthly resources immediately.

<span id="结算周期"></span>
## Billing period

The billing period for annual or monthly clusters corresponds to the duration of your purchase, based on UTC+8 time. It starts at the time resources are activated (down to the second) and ends at 23:59:59 on the expiry date.

For example, if you create an annual or monthly cluster on July 1, 2021, at 14:00:00 and purchase it for a duration of one month, the billing period is from July 1, 2021, 14:00:00 to August 1, 2021, 23:59:59.

If the available credit in your account (including account balance and vouchers) is less than the pending bill, it will be considered overdue, and you will receive a reminder via SMS or email for insufficient balance. You can refer to [Bill Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-having-an-overview-of-bills) to view the details of the overdue amount.

<span id="续费说明"></span>
## Renewal explanation

You can refer to this operation for annual and monthly cluster subscription renewals in the following scenarios. Currently, both automatic renewal and manual renewal methods are supported.


* Before the cluster expires

* After the cluster expires, it enters the "Expired Retention" state.

* After unsubscribing from a cluster, its billing status changes to "Unsubscribed".


When renewing during the resource retention period, the renewal period starts from the **original resource expiration date/unsubscription time** and is included in the renewal bill. After a successful renewal, the shut down cluster will automatically restart and enter the "Running" state. If restarting fails, please go to the [Console](https://console.byteplus.com/ecs/instance) and click on "Support \> Create New Ticket" at the top navigation bar to get support.

<span id="手动续费"></span>
### Manual renewal


1. Log in to the ByteHouse Corporate Console.

2. Default to the "Manage Clusters" page, where you can select "Cluster Details" for the corresponding cluster to see the renewal operations.

3. Jump to the renewal management page and confirm the cluster information to be renewed.

4. Select the renewal duration and amount.

5. Check the box that says "I have read the renewal instructions and agree to the above actions", and click the "Go to Pay" button.

6. Click "Next", submit payment information, then click "Go to Pay" to pay the fee.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you have coupons available, you can select the coupons to use and then apply them to offset the payment</div>


<span id="自动续费"></span>
### Automatic renewal

You can activate automatic renewal before the annual and monthly clusters expire. 7 days before the cluster expires, the system will automatically deduct the renewal cost from your account balance, so please ensure sufficient balance. You can also check the "Automatic renewal" option when purchasing an annual and monthly cluster. For detailed operations, please refer to [Automatic Renewal](https://docs.byteplus.com/en/docs/byteplus-platform/docs-overview-of-renewal-rules).

After enabling auto\-renewal, if there are available vouchers in your account, the system will prioritize using these vouchers for renewal.


* Resources with auto\-renewal enabled can be renewed manually at any time. Even after a successful manual renewal, auto\-renewal remains effective, and the system will start debiting 7 days before the new expiration date of the resource.

* Clusters that have expired are not allowed to enable or modify auto\-renewal.


<span id="到期处理"></span>
## Expiration processing

If a cluster on an annual or monthly plan is not renewed after expiration, your resources will enter a retention period, during which resource usage will be limited. After exceeding the resource retention period, your resources will be forcibly reclaimed, and once reclaimed, they cannot be restored. Please renew on time within the specified period (before the forced reclamation of resources) to avoid inability to use the ByteHouse cluster normally. [Renew](https://docs.byteplus.com/en/docs/ecs/Renewal-and-unsubscription) You can view the expiration dates of annual or monthly clusters on the Cluster List Page.

<span id="ffa9c409"></span>
### **Expiration release description**


* Expiration moment: 23:59:59 on the day of expiration.

* Shutdown time: 12 hours after expiration. (After shutdown, if not renewed, clusters cannot be launched, and data will be temporarily retained)

* Release time: 15 days after expiration. (After release, data cannot be retrieved)


<span id="500fea4a"></span>
### **Resource status explanation**

More than 12 hours after the cluster expiration, the cluster status in the cluster list will be "Stopped", and the "Billing method" for the annual/monthly clusters will display "Retain temporarily".

<span id="2fd9e11e"></span>
## Unsubscribe

For annual and monthly clusters not yet expired, if you wish to release them early, you can apply to unsubscribe from the cluster, and it can be restored through renewal after unsubscribing.

<span id="5cf260c6"></span>
### Unsubscribe description

Annual and monthly clusters support unsubscribe operations before expiration; you can apply for an unsubscribe in BytePlus Console [Cost > Unsubscribed Management](https://console.byteplus.com/finance/unsubscribe/). After a successful cancellation, BytePlus will refund the actual amount paid (excluding deductions from vouchers) for the order to your BytePlus account balance based on the type of cancellation and corresponding rules. Vouchers already used cannot be refunded. For more content, please refer to [Unsubscription Management](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management).

After unsubscribing from a cluster, the state of the cluster becomes "Stopped" and it is shut down. Under the billing type, it will display "Unsubscribed", and related resources will enter a retention period of 14 days. You can renew and restore the unsubscribed resources within this retention period. After the retention period, unsubscribed resources will be recycled and cannot be restored. Please proceed cautiously and back up important data in time.

<span id="7832f745"></span>
### Unsubscription type

Currently, annual and monthly clusters support **non\-seven\-day refund rules**. Non\-seven\-day refund rules will charge based on the actual duration of resource usage, and the remaining actual fees paid for the order will be refunded. For specific refund amounts, please refer to the amounts displayed on the Console. For more unsubscription rules, please refer to [Non-seven-day refund rules](https://docs.byteplus.com/en/docs/byteplus-platform/docs-unsubscription-management#ii-non-seven-day-refund-policy).

<div data-tips="true" data-tips-type="danger" data-tips-is-title="true">danger</div>


<div data-tips="true" data-tips-type="danger">Should there be any suspected abnormal or malicious unsubscribe actions, BytePlus has the right to refuse your unsubscribe request</div>


<span id="483941f4"></span>
# Cold storage billing

<span id="28191959"></span>
## Billing introduction

Cold storage adopts a pay\-as\-you\-go billing mode. Pay\-as\-you\-go is a post\-use prepayment billing method. BytePlus platform calculates costs based on the actual resources you use, achieving true pay\-as\-you\-use. Settlement costs are calculated by duration and the storage capacity of cold storage, with billing by the second. Below is an introduction to the billing and settlement rules for cold storage.

<span id="568b8aac"></span>
## **Purchase requirements**


* Your account needs to complete real\-name authentication before you can enable cold storage.

* When enabling cold storage, the total value of your account balance (i.e., cash balance) and vouchers must not be less than 100.00 Yuan RMB.


<span id="0e837979"></span>
## **Settlement period**

The billing type for cold storage is pay\-as\-you\-go, with a daily settlement (around UTC+8 9:00) of the previous day's usage, generating a bill and deducting fees.

If the available credit in your account (including account balance and vouchers) is less than the pending bill, you will receive an SMS or email reminder of insufficient balance.

Billing method: The system obtains the usage value once every hour (accurate to 0.01 GiB), and the total charges of all hourly points for the day constitute the total daily cost. For more details, please see [Cold Storage Billing Example](https://docs.byteplus.com/docs/bytehouse/pricing-rules#3db72f35).

<span id="0bcba7f4"></span>
## Handling overdue payments

After your account is overdue, data in your cold storage will enter a retention period and access will be restricted. After exceeding the resource retention period, your resources will be forcibly reclaimed and cannot be restored once reclaimed.


1. Please recharge and settle the overdue bill within 24 hours of incurring debt, otherwise you will not be able to normally use the cold storage service.

2. **If the debt exceeds 24 hours, cold storage access will be suspended. Data is retained and continues to be billed:** 

   1. Your cluster will automatically restart to pause cold storage

   2. Some data in the tables on cold storage will be marked as "broken" (which can be queried in system.broken_tables) and those tables will not be accessible for reading or writing

   3. Your data will be retained and continue to accrue costs, thus overdue charges will accumulate

3. If you recharge and restore the service, the cluster will restart again and normal access will be restored

4. **If you haven't paid off the outstanding amount within 15 days after the service suspension, it will be considered an abandonment of the service by you; BytePlus will terminate the service agreement for this product, and all your data stored in cold storage will be deleted and cannot be recovered.** 


<span id="9fe57f00"></span>
## Unsubscribe

Once cold storage is activated, it cannot be temporarily Unsubscribed.

You can stop billing by emptying the data into cold storage.
