---
title: "Video security overview"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-video-security-overview"
---

BytePlus VOD offers comprehensive and end\-to\-end security protection mechanisms, which you can choose to implement according to the security requirements of your specific business scenarios.

<span id="010bbda8"></span>
## Common forms of infringement

Online copyright infringement has become a significant challenge in areas such as copyrighted video content, self\-produced media, e\-commerce, entertainment social platforms and more. Widespread piracy directly affects publisher profits. For example, assume the latest hit TV series is only available to members on a video site, meaning that a membership is required to watch it. If the copyright protection mechanism of the video files is defective, resulting in mass downloading and re\-uploading of the videos, most viewers will not purchase a membership, which will have a devastating impact on the entire digital content industry chain.

The table below lists several common forms of infringement in the audio and video industry.


|**Infringement type** |**Description** #{style="min\-width: 100px;"}# |**Negative impact** |
|---|---|---|
|Hotlinking |Hotlinking is the illegal acquisition and distribution of playback URLs of audio and video assets. In this case, the infringer does not directly download or copy the content, but rather copies links to those resources, allowing users to access them without authorization.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/de54c5b82ed842e5b1eb6df6db572cd2~tplv-goo7wpa0wc-image.image) </span> |Bearing additional distribution costs without monetization |
|Software cracking |Software cracking is the illegal access, download, and dissemination of encrypted audio and video content using decryption technology.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a56f13686d4c4a65a77b478ad9fc73c6~tplv-goo7wpa0wc-image.image) </span> |Copyrighted videos are cracked and then widely disseminated |
|Piracy |Piracy is the use of various equipment and technology (such as screen recording software or cameras) to illegally copy and distribute audio and video content without the permission of the copyright holder.<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b3d9d85a35b4d1fab51153129d213dc~tplv-goo7wpa0wc-image.image) </span> |Copyrighted videos are widely disseminated |


<span id="338987d7"></span>
## BytePlus VOD copyright protection features

BytePlus VOD provides an end\-to\-end copyright protection solution, covering all stages from video upload to playback, as shown in the following diagram:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/752b0d2b86d74df6b8f8d82d54f0987b~tplv-goo7wpa0wc-image.image) </span>

These copyright protection capabilities can be used in tandem to address different forms of infringement. The following sections introduce three aspects of the copyright protection solution provided by BytePlus VOD: Content protection, access restriction, and piracy tracking.

<span id="5d45dc12"></span>
### Content protection


