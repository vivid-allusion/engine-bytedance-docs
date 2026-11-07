---
title: "Basic concepts"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-glossary"
---

A solid understanding of audio and video terminology is essential for effectively using BytePlus VOD. This document serves as a glossary, defining fundamental concepts like container formats, codecs, and transcoding, alongside product\-specific terms such as Spaces and Vid, to help you master the platform.

## **Container format**

Container format refers to the organization of audio, video, subtitles, and other data streams according to certain specifications to form a complete media file. Container formats typically include the following components:

* File header: Contains basic information about the entire media file.

* Data block: Contains specific audio and video data.

* Metadata: Contains information such as the data block codec and timestamp.

The supported codecs, container properties, and compatibility of different container formats vary.

The choice of container format will affect the quality, compatibility, and playback of media files during production, transmission, and playback. The following are common container formats:

* MP4: MP4 is one of the most common container formats and is supported by mainstream players and browsers. The MP4 format can be compressed using codecs such as H.264 and H.265, resulting in a smaller file size and higher video quality. This makes it a popular choice for VOD services. However, since the MP4 format is a static format that does not allow for adaptive bitrate adjustment based on network bandwidth and device performance, stuttering and buffering problems may occur in unstable network environments.

* HLS (HTTP Live Streaming): HLS is a video streaming protocol developed by Apple. It splits the entire video stream into small TS (Transport Stream) segments and transmits them using the HTTP protocol. HLS streams can be played on different devices and operating systems and support adaptive bitrate streaming, which can be adjusted according to the user's internet bandwidth and device performance to ensure an optimal video playback experience. HLS is commonly used for live streaming and VOD services. HLS converts the video file into multiple TS segments, which are then packaged into an M3U8 index file containing information about all the segments and their URLs on the server. This M3U8 file is used by client\-side applications to fetch and play video streams on demand.

* DASH (Dynamic Adaptive Streaming over HTTP): DASH is a video streaming protocol developed by MPEG (Moving Pictures Experts Group). Like HLS, DASH also uses the HTTP protocol for transmission. However, unlike HLS, DASH splits a video file into multiple MP4 segments, which are then packaged into a single MPD playlist file. This MPD file is used by client\-side applications to fetch and play video streams.

* FLV: FLV is a container format launched by Adobe, originally developed for Flash Player. FLV files are usually small and can support efficient codecs such as H.264 and AAC. However, with the deprecation of Flash Player, FLV format is no longer widely used.

