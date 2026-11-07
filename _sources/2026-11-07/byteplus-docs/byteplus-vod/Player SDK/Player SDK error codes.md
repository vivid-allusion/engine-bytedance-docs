---
title: "Player SDK error codes"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-error-code"
---

When you encounter an error while using the Player SDK, this reference guide helps you quickly identify the cause and find a solution. It lists common error codes for Android, iOS, and Web SDKs, along with detailed descriptions and troubleshooting tips to resolve playback issues.

<span id="0e7e4559"></span>
## General error codes of the Android and iOS Player SDK


|**Error code** |**Description** |**Troubleshooting tip** |
|---|---|---|
|\-499999 |Empty setting |Restart the player. |
|\-499998 |Failed to set the decoder. |The video encoding format is not supported and cannot be decoded. Please re\-transcode the video. |
|\-499997 |Failed to launch the decoder. |Restart the player. |
|\-499996 |Failed to open the decoder. |Restart the player. |
|\-499995 |Failed to set the output. |An internal player error caused by \-499999. Re\-transcode the video. |
|\-499994 |Failed to output and display the error. |An internal player error caused by \-499996. |
|\-499993 |Failed to open the output. |Restart the player. |
|\-499992 |Failed to output and display the error. |Restart the player. |
|\-499991 |Failed to launch the video output. |Restart the player. |
|\-499990 |Failed to launch the audio output. |Restart the player. |
|\-499989 |Failed to launch the video device. |Restart the player and report your phone model to BytePlus technical support. |
|\-499988 |Empty video URL |Change the video URL. |
|\-499987 |Invalid video URL |The player considers URLs less than 8 characters to be invalid. Change the video URL. |
|\-499986 |The URL is not an MP4 file. |Change the video URL. |
|\-499985 |Invalid input |The URL corresponding to the data is not a valid video file. Change the video URL. |
|\-499984 |End of file |None |
|\-499983 |Not a video stream |If you encounter this error while playing an audio file, please check the version of ttffmpeg, as supported audio formats may differ. |
|\-499982 |Timeout while the player buffers the video. |Prompt users to switch to a different network. |
|\-499981 |Failed to open the decoder. |Check whether the player supports the video format or whether there are errors in the video file. |
|\-499980 |URL is empty or URL length is less than 8 characters. |Use a valid URL instead. |
|\-499979 |Failed to open the audio filter. |Check whether the audio channel, sample rate, and audio format are normal. |
|\-499978 |The audio decoder in the player failed to read or write data. |Check for errors in the video file or restart the player. |
|\-499977 |The video decoder in the player failed to read or write data. |Check for errors in the video file or restart the player. |
|\-499976 |Failed to seek to a specific position and play. |Restart the player. |
|\-499975 |Network error |Prompt users to switch to a different network. |
|\-499974 |Unexpected EOF |The decoder has ended unexpectedly and cannot be processed at this time. |
|\-499973 |The decryption key is null. |Check whether the decryption key is set correctly. |
|\-499972 |The player is hijacked. |Check whether there has been a hijacking attempt. |
|\-499971 |No stream |Check for data transfer errors. |
|\-499899 |The HTTP 400 error: The request contains bad syntax. |Change the video URL.<br><br>> For all HTTP errors, you can retrieve the currently received HTTP message network packet through the `getStringOption` (`HTTP_RECEIVE_HEADER`) method. The HTTP message has a maximum of 4096 bytes. |
|\-499898 |The HTTP 401 error: Unauthorized HTTP access. |Change the video URL. |
|\-499897 |The HTTP 403 error: Access forbidden. |Change the video URL. |
|\-499896 |The HTTP 404 error: Resource not found. |Change the video URL. |
|\-499895 |The HTTP timeout error |Check whether the video URL is valid or change the video URL. |
|\-499894 |Other HTTP 4xx errors |Change the video URL. |
|\-499893 |HTTP 5xx server errors |Change the video URL. |
|\-499892 |HTTP download interrupted by the user |None |
|\-499891 |Invalid HTTP content |You can set the valid HTTP content format by calling the `setStringOption (VALID_HTTP_CONTENT, "video/mp4 html/text")` method. Multiple content formats should be separated by spaces. If not set, all formats are valid by default. If non\-video data in the HTTP request is sent to the decoder, the \-499978 error will be reported. |
|\-499890 |The HTTP redirection error |When encountering the HTTP 3xx redirection status codes, the player redirects by default. You can turn off the player's 3xx redirection through the `setIntOption (HTTP_RECONNECT_OPTION, 0)` method. After redirection is disabled, when an HTTP 3xx status code occurs, an HTTP_REDIRECT error will be thrown, and you can retrieve the current HTTP header data through the `getStringOption(HTTP_RECEIVE_HEADER)` method. |
|\-499799 |Failed to resolve the domain name in the TCP layer. |This error only occurs when the player starts playing but has not yet received data. Change the video URL. |
|\-499798 |Timeout while resolving the domain name in the TCP layer. |Prompt users to switch to a different network. |
|\-499797 |Failed to establish a socket connection. |You can retrieve the reason for the failure through the `getIntOption (SYS_ERROR_CODE_OPTION)` method. This error only occurs when establishing a socket connection. It is recommended that you change the video URL or inform the user of poor network conditions. |
|\-499796 |Failed to establish a socket connection. |You can retrieve the reason for the failure through the `getIntOption (SYS_ERROR_CODE_OPTION)` method. This error only occurs when establishing a socket connection. It is recommended that you change the video URL or inform the user of poor network conditions. |
|\-499795 |Failed to send data with the socket. |Domain name resolution was successful, but HTTP failed to send data with the socket. You can retrieve the reason for the failure through the `getIntOption(SYS_ERROR_CODE_OPTION)` method. At this time, the player has not yet received data. It is recommended that you change the video URL or inform the user of poor network conditions. |
|\-499794 |Failed to receive data with the socket. |Domain name resolution and the HTTP request were both successful, but HTTP failed to receive data with the socket. You can retrieve the reason for the failure through the `getIntOption(SYS_ERROR_CODE_OPTION)` method. It is recommended that you change the video URL or inform the user of poor network conditions. |
|\-499793 |Timeout while receiving data with the socket. |Domain name resolution and the HTTP request were both successful. However, the socket has been blocked due to other network operations before receiving data, resulting in a timeout. This situation can occur when playback is started or during playback, but you can differentiate between the two cases based on the current playback time. We suggest you change the video URL or inform the user of poor network conditions. |
|\-499792 |Timeout while receiving data with the socket. |Domain name resolution and the HTTP request were both successful. However, the socket has been blocked due to other network operations before receiving data, resulting in a timeout. This situation can occur when playback is started or during playback, but you can differentiate between the two cases based on the current playback time. We suggest you change the video URL or inform the user of poor network conditions. |
|\-59983 |Too much redirection |None |
|\-59987 |Failed to receive data with the socket. |Change the video URL or inform the user of poor network conditions. |
|\-59989 |Timeout while receiving data with the socket. |Change the video URL or inform the user of poor network conditions. |
|\-59990 |Failed to establish a socket connection. |Inform the user of poor network conditions. |
|\-59997 |Timeout while resolving the domain name in the TCP layer. |The player has not yet requested data, and the error will only occur when it starts playing. |
|\-59998 |Failed to resolve the domain name in the TCP layer. |The player has not yet requested data, and the error will only occur when it starts playing. |
|\-499960 |Invalid data source |Check whether there are any CDN, video transcoding, video source issues. |
|\-1094995529<br><br>> Deprecated and replaced by \-499960. |Invalid data source |Check whether there are any CDN, video transcoding, video source issues. |
|\-30001 |Failed to authenticate the user with the license. |Check whether the license has expired and whether the app ID and package name match the information registered in the BytePlus VOD console. |
|\-2139062143 |This error code appears in the old version of the player. |Update to a newer version of the player. |
|\-1414092869 |Unexpected exit caused by network jitter. |Change the video URL or check the network. |
|\-499697 |Playback failed because the encrypted video's expiration time had passed before playback was initiated. |Use an unexpired video source or check whether the system local time is normal. |
|\-499696 |Playback failed due to missing or invalid encrypted local time data. Either the encrypted local time was not passed in the callback, or an error occurred during decryption. |Check whether the local time setting of private encryption is normal. |
|\-1129137469 |This usually indicates a network issue, such as a loss of internet connection or a weak network signal while switching resolutions. This can prevent the device from downloading the data for the new resolution. |Check the internet connection. |
|\-110001 |The resolution you're trying to switch to is the same as the current resolution. |Check the resolution you're trying to switch to. |
|\-110002 |There is no available video source data. |Check the video source data. |
|\-1001 |Preloading: Duplicate task exists with the same `cacheKey`. |This error can be ignored. If it occurs frequently, it is recommended to check the preloading task list. |
|\-1002 |Preloading: Too many preloading tasks are in progress. |Wait for the remaining preloading tasks to finish before retrying. |
|\-1003 |Preloading: Connection establishment failed. |Retry a limited number of times. |
|\-2000 |Preloading: No error status code received, but the file length is invalid; `content-length` is abnormal. |Retry a limited number of times. |
|\-3000 |Preloading: 4xx error, possibly due to an expired URL. |Update the URL and retry. |
|\-3001 |Preloading: 5xx error, server error or local gateway error. |Retry a limited number of times. |
|\-4000 |Preloading: Incorrect request parameters, such as `cacheKey` or `url` being empty. |Check the parameters and retry. |
|\-9995 |Downloading Video: User called the `invalidateAndCancel` method to delete a download task. The deletion process is asynchronous. Once the deletion is complete, the SDK will trigger the `downloaderDidComplete` callback. The callback parameter `error` will not be empty; `error.code` will be \-9995. |No action needed. |
|\-9960 |Downloading Video: User's current network is unavailable. |Advise the user to check their network status. |
|\-9949 |Downloading Video: Database error occurred. |Delete the current download task and restart the download. |
|\-9948 |Downloading Video: Disk write error. |Delete the current download task and restart the download. |
|\-9947 |Downloading Video: When the SDK triggers a download task, it checks the available disk space. If the free space is less than `LimitFreeDiskSize`, this error occurs. |Advise the user to clear some space before downloading. |
|\-9946 |Downloading Video: When calling `loadAllTasks`, if the SDK's data loading module hasn't been started, this error will be returned in the `downloaderDidLoadAllTask` callback. |Start the SDK's data loading module and retry. |
|\-9945 |Downloading Video: The URL is unavailable. |Check the download task's URL and retry. |
|\-9944 |Downloading Video: URL request returned a 500 error or similar, preventing the resource from being downloaded. |Change the URL or indicate that the download is not possible (service unavailable). |
|\-9999 |Downloading Video: Vid download task parameters are empty. |Check the download task parameters and retry. |
|\-9990 |Downloading Video: Vid download task authentication failed. |Check and update the `playAuthToken`. |
|\-9997 |Downloading Video: The server returned an empty result. |Retry. |
|\-9994 |Downloading Video: Network issue. |Retry. |