|**Copyright protection feature** |**Description** |**Security level** |**Difficulty** |
|---|---|---|---|
|[HLS standard encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-standard-encryption) |HLS standard encryption supports the common encryption method specified in [HTTP Live Streaming](https://tools.ietf.org/html/draft-pantos-http-live-streaming-23). It uses AES_128 to encrypt video content and works with all HLS players, but the keys are vulnerable to theft. |Medium |Medium, requires cloud configuration and self\-implementation of playback decryption logic |
|[Private encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-private-encryption) |The cloud\-based integrated video encryption solution developed by BytePlus uses a private encryption algorithm to ensure secure end\-to\-end transmission. This solution offers the following advantages over HLS standard encryption:<br><br><br>* Each video file has an independent key, effectively preventing security risks from the leak of a single key. The keys are also double\-encrypted for additional protection.<br><br>* Player SDKs are provided for Android, iOS, web, and other platforms, which can automatically decrypt and play encrypted content. The SDKs also support device\-level `UnionInfo` verification, which reduces the risk that videos can be played on any device in the event that the key is leaked.<br><br>* Downloads are secure, and videos downloaded locally are encrypted again, preventing theft even by methods not involving internet transmission. |High |Low, only requires simple cloud configuration and integration of [Player SDK overview](https://docs.byteplus.com/docs/byteplus-vod/docs-player-sdk-overview) |
|[DRM encryption overview](https://docs.byteplus.com/docs/byteplus-vod/docs-drm-encryption) |The industry\-standard encryption method for DRM (Digital Rights Management) is widely adopted. DRM encryption is supported at the system level by Apple's FairPlay, Google's Widevine, and Microsoft's PlayReady. |Extremely High |Medium, DRM involves encryption, licensing, authentication, and playback restrictions. Integrating all these components can be challenging. |
|[UploadMediaByUrl](https://docs.byteplus.com/en/docs/byteplus-vod/reference-uploadmediabyurl) |Bulk upload of media assets to the BytePlus VOD server via encrypted URL. The original URL is decrypted in the VOD server according to your pre\-set encryption algorithm and encryption key to ensure the security of the upload process. |Medium |Low, only requires cloud configuration |


<span id="9aca117d"></span>
### Supported encryption type by container format


|Container format |Supported encryption type |Supported encryption subtype |
|---|---|---|
|MP4 |Private encryption |/ |
|Dash |Private encryption |/ |
||DRM encryption |Widevine |
||Private Encryption |PlayReady |
|HLS |Private encryption |/ |
||DRM encryption |FairPlay + Widevine |
|||PlayReady |
||HLS standard encryption |/ |


<span id="af51b81a"></span>
### Access restriction


|**Copyright protection feature** |**Description** |**Security level** |**Difficulty** |
|---|---|---|---|
|[Referer restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-referer-restrictions) |Access control is based on the Referer field in the HTTP request header, but it is highly susceptible to forgery. |Low |Low, only requires cloud configuration |
|[UA restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-ua-restrictions) |Access control is based on the User\-Agent field in the HTTP request header, but it is highly susceptible to forgery. |Low |Low, only requires cloud configuration |
|[Origin restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-origin-restrictions) |Access control is based on the Origin field in the HTTP request header, but it is highly susceptible to forgery. |Low |Low, only requires cloud configuration |
|[IP restrictions](https://docs.byteplus.com/docs/byteplus-vod/docs-ip-restrictions) |Denying or allowing access only from specific IP addresses is not suitable for distribution to a large number of end users. |Low |Low, only requires cloud configuration |
|[URL signing overview](https://docs.byteplus.com/docs/byteplus-vod/docs-url-authentication-overview) |When the client sends a request to the server, it computes the signature according to the signature rules you set and includes the signature in the request. After the server receives the request, it needs to verify the signature. The server responds to the request only if the signature passes verification.<br><br>The URL's validity period can also be configured. After the validity period expires, the playback URL fetched through the `GetPlayInfo` interface will no longer be playable. |Low |Medium, use the API to fetch the dynamic URL or concatenate it yourself according to the rules |
|[Remote authentication](https://docs.byteplus.com/docs/byteplus-vod/docs-remote-authentication) |BytePlus VOD forwards client\-side requests to your authentication server for authentication. Suitable for scenarios where your site has a dedicated authentication server and the business has high security requirements. |Medium |High, you need to deploy your own authentication server and ensure high availability |


<span id="9cb45524"></span>
### Piracy tracking


|**Copyright protection feature** |**Description** |**Security level** |**Difficulty** |
|---|---|---|---|
|[Watermark and ad insertion](https://docs.byteplus.com/docs/byteplus-vod/docs-watermark-and-ad-insertion) |Add a picture, video, or text watermark to a video using BytePlus VOD's media processing capabilities. |Low |Low, only requires cloud configuration |


<span id="15b194b3"></span>
## Encryption scheme comparison

<span id="fbc01a45"></span>
### Comparison between BytePlus private encryption and HLS standard encryption


|Category |Comparison |
|---|---|
|Security level |BytePlus private encryption \> HLS standard encryption |
|Ease of use |BytePlus private encryption \> HLS standard encryption |
|Versatility |HLS standard encryption \> BytePlus private encryption<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">HLS standard encryption: Adapted to all HLS playback scenarios, playable by players that support HLS standard encryption.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">BytePlus private encryption: Player SDK (web, Android, iOS, Flutter, React Native)</div><br> |
|Usage fee |BytePlus private encryption = HLS standard encryption<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">No additional cost.</div><br> |


<span id="14f4313f"></span>
### Comparison between DRM and BytePlus private encryption

BytePlus VOD supports both DRM and private encryption solutions. From encrypting content at the media processing end to decrypting it at the playback end, it can effectively prevent various video cracking behaviors from end to end, ensuring media copyright and content security.

Comparison of these encryption schemes:


|Encryption Scheme |Description |Scheme details |Compatibility of Playback Endpoints |
|---|---|---|---|
|DRM encryption |The industry\-standard encryption method for DRM (Digital Rights Management) is widely adopted. DRM encryption is supported at the system level by Apple's FairPlay, Google's Widevine, and Microsoft's PlayReady. |The InterTrust Encryption Cooperation Solution ensures that content keys are securely managed through protocols specifically engineered within the DRM system. |FairPlay and Widevine support corresponding devices according to the requirements of Apple and Android, respectively. PlayReady only supports some browsers. |
|Private encryption |BytePlus VOD's self\-developed encryption solution encrypts and protects video content, effectively preventing issues such as video leakage, hotlinking, and pirated downloads. |The self\-developed encryption solution secures content keys using BytePlus VOD's proprietary protocol, ensuring robust protection and reliability. |It needs to be used in conjunction with the BytePlus VOD player. |


<span id="bebf3439"></span>
#### Usage scenario


|Encryption Scheme |Security level |Usage scenario |Compatibility of Playback Endpoints |
|---|---|---|---|
|DRM encryption |Extremely high. Hardware\-level encryption solution to meet the needs of global video content providers. |Media platforms<br><br>Copyrighted TV dramas<br><br>Self\-produced content |Video content, whether from professional studios or self\-produced, involves significant costs and copyright authorization, making robust protection essential. For such content, a commercial DRM solution with system\-level encryption is highly recommended to prevent copyright leakage. |
|Private encryption |High. The solution effectively defends against cracking attempts carried out by browser plugins and gray\-market tools, ensuring enhanced content security. |E\-commerce and pan\-entertainment |For daily live streaming recordings and video content intended for social media platforms, strong anti\-cracking and anti\-downloading measures are required. Considering cost efficiency, a private encryption solution is recommended to provide end\-to\-end protection, encrypting content from the server to the client and ensuring secure playback. |


<span id="29a6b70c"></span>
#### Reference


* For commercial DRM, please refer to [DRM encryption overview](https://docs.byteplus.com/docs/byteplus-vod/docs-drm-encryption).

* For private encryption, please refer to [Private encryption](https://docs.byteplus.com/docs/byteplus-vod/docs-private-encryption)
