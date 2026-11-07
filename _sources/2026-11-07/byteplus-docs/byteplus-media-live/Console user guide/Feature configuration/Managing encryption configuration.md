---
title: "Managing encryption configuration"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-a-drm-encryption-task"
---

This article introduces how to configure and enable encryption for origin stream and transcoding stream with a specified AppName.

<span id="1872b015"></span>
## Fee description

For transcoded encrypted videos, charges apply only for transcoding. Refer to [transcoding](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding) for transcoding fees.

<span id="01b55900"></span>
## Prerequisite


* If using commercial DRM encryption technologies such as Widevine, FairPlay, or PlayReady, ensure that:

   * You have uploaded the API access key to the DRM certificate management platform. For upload instructions, refer to [Managing DRM licenses](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-drm-licenses).

   * For iOS, upload the FairPlay certificate for encryption as described in [Managing DRM licenses](https://docs.byteplus.com/docs/byteplus-media-live/docs-managing-drm-licenses).

   * If you intend to encrypt a transcoding stream, create a transcoding configuration for that stream. See [Configuring a transcoding task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding).

* If using HLS standard encryption:

   * Configure the key acquisition address of the self\-built key management service. Refer to [Managing HLS key acquisition address](https://docs.byteplus.com/docs/byteplus-media-live/docs-hls-keyaddress).

   * If you intend to encrypt a transcoding stream, create a transcoding configuration for that stream. See [Configuring a transcoding task](https://docs.byteplus.com/docs/byteplus-media-live/docs-configuring-transcoding).


<span id="e136d0b7"></span>
## Restrictions

When the source name (StreamName) of the live stream contains an underscore, the encryption function is not supported.

<span id="6e210e8a"></span>
## Procedure


1. Log in to the [BytePlus MediaLive console](https://console.byteplus.com/live).

2. In the left\-side navigation pane, select **Settings** \> **Feature configuration**. Click the **Encryption** tab.

3. Find **Domain name space** on the top left and select a domain name space from the drop\-down list. The configurations will then apply to all domain names under the domain name space. You can refer to [Domain name space](https://docs.byteplus.com/docs/byteplus-media-live/docs-glossary#Vhost) for more information about these concepts.

4. Click **Add configuration** to open the **Add Encrypton configuration** dialog box.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4d80ebdbb43d42b6ba304f000a1d6203~tplv-goo7wpa0wc-image.image) </span>

5. Configure the settings:

   * **AppName**: Take the same value as the value of the AppName field in the live stream address. In this way, it specifies the effective stream range.

   * **Encryption type**: Select encryption technology.

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When using commercial DRM encryption supports three encryption methods: Widevine, FairPlay, and PlayReady.      </div>
      

      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">When using HLS standard encryption, the ClearKey AES\-128 encryption method is supported.      </div>
      

   * **Encrypted content**: Select the encrypted origin stream, or select the encrypted transcoding stream based on the suffix of transcoding configuration.

6. Click **Confirm**.


<span id="4f7ec3d9"></span>
## What's next

You can now generate an encrypted pull streaming address with Address Generator. For details, refer to [Generating an encrypted playback address](https://docs.byteplus.com/docs/byteplus-media-live/docs-encrypting-your-live-streams-using-drm#4763a627).
