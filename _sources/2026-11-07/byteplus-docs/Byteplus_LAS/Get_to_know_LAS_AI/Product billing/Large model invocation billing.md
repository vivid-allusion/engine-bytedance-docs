---
title: "Large model invocation billing"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Large_model_billing"
---

This article introduces the details of model fees incurred when using LAS AI operators and related features to call large models.

# Background information

## Description of billing items

|Function modules |Billing item |Billing overview |
|---|---|---|
|Operator plaza & operator services |**ModelArk models**<br><br>When using LAS AI operators for data processing, some operator capabilities are based on ModelArk models. When using such operators, model fees will be charged based on the type of ModelArk model used. |Billing method: "Pay\-as\-you\-go", charged according to the type of model used. |
||**Self\-developed models, model enhancement**:<br><br>Some operators use LAS self\-developed models, or have enhanced capabilities based on certain models. When using such operators, model fees will be charged based on the type of model associated with the operator. |Billing method: "Pay\-as\-you\-go", charged according to the type of model used. |

## Description of billing unit: token

Large models use tokens as the basic unit when processing data. A token can be a word, part of a word, a punctuation mark, a number, or another text fragment. The exact segmentation and the number of characters represented by each token depend on the model's tokenization strategy and the language of the input.

A common calculation method for language large model inference service fees is as follows:

```Plain
Cost = Number of tokens used * Price per token
```

* Because different models use different tokenization strategies, the same text may be converted into different numbers of tokens.

