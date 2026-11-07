---
title: "Create Webhook Integration Configuration"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Create_Webhook_Integration_Configuration"
---

Webhook integration configuration manages Webhook alarm notification channels such as DingTalk, Feishu, WeCom, and custom Webhooks. This article introduces the steps to create a Webhook integration configuration.

<span id="74b5305c"></span>
## Background information

Log Service supports managing Webhook addresses through Webhook integration, sending alarm notifications to Feishu groups, DingTalk groups, WeCom groups, or other custom Webhook addresses (such as self\-built systems or third\-party alarm systems). When managing Webhook addresses this way, the alarm system determines whether the alarm notification was sent successfully based on the response body of each request. In addition, the Webhook integration method centrally manages all your Webhook addresses. You only need to bind the corresponding Webhook integration configuration in the alarm group, without repeatedly configuring Webhook addresses.

<span id="45104bd4"></span>
## Webhook Security Configuration

Log Service alarms support the following security configurations.


* Feishu and DingTalk channels

   * Custom keywords

      If custom keywords are configured in Feishu or DingTalk bots, at least one of these keywords must be included in the log service alarm notification content. When using this method, it is recommended to set one of the keywords as **alert** in DingTalk or Feishu.

   * Signature verification

      If a signing key is configured in Feishu or DingTalk bots, you need to enter the signing key in the webhook integration settings of the log service.

* Other custom webhook addresses

   Verify permissions through HTTP request headers by adding `"Authorization": "Bearer ${token}"` in the **request header**, replacing `${token}` with your custom token.


<span id="159745be"></span>
## Procedure


1. Log in to the [Torch Log Service console](https://console.byteplus.com/tls).

2. On the top navigation bar, select the region where the log service is located.

3. In the left navigation bar, select **Common Functions** \> **log alarm** \> **notification management**.

4. On the **notification management** page, under the **webhook integration** tab, click **Create webhook integration**.

5. In the **Create Webhook Integration Configuration** dialog, complete the following settings.

   1. Set the name for the Webhook integration configuration.

   2. Select the notification channel type.

      Supports Feishu, DingTalk, WeCom, and custom Webhook.

   3. Complete the following configurations according to your selected notification channel type.

      * Feishu

         
         |Configure |Description |
         |---|---|
         |Request URL |Webhook URL. You need to first add a custom bot in Feishu, then enter the Webhook URL of the Feishu bot here. For detailed instructions, please refer to the [Custom Robot User Guide](https://open.feishu.cn/document/client-docs/bot-v3/add-custom-bot). |
         |Encryption key |Webhook encryption key. Optional; enter the signature key here only when **Security Settings** in Feishu robot are set to **Signature Verification**. For details, please refer to the [Custom Robot User Guide](https://open.feishu.cn/document/client-docs/bot-v3/add-custom-bot). |
         

      * DingTalk

         
         |Configuration |Description |
         |---|---|
         |Request URL |Webhook URL. You need to add a custom bot in DingTalk first, then enter the Webhook URL of the DingTalk bot here. For details, refer to [creating and installing enterprise internal application bots](https://open.dingtalk.com/document/orgapp/the-creation-and-installation-of-the-application-robot-in-the). |
         |encryption key |Webhook encryption key. If you set a signature value in the DingTalk bot, enter the signature value of the DingTalk bot here. For details, refer to [developing bots](https://open.dingtalk.com/document/orgapp/enterprise-created-chatbot#title-l1n-dbh-82f). |
         

      * WeCom

         
         |Configuration |Description |
         |---|---|
         |Request URL |Webhook address. You need to add a custom robot in WeCom first and then enter the WeCom robot's Webhook address here. For detailed instructions, please refer to the [Group Robot Configuration Instructions](https://developer.work.weixin.qq.com/document/path/91770). |
         

      * Custom Webhook

         
         |Configure |Description |
         |---|---|
         |Request method |The method to request the Webhook URL. Supports POST and PUT. |
         |Request URL |Webhook address.<br><br><br>* For self\-built systems, you need to implement a callback interface on the server side for the log service backend to call and provide the request URL.<br><br>* For third\-party alarm systems, refer to the official documentation to obtain the custom callback address and request body structure. |
         |Request headers |Request headers for this Webhook URL.<br><br>The log service provides the default request header `"content-type": "application/json"`. You can also click **Add a line** to add headers. The log service includes this information in the request headers of each alarm notification.<br><br>For details on request body configuration when using a custom Webhook, refer to [Custom Webhook](https://docs.byteplus.com/docs/tls/content_templates#8af98848). |
         

   4. Click **create**.


<span id="cc8002a5"></span>
## Related actions

After creating the Webhook integration configuration, you can also perform the following actions on the **Webhook Management** page.


|Actions |Description |
|---|---|
|View Webhook integration configuration |Find the target Webhook integration configuration and click the webhook integration name in its operation column to view related settings. |
|Edit Webhook integration configuration |Find the target Webhook integration configuration, click **edit** in its operation column to modify related settings. |
|Copy Webhook integration configuration |Find the target Webhook integration configuration, then click **Copy** in its action column to duplicate a Webhook integration configuration. |
|Delete Webhook integration configuration |Find the target Webhook integration configuration, expand the dropdown menu in its operation column, and click **Delete** to remove the Webhook integration configuration. |
