---
title: "Overview of notifications"
product: "SealSuite"
product_code: "sealsuite"
source: "https://docs.byteplus.com/en/docs/sealsuite/docs-overview-of-notifications"
---

The **Notifications** feature allows you to centrally manage message notification methods and templates across SealSuite channels. By configuring SMS, email, or third\-party IM, you ensure that critical information—such as system verification codes, account details, and alarm events—reaches administrators and employees accurately and promptly.

<span id="0c8d388f"></span>
## Notification methods

SealSuite supports the following four notification channels, which can be configured in combination to suit your enterprise workflow:


* **SMS Configuration**: Use for high\-security notifications, such as verification codes and initial passwords.

* **Email**: Use for formal onboarding guides, account resets, and detailed alarm information.

* **Third\-party IM**: Connect existing Lark, WeCom, or Slack bots to push real\-time dynamic policy reminders within the IM software.

* **SealSuite Configuration**: Customize pop\-up notification copy delivered via the SealSuite desktop client.


<span id="4dc04d9e"></span>
## Manage SealSuite configuration

SealSuite client notifications appear as system\-level pop\-ups for employees using the desktop client. When the backend triggers a Dynamic Control policy (e.g., blocking network access because a device fails to meet security baseline requirements), the client displays a real\-time prompt.


1. Log in to the Admin Console.

2. In the left navigation bar, go to **Settings** \> **System Settings** \> **Notifications**.

3. On the **Notifications** page, click the **SealSuite Configuration** tab to view and manage notification push copy.


<span id="e10840ea"></span>
## Manage SMS configuration

SealSuite allows enterprises to flexibly configure SMS service providers to send messages domestically and internationally. The Admin Console includes pre\-built templates for common scenarios like verification codes and password resets to help you quickly set up SMS content.


1. Log in to the Admin Console.

2. In the left navigation bar, go to **Settings** \> **System Settings** \> **Notifications**.

3. On the **Notifications** page, switch to the **SMS Configuration** tab and click **Edit**.

4. **Configure SMS Gateway**: Select a provider and enter the required configuration details.

   
   |**SMS Service Provider** |**Configuration Description** |
   |---|---|
   |SMS services |Follow the on\-page prompts to configure the AccessKey ID, AccessKey Secret, signature, and other service credentials.<br><br>**Example: Byteplus SMS Service**<br><br>Use the provided official BytePlus documentation to complete service configuration in the BytePlus Messaging console, then enter the details into the SealSuite Admin Console. For example:<br><br><br>* **Access Key ID** & **Secret Access Key**: Found in **BytePlus Console** \> **User Profile** \> **IAM** \> **Access Key Management**.<br><br>   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/04fe31ddd6d24931be814ce36de664fa~tplv-goo7wpa0wc-image.image) </span><br><br>* **Message Group Account**: Found in the upper right corner of the **BytePlus Console** \> **BytePlus Messaging** page.<br><br>* **SMS Signature**: Found after adding a signature in the upper right corner of the **BytePlus Console** \> **BytePlus Messaging** page.<br><br>* **Notification Scenario**: SealSuite provides default templates for **SMS verification code**, **initial password**, and **reset password**. Click **Edit** to customize content.<br><br>   * **Language Support**: Configure separate templates for **Simplified** **Chinese** and **English** tabs.<br><br>   * **Reset to Default**: Click **Restore default settings** to clear custom input and revert to system presets.<br><br>   * **Formatting Limits**: Titles and content support up to 20 characters (including text, variables, and hyperlinks).<br><br>   * **Variables**: Type `#` to call up the list of predefined system variables.<br><br>* Alternatively, create templates directly within your SMS provider's console and enter the **Template ID** into the **SMS Template Code** field in SealSuite. |
   |Subscribe to SMS notification events |The content of the SMS notification will be sent to the event center, and the three\-party service can be obtained by subscribing to the "SMS Notification" event through the event center. |
   |System\-built\-in SMS service |Use SealSuite's default SMS service. No manual gateway or template configuration is required; simply save to enable. |
   |SMS service not enabled |Disable SMS notification functionality. |
   

