---
title: "Precision erasure overview"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/docs-precision-subtitle-erasure"
---

To programmatically remove hardcoded subtitles for content localization or secondary creation, you can use the BytePlus VOD precision erasure feature. This guide provides step\-by\-step instructions and API examples for implementing both automatic and manual subtitle removal. You will learn how to configure tasks to erase multilingual subtitles, specify precise erasure areas to prevent accidental removal, and achieve high\-quality background restoration for a seamless final video.

<span id="eb00b0f3"></span>
## Key features


* **High\-frame\-rate OCR subtitle detection:**  Leveraging BytePlus’s high\-frame\-rate OCR (Optical Character Recognition) detection algorithms, the system precisely identifies and locates subtitle content within videos. This technology is specifically optimized for short\-form drama scenarios, accurately distinguishing between dialogue subtitles (to be erased) and essential contextual text—such as plot prompts, series titles, and text stickers—which should be preserved. High\-frequency frame sampling ensures comprehensive detection, providing a solid foundation for subsequent erasure.

* **AIGC\-powered image restoration:**  For the restoration phase, we utilize self\-developed AIGC (AI\-Generated Content) inpainting algorithms, combining temporal analysis with multi\-frame joint processing to intelligently reconstruct the background in erased areas. The algorithm maintains inter\-frame stability through optical flow estimation and feature matching. By applying deep learning to generate realistic textures, the restored areas blend seamlessly with the original video, achieving a high\-quality visual result with virtually no visible artifacts.


<span id="3825ab11"></span>
## Application scenarios


* **Short\-form drama and TV series:** 

   * **Secondary creation:**  When performing secondary edits on series, you can remove the original subtitles and add new ones that align with your creative vision.

   * **Translated series:**  You can erase original subtitles and replace them with localized subtitles to help audiences from different linguistic backgrounds understand the content.

* **Education and training:** 

   * **Course material production:**  When using video clips as teaching materials, the existing subtitles might not fully align with the teaching objectives or could even distract students. You can erase the original subtitles and add new ones tailored to your educational needs.

   * **Language learning:**  When developing language learning materials, you can create a "subtitle\-free" environment by erasing the original subtitles. This encourages learners to engage more effectively in listening comprehension and oral imitation, ultimately enhancing their overall language proficiency.

* **Advertising and marketing:** 

   * **Ad production:**  To emphasize product features or brand message, you can remove irrelevant subtitles. This allows for the redesign of subtitles that match the advertisement's visual style and promotional focus, enhancing visual impact and information delivery efficiency.

   * **Multi\-platform distribution:**  When launching advertisements across different platforms, subtitles can be adjusted according to platform\-specific characteristics and audience preferences, improving the communication impact.


<span id="5cdd51e2"></span>
## Capabilities and limitations


|Type |Description |
|---|---|
|Supported types |* **Subtitle**: This feature is specifically optimized for removing white subtitles in the lower half of the video, without black drop shadows, moderately sized, non\-decorative, and horizontally aligned.<br><br>* **Text**: Supports erasing all text in the video, including:<br><br>   * In\-scene text<br><br>   * Regulatory filing information<br><br>   * Stylized text<br><br>   * Location information and text watermarks<br><br>   * Narrative elements (such as plot or character cues, and text stickers) |
|Unsupported types |Vertically aligned text, oversized subtitles, and highly transparent subtitles are not supported by this feature. |


<span id="f9b27a72"></span>
## Pricing

Fees for precision erasure are calculated based on the actual duration of the output video. For detailed pricing information, please refer to [Precision erasure pricing](https://docs.byteplus.com/docs/byteplus-vod/docs-pay-as-you-go-pricing#e536c685).