<span id="79e01437"></span>
## Error codes specific to the play method


|**Error code** |**Enum** |**Description** |
|---|---|---|
|\-9959 |ModelUrlExpired |The URL in `videomodel` has expired. |
|\-9967 |UrlEmpty |The URL is null. |
|\-9969 |TTVideoEngineErrorAuthFail |Authentication failed. |
|\-9987 |VideoDecryptFailed |Failed to decrypt the video or the system player failed to play the encrypted video. |
|\-9988 |DecodeEncryptionKeyError |The key was unable to decrypt the video. |
|\-9989 |CreatePLuginPlayerFailed |Failed to create an external player plugin. |
|\-9990 |TTVideoEngineErrorInvalidRequest |Authentication failed. Refer to `kTTVideoEngineAPIRetCodeKey` in the error userinfo for details. |
|\-9991 |TTVideoEngineErrorVideoValidateFail |The video headers could not be verified. |
|\-9992 |PlayerStateIllegal |* This error code in the Android SDK indicates that the system player is not functioning properly.<br><br>* This error code in the iOS SDK indicates that the IP address of the local cache is empty. |
|\-9993 |TTVideoEngineErrorInvalidURLFormat |* This error code in the Android SDK indicates that the system player cannot be created.<br><br>* This error code in the iOS SDK indicates that the URL provided by the application to the `play` method is not in the correct format. |
|\-9994 |TTVideoEngineErrorHTTPNot200 |The status code returned by the HTTP request is not 200, or the request to call the `play` method failed, commonly due to a poor network. |
|\-9995 |TTVideoEngineErrorUserCancel |The local DNS resolution takes too long, and the user cancels. |
|\-9996 |TTVideoEngineErrorResultNotApplicable |The url returned by the `play` method is invalid. |
|\-9997 |TTVideoEngineErrorResultEmpty |The request returns a null result. This can mean the DNS resolution result is null, or the `videomodel` or `urls` returned by the `play` method are null. |
|\-9998 |TTVideoEngineErrorParsingResponse |The `play` method parsing failed for one of the following reasons:<br><br><br>* `video_info` is empty<br><br>* `Code` is not equal to 0<br><br>* Failed to resolve the Data field |
|\-9999 |TTVideoEngineErrorParameterNull |The `url` parameter passed by the application to the SDK is either empty or in the wrong format. |
|\-10000 |TTVideoEngineErrorTimeout |Timeout occurred while calling the `play` method or during DNS resolution. |


