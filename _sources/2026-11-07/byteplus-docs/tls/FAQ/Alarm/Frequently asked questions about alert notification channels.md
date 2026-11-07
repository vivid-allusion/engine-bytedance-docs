---
title: "Frequently asked questions about alert notification channels"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Alarm-faq"
---

<span id="a2617578"></span>
## Why was an alert triggered but no alert notification received?

After the alarm is triggered, the alarm recipient did not receive a notification. The alarm history page contains records of alarm events corresponding to the alarm policy. You can click View Details in the corresponding **Operation** column, and the page will redirect to the **Execution Information** page for the alarm policy. In the notification status column, **Send Failed** or **Partial Success** will be displayed.


* Possible causes

   * The IAM user has not configured a mobile phone number or email address in their personal information, or has not verified their mobile phone number and email address. On the notification group details page, you can find objects that have not received alert notifications. In the column for the corresponding receiving channel, click **View**. If the object has not passed security verification, **Not configured** will be displayed.

   * The phone number or email address associated with the IAM user is in an abnormal state and cannot be used for normal communication.

   * Rate limiting restrictions for certain channels in the message center have been triggered. For example, each phone number can receive up to 10 alert SMS notifications per minute. For detailed rate limiting restrictions, please refer to [Usage restrictions](https://docs.byteplus.com/en/docs/tls/Limits).

   * Alert notification content is too long.

   * When using a custom Webhook channel and inserting alert variables into the content template, if the alert content is parsed as non\-JSON, the message will fail to send.

* Handling recommendations

   * Check whether the security phone and security email configured for IAM users have passed the relevant security verification and whether the corresponding channels are reachable.

   * Please try again later.

   * Check whether the format and length of the alert notification content meet expectations. For details on the format and length of notification content for each channel, please refer to [Create content template](https://docs.byteplus.com/docs/tls/content_templates).


<span id="0737aab6"></span>
## How to set up access permission verification for the alert **Webhook address**?

The TLS alert webhook address supports the following access permission verification methods. For more information about the alert Webhook address, refer to [the Create Webhook integration configuration](https://docs.byteplus.com/docs/tls/Create_Webhook_Integration_Configuration).


* Feishu and DingTalk channels

   * Custom keywords

      If custom keywords are configured in Feishu or DingTalk bots, you must include at least one of these keywords in the alert notification content of TLS. When using this method, it is recommended to set one of the keywords to **Alert** on the DingTalk or Feishu side.

   * Signature verification

      If a signing key is configured in the Feishu or DingTalk bot, you must enter this signing key in the Webhook integration configuration on the TLS side.

* Other custom webhook addresses

   Perform authorization by adding `Authorization: Bearer ${token}` to the **request header**, where you need to replace `${token}` with your own token.


<span id="e211b6ac"></span>
## How to disable alert recovery notifications?

TLS sends alert and recovery notifications to specified channels by default. You can disable alarm recovery notifications in the notification group configuration.


1. Log in to the [Torch log service console](https://console.byteplus.com/tls).

2. Select the region where torch log service is located from the top navigation bar.

3. In the left navigation bar, select **Common Functions** \> **Log Alarm** \> **Notification Management**.

4. On the **notification management** page, under the **notification group** tab, locate the specified notification group, and in its corresponding **action** column, click **edit**.

5. On the **Edit notification group** page, under **Notification policy**, deselect **Alarm recovery**.

   <span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_8e9f1f788817f0f7c7024cf60e19709f.png) </span>

6. Click **Save**.
