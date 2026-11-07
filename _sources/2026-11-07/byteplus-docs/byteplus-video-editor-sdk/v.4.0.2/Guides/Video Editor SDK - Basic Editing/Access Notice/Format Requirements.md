---
title: "Format Requirements"
product: "BytePlus Video Editor (Archive)"
product_code: "byteplus-video-editor-sdk"
source: "https://docs.byteplus.com/en/docs/byteplus-video-editor-sdk/docs-format-requirements-v.4.0.2"
---

<span id="Format limits"></span>
# Format limits

<span id="Input"></span>
# Input


1. You can import multiple pictures and videos.

2. You can import both pictures and videos at a time.

3. You can import videos with a resolution of up to 4K.

4. The H.264 and H.265 standards are supported.


<span id="Video formats"></span>
## Video formats

MP4, MOV

<span id="Picture formats"></span>
## Picture formats

JPG, PNG, JPEG, GIF

<span id="Video encoding"></span>
## Video encoding

H264, H265

<span id="Audio formats"></span>
## Audio formats

MP3 / AAC / WAV / FLAC/ m4a (iOS) / OGG (Android) / PCM (Android)

<span id="Output"></span>
# Output

<span id="Video formats"></span>
## Video formats

The MP4 and MOV (iOS only) formats are supported for video output. Different formats are supported for Android and iOS.

<span id="Video encoding"></span>
## Video encoding

Encoding standard: H.264 (default).

Encoding method: hard coding (default). The transition from hard coding to soft coding is not supported.

Resolution: The default resolution for Android is 576x1024 pixels. You can set a resolution based on your business needs. Resolutions that are not commonly used must be adjusted. The number of horizontal or vertical pixels must be an integral multiple of 16. The default resolution for iOS is 1280x720 pixels.

Frame rate: Supported frame rates are 25, 30, 50, and 60 frames per second. You can select a frame rate based on your business needs.

Keyframe: The default number of groups of pictures is 60, which indicates that there's one keyframe in every 60 frames. You can set this number based on your business needs.

<span id="Audio encoding"></span>
## Audio encoding

Transcoding format: the encoding standard Advanced Audio Coding (AAC).

Sampling frequency: 44,100 Hz (default and also the lowest allowed).

Encoding bit rate: 128x1024 bits per second (default).

Quantity of audio channels: 2 (default).