<span id="0a81251d"></span>
## Error codes of the Web Player SDK

<span id="eee731bb"></span>
### veErrorCode

Starting with version 1.10.0, the Web Player SDK has optimized error codes, adding veErrorCode to provide more detailed error information. Please refer to [Listening for player error](https://docs.byteplus.com/docs/byteplus-vod/docs-implementing-basic-features-web#ad54b612) for more details.


|**Error code** |**Description** |**Troubleshooting tip** |
|---|---|---|
|1100 |HLS parsing error. |Check if the current M3U8 file format is correct. |
|1200 |MPD parsing error. |Check if the MPD file conforms to the standard. |
|2100 |Network error. |Check for general network issues, such as cross\-domain request failures or other 4xx/5xx errors. |
|2101 |Network request timeout. |Check the network status. |
|2103 |Request returned 403. |Authentication failed or address expired. Re\-acquire the playback address. |
|2116 |Incorrect request range. |This usually occurs when the size of the video file changes during playback. It is recommended to:<br><br><br>* Avoid playing online before transcoding is complete.<br><br>* After listening to this error, refresh the page or recreate the player to retry. |
|2190 |Protocol error. |This usually occurs when an HTTP playback address is used on an HTTPS page. Please go to the BytePlus VOD console to [configure an SSL certificate](https://docs.byteplus.com/en/docs/byteplus-vod/docs-configuring-ssl-certificates), then obtain an HTTPS playback address for playback. |
|2191 |Video address expired. |The video address has expired. You can choose one of the following solutions:<br><br><br>* Extend the video expiration time.<br><br>   * In Vid playback mode, please go to the BytePlus VOD console to [adjust the configuration for the video address's effective time](https://docs.byteplus.com/en/docs/byteplus-vod/docs-timestamp-).<br><br>   * In DirectUrl mode, if the video address is self\-signed, you need to adjust the `duration` parameter of the generated video address.<br><br>* Implement [automatic refresh of expired playback sources](https://docs.byteplus.com/en/docs/byteplus-vod/docs-implementing-basic-features-web#automatically-refreshing-playback-assets-after-expiration). |
|2192 |Video address signature error. |The video address signature is incorrect. Please check if the address is correct. |
|2193 |Failed to request M3U8 when playing encrypted HLS video. |First [Configure cross-domain access](https://docs.byteplus.com/docs/byteplus-vod/common-playback-configurations#8793e0fe) for the domain, then check as follows:<br><br><br>1. Check if the video address has expired or if the video address is correct.<br><br>2. Check if the `keyToken` is correct.<br><br>3. Check if the key acquisition interface has failed. |
|3100 |FLV unsealing and transcoding errors. |The video format is abnormal. Check if the current resource is valid or try to transcode again. |
|3200 |TS unsealing and transcoding errors. |The video format is abnormal. Check if the current resource is valid or try to transcode again. |
|3300 |MP4 unsealing and transcoding errors. |The video format is abnormal. Check if the current resource is valid or try to transcode again. |
|3400 |DASH unsealing and transcoding errors. |The video format is abnormal. Check if the current resource is valid or try to transcode again. |
|3410 |SIDX box parsing failure |The SIDX information is incorrect. You need to transcode again. |
|4100 |fMP4 packaging error. |The video format is abnormal. Check if the current resource is valid or try to transcode again. |
|4200 |MP4 packaging error. |N/A |
|5101 |The retrieval of related resources has been terminated due to user request. |Canceled by user. No need to handle. |
|5102 |A network error occurred, which prevented media retrieval or means the current video format is not playable. |Retry and check the user's network status. |
|5103 |A decoding error occurred during playback. The current video decoding failed. |Check if the Web SDK supports the codec and container format of the current video. |
|5104 |The video resource is not available. This may be because the request to retrieve the video resource returned a 4xx error, or the video itself cannot be decoded. |The current playback address is invalid or the format is not supported. Check if the video format and playback address are valid. It is recommended to [Configure cross-domain access](https://docs.byteplus.com/docs/byteplus-vod/common-playback-configurations#8793e0fe) for the domain of the video address to facilitate further analysis of the actual error caused by the SDK. |
|5105 |The current browser does not support video decoding. This error is common for web crawlers. |Switch to another browser. |
|5106 |The current playback address is empty |Check if the playback address is correct during initialization. |
|5200 |MSE addSourceBuffer error |The current browser does not support the codec setting of the current video. Check the resource encoding type and user browser support. |
|5201 |MSE appendBuffer error |The video is in an error state or the mediasource has been unbound from the video. |
|5202 |Other MSE errors |N/A |
|5203 |MSE FULL |Buffer addition exceeds the buffer limit allowed for a single video instance. |
|5204 |MSE API hijacked |N/A |
|5301 |EME API hijacked |N/A |
|5901 |The video file is not supported by the current browser |Please check if the video file format is correct. |
|5902 |Video playback error |This error is usually caused by the following reasons:<br><br><br>* The video file is incompatible, some video data is lost, resulting in decoding and playback errors.<br><br>* The playback browser is incompatible with the video file.<br><br><br>For both cases, it is recommended to transcode the video before playback. |
|7100 |DRM license authentication failure |Check if the DRM key is correct. |
|7101 |DRM is not supported. |Avoid playing DRM\-encrypted videos on browsers that do not fully support commercial DRM. Guide users to play on Chrome or other browsers. |
|7102 |Screen recording protection not supported |This is usually due to an insufficient security level of the device browser. Guide users to watch on the app or disable screen recording detection. |
|7103 |Video data lacks associated MediaKey |Check if the video transcoding is correct. |
|7104 |The current browser does not support the related DRM KeySession |Check if the video transcoding is correct. |
|7105 |Key request failed when playing DRM encrypted video |Check if `getVideoByToken.thirdPartyDrmAuthToken` is correct. |
|7106 |Missing certificate link when playing DRM encrypted video |Check if the player has configured the FairPlay certificate link address, corresponding to the `getVideoByToken.serverCertificatePath` parameter. |
|7107 |Missing certificate request configuration when playing DRM encrypted video |Check if the player has configured `getVideoByToken.thirdPartyDrmAuthToken`. |
|7108 |Certificate update error when playing DRM encrypted video |Check if `getVideoByToken.thirdPartyDrmAuthToken` is configured correctly and confirm if it has expired. |
|7109 |Decryption error when playing DRM encrypted video |Video data is abnormal. Check if the current resource is valid or try to transcode again. |
|7110 |Certificate request failed when playing DRM encrypted video |Check if the FairPlay certificate link address configured by the player (corresponding to the `getVideoByToken.serverCertificatePath` parameter) can obtain certificates normally. |
|7200 |Private encryption interface error |License key parsing error. Check if the interface or key is correct. |
|8000 |Unknown error |Unknown error. |
|8100 |Parameter error |Check if the parameters are valid. |
|8200 |Other errors |N/A |
|9001 |Long time without playback |Re\-initialize the player. |
|9002 |Playback stuttering and cannot be recovered for a long time |Re\-initialize the player. |
|9003 |Playback is stuck and `document.hidden` is `true` |Re\-initialize the player. |
|9201 |Audio and video tracks have unequal lengths, resulting in resource issues, audio and video packaging anomalies |Re\-transcode. |
|9202 |Unable to obtain init data during initialization |Re\-initialize the player. |
|10001 |`playAuthToken` expired |Please handle it in one of the following ways:<br><br><br>* In playlist scenarios, it is recommended to obtain `playAuthToken` before starting playback to avoid obtaining too many playAuthTokens at once.<br><br>* After updating `playAuthToken`, recreate the player for playback.<br><br>* When the server issues `playAuthToken`, set a longer token expiration time. |
|10002 |`keyToken` expired when playing encrypted HLS video |Please handle it in one of the following ways:<br><br><br>* In playlist scenarios, it is recommended to obtain `keyToken` before starting playback to avoid obtaining too many keyTokens at once.<br><br>* After updating `keyToken`, recreate the player for playback.<br><br>* When the server issues `keyToken`, set a longer expiration time for the token. |
|10003 |ThirdPartyDrmAuthToken expired when playing commercial DRM encrypted video |Please handle it in one of the following ways:<br><br><br>* In playlist scenarios, it is recommended to obtain `thirdPartyDrmAuthToken` before starting playback to avoid obtaining too many thirdPartyDrmAuthTokens at once.<br><br>* After updating `thirdPartyDrmAuthToken`, recreate the player for playback.<br><br>* When the server issues `thirdPartyDrmAuthToken`, set a longer expiration time for the token. |
|11001 |Failed to retrieve video information |Check in the following ways:<br><br><br>* Check if the parameters set when the server issues `playAuthToken` are correct, such as whether the corresponding vid has permissions.<br><br>* Check if the interface request for the domain `https://vod.byteplusapi.com/` is successful. Check the returned errors for this type of interface:<br><br>   * If it is a sporadic network error, you can rebuild the player and retry.<br><br>   * If there is another error, contact technical support for assistance in troubleshooting. |
|11002 |Failed to retrieve HLS key |Check in the following ways:<br><br><br>* Check if the parameters set when the server issues `keyToken` are correct, such as whether the corresponding vid has permissions.<br><br>* Check if the interface request for the domain `https://vod.byteplusapi.com/` is successful. Check the returned errors for this type of interface:<br><br>   * If it is a sporadic network error, you can rebuild the player and retry.<br><br>   * If there is another error, contact technical support for assistance in troubleshooting. |
|12001 |Invalid license verification |Check whether the [license is configured correctly](https://docs.byteplus.com/docs/byteplus-vod/docs-getting-started-with-the-web-player-sdk#5c74adef). |
|12002 |The license wildcard domain does not match |A license can authorize only one wildcard domain. Check whether the wildcard domain configured when applying for the license in the BytePlus VOD console matches the domain of the page where the player is located. |


<span id="b80fae18"></span>
### errorCode

Error codes for Web Player SDK versions prior to 1.10.0 are shown in the table below.


|**Error code** |**Description** |**Troubleshooting tip** |
|---|---|---|
|\-499995 |The current browser does not support this codec. |Provide guidance for users to switch to another browser. |
|\-499994 |The video resource is not available. This could be because the request to retrieve the video resource returned a 4xx error, or the video itself cannot be decoded. |Check whether the video address is valid or whether the browser supports decoding the video. |
|\-499993 |An error occurred while trying to decode the video resource. |Check whether the Web SDK supports the codec and container format of the current video. |
|\-499992 |A network error prevented video resource retrieval. |Check the network condition of the user. |
|\-499991 |Video resource retrieval has been aborted due to user intervention. |Simply cancel the user intervention, and no further processing is required. |
|\-499988 |The video address is empty. |Investigate why the video address returned by the server is empty. |
|\-499986 |Unexpected playback error. |The playback is experiencing buffering issues, resulting in a downgrade of quality. |
|\-499985 |Failed to play H.265 due to unknown unexpected reasons. |Check whether the current environment supports decoding H.265 videos. If a timeout occurs when playback starts, check whether the video resource retrieval request timed out or failed. |
|\-499984 |Failed to resolve mdhd when playing an MP4 file. |Check whether the container format of the current video file is supported. |
|\-499983 |Failed to resolve mdat when playing an MP4 file. |Check whether the container format of the current video file is supported. |
|\-499982 |The current playback parameters are for H.265, but the current video codec is H.264. |Check whether the playback parameters match the current video codec. |
|\-499981 |Failed to resolve the MP4 MOOV atom. |Check whether the container format of the current video file is supported. |
|\-499980 |Failed to resolve the MP4 box. |None |
|\-499975 |An error occurred when resolving the DASH sid. |Re\-transcode the video. |
|\-499974 |An error occurred when resolving the DASH key. |Check whether the SDK successfully obtained the key. |
|\-499973 |Failed to call `appendBuffer` when playing DASH, which resulted in the `initSegment` not being resolved successfully. |None |
|\-499972 |The total duration of audio and video streams is significantly different, resulting in an early end of playback. |Check the total duration of audio and video streams. |
|\-499971 |Failed to append the initial data using MSE. |None |
|\-499970 |An error occurred when resolving the MPD file. |Check whether the MPD file adheres to the specification. |
|\-499902 |Failed to add audio and video tracks using MSE. |Failed to add an audio track. This error may appear in higher versions of Safari. |
|\-499901 |Failed to request the DRM license. |Check whether the DRM\-related request returns 403. |
|\-499899 |The HTTP 416 error |None |
|\-499898 |The HTTP 401 error |None |
|\-499897 |The HTTP 403 error |Check whether the video address is still valid or whether CDN authentication has been passed. |
|\-499896 |The HTTP 404 error |Check whether the source video is offline. |
|\-499895 |Timeout in the HTTP request |Check whether the video address is valid. |
|\-499894 |Other HTTP 4xx errors |Check whether the video address is valid. |
|\-499893 |Other HTTP 5xx errors |Check whether the video address is valid. |
|\-499892 |An error occurred when sending the HTTP request. |Check whether the video address supports cross\-domain requests. |
|\-499891 |The length of the content returned by HTTP is inconsistent with the request. |Check whether CDN supports the HTTP range requests. |
|\-499791 |An error is automatically reported when a playback freeze times out. |None |
|1100 |An error occurred when resolving the HLS file. |Check whether the container format of the M3U8 file is valid. |
|1200 |An error occurred when resolving the MPD file. |None |
|2100 |A network error occurred. |Check whether the video address returns a 403 error, which indicates the video has expired or permission verification failed. |
|2101 |The network request timed out. |Check whether the video address is valid. |
|3100 |An error occurred when unpackaging the FLV file. |None |
|3200 |An error occurred when unpackaging the TS file. |None |
|3300 |An error occurred when unpackaging the MP4 file. |None |
|3400 |An error occurred when unpackaging the DASH file. |None |
|4100 |An error occurred when packaging the fMP4 file. |None |
|4200 |An error occurred when packaging the MP4 file. |None |
|5200 |An error occurred when calling the `addSourceBuffer` method of MSE. |None |
|5201 |An error occurred when calling the `appendBuffer` method of MSE. |None |
|5202 |An error occurred when calling other methods of MSE. |None |
|8100 |An error occurred due to wrong parameters. |Check whether the parameter is valid. |
|8200 |Other errors |None |
