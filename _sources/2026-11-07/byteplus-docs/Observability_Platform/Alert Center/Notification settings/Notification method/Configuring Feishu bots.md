---
title: "Configuring Feishu bots"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_Feishu_bots"
---

This topic describes how to configure a custom Feishu bot.

<span id="BrNapVfP"></span>
## Procedure

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The Feishu alerting bot may vary across organizations. This topic uses <strong>the custom bot</strong> as an example. If you do not know the name of the alert bot in your organization, contact your Feishu administrator.</div>



1. Log in to Feishu, and create or find a group that needs to receive alerts. Click the `...` icon in the upper right corner of the group, and click **Settings** on the drop\-down menu.

2. In the "Settings" pop\-up window, select **Bots**, and click **Add Bot**.

3. In the bot list, select **Custom Bot**, click **Add**, and follow the on\-screen instructions to configure and add a bot for the group.

4. After the bot is added, you will be redirected to the bot configuration page, where you can configure it based on your actual needs.

   The two key configurations related to notifications are as follows:

   
   |Parameter |Description |
   |---|---|
   |Webhook URL |The callback URL automatically generated after the custom bot is created. It serves as a unique identifier for connecting to the Feishu bot.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Keep the webhook URL secure. Do not share it on public platforms such as GitHub or blogs to prevent unauthorized use due to URL exposure.</div><br> |
   |Set signature verification |It is disabled by default. You can enable it based on your actual needs. When signature verification is enabled, a secret key is automatically generated, corresponding to the Feishu Secret in the alert settings.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">If signature verification is enabled here, the Feishu Secret must be provided when you configure the callback URL for the Feishu channel. If signature verification is disabled here, the Feishu Secret is not required when you configure the callback URL for the Feishu channel.</div><br> |
   


<span id="lsZmSSF3"></span>
## What to do next

After a Feishu bot is configured, you can use the callback URL and Secret obtained from the custom bot to add a Feishu bot channel in the callback URL configuration. For information about how to create a callback URL, see [Callback URL](https://docs.byteplus.com/en/docs/Observability_Platform/Callback_URL).
