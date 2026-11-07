---
title: "Short Link"
product: "BytePlus Messaging"
product_code: "byteplus-sms"
source: "https://docs.byteplus.com/en/docs/byteplus-sms/Short_Link"
---

BytePlus Messaging can convert long links into short links in the message template. By clicking these short links, recipients will be redirected to the original long links. Additionally, Click Statistics can be sent to a specified callback URL for tracking engagement metrics. Failed clicks on redirect links trigger immediate error reporting.

<span id="1af04a55"></span>
## Short Link Feature Rules & Usage Logic


1. Only marketing messages support the short link feature.

2. When creating a short link template on BytePlus Messaging, the original long link must be filled into the template content.

3. Only 1 long link is supported per short link template.

4. Personalized Click Statistics are supported:

   * When using Personalized Click Statistics:

      * After the template is successfully created, the original long link will be displayed in the preview pane.

      * The short link sent to the mobile phone differs each time.

      * Click\-through data for each short link can be tracked.

   * When not using Personalized Click Statistics:

      * After the template is successfully created, the converted short link will be shown in the platform \- displayed copy.

      * The short link sent to the mobile phone remains the same each time (matching the short link in the platform \- displayed copy).

      * Short link click\-through tracking is not available.


<span id="7f5e953a"></span>
## Configuring Short Link Templates and Callback URLs

<span id="0e36b472"></span>
### Creating Short Link Templates


1. Go to [BytePlus Messaging console](https://console.byteplus.com/sms).

2. In the left navigation bar, click **Messaging** \> **Template**.

3. Click  **+**  **Add Template**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/357fee6ccf3f4cd69e0020858f5cc653~tplv-goo7wpa0wc-image.image) </span>


4. Choose **SMS**, then click **Next step**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5b4ccbbd1a9a4ed6877e97295c7168d4~tplv-goo7wpa0wc-image.image) </span>


5. Next, enter the template name and select the template type **MKT message**.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4134bffa66b144fdb28395d3e2e637c6~tplv-goo7wpa0wc-image.image) </span>


6. **Use the platform to generate short URLs** → Select **Yes**.

7. **Personalized Click Statistics**:

   1. If select **Yes**,

      1. After the template is successfully created, the original long link will be in the template content.

      2. The short link sent to the mobile phone is different each time.

      3. Short link click statistics can be tracked and supports callback of click data to a specified URL.

   2. If select **No**,

      1. After the template is successfully created, the converted short link will be in the template content.

      2. The short link sent to the mobile phone is the same each time.

8. The template content must include the original long link.

9. Click **OK** to create a template that uses the short link feature.

10. After the template is approved, the template with short link is active for use.


<span id="f02901d8"></span>
### Short Link Click Callback

We also provide the short link click details callback feature. It can send click\-related data of short links with Personalized Click Statistics feature enabled to a specified callback address.

**Prerequisite**


* A short link click callback address has been configured.

* When sending text messages, use a template where the Personalized Click Statistics setting is “Yes”.


**Configuration Procedure**


1. In the left navigation bar, click **Setting** \> **Receipt address**.

2. Select the message group to the one that contains the short link template for which you want to track click details.

3. Configure the **Short URL Click Status Webhook Enpoint** for this message group.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fcba8669d82b4522a3a259a1033f0252~tplv-goo7wpa0wc-image.image) </span>