* You can use the [Tokenization API](https://docs.byteplus.com/en/docs/modelark/tokenization-api) to estimate the number of tokens corresponding to your content.

# Billing details for self\-developed models and model enhancement

## Video content generation (basic version + enhanced version)

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Enhanced/basic video generation](https://docs.byteplus.com/docs/Byteplus_LAS/video_gen_enhanced) |Online |The LAS Enhanced Video Generation/Basic Video Generation service is built around the Seedance 2.x series models, and enhances both the pre\-processing and post\-processing workflows for video generation. It integrates capabilities such as video format conversion, video segmentation, Video Inpaint, subtitle generation, Audio and Video Merge, Video Super Resolution, and more, expanding the boundaries of video generation models, improving the quality and duration of generated videos, reducing token consumption costs, and helping customers increase production efficiency. |

* Billing standards

   |Breakdown |Description of billing standards |
   |---|---|
   |Billing item |Duration of input/output video. |
   |Billing type |Pay\-as\-you\-go, unit: USD/second, billed hourly based on actual billing usage. |
   |Unit price |Related to the model version you select (Basic version, Enhanced version). |

   > **警告**

   * > Total cost: In addition to the unit price, it also depends on the duration and resolution of the input/output video.

   * > Only tasks that successfully generate videos will incur charges. Scenarios where video generation fails due to review or other operational reasons will not be charged.

* Billing details

   Billing estimate: `Total cost ≈ Unit price * Billing usage = Unit price * (Video duration * Duration conversion factor)`

   > **警告**

   > The above formula is for cost estimation only. Actual charges are determined by the bill.

   |Version breakdown |Unit price |Model type |Scenario breakdown |Billing item: Video duration |Duration conversion factor: Related to video resolution |
   |---|---|---|---|---|---|
   |Basic version |0.242 USD/second |seedance2.0fast |No input video |Output video duration |* 480P：0.465<br><br>* 720P：1 |
   ||||With input video |Input video duration + Output video duration |* 480P：0.2770<br><br>* 720P：0.5988 |
   |||seedance2.0mini |No input video |Output video duration |* 480P：0.2907<br><br>* 720P：0.625 |
   ||||With input video |Input video duration + Output video duration |* 480P：0.1769<br><br>* 720P：0.3812 |
   |Enhanced version |0.303 USD/second |seedance2.0 |No input video |Output video duration |* 480P：0.4651<br><br>* 720P：1<br><br>* 1080P：2.5<br><br>* 4k：5.0761 |
   ||||With input video |Input video duration + Output video duration |* 480P：0.2830<br><br>* 720P：0.6098<br><br>* 1080P：1.5251<br><br>* 4k：3.1348 |
   |||seedance 2.5 |No input video |Output video duration |* 480P：0.6785<br><br>* 720P：1.525 |
   ||||With input video |Input video duration + Output video duration |* 480P：0.406<br><br>* 720P：0.9125 |

* Billing example

   * Example scenario: Using the enhanced version of video generation (Seedance 2.0), the input includes a reference video (duration: 10 seconds), the output video duration is 10 seconds, and the resolution is 1080p.

   * Cost details:

      `Total cost ≈ Unit price * Billing usage = 0.303 USD/second * (10 seconds + 10 seconds) * 1.5251 = 9.2421 USD`

## HyperFrames Video Generation

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[HyperFrames Video Generation](https://docs.byteplus.com/docs/Byteplus_LAS/hyperframes-video-generation) |Online |Generates videos from natural\-language requests and image, audio, or video references, with configurable rendering, narration, background music, and output storage. |

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |Duration of the output video. |
   |Billing type |Pay\-as\-you\-go in `USD/second`. Bills are generated hourly based on actual billable usage. Billing precision is millisecond\-level, with truncation. |
   |Unit price |0.075 USD/second. |

* Billing details

   Billing formula: `Total fee = Unit price × Output video duration`

## Audio Rebuild

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Audio Rebuild](https://docs.byteplus.com/docs/Byteplus_LAS/audio-rebuild) |Online |Merges generated video clips and rebuilds their audio tracks, or generates audio directly from an authoritative script, with standalone audio and subtitle outputs. |

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |Rebuilt\-audio duration returned in `total_duration_sec` by a successful Poll response. Text\-model tokens are not billed separately. |
   |Billing type |Usage\-based billing in `USD/minute`. |
   |Unit price |0.77 USD/minute. |

## Video Edit Enhanced 2.0

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Video Edit Enhanced 2.0](https://docs.byteplus.com/docs/Byteplus_LAS/Enhanced_video_editing_2) |Online |The Video Edit Enhance 2.0 operator (las_video_edit_enhance) is designed for video production and post\-editing scenarios. Provide a source video, a clear editing request, and the necessary reference images to enhance a video, change local content, replace a person's identity or appearance, replace an object or background, or apply a consistent style to the entire video. The source video is used to preserve existing motion, camera work, composition, and timing, while reference images describe the target result. Content outside the requested edit is preserved as much as possible. |

* Billing standards

   |Breakdown |Billing standards description |
   |---|---|
   |Billing item |Duration of input/output video. |
   |Billing type |Usage\-based billing, unit: USD/second, billed hourly based on actual billing quantity. |
   |Unit price |Depends on the algorithm service version you select (basic version, enhanced version). |

   > **警告**

   * > Total cost per task: In addition to the unit price, it also depends on the duration of the input/output video and the resolution of the input/output video.

   * > If you enable retry based on evaluation results (`"enable_retry"= "true"`), each retry will submit a new task and will be billed separately.

   > For example, after your task runs, if the evaluation result does not meet the standard and you retry twice, there will be costs for three video editing tasks in total.

   * > Only tasks that successfully generate videos will incur costs. Scenarios where video generation fails due to review or other operational reasons will not be charged.

* Billing details

   Billing estimate: `Total cost ≈ Video preprocessing cost + Video editing cost = Video preprocessing unit price * (input video duration + output video duration) + Video editing unit price * (input video duration + output video duration) * conversion factor`

   > **警告**

   > The above formula is for cost estimation only. Actual billing is based on the bill.

   * **`Video preprocessing`** unit price: 0.025 USD/second

   * **`Video editing`** unit price details: This depends on the model type and video resolution you select. Details are as follows.

      |Version breakdown |Unit price |Model type |Duration conversion coefficient: depends on video resolution |
      |---|---|---|---|
      |Basic version |0.242 USD/second |seedance 2.0\-fast |* 480P：0.2770<br><br>* 720P：0.5988 |
      |||seedance 2.0\-mini |* 480P：0.1769<br><br>* 720P：0.3812 |
      |Enhanced version |0.303 USD/second |seedance 2.0 |* 480P：0.2830<br><br>* 720P：0.6098<br><br>* 1080P：1.5251<br><br>* 4k：3.1348 |
      |||seedance 2.5 |* 480P：0.406<br><br>* 720P：0.9125 |

* Billing example

   * Example scenario: Use the `replace/person_replace` task template and the Seedance 2.0 model to perform video face replacement editing. The input video duration is 10 seconds, with a resolution of 1080p.

   * Cost details:

      `Total cost ≈ Video preprocessing cost + Video editing cost = 0.025 USD/second * (10 seconds + 10 seconds) + 0.303 USD/second * (10 seconds + 10 seconds) * 1.5251 ≈ 9.7421 USD`

## Video Edit Enhanced

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Video Edit Enhanced](https://docs.byteplus.com/docs/Byteplus_LAS/Enhanced_video_editing) |Online |The enhanced version of the video editing online service combines input videos and reference images to perform targeted video replacement. It is suitable for scenarios such as advertising material remastering, product replacement, background redrawing, and creative video editing. |

* Billing standards

   |Breakdown |Billing standards description |
   |---|---|
   |Billing item |Duration of input/output video. |
   |Billing type |Usage\-based billing, unit: USD/second, billed hourly based on actual billing quantity. |
   |Unit price |Depends on the algorithm service version you select (basic version, enhanced version). |

   > **警告**

   * > Total cost per task: In addition to the unit price, it also depends on the duration of the input/output video and the resolution of the input/output video.

   * > If you enable retry based on evaluation results (`"enable_retry"= "true"`), each retry will submit a new task and will be billed separately.

   > For example, after your task runs, if the evaluation result does not meet the standard and you retry twice, there will be costs for three video editing tasks in total.

   * > Only tasks that successfully generate videos will incur costs. Scenarios where video generation fails due to review or other operational reasons will not be charged.

* Billing details

   Billing estimate: `Total cost ≈ unit price * billing quantity = unit price * (video duration * duration conversion coefficient)`

   > **警告**

   > The above formula is for cost estimation only. Actual billing is based on the bill.

   |Version breakdown |Unit price |Billing item: Video duration |Duration conversion coefficient: Related to video resolution |
   |---|---|---|---|
   |Basic version |0.242 USD/second |Input video duration + output video duration |`seedance_model` set to seedance 2.0\-fast:<br><br><br>* 480P：0.2770<br><br>* 720P：0.5988 |
   ||||`seedance_model` set to seedance 2.0\-mini:<br><br><br>* 480P：0.1769<br><br>* 720P：0.3812 |
   |Enhanced version |0.303 USD/second |Input video duration + output video duration |`seedance_model` set to seedance 2.0:<br><br><br>* 480P：0.2830<br><br>* 720P：0.6098<br><br>* 1080P：1.5251<br><br>* 4k：3.1348 |
   ||||`seedance_model` set to seedance 2.5:<br><br><br>* 480P：0.406<br><br>* 720P：0.9125 |

* Billing example

   * Example scenario: Using video generation \- enhanced version (Seedance 2.0 model) for video generation, retry option not enabled, input includes a reference video (duration 10 seconds), output video duration is 10 seconds, resolution is 1080p.

   * Cost details:

      `Total cost ≈ unit price * billing quantity = 0.303 USD/second * (10 seconds + 10 seconds) * 1.5215 = 9.2421 USD`

## Short drama script generation

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Short drama script generation](https://docs.byteplus.com/docs/Byteplus_LAS/Short_drama_script_generation) |Online |The short drama/movie script generation operator (`las_short_drama_script_gen`) is a reverse script extraction tool designed for short dramas as well as serialized or ultra\-long video content such as long videos and movies. Powered by a visual large multimodal model (VLM), this operator can automatically extract all characters from the drama or film, analyze character relationships, and reverse\-generate high\-quality textual scripts and character lists containing scene, action, expression, and dialogue details based on visuals and lines. This supports secondary creation, overseas translation, and copyright protection of video content. |

* Billing standards

   |Sub\-items |Billing standards description |
   |---|---|
   |Billing item |Usage is calculated and billed based on **the duration of the input video**. |
   |Billing type |Usage\-based billing, unit: `USD/minute`, invoiced every hour based on actual usage. Billing precision: rounded to the nearest value |
   |Unit price |0.21 USD/minute |

* Billing details

   Billing formula: `Total cost = unit price * usage`

## Short drama script fission

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Short drama script fission](https://docs.byteplus.com/docs/Byteplus_LAS/Short_drama_script_fission) |Online |The short drama script fission operator (`las_short_drama_script_fission`) is used to perform targeted adaptation based on existing episodic scripts. The operator retains the core character structure, conflict chain, emotional curve, and key highlights of the original script, systematically rewrites character identities, worldview settings, regional context, industry background, and key terminology, and generates new script versions tailored to the target market and subject matter. The output includes the diversified episodic script catalog, the complete script, the outline, and the mapping table between the original and new versions, making it suitable for short drama overseas distribution, blockbuster remakes, and content direction testing. |

* Billing standard

   |Item |Billing standard description |
   |---|---|
   |Billing items |There are two billing items: **model input, model output**. The total fee payable is the sum of the fees for all billing items.<br><br><br>* After the process completes the task, you can view the model's token usage in the result returned by the poll interface.<br><br>* `token_usage.prompt_tokens`: Token usage for model input.<br><br>* `token_usage.completion_tokens`: Token usage for model output. |
   |Billing type |Pay\-as\-you\-go, unit: `USD per million tokens`, billed hourly based on actual usage. |
   |Unit price |The unit prices for **model input and model output** are different.<br><br><br>* Input: 1.25 USD per million tokens<br><br>* Output: 7.5 USD per million tokens |

## Short Drama Script Revision

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Short Drama Script Revision](https://docs.byteplus.com/docs/Byteplus_LAS/Short_drama_script_revision) |Online |Performs controlled local revisions on existing short drama generation results, synchronizing updates across global character, scene, and prop tables, episode scripts, and optional structured episode files. |

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing items |There are three billing items: **model input, model output, and cache\-hit input**. The total payable fee is the sum of all billing items.<br><br><br>* `token_usage.prompt_tokens`: Model input token usage.<br><br>* `token_usage.completion_tokens`: Model output token usage.<br><br>* `token_usage.cached_tokens`: Input tokens that hit the cache. |
   |Billing type |Pay\-as\-you\-go in `USD/million tokens`, billed hourly based on actual usage. |
   |Unit price |* Model input: 1.25 USD/million tokens.<br><br>* Model output: 7.5 USD/million tokens.<br><br>* Cache\-hit input: 0.25 USD/million tokens. |

## Short drama script parsing

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Short drama script parsing](https://docs.byteplus.com/docs/Byteplus_LAS/Short_drama_script_parsing) |Online |The short drama script parsing operator is used to automatically convert short drama script text into a structured asset table. The operator reads one or more script files, automatically recognizes the script format and output language, extracts three types of assets—characters, props, and scenes—and supplements character appearance, character styling, prop visual descriptions, and scene spatial descriptions through visual expansion, finally saving the results as a JSON file. |

* Billing standards

   |Sub\-items |Billing standard description |
   |---|---|
   |Billing items |There are two billing items: **model input, model output**. The total fee payable is the sum of all billing items.<br><br><br>* The model's token usage can be viewed in the result returned by the poll interface after the operator completes the task.<br><br>* `token_usage.prompt_tokens`: Token usage for model input.<br><br>* `token_usage.completion_tokens`: Token usage for model output. |
   |Billing type |Usage\-based billing, unit: `USD/million tokens`, billed hourly based on actual usage. |
   |Unit price |The unit prices for **model input, model output** are different.<br><br><br>* Input: 1.25 USD/million Tokens<br><br>* Output: 6.25 USD/million Tokens |

## Video scene segmentation

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Video scene segmentation](https://docs.byteplus.com/docs/Byteplus_LAS/Video_scene_segmentation) |Online |Video shot segmentation operator, based on a multimodal large model, performs shot and scene segmentation, global character recognition, scene\-level character association, and character image extraction on the input video. The operator outputs scene summary results, a character registry, sliced video clips for each scene, and image files organized by character, facilitating subsequent retrieval, editing, and content understanding. |

* Billing standard

   |Breakdown |Billing standard description |
   |---|---|
   |Billing item |Usage is calculated based on **the duration of the input video**. |
   |Billing type |Usage\-based billing, unit: `USD/minute`, billed hourly based on actual usage. Billing accuracy: millisecond\-level accuracy, rounded to the nearest millisecond |
   |Unit price |0.25 USD/minute |

* Billing details

   Billing formula: `Total cost = unit price * usage`

## Storyboard Script Generation

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Storyboard Script Generation](https://docs.byteplus.com/docs/Byteplus_LAS/Storyboard_Script_Generation) |Online |The LAS Storyboard Rewrite operator is designed for script production and e\-commerce voice\-over video workflows, converting input text into a standard `storyboard_bundle`. Currently, two capabilities are provided: generating storyboards from scripts combined with character, prop, and scene asset JSON files, and directly generating storyboards from voice\-over scripts. |

* Billing standards

   |Sub\-items |Billing standards description |
   |---|---|
   |Billing items |The following billing items are included:<br><br><br>* Basic invocation fee: A fixed fee for invoking the operator.<br><br>* Script generation \- image interpretation fee: Billed based on the number of input images.<br><br>* Script generation \- text interpretation fee: Billed based on the amount of input text. |
   |Billing type |Usage\-based billing, invoiced hourly based on actual usage. |
   |Unit price |The unit prices for different billing items vary. See the table below for details. |

* Billing details

   |Billing item |Unit price |
   |---|---|
   |Basic invocation fee |0.86 USD per call |
   |Script generation \- image interpretation fee |0.04 USD per image |
   |Script generation \- text interpretation fee |0.17 USD per 1,000 characters |

## Video Storyboard Gen

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Video Storyboard Gen](https://docs.byteplus.com/docs/Byteplus_LAS/video-storyboard-gen) |Online |Jointly understands reference videos, target product images, and ecommerce requirements, then generates multiple product voiceover and storyboard candidates as standard storyboard bundles. |

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing items |* Basic Call Fee: charged per successful call.<br><br>* Copywriting Generation \- Basic Fee: charged by generated copywriting duration. |
   |Billing type |Usage\-based billing in USD. |

* Billing details

   |Billing item |Unit price |
   |---|---|
   |Basic Call Fee |0.14 USD/call |
   |Copywriting Generation \- Basic Fee |0.21 USD/minute |

## Video Script Planner

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Video Script Planner](https://docs.byteplus.com/docs/Byteplus_LAS/video-script-planner) |Online |Converts video topics, creative requirements, and optional multimodal references into structured production plans containing content structure, storyboards, asset states, character voices, and pacing. |

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing items |* Plan\-generation charge: billed by the planned output duration tier.<br><br>* Multimodal reference\-input surcharge: charged at most once per task when valid content images, PDFs, videos, or a standalone style image are provided. Creative or style text alone does not trigger the surcharge. |
   |Billing type |Pay\-as\-you\-go in USD. Charges are calculated per successful call according to the applicable billing item. |

* Billing details

   |Billing item |Planned output duration |Unit price |
   |---|---|---|
   |Plan\-generation charge |Output plan length ≤ 30 seconds |1.80 USD/call |
   ||30 seconds < output plan length ≤ 1 minute |2.30 USD/call |
   ||1 minute < output plan length ≤ 2 minutes |3.00 USD/call |
   ||2 minutes < output plan length ≤ 5 minutes |4.50 USD/call |
   ||5 minutes < output plan length ≤ 10 minutes |6.80 USD/call |
   ||Output plan length \> 10 minutes |6.80 USD base price, plus 3.70 USD for each additional 10\-minute tier; a partial tier is rounded up. |
   |Multimodal reference\-input surcharge |Not applicable |1.50 USD/call when applicable |

## Intelligent Short Drama & Film Narration

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Intelligent Short Drama & Film Narration](https://docs.byteplus.com/docs/Byteplus_LAS/intelligent-short-drama-and-film-narration) |Online |The Intelligent Short Drama & Film Narration operator (`las_short_drama_highlight_narration`) processes multi\-episode short dramas or a single film, discovers story highlights, and generates a narrated highlight video with configurable narration, TTS voices, original\-audio strategies, and subtitle styles. |

* Billing standards

   |Breakdown |Billing standards description |
   |---|---|
   |Billing items |Charges consist of two billing items: **original video understanding** and **narration video generation**. The total task charge is the sum of these two items.<br><br><br>* **Original video understanding**: Billed based on the total duration of all input videos. Tiered pricing applies to the portion up to and including 60 minutes and the portion exceeding 60 minutes.<br><br>* **Narration video generation**: Billed based on the total duration of all generated narration videos. The actual duration of each generated video is returned in the Poll response field `duration_s`. |
   |Billing type |Usage\-based billing, unit: `USD/minute`. Charges are generated hourly based on actual usage. Billing precision: millisecond\-level accuracy, rounded down to the nearest millisecond. |
   |Unit price |The unit price varies by billing item and duration tier. See the table below. |

* Billing details

   Billing formula: `Total charge = Original video understanding charge + Narration video generation charge`

   |Billing item |Billing tier |Unit price |
   |---|---|---|
   |Original video understanding |Portion of total input video duration up to and including 60 minutes |0.04 USD/minute |
   |Original video understanding |Portion of total input video duration exceeding 60 minutes |0.05 USD/minute |
   |Narration video generation |Total generated narration video duration |0.20 USD/minute |

* Billing example

   * Example scenario: A task processes 30 short drama videos, each 3 minutes long, and generates 20 minutes of narration video.

   * Cost details:

      * Original video understanding charge: `60 minutes × 0.04 USD/minute + 30 minutes × 0.05 USD/minute = 3.90 USD`.

      * Narration video generation charge: `20 minutes × 0.20 USD/minute = 4.00 USD`.

      * Total charge: `3.90 USD + 4.00 USD = 7.90 USD`.

## Intelligent video editing

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Intelligent video editing](https://docs.byteplus.com/docs/Byteplus_LAS/Intelligent_video_editing) |Online |The intelligent video editing operator, based on multimodal large models, provides intelligent video editing capabilities to help users quickly extract valuable content segments from long videos. Supports understanding of editing requirements described in natural language, assisted recognition using reference images (such as characters, objects, scenes), multidimensional video content analysis (visual, subtitles, plot), and outputs standardized editing decision information (timestamps, descriptions, tags). |

* Billing standards

   |Component |Billing standard description |
   |---|---|
   |Billing item |Duration of the input source file. |
   |Billing type |Usage\-based billing, unit: `USD/minute`, billed hourly based on actual usage. Billing precision: rounded down to the nearest second |
   |Unit price |The unit price depends on the selected intelligent editing scenario. Different editing scenarios and modes have different unit prices. |

* Billing details

   Billing formula: `Total cost = unit price * usage`

   |Scenario breakdown |Unit price |
   |---|---|
   |Video editing in `simple` mode<br><br>That is, the request parameter is set to `mode = simple` |0.21 USD/minute |
   |Video editing in `detail` mode<br><br>That is, the request parameter is set to `mode = detail` |0.29 USD/minute |
   |Audio\-only editing<br><br>That is, the request does not specify the `mode` parameter and `enable_asr = true` |0.07 USD/minute |

   > **说明**

   > In the audio\-only editing scenario, after invoking the operator, the billing details will display the billing item as "video editing \- simple mode". The difference in the displayed billing item does not affect the actual cost calculation and settlement.

## Viral content editing

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Viral clip generation](https://docs.byteplus.com/docs/Byteplus_LAS/Viral_content_editing) |Online |The Viral Clip Generation operator can automatically perform shot detection, semantic analysis, editing decisions, and video synthesis based on multiple episodes of short drama videos, generating multiple traffic\-attracting material videos in batches that are suitable for distribution on short video platforms. |

* Billing standards

   |Breakdown |Billing standards description |
   |---|---|
   |Billing items |Billing is calculated based on video duration. Billing items include two parts: **AI analysis fees for input videos** and **clip composition fees**. The total cost to be paid is the sum of all billing items. |
   |Billing type |Usage\-based billing, unit: `USD/minute`. Billing is generated hourly based on actual usage. Billing precision: millisecond\-level accuracy, rounded to the nearest millisecond |
   |Unit price |The unit price depends on the selected intelligent editing mode. Different editing modes have different unit prices. |

* Billing details

   Billing formula: `Total cost = AI analysis fees for all input videos + clip composition fees = ∑(unit price for input video analysis * input video duration) + unit price for clip composition * output video duration`

   |Billing items |Unit price |
   |---|---|
   |Input video analysis |* 0.25 USD/minute<br><br>* When multiple videos are input, each video incurs AI analysis fees. |
   |Output video from clip composition |0.01 USD/minute |

* Billing example

   * Example scenario: 10 short videos, each 3 minutes long, are input. After processing by the algorithm, a 1\-minute viral clip is generated. The cost is as follows:

   * Cost details:

      `Total cost = 10 * 3 minutes * 0.25 USD/minute + 1 minute * 0.01 USD/minute = 7.51 USD`

## Intelligent Video Remix

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Intelligent Video Remix](https://docs.byteplus.com/docs/Byteplus_LAS/Intelligent-Video-Remix) |Online |The Intelligent Video Remix operator leverages understanding of input materials, speech recognition, semantic retrieval, and large model orchestration capabilities to automatically match, sort, and edit talking head, b\-roll, or long real\-shot materials according to script, structured shot list, or natural language creative requirements, producing the final video. |

* Billing standards

   |Sub\-items |Billing standards description |
   |---|---|
   |Billing items |The following billing items are included:<br><br><br>* **Material understanding fee**: The material understanding fee for input video materials is billed based on the total duration of the input video materials.<br><br>   * When inputting video materials via TOS, the material understanding fee is incurred for the same material when the task is submitted for the first time.<br><br>   * If the material does not change in TOS (such as path and file content), the same material will not incur xxx repeatedly.<br><br>* **Intelligent editing fee**: The fee for invoking the model to edit the final video content when generating the final video output. Billed based on the total duration of the output video. No fee is incurred if the final video output is not generated.<br><br>* **Voice\-over (TTS) fee**: Billed based on the number of characters generated for the voice\-over. No fee is incurred if the voice\-over is not generated.<br><br>* **Intelligent subtitle fee**: Billed based on the number of characters generated for intelligent subtitles. No fee is incurred if intelligent subtitles are not generated.<br><br>* **Special effects text fee**: Billed based on the number of characters generated for special effects. No fee is incurred if special effects text is not generated.<br><br><br>The total task fee is the sum of the above billing items. |
   |Billing type |Usage\-based billing, invoiced hourly based on actual usage. Billing precision: millisecond\-level, proportional, no rounding up for durations less than one minute. |
   |Unit price |The unit price varies for different billing items. Details are as follows. |

* Billing details

   |Billing item |Unit price |
   |---|---|
   |Material understanding |0.2 USD/minute |
   |Intelligent editing |* lite: 4 USD/minute<br><br>* pro: 6.5 USD/minute |
   |Voice\-over |0.15 USD/1,000 characters |
   |Intelligent subtitles |0.7 USD/1,000 characters |
   |Special effects text |0.1 USD/1,000 characters |

## Fast Video Remix

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Fast Video Remix](https://docs.byteplus.com/docs/Byteplus_LAS/fast-video-remix) |Online |Combines video materials by act order into multiple short videos for product showcases, marketing campaigns, and promotions. It supports manual, automatic, and random act planning, as well as silent output, synthesized narration, or existing narration. |

* Billing standards

   |Sub\-items |Billing standards description |
   |---|---|
   |Billing items |The following billing items apply:<br><br><br>* **Remix output fee**: Billed by the total actual duration of all successfully generated videos. Subtitled and clean versions of the same video are counted once.<br><br>* **Automatic act\-planning fee**: When `enable_auto_chaptering=true`, billed by the original duration of all visual\-source materials, counting each source once and excluding existing narration. Understanding\-cache hits do not reduce the measured duration. This item is not billed for manual or random act planning.<br><br>* **Narration (TTS) fee**: Billed by the number of characters actually synthesized. Reused narration is not billed repeatedly, and no fee is incurred for existing narration or silent output.<br><br><br>The total task fee is the sum of the preceding billing items. |
   |Billing type |Usage\-based billing. Duration is recorded in milliseconds and prorated without rounding up to a whole minute. Only tasks with `task_status=COMPLETED` and `business_code="0"` are billed. Failed, timed\-out, and canceled tasks are not billed. Regular subtitles and ASR do not incur separate fees. |
   |Unit price |Unit prices vary by billing item. Details are as follows. |

* Billing details

   |Billing item |Unit price |
   |---|---|
   |Remix output |0.1 USD/minute of output |
   |Automatic act planning |0.1 USD/minute of material |
   |Narration (TTS) |0.075 USD/1,000 characters |

## Video Packaging

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Video Packaging](https://docs.byteplus.com/docs/Byteplus_LAS/video-packaging) |Online |Adds subtitles, emphasis, music, and visual packaging to edited portrait videos and delivers a complete video, a clean version, SRT subtitles, and a packaging plan. |

* Billing standards

   |Sub\-items |Billing standards description |
   |---|---|
   |Billing items |Billed by the total original duration of all input videos before playback\-speed adjustment. Subtitles, ASR, and TTS do not incur separate fees. Increasing `playback_speed` does not reduce measured input usage. |
   |Billing type |Usage\-based billing. Duration is recorded in milliseconds and prorated without rounding up to a whole minute. Only tasks with `task_status=COMPLETED` and `business_code="0"` are billed. Failed, timed\-out, and canceled tasks are not billed. |
   |Unit price |Two mutually exclusive tiers are available. Only one tier applies to each task. |

* Billing details

   |Billing item |Unit price |
   |---|---|
   |Standard packaging (`usage.visual_understanding_duration_ms=0`) |0.075 USD/minute of input |
   |With visual understanding (`usage.visual_understanding_duration_ms>0`) |0.15 USD/minute of input. This price includes packaging. |

## Video translation

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Video Translation](https://docs.byteplus.com/docs/Byteplus_LAS/Video_Translation_operator) |Online |The Video Translation operator efficiently and accurately converts video content from the source language to one or more target languages. The service scope includes not only subtitle translation, but also audio translation and facial translation, ultimately outputting the dubbed video and subtitle files in the corresponding languages. |

* Billing standards

   |Breakdown |Explanation of billing standards |
   |---|---|
   |Billing items |Billing is based on the input video duration, and each new language video generated by translation is billed separately. The following billing items may apply to each translated language:<br><br><br>* Video Translation fee: The fixed billing item for invoking this operator.<br><br>* (Optional, charged as needed) Facial translation fee: If the facial translation feature is enabled when invoking the operator, an additional facial translation fee will be charged.<br><br>* (Optional, charged as needed) Video restoration fee: If video restoration is enabled by setting `enable_video_inpaint=true`, an additional fee is charged according to the input parameters in `video_inpaint_params` and the billing rules of the `las_video_inpaint_pro` operator. This fee is not included in the Video Translation unit price. |
   |Billing type |Usage\-based billing, unit: `USD/minute`, with charges settled hourly based on actual usage. Billing precision: rounding |
   |Unit price |The unit prices for Video Translation and facial translation are different.<br><br><br>* Video Translation: 0.32 USD/minute<br><br>* Facial translation: 0.68 USD/minute |

* Billing details

   Billing formula: `Total cost = (Video Translation unit price * input video duration + facial translation unit price * facial translation duration) * number of new language videos generated by translation`

   If video restoration is enabled, its fee is calculated separately according to the billing rules of `las_video_inpaint_pro` and added to the preceding cost.

* Billing example

   * Example scenario: A 10\-minute Chinese video is provided as input, and new videos in English, Japanese, and Korean are required to be generated through translation, with no facial translation needed.

   * Cost details:

      `Total cost = 0.32 USD/minute * 10 minutes * 3 = 9.6 USD`

## Video Subtitle Translation

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Video Subtitle Translation](https://docs.byteplus.com/docs/Byteplus_LAS/Video_Subtitle_Translation) |Online |Extracts subtitles through OCR or ASR, translates them into one or more target languages, and outputs TXT, SRT, XML, or VTT subtitle files. |

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |The total charge is the sum of subtitle extraction and subtitle generation charges. Extraction is billed by input video duration and the selected OCR or ASR precision tier. Generation is billed by video duration for each generated caption file. |
   |Billing type |Pay\-as\-you\-go in `USD/minute`. Charges are generated hourly based on actual billable usage. |

* Billing details

   Billing formula: `Total fee = Selected subtitle extraction unit price × Input video duration + Subtitle generation unit price × Input video duration × Number of caption files`

   |Billing item |Unit price |
   |---|---|
   |Subtitle extraction |* OCR low precision: 0.03 USD/minute.<br><br>* OCR high precision: 0.060 USD/minute.<br><br>* ASR low precision: 0.006 USD/minute.<br><br>* ASR high precision: 0.23 USD/minute. |
   |Subtitle generation |0.02 USD/minute/caption file. |

## Fine\-grained video understanding

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Fine-grained video understanding](https://docs.byteplus.com/docs/Byteplus_LAS/Fine-grained_video_understanding) |Online |The fine\-grained video understanding operator is designed for various types of video content and provides multi\-dimensional, detailed content analysis. Whether it is a short video, movie clip, or long meeting recording, after the user uploads the video and specifies the analysis target, they can obtain searchable and question\-answerable results as well as detailed summaries. |

* Billing standards

   |Breakdown |Description of billing standards |
   |---|---|
   |Billing items |There are four billing items: **model input, model output, cache storage, cache hits**. The total payable cost is the sum of all billing items. |
   |Billing type |Usage\-based billing, unit: `USD/million tokens`, billed hourly based on actual usage. |
   |Unit price |The unit price for each billing item is tiered based on the model input length at the time of model invocation. The unit price varies depending on the input length tier. |

* Billing details

   Billing formula: `Total cost = Model input cost + Model output cost + Cache storage cost + Cache hit cost`

   |Model type |Input length range (thousand tokens) |Input (non\-audio)<br><br>USD/million tokens |Input (audio)<br><br>USD/million tokens |Cache storage<br><br>USD/million tokens/hour |Cache hit (non\-audio)<br><br>USD/million tokens |Cache hit (audio)<br><br>USD/million tokens |Output<br><br>USD/million tokens |
   |---|---|---|---|---|---|---|---|
   |dola\-seed\-2.1\-turbo |Input length [0, 256] |1 |Not applicable |0.0166 |0.2 |Not applicable |5 |
   |seed\-2.0\-pro |Input length [0, 128] |1 |Not applicable |0.0166 |0.2 |Not applicable |6 |
   ||Input length (128, 256] |2 |Not applicable |0.0166 |0.4 |Not applicable |12 |
   |seed\-2.0\-lite |Input length [0, 128] |0.5 |7.5 |0.0166 |0.1 |1.5 |4 |
   ||Input length (128, 256] |1 |15 |0.0166 |0.2 |3 |8 |
   |seed\-2.0\-mini |Input length [0, 128] |0.2 |Not applicable |0.0166 |0.04 |Not applicable |0.8 |
   ||Input length (128, 256] |0.4 |Not applicable |0.0166 |0.08 |Not applicable |1.6 |
   |seed\-1.8 |Input length [0, 128] |0.5 |Not applicable |0.0166 |0.1 |Not applicable |4 |
   ||Input length (128, 256] |1 |Not applicable |0.0166 |0.1 |Not applicable |8 |

* Billing estimation

   * Based on the above billing details table, you can estimate the approximate number of tokens in the input video. Combined with the operator request code, this provides an estimate of the overall model input length.

   * Caution: This estimation result is for reference only and cannot be used as the exact input length data. When processing tasks, there will also be system prompts and other inputs, but the length of these other inputs is generally short.

## Video Inpaint

* Operator Service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Video Inpaint](https://docs.byteplus.com/docs/Byteplus_LAS/Video_Inpaint-Pro) |Online |The video intelligent inpainting operator takes a single video as input and outputs a repaired video with specified content erased. Supports subtitles, scrolling subtitles, text watermarks, corner marks, logos, and episode information, and allows separate control of the erasure range for subtitles and watermarks. |

* Billing standards

   |Sub\-items |Billing standards description |
   |---|---|
   |Billing item |Usage is calculated based on the duration of the output video. For billing, the output video duration is adjusted using coefficients for the output video frame rate and resolution. The adjusted billing duration is used as the billing usage.<br><br>After the task is completed, you can check the actual output video frame rate and resolution values for the current task via the `output_fps` and `resolution` parameters returned by the poll interface. |
   |Billing type |Usage\-based billing, unit: `USD/minute`, billed hourly based on actual billing usage. Billing precision: billed by the minute, accurate to the millisecond |
   |Unit price |The unit price depends on the repair version, target detection, and repair mode you select when using Video Inpaint. When submitting an operator task, you can set the repair version, target detection, and repair mode for the task via<br><br>`model_level` and `detection_mode` request parameters |

   > **警告**

   * > Total cost paid: In addition to the unit price, service billing is associated with the **actual repaired** video duration, frame rate, and resolution.

   * > Video Inpaint does not change the video frame rate, and the duration of the repaired video may be less than the input video duration.

* Billing details

   Billing formula: `Total cost = unit price * billing usage = unit price * (video duration * duration-output frame rate conversion coefficient * duration-output resolution conversion coefficient)`

   |Sub\-scenarios |Unit price |Billing duration\-output frame rate conversion coefficient |Billing duration\-output resolution conversion coefficient |
   |---|---|---|---|
   |* Fast version repair, that is,<br><br>   * `model_level` : `lite` |0.125 USD/minute |Actual output frame rate:<br><br><br>* (0 , 24fps]: coefficient is 0.8<br><br>* (24fps , 30fps]: coefficient is 1<br><br>* Greater than 30fps: The coefficient is determined by the ratio of the actual output video frame rate to the base frame rate (30fps), rounded up to the nearest integer. |Actual total output pixels:<br><br><br>* (0 , 1920×1080]: coefficient is 1<br><br>* (1920×1080 , 3840×2160]: coefficient is 2 |
   |* Professional edition \- standard\-level object detection and restoration, that is,<br><br>   * `model_level` : `pro`<br><br>   * `detection_mode` : `standard_*` |0.375 USD/minute ||Actual total output pixels:<br><br><br>* (0 , 1280×720]: coefficient is 0.6<br><br>* (1280×720 , 1920×1080]: coefficient is 1<br><br>* (1920×1080 , 3840×2160]: coefficient is 2 |
   |* Professional edition \- precise\-level object detection and restoration, that is,<br><br>   * `model_level` : `pro`<br><br>   * `detection_mode` : `precise` |1.50 USD/minute |||

* Billing example

   When using the professional version – precise level target detection and repair mode for Video Inpaint, if the actual output video has a frame rate of 50fps, a resolution of 1080p (1920×1080), and a video duration of 10 minutes:

   * The multiplier of the actual output video frame rate to the base frame rate is 1.6, rounded up to 2.0.

   * The actual cost is:

      `Total cost = 1.5 USD/minute * (10 minutes * 2 * 1) = 30 USD`.

## Face Blur

* Operator Service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Face Blur](https://docs.byteplus.com/docs/Byteplus_LAS/Face_Blur) |Online |The face blur operator processes video in two modes: it can automatically detect faces and blur them to protect privacy, or detect faces without modifying the video and return per\-frame face bounding boxes in a JSON file. |

* Billing standards

   |Sub\-items |Billing standards description |
   |---|---|
   |Billing item |Charges are calculated based on the duration of the output video. |
   |Billing type |Usage\-based billing, unit: `USD/minute`, billed hourly based on actual usage. Billing precision: rounding |
   |Unit price |0.1 USD/minute |

* Billing details

   Billing formula: `Total cost = unit price * usage`

## Sensitive Content Masking

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Sensitive Content Masking](https://docs.byteplus.com/docs/Byteplus_LAS/sensitive-content-masking) |Online |Detects and masks sensitive visual or textual content in images and videos, optionally mutes sensitive speech, and returns processed media and structured detection results. |

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |* Image input: billed by the number of input images.<br><br>* Video input in whole\-video mode: billed by input video duration.<br><br>* Video input in segment mode: billed by the union of the requested intervals within the input video duration. Overlapping portions are counted only once. |
   |Billing type |Pay\-as\-you\-go. Charges are generated hourly based on actual billable usage. |
   |Unit price |* Image: 0.005 USD/image.<br><br>* Video: 0.4 USD/minute. |

## Text to Speech (Doubao Speech 2.0)

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Text to Speech (Doubao Speech 2.0)](https://docs.byteplus.com/docs/Byteplus_LAS/text-to-speech-doubao-speech-2-0) |Online |Provides synchronous streaming speech synthesis through the Process API and returns audio, subtitle, and completion events over SSE. |

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |Synthesized text characters. |
   |Billing type |Usage\-based billing in `USD/10K characters`. |
   |Unit price |4.5 USD/10K characters. |

## Voice Cloning Synthesis

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Voice Cloning Synthesis](https://docs.byteplus.com/docs/Byteplus_LAS/voice-cloning-synthesis) |Online |Supports voice design, voice cloning from reference audio, high\-fidelity continuation, and short\- or long\-form speech synthesis in multiple audio formats. |

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |Unicode characters in the original decoded `req_params.text` for successful tasks. SSML tags, punctuation, spaces, and line breaks are included; audio duration is not billed. |
   |Billing type |Usage\-based billing in `USD/10K characters`. |
   |Unit price |1.5 USD/10K characters. |

## Vocal Separation

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Vocal Separation](https://docs.byteplus.com/docs/Byteplus_LAS/vocal-separation-d93f41dcef5cac84) |Online |Separates input media into vocal and non\-vocal residual tracks; video input also produces a vocals\-only video. |

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |Input audio duration, including the input audio track of video files. |
   |Billing type |Usage\-based billing in `USD/media minute`. |
   |Unit price |0.010 USD/media minute. |

## Speech\-to\-text (LAS ASR Service)

|Operator services |Unit price |
|---|---|
|[Speech-to-Text (LAS ASR Service)](https://docs.byteplus.com/docs/Byteplus_LAS/las_asr) |0.6USD/Hour |

## Speech\-to\-text (Doubao \- enhanced version for audio file recognition)

|Operator services |Unit price |
|---|---|
|[Speech-to-Text (Doubao - Audio File Recognition) Enhanced Version](https://docs.byteplus.com/docs/Byteplus_LAS/las_asr_pro) |* ASR\-Pro standard：0.6 USD/Hour<br><br>   * That is, the `resource` request parameter is set to `bigasr`<br><br>* ASR\-Pro seed：0.35 USD/Hour<br><br>   * That is, the `resource` request parameter is set to `seedasr` |

## Image Pro Image Generation

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Image Pro Image Generation](https://docs.byteplus.com/docs/Byteplus_LAS/image-pro-image-generation) |Online |Generates high\-quality images from natural\-language prompts, with configurable size, quantity, quality, output format, and URL or Base64 JSON results. |

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing items |Input tokens and output tokens. |
   |Billing type |Usage\-based billing in `USD/1K tokens`. |

* Billing details

   |Model |Billing item |Unit price |
   |---|---|---|
   |Image Pro |Input tokens |0.012 USD/1K tokens |
   |Image Pro |Output tokens |0.04 USD/1K tokens |

## Seedream Image Generation

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[Seedream Image Generation](https://docs.byteplus.com/docs/Byteplus_LAS/seedream-image-generation) |Online |Generates images from text or reference images with Seedream 4.5 and 5.0, supporting single\-image generation, sequential generation, and SSE streaming output. |

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |Successful image generation, billed by the number of generated images and the selected model. |
   |Billing type |Usage\-based billing in `USD/image`. |
   |Unit price |Unit prices vary by model. See Billing details. |

* Billing details

   |Model |Unit price |
   |---|---|
   |Seedream 4.5 |0.048 USD/image |
   |Seedream 5.0 |0.042 USD/image |

## PDF Document Parsing (Doubao)

* Operator service

   |Operator name |Usage method |Operator overview |
   |---|---|---|
   |[PDF Document Parsing (Doubao)](https://docs.byteplus.com/docs/Byteplus_LAS/pdf-document-parsing-doubao-22cb891fa6299267) |Online |Parses PDF, Word (DOC and DOCX), and image files through a visual model and outputs high\-fidelity Markdown and structured results. The operator detects the input type from the file header. |

* Billing standards

   |Breakdown item |Billing standard description |
   |---|---|
   |Billing item |Usage is calculated from the number of pages after intelligent segmentation of the input PDF, converted Word document, or image.<br><br>> **Note**<br><br><br>> When an input PDF page or image is too long and its width\-to\-height ratio is below the threshold, LAS automatically segments and parses it. The `billable_pages` field returned by Poll is the number of pages after intelligent segmentation.<br> |
   |Billing type |Usage\-based billing in `USD/page`, with charges generated hourly based on actual billable usage. |
   |Unit price |The unit price depends on the selected PDF parsing mode. |

* Billing details

   Billing formula: `Total fee = Unit price × Usage`

   |Scenario |Unit price |
   |---|---|
   |PDF parsing mode: normal |0.006 USD/page |
   |PDF parsing mode: detail |0.015 USD/page |

# Billing details for ModelArk model

Operators based on the ModelArk model can be divided into two types according to the inference type when processing data: "online inference" and "batch inference". The following sections introduce the billing details for these two types of models.

## Operators billed by ModelArk model usage

The following operators invoke ModelArk models and are billed according to the applicable model and usage. Some operators require a ModelArk API key. They do not have an additional fixed operator unit price.

|Operator name |Usage method |Billing overview |
|---|---|---|
|[Video Prompt Generation](https://docs.byteplus.com/docs/Byteplus_LAS/video-prompt-generation) |Online |Model input, model output, and applicable cache usage are billed according to the selected ModelArk model. |
|[Video-to-Prompt Generation](https://docs.byteplus.com/docs/Byteplus_LAS/video-to-prompt-generation) |Online |Model input, model output, and applicable cache usage are billed according to the models used for source\-video fact extraction and prompt generation. |
|[Embodied Semantic Annotation](https://docs.byteplus.com/docs/Byteplus_LAS/embodied-semantic-annotation) |Online |Model input, model output, and applicable cache usage are billed according to the ModelArk model selected through `model_name`. |
|[Image-Text Embedding (Skylark Models)](https://docs.byteplus.com/docs/Byteplus_LAS/image-text-embedding-skylark-models-67f8e3f58049150a) |Online |Text and image inputs are billed according to their respective Skylark multimodal embedding inference rates. |

## Online inference models

|Model name |Billing item |Unit price |Condition (thousand tokens) |
|---|---|---|---|
|Seed\-2.0\-pro |Input |0.5 USD/M Tokens |Prompt length [0, 128] |
||Output |3 USD/M Tokens ||
||Cache\-hit Input |0.1 USD/M Tokens ||
||Input |1 USD/M Tokens |Prompt length (128, 256] |
||Output |6 USD/M Tokens ||
||Cache\-hit Input |0.2 USD/M Tokens ||
||Cache\-storage |0.008333 USD/M Tokens/Hour |Not applicable |
|Seed\-2.0\-lite |Input |0.25 USD/M Tokens |Prompt length [0, 128] |
||Output |2 USD/M Tokens ||
||Cache\-hit Input |0.05 USD/M Tokens ||
||Input |0.5 USD/M Tokens |Prompt length (128, 256] |
||Output |4 USD/M Tokens ||
||Cache\-hit Input |0.1 USD/M Tokens ||
||Cache\-storage |0.008333 USD/M Tokens/Hour |Not applicable |
|Seed\-2.0\-mini |Input |0.1 USD/M Tokens |Prompt length [0, 128] |
||Output |0.4 USD/M Tokens ||
||Cache\-hit Input |0.02 USD/M Tokens ||
||Input |0.2 USD/M Tokens |Prompt length (128, 256] |
||Output |0.8 USD/M Tokens ||
||Cache\-hit Input |0.04 USD/M Tokens ||
||Cache\-storage |0.008333 USD/M Tokens/Hour |Not applicable |
|Dola\-Seed\-2.1\-Turbo |Input |0.5 USD/M Tokens |Prompt length [0, 256] |
||Output |2.5 USD/M Tokens ||
||Cache\-hit Input |0.1 USD/M Tokens ||
||Cache\-storage |0.008333 USD/M Tokens/Hour |Not applicable |
|Seed\-1.8 |Input |0.25 USD/M Tokens |Prompt length [0, 128] |
||Output |2 USD/M Tokens ||
||Input |0.5 USD/M Tokens |Prompt length (128, 256] |
||Output |4 USD/M Tokens ||
||Cache\-storage |0.008333 USD/M Tokens/Hour |Not applicable |
||Cache\-hit Input |0.05 USD/M Tokens |Not applicable |
|Seed\-1.6 |Input |0.25 USD/M Tokens |Prompt length [0, 128] |
||Output |2 USD/M Tokens ||
||Input |0.5 USD/M Tokens |Prompt length (128, 256] |
||Output |4 USD/M Tokens ||
|Seedream\-4.5 |Not applicable |0.04 USD / image |Not applicable |
|Seedream\-4.0 |Not applicable |0.03 USD / image |Not applicable |
|skylark\-embedding\-vision\-251215 |Inference service (text input) |0.125 USD/million tokens |Not applicable |
||Inference service (image input) |0.325 USD/million tokens |Not applicable |

## Batch inference models

|Model name |Billing item |Unit price |Condition (thousand tokens) |
|---|---|---|---|
|Seed\-1.8 |Input |0.125 USD/M Tokens |Prompt length [0, 128] |
||Output |1 USD/M Tokens ||
||Input |0.25 USD/M Tokens |Prompt length (128, 256] |
||Output |2 USD/M Tokens ||
||Cache\-hit Input |0.05 USD/M Tokens |Not applicable |
|Seed\-1.6 |Input |0.125 USD/M Tokens |Prompt length [0, 128] |
||Output |1 USD/M Tokens ||
||Input |0.25 USD/M Tokens |Prompt length (128, 256] |
||Output |2 USD/M Tokens ||

# Quota description

* Batch inference quota TPD calculation logic:

   * For the same account, calculation is aggregated by model name (such as all versions of `bytedance-pro-32k-***`).

   * It is not combined with the rate limit for online inference.

> **说明**

> For example, if you use the bytedance\-pro\-32k model under your primary account, there are three batch inference tasks (a, b, c) and two online inference tasks (d, e). Then, each day, batch inference tasks a, b, and c share a 10B token quota, while d and e share the TPM and RPM rate limits for online inference tasks.

* The principle of ModelArk's batch inference quota setting is to ensure fair resource allocation among users and prevent abuse or misuse of interfaces that could cause platform overload and service interruption. To process more data daily for your business, you can [submit a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D).

* You can submit tasks that exceed your quota. When the ModelArk platform has available resources, your quota will be dynamically expanded.

* The TPD time calculation window is a 24\-hour sliding window. A single short\-term high\-concurrency request will affect the quota for the subsequent 24 hours. Compared to a fixed window, please pay attention to the even distribution of your requests.

* Account quota: By default, each model is allocated 10B tokens per day. You can apply for a quota increase by [submitting a ticket](https://console.byteplus.com/workorder/create?ref=L2xhcy9yZWdpb246bGFzK2FwLXNvdXRoZWFzdC0xL25leHQvaG9tZQ%3D%3D).
