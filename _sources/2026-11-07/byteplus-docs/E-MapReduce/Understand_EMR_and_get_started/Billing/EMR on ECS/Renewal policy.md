---
title: "Renewal policy"
product: "BytePlus EMR"
product_code: "E-MapReduce"
source: "https://docs.byteplus.com/en/docs/E-MapReduce/Renewal_policy"
---

This article provides a note on the renewal feature for subscription clusters.

<span id="cd13e1ee"></span>
## Renewal note

Before a subscription cluster is automatically released, you can renew the cluster manually or automatically. Once automatic renewal is enabled, the system will automatically renew your resources before they expire. You do not need to perform any manual operations, and you no longer need to worry about your resources or data being deleted due to late renewal. This article introduces how to manually and automatically renew EMR clusters, as well as the corresponding steps to cancel automatic renewal.

<span id="79460473"></span>
### Prerequisites


* Clusters pending renewal must have the payment type set to Subscription, and the cluster status must be in normal **running** status.

* Automatic renewal supports the use of coupons.

* After automatic renewal is enabled, please always ensure that your account balance remains sufficient.


<span id="ff4e0cf8"></span>
### Manual renewals

<span id="e7493f16"></span>
#### Procedure


1. Log in to the **EMR Console**.

2. In the left navigation pane, click **Resource Management \> on ECS,**  then on the cluster list page, click the **Renew** button in the cluster actions for the target cluster.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b590795917ce410284349fc5d7a5f68c~tplv-goo7wpa0wc-image.image) </span>


3. Navigate to **Fee Center \- Renewal Management** and confirm the renewal information. Cluster resources, including E\-MapReduce, Cloud Server ECS, Elastic Block Storage, Public IP, and other resources, must be renewed simultaneously.

4. Select "**I have read the renewal instructions and agree to proceed with the above actions**", click to pay, and follow the on\-screen instructions to complete the payment.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/755c8d6695ca4b3f8a3416e4319e2280~tplv-goo7wpa0wc-image.image) </span>


5. After the payment is successful, on the **Cluster Overview** page, the expiration time of the renewed cluster will be updated to the expiration time after renewal.


<span id="8a6faf9d"></span>
#### Unify expiration dates

The unified renewal expiration date feature allows you to renew multiple monthly (non\-calendar month) instances so that they all expire on a fixed day each month. After configuration is completed, the setting applies to all monthly subscription instances that are not based on the calendar month. During each manual renewal, you can choose whether to align with the unified expiration date that has been set.

For operation methods, please refer to [Unified expiration day](https://docs.byteplus.com/zh-CN/docs/byteplus-platform/docs-unified_expiration_day).

<span id="afe6057f"></span>
#### Specify the expiration time

Manual scaling of node groups in an EMR cluster during use can result in newly purchased instances having expiration dates that do not match the cluster's expiration date. This issue can currently be resolved by specifying the expiration date, that is, by renewing the subscription so that all instances with monthly subscriptions (not based on calendar months) have expiration dates that are exactly the same down to the year, month, and day.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The earliest date for setting the expiration time is 23:59:59 on the date that is one month after the latest expiration date among the renewal instances.</div>


* <div data-tips="true" data-tips-type="tip">After you specify the expiration date, the renewal billing period will be calculated to the exact day, with the monthly price prorated to a daily rate. Please refer to the order confirmation page for the final renewal amount.</div>


* <div data-tips="true" data-tips-type="tip">Only instances with non\-calendar\-month subscriptions can specify the expiration time during manual renewal. Instances with daily or calendar\-month subscriptions do not support this feature at this time.</div>


* <div data-tips="true" data-tips-type="tip">You can specify the expiration date only when renewing manually. Automatic renewal will continue to follow the preset single renewal cycle.</div>



**Procedure**


1. Log in to the [EMR Console](https://console.byteplus.com/emr/).

2. In the left navigation pane, click **Resource Management \> on ECS,**  on the cluster list page, click the **Renew** button in the **Actions** column of the target cluster.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/30d1ba6885e84a779d60e0ee5bd41737~tplv-goo7wpa0wc-image.image) </span>


3. On the **Billing Center \- Renewal Management** page, select **Specify expiration date**, and then choose the specific date to renew until.

4. Click "**Proceed to payment**" and complete the renewal.


<span id="79d9f495"></span>
### Automatic renewals

Before your subscription instance expires, you can enable automatic renewal. Seven days before the instance expires, the system will automatically deduct the renewal fee from your account balance. Please ensure that your balance is sufficient. You can also select the "Auto\-renewal" option when purchasing a Subscription cluster. You can also enable automatic renewal after purchasing a subscription cluster.

After enabling automatic renewal, if there are available vouchers in your account, the system will give priority to using vouchers for renewal.


|**Scenario** |**Operation** |
|---|---|
|Enable automatic renewal when purchasing subscription clusters |1. Log in to [EMR Console](https://console.Byteplus.com/emr/).<br><br>2. In the left navigation pane, click **Resource Management \> ECS \> Create Cluster.** <br><br>3. In Create Cluster \> Hardware Configuration \> Billing Settings, enable the auto\-renewal switch. |
|Enable auto\-renewal after purchasing a subscription cluster |1. Log in to the [EMR Console](https://console.volcengine.com/emr/).<br><br>2. In the left navigation pane, click **Resource Management \> on ECS,** . On the cluster list page, click the cluster ID of the target cluster.<br><br>3. On the cluster overview page, enable the auto\-renewal switch in the billing information module.<br><br>4. In the popup prompt, click OK to confirm that you want to enable auto\-renewal.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">After automatic renewal is enabled, your account will be automatically charged seven days before the cluster expires, and each renewal is for a period of one month.</div><br><br><br><div data-tips="true" data-tips-type="tip">The automatic renewal payment date can be adjusted. For details, see <a href="https://docs.byteplus.com/docs/E-MapReduce/109016#78895cfc">The automatic renewal deduction date</a>.</div><br><br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/62b0d88c57324d5b8620eed56a937932~tplv-goo7wpa0wc-image.image) </span> |


<span id="78895cfc"></span>
#### The automatic renewal deduction date

For detailed instructions, see [Cost Center - Renewal Management - Automatic Renewal Deduction Date](https://docs.byteplus.com/zh-CN/docs/byteplus-platform/docs-auto-renewal-billing-date).

<span id="e59743b7"></span>
### Cancel automatic renewal

If you no longer need the instance to be automatically renewed after the current billing cycle ends, you can cancel automatic renewal in advance. After you enable automatic renewal, the system will start automatically deducting payment seven days before the instance expires. If you need to cancel automatic renewal, please do so before the automatic payment is processed.


1. Log in to [EMR Console](https://console.Byteplus.com/emr/).

2. In the left navigation pane, click **Resource Management \> on ECS,**  and on the cluster list page, click the cluster ID of the target cluster.

3. On the cluster overview page, turn off the auto\-renewal switch in the billing information module.

4. In the popup prompt, click **OK** to confirm turning off auto\-renewal.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">After disabling automatic renewal, you must manually renew the cluster before it expires; otherwise, after overdue payment, the cluster will enter a shutdown state.</div>
