---
title: "Message group"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-creating-a-message-group"
---

Message group is for organizing text message templates that meet the same transactional requirements. You can precisely control geographic sending permissions for different message groups.

<span id="48779016"></span>
# Prerequisite

BytePlus Messaging has been activated.

<span id="5a421d1a"></span>
# Context

BytePlus Messaging provides a default message group that you can customize to align with your business requirements, and you also have the option to create additional groups independently. Once a message group is created, a unique group ID number is generated, which serves as a mandatory requirement when initiating the process of sending text messages.

<span id="e4d257fe"></span>
# Procedure

<span id="572bdf6a"></span>
## Create a message group


1. Go to [BytePlus Messaging console](https://console.byteplus.com/sms).

2. In the left navigation pane, click **Message Group**.

3. Click  **+ Create Message Group**.

4. Enter the message group name.

5. Select an affiliated project from the dropdown menu.

6. Select at least one Channel (SMS/WhatsApp/Voice). If you select SMS Channel, you need to select an SMS Type (Multi\-routing/SMS):

   * **SMS**: SMS is the sole channel to deliver messages.

   * **Multi\-Routing**: a smart way to send messages through various channels to achieve high delivery rate, including SMS, WhatsApp, OTTs, etc.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The SMS type cannot be changed once you select. Please review the <a href="https://docs.byteplus.com/en/docs/byteplus-sms/docs-overview-of-sms-service#product-introduction">product introduction</a> and <a href="https://docs.byteplus.com/en/docs/byteplus-sms/docs-sms-pricing-4042bb23">price </a>before fanlizing .</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/412cd9885e03458f9322a51ee261ed5a~tplv-goo7wpa0wc-image.image) </span>

7. Click **OK** to create the message group.

<span id="2debbf8f"></span>
## **Configure message types and sending markets**


1. In the Message Group ID list, find the group you want to configure and click **Edit** to configure advanced settings.

2. In the **Message Group Configuration** window, you can select the types of messages and the markets allowed to be sent to.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1767c4c849a441af88da6a343aca6fcb~tplv-goo7wpa0wc-image.image) </span>

3. Click **Submit** to finish configuration.


<span id="78622d19"></span>
## Set passwords for OTP/MKT messages


1. In the Message Group list, find the message group you want to configure and click **Password** to set OpenAPI password.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/95ddd6f9e9544a999498ae5876b20918~tplv-goo7wpa0wc-image.image) </span>


2. In the **OpenAPI Password** window, click  **+ Create Password**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d1cf25e95d34c8ca3e7599f2875923b~tplv-goo7wpa0wc-image.image) </span>


3. In the **Create Password** popup,

   * For **Channel**, select **SMS** or **WhatsApp**.

   * If you select **SMS**, choose an **SMS Type** (either **MKT message** or **OTP message**).

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21297d850cec46ce90f0820fa1341200~tplv-goo7wpa0wc-image.image) </span>


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">One pair of username and password can only be used for one message type (either OTP or MKT). You’ll need to create separate passwords for each message type.</div>



4. Click **Submit** to generate and save the password


<span id="73d655e4"></span>
# Result

The message group has been successfully configured and is available for sending messages.
