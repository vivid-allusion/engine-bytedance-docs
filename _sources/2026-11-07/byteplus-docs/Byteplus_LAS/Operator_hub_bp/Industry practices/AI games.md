---
title: "AI games"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/AI_games"
---

The core competitiveness of AI games lies in reliably ensuring a stable multi\-user voice interaction experience, real\-time identification of violations and risky content, and continuous optimization of voice link quality. High\-quality, highly available audio data, high\-standard penalty results, and high\-quality training samples are accumulated to support model capability iteration and business rule upgrades. However, traditional audio governance and training processes rely heavily on manual sampling and rule configuration, resulting in limited quality inspection coverage, inconsistent penalty standards, and lengthy training data construction cycles. LAS multimodal operators focus on two main scenarios: audio quality inspection and penalty, and audio model training. They help AI game businesses achieve higher accuracy, greater efficiency, and stronger generalization in audio understanding and governance at lower cost.

<span id="500d3dca"></span>
# Application scenarios

<div style="text-align: center">
<h2 id="90cd4bb5">Audio quality inspection moderation</h2></div>


For AI gaming scenarios such as voice companionship, multi\-user voice chat, real\-time battles, and voice\-based social interactions, automatic recognition, quality inspection, review, and graded penalties are applied to in\-game audio content to address issues including abusive attacks, vulgar and pornographic content, advertising redirection, negative remarks, noise interference, and muting or AFK behavior. This enhances the efficiency of audio content governance and ensures the consistency of the community environment and player experience.

<div style="text-align: center">
<h2 id="59f40608">Audio model pre\-training</h2></div>


For tasks such as speech recognition, speaker diarization, emotion recognition, language identification, non\-compliant audio detection, and semantic understanding, massive volumes of game voice data are cleaned, segmented, annotated, classified, and subjected to sample augmentation to build high\-quality training datasets, improving model recognition performance and generalization in complex gaming contexts, multi\-character dialogues, and environments with strong noise.

<span id="bc8cb4f1"></span>
# Related operators

For the two sub\-scenarios of AI games, LAS provides corresponding multimodal operators:


* [Speech-to-Text (Doubao - Audio File Recognition) Enhanced Version](https://docs.byteplus.com/docs/Byteplus_LAS/las_asr_pro): Handles the speech transcription stage for audio quality inspection and penalty.

* Audio Format Conversion (online), Audio Segmentation: Handle the data preprocessing stage for audio model pre\-training.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1dc6e96280f94e33990a8e7e15b20031~tplv-goo7wpa0wc-image.image) </span>

<span id="95a3f56e"></span>
# Application practices

<span id="ca27d95b"></span>
## Audio quality inspection and penalty: Speech\-to\-text · Doubao Speech ASR

Based on the Doubao speech recognition large model, speech in input audio/video files can be transcribed into text output. Supports multiple audio/video formats, multiple languages, audio noise reduction, and large file processing. Suitable for content quality inspection and review, audio/video subtitle generation, speech search, and many other scenarios. Operator advantages include: full\-format access (supports raw/wav/mp3/ogg/mp4/mov/mkv/flac and other formats), worry\-free long audio (no file size limit), and multi\-language coverage (supports recognition of 99 languages).

<span id="41181227"></span>
### Application process flow


* **Upload game audio:**  Upload in\-game reported audio, live broadcast voice, group chat recordings, and other materials to the LAS operator marketplace or submit via API.

* **Speech\-to\-text:**  The operator automatically transcribes audio content into structured text, supporting automatic recognition of multiple languages and segmented processing of long audio files.

* **Text moderation:**  Transcribed text is input into a review model or rule engine to automatically identify and classify violations such as abusive language, vulgarity, and traffic diversion.

* **Result handling:**  Actions such as muting, point deduction, and account banning are executed based on the moderation results, forming a closed\-loop automated review process.


<span id="b6e85f5a"></span>
## Audio model pre\-training: Audio Format Conversion + Audio Segmentation

The Audio Format Conversion operator uniformly converts audio or video files to the specified audio format and outputs them to a designated storage path. It is primarily used for audio format normalization in data processing pipelines, extracting audio from video, and preparing training data. Batch concurrent processing and configurable audio encoding parameters are supported. The Audio Segmentation operator extracts audio from audio or video files and segments it into multiple clips according to specified rules. This is suitable for structured processing of long audio files, data segmentation, and training data construction. When used together, these operators convert raw audio and video materials into standardized audio clips required for model training.

<span id="77c4c71e"></span>
### Application workflow


* **Input raw audio and video:**  Upload original files such as in\-game recorded battle voice, NPC dialogue, and live broadcast audio to TOS storage.

* **Audio Format Conversion:**  Use the format conversion operator to uniformly convert files to target formats such as MP3/WAV. Audio tracks are automatically extracted from video files, ensuring consistent formats for downstream processing.

* **Audio Segmentation:**  Segment long audio files into valid dialogue clips based on specified duration or VAD rules, filtering out silent and invalid noise segments.

* **Output training samples:**  The segmented audio clips serve as high\-quality training data for AI NPC dialogue models, speech recognition models, or emotion recognition models.
