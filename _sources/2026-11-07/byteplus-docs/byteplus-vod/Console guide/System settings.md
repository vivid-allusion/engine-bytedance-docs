---
title: "System settings"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-system"
---

To customize your BytePlus VOD space for optimal media management and security, this guide provides instructions for configuring key system settings. You will learn how to organize your media with categories, automate post\-upload actions, accelerate cross\-region uploads, secure your content using URL signing and IP lists, and set up callback notifications for important events.

<span id="e83439dc"></span>
## Categories

You can manage the uploaded audio and video files by category. The BytePlus VOD console supports up to three levels of categories and up to 100 sub\-categories for each level. If you do not specify a category, the uploaded file will be classified in **Uncategorized** by default.

To create a category, follow these steps:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and select a space.

2. Click **System settings** \> **Categories** on the left navigation bar.

3. Click **Create a category**.

4. Edit the category name and save it.


After creating a category, you can specify categories for the uploaded audio and video files on the following pages:


* Select a category when uploading a file.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be332c6676ca4d88978e116ef04d90af~tplv-goo7wpa0wc-image.image) </span>

* Edit the video details after uploading a file.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81c3273ee11c453288b45add2435d7a4~tplv-goo7wpa0wc-image.image) </span>


<span id="ceae671a"></span>
## Upload and storage settings


* **Post\-upload actions:**  Includes cover generation, default workflow trigger, and auto\-publishing.

* **Upload acceleration settings:**  Accelerates cross\-region uploads to a VOD space in Asia Pacific (Johor) through BytePlus IntelliEdge Global Accelerator (IGA).

* **Public access settings:**  When the URL signing is disabled, read/write access switches to **Public**, allowing any user on the Internet to access the source files within the Bucket.


<span id="3cd0f7b4"></span>
### Post\-upload actions

The BytePlus VOD console supports the following post\-upload actions:


* **Cover generation**: You can generate video covers in two ways:

   * Extracting the first non\-black frame

   * Extracting frames at a specific time point

* **Default workflow trigger**. You can specify a default workflow.

* **Auto\-publishing**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>



* <div data-tips="true" data-tips-type="tip">Post\-upload actions take effect on all uploaded videos in this space.</div>


* <div data-tips="true" data-tips-type="tip">The workflow specified in the Open API takes priority over the default workflow.</div>



To configure your upload settings, simply follow these steps:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and select a space.

2. Click **System settings** \> **Upload and storage** on the left navigation bar.

3. Click **Post\-upload actions**.

4. Click **Modify**.

5. You can:

   1. Turn on **Cover generation**.

   2. Turn on **Default workflow trigger** and select the default workflow.

   3. Set the video status to **Publish**.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/69ab23f0b0a344f0ad8c5d0e6d03f6f0~tplv-goo7wpa0wc-image.image) </span>

6. Click **Confirm**.


<span id="upload-acceleration-settings"></span>
### Upload acceleration settings

For a VOD space in Asia Pacific (Johor), you can configure an IGA custom domain to accelerate cross\-region uploads. The console provides primary and backup storage endpoints for configuring origins in BytePlus IntelliEdge Global Accelerator (IGA). You can also choose whether the IGA custom domain or the VOD upload domain is used as the primary upload domain. The VOD upload domain is selected by default.

