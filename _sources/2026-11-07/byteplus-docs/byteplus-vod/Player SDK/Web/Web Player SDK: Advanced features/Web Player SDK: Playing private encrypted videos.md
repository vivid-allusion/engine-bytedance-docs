---
title: "Web Player SDK: Playing private encrypted videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/playing_private_encrypted_videos_web"
---

BytePlus VOD offers a private encryption solution using a highly secure algorithm to safeguard your audio and video copyrights.

<span id="ef817454"></span>
## Compatibility

The Web Player SDK supports the playback of privately encrypted videos in HLS, MP4, and DASH formats. The specific compatibility details are shown in the table below.


|**System/Browser** |**Description** |
|---|---|
|PC Chrome |Supports HLS, MP4, and DASH protocols on version 34 and above. |
|PC Edge |Supports HLS, MP4, and DASH protocols on Windows 10 and above. |
|iOS Mobile |Supports iOS 10 and later, with the exception of versions 11.2 to 11.4, which are **not** supported. Only the HLS protocol is compatible. Due to the lack of necessary APIs such as [MSE](https://developer.mozilla.org/en-US/docs/Web/API/MediaSource) (Media Source Extensions) in iOS browsers, the MP4 format and DASH protocol are not supported. |
|Android Mobile |Supports HLS, MP4, and DASH formats on Android 5 and later. Please note that this feature may not function correctly in environments where the player is hijacked. Such environments include, but are not limited to, UC Browser, QQ Browser, and some default browsers from phone manufacturers (e.g., the VIVO default browser). |


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip">Playback in a live <code>http://</code> environment is not supported. However, this does not affect debugging in <code>localhost</code> and <code>127.0.0.1</code> environments.</div>


<span id="4584d930"></span>
## Prerequisites

Encrypt your audio and video files using the BytePlus VOD media processing service. For details, see [Private encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-private-encryption).

<span id="fa47102e"></span>
## Playback in Vid mode

<span id="21e2b459"></span>
### Overall process

The overall decryption and playback process for Vid mode on web is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06bedd1d00d84123956aba3babaec613~tplv-goo7wpa0wc-image.image) </span>


1. **Client\-side key generation**: The process begins on the client device. The BytePlus Player SDK generates a unique device identifier (`UnionInfo`) and a public key (`DrmKek`). This pair of credentials serves as the foundation for the secure playback session.

2. **Token authorization**: The client sends the newly generated `UnionInfo` and `DrmKek` to your application server. Your server, acting as a trusted authority, uses the BytePlus VOD Server SDK to generate a short\-lived, signed playback token. This token essentially grants the specific device permission to play the video.

3. **Requesting playback info**: The Player SDK then sends a request to the BytePlus VOD service, presenting the Video ID (Vid) and the temporary token it received from your server.

4. **Secure key delivery**: The BytePlus VOD service validates the token. Upon successful validation, it uses the public key (`DrmKek`) provided by the client to encrypt the actual video decryption key. This critical step ensures that only the original device holding the corresponding private key can decrypt the video key. The VOD service then returns the encrypted video key and the video's streaming address (PlayUrl) to the client.

5. **Fetching video content**: The Player SDK requests the encrypted video content from the CDN using the provided `PlayUrl`.

6. **Decryption and playback**: Internally, the Player SDK uses its private key to decrypt the video key it received from the VOD service. With the actual key now available, the SDK can decrypt the video stream from the CDN in real\-time as it plays.


<span id="fdc83f5d"></span>
### Implementation steps

This section provides a step\-by\-step guide for developers to implement the playback of private encrypted videos.


1. **Generate** **`unionInfo`** ** and ** **`drmKeK`**: Call the Player SDK's `generateEncryptInfo` method to generate the `sessionId`, `drmKeK`, and `unionInfo`.

   ```JavaScript
   const unionId = 'user_xxxx'; // A unique identifier for the device
   const format = 'hls'; // The format of the private encrypted video. Supported values: 'hls', 'mp4', 'dash'
   
   const { drmKeK, unionInfo, sessionId } = await VePlayer.generateEncryptInfo(unionId, format);
   ```
   

   **Input parameters:** 

   * `unionId`: A unique identifier for the device, used to ensure a one\-to\-one correspondence between the key and the device, thereby enhancing security.

   * `format`: The format of the video to be played. If you need to play videos in multiple formats, you must call this method for each format.

      **Return value:** 

   * `drmKeK`: The obfuscated public encryption key, used to generate the temporary playback token in the next step.

   * `unionInfo`: The unique device information, used to generate the temporary playback token in the next step.

   * `sessionId`: A session identifier for private encryption, used for initializing the player later.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>generateEncryptInfo</code> method should only be called once. After calling it, do not refresh or navigate away from the page until the player has been initialized.   </div>
   

