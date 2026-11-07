---
title: "DRM encryption overview"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-drm-encryption"
---

To protect your video content from unauthorized distribution, you can implement Digital Rights Management (DRM) encryption with BytePlus VOD. This guide provides step\-by\-step instructions on the entire process, including obtaining DRM keys, configuring licenses, encrypting your content, and enabling playback for authorized users.

# Overview

DRM (Digital Rights Management) is a comprehensive method of protecting digital media copyrights. It prevents unauthorized distribution and restricts copying of purchased content. By encrypting your content with DRM, you enhance security, allowing only authorized users to access and view it.

BytePlus VOD supports **Google Widevine**, **Apple FairPlay**, and **Microsoft PlayReady** DRM encryption. Before implementing DRM encryption, ensure that you are familiar with the rules and limitations of [Widevine](https://www.widevine.com/), [Fairplay](https://developer.apple.com/streaming/fps/), and [PlayReady](https://www.microsoft.com/playready/).

# Playback compatibility and limitations

## Widevine and FairPlay

### BytePlus VOD Player SDK support

|**DRM solution** |**Platform** |**Supported environment** |
|---|---|---|
|**Widevine** |Android |Native app |
||macOS, Windows, Android |Browsers: Chrome, Microsoft Edge, Firefox |
|**FairPlay** |iOS |* Native app<br><br>* Browsers: Safari, Chrome, Microsoft Edge, Firefox |
||macOS |Safari |

### Third\-party players

You can also use third\-party players like [Shaka Player](https://shaka-player-demo.appspot.com/docs/api/tutorial-drm-config.html) and [Bitmovin Player](https://developer.bitmovin.com/playback/docs/drm-content-protection) for playback. See [Use a third-party player](https://docs.byteplus.com/docs/byteplus-vod/docs-drm-encryption#using-a-third-party-player) for more details.

## PlayReady

The BytePlus VOD Player SDKs **do not** support PlayReady. Playback is only possible using a third\-party player that supports PlayReady, and the video must be delivered in **DASH (MPD) mode**.

## Special domain configuration

Please note that the following scenarios require a special domain configuration to be enabled by [BytePlus technical support team](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00001112):

* **HLS with DRM**: This is required for playback on all players (BytePlus VOD Player SDKs and third\-party players).

* **DASH in MPD mode**: This is required for playback on third\-party players.

# Benefits

* BytePlus VOD allows you to manage DRM licenses and FairPlay certificates, encrypt videos based on DRM, and decrypt and play DRM\-encrypted videos.

* BytePlus VOD uses the Common Encryption (CENC) scheme to encrypt videos, enabling the same content to be played on various devices for different audience groups. This reduces transcoding and storage costs.

# Procedure

See the diagram below for a comprehensive overview of the DRM user flow.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5675abcecfba49bb8c3549f62d872d76~tplv-goo7wpa0wc-image.image)

## Step 1: Getting the DRM key

1. You must first get a DRM key from [Intertrust](https://portal.expressplay.com/). For detailed instructions on obtaining the key, please refer to [Getting a DRM key from Intertrust](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-drm-key).

2. (Optional) To enable encryption on Apple devices, it is also necessary to get a FairPlay certificate. You will then need to upload the certificate to BytePlus VOD console and Intertrust. For details, see the following documents:

   * [Getting a FairPlay certificate from Apple](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-fairplay-certificate)

   * [Uploading a FairPlay certificate to Intertrust](https://docs.byteplus.com/docs/byteplus-vod/docs-uploading-fairplay-certificate-to-intertrust)

## Step 2: Configuring DRM licenses

To enable Widevine and PlayReady, simply add the API key. However, for FairPlay, in addition to the API key, you also need to provide a certificate. This article introduces how to upload the DRM key and FairPlay certificate to the BytePlus VOD console.

### Uploading the DRM key

1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar and select a specific space.

3. Click **Media processing** \> **DRM licenses**.

4. Click **Add API key**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3f83e3fdb3464655897cfaeea664c108~tplv-goo7wpa0wc-image.image)

5. In the dialog box that appears, enter the key.

6. Click **Confirm** to save the settings.

### (Optional) Uploading the FairPlay certificate

To enable encryption on Apple devices, you must also upload a FairPlay certificate.

1. Sign in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/).

2. Click **Spaces** on the left navigation bar and select a specific space.

3. Click **Media processing** \> **DRM licenses**.

4. Click the **Certificate** tab.

5. Click **Add certificate**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1be5f251d9d64773891099dc8908f237~tplv-goo7wpa0wc-image.image)

