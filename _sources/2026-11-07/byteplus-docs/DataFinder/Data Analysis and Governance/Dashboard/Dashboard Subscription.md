---
title: "Dashboard Subscription"
product: "BytePlus DataFinder"
product_code: "DataFinder"
source: "https://docs.byteplus.com/en/docs/DataFinder/Dashboard_Subscription"
---

In some scenarios, we hope to receive our own data on a daily/weekly basis without opening the growth analysis (DataFinder), which can be achieved through the function of Dashboard subscription. This article provides you with instructions on how to subscribe to Dashboard.

<span id="_2-看板订阅说明"></span>
# Function Description


* DataFinder's Dashboard supports image subscription through email/Lark group/DingTalk group, and a single Dashboard board can subscribe up to 20 items.

* Subscription permissions: Users with viewing permissions to the Dashboard board can subscribe.

* Subscription management: Users with edit rights to Dashboard can manage all subscription tasks under the board.

* Subscription\-supported chart types: Currently, subscriptions are only supported for charts created on DataFinder; for charts on other platforms that require dynamic login verification, subscriptions are not currently supported.


<span id="6e1217ec"></span>
# Prerequisite

If you want to subscribe to Dashboard and then push the subscription content to the Lark group, DingTalk group and other enterprise groups, you need to add the webhook of the corresponding group in the DataFinder first, see for details [Webhook Management](https://docs.byteplus.com/docs/DataFinder/Webhook_Management).

<span id="_3-看板订阅操作"></span>
# Operation steps


1. After logging in to the DataFinder console, click the top "Dashboard" navigation to enter the Dashboard page, and click the "Subscribe" button in the upper right corner of the Dashboard page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be668b60806b44bcabc5975210bc153a~tplv-goo7wpa0wc-image.image) </span>

2. Configure subscription task parameters in the "Subscription Settings" tab of the pop\-up subscription configuration window.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d58ba2c631bc47ef9ac96cb850c88e01~tplv-goo7wpa0wc-image.image" width="600px" />   </div>
   

   
   |Parameter |Configuration instructions |
   |---|---|
   |Subscription name |Customize the subscription name of the subscription task. |
   |Push time |Select the push period and specific time for the subscription chart.<br><br><br>* The current support is flexible to choose a time of day, week, or month for routine push.<br><br>* If multiple time zones are enabled, setting the time zone for the corresponding time is also supported. |
   |Push effect |Support to choose to push **pictures** or push **pictures and PDFs** .<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When you choose to push <strong>images and PDFs</strong> , only push to email is supported, not push to enterprise groups.</div><br> |
   |Push method |Currently, push to mailbox or enterprise group is supported. If you need to push to an enterprise group, you need to add a webhook for the corresponding group in the DataFinder first, see for details [Webhook Management](https://docs.byteplus.com/docs/DataFinder/Webhook_Management). |
   |Push failure handling |Configure the processing strategy after push failure. Select whether to retry if push fails and whether to notify the subscription owner.<br><br><br>* If you retry, you currently support retrying once within 30 minutes.<br><br>* If the subscription owner is notified, the subscription task creator is notified via a BytePlus in\-app letter. |
   |Data exception handling |Configure the handling strategy for chart data exceptions in Dashboard. Select whether to push Dashboard when the chart is abnormal and whether to notify the subscription owner.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the chart in Dashboard memory has query timeout, failure, data is not ready, etc., it will be judged as an abnormal scenario.</div><br> |
   

3. Once the configuration is complete, you can click **Send Test** to see if the setup was successful.

4. Click the "Subscription Management" tab at the top to view the current subscription task list, push status, and more. It also supports pausing, editing, and deleting subscription tasks.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6258602d805c46188e9594258173e454~tplv-goo7wpa0wc-image.image" width="600px" />   </div>
   


<span id="03e51e9a"></span>
# Related operations

DataFinder provides you with a project\-level subscription management page. You can view all subscription tasks and push status in the project on the subscription management page, and you can also edit, delete and other management operations on the subscription management page. See the details [Subscription Management](https://docs.byteplus.com/docs/DataFinder/Subscription_Management).