For prerequisites, IGA configuration, and failover recommendations, see [Cross-region upload acceleration](https://docs.byteplus.com/docs/byteplus-vod/docs-cross-region-upload-acceleration).

<span id="73e10e90"></span>
### Public access settings via storage URLs

If you haven't configured an acceleration domain (CDN), you can download or play video files directly from the VOD storage addresses.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Since M3U8 rewriting is not supported on the VOD storage bucket's public access domain, you cannot play HLS (HTTP Live Streaming) protocol videos when URL signing is enabled.</div>



1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and select a specific space.

2. Click **System settings** \> **Upload and storage** on the left navigation bar.

3. Under the **Public access** tab, you can view the following basic information:

   * **Region:**  The region where the VOD storage bucket is located, defaulting to Asia Pacific (Johor).

   * **Create time**: The time the VOD storage bucket was created.

   * **Storage address:**  The storage address automatically generated by the system.

   * **Read/write access:**  Defaults to **Private**. When URL signing is enabled, access is **Private**; when disabled, access is **Public**.

4. Click **Modify**. You can modify the following information:

   * **URL signing:**  User requests must include a signature calculated from multiple fields. The request is accepted only if the signature in the request matches the signature calculated by the server. Configuration takes approximately 5 minutes to update. Currently, only Type A is supported. Specific parameters are as follows:

      
      |**Parameter** |**Description** |
      |---|---|
      |Status |Defaults to **Enabled**. If URL signing is disabled, read/write access switches to **Public**, allowing any user on the Internet to access files in the Bucket. This may cause data leakage and a surge in fees. Please proceed with caution. For payment details, see [Storage outbound traffic pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#b7992460). |
      |Type |Only Type A is supported. |
      |Primary key |Set a primary key. The key consists of 6\-40 characters and can only contain printable ASCII characters, excluding the Delete character (ASCII code 127). You can generate a random key by clicking **Randomize**. |
      |Backup key |Set a backup key. The requirements are the same as the primary key. |
      |Signature parameter |Set the request signature parameter name. Defaults to `auth_key`. You can customize but cannot set to `timestamp`. The parameter name supports letters, numbers, underscores `_`, hyphens `-`, periods `.`, commas `,`, and exclamation marks `!`, and cannot exceed 100 characters. It must contain at least one letter or number. |
      |Validity period |Set the validity period of the signature. Defaults to 1800 seconds. Value range is [0, 315,360,000].<br><br><br>* This field is used with the signature parameter to calculate the signature expiration time.<br><br>* Signature expiration time = Signature parameter + Validity period. When VOD receives a request, if the signature expiration time in the request is less than the current time, the signature is considered expired. In this case, it returns a 403 response status code, indicating signing failure. |
      |Time format |This is fixed to **Decimal** (Unix timestamp). |
      

   * **IP allowlist and blocklist:**  Allow or prohibit requests from specific IPs to access the VOD storage address. The specific parameters for IP allowlists and blocklists are as follows:

      * **Status:**  Defaults to **Disabled**. You can change the status.

      * **Type:**  Select Allowlist or Blocklist.

      * **IP:**  Enter IP addresses. IP rules are as follows:

         * Supports IP format (IPv4 or IPv6) and CIDR blocks.

         * You can enter multiple IP addresses and separate them with semicolons (`;`) or newlines, with a maximum of 1,000 entries.

         * The length limit is 1 to 30,000 characters.


<span id="aed0518b"></span>
## Callbacks

To receive timely notifications when tasks such as media uploads and media processing are completed, you can configure callback subscriptions. After the callback event is completed, the BytePlus VOD service will send callback information to the configured callback address. You can manage callback events, callback authentication, and callback subscriptions for your space on the **Callbacks** page.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">For the callback mechanism and supported events, see <a href="https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-">Event notification overview</a>.</div>


<span id="d54fbf60"></span>
### Configuring callback settings

To configure callback settings, follow these steps:


1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and select a space.

2. Click **System settings** \> **Callbacks** on the left navigation bar.

3. In the **Parameter configuration** tab, click **Modify**.

4. Select the callback events that you want to receive. For more information, please refer to the [Event list](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-notifications-#11f54192).

5. (Optional) Enable callback authentication. The authentication key will be displayed when enabled. You can either customize an authentication key, or click **Randomly generated**. For details, see [Callback authentication](https://docs.byteplus.com/docs/byteplus-vod/docs-callback-authentication).

6. Click **Save**.


<span id="f6a8e7d6"></span>
### Adding callback subscription

To add a callback subscription, follow these steps:


3. In the **Callback subscription** section, click **Add subscription**.

4. In the **Callback subscription configuration** dialog box, select the **Request Content Type** and enter the callback address.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7f060cb9a1524cd8b07bf49fddd742a5~tplv-goo7wpa0wc-image.image) </span>

5. Click **Confirm**.


<span id="d31df6d9"></span>
### Testing the receiving address

To test the address, follow these steps:


1. Find the address that you want to test, click **Test**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24c68811b987441fb20a969c602887e5~tplv-goo7wpa0wc-image.image) </span>

2. In the dialog box that appears, select the test events and click **OK** to send the test message.

3. Switch to the **Callback record** tab to check the callback test result. A status of **Callback successfully** indicates that the address is available.


<span id="8463110f"></span>
### Viewing callback records


1. Navigate to the **Callback record** tab to access and filter callback records based on Vid, callback status, or callback time.

   
   |Filter |Description |
   |---|---|
   |Vid |Input the Vid, which can be found on the **Videos** page. |
   |Callback status |Choose from:<br><br><br>* Success<br><br>* Fail<br><br>* All |
   |Time |Query callback records from the past 7 days, with precision to the hour. |
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Note that there might be a delay in displaying the most recent callback records. If you do not see the latest updates, please refresh the page at a later time.   </div>
   

2. To view the detailed information on a specific callback, click the **Details** button.