2. **Request a temporary playback token**: Send a request to your application's web server with the `drmKeK` and `unionInfo` generated in the previous step to obtain a temporary playback token. The application server generates a temporary playback token locally using the VOD Server SDK and then sends it back to the client.

   When generating the token on the server, you must set the following parameters:

   * `Vid`: Set to the ID of the video to play.

   * `Format`: Set to the same format used in Step 1 (for example, `hls`). If this parameter is not specified, it defaults to `mp4`.

   * `FileType`: Set to `private_evideo`.

   * `JSPlayer`: Set to `1`.

   * `UnionInfo`: Set to the `unionInfo` generated by the Player SDK.

   * `DrmKEK`: Set to the `drmKek` generated by the Player SDK.

   * `Ssl`: Set to `1`. Web playback only supports HTTPS playback addresses.

   * `X-Expires`: The validity period of the token, in seconds. We recommend setting it to one hour. A period that is too long increases the risk of the token being leaked, while one that is too short may cause it to expire before playback.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Set the Format parameter   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you need to play HLS (or DASH) streams, you must explicitly set <code>Format</code> to the desired format. When <code>Format</code> is omitted, the token defaults to <code>mp4</code>, and the player will only receive an MP4 playback address even if HLS encryption and transcoding are configured.   </div>
   

   For specific code examples, please refer to the following documents:

   * [Java SDK - Generating temporary playback token](https://docs.byteplus.com/en/docs/byteplus-vod/docs-java-sdk#generating-temporary-playback-token)

   * [Python SDK - Generating temporary playback token](https://docs.byteplus.com/en/docs/byteplus-vod/docs-python-sdk#generating-temporary-playback-token)

   * [PHP SDK - Generating temporary playback token](https://docs.byteplus.com/en/docs/byteplus-vod/docs-php-sdk#generating-temporary-playback-token)

   * [Go SDK - Generating temporary playback token](https://docs.byteplus.com/en/docs/byteplus-vod/docs-go-sdk#generating-temporary-playback-token)

   * [Node.js SDK - Generating temporary playback token](https://docs.byteplus.com/en/docs/byteplus-vod/docs-nodejs-sdk#generating-temporary-playback-token)

3. **Create the player**: Refer to the following code example to initialize the player. You need to set `encryptSessionId` to the `sessionId` returned by the `generateEncryptInfo` method in Step 1, and set `drmType` to `private_encrypt_upgrade`.

   ```JavaScript
   const playerSdk = new VePlayer({
       id: 'mse',
       lang: 'zh',
       width: 640,
       height: 360,
       defaultDefinition: '720p',
       drmType: 'private_encrypt_upgrade', // Encryption type: private encryption
       encryptSessionId: sessionId, // The sessionId returned by the generateEncryptInfo method
       getVideoByToken: {
         playAuthToken: 'playAuthToken with unionInfo and KEK', // The temp token from your app server, containing unionInfo and drmKeK
       },
   });
   ```
   

4.  **(Optional) Switch videos**: Call the `playNext` method and pass in the temporary playback token for the new video.

   ```JavaScript
   playerSdk.playNext({
     getVideoByToken: {
       playAuthToken: token, // The new temporary playback token
     },
   });
   ```
   


<span id="eaf5f9a7"></span>
## Playback in DirectUrl mode

<span id="92258255"></span>
### Overall process

The overall decryption and playback process for Vid mode on web is as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/13bb77e4fd7a4adba3001392d5d4d1ce~tplv-goo7wpa0wc-image.image) </span>


1. **Client\-side key generation**: The process begins on the client device. The BytePlus Player SDK generates a unique device identifier (`UnionInfo`) and a public key (`DrmKek`). This pair of credentials serves as the foundation for the secure playback session.

2. **Request playback info**: The client sends its public key to your application server. Your server then makes a direct call to the BytePlus VOD service's `GetPlayInfo` API.

3. **Secure key delivery to server**: The VOD service validates the request. It uses the client's public key to encrypt the video decryption key and returns this encrypted key (`PlayAuth`) and the video's direct streaming URL to your server.

4. **Player initialization**: Your server passes the direct URL and the encrypted key down to the client. The client then initializes the player with this information.

5. **Decryption and playback**: The Player SDK requests the encrypted video content from the URL. It uses its internal private key and the session ID to securely decrypt the `PlayAuth` and resolve the real video key. This key is then used for real\-time decryption and playback.


<span id="240ab5d2"></span>
### Implementation steps


1. **Generate** **`unionInfo`** ** and ** **`drmKeK`**: Call the Player SDK's `generateEncryptInfo` method to generate the `sessionId`, `drmKeK`, and `unionInfo`.

   ```JavaScript
   const unionId = 'user_xxxx'; // A unique identifier for the device
   const format = 'hls'; // The format of the private encrypted video. Supported values: 'hls', 'mp4', 'dash'
   
   const { drmKeK, unionInfo, sessionId } = await VePlayer.generateEncryptInfo(unionId, format);
   ```
   

   **Input parameters:** 

   * `unionId`: A unique identifier for the device, used to ensure a one\-to\-one correspondence between the key and the device, thereby enhancing security.

   * `format`: The format of the video to be played. If you need to play videos in multiple formats, you must call this method for each format.

      **Return value:** 

   * `drmKeK`: The obfuscated public encryption key, used to generate the temporary playback token in the next step.

   * `unionInfo`: The unique device information, used to generate the temporary playback token in the next step.

   * `sessionId`: A session identifier for private encryption, used for initializing the player later.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The <code>generateEncryptInfo</code> method should only be called once. After calling it, do not refresh or navigate away from the page until the player has been initialized.   </div>
   

2. **Request video address and playback key**: Your application server calls the `GetPlayInfo` API via the VOD Server SDK to get the video playback address and the encrypted playback key.

   When calling the API, you must set the following parameters:

   * `Vid`: Set to the ID of the video to play.

   * `Format`: Set to the same format used in Step 1 (for example, `hls`). If this parameter is not specified, it defaults to `mp4`.

   * `FileType`: Set to `private_evideo`.

   * `JSPlayer`: Set to `1`.

   * `UnionInfo`: Set to the `unionInfo` generated by the Player SDK.

   * `DrmKEK`: Set to the `drmKek` generated by the Player SDK.

   * `Ssl`: Set to `1`. Web playback only supports HTTPS playback addresses.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">Set the Format parameter   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If you need to play HLS (or DASH) streams, you must explicitly set <code>Format</code> to the desired format. When <code>Format</code> is omitted, <code>GetPlayInfo</code> defaults to <code>mp4</code> and returns an MP4 playback address even if HLS encryption and transcoding are configured.   </div>
   

   After receiving the request, the VOD service will encrypt the playback key and return the video address along with the encrypted key to your application server. These are returned in the `PlayAuthId` (the key ID) and `PlayAuth` (the encrypted key) parameters. For specific code examples, please refer to the following documents:

   * [Java SDK - Getting the playback address](https://github.com/byteplus-sdk/byteplus-sdk-java/blob/master/example/src/main/java/com/byteplus/example/vod/play/VodGetPlayInfoDemo.java)

   * [Python SDK - Getting the playback address](https://github.com/byteplus-sdk/byteplus-sdk-python/blob/master/byteplus_sdk/example/vod/play/GetPlayInfoExample.py)

   * [PHP SDK - Getting the playback address](https://github.com/byteplus-sdk/byteplus-sdk-php/blob/master/examples/Vod/DemoGetPlayInfo.php)

   * [Go SDK - Getting the playback address](https://github.com/byteplus-sdk/byteplus-sdk-golang/blob/master/example/vod/demo_vod_play_service_test.go)

   * [Node.js SDK - Getting the playback address](https://docs.byteplus.com/en/docs/byteplus-vod/docs-nodejs-sdk#getting-the-playback-addresses-with-the-video-id)

3. **Create the player**: Refer to the following code example to initialize the player. Pay attention to these parameters:

   * `encryptSessionId` is set to the `sessionId` returned from Step 1.

   * `drmType` is set to `private_encrypt_upgrade`.

   * `playAuth` and `playAuthId` are set to the key ID and encrypted key obtained in Step 2.

   ```JavaScript
   const playerSdk = new VePlayer({
       id: 'mse',
       lang: 'zh',
       width: 640,
       height: 360,
       streamType: 'hls',
       drmType: 'private_encrypt_upgrade', // Encryption type: private encryption
       encryptSessionId: sessionId, // The sessionId returned by the generateEncryptInfo method
       url: 'https://xxx.demo.com/1.m3u8',
       playAuth: 'nLwS81+KFNpqkBPAW4sXxmmJIZmZ',
       playAuthId: 'xsdsdsdsd',
   });
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">Note   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">If you are setting up multiple video definitions (resolutions), each item in the <code>playList</code> instantiation parameter must include its corresponding <code>playAuth</code> and <code>playAuthId</code>.   </div>
   

4.  **(Optional) Switch videos**: Call the `playNext` method and pass in the new video's URL, `playAuth`, and `playAuthId`.

   ```JavaScript
   playerSdk.playNext({
     url: 'newUrl',
     playAuth: 'new playAuth',
     playAuthId: 'new playAuthId'
   });
   ```
