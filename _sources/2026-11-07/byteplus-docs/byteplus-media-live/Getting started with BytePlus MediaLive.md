---
title: "Getting started with BytePlus MediaLive"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
section: "Document"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-getting-started"
---

This topic describes how to get started streaming your live content, including adding and configuring domain names, generating stream addresses, and starting to stream.

<span id="6cf2b444"></span>
## Prerequisites


* A BytePlus account.

* If this is your first time logging in to the [BytePlus console](https://console.byteplus.com), complete the authentication.

* Two domain names.


<span id="b3bed337"></span>
## Procedure

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a390beb258b4fb589a233096aa071f3~tplv-goo7wpa0wc-image.image) </span>

<span id="da5a6a63"></span>
### Activating the MediaLive service


1. Log in to the [BytePlus console](https://console.byteplus.com/).

2. In the **Products** section, click **BytePlus MediaLive**.

3. Follow the instructions on the screen to enter your billing information if you are asked to. Otherwise, proceed to the next step.

4. Click **Activate** **now**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/718efbc829a14a5c939be63e0b4f3dbf~tplv-goo7wpa0wc-image.image) </span>

5. Follow the instructions on the screen to fill out your information and then click **Apply for activation**.

6. After the activation is complete, log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).


<span id="fc8ae6de"></span>
### Adding domain names

To use BytePlus MediaLive, you must add at least two domain names, one for stream pushing, and the other for stream pulling.

MediaLive uses a domain name space to associate domain names for stream pushing and pulling. Domain names for stream pushing and pulling that serve the same line of business need to be in the same domain name space. Refer to [Domain name space](https://docs.byteplus.com/docs/byteplus-media-live/docs-glossary#Vhost) for a detailed explanation of how domain names for stream pushing and pulling are related.


1. In the left\-side navigation pane, click **Domains**.

2. Click **Add domain name** on the **Domains** page that appears.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ec6554b63b6491d81155cd2a980b6c5~tplv-goo7wpa0wc-image.image) </span>