6. In the dialog box that appears, configure the following parameters:

   |**Parameter** |**Description** |
   |---|---|
   |Certificate name |The name of your FairPlay certificate. |
   |Certificate file |Upload a `.cer` file. |
   |Private key file |Upload a `.pem` file. |
   |Private key |The key that is used to decrypt the private key file. |
   |ASK |The Application Secret Key (ASK) provided by Apple when applying for the certificate. |

7. Click **Confirm** to save the settings.

## Step 3: Encrypting your content

To encrypt your audio and video files with DRM licenses using the BytePlus VOD media processing service, follow these steps:

1. Create an audio, video, or low\-bitrate HD transcoding template and enable **DRM encryption** in the template, then select the DRM type you want to enable. For the detailed instructions on how to create a media processing template and complete the configuration, see the following documents:

   * [Audio transcoding template](https://docs.byteplus.com/docs/byteplus-vod/docs-audio-transcoding-template)

   * [Video transcoding template](https://docs.byteplus.com/docs/byteplus-vod/docs-video-transcoding-template)

   * [Low-bitrate HD template](https://docs.byteplus.com/docs/byteplus-vod/docs-high-definition-and-low-bitrate-template)

      ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee5473f125c041539d3b6c00834db110~tplv-goo7wpa0wc-image.image)

2. Set up a workflow for processing your audio and video files. Choose the appropriate transcoding task (audio, video, or low\-bitrate HD) and configure it with the template you created. For the detailed instructions on how to create a workflow, see [Workflows](https://docs.byteplus.com/docs/byteplus-vod/docs-workflow).

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6db4d9aaa32946fc9b34407da785a056~tplv-goo7wpa0wc-image.image)

3. Trigger the workflow. You can set it as the default workflow for your space, specify it when uploading files, or manually trigger it after uploading. For more information, refer to the documentation on [Triggerring a workflow](https://docs.byteplus.com/docs/byteplus-vod/docs-media-processing-overview#trigger-workflow).

## Step 4: Playing encrypted content

### Using the BytePlus VOD Player SDK

For details, see the following content:

* [Android Player SDK: Playing DRM encrypted videos](https://docs.byteplus.com/en/docs/byteplus-vod/docs-playing-drm-videos-android)

* [iOS Player SDK: Playing DRM encrypted videos](https://docs.byteplus.com/en/docs/byteplus-vod/docs-playing-drm-videos-ios)

* [Web Player SDK: Playing DRM encrypted videos](https://docs.byteplus.com/en/docs/byteplus-vod/docs-implementing-advanced-features-web#playing-drm-encrypted-videos)

* [Flutter Player SDK: Playing DRM encrypted videos](https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-player-advanced-features#playing-drm-encrypted-videos)

### Using a third\-party player

1. Call [GetPlayInfo](https://docs.byteplus.com/docs/byteplus-vod/reference-getplayinfo) to obtain the video playback URL `MainPlayUrl` and the key ID `playAuthId`.

   > **注意**

   > DASH (including regular DASH and DRM DASH) must be delivered via MPD for playback using third\-party players. Set the `DashMode` parameter of `GetPlayInfo` to `mpd`.

2. Obtain the third\-party DRM auth token using the BytePlus VOD Server SDKs. Decode it using a base64 decode tool to get a JSON object. The `GetThirdPartyDrmAuthToken` field within this JSON represents the parsed token. For more information about how to generate the token using the BytePlus VOD Server SDKs, please refer to the following documentation.

   * [Java SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-java-sdk#generating-drm-auth-token)

   * [Python SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-python-sdk#generating-drm-auth-token)

   * [PHP SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-php-sdk#generating-drm-auth-token)

   * [Go SDK](https://docs.byteplus.com/en/docs/byteplus-vod/docs-go-sdk#generating-drm-auth-token)

3. Construct the license URL following this pattern: `https://vod.byteplusapi.com/${parse(thirdPartyDrmAuthToken)}&ThirdPartyDrmType=${thirdPartyDrmType}&Kid=${playAuthId}`. Replace the following fields:

   1. `{parse(thirdPartyDrmAuthToken)}`: With the parsed token from Step 2.

   2. `{thirdPartyDrmType}`: With the corresponding DRM type (`fairplay`, `widevine`, or `playready`).

   3. `{playAuthId}`: With the key ID from Step 1.

4. Set both the video source URL `MainPlayUrl` (from step 1) and the license URL (from step 3) to the player for decryption and playback.