The BytePlus VOD transcoding service supports a variety of container formats for adapting to different application scenarios and requirements. For more information, see [Overview](https://docs.byteplus.com/docs/byteplus-vod/docs-media-processing-overview).

## Codec

An audio\-video codec is a device or program that compresses and decompress digital audio or video data. Different audio and video codecs have distinctive advantages and disadvantages, and codec selection must be carefully considered according to the specific application scenario and requirements. Common audio codecs used in VOD services include MP3, AAC, FLAC, and WAV. Common video codecs include H.264, H.265, and VP9. H.264 is currently one of the most widely used video codecs, and H.265 is its upgraded version. H.265 is also known as HEVC (High Efficiency Video Coding), which provides a higher compression ratio and better video quality, making it suitable for the transmission and storage of high\-definition and ultra\-high\-definition video.

Some of the key differences between H.264 and H.265 are as follows:

* Compression efficiency: H.265 has a higher compression efficiency than H.264, so video files can be compressed to a smaller size, reducing bandwidth requirements for storage and transmission.

* Video quality: H.265 provides better video quality than H.264, especially at low bitrates. H.265 can provide clearer videos with reduced distortion and noise.

* Complexity: H.265 involves higher encoding and decoding complexity than H.264, so it requires higher computing power and more powerful hardware support.

* Compatibility: H.264 is widely used in a variety of devices and applications, while the compatibility of H.265 is still limited. Many low\-end devices and legacy software do not support H.265 decoding. The Player SDK supports playback of H.265 video sources and hardware decoding. Based on a blocklist of H.265 hardware decoding models compiled from big data, the Player SDK determines whether specific device models are suitable for hardware decoding and provides flexible downgrading strategies to effectively avoid compatibility issues such as playback failures, screen noise, or a black screen.

The BytePlus VOD transcoding service supports a variety of audio and video codecs, allowing it to adapt to different application scenarios and requirements. For details, see [Overview](https://docs.byteplus.com/docs/byteplus-vod/docs-media-processing-overview).

## Transcoding

Transcoding refers to the process of decoding and re\-encoding an audio or video stream that has been compressed and encoded. Transcoding typically involves the conversion of codecs (such as H.264, AAC), encoding parameters (for example, sample rate, bitrate, and iframe interval), and container formats (such as MP4, TS). The graphic below shows the transcoding process:

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/982634c103844cfeabeaeac3e5e212da~tplv-goo7wpa0wc-image.image)

Transcoding can help you achieve the following goals:

* Meet business needs, such as compatibility with Douyin, Xigua, and other long and short\-form video platforms, customized event watermarks, detection of and support for malformed or non\-standard video inputs.

* Optimize the user experience, such as using video enhancement, super resolution, frame interpolation, noise suppression, and other intelligent algorithms to improve audio and video quality.

* Cost savings, such as reducing device resource usage or bandwidth costs through transcoding.

## Transmuxing

Transmuxing is the process of unpacking and repacking audio and video data from one container format into another without changing the codec and content of the audio and video data.

The purpose of transmuxing is to adapt to different playback platforms and devices, and to optimize network transmission efficiency. It should be noted that transmuxing only changes the container format of the audio and video data and does not change the codec. Therefore, only limited computation and processing are required for transmuxing, and it does not have a significant impact on video quality and file size. This is in contrast to transcoding, which requires a high level of computation and processing, and can affect video quality and file size.

## Bitrate

Bitrate represents the number of bits transmitted or processed per unit of time. It is generally expressed as Mbps (megabits per second) or Kbps (kilobits per second). In the context of video, bitrate is a primary factor that determines the quality of the compressed video.

A higher bitrate can improve video quality, but it will also increase the size of the video file and the bandwidth requirements for network transmission.

## Resolution

Resolution refers to the size of each image frame in a video, expressed in pixels. For example, 720p means a video with a width of 1280 pixels and a height of 720 pixels. The higher the resolution, the clearer the image – but it also increases the size of the video file and the computing power required to decode it.

Resolution and bitrate are closely related. Higher resolutions require more data to be transmitted over a given period of time, so higher bitrates are needed to ensure video quality.

Mismatched resolution and bitrate can result in issues such as poor video quality or stuttering. For example, the current video resolution is 1080p and the bitrate is 2 Mbps. If the resolution is increased to 4K, the size of the video increases and a higher bitrate is required to ensure video quality. If you continue to use a bitrate of 2 Mbps, the video quality may decrease because the bitrate is insufficient to encode the additional detail required by the 4K resolution, which can result in compression artifacts.

## Frame rate

The frame rate represents the number of frames contained in the video per second, in fps (frames per second). A higher frame rate can improve the smoothness and motion fluidity of the video, but it will also increase the size of the video file and the amount of computing power required for decoding. In VOD applications, the video frame rate is typically set to 25 to 30 fps. This is because a frame rate of 25 to 30 fps is more than enough to provide a smooth viewing experience, as this is sufficient for the human eye to perceive fluid motion.

At the same time, a lower frame rate can reduce the size of video files and the bandwidth requirements for network transmission, making it suitable for transmission and playback in network environments with limited bandwidth. However, for some specific types of video, such as sports events and game videos, the frame rate of the video can be increased appropriately to ensure the smoothness of the video and a good viewing experience.

## Channel

Channel refers to the number of microphones used when recording audio and the number of speakers used when playing audio. The more channels there are, the more spatial and immersive the audio will be. There are two common channel settings:

* **Mono**: A single channel, typically used in applications such as broadcasting, recording, and telephones.

* **Stereo**: Two channels, usually used in audio entertainment such as music and movies. The left and right channels carry different audio information, and the spatial difference in the sound creates richer sound effects.

* **5.1 channel**: A common surround sound format that utilizes six channels to create an immersive audio experience. It consists of five full\-bandwidth channels (Front Left, Center, Front Right, Surround Left, Surround Right) and one Low\-Frequency Effects (LFE) channel. This setup allows for precise audio placement, with the center channel typically dedicated to dialogue, while the surround channels deliver ambient sounds and directional effects. The LFE channel (.1) is routed to a subwoofer to handle deep bass sounds, making it a standard for home theaters and cinematic content. To ensure a player can successfully play 5.1 channel video and output true surround sound, the entire processing and playback chain must meet specific conditions. A failure at any stage can result in the audio being downmixed to stereo or even mono.

   * **Transcoding limitations:**

      * **Source file dependency**: Transcoding can only convert or compress existing multi\-channel audio tracks. If the source track is mono or stereo, it cannot be upmixed to 5.1 channels.

      * **Format compatibility**: When transcoding advanced formats (like the TrueHD core of Dolby Atmos) to a lossy format (like AC\-3), crucial metadata and top\-channel information will be lost. The audio will be downgraded to its standard 5.1 or 7.1 core.

      * **Risk of incorrect channel mapping**: If the source file has a non\-standard channel layout or incorrect labeling, the transcoding process may result in incorrect channel mapping (such as center channel dialogue being output from surround speakers).

      * **Audio quality loss**: Transcoding from a lossless format (such as TrueHD, DTS\-HD MA) to a lossy format (such as AC\-3, AAC), or using an excessively low bitrate, will result in an irreversible loss of audio quality.

   * **Playback limitations**

      * **Hardware dependency**:

         * **Passthrough mode**: This feature is dependent on hardware support from the computer's sound card (or motherboard's HDMI port). Older or lower\-end hardware may not support it.

         * **Multi\-channel PCM output**: Requires the operating system to correctly identify the audio device as a multi\-channel device and relies on an HDMI connection.

         * **S/PDIF (Optical) interface**: Due to bandwidth limitations, this interface can only pass through legacy AC\-3 and DTS signals. It cannot transmit lossless formats (TrueHD, DTS\-HD MA) or multi\-channel PCM.

      * **Dependency on system settings**: The player's ability to output 5.1 sound is heavily influenced by the operating system's audio settings. The output device *must* be manually configured to "5.1 Surround" in the audio settings of Windows or macOS. The player cannot bypass this limitation if the system is set to "Stereo".

      * **DRM protection on source content: Content from some commercial streaming platforms is protected by DRM. Even if the content is 5.1, DRM may block the passthrough feature, forcing the player to decode the audio to PCM before output. This can affect the integrity and maximum quality of the audio format.**

      * **Cabling requirements**: High\-quality HDMI cables are mandatory. Subpar cables may fail to reliably transmit the high\-bandwidth signal required for lossless audio.

