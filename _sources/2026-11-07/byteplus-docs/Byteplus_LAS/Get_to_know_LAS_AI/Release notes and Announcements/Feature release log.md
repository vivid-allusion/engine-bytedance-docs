---
title: "Feature release log"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/las_release_notes"
---

# November 5, 2026

Release version: LAS AI 1.6.4.

|Feature module |Feature description |
|---|---|
|LAS operator |Operator optimization:<br><br><br>* [Intelligent Short Drama & Film Narration](https://docs.byteplus.com/docs/Byteplus_LAS/intelligent-short-drama-and-film-narration): Added Material Library voice and BGM selection by asset ID, labels, or inferred preferences. The selected voice and BGM are fixed for the task, with explicit validation and failure reporting when an asset or revision is unavailable.<br><br>* [Voice Cloning Synthesis](https://docs.byteplus.com/docs/Byteplus_LAS/voice-cloning-synthesis): Added Material Library voice selection. You can select a voice by material ID and optional revision, filter voices by labels, or let the operator infer voice preferences from the synthesis text and style description.<br><br>* [PDF Document Parsing (Doubao)](https://docs.byteplus.com/docs/Byteplus_LAS/pdf-document-parsing-doubao-22cb891fa6299267): Added password\-protected PDF parsing for standard RC4, AES\-128, and AES\-256 encryption, and added optional text recognition for image regions. Poll results now distinguish missing, invalid, and unsupported PDF\-password errors and clarify the parsed\-page count for long\-page splitting.<br><br>* [Video Translation](https://docs.byteplus.com/docs/Byteplus_LAS/Video_Translation_operator): Added the `high_quality` dubbing mode for richer emotional expression, closer voice\-timbre reproduction, and more accurate pronunciation. You can enable `enable_fast_mode` with this mode to reduce processing time.<br><br>* [Video scene segmentation](https://docs.byteplus.com/docs/Byteplus_LAS/Video_scene_segmentation): Updated uniform splitting to merge a short tail into the preceding segment, so only the final segment may exceed the configured maximum.<br><br>* [Video Inpaint](https://docs.byteplus.com/docs/Byteplus_LAS/Video_Inpaint-Pro): Added `subtitle_protect` to exclude regular and scrolling subtitle regions from watermark masks in supported detection modes. |

# October 30, 2026

Release version: LAS AI 1.6.3.

|Feature module |Feature description |
|LAS operator<br><br>^^ |New operators:<br><br><br>* [Fast Video Remix](https://docs.byteplus.com/docs/Byteplus_LAS/fast-video-remix): Combines up to 30 source videos into multiple short\-video variants through manual, automatic, or random act planning. It supports silent output, TTS or existing narration, regular subtitles, configurable delivery specifications, and editing\-plan artifacts.<br><br>* [Video Packaging](https://docs.byteplus.com/docs/Byteplus_LAS/video-packaging): Adds subtitles, decorative captions, keyword highlights, information cards, sound effects, BGM, and transitions to edited portrait videos. It supports external SRT or ASR subtitles, configurable asset pools and styles, 1–2× playback speed, and complete, clean, SRT, and packaging\-plan outputs.<br><br>   Operator optimization:<br><br>* [Sensitive Content Masking](https://docs.byteplus.com/docs/Byteplus_LAS/sensitive-content-masking): Added time\-segment processing for videos. Each segment can specify preset sensitive\-content categories or custom text and independently control whether matching speech is muted. Poll results now return per\-segment processing receipts, and billing is based on the actual processed duration.<br><br>* [Intelligent Video Remix](https://docs.byteplus.com/docs/Byteplus_LAS/Intelligent-Video-Remix): Added supplementary image input and system\-planned image layouts or stickers, independent gain controls for BGM, TTS, and original speech, and `repackage` mode for rendering from a previously generated editing scheme. Submit and Poll results now expose more complete editing\-plan, artifact, and usage information.<br><br>* [Video scene segmentation](https://docs.byteplus.com/docs/Byteplus_LAS/Video_scene_segmentation): Added multi\-video episode results and the standard storyboard bundle output structure for correlating scenes, shots, characters, props, and source videos. Equal\-duration segmentation now preserves the final remainder segment even when it is shorter than the configured minimum, and public character results have been streamlined to documented fields.<br><br>* [Video Translation](https://docs.byteplus.com/docs/Byteplus_LAS/Video_Translation_operator): Added dynamic\-duration translation, a separate picture source for subtitle burn\-in, and optional video restoration for removing existing subtitles or watermarks. The minimum input duration is now 2 seconds, and Poll results can return the repaired source video and restoration task information.<br><br>* [Image Pro Image Generation](https://docs.byteplus.com/docs/Byteplus_LAS/image-pro-image-generation): Standardized the operator model ID as `las_image_pro` and added image editing and masked editing. You can edit one or more source images and optionally provide masks for local changes. Generation and editing responses now return Base64\-encoded image data.<br><br>* [Video-to-Prompt Generation](https://docs.byteplus.com/docs/Byteplus_LAS/video-to-prompt-generation): Expanded accepted source\-video, storyboard, and reference\-image inputs, including valid presigned URLs, and removed the previous 4–30 second source\-video and nine\-reference\-image limits. Poll results now clarify duplicate reference renaming, fallback behavior, task statuses, and errors.<br><br>* [Video Prompt Generation](https://docs.byteplus.com/docs/Byteplus_LAS/video-prompt-generation): Added an explicit prompt revision template that accepts an original prompt, revision requirements, and target aspect ratio or resolution. Reference\-image metadata and Poll reference results have also been expanded, with clearer task status and error handling. |
|---|---|

# October 22, 2026

Release version: LAS AI 1.6.2.

|Feature module |Feature description |
|---|---|
|LAS operator |Operator optimization:<br><br><br>* [Video Inpaint](https://docs.byteplus.com/docs/Byteplus_LAS/Video_Inpaint-Pro): Added `fixed_bboxes_intervals` for configuring the active time range of each fixed inpainting region.<br><br>* [Intelligent Short Drama & Film Narration](https://docs.byteplus.com/docs/Byteplus_LAS/intelligent-short-drama-and-film-narration): Added support for TV series input. A task can accept up to 160 videos, with a combined duration of up to 300 minutes and a combined size of up to 20 GiB. When no output TOS path is specified, results are returned through presigned download URLs valid for 3 days.<br><br>* [Embodied Semantic Annotation](https://docs.byteplus.com/docs/Byteplus_LAS/embodied-semantic-annotation): Increased the Poll API quota to 1,200 RPM and updated the supported Seed model versions, including Seed 2.0 Mini, Lite, and Pro, and Seed 2.1 Turbo.<br><br>* [Fine-grained Video Understanding](https://docs.byteplus.com/docs/Byteplus_LAS/Fine-grained_video_understanding): Changed the default model to `seed-2-0-lite-260428` and updated the supported Seed model versions.<br><br>* [Multimodal Deep Thinking (Doubao-Seed-2.0)](https://docs.byteplus.com/docs/Byteplus_LAS/Multimodal-Deep-Thinking-Doubao-Seed-2-0): Updated supported model versions to include Seed 2.0 Mini, Lite, and Pro variants.<br><br>* [Video Script Planner](https://docs.byteplus.com/docs/Byteplus_LAS/video-script-planner): Made `output_tos_path` optional. When no output path is specified, Poll returns download URLs for generated artifacts that remain valid for 24 hours. |
|Workflow |Added the centralized [Workflow instance](https://docs.byteplus.com/docs/Byteplus_LAS/workflow#view-workflow-instances) page. You can query workflow run records, filter instances by workflow, runner, run time, status, or trigger type, view status and runtime information, and retry supported instances. |

# October 16, 2026

Release version: LAS AI 1.6.1.

|Feature module |Feature description |
|---|---|
|LAS operator |New operators:<br><br><br>* [Video Storyboard Gen](https://docs.byteplus.com/docs/Byteplus_LAS/video-storyboard-gen): Jointly understands reference videos, target product images, and ecommerce requirements, then generates multiple product voiceover and storyboard candidates as standard storyboard bundles for downstream video production.<br><br>* [Vocal Separation](https://docs.byteplus.com/docs/Byteplus_LAS/vocal-separation-d93f41dcef5cac84): Separates the first audio stream of an audio or video file into vocal and non\-vocal residual tracks. It supports WAV, MP3, and AAC audio output; video input can additionally produce an MP4 that retains the original picture with vocals\-only audio.<br><br>* [Image-Text Embedding (Skylark Models)](https://docs.byteplus.com/docs/Byteplus_LAS/image-text-embedding-skylark-models-67f8e3f58049150a): Generates unified embeddings for images, videos, and text with Skylark embedding models, supporting dense vectors and optional sparse embeddings for pure\-text input.<br><br>* [PDF Document Parsing (Doubao)](https://docs.byteplus.com/docs/Byteplus_LAS/pdf-document-parsing-doubao-22cb891fa6299267): Parses PDF, Word (DOC and DOCX), and image files into high\-fidelity Markdown and structured page results, supporting normal and detail modes, intelligent long\-page segmentation, and optional TOS artifact output.<br><br>* [Short Drama Script Revision](https://docs.byteplus.com/docs/Byteplus_LAS/Short_drama_script_revision): Applies controlled local revisions to short drama generation results, synchronizing changes across global character, scene, and prop tables, episode scripts, and optional structured episode files without regenerating the full series. |
||Operator optimization:<br><br><br>* [Face Blur](https://docs.byteplus.com/docs/Byteplus_LAS/Face_Blur): Added flexible output selection through `outputs`. You can return a blurred video, a per\-frame face bounding\-box JSON file, or both outputs together. Poll results now include dedicated paths and presigned URLs for the bbox JSON output. |

# October 12, 2026

Release version: LAS AI 1.6.0.

|Feature module |Feature description |
|---|---|
|LAS operator |New operators:<br><br><br>* [Image Pro Image Generation](https://docs.byteplus.com/docs/Byteplus_LAS/image-pro-image-generation): Generates high\-quality images from natural\-language prompts and supports URL or Base64 JSON output.<br><br>* [Seedream Image Generation](https://docs.byteplus.com/docs/Byteplus_LAS/seedream-image-generation): Generates images from text or reference images with Seedream 4.5 and 5.0, supporting single\-image generation, sequential generation, and SSE streaming output.<br><br>* [HyperFrames Video Generation](https://docs.byteplus.com/docs/Byteplus_LAS/hyperframes-video-generation): Generates videos from natural\-language requests and image, audio, or video references, with configurable duration, frame rate, aspect ratio, resolution, narration, background music, and output storage.<br><br>* [Video Script Planner](https://docs.byteplus.com/docs/Byteplus_LAS/video-script-planner): Converts video topics and creative requirements into structured production plans, including content structure, storyboards, asset states, character voices, and pacing.<br><br>* [Text to Speech (Doubao Speech 2.0)](https://docs.byteplus.com/docs/Byteplus_LAS/text-to-speech-doubao-speech-2-0): Provides synchronous streaming speech synthesis through the Process API and returns audio, subtitle, and completion events over SSE.<br><br>* [Audio Rebuild](https://docs.byteplus.com/docs/Byteplus_LAS/audio-rebuild): Merges generated video clips and rebuilds their audio tracks, or generates audio directly from an authoritative script, with standalone audio and subtitle outputs.<br><br>* [Voice Cloning Synthesis](https://docs.byteplus.com/docs/Byteplus_LAS/voice-cloning-synthesis): Supports voice design, voice cloning from reference audio, high\-fidelity continuation, and short\- or long\-form speech synthesis in multiple audio formats.<br><br>* [Sensitive Content Masking](https://docs.byteplus.com/docs/Byteplus_LAS/sensitive-content-masking): Detects and masks sensitive visual or textual content in images and videos, optionally mutes sensitive speech, and returns processed media and structured detection results.<br><br>* [Video Subtitle Translation](https://docs.byteplus.com/docs/Byteplus_LAS/Video_Subtitle_Translation): Extracts subtitles through OCR or ASR, translates them into multiple languages, and outputs TXT, SRT, XML, or VTT subtitle files.<br><br>* [Embodied Semantic Annotation](https://docs.byteplus.com/docs/Byteplus_LAS/embodied-semantic-annotation): Supports interactive\-object identification, temporal action annotation, and candidate\-guided task annotation for robot, UMI, and human\-demonstration videos.<br><br>* [Video Prompt Generation](https://docs.byteplus.com/docs/Byteplus_LAS/video-prompt-generation): Added configurable model tiers or exact model selection, editable requirements templates, reference\-image input, and examples for generating or refining video prompts.<br><br>* [Video-to-Prompt Generation](https://docs.byteplus.com/docs/Byteplus_LAS/video-to-prompt-generation): Added storyboard asset packages, prompt templates, configurable model selection, visual and voice style controls, and clearer storyboard duration and input constraints. |

# September 24, 2026

Release version: LAS AI 1.5.4.

|Feature module |Feature description |
|---|---|
|LAS operator |New operator:<br><br><br>* [Intelligent Short Drama & Film Narration](https://docs.byteplus.com/docs/Byteplus_LAS/intelligent-short-drama-and-film-narration): Added the Intelligent Short Drama & Film Narration operator, which processes multi\-episode short dramas or a single film, understands storylines and discovers highlight clues, and generates a narrated highlight video. It supports Chinese and English narration, preset and custom writing styles, narration speed control, original\-audio segments and opening strategies, high\-quality preset voices or reference\-audio voice cloning, and configurable subtitle backgrounds and positions. |
||Operator optimization:<br><br><br>* [Viral Clip Generation](https://docs.byteplus.com/docs/Byteplus_LAS/Viral_content_editing): Added support for configuring a pool of up to 20 preroll videos through `preroll_urls`. One preroll is randomly selected and prepended to each output clip. Added `aspect_ratio` to normalize output clips to portrait `9:16`. Poll results now identify preroll and postroll segments in the clip timeline and return their source URLs. |

# September 18, 2026

Release version: LAS AI 1.5.3.

|Feature module |Feature description |
|---|---|
|LAS operator |New operators:<br><br><br>* [Storyboard Script Generation](https://docs.byteplus.com/docs/Byteplus_LAS/Storyboard_Script_Generation): Added Storyboard Script Generation operator, designed for script production and e\-commerce voice\-over video workflows, which converts input text into a standard `storyboard_bundle`. Currently provides two capabilities: generating storyboards from scripts combined with character, prop, and scene asset JSON, and generating storyboards directly from voice\-over scripts.<br><br>* [Intelligent Video Remix](https://docs.byteplus.com/docs/Byteplus_LAS/Intelligent-Video-Remix): Added intelligent montage operator, which, based on understanding of input materials, speech recognition, semantic retrieval, and large model orchestration capabilities, automatically matches, sorts, and edits voice\-over, B\-roll, or long live\-action footage according to script, structured storyboard, or natural language creative requirements to produce the final video. |
||Operator optimization:<br><br><br>* [Video Edit Enhanced 2.0](https://docs.byteplus.com/docs/Byteplus_LAS/Enhanced_video_editing_2): Added support for `replace/subject_replace` preset templates, which can be used to replace objects, props, partial backgrounds, complete backgrounds, or the overall content of people and environments in videos.<br><br>* [Video Translation](https://docs.byteplus.com/docs/Byteplus_LAS/Video_Translation_operator): Added support for setting dubbing mode during translation via the dubbing_mode request parameter, supporting both emotional cloning and timbre restoration modes. |

# September 11, 2026

Release version: LAS AI 1.5.2.

|Feature module |Feature description |
|---|---|
|LAS operator |New operators:<br><br><br>* [Video Edit Enhanced 2.0](https://docs.byteplus.com/docs/Byteplus_LAS/Enhanced_video_editing_2): The new Video Edit Enhanced 2.0 operator is now available, providing video editing templates tailored to business scenarios. While preserving the original video’s actions, shots, composition, and timeline, it enables direct generation, general keyframe editing, face swapping, complete character replacement, general subject replacement, or global style transfer, delivering higher\-quality video editing capabilities for targeted business scenarios.<br><br>* [Video Inpaint](https://docs.byteplus.com/docs/Byteplus_LAS/Video_Inpaint-Pro): Supports additional Video Inpaint capabilities, including subtitles, scrolling subtitles, text watermarks, corner marks, logos, and episode information. It allows separate control of the erasure range for subtitles and watermarks, significantly improving the quality of Video Inpaint output results.<br><br>* [Face Blur](https://docs.byteplus.com/docs/Byteplus_LAS/Face_Blur): Face Blur operator, an automated face blur processing tool for video content. The operator can automatically detect faces in videos and apply blur to faces according to the user\-specified blur level, protecting user privacy. |

# September 3, 2026

Release version: LAS AI 1.5.1.

|Function module |Function description |
|---|---|
|LAS operator |Operator optimization:<br><br><br>* [Video Translation](https://docs.byteplus.com/docs/Byteplus_LAS/Video_Translation_operator): The facial translation feature now supports pure visual speech detection for matching faces. When the original video’s audio and lip movements do not match, you can set `lip_translate_param.lip_fuzzy_matching=true` to use pure visual speech detection for fuzzy matching, synchronizing the translated audio with the character’s lip movements. This is suitable for scenarios where the original video’s audio and lip movements are not fully aligned.<br><br>* [Short drama script parsing](https://docs.byteplus.com/docs/Byteplus_LAS/Short_drama_script_parsing): Newly supports script parsing for more languages (Japanese/Korean/Thai/Indonesian/Vietnamese). Except for Chinese scripts, scripts in other languages return English script parsing results after analysis. |
||Newly supports the LAS operator price calculator. You can quickly estimate operator invocation costs on the price calculator page. |

# August 27, 2026

Release version: LAS AI 1.5.0.

|Function module |Function description |
|---|---|
|LAS operator |New operator:<br><br>[Video Translation](https://docs.byteplus.com/docs/Byteplus_LAS/Video_Translation_operator)：The Video Translation operator efficiently and accurately converts video content from the source language to one or more target languages. The service scope includes not only subtitle translation, but also audio translation and facial translation, ultimately outputting the dubbed video and subtitle files in the corresponding languages. |

# August 21, 2026

Release version: LAS AI 1.4.4.

|Function module |Function description |Release region |
|---|---|---|
|LAS operator |New operator:<br><br><br>* [Short drama script parsing](https://docs.byteplus.com/docs/Byteplus_LAS/Short_drama_script_parsing): The short drama script asset parsing operator converts Chinese, English, or Thai scripts into structured asset tables. It reads one or more script files, automatically detects the script language and structure, extracts character, prop, and scene assets, and enriches them with visual descriptions.<br><br>* [Video super-resolution](https://docs.byteplus.com/docs/Byteplus_LAS/Video_super-resolution): The Video Super Resolution operator uses the DOVE video super\-resolution model to upscale input videos and produce higher\-resolution output videos. It supports long\-duration and high\-resolution video processing. |All supported regions |

# August 14, 2026

Release version: LAS AI 1.4.3.

|Function module |Function description |Release region |
|---|---|---|
|LAS operator |New operator:<br><br><br>* [Enhanced/basic video generation](https://docs.byteplus.com/docs/Byteplus_LAS/video_gen_enhanced)：The LAS Enhanced Video Generation/Basic Video Generation service is built around the Seedance 2.x series models, and enhances both the pre\-processing and post\-processing workflows for video generation. It integrates capabilities such as video format conversion, video segmentation, Video Inpaint, subtitle generation, Audio and Video Merge, Video Super Resolution, and more, expanding the boundaries of video generation models, improving the quality and duration of generated videos, reducing token consumption costs, and helping customers increase production efficiency.<br><br>* [Video Edit Enhanced](https://docs.byteplus.com/docs/Byteplus_LAS/Enhanced_video_editing)：The enhanced version of the video editing online service combines input videos and reference images to perform targeted video replacement. It is suitable for scenarios such as advertising material remastering, product replacement, background redrawing, and creative video editing. |All supported regions |

# August 6, 2026

Release version: LAS AI 1.4.2.

|Function module |Function description |Release region |
|---|---|---|
|LAS operator |New operator:<br><br><br>* [Viral clip generation](https://docs.byteplus.com/docs/Byteplus_LAS/Viral_content_editing)：The Viral Clip Generation operator can automatically perform shot detection, semantic analysis, editing decision\-making, and video synthesis based on multiple episodes of short drama videos, generating multiple traffic\-attracting videos suitable for distribution on short video platforms in batches.<br><br>* [Short drama script generation](https://docs.byteplus.com/docs/Byteplus_LAS/Short_drama_script_generation)：The short drama/movie script generation operator (`las_short_drama_script_gen`) is an automated tool for reverse script extraction, designed for serialized or ultra\-long video content, including short dramas, long videos, and movies. Powered by a visual multimodal large model (VLM), the operator can automatically extract all characters from the entire drama or film, analyze character relationships, and generate high\-quality textual scripts and character lists in reverse, including detailed scenes, actions, expressions, and dialogues based on visuals and lines. This facilitates secondary creation, translation for overseas markets, and copyright protection for video content.<br><br>* [Short drama script fission](https://docs.byteplus.com/docs/Byteplus_LAS/Short_drama_script_fission): The short drama script fission operator (`las_short_drama_script_fission`) is used to perform targeted adaptation based on existing episodic scripts. The operator retains the core character structure, conflict chain, emotional curve, and key highlights of the original script, systematically rewrites character identities, worldview settings, regional context, industry background, and key terminology, and generates new script versions tailored to the target market and subject matter. The output includes the diversified episodic script catalog, the complete script, the outline, and the mapping table between the original and new versions, making it suitable for short drama overseas distribution, blockbuster remakes, and content direction testing.<br><br>* [Video scene segmentation](https://docs.byteplus.com/docs/Byteplus_LAS/Video_scene_segmentation)：The video scene segmentation operator uses a multimodal large model to perform shot/scene segmentation, global character recognition, scene\-level character association, and character image extraction on the input video. The operator outputs scene summary results, a character registry, sliced videos for each scene, and image files archived by character, facilitating subsequent retrieval, editing, and content understanding.<br><br>* [Fine-grained video understanding](https://docs.byteplus.com/docs/Byteplus_LAS/Fine-grained_video_understanding)：The video fine\-grained understanding operator is designed for general video content and supports direct understanding and analysis of videos. Whether it is a short video, film clip, course recording, or surveillance footage, after the user uploads a video and provides a query or task_template, the video content can be described, queried, and information can be extracted, with relevant segments located using timestamps. Supports video input up to several hours (maximum 3 hours, 10 GB), and also supports joint audio\-video understanding by combining visual, speech, and sound effect information, making it suitable for retrieval, question answering, and content analysis scenarios. |All supported regions |

# July 30, 2026

Release version: LAS AI 1.4.1.

|Function module |Function description |Release regions |
|---|---|---|
|LAS operators |New operators:<br><br>[Intelligent video editing](https://docs.byteplus.com/docs/Byteplus_LAS/Intelligent_video_editing)：The video intelligent editing operator leverages multimodal large models to provide intelligent video editing capabilities, enabling users to quickly extract valuable content segments from long videos. Supports understanding editing requirements described in natural language, reference image\-assisted recognition (such as characters, objects, scenes, and dialogues), multidimensional video content analysis (visuals, subtitles, storyline), and outputs standardized editing decision information (timestamps, descriptions, and more). |All supported regions |
|Development machine |The development machine now supports directly using the preset Base URL environment variable (`$LAS_BASE_URL`) to call operators. Compared to using a public URL, using the internal network environment is more stable when submitting operator processing tasks in batches.<br><br>For more details about using preset environment variables to call operators on the development machine, see [Obtain the Base URL](https://docs.byteplus.com/docs/Byteplus_LAS/Obtain_the_Base_URL). |All supported regions |

# July 23, 2026

Release version: LAS AI 1.4.0.

|Feature modules |Feature description |Release regions |
|---|---|---|
|Workflow |* The workflow now supports permission control features, allowing you to grant or revoke permissions for workflows you have permission to manage.<br><br>* When running a workflow, you can now customize and modify the workflow instance name. The workflow instance name defaults to the workflow name. You can modify it as needed to other names for easier identification and subsequent searching.<br><br><br>For more information about workflows, see [Workflow](https://docs.byteplus.com/docs/Byteplus_LAS/workflow). |All supported regions |

# July 9, 2026

Release version: LAS AI 1.3.3.

|Feature modules |Feature description |Release regions |
|---|---|---|
|Task management |TOS mounting capability optimization: When creating a task, storage path mounting now supports TOS mounting based on the FSX protocol.<br><br>For more information about task management features, see [Task management](https://docs.byteplus.com/docs/Byteplus_LAS/Task_manage). |All supported regions |

# June 25, 2026

Release version: LAS AI 1.3.1.

|Feature modules |Feature description |
|---|---|
|Task management |* Task instances now support batch retry. You can select multiple task instances for batch retry execution on the Task management page or the Task instances page.<br><br>* New support for periodic task scheduling at 5\-minute and 10\-minute intervals.<br><br>* TOS mounting capability optimization:<br><br>   * New support for mounting TOS Buckets of the HNS type.<br><br><br>For more information about task management features, see [Task management](https://docs.byteplus.com/docs/Byteplus_LAS/Task_manage) |
|General |Product console interface layout and UI optimization:<br><br><br>* The navigation bar entry on the left side of the console page has been optimized. The operation entries for LAS operator\-related features (Operator square, API key management, quota management, asset management) have been consolidated under the unified "Operator service" entry, making it easier for you to learn about, try, and monitor the usage of LAS operators.<br><br>* UI optimization improvements for the Operator square and individual operator pages:<br><br>   * On the Operator square page, you can hover over an operator card to display core information such as billing, input/output modalities, and performance, allowing you to quickly understand key details about the operator.<br><br>   * On the individual operator page, additional information is now displayed, including billing, core capabilities, and major limitations. A link to the operator documentation is provided in the upper right corner, enabling you to conveniently access the operator help documentation for detailed information. |

# June 15, 2026

Release version: LAS AI 1.3.0.

|Feature module |Feature description |
|---|---|
|Task management |Task instances now support batch termination operations. |

# June 2, 2026

Release version: LAS AI 1.2.3.

|Feature module |Feature description |
|---|---|
|Operator square |* New operators:<br><br>   * [Multimodal Deep Thinking (Doubao-Seed-2.0)](https://docs.byteplus.com/docs/Byteplus_LAS/Multimodal-Deep-Thinking-Doubao-Seed-2-0)<br><br>   * Multimodal Deep Thinking (Doubao\-Seed\-1.8) |

# May 14, 2026

Release version: LAS AI 1.2.0.

|Feature module |Feature description |
|---|---|
|Resource management |* LAS has optimized the queue resource troubleshooting and statistics logic. When allocating queue resources, statistics on remaining resources can now be displayed more promptly and accurately. You can use the data on remaining resources to flexibly and efficiently allocate resources based on different business scenarios. When resources are insufficient, you will be reminded to expand resources in a timely manner to ensure stable business operations.<br><br>* The generation logic for LAS API Key values has been optimized. After the optimization, the format for newly generated LAS API Key values has changed to "las\-xxxxxx", with the unified addition of the "las" prefix, making it easier for you to categorize and manage various API Keys.<br><br>   > **Note**<br>   <br><br>   > The format of previously generated LAS API Keys is not affected, and the keys can be used as usual.<br>    |

# April 8, 2026

Release version: LAS AI 1.1.0.

|Feature module |Feature description |
|---|---|
|Operator service |Operator service capability optimization:<br><br><br>* Broader operator coverage: You can now view monitoring metrics for all online operators.<br><br>* More comprehensive operator monitoring metrics: The monitoring metrics for each operator have been enriched, covering more key indicators for each operator. |
|Resource management |LAS API Key functionality optimization:<br><br><br>* The maximum number of LAS API Keys that can be created per primary account has been increased to 20.<br><br>* Support has been added for viewing the last usage time (active time) of each LAS API Key. You can view the corresponding time on the API Key management page.<br><br><br>For more information about LAS API Keys, please refer to [API Key management](https://docs.byteplus.com/docs/Byteplus_LAS/API_key_management). |
|Dataset |When creating a new dataset share, if the access type is Direct access, you can choose whether to enable the open write permission switch as needed.<br><br><br>* After enabling this option, the recipient is allowed to write or delete data, and can inject or update data in this dataset.<br><br>* This configuration is typically used in scenarios where the recipient delivers data to you. Please ensure that you trust this partner.<br><br><br>For more guidance on dataset sharing operations, see [Dataset sharing](https://docs.byteplus.com/docs/Byteplus_LAS/Dataset_sharing). |
|Data processing |* The development machine now supports using the public IP address of the user's public NAT gateway to access it, ensuring a better experience when using public SSH.<br><br>   For more configuration guidance on the development machine, see [Create a development machine](https://docs.byteplus.com/docs/Byteplus_LAS/create_a_development_machine).<br><br>* Workflow now supports enabling a retry switch for individual task nodes. After enabling the retry switch, you can configure the retry policy for the current task node if its execution fails. For more information, see [Workflow](https://docs.byteplus.com/docs/Byteplus_LAS/workflow). |
|General |Optimized the interface operation experience. For example, some list pages now support a button to manually refresh the list status. |
