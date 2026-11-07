---
title: "HLS standard encryption"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-standard-encryption"
---

HLS Standard Encryption utilizes the general encryption scheme defined in the [HTTP Live Streaming](https://datatracker.ietf.org/doc/html/draft-pantos-http-live-streaming-23) specification. It encrypts video content using AES\-128, ensuring compatibility with any standard HLS player. While highly compatible, it's important to note that this method's key protection is less robust than that of more advanced DRM solutions.

This document provides a complete guide, including an introduction to the feature, common use cases, pricing, the technical workflow, and a step\-by\-step implementation guide.

<span id="cf841c9d"></span>
## Use cases


* **Content protection:**  Ideal for industries like online education, finance, and exclusive content streaming that require a solid layer of content protection.

* **Broad compatibility:**  Suitable for scenarios where playback on any standard HLS\-compliant player is a requirement.


<span id="501ca786"></span>
## Pricing


* Using the HLS standard encryption feature is free, but it requires video transcoding, which is a billable service. For specific pricing details, please refer to [Transcoding pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#0dc94472).

* Encrypted videos can be played using the BytePlus VOD Player SDKs or any third\-party player. If you use our Player SDK, it is billed on a license basis. For specific pricing details, please refer to [Player SDK license pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-sdk-license-pricing).


<span id="d7e26977"></span>
## How to use

<span id="b9252221"></span>
### Prerequisites


* You have activated the [Video-on-Demand (VOD) service](https://www.google.com/url?sa=E&q=https%3A%2F%2Fwww.volcengine.com%2Fdocs%2F4%2F2834).

* You have configured an [acceleration domain](https://www.google.com/url?sa=E&q=https%3A%2F%2Fwww.volcengine.com%2Fdocs%2F4%2F1165108) in the VOD console.

* You have integrated the [server-side SDK](https://www.google.com/url?sa=E&q=https%3A%2F%2Fwww.volcengine.com%2Fdocs%2F4%2F4374). This guide uses Java for its examples.


<span id="8cfc00b2"></span>
### Step 1: Setting up a key delivery service

Before using HLS standard encryption, you must build and deploy your own **key delivery service**. The URL for this service will be required during [Step 2: Encrypt and transcode](https://docs.byteplus.com/docs/byteplus-vod/docs-standard-encryption#d96c5abf). The workflow is as follows:


1. The player parses the M3U8 manifest and extracts the key URI.

2. The player sends a request to this URI (your key delivery service).

3. Your service is responsible for validating the request's authenticity and returning the correct decryption key.

4. The player uses the fetched key to decrypt and play the video content.


BytePlus VOD supports two key management modes:


<Tabs>
<Tab zoneid="AL2w72CESc" title="Mode 1: Keys generated and managed by BytePlus VOD">
<TabTitle>Mode 1: Keys generated and managed by BytePlus VOD</TabTitle>

In this mode, the VOD service **automatically generates and manages** the decryption key when you initiate an encrypted transcoding job. **Workflow:** 


1. When your Key Delivery Service receives a request from a player, you need to:

   1. Call the VOD server\-side SDK's local method `createSha1HlsDrmAuthToken` to issue a `DrmAuthToken`.

   2. Call the VOD server\-side SDK's `GetHlsDecryptionKey` method to retrieve the plaintext key. You need to pass the `DrmAuthToken` and the Key ID to this API. The Key ID is obtained from the `PlayAuthId` parameter returned by the `GetPlayInfo` API.

2. Return the fetched plaintext key to the player.


Java code example for `GetHlsDecryptionKey`:

```Java
package com.byteplus.example.vod.play;

import com.byteplus.service.vod.IVodService;
import com.byteplus.service.vod.impl.VodServiceImpl;

public class VodGetHlsDecryptionKeyDemo {

    public static void main(String[] args) throws Exception {
        IVodService vodService = VodServiceImpl.getInstance();

        // Configure AK and SK in environment variables or in the local ~/.volc/config file.
        // For details, see: https://docs.byteplus.com/en/docs/byteplus-vod/docs-java-sdk
        // The SDK automatically fetches AK and SK from environment variables or the configuration file.
        // You can use the following two lines for testing, but do not hardcode AK and SK directly in project code to prevent leakage.        
        vodService.setAccessKey("your ak");
        vodService.setSecretKey("your sk");

        try {
            // Step 1: Call createSha1HlsDrmAuthToken to issue a URL query string containing DrmAuthToken
            // The validity period of DrmAuthToken is set here, such as 3600 seconds (1 hour).
            String drmAuthToken = vodService.createSha1HlsDrmAuthToken(3600L);
            System.out.println("Generated Full Query String: " + drmAuthToken);

            // Step 2: Call GetHlsDecryptionKey method to get the plaintext key
            com.byteplus.service.vod.model.request.VodGetHlsDecryptionKeyRequest.Builder reqBuilder = 
                    com.byteplus.service.vod.model.request.VodGetHlsDecryptionKeyRequest.newBuilder();
     
            /* 
             * ============================== IMPORTANT NOTICE ============================== 
             * The createSha1HlsDrmAuthToken method returns a complete URL query string, not just the Token value. 
             * For example, "X-Expires=...&DrmAuthToken=HMAC-SHA1%3A...&Action=..." 
             *
             * You need to parse the value of the "DrmAuthToken" parameter (the "HMAC-SHA1%3A..." part) from this string, 
             * Pass only the parsed value into the setDrmAuthToken method below. 
             *
             * The code below is a simplified demonstration. It directly passes the full string, which is incorrect in actual runtime. 
             * In your implementation, be sure to parse the drmAuthToken first. 
             * ===================================================================== 
             */
             
             // Pass the DrmAuthToken value parsed from the string obtained in the previous step
            reqBuilder.setDrmAuthToken(drmAuthToken);// Pass the parsed Token, not the full string
            
            // Pass the Key ID. You can obtain it from the PlayAuthId returned by the GetPlayInfo API.
            reqBuilder.setAk("your Ak");// Replace with the actual Key ID
            
            // The Source parameter is a fixed value: jarvis
            reqBuilder.setSource("jarvis");
                        
            com.byteplus.service.vod.model.response.VodGetHlsDecryptionKeyResponse resp = vodService.getHlsDecryptionKey(reqBuilder.build());
            if (resp.getResponseMetadata().hasError()) {
                System.out.println(resp.getResponseMetadata().getError());
                System.exit(-1);
            }
            System.out.println(resp);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```



</Tab>
<Tab zoneid="YkK6u0wHk3" title="Mode 2: Keys generated and managed by yourself">
<TabTitle>Mode 2: Keys generated and managed by yourself</TabTitle>

In this mode, you generate and manage the key yourself. Workflow:


1. **Before transcoding**, call the `CreateHlsDecryptionKey` API to generate a key. The API returns an access key ID (`AK`) and a secret access key (`SK`). You must **securely store** the mapping between these two values.

2. When your key delivery service receives a request from a player, use the key ID from the request to look up and return the corresponding plaintext key you stored.


Java Code Example for `CreateHlsDecryptionKey`:

```Java
package com.byteplus.example.vod.play;

import com.byteplus.service.vod.IVodService;
import com.byteplus.service.vod.impl.VodServiceImpl;
public class VodCreateHlsDecryptionKeyDemo {

    public static void main(String[] args) throws Exception {
        // Create a VOD instance in the specified region.
        IVodService vodService = VodServiceImpl.getInstance();
        
        // Configure your Access Key ID (AK) and Secret Access Key (SK) in the environment variables or in the local ~/.volc/config file. For detailed instructions, see https://docs.byteplus.com/en/docs/byteplus-vod/docs-java-sdk
        // The SDK will automatically fetch the AK and SK from the environment variables or the ~/.volc/config file as needed.
        // During testing, you may use the following code snippet. However, do not store the AK and SK directly in your project code to prevent potential leakage and safeguard the security of all resources associated with your account.
        vodService.setAccessKey("your ak");
        vodService.setSecretKey("your sk");

        try {
            com.byteplus.service.vod.model.request.VodCreateHlsDecryptionKeyRequest.Builder reqBuilder = com.byteplus.service.vod.model.request.VodCreateHlsDecryptionKeyRequest.newBuilder();
                        reqBuilder.setSpaceName("your SpaceName");
                        
            com.byteplus.service.vod.model.response.VodCreateHlsDecryptionKeyResponse resp = vodService.createHlsDecryptionKey(reqBuilder.build());
            if (resp.getResponseMetadata().hasError()) {
                System.out.println(resp.getResponseMetadata().getError());
                System.exit(-1);
            }
            System.out.println(resp);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```



</Tab>
</Tabs>


<span id="d96c5abf"></span>
### Step 2: Encrypting your content


1. Create a media processing template in the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/). The audio transcoding template, video transcoding template, and low\-bitrate HD template all support HLS standard encryption. You need to select the **HLS standard encryption** option and enter the **Key delivery service address** you set up in [Step 1: Set up a key delivery service](https://docs.byteplus.com/docs/byteplus-vod/docs-standard-encryption#8cfc00b2), as shown in the following figure.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8368b7e8c3e4066b0096ece12dced72~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For other parameter configurations of the media processing template, please refer to the following documents:   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><a href="https://docs.byteplus.com/docs/byteplus-vod/docs-video-transcoding-template">Video transcoding template</a>   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><a href="https://docs.byteplus.com/docs/byteplus-vod/docs-audio-transcoding-template">Audio transcoding template</a>   </div>
   

   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><a href="https://docs.byteplus.com/docs/byteplus-vod/docs-high-definition-and-low-bitrate-template">Low\-bitrate HD template</a>   </div>
   

2. Create a workflow in the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/). Select the appropriate workflow tasks (such as video transcoding) and associate them with the media processing template you configured for HLS standard encryption.

3. Trigger the transcoding task by calling the [StartWorkflow](https://docs.byteplus.com/docs/byteplus-vod/reference-startworkflow) API. If you use **Mode 2** and generate and manage the key yourself, you must specify your pre\-generated key ID (`Kid`) in the `Input` parameter.

   ```JSON
   https://vod.byteplusapi.com?Action=StartWorkflow&Version=2023-01-01
   {
     "Vid": "v0d399g10001***aljhtddi6hgvn0",
     "TemplateId": "a378f66a5bc2495***5fc14ac109625f",
     "Input": "{\"OverrideParams\": {\"TranscodeVideo\": [{\"TemplateId\": [\"All\"],\"Encryption\": {\"Kid\":\"68637bee559c7a***99f8c500e9840a\"}}]}}"
   }
   ```
   

4. Check the transcoding result.

   * **Console:** 

      1. Log in to the [BytePlus VOD console](https://console.byteplus.com/vodpaas/totalOverview/) and enter the specified space.

      2. On the **Media assets** \> **Videos** page, click the **Details** in the **Action** column of the target video.

      3. Click the **Playback address** tab. The output stream will be marked as **Standard encrypted**. \*\*\*\*

   * **Event callback notification:**  Configure the [WorkflowComplete](https://docs.byteplus.com/docs/byteplus-vod/docs-workflowcomplete) event to receive a callback when the job is complete. The callback payload will indicate if the output is encrypted.


<span id="6cdfbc30"></span>
### Step 3: Configuring HLS encryption rewrite (recommended)

This feature adds encryption parameters (including the encryption algorithm, key URI, and authentication parameters) to the `#EXT-X-KEY` tag in the M3U8 file. The client receives the rewritten M3U8 file and uses the tokenized URI to request the key. After obtaining the key, the player uses the corresponding encryption algorithm and key to decrypt the TS file. By configuring this feature, you can secure the HLS key delivery process. For the detailed setup instructions, see [HLS standard encryption rewrite](https://docs.byteplus.com/docs/byteplus-vod/hls_standard_encryption_rewrite).

After enabling this feature, your application client must initiate an access request for the M3U8 file to the CDN node using an `AppAuthToken`. You need to append `AppAuthToken=<token>` to the end of the M3U8 URL.


* **Original M3U8 URL example:**  `https://demo.bytedance.com/index.m3u8`

* **URL for player example:**  `https://demo.bytedance.com/index.m3u8?AppAuthToken=<token>`


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You need to build your own token service to generate the <code>AppAuthToken</code>. <code>AppAuthToken</code> is the default parameter name but can be customized when you have configured the HLS standard encryption rewrite feature in the BytePlus VOD console.</div>


<span id="8220d740"></span>
### **Step 4:**  Playing encrypted content

<span id="315d1ef9"></span>
#### Overall process

The overall process for decrypted playback is shown below. The client first obtains the video's M3U8 playback address and then fetches the decryption key based on the information in the M3U8 file.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3f83a60c5f5485699186ed1ac3cba58~tplv-goo7wpa0wc-image.image) </span>


1. **Playback request:**  The client requests playback from your application server. Your server performs business logic checks (such as user authentication and subscription status) and then generates a short\-lived `PlayAuthToken` or a signed playback URL.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">In DirectURL mode, where the playback URL is set directly in the player's SDK, your application server returns the video's playback address to the client after completing the logic checks.   </div>
   

2. **Fetch playback info:**  The client passes the `Vid` and `PlayAuthToken` to the Player SDK, which calls the `GetPlayInfo` API to retrieve video metadata, including the M3U8 PlayURL from the CDN. The M3U8 file contains the addresses of TS files and an address (URI) to fetch the decryption key.

3. **Fetch decryption key:**  The Player SDK must first obtain the decryption key to play encrypted segments. For detailed methods, see [Step 1: Setting up a key delivery service](https://docs.byteplus.com/docs/byteplus-vod/docs-standard-encryption#8cfc00b2).

   * Assuming the M3U8 file is as follows:

      ```Plain
      #EXTM3U
      #EXT-X-VERSION:3
      #EXT-X-TARGETDURATION:10
      #EXT-X-KEY:METHOD=AES-128,URI="https://example.com/kds/api/v1/keys?source=jarvis&ak=685e86b66c******9723be88b010c03ab",IV=0x000000000000000000$99999999999999999,
      #EXTINF:10,
      segment1.ts
      #EXTINF:10,
      segment2.ts
      #EXT-X-ENDLIST
      ```
      

   * The player downloads the M3U8 file, parses the `#EXT-X-KEY` tag to find the key URI, and sends a request to your key delivery service. Your key delivery service returns the corresponding decryption key based on the `ak` parameter.

4. **Decrypt and play:**  The player receives the key, decrypts the video segments (TS files), and begins playback.


<span id="b88f9ab7"></span>
#### Getting playback information

You can initiate playback using either a temporary playback token (see [Playing videos with temporary playback tokens](https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-temporary-playback-tokens)) or a direct playback URL (see [Playing videos with playback addresses](https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-playback-addresses)). The key requirement for playing HLS standard encrypted videos is: on your application server, when calling the `GetPlayInfo` API or issuing a `PlayAuthToken`, you **must** set the `FileType` parameter to `standard_evideo` (for encrypted video) or `standard_eaudio` (for encrypted audio) to ensure you receive the correct playback information for the HLS encrypted stream. Beyond this parameter, all other player configurations are identical to playing standard, unencrypted videos.

<span id="4acce4a7"></span>
#### Playback options

You can play HLS standard encrypted videos using either the BytePlus VOD Player SDKs or a third\-party player.

<span id="cb69740e"></span>
##### **Using BytePlus VOD Player SDK (recommended)** 

For more details, please refer to the following documents:


* Web Player SDK: [Playing HLS standard encrypted videos](https://docs.byteplus.com/docs/byteplus-vod/playing_hls_standard_encrypted_videos_web_new#8830576c)

* Android Player SDK: [Playing HLS standard encrypted videos](https://docs.byteplus.com/docs/byteplus-vod/docs-implementing-basic-features-android#4e387004)

* iOS Player SDK: [Playing HLS standard encrypted videos](https://docs.byteplus.com/docs/byteplus-vod/docs-implementing-basic-features-ios#d9fa839e)


<span id="6ed9c8a3"></span>
##### **Using a third\-party player**

If you use a third\-party player, you are responsible for implementing the entire key fetching and decryption logic yourself. The process is as follows:


1. **Obtain playback URL:**  Fetch the M3U8 playback URL from the BytePlus VOD service. For details, see [Obtaining playback addresses](https://docs.byteplus.com/docs/byteplus-vod/docs-playing-videos-with-playback-addresses#a46c2be1).

2. **Parse Key URI:**  On the client side, download the M3U8 manifest and parse the `#EXT-X-KEY` tag to extract the key delivery URI.

3. **Request decryption key:**  Send a request from the client to the extracted URI to fetch the decryption key.

4. **Decrypt and play:**  Pass the fetched key to the player, which will use it to decrypt the video stream for playback.