## Sampling rate

The sampling rate is the frequency at which sound is sampled when recording audio, given in Hz (hertz). In digital audio, analog audio signals need to be sampled, quantized, and encoded before they can be stored and transmitted. The higher the sampling rate, the more accurately the original analog audio signal can be restored, but this also increases the file size and required transmission bandwidth. Common sampling rates include: 44.1 kHz, 48 kHz, 96 kHz, and 192 kHz. 44.1 kHz and 48 kHz are the standard sampling rates for CDs and DVDs, while 96 kHz and 192 kHz are commonly used in high\-fidelity audio and professional audio production.

## HDR

Unlike Standard Dynamic Range (SDR) images, which have a limited brightness range, HDR images offer a wider range of brightness and color, more accurately reproducing the details in a real\-world scene.

However, HDR images offer a greater brightness range and more color information, which can more accurately reproduce the brightness, darkness, and color information of the real scene.

The BytePlus VOD transcoding service supports the conversion of SDR videos to HDR videos using intelligent algorithms to improve the contrast and color richness of the video and achieve better visual effects. For details, see [Video enhancement](https://docs.byteplus.com/docs/byteplus-vod/docs-video-enhancement).

## UHD

Ultra High Definition (UHD) refers to video with a resolution of 3840×2160 (4K) or higher and is compatible with the UHD standard issued by the International Telecommunication Union.

This resolution is several times higher than that of traditional high\-definition video formats, which means that UHD videos can provide more pixels and produce more detailed and realistic images, allowing viewers to experience the details and colors in the image more clearly and realistically. The increase in resolution is accompanied by an increase in bandwidth and processing power requirements. UHD video requires high\-performance processors, graphics cards, storage devices, and monitors and televisions that support UHD video formats.

## Super resolution

Super resolution is an image processing technique used to convert low\-resolution images into high\-resolution images. Super resolution techniques are usually divided into two types:

* Interpolation\-based super resolution: This method enhances the resolution of low\-resolution images using interpolation methods, such as bilinear or bicubic interpolation. Although this method is simple, it is prone to problems such as pixelation and distortion, and cannot guarantee the quality and authenticity of the resulting image.

* Reconstruction\-based super resolution: This method generates high\-resolution images by learning a model that can reconstruct or infer missing details in low\-resolution images. This method usually requires the use of more complex algorithms and models, which can more accurately restore the details and information of the original image, while also ensuring the quality and authenticity of the image.

The BytePlus VOD transcoding service supports AI super resolution. Based on deep learning methods, missing details are reconstructed by modeling the video information in the spatial and temporal domains in order to reconstruct a low\-resolution video into a high\-resolution video. For details, see [Video enhancement](https://docs.byteplus.com/docs/byteplus-vod/docs-video-enhancement).

## Spaces

Spaces are the basic unit used for VOD resource isolation. Spaces allow for granular management of your media assets. You can configure separate templates, workflows, and business policies for different spaces.

## Vid

Vid is the abbreviation of video ID, a unique identifier for each audio and video file in the BytePlus VOD service. You can use Vids to search for videos in the BytePlus VOD service or specify Vids when performing tasks such as video media processing. Note that video transcoding does not change a video's Vid.

## Media assets

In BytePlus VOD, media assets refer to content such as audio, video, images, and subtitles, as well as their associated metadata. Media assets can be divided into the following three categories:

* Audio and video assets: Audio and video files that can be used for media processing and playback after being uploaded to a VOD space.

* Image assets: Images identified by a unique picture ID (`Pid`). The original image and its processed files are managed together. For details, see [Image enhancement and processing](https://docs.byteplus.com/docs/byteplus-vod/docs-image-enhancement).

* Material assets: Audio, videos, animations, images, and other files uploaded to a VOD space as materials. Materials cannot be processed as media assets, are not playable, and can only be used for video covers, watermarks, or editing.

## BucketName

BucketName is the name of the storage bucket. The underlying storage layer for a VOD space is an object storage service. BucketName is the name of a storage bucket in the object storage service.

## FileName

FileName refers to the full path of a file within a bucket, which serves as its unique identifier.

If a file called `123.mp4` is saved as `BucketName/Project/VideoFiles/123.mp4`, the file path is `Project/VideoFiles/123.mp4`. For the specific character rules for the FileName, see [Character rules for file naming](https://docs.byteplus.com/docs/byteplus-vod/docs-character-rules-for-file-naming).

## FilePrefix

FilePrefix is the full path before the media asset file name, excluding the bucket name. For example, if file `123.mp4` is saved as `{BucketName}/Project/VideoFiles/123.mp4`, the file prefix is `/Project/VideoFiles/`. If you save `123.mp4` in a bucket with an unspecified path, the file prefix is `/`.

## FileTitle

FileTitle is the file name, which is used to refer to different media asset files. For example, the FileTitle of `123.mp4` is `123`.

## FileExtension

FileExtension is a mechanism used by BytePlus VOD to indicate the file format.

For example, for file `123.mp4`, the FileExtension is `mp4`, indicating that the file is an MP4 video file. A full stop `.` is used to separate the file name and the file extension.

## PGC

Professionally Generated Content (PGC) is created by experts with specialist knowledge and qualifications in content\-related fields who have recognized expertise or credibility in a specific field.

## UGC

UGC (User Generated Content) refers to content created by users, also known as user\-originated content.

## CNAME

Canonical Name (CNAME) is an alias record that maps one domain name to another. Using CNAMEs makes it easy to change IP addresses by pointing multiple hostnames to a single alias.
