---
title: "Flutter Player SDK: Playing private encrypted videos"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-flutter-player-playing-private-encrypted-videos"
---

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">Note</div>


<div data-tips="true" data-tips-type="tip"><strong>Applicable version</strong>: byteplus_vod Flutter SDK ≥ <strong>1.51.201</strong></div>


<div data-tips="true" data-tips-type="tip"><strong>Platforms</strong>: iOS and Android</div>


<div data-tips="true" data-tips-type="tip"><strong>Overview</strong>: This document describes the client\-side integration flow for playing BytePlus VOD private encrypted videos with the Flutter Player SDK. The client obtains device binding information from the Player SDK, your application server uses it to issue a short\-lived <code>PlayAuthToken</code>, and the client then creates a playback source using the Vid and the <code>PlayAuthToken</code>.</div>


<span id="overview"></span>
## Overview

BytePlus VOD offers a [private encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-private-encryption) solution that uses a proprietary algorithm to protect your audio and video copyrights. To play a private encrypted video, the client obtains device binding information (`UnionInfo` and `DrmKEK`) from the Player SDK and sends it to your application server. Your server uses this information to issue a short\-lived, signed `PlayAuthToken`. The client then uses the Vid and the `PlayAuthToken` to create the playback source. Long\-term credentials and the token\-signing logic stay on the server.

<span id="prerequisites"></span>
## Prerequisites


* Integrate Flutter Player SDK version 1.51.201 or later.

* Complete Player SDK initialization with a valid AppID and a player License that includes the corresponding DRM capability.

* Process the video with the BytePlus VOD private encryption solution. For details, see [Private encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-private-encryption).

* Your application server can issue a `PlayAuthToken`. Long\-term credentials such as the AK/SK are stored only on the server. You can use the BytePlus VOD Server SDKs to generate the token. For more information, see the following documentation:

   * [PHP SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-php-sdk)

   * [Python SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-python-sdk)

   * [Go SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-go-sdk)

   * [Java SDK](https://docs.byteplus.com/docs/byteplus-vod/docs-java-sdk)


<span id="playback-flow"></span>
## Playback flow


1. The client calls `getEngineUniqueId()` to obtain the `UnionInfo`, and calls `getEngineUniqueKek()` to obtain the `DrmKEK`.

2. The client sends the Vid, `UnionInfo`, and `DrmKEK` to a server endpoint protected by your own authentication.

3. Your application server uses the Server SDK or a controlled signing service to generate a short\-lived `PlayAuthToken` with `FileType=private_evideo`.

4. The server returns only the Vid and the `PlayAuthToken` to the client.

5. The client creates a `TTVideoEngineVidSource`, sets the playback source, and starts playback.


<span id="obtain-the-device-binding-information"></span>
## Obtain the device binding information

```Dart
final supported = await FlutterTTSDKManager.isDeviceSupportDrm();
if (supported != true) {
  throw StateError('The current device does not support DRM playback');
}

final unionInfo = await FlutterTTSDKManager.getEngineUniqueId();
final drmKek = await FlutterTTSDKManager.getEngineUniqueKek();

if (unionInfo == null ||
    unionInfo.isEmpty ||
    drmKek == null ||
    drmKek.isEmpty) {
  throw StateError('The Player SDK did not return the device binding information');
}
```


The following table describes the fields that your application server uses to issue the token:


|Field |Value or source |
|---|---|
|`Vid` |The Vid of the private encrypted video to play. |
|`FileType` |Fixed to `private_evideo`. |
|`UnionInfo` |The return value of `getEngineUniqueId()` on the client. |
|`DrmKEK` |The return value of `getEngineUniqueKek()` on the client. |
|`Format` |Configured based on the actual video and your server's signing endpoint, for example `hls`, `dash`, or `mp4`. |


<span id="play-with-a-playauthtoken"></span>
## Play with a PlayAuthToken

```Dart
final playAuthToken = await requestPrivatePlayAuthToken(
  vid: vid,
  unionInfo: unionInfo,
  drmKek: drmKek,
);

final player = VodPlayerFlutter();
await player.createPlayer();

final source = TTVideoEngineVidSource.init(
  vid: vid,
  playAuthToken: playAuthToken,
);

await player.setMediaSource(source);
await player.play();
```


`requestPrivatePlayAuthToken` represents your own authenticated endpoint. It generates a `playAuthToken` based on the `vid`, `unionInfo`, and `drmKek`.

<span id="faq"></span>
## FAQ

**The ** **`UnionInfo`** ** or ** **`DrmKEK`** ** cannot be obtained.** 

Confirm that the Player SDK is initialized and the License is valid, and check whether the current device supports DRM.

**The server returns a token, but playback fails.** 

Check whether the Vid, `FileType`, `UnionInfo`, `DrmKEK`, and the token validity period are consistent. Confirm that the signing information comes from the current playback device.

**Can the token be issued on the client?** 

No. The client only obtains the device binding information and plays with the token. Long\-term credentials and the signing logic must stay on the server.
