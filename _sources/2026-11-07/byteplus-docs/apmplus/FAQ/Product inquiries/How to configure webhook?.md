---
title: "How to configure webhook?"
product: "Application Performance Management Plus"
product_code: "apmplus"
source: "https://docs.byteplus.com/en/docs/apmplus/How_to_configure_a_webhook"
---

<span id=".6aOe5Lmm6YWN572ud2ViaG9va-acuuWZqOS6ug=="></span>
## Feishu configuration for webhook bot


1. Open the Feishu group settings and click **Group bot**.

2. On the **Group bot** page, click **Add bot**.

3. Click **Add** next to "Add custom bot".

4. On the **Step 1: Add custom bot to group** page, enter the bot name and description.

5. In **Step 2**, scroll down to **Security settings**, check **Custom keywords**, enter "APM" and press Enter to confirm. Then view the webhook address, complete the settings, and click **Save**.

6. On the **Dashboard subscription** page, check Feishu, paste the bot's webhook address, and click **Confirm**.


<span id=".6ZKJ6ZKJ6YWN572ud2ViaG9va-acuuWZqOS6ug=="></span>
## DingTalk configuration for webhook bot


1. Open the DingTalk group settings and click **Smart group assistant**.

2. On the bot management page, click **Add bot**.

3. Scroll down to **Security settings**, add alert keywords, and click **Done**.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">When configuring alert\-receiving webhook bots for different endpoint monitoring, different alert keywords are required. Please refer to the following examples for configuration.   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Keywords that can be added for App Monitoring: APMPlus alert, alert module, alert level, alert time   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Keywords that can be added for WebPro Monitoring: application, service, alert name, alert info   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Keywords that can be added for Mini Pro Monitoring: application, service, mini program type, alert name, alert info   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Keywords that can be added for PC Monitoring: application, service, alert name, alert info   </div>
   

4. On the **Dashboard subscription** page, check DingTalk, paste the webhook address, and click **Confirm**.
