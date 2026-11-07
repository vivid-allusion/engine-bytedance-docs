---
title: "Model training"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Model_training"
---

This document is intended for data production teams working with world models, video understanding models, and video generation models. It introduces how to use the Fine\-grained Video Understanding API to produce general video descriptions for large\-scale pretraining datasets: generating unified whole\-video semantic descriptions for raw videos, or structured descriptions with temporal boundaries. The solution is not tied to any specific vertical scenario or action label system, and the output can be integrated into the data production, filtering, quality inspection, and manual review pipeline.

<span id="c0b6bb1c"></span>
# Typical scenarios

In large\-scale video pretraining data production, the core requirement is usually not to write specialized rules for a fixed scenario, but to convert videos from different sources and content types into stable, batch\-processable, and sample\-checkable textual supervision signals.


|Training direction |Large\-scale data requirements |Recommended products |
|---|---|---|
|World models |Learn scenes, objects, spatial relationships, action changes, and physical processes from general videos. |General video description, spatial relationships, action processes, and event segments. |
|Video understanding models |Build video\-level semantic, segment indexing, and temporal supervision data covering content from multiple sources. |Video\-level fine\-grained description, dense video description, event\-level, and action/scene\-level time segments. |
|Video generation models |Build high\-quality video\-text pairs covering subjects, actions, shots, styles, and temporal changes. |Generative prompts, shot descriptions, motion descriptions, style descriptions, and usability tags. |


<span id="59e93db7"></span>
# Related operators

[Fine-grained video understanding](https://docs.byteplus.com/docs/Byteplus_LAS/Fine-grained_video_understanding)Operator: Capable of generating general video\-level descriptions and dense video descriptions (segment\-level descriptions with temporal boundaries), covering overall semantics, subjects and environment, action changes, shot information, subtitles/on\-screen text, and temporal progression, among other general dimensions.

<span id="3c2bff74"></span>
# Application practices

<span id="1bc6a21f"></span>
## Usage recommendations


|Comparison items |Video\-level fine\-grained description |Dense video description |
|---|---|---|
|Best suited for |Large\-scale video\-level text supervision, video\-text pairing, retrieval indexing, and generation prompts. |Segment\-level temporal supervision, long video slicing, event indexing, and batch quality inspection. |
|Advantages |The text is complete and natural, making it convenient as general video\-level semantic tags. |The structure is unified and has temporal boundaries, making it convenient for batch cropping, filtering, and sampling inspection. |
|Result consumption |Forms video\-text pairs with the original video and enters the pretraining sample pool. |Segment event fragments or action/scene fragments based on `start/end`, and add them to the fragment\-level sample pool. |
|Recommended combinations |First, generate a global semantic description for coarse filtering and video\-level training. |Then, generate sliceable temporal descriptions for fine\-grained sample derivation. |



* To achieve video\-text alignment as the training objective, prioritize video\-level fine\-grained descriptions.

* To achieve segment\-level temporal supervision, automatic slicing, or long video indexing as the training objective, prioritize dense video descriptions.

* The generated results are based solely on visual content and should not supplement information not present in the visuals using audio, file names, or external context.

* It is recommended to conduct sampling evaluation before batch production: check whether the video\-level fine\-grained descriptions are accurate, whether the time segments in dense video descriptions are continuous or overlapping, and whether there are any fabrications.


<span id="c1877840"></span>
## Practice reference 1: Video\-level fine\-grained description

<span id="d27946b9"></span>
### Task description

Video\-level fine\-grained descriptions are used for large\-scale video corpora, to generate a general Chinese description for each complete video. No timestamps, lists, or JSON are output. It does not rely on specific scenario rules and is suitable for use as video\-level semantic tags, video\-text pairing, and supervision of pretraining data text.

<span id="b3f458bb"></span>
### Invocation method

In the request, set `task_template` to `general_video_captioning`, and simply provide the video URL additionally.

```JSON
{
  "operator_id": "las_long_video_understand",
  "operator_version": "v1",
  "data": {
    "video_url": "tos://bucket/path/to/video.mp4",
    "task_template": "general_video_captioning"
  }
}
```


<span id="a5756291"></span>
### Effect demonstration


* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8ce9a7d0b5d4aa98672fa66ec2e226b~tplv-goo7wpa0wc-image.image" controls></video>


* Use case 1: Fine\-grained description

   * Task template: `general_video_captioning`, which generates a general Chinese description.

   * Applicable scenarios: Suitable for use as video\-level semantic tags, video\-text pairing, and text supervision for pre\-training data.

   * Example output

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d918b79ebbb042ad94500c8bd4ce13fb~tplv-goo7wpa0wc-image.image) </span>

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c6c2a574899a48a0b876be777df77088~tplv-goo7wpa0wc-image.image" name="EP01-general.json">EP01-general.json</Attachment>
      


<span id="9e4d7bc3"></span>
## Practical reference 2: Dense video description

<span id="15a18b0e"></span>
### Task description

Dense video description is used for large\-scale video corpora, organizing general video content into video\-level summaries, event segments, and action/scene segments, and outputting JSON with `start/end`. It emphasizes unified structure and temporal boundaries, making it suitable for segment\-level indexing, temporal supervision construction, automatic slicing, and batch quality inspection, without being restricted to any specific scenario category.

<span id="f3555fcb"></span>
### Invocation method

In the request, set `task_template` to `dense_video_captioning`, and simply provide the video URL additionally.

```JSON
{
  "operator_id": "las_long_video_understand",
  "operator_version": "v1",
  "data": {
    "video_url": "tos://bucket/path/to/video.mp4",
    "task_template": "dense_video_captioning"
  }
}
```


<span id="3c81dcf0"></span>
### Effect demonstration


* <video src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8ce9a7d0b5d4aa98672fa66ec2e226b~tplv-goo7wpa0wc-image.image" controls></video>


* Use case 2: Dense video description

   * Task template: `dense_video_captioning`, which segments by time and generates summaries of actions and scene content.

   * Applicable scenarios: Emphasizing unified structure and temporal boundaries, it is suitable for fragment\-level indexing, temporal supervision construction, automatic slicing, and batch quality inspection, without restriction to any specific scene category.

   * Example output:

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6ec62aca436847cd9e8b17f03f1e8b85~tplv-goo7wpa0wc-image.image) </span>

      <Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e4bfaf5ef67e46368ea23d681bcf0b8a~tplv-goo7wpa0wc-image.image" name="EP01.json">EP01.json</Attachment>
