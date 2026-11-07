---
title: "Alert"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-alarm"
---

To detect and address application issues before users notice, set up alerts for any metric in the BytePlus VOD quality platform to get proactive notifications when problems are indicated.

This guide shows you how to add alert contacts, create SDK/OpenAPI alert rules, and view alert history.

<span id="ff39a0b9"></span>
## Prerequisites

Before creating an alert rule, you must complete the necessary setup for your chosen notification channel. The required steps vary depending on the method you select, as outlined below.

<span id="22a58929"></span>
### **Email notifications**

To receive alerts via email, you must first add alert contacts:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Quality insights \> Alert** on the left navigation bar.

3. Click the **Alert contacts** tab, and select your app name from the drop\-down list.

4. Click **Add alert contact.** 

5. In the dialog box that appears, fill in the alert contact information, including the contact name, E\-mail, and group.

6. Click **Confirm**.


<span id="063ea2ca"></span>
### **Slack notifications**

To receive alerts in a Slack channel, you must first generate an incoming Webhook URL for that channel. For instructions on generating a URL, see [Slack documentation](https://www.google.com/url?sa=E&q=https%3A%2F%2Fapi.slack.com%2Fquickstart%23webhooks).

<span id="b125e7cb"></span>
### **Lark group notifications**

To receive alerts in a Lark group, you need to obtain a Webhook URL by adding a custom bot to the group. You can add a maximum of five webhook addresses. The following steps display how to obtain the Lark group Webhook URL:


1. Invite a Custom Bot to the Group

   1. Enter the target group, open **Settings**, find **Bots**, click **Add Bot**, and select **Custom Bot** to join the group chat

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0982b30e976248b8971c3200fade0ace~tplv-goo7wpa0wc-image.image) </span>

   2. Enter a name and description for your bot. You can also upload an avatar, and then click **Add**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b61f742afac548dbba0426d974797ad6~tplv-goo7wpa0wc-image.image) </span>

2. Get the Webhook: You need to copy and record the automatically generated **Webhook URL**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08acc38c4d2f4eada7c96ed528ac528f~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Please save this Webhook URL securely and do not publish it on publicly accessible websites like GitLab or blogs, to prevent malicious calls from sending spam messages after the URL is leaked.   </div>
   

<span id="9e2b5076"></span>
## Creating an alert rule


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Quality insights** \> **Alert** on the left navigation bar. BytePlus VOD supports two types of alert rules:



<Tabs>
<Tab zoneid="NaLlG9Uqaq" title="SDK alert">
<TabTitle>SDK alert</TabTitle>

3. On the **SDK alert** tab, click **Create alert rule**.

4. Enter the alert name. It is recommended to use a name that can identify the rule, and the maximum length cannot exceed 64 characters.

5. Configure the scope for the alert rule.

   * App name : Select your app name from the drop\-down list.

   * Platform type : Select the platform type from the drop\-down list.

      * **Mobile**

      * **Web**

   * Metric type : Choose to monitor playback metrics or upload metrics.

   * System type : Select the appropriate operating system from the drop\-down list according to the client type:

      * If you select **Mobile** as the client type, the options are Android or iOS.

      * If you select **Web** as the client type, the options are Android, iOS, Linux, Mac, and Windows.

   * Metric : Select the metrics that you want to monitor.


</Tab>
<Tab zoneid="LXAYJxqJaq" title="OpenAPI alert">
<TabTitle>OpenAPI alert</TabTitle>

3. On the **OpenAPI alert** tab, click **Create alert rule**.

4. Enter the alert name. It is recommended to use a name that can identify the rule, and the maximum length cannot exceed 64 characters.

5. Configure the scope for the alert rule.

   * Alert object : Select the API operations from the API drop\-down list.

   * Metric : Select the metrics that you want to monitor.

      * OpenAPI failure request count

      * OpenAPI rate limit request count


</Tab>
</Tabs>



6. Set the monitoring rules.

   1. Select how often the alert rule is to be run. The options include:

      * 5 minutes

      * 1 hour

      * 1 day

   2. Select **Alert dimension**. You can configure it to send notification based on the specific dimensions when the alert rule is met.

   3. Click **Add filter (dimension)** . The data will be filtered by dimension. You also need to select the operator you want to apply to the dimension and select which dimension values you want to apply to the filter.

7. Set the alert rules. BytePlus supports two alert modes: smart alert and custom alert. Smart alert uses algorithms to continuously learn the metric's behavior patterns and calculate the appropriate thresholds for unexpected behavior. Custom alert evaluates the rule using the threshold value you configure.

   * If you choose **Smart alert**, you need to do the following:

      * Set the threshold value. The default value is 0, meaning that the appropriate thresholds will be calculated and applied to the metric.

      * Set the time range to include in the results.

      * Select the operator to compare the metric value against the threshold:

         * The metric surges.

         * The metric suddenly fluctuates.

         * The metric plummets.

   * If you choose **Custom alert**, you need to choose **Threshold**, **Fluctuation**, or **Trend** and set the alert logic accordingly.

8. Preview alert metrics.

9. Configure alert notifications:

   1. **Select alert method**: Select Email, Slack, or Lark group as your notification channel. The setup steps vary depending on the method you chose. See [Prerequsites](https://docs.byteplus.com/docs/byteplus-vod/docs-alarm#ff39a0b9).

   2. **Select recipients**: Specify who should receive alert notifications.

   3. **Set re\-alert interval**: This setting specifies how often a reminder notification is sent if an alert remains unresolved. The default interval is **30 minutes**. For example, a notification will be sent again 30 minutes after the initial alert if the issue persists.

10. Click **Save**. After your alert rule is successfully created and its conditions are met, you will receive a notification similar to the example below.


```Plain
[BytePlus VOD Quality Insights] The alert rule "test_slack" was triggered at 2025-08-26 07:10:00. For more details, log in to the BytePlus console (https://console.byteplus.com/vodpaas/quality_control/history/)
```


<span id="342a680c"></span>
## Viewing alert history


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Quality insights \> Alert** on the left navigation bar.

3. Click the **Alert history** tab to view the alert history of each app. You can do the following:

   * Search for a specific alert by name.

   * View alert history for the last 1, 15, or 30 days.

   * Click **Details** to view the details of the alert.
