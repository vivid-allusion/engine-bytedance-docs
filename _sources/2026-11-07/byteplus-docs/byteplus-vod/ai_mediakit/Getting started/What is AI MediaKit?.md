---
title: "What is AI MediaKit?"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/ai-mediakit-overview"
---

AI MediaKit from BytePlus is a suite of intelligent, API\-driven multimedia services. It deconstructs sophisticated media processing technologies into fine\-grained, developer\-friendly APIs. With AI MediaKit, you can easily integrate advanced media processing capabilities into your applications without handling the underlying engineering complexities, empowering your AI agents to perform video processing tasks with precision and efficiency.

## Product advantages

* **Agent\-friendly design**: The AI MediaKit tools are designed to be agent\-friendly, featuring a clear, semantically rich description and metadata that large models can easily understand. This design allows AI agents to accurately identify and utilize the tool's capabilities with minimal training, effectively reducing tool\-calling errors.

* **Cost\-effective processing**: By leveraging elastic cloud resource scheduling and optimized batch processing strategies, AI MediaKit offers highly competitive pricing for large\-volume media tasks, significantly reducing the overall operational costs of AI applications.

* **Comprehensive enhancement capabilities**: AI MediaKit provides a suite of powerful tools for video enhancement, privacy protection, and content analysis. It integrates over 30 high\-quality atomic algorithms—for tasks like super\-resolution, frame interpolation, face detection, and scene analysis—to handle diverse media processing needs across various scenarios.

## Core capabilities

AI MediaKit offers a range of powerful tools to handle various media processing tasks. The core capabilities currently available are summarized below.

### Video tools

|**Tool** |**Description** |**Related document** |
|---|---|---|
|Video Enhancement |Intelligently analyzes and enhances video quality using a library of over 30 AI algorithms. It offers **Standard** and **Professional** versions to balance quality and cost. |[Video enhancement](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-quality-enhancement) |
|Video Quality Enhancement (Fast) |Uses lightweight super\-resolution and quality enhancement to improve video quality with faster processing for latency\-sensitive workflows. |[Video quality enhancement (fast)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-quality-enhancement-lite) |
|Video Quality Enhancement (AI\-Enhanced) |Uses diffusion models to restore and enhance video, reconstructing realistic details lost through compression or aging. |[Video quality enhancement (AI-enhanced)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-quality-enhancement-ai-enhanced) |
|Precision Erasure |Automatically detects and removes hardcoded subtitles and on\-screen text from videos. |[Precision erasure](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-precision-erasure) |
|Face Blurring |Automatically detects and masks faces in videos with a mosaic or blur effect for privacy protection. |[Face blurring](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-face-mosaic) |
|Highlight Clipping |Identifies key moments in one or more videos and assembles highlight reels using scenario presets or criteria you describe in natural language. |[Highlight clipping](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-highlight-clipping) |
|Frame Extraction |Captures still images from a video by time interval, specified timestamps, first or last frame, or scene changes. |[Frame extraction](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-frame-extraction) |
|Scene Segmentation |Detects scene and shot changes to split a video into segments, returning segment timestamps and clip URLs. |[Scene segmentation](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-scene-segmentation) |
|Semantic Segmentation (Basic) |Analyzes visuals, speech, and narrative structure to split a video into semantically complete segments and return their timestamps. |[Semantic segmentation](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-semantic-segmentation) |
|Semantic Segmentation (Pro) |Combines shot boundaries, scene semantics, recognized text, and duration constraints to produce complete segments using industry or custom strategies. |[Semantic segmentation (pro)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-semantic-segmentation-pro) |
|Script Reconstruction |Converts live\-action short\-drama videos into structured script text for content analysis, repurposing, and retrieval. |[Script reconstruction](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-script-reconstruction) |
|Video Invisible Watermark |Embeds invisible numeric information in videos and extracts it for copyright protection, content leak tracing, and authenticity verification. |[Video invisible watermark](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-invisible-watermark) |
|Video Transcoding |Converts video encoding, resolution, bitrate, frame rate, and container format to meet playback and distribution requirements. |[Video transcoding](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-transcoding) |
|Low\-bitrate HD Transcoding |Optimizes encoding parameters to preserve perceived video quality at a lower bitrate, reducing storage and bandwidth costs. |[Low-bitrate HD transcoding](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-low-bitrate-hd-transcoding) |
|Remuxing |Changes the media container format without re\-encoding the audio or video streams, preserving their quality. |[Remuxing](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-remuxing) |
|Video Quality Assessment (VQScore) |Uses a no\-reference quality assessment algorithm to provide an objective video quality score that reflects human perception. |[Video quality assessment (VQScore)](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-quality-assessment) |
|Video Frame Interpolation |Synthesizes intermediate frames to increase the video frame rate and improve motion continuity. |[Video frame interpolation](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-frame-interpolation) |
|Video Matting |Separates a subject from the background using portrait or green screen matting to create video assets with transparent or solid\-color backgrounds. |[Video matting](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-matting) |
|Reframe to Vertical |Automatically detects and tracks subjects to crop landscape videos into a vertical format for social media distribution. |[Reframe video to vertical](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-reframe-video-to-vertical) |
|Video Metadata Acquisition |Retrieves video metadata such as resolution, bitrate, frame rate, and codec for asset management and processing decisions. |[Create a video metadata acquisition task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-a-video-metadata-probe-task) |

### Image tools

