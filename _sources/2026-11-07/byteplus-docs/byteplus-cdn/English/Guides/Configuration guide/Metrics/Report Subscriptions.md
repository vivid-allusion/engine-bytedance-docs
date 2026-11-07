---
title: "Report Subscriptions"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/report-subscription_en-us"
---

BytePlus CDN provides report subscription functionality. You can subscribe to metrics that you are interested in from the "Edge Report", "Traffic Hit Ratio", "Origin Report", "Popular Objects", and "Insights" pages. CDN will regularly send metric data to your specified email address, allowing you to stay informed about your business status. The reports are sent in PDF format.

When creating a subscription, you need to specify the email address for receiving reports, delivery frequency, domain names, and report contents. A primary account can create up to 25 subscriptions. Each IAM user can create up to 5 subscriptions. IAM users can only create subscriptions for resources they have permission to access.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">On the <strong>Create Subscription</strong> page, you can click the link in the lower\-left corner to preview the report.</div>


<span id="procedure"></span>
## Procedure


1. Log in to the [BytePlus CDN Console](https://console.byteplus.com/cdn).

2. In the left navigation pane, click **Report Subscriptions**.

   <span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_bc470b44a52f49af032924dc1c5555e1.png) </span>

3. On the **Report Subscriptions** page, click **Create Subscription**.

4. On the **Create Subscription** page, configure the settings according to the field descriptions.

5. After completing the settings, click **OK**.


You can click the link in the lower\-left corner to view a sample report.

<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_cf6e35f2a5c85266e495e33be81bcce5.png) </span>

<span id="field-descriptions"></span>
### Field descriptions


|**Field** |**Description** |
|---|---|
|Subscription Name |The name can contain Chinese characters, letters, numbers, and underscores (_), with a length between 3\-45 characters. Each Chinese character counts as 3 characters toward the length limit. |
|Recipient Emails |The email addresses that will receive the reports. You can add up to 5 email addresses. |
|Delivery Frequency |The frequency of report delivery. This field has the following options:<br><br><br>* **Daily**: CDN sends the previous day's report to your specified email address around 10:00 AM each day.<br><br>* **Weekly**: CDN sends the previous week's report to your specified email address around 10:00 AM every Monday.<br><br>* **Monthly**: CDN sends the previous month's report to your specified email address around 10:00 AM on the first day of each month. |
|Domain Names |The domains for which you are subscribing to metrics. This field has the following options:<br><br><br>* **All**: All domains under your account.<br><br>* **Specified Domain Names**: The specified domains you select. You can specify up to 200 domains. |
|Report Contents |The metrics to include in the report. |


<span id="view-subscriptions"></span>
## View subscriptions

The primary account can view all subscriptions. If any subscriptions were created by IAM users, a **Creator** column is displayed to identify them. This column is hidden if all subscriptions are created by the primary account.

When an IAM account opens the **Report Subscriptions** page, it only displays the subscriptions created by that IAM account.

<span id="subscription-operations"></span>
## Subscription operations

Your created subscriptions appear in the subscription list. You can perform the following operations on these subscriptions:


* Modify: Change a subscription's configuration.

* Disable/Enable: Disable or re\-enable subscription. When you disable a subscription, CDN will not send reports to the email addresses specified in the subscription.

* Delete: Delete a disabled subscription.


<span>![图片](https://sf16-resources.bytepluscdn.com/obj/byteplus-public-aiso/cloud-universal-doc/upload_b0a668c5f2aa7a0c6f8672d2ac1ad583.png) </span>
