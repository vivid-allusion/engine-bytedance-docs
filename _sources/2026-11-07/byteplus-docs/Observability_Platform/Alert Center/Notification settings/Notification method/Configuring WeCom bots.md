---
title: "Configuring WeCom bots"
product: "Observability Platform"
product_code: "Observability_Platform"
source: "https://docs.byteplus.com/en/docs/Observability_Platform/Configuring_WeCom_bots"
---

This topic describes how to configure a WeCom bot.

<span id="KOk08EAu"></span>
## Procedure

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="0">tip</div>


* <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">For more configuration details and instructions on WeCom group bots, see the <a href="https://open.work.weixin.qq.com/help2/pc/14931?person_id=1&is_tencent=">WeCom official documentation</a>.</div>


* <div data-tips="true" data-tips-type="tip" data-wrapper-indent="0">If you cannot find or add a bot, contact your WeCom administrator.</div>


1. Log in to WeCom, create or find the group that needs to receive alerts.

2. Click the `...` icon in the upper right corner of the group, and click **Add Group Robot** on the drop\-down menu.

2. Check the definition of the group robot and click **Add Robot**.

3. Click **Create Robot** and specify a name for the group robot. Click **Add Robot** to add the robot to the group and obtain the webhook address of the robot.

4. Click **Copy Address** to copy the webhook address of the robot, which will be used in the subsequent configuration.


<span id="bl8AuBKT"></span>
## What to do next

After a WeCom bot is configured, you can use the callback URL obtained from the bot to add a WeCom channel in the callback URL configuration. For information about how to create a callback URL, see [Callback URL](https://docs.byteplus.com/en/docs/Observability_Platform/Callback_URL).
