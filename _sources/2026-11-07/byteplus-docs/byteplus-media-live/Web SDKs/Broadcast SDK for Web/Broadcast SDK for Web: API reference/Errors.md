---
title: "Errors"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-errors"
---

<span id="rtmerrorcode"></span>
## RTMErrorCode  

Type：`enum`

Error codes in the BytePlus MediaLive Broadcast SDK are used to identify issues during the process of audio and video capture and streaming. By using these error codes, problems can be quickly located and appropriate measures can be taken.


|Property |Value |Description |
|---|---|---|
|OPEN_CAMERA_FAILED |`1001` |Failed to open the camera. |
|OPEN_MICROPHONE_FAILED |`1002` |Failed to open the microphone. |
|OPEN_SCREEN_FAILED |`1003` |Failed to start screen sharing. |
|VIDEO_FILE_CAPTURE_FAILED |`1004` |Failed to load video file. This error occurs when the file path is incorrect or the format is not supported while attempting to load the video file as a stream. |
|AUDIO_FILE_CAPTURE_FAILED |`1005` |Failed to capture audio file. This error occurs when attempting to load an audio file as a stream if the file path is incorrect or the format is not supported. |
|IMAGE_FILE_CAPTURE_FAILED |`1006` |Failed to capture image file. This error occurs when the file path is incorrect or the format is not supported while trying to load the image file as a stream. |
|VOLUME_DETECT_FAILED |`1008` |Volume detection failed. This error is triggered when the audio stream is unavailable or the detection logic is abnormal. |
|PUBLISH_FAILED |`2001` |Failed to push stream. Applicable when the push stream address is unreachable, the network is unstable, or the server returns an error. |
|UPDATE_PUBLISH_FAILED |`2002` |Failed to update streaming content. This error occurs when replacing the video source fails in non\-mixing scenarios. |
|PUSH_CONNECT_FAILED |`2003` |Stream connection failed. This error will be returned if the network connection fails or the server address is unreachable. |