5. (Optional) In the **Send Test SMS** section, select a notification type and enter a mobile number (including the country code) to send a test message. This verifies the format and delivery status using the current configuration.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">SMS templates must be submitted to third\-party operators for review. They only take effect after approval, which may involve delays or rejection risks.   </div>
   

6. Click **Save** in the upper right corner to apply changes.


<span id="598a8170"></span>
## Manage Email configuration

Configure an SMTP email gateway to deliver notifications via your enterprise email system.


1. Log in to the Admin Console.

2. In the left navigation bar, go to **System** \> **System Settings** \> **Notifications**.

3. On the **Notifications** page, switch to the **Email** tab and click **Edit**.

4. Configure the following gateway settings and click **Save**.

   
   |**Configuration Item** |**Description** |
   |---|---|
   |* **SMTP Server Address**<br><br>* **SMTP Port** |Enter the SMTP host and port for your enterprise email provider.<br><br>**Examples:** <br><br><br>* **Alibaba Cloud Enterprise Mail:**  Server: `smtp.qiye.aliyun.com`<br><br>* **Tencent Enterprise Mail:**  Server: `smtp.exmail.qq.com`<br><br>* **Gmail:**  Server: `smtp.gmail.com` |
   |**Email Address** |Specify the email address for SealSuite notifications (e.g., `sealsuite@<enterprise_domain>.com`). |
   |**Sender Email Address** |The full email address displayed to recipients (optional). |
   |**Email Password** |The password or app\-specific password for the enterprise email account. |
   |**Custom Template** |Choose **Enable** or **Not applicable**.<br><br><br>* **Not applicable**: SealSuite uses default system templates for all notification scenarios.<br><br>* **Enable**: Click **Edit** next to a scenario to manually customize template content.<br><br>   * **Language Support**: Configure separate templates for **Simplified Chinese** and **English**.<br><br>   * **Reset to Default**: Revert to initial system presets.<br><br>   * **Formatting Limits**: Titles support up to 20 characters. Content supports rich text, HTML, and hyperlinks.<br><br>   * **Variables**: Type `#` to call up the list of predefined system variables. |
   |**Send Test Email** |Verify gateway connectivity. Select a scenario and enter a recipient email address, then click **Send Test** to deliver a simulated notification. |
   


<span id="7e2d6168"></span>
## Manage third\-party IM

Integrate SealSuite security posture with enterprise collaboration platforms (Lark, WeCom, Slack). Administrators can configure self\-built apps or group bots to push Dynamic Control policy reminders (e.g., violation alerts) to specific employees or real\-time alarms to management groups.


1. Log in to the Admin Console.

2. In the left navigation bar, go to **System** \> **System Settings** \> **Notifications**.

3. On the **Notifications** page, click the **Third\-Party IM Applications** tab to perform the following:

   * **Add Bots.**  Click **New Integration** to add a Lark, or WeCom bot. Refer to:

      * [Adding a Lark robot](https://docs.byteplus.com/docs/sealsuite/docs-6zjnstxl2m)

      * [Adding a WeCom robot](https://docs.byteplus.com/docs/sealsuite/docs-zya0oh878g)

      * [Adding a Slack robot](https://docs.byteplus.com/docs/sealsuite/docs-adding-slack-robot)

   * **Manage Bots.** 

      * Use the toggle on a bot card to enable or disable its status.

      * Click the ellipsis ( **...** ) to **Edit** or **Delete** a bot.

   * **Manage Notification Templates.**  View template details and click **Edit** to modify historical notification content.

      * **Language Support**: Configure separate templates for **Simplified Chinese** and **English**.

      * **Reset to Default**: Revert to initial system presets.

      * **Formatting Limits**: Titles support up to 20 characters. Content supports hyperlinks.

      * **Variables**: Type `#` to call up the list of predefined system variables.

   * **Test Connectivity.**  After configuring a bot and template, click **Test** to send a simulated notification to the specified target.
