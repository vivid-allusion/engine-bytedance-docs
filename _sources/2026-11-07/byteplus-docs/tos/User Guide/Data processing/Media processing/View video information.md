---
title: "View video information"
product: "Torch Object Storage"
product_code: "tos"
source: "https://docs.byteplus.com/en/docs/tos/docs-viewing-video-information"
---

The info feature allows you to retrieve the metadata of a specified video. This topic introduces the parameters and provides examples of the info feature.

<span id="1d5c5851"></span>
## Charging description


* Using the info feature incurs fees for metadata retrieval, requests, and data transfer. For billing details, see [Data processing Fee](https://docs.byteplus.com/en/docs/tos/docs-data-processing-fee), [Request Fee](https://docs.byteplus.com/docs/tos/docs-request-fee) and [Traffic Fee](https://docs.byteplus.com/docs/tos/docs-traffic-fee).

* Viewing video information from low\-frequency storage or archive flashback storage types will incur data retrieval charges, billed based on the size of content returned after viewing. For billing details, please see [Data Retrieval Fee](https://docs.byteplus.com/docs/tos/docs-data-retrieval-fee).


<span id="tZrAtUNM"></span>
## Precautions

For information on supported video formats, please refer to the [Video processing overview](https://docs.byteplus.com/en/docs/tos/docs-overview_7) for relevant usage limitations.

<span id=".5Y-C5pWw6K-05piO"></span>
## Parameter description

To retrieve specific video metadata using the request URL, simply add `x-tos-process=video/info` to the URL without setting any other request parameters.

The return parameter details are explained as follows:

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Differences may exist in the results returned for different video formats.</div>


```json
{ 
    "streams": [ 
        { 
            "index": 0,                 // stream index number
            "codec_name": "aac",        // encoder name 
            "codec_long_name": "AAC (Advanced Audio Coding)",    // Codec Detailed Name 
            "codec_type": "audio",      // Codec Type 
            "codec_tag_string": "mp4a", // Codec Tag Name 
            "codec_tag": "0x6134706d",  // Codec Tag 
            "sample_fmt": "fltp",       // Sample Format 
            "sample_rate": "44100",     // Sample Rate 
            "channels": 2,              // Number of Channels 
            "channel_layout": "stereo", // Channel Layout 
            "r_frame_rate": "0/0",      // Frame Rate 
            "avg_frame_rate": "0/0",    // Average Frame Rate 
            "time_base": "1/44100",     // Encoding time base 
            "start_time": "0.000000",   // Audio start time 
            "duration": "596.474195",   // Audio duration 
            "bit_rate": "125587",       // Bit rate 
            "nb_frames": "25688",       // Total frames 
            "tags": {                   // Tag information 
                "language": "und",      // Language 
                "handler_name": "(C) 2007 Google Inc. v08.13.2007." // Handler name 
            } 
        }, 
        { 
            "index": 1,                     // Stream index number 
            "codec_name": "h264",           // Encoder name 
            "codec_long_name": "H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10",    // Detailed encoder name 
            "profile": "High",              // Video encoding profile 
            "codec_type": "video",          // Encoder type 
            "codec_tag_string": "avc1",     // Codec tag name 
            "codec_tag": "0x31637661",      // Codec tag 
            "width": 1280,                  // Width in pixels 
            "height": 720,                  // Height in pixels 
            "sample_aspect_ratio": "1:1",   // sample aspect ratio 
            "display_aspect_ratio": "16:9", // display aspect ratio 
            "pix_fmt": "yuv420p",           // pixel format 
            "level": 31,                    // video encoding level 
            "r_frame_rate": "24/1",         // frame rate 
            "avg_frame_rate": "24/1",       // average frame rate 
            "rotation": "90",               // Rotate clockwise
            "time_base": "1/24000",         // encoding base time 
            "start_time": "0.000000",       // video start time 
            "duration": "596.458333",       // video duration 
            "bit_rate": "1991287",          // bit rate 
            "nb_frames": "14315"            // Total frames 
        } 
    ], 
    "format": { 
        "nb_streams": 2,  // Number of streams 
        "nb_programs": 0, // Number of programs 
        "format_name": "mov,mp4,m4a,3gp,3g2,mj2", // Container format name 
        "format_long_name": "QuickTime / MOV",    // Full name of container format 
        "start_time": "0.000000", // Start time of the first frame 
        "duration": "596.473333", // Duration 
        "size": "158008374",      // File size 
        "bit_rate": "2119234"     // Bitrate 
    } 
}
```


<span id="Example"></span>
## Example

Original video example: [https://tos-tools.tos-cn-beijing.volces.com/misc/video.mp4](https://tos-tools.tos-cn-beijing.volces.com/misc/video.mp4)

Example URL for obtaining video metadata is as follows:

[https://tos-tools.tos-cn-beijing.volces.com/misc/video.mp4?x-tos-process=video/info](https://tos-tools.tos-cn-beijing.volces.com/misc/video.mp4?x-tos-process=video/info)

Expect the following results:

```json
{ 
    "streams": [ 
        { 
            "index": 0, 
            "codec_name": "h264", 
            "codec_long_name": "H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10", 
            "profile": "High", 
            "codec_type": "video", 
            "codec_tag_string": "avc1", 
            "codec_tag": "0x31637661", 
            "width": 1920, 
            "height": 1080, 
            "coded_width": 1920, 
            "coded_height": 1088, 
            "sample_aspect_ratio":"1:1", 
            "display_aspect_ratio":"16:9", 
            "pix_fmt":"yuv420p", 
            "level":40, 
            "chroma_location":"left", 
            "refs":1,"is_avc":"true", 
            "nal_length_size":"4", 
            "r_frame_rate":"30/1", 
            "avg_frame_rate":"30/1", 
            "time_base":"1/1000000", 
            "start_pts":0, 
            "start_time":"0.000000", 
            "duration_ts":51200000, 
            "duration":"51.200000", 
            "bit_rate":"2597036", 
            "bits_per_raw_sample":"8", 
            "nb_frames":"1536", 
            "extradata_size":0, 
            "disposition": { 
                "default":1, 
                "dub":0, 
                "original":0, 
                "comment":0, 
                "lyrics":0, 
                "karaoke":0, 
                "forced":0, 
                "hearing_impaired":0, 
                "visual_impaired":0, 
                "clean_effects":0, 
                "attached_pic":0, 
                "timed_thumbnails":0, 
                "captions":0, 
                "descriptions":0, 
                "metadata":0, 
                "dependent":0, 
                "still_image":0 
            }, 
            "tags": { 
                "language": "und", 
                "handler_name": "VideoHandler", 
                "vendor_id": "" 
            } 
        }, 
        { 
            "index":1, 
            "codec_name":"aac", 
            "codec_long_name":"AAC (Advanced Audio Coding)", 
            "profile":"LC", 
            "codec_type":"audio", 
            "codec_tag_string":"mp4a", 
            "codec_tag":"0x6134706d", 
            "sample_fmt":"fltp", 
            "sample_rate":"44100", 
            "channels":2, 
            "channel_layout":"stereo", 
            "r_frame_rate":"0/0", 
            "avg_frame_rate":"0/0", 
            "time_base":"1/44100", 
            "start_pts":0, 
            "start_time":"0.000000", 
            "duration_ts":2257920, 
            "duration":"51.200000", 
            "bit_rate":"192755", 
            "nb_frames":"2206", 
            "extradata_size":0, 
            "disposition": { 
                "default":1, 
                "dub":0, 
                "original":0, 
                "comment":0, 
                "lyrics":0, 
                "karaoke":0, 
                "forced":0, 
                "hearing_impaired":0, 
                "visual_impaired":0, 
                "clean_effects":0, 
                "attached_pic":0, 
                "timed_thumbnails":0, 
                "captions":0, 
                "descriptions":0, 
                "metadata":0, 
                "dependent":0, 
                "still_image":0 
            }, 
            "tags": { 
                "language": "und", 
                "handler_name": "SoundHandler", 
                "vendor_id": "" 
            } 
        } 
    ], 
    "format": { 
        "nb_streams":2, 
        "nb_programs":0, 
        "format_name":"mov,mp4,m4a,3gp,3g2,mj2", 
        "format_long_name":"QuickTime / MOV", 
        "start_time":"0.000000", 
        "duration":"51.200000", 
        "size":"17899516", 
        "bit_rate":"2796799", 
        "probe_score":100, 
        "tags": { 
            "major_brand": "isom", 
            "minor_version": "512", 
            "compatible_brands": "isomiso2avc1mp41", 
            "encoder":"Lavf58.76.100" 
        } 
    } 
}
```