3. Complete the configurations:

   * **Add domain name**:

      1. Select **Push** as the domain name type. You cannot change the domain name type after the domain name is added.

      2. Enter a domain name for stream pushing. You cannot add a wildcard domain name. We recommend that you use a second\-level domain name, such as `example.live.com`. You can add a maximum of 10 domain names under each account.

      3. If you want to use the [Real Time Media (RTM)](https://docs.byteplus.com/en/byteplus-media-live/docs/introduction) protocol, you must configure an SSL certificate for your domain names.

   * **Associated domain name space**:

      * We recommend using the first added domain name as the name of the domain name space.

      * Enter a domain name in lowercase letters that end with ".com"

      * Enter a second level domain name or a subordinate domain name.

      * A domain name is associated with a domain name space. You can add 10 domain name spaces by default. If you need to add more, please contact [BytePlus technical support](https://www.byteplus.com/en/support).

   * **Acceleration region:**  Select the region where you want to accelerate content delivery. The live\-streaming service fees vary depending on the acceleration region. Refer to [Live-streaming service fees](https://docs.byteplus.com/docs/byteplus-media-live/docs-live-streaming-service-fees) for detailed pricing information.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">If you select <strong>Global acceleration</strong> or <strong>The Chinese mainland</strong>, you must get an Internet Content Provider (ICP) license for the domain name. You can complete the verification process on the <a href="https://beian.miit.gov.cn/#/Integrated/index">ICP/IP Address/Domain Name Information Filing Management System</a>.      </div>
      

   * **Project**: Select a project for the domain name space. After the domain name space is associated with a project, you can manage your resource usage and billing by project. For more information about projects, please refer to [About projects](https://docs.byteplus.com/en/docs/byteplus-platform/docs-managing-projects).

4. Click **Next** to save the settings.

5. Repeat step 2 to 4 to add a domain name for stream pulling. Remember to select **Pull** as the domain type.


You can view added domain names in the domain name list.

<span id="f55c33b3"></span>
### Configuring a CNAME record

Add a CNAME record for the domain names to point to their corresponding BytePlus MediaLive domain names, which are automatically assigned. By doing so, all traffic that goes to your domain names will be directed to the BytePlus MediaLive domain names.


1. In the domain name list, find the domain name that you want to configure and then copy the corresponding BytePlus MediaLive domain name in the **CNAME** column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c5facfd095c54e19b6fb629e262ad6df~tplv-goo7wpa0wc-image.image) </span>

2. Log in to the DNS platform of your domain service provider. Add a CNAME record for the domain name to point to the BytePlus MediaLive domain name.

3. Run the `ping` or `dig` command to check whether the CNAME record takes effect. If the CNAME in the output is the same as the BytePlus MediaLive domain name, it indicates that the configuration is successful and the domain name can be used. You can also verify the configuration by checking if the icon beside the BytePlus MediaLive domain name has become a green checkmark.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a8f1391c173444ff8a74ca5db24385da~tplv-goo7wpa0wc-image.image) </span>


For a more detailed explanation about configuring a CNAME record, refer to [Adding a CNAME record](https://docs.byteplus.com/docs/byteplus-media-live/docs-adding-a-cname-record).

<span id="4f17ce32"></span>
### (Optional) HTTPS and other domain name settings

You can complete additional domain name settings to satisfy your business requirements, such as setting up an SSL certificate or a referer blocklist. Refer to the following topics for detailed instructions on completing the settings.


* [Adding an SSL certificate](https://docs.byteplus.com/docs/byteplus-media-live/docs-https)

* [Referer](https://docs.byteplus.com/docs/byteplus-media-live/docs-referer)

* [URL authentication](https://docs.byteplus.com/docs/byteplus-media-live/docs-url-authentication)

* [IP restrictions](https://docs.byteplus.com/docs/byteplus-media-live/docs-ip-blocklist-and-allowlist)


This topic uses SSL certificate configuration as an example. If you want to configure an SSL certificate for your domain name, complete the following steps:

<span id="7a4f3332"></span>
#### Adding an SSL certificate


1. In the left\-side navigation pane, click **Certificates**.

2. On the **Certificates** page, click **Add certificate** to open the **Add HTTPS certificate** dialog box.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9223e729e0c74fc2a6075fbaed9b4043~tplv-goo7wpa0wc-image.image) </span>

3. Enter the name and content of the certificate that you are about to add, and then enter the private key. Currently, you can only add a certificate in the PEM format.

4. Click **Confirm** to save the SSL certificate.


<span id="67853b4d"></span>
#### Enabling HTTPS


1. In the left\-side navigation pane, click **Domains**.

2. On the **Domains** page that appears, find the domain name that you are about to configure and click **Settings** in the **Actions** column.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86933bf66e50428889bd16253b570a0e~tplv-goo7wpa0wc-image.image) </span>

3. On the domain name page that opens,click the **HTTPS** tab.

4. Click **Edit** to the right of the **HTTPS** toggle.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10c428c6e1f14e32b86461545b03bf08~tplv-goo7wpa0wc-image.image) </span>

5. In the **Edit HTTPS information** dialog box that appears, **HTTPS** is turned on automatically. Select the SSL certificate you want to use and click **Confirm**.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Your SSL certificate will appear in the <strong>Certificates</strong> list only if your domain name is added in the <strong>Subject Alternative Name</strong> field in the certificate.</div>


* <div data-tips="true" data-tips-type="tip">The HTTPS encryption takes about 10 minutes to take effect. If the configuration does not take effect, contact your technical support for help.</div>



<span id="fc6a3cf4"></span>
### (Optional) Transcoding and other feature settings

BytePlus MediaLive also provides you with a variety of value\-added services, such as transcoding and recording. Refer to the following topics for detailed instructions on how to use these services:


* [Configuring a transcoding task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding)

* [Configuring a recording task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-recordings)

* [Configuring a screenshot-taking task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-screenshot-capturing)

* [Configuring an origin-pull task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-origin-pull-settings)

* [Configuring a time-shifting task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-time-shifting)

* [Configuring a watermarking task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-live-stream-watermarks)

* [Configuring a callback task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-a-callback-task)


<span id="f4551ba7"></span>
### Generating stream addresses

You can generate push and pull stream addresses by using the [address generator](https://console.byteplus.com/live/main/locationGenerate) or manually constructing them by using a set of concatenation rules. For details, refer to [Generating live-stream addresses](https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses).

<span id="Starting the live stream"></span>
### Starting to stream

You can start streaming by using any of the following methods:


* Use [Web push](https://console.byteplus.com/live/main/WebPushStream) and [Web pull](https://console.byteplus.com/live/main/webPullStream/play), which are web tools available within the BytePlus MediaLive console, to push and pull a live stream directly from your web browser. Refer to the following topics for instructions on how to use the tools:

   * [Pushing a stream through the console](https://docs.byteplus.com/docs/byteplus-media-live/docs-web-push)

   * [Pulling a stream through the console](https://docs.byteplus.com/docs/byteplus-media-live/docs-web-pull)

* Use third\-party streaming tools such as Open Broadcaster Software (OBS) and video players such as VLC to push and pull a live stream.

* Integrate the BytePlus MediaLive Broadcast SDK and BytePlus MediaLive Player SDK into your apps to push and pull a live stream:

   * Android and iOS: [SDK introduction](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction)

   * Web: [Player SDK for Web: SDK overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-to-the-player-sdk-for-web) and [Broadcast SDK for Web: SDK overview](https://docs.byteplus.com/docs/byteplus-media-live/docs-introduction-to-the-broadcast-sdk-for-web)


<span id="1f2fd5c3"></span>
### (Optional) Using OpenAPIs

Apart from using the BytePlus MediaLive console, you can also use OpenAPI to access the MediaLive service. Refer to

[Introduction to BytePlus MediaLive OpenAPI](https://docs.byteplus.com/docs/byteplus-media-live/docs-getting-started-with-your-api) for how to get started using MediaLive OpenAPI.

Furthermore, BytePlus MediaLive provides server SDKs that include sample API requests written in Java, Python, Go, and PHP. For details, see [Server SDK](https://docs.byteplus.com/docs/byteplus-media-live/docs-server-sdk).