|**Tool** |**Description** |**Related document** |
|---|---|---|
|Image Quality Enhancement |Improves image resolution, clarity, and color through content\-aware enhancement. |[Image quality enhancement](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-quality-enhancement) |
|Image Quality Assessment |Assesses image quality across dimensions such as clarity, aesthetics, noise, texture, and tonal balance. |[Image quality assessment](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-vqscore) |
|Image Face Blurring |Detects faces in an image and applies a mosaic effect to protect privacy. |[Image face blurring](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-face-blurring) |
|Image Matting |Removes complex image backgrounds and outputs the foreground subject with a transparent background. |[Image matting](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-matting) |
|Image Inpainting |Erases common icons or specified text and repairs the affected regions to match the surrounding background. |[Image inpainting](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-inpainting) |
|Image Character Recognition |Extracts text from images and returns structured, editable text data. |[Image character recognition](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-character-recognition) |
|Intelligent Image Compression |Reduces image file size while repairing compression artifacts and enhancing edge and texture details. |[Intelligent image compression](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-intelligent-image-compression) |
|Image Invisible Watermark |Embeds invisible numeric information in an image and extracts it for copyright protection and content tracing. |[Image invisible watermark](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-invisible-watermark) |
|Image Metadata Acquisition |Retrieves image metadata, including format, dimensions, color space, and Exif information. |[Create an image metadata acquisition task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-image-metadata-probe-task) |
|Basic Image Editing |Provides synchronous image editing, including rounded corners, rotation, flipping, sharpening, Gaussian blur, pixelation, text and image watermarks, color adjustment, resizing, color inversion, cropping, and compression. |[Basic image editing](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-basic-image-editing) |

### Editing tools

|**Tool** |**Description** |**Related document** |
|---|---|---|
|Multi\-track Editing |Combines video, audio, image, text, and subtitle tracks on a structured timeline, with transitions, effects, filters, trimming, speed control, and volume adjustment. |[Multi-track editing](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-multi-track-editing) |
|Audio and Video Concatenation |Joins multiple video or audio clips into a single file in a specified order. |[Audio and video concatenation](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-audio-video-concatenation) |
|Audio and Video Trim |Extracts a specified time range from a video or audio file. |[Audio and video trim](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-audio-video-trim) |
|Audio and Video Speed Control |Changes video or audio playback speed to create faster or slower playback. |[Audio and video speed control](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-audio-video-speed-control) |
|Audio Extraction |Extracts the audio track from a video and saves it as a standalone audio file. |[Audio extraction](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-audio-extraction) |
|Audio and Video Merging |Adds an audio track to a video, either mixing it with or replacing the original audio. |[Audio and video merging](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-audio-video-merging) |
|Image to Video |Combines static images into a video. |[Image to video](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-image-to-video) |
|Audio Mixing |Mixes multiple audio files, such as vocals, background music, and sound effects, into a single audio file. |[Audio mixing](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-audio-mixing) |
|Volume Adjustment and Audio Fade In/Out |Adjusts a video audio track's volume and adds fade\-in or fade\-out effects to video audio tracks or standalone audio files. |[Volume adjustment and audio fade in-out](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-volume-adjustment-and-audio-fade-in-out) |
|Visual Transitions |Flips, rotates, or crops video frames, or arranges multiple videos horizontally or vertically in a single frame. |[Visual transitions](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-visual-transitions) |
|Subtitle Burn\-in |Renders subtitle files or text directly into video frames with a specified style. |[Subtitle burn-in](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-subtitle-burn-in) |
|Image Overlay on Video |Overlays a static image, such as a logo or watermark, at a specified position in a video. |[Image overlay on video](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-image-overlay) |
|Apply a Video Filter |Applies preset filters to change a video's visual atmosphere and style. |[Apply a video filter](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-apply-video-filter) |
|Apply Camera Motion |Adds dynamic camera effects, such as zoom and pan\-and\-zoom, to static or steadily shot footage. |[Apply camera motion](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-apply-camera-motion) |
|Video to Animated Image |Converts a specified video segment into an animated image in GIF or WebP format. |[Video to animated image](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-to-animated-image) |
|Video Gaussian Blur |Applies Gaussian blur to one or more specified rectangular regions in a video. |[Video gaussian blur](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-video-gaussian-blur) |
|Text\-to\-scrolling Video |Combines text with a background image and music to create a vertical scrolling\-text video. |[Text-to-scrolling video](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-text-to-scrolling-video) |

### Audio tools

|**Tool** |**Description** |**Related document** |
|---|---|---|
|Voice and Background Audio Separation |Separates audio or video into vocal and background tracks. For short\-drama, voice\-over, and game scenes, it can output separate vocal, music, and sound\-effects tracks. |[Voice and background audio separation](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-voice-and-background-audio-separation) |
|Voice Activity Detection |Detects the start and end times of speech segments in audio or video, distinguishing speech from silence and background noise. |[Voice activity detection](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-voice-activity-detection) |
|Audio Transcoding |Converts audio formats and adjusts encoding parameters such as sample rate, bitrate, and channel count. |[Audio transcoding](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-audio-transcoding) |
|Audio Metadata Acquisition |Retrieves audio metadata such as duration, bitrate, sample rate, and codec. |[Create an audio metadata acquisition task](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-create-an-audio-metadata-probe-task) |

### LLM\-based multimedia tools

|**Tool** |**Description** |**Related document** |
|---|---|---|
|Adaptive Video Understanding (AVU) |Analyzes a video and a natural\-language prompt, selecting frame extraction, audio analysis, and ModelArk models according to your quality and cost preferences to return structured understanding results. |[Adaptive video understanding](https://docs.byteplus.com/docs/byteplus-vod/ai-mediakit-adaptive-video-understanding) |
