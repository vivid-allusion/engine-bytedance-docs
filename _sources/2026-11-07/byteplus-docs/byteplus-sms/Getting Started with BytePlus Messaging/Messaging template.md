---
title: "Messaging template"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/docs-creating-signature-and-templates"
---

Create a messaging template in a message group on the Messaging Console, ensuring it aligns with your activated channels.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Template creation is unnecessary when sending messages via <strong>OpenAPI</strong>. For more details, please see <a href="https://docs.byteplus.com/en/docs/byteplus-sms/docs-openapi-overview">OpenAPI for messaging</a>.</div>


<span id="fdd43114"></span>
# Prerequisite


1. BytePlus Messaging has been activated.

2. A message group has been created.


<span id="f67ec2da"></span>
# Context

After enabling BytePlus Messaging, you can create message templates tailored to your activated channels, which helps route messages through the most suitable channel for your audience. While there’s no limit to the number of templates you can create, the console displays up to 1,000 templates at a time, sorted by creation date (oldest to newest).

<span id="ee72bcc5"></span>
# Procedure


1. Go to [BytePlus Messaging console](https://console.byteplus.com/sms).

2. In the left navigation bar, click **Messaging** \> **Template**.

3. Click  **+Add Template**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/052143c3513a4914acd9c1aca2a8ba35~tplv-goo7wpa0wc-image.image) </span>


4. Select a channel and click **Next step**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5fb1f3b72134440caa0675138d1ce0c1~tplv-goo7wpa0wc-image.image) </span>

5. Complete template configuration based on your selected channel:


<span id="94d82e36"></span>
## **SMS**

Fill in the required fields and preview the SMS template in the right\-side panel as you go.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e4387967abe42179e4e98eb8b71fa5b~tplv-goo7wpa0wc-image.image) </span>


|**Field** |**Required** |**Description** |
|---|---|---|
|Template Name |Yes |Type a template name within 50 characters. |
|Template Type |Yes |Select OTP message for sending verification codes, or MKT message for notifications and marketing promotions. |
|Use the platform to generate short URLs |Only required for MKT messages. |Enable to let BytePlus Messaging shorten URLs in this template. Choose Yes/No as needed. |
|Personalized Click Statistics |Only required when URL shortening is enabled. |Shows only if URL shortening is enabled. Turn on to track how many times short URLs in this template get clicked. |
|Description |No |Type a description of the current template to differentiate it from other templates. |
|Template Content |Yes |Type the message content to be sent to recipients. |


<span id="6c96bb8e"></span>
## **WhatsApp**

First, select a WABA (WhatsApp Business Account). Then follow the table and steps below to complete template details.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ef937f1392c4207a8bb40f42162ac89~tplv-goo7wpa0wc-image.image) </span>


|**Template Category** |**Supported Template Type** |**Description** |
|---|---|---|
|Authentication |Fixed Template |Used for user identity verification (e.g., account authentication or recovery) via one\-time passwords. Authentication templates use Fixed Templates and cannot modify the verification text, as it is predefined by Meta. |
|Marketing |Custom Template/ Carousel Template |Includes promotional offers, updates, or invitations to encourage customer actions. Any non\-authentication or transaction\-related conversations are considered marketing. |
|Utility |Custom Template |Used for specific requests or transactions agreed upon with the customer, as well as updates related to ongoing transactions (e.g., post\-sales notifications, billing reminders). |


Configuring WhatsApp Message Templates for Different Use Cases:


1. **Authentication Templates**

* Meta supports multi\-language authentication templates. Begin by selecting a language and configuring the template content.

* The verification text in authentication templates is predefined by Meta and cannot be edited. As a result, no text\-editing input field appears on the configuration page.

* You can set expiration times, add security suggestions, and configure text for the **Copy Code** button based on your business scenario.

* Changes made to the template automatically reflect in the right\-side preview panel as you configure.

2. **Marketing Templates**

   1. **Custom Template**

      1. Start by selecting a language and setting the template content.

      2. Sections of a Custom Template:

      
      |**Section** |**Required** |Details |
      |---|---|---|
      |Header |No |Supports text, images, videos, or documents. For images, videos, or documents files upload, please see [META guide](https://developers.facebook.com/docs/whatsapp/cloud-api/guides/send-messages) for supported formats to ensure compatibility. |
      |Body |Yes |Supports rich media (e.g., emojis, bold text) and can include up to 5 variables with a maximum length of 1020 characters. META requires sample variables during template creation. |
      |Footer |No |Plain text only, with a maximum length of60 characters. |
      |Buttons |No |Add up to 10 buttons. If more than 3, they display as a list. Buttons are required when the template type is OTP message, while they are optional for non\-OTP message templates. |
      


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">When selecting text, allow the addition of a variable that you will need to replace when sending it. META requires that a variable example must be provided when creating a template containing variables.</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/914e97be4c6342708e2df3a6ddfda20a~tplv-goo7wpa0wc-image.image) </span>


2. **Carousel Template**

   1. Select a language and configure the template content.

   2. Carousel templates do not include headers, but the body is configured similarly to Custom Templates.

   3. Carousel Card Configuration:

      * Specify whether the carousel includes images or videos.

      * Set buttons that apply to all carousel cards.

      * Configure content for each card and preview changes in the right\-side panel.

3. **Utility Templates**


Set up Utility Templates the same way as Marketing Custom Templates. Just remember to follow Meta’s specific guidelines for different use cases.

<span id="3fe654a4"></span>
# Result

Your application will be submitted for review, and you can track its progress in the template list. Review processes typically take 1\-2 business days. For real\-time updates, you may configure a webhook to receive callbacks for template status updates.
