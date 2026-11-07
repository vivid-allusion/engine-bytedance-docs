---
title: "Video subtitle synchronization check"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Video_subtitle_synchronization_check"
---

The AI Data Lake Service provides advanced multimodal data processing capabilities. Its video subtitle synchronization check solution is based on the Daft distributed computing framework and LAS multimodal processing operators, and uses a multi\-stage, intelligent video analysis pipeline to help users automatically detect the synchronization between video subtitles and speech content. This solution can convert raw video data into a structured dataset with precise synchronization analysis results, providing a reliable basis for video content quality assessment and optimization.

<span id="0e893637"></span>
## **Background information**

As video has become the mainstream medium for information dissemination, the quality of subtitles directly affects the viewer experience, the accuracy of information acquisition, and content accessibility (Accessibility). A common quality issue is that subtitles and speech are out of sync, meaning that the appearance and disappearance times of subtitles are delayed or advanced compared to the corresponding speech timeline.

Traditionally, detection of such issues relies on manual review. However, when faced with massive amounts of video data, manual review is not only inefficient and costly, but also prone to errors due to subjective judgment and fatigue. Automated synchronization detection capabilities are especially critical in scenarios with extremely high requirements for information accuracy, such as online education, professional training, film and television productions, and news broadcasting. Therefore, building an automated solution that can accurately, efficiently, and analyze the synchronization between video subtitles and speech in batches has become a key technical component for improving video content quality and production efficiency.

<span id="ed1668e1"></span>
### **Applicable scenarios**


* **Video content quality assessment**: Suitable for scenarios that require batch assessment of video subtitle quality, such as online education platforms, recorded video conferences, streaming media services, and other applications with strict requirements for subtitle synchronization.

* **Multimedia content review**: Suitable for large\-scale video content review scenarios, it rapidly identifies videos with subtitle and audio desynchronization issues through automated detection, improving platform content quality.

* **Subtitle production quality control (QC)** : Designed for the quality control stage in the subtitle production workflow, it automatically detects whether the timeline is accurately aligned with the audio content before subtitle delivery, ensuring production quality.


<span id="3e24f89d"></span>
### **Key features**


* **End\-to\-end detection process**: Supports a complete processing pipeline from raw video to final synchronization analysis results, covering core stages such as audio extraction, automatic speech recognition (ASR), and visual language model (VLM) analysis.

* **Multimodal fusion analysis**: Deeply integrates audio processing, speech recognition, video understanding, and other multimodal operators. Cross\-verification of audio, visual, and textual information ensures the accuracy of detection results.

* **Intelligent speech and speaker recognition**: Based on Doubao ASR's high\-precision speech recognition and speaker separation capabilities, it accurately extracts structured speech text containing timestamps and speaker information.

* **Advanced visual language understanding**: Utilizes the advanced Doubao 1.5\-vision\-pro visual language model to accurately recognize subtitle text in video frames and its display timing.

* **Precise time alignment analysis**: By matching and semantically analyzing ASR speech timestamps with VLM visual subtitle timestamps, it precisely determines the synchronization and latency between subtitles and audio content.

* **Distributed processing capability**: Leveraging the parallel scheduling mechanism provided by Daft, it enables high\-performance, distributed detection of video data at the terabyte scale.

* **Flexible operator composition**: All processing steps are implemented based on composable operators in LAS, allowing users to flexibly adjust, replace, or extend processing modules according to specific requirements.


<span id="7bcf4338"></span>
## **Prerequisites**


* You have registered a and a [Byteplus account](https://www.Byteplus.com/). To log in to the for the first time, please complete and [identity verification](https://console.byteplus.com/user/authentication/) first.

* Object Storage TOS product has been enabled.

* [AI Data Lake Service product](https://console.byteplus.com/las/region:las+ap-southeast-1/next/home) has been enabled.

* General queue and compute queue have been created.

* Development machine has been created, and the relevant environment variables have been configured, especially `OPENSPEECH_APPID`, `OPENSPEECH_TOKEN`, and `OPENSPEECH_ENDPOINT` required for the Doubao ASR service.


<span id="43dd9f9a"></span>
## **How it works**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7e86fc95b3544d1183ff0fff4376866f~tplv-goo7wpa0wc-image.image) </span>

This solution uses a multi\-stage pipeline architecture, enabling precise detection of video subtitle synchronization through the collaborative operation of multimodal operators.

<span id="4f55eebc"></span>
### **Core processing workflow**


|Stage |Function description |Details |Operator list |
|---|---|---|---|
|**Audio extraction** |Extract the audio stream from the video file. |Separate the audio track from the video and standardize it into a format suitable for subsequent ASR processing (such as 16kHz mp3). |VideoExtractAudio |
|**Speech recognition** |Perform speech recognition and speaker separation on the extracted audio. |Use the Doubao ASR service for high\-precision speech recognition, outputting structured data containing the start and end times, speaker ID, and text content for each speech segment. |AudioAsrDoubao |
|**ASR result parsing** |Parse the raw output of ASR into a structured subtitle list. |Use a custom operator to parse the text returned by ASR into a JSON array containing the speaker, start time, end time, and text content. |Custom AsrTextParser |
|**Prompt generation** |Generate prompts for analysis tasks for the Visual Language Model (VLM). |Embed the structured ASR results into a preset prompt template, instructing the VLM to perform subtitle synchronization analysis on the video. |Custom VlmPromptGenerator |
|**Video understanding and synchronization analysis** |Use VLM to perform multimodal analysis on the video and detect synchronization. |The VLM receives the video file and the generated prompt, analyzes the video frame content to determine whether the timing of subtitle appearance in the picture matches the speech timestamps provided by ASR, and outputs a structured JSON result. |ArkLLMThinkingVision |


<span id="8072c21c"></span>
### Case study

**Original video:**  This article uses videos selected from the open\-source MME\-VideoOCR dataset ([CC-BY-4.0](https://creativecommons.org/licenses/by/4.0/deed.en)).


* HuggingFace：https://huggingface.co/datasets/DogNeverSleep/MME\-VideoOCR_Dataset/tree/main


**Processing results**: You can select files from the dataset and store them in the TOS bucket. After completing the configuration described in this article, you will obtain the demo results.


* Synchronization analysis results


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/93f4e30353594d4dadf0be4f83c1e9d5~tplv-goo7wpa0wc-image.image" width="3668px" /></div>


For details, refer to the processing results section later in this article.


* Audio extraction results


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e12de17cc0a84d969f99b11cfa4a7225~tplv-goo7wpa0wc-image.image" width="1280px" /></div>


<span id="f0f3668e"></span>
## **Operating procedure**

<span id="05b6d37f"></span>
### **Step 1: Development and debugging**

The development machine is a professional development environment provided by the AI Data Lake Service for algorithm developers. It features high efficiency and convenience, enabling developers to quickly start writing, debugging, and running data processing tasks.

You can use a terminal or an IDE such as VSCode on your local or other devices to connect to the development machine remotely via direct SSH connection, and quickly start writing, debugging, and running data processing tasks. For operation guidance, see [Remote connection to the development machine](https://www.volcengine.com/docs/6492/1747863).


1. Developers use the Daft framework on the LAS development machine to write and run the complete video processing pipeline.


The following is the complete pipeline code, including data loading, invocation of processing operators at each stage, and custom parsing and prompt generation logic.

```Python
from __future__ import annotations

import logging
import os
import re
from datetime import datetime
from typing import List, Dict, Any

import daft
from daft import col
from daft.las.functions.video.video_extract_audio import VideoExtractAudio
from daft.las.functions.audio.audio_asr_doubao import AudioAsrDoubao
from daft.las.functions.text.pre_sign_url_for_tos import PreSignUrlForTos
from daft.las.functions.ark_llm.ark_llm_thinking_vision import ArkLLMThinkingVision
from daft.las.functions.udf import las_udf
from daft.las.io.tos import TOSConfig
from daft.las.functions.types import Operator
from daft.dependencies import pa

logging.basicConfig(level=logging.INFO, format="%(asctime)s - %(levelname)s - %(message)s")
logger = logging.getLogger(__name__)

class AsrTextParser(Operator):
    def parse_asr_segments(self, asr_text_simple: str) -> List[Dict[str, Any]]:
        if not asr_text_simple or asr_text_simple.strip() == "None":
            return []
        
        segments = []
        speaker_blocks = asr_text_simple.strip().split('\n\n')
        
        for block in speaker_blocks:
            lines = block.strip().split('\n')
            if len(lines) < 2:
                continue
                
            header_line = lines[0]
            text_content = '\n'.join(lines[1:]).strip()
            
            pattern = r'说话人\s+(\d+)\s+(\d+:\d+:\d+)\s+(\d+:\d+:\d+)'
            match = re.match(pattern, header_line)
            
            if match:
                speaker_id = match.group(1)
                start_time = match.group(2)
                end_time = match.group(3)
                
                segments.append({
                    "speaker": f"说话人 {speaker_id}",
                    "start_time": start_time,
                    "end_time": end_time,
                    "text": text_content
                })
        
        return segments
    
    def transform(self, asr_texts: pa.Array) -> pa.Array:
        results = []
        for asr_text in asr_texts.to_pylist():
            parsed_segments = self.parse_asr_segments(asr_text)
            results.append(parsed_segments)
        
        return pa.array(results, type=self.__return_column_type__())
    
    @staticmethod
    def __return_column_type__() -> pa.DataType:
        return pa.list_(pa.struct([
            pa.field("speaker", pa.string()),
            pa.field("start_time", pa.string()),
            pa.field("end_time", pa.string()),
            pa.field("text", pa.string())
        ]))

class VlmPromptGenerator(Operator):
    def time_str_to_seconds(self, time_str: str) -> float:
        parts = time_str.split(':')
        hours = int(parts[0])
        minutes = int(parts[1])
        seconds = int(parts[2])
        return hours * 3600 + minutes * 60 + seconds
    
    def generate_vlm_prompt(self, asr_segments: List[Dict[str, Any]]) -> str:
        subtitles = []
        timestamps = []
        
        for segment in asr_segments:
            subtitles.append(segment['text'])
            start_seconds = self.time_str_to_seconds(segment['start_time'])
            end_seconds = self.time_str_to_seconds(segment['end_time'])
            timestamps.append([start_seconds, end_seconds])
        
        original_prompt = """你是一名视频字幕核对助手，负责核对视频声音和字幕是否同步。具体任务是结合ASR提取的一一对应的视频字幕以及时间戳列表，对比分析视频画面中的字幕时间是否和结构化视频字幕的开始时间和结束时间同步，并记录分析结果。

如下ASR 字幕示例，字幕 "很高兴你能过来" 开始时间是 4.8 秒，结束的时间是 7.46 秒。 
<ASR 字幕示例>
[……,"很高兴你能过来",……]
</ASR 字幕示例>
<ASR 字幕时间戳示例>
[……,[4.8,7.46],……]
</ASR 字幕时间戳示例>

首先，请仔细阅读以下ASR提取的视频字幕列表、字幕起始和终止时间戳列表：
<ASR_list_subtitles>
{{ASR_LIST_SUBTITLES}}
</ASR_list_subtitles>
<ASR_list_timestamps>
{{ASR_LIST_TIMESTAMPS}}
</ASR_list_timestamps>
接下来，请仔细分析视频画面中的字幕，按照以下步骤进行：
1. 逐一对视频画面中的字幕与结构化的语音字幕逐一进行匹配。
2. 对比每一条匹配字幕的开始时间和结束时间。
3. 若开始时间和结束时间一致或在可接受的误差范围内（如±0.5秒），则判定为同步；否则判定为不同步。
4. 记录每一条字幕的核对结果，如果不同步，在结果 "notes" 字段说明视频画面字幕的延迟出现，还是提前出现，并记录具体的时间，。

请结合结构化的视频字幕和时间戳列表仔细分析视频，然后逐条给出视频字幕和语音字幕匹配检测的结果，结果格式为 JSON，不做额外解释。
其中，start_time为语音字幕开始时间，end_time为语音字幕结束时间，text为语音字幕，vlm为检索结果，如下为输出示例：
[……,
  {
    "start_time": 4.8,
    "end_time": 7.46,
    "text": "很高兴你能过来",
    "vlm": {"是否同步":"<是/否>", "notes":"<视频画面字幕的延迟出现/提前出现> X 秒"}
  },
……
]"""
        
        prompt = original_prompt.replace("{{ASR_LIST_SUBTITLES}}", str(subtitles))
        prompt = prompt.replace("{{ASR_LIST_TIMESTAMPS}}", str(timestamps))
        
        return prompt
    
    def transform(self, asr_segments_list: pa.Array) -> pa.Array:
        results = []
        for asr_segments in asr_segments_list.to_pylist():
            prompt = self.generate_vlm_prompt(asr_segments)
            results.append(prompt)
        
        return pa.array(results, type=self.__return_column_type__())
    
    @staticmethod
    def __return_column_type__() -> pa.DataType:
        return pa.string()

def run_pipeline(input_tos_dir: str, audio_output_tos_dir: str):
    input_s3_dir = input_tos_dir.replace("tos://", "s3://", 1)
    tos_config = TOSConfig.from_env()
    IO_CONFIG = daft.io.IOConfig(s3=tos_config.to_s3_config())
    
    logger.info("视频字幕同步检查pipeline开始运行...")
    
    df = daft.from_glob_path(
        f"{input_s3_dir}/*.mp4",
        io_config=IO_CONFIG,
    )
    
    df = df.with_column(
        "video_tos_path",
        col("path").str.replace("s3://", "tos://")
    )
    df = df.with_column(
        "video_id",
        col("path").str.split("/").list.get(-1).str.replace(".mp4", "")
    )
    df = df.select("video_tos_path", "video_id")
    
    logger.info("视频文件加载完成: %d 条记录", df.count_rows())
    
    logger.info("开始视频音频抽取...")
    df = df.with_column(
        "audio_extraction_result",
        las_udf(
            VideoExtractAudio,
            construct_args={
                "output_tos_dir": audio_output_tos_dir,
                "output_audio_binary": True,
                "output_audio_array": False,
                "return_first_stream": True,       
                "output_format": "mp3",
                "output_sample_rate": 16000,
            },
            num_gpus=0,
            batch_size=2,
            concurrency=1,
        )(col("video_tos_path")),
    )
    df.collect()
    logger.info("视频音频抽取完成: %d 条记录", df.count_rows())

    df = df.with_columns({
        "audio_tos_path": col("audio_extraction_result").struct.get("audio_paths").list.get(0),
        "audio_binary": col("audio_extraction_result").struct.get("binaries").list.get(0),
        "original_sample_rate": col("audio_extraction_result").struct.get("original_audio_sampling_rates").list.get(0)
    })
    
    logger.info("开始音频URL预签名...")
    df = df.with_column(
        "audio_presigned_url",
        las_udf(
            PreSignUrlForTos,
            construct_args={"expire_seconds": 3600},
        )(col("audio_tos_path")),
    )
    df.collect()
    logger.info("音频URL预签名完成: %d 条记录", df.count_rows())
    
    logger.info("开始音频ASR识别...")
    appid = os.getenv("OPENSPEECH_APPID")
    token = os.getenv("OPENSPEECH_TOKEN")
    
    if not appid or not token:
        logger.error("缺少OPENSPEECH_APPID或OPENSPEECH_TOKEN环境变量")
        return
    
    df = df.with_column(
        "asr_result",
        las_udf(
            AudioAsrDoubao,
            construct_args={
                "appid": appid,
                "token": token,
                "uid": "video_subtitle_sync",
                "enable_speaker_info": True,
                "enable_punc": True,
                "enable_ddc": True,
                "poll_interval": 10,
                "num_coroutines": 1,
            },
            num_gpus=0,
            batch_size=1,
            concurrency=1,
        )(col("audio_presigned_url")),
    )
    df.collect()
    logger.info("音频ASR识别完成: %d 条记录", df.count_rows())
    
    df = df.with_columns({
        "asr_text_simple": col("asr_result").struct.get("asr_result_simple"),
        "asr_text_raw": col("asr_result").struct.get("asr_result_raw"),
        "asr_text_content": col("asr_result").struct.get("asr_result_text")
    })
    
    logger.info("开始ASR文本结构化解析...")
    df = df.with_column(
        "asr_segments_structured",
        las_udf(AsrTextParser)(col("asr_text_simple")),
    )
    df.collect()
    logger.info("ASR文本结构化解析完成: %d 条记录", df.count_rows())
    
    logger.info("开始生成VLM提示词...")
    df = df.with_column(
        "vlm_prompt",
        las_udf(VlmPromptGenerator)(col("asr_segments_structured")),
    )
    df.collect()
    logger.info("VLM提示词生成完成: %d 条记录", df.count_rows())
    
    logger.info("开始视频字幕同步分析...")
    
    df = df.with_column(
        "vlm_analysis_struct",
        las_udf(
            ArkLLMThinkingVision,
            construct_args={
                "model": "doubao-1.5-thinking-vision-pro",
                "version":"250428",
                "multimodal_type": "video",
                "inference_type": "online",
                "source_type": "url",
                "video_format": "mp4",
                "video_fps": 1.0,
                "max_tokens": 4000,
                "temperature": 0.1,
            },
            num_gpus=0,
            batch_size=1,
            concurrency=1,
        )(col("video_tos_path"), col("vlm_prompt")),
    )
    df.collect()
    logger.info("视频字幕同步分析完成: %d 条记录", df.count_rows())
    
    df = df.with_column(
        "vlm_analysis_result",
        col("vlm_analysis_struct").struct.get("llm_result")
    )
    
    df_clean = df.exclude("audio_extraction_result", "audio_binary", "asr_result", "asr_text_raw","audio_presigned_url","original_sample_rate","asr_segments_structured","vlm_prompt","vlm_analysis_struct")
    df_clean.show()

    timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
    output_tos_dir = "tos://tos_bucket/video_subtitle_sync/results/"
    output_s3_dir = output_tos_dir.replace("tos://", "s3://", 1)
    
    tos_config = TOSConfig.from_env()
    io_config = daft.io.IOConfig(s3=tos_config.to_s3_config())
    
    parquet_s3_path = f"{output_s3_dir}video_subtitle_sync_parquet_{timestamp}"
    
    df_clean.write_parquet(parquet_s3_path, io_config=io_config)
    
    logger.info("视频字幕同步结果已保存到TOS:")
    logger.info("Parquet: %s", output_tos_dir + f"video_subtitle_sync_parquet_{timestamp}")

if __name__ == "__main__":
    input_tos_dir = "tos://tos_bucket/video_subtitle_sync/test_video"
    audio_output_tos_dir = "tos://tos_bucket/video_subtitle_sync/video_audio_extracted/"
    
    run_pipeline(input_tos_dir, audio_output_tos_dir)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Code resources</strong>: The complete Pipeline script can be downloaded here: <a href="https://las-ai-cn-beijing.tos-cn-beijing.volces.com/qa/experience_center/video_subtitle_sync/video_subtitle_sync_pipeline_show.py">video_subtitle_sync_pipeline_show.py</a>.</div>



2. View the processing results and adjust the pipeline script based on the results.


After executing the pipeline, you will obtain a structured Parquet file containing the synchronization analysis results for each video.

**Sample log output:** 

```Bash
2025-08-19 05:58:10,INFO - 视频字幕同步检查 pipeline 开始运行...
2025-08-19 05:58:12,INFO - 视频文件加载完成: 3 条记录
2025-08-19 05:58:13,INFO - 开始视频音频抽取...
2025-08-19 05:58:45,INFO - 视频音频抽取完成。
2025-08-19 05:58:46,INFO - 开始音频ASR识别...
2025-08-19 06:00:10,INFO - 音频ASR识别完成。
2025-08-19 06:00:11,INFO - 开始ASR文本结构化解析...
2025-08-19 06:00:12,INFO - ASR文本结构化解析完成。
2025-08-19 06:00:13,INFO - 开始生成VLM提示词...
2025-08-19 06:00:14,INFO - VLM提示词生成完成。
2025-08-19 06:00:15,INFO - 开始视频字幕同步分析...
2025-08-19 06:05:20,INFO - 视频字幕同步分析完成。
2025-08-19 06:05:25,INFO - Pipeline 执行完毕！结果已保存至: tos://your-bucket/sync_results/sync_results_20250819_060525
```


After executing the Pipeline, in addition to the audio extraction results, you will also receive a structured Parquet file containing the **synchronization analysis results** for each video. The following is a sample of partially anonymized data:


|video_id |video_tos_path |asr_text_simple (speech recognition text and timestamps) |vlm_analysis_result (synchronization analysis summary) |
|---|---|---|---|
|751 |tos://.../test_video/751.mp4 |Speaker 1 0:00:00 0:00:03<br><br>Maybe china, I'll check...<br><br>&nbsp;<br><br>Speaker 1 0:00:04 0:00:05<br><br>I really want to check out japan... |Partial desynchronization (1 out of 5 segments)<br><br>Example issue: The on\-screen subtitle for the "Why japan?" segment appears with a 1\-second delay. |
|1160 |tos://.../test_video/1160.mp4 |Speaker 1 0:00:00 0:00:02<br><br>Wish you happiness every day. |Fully synchronized<br><br>All audio segments are accurately aligned with the on\-screen subtitles. |
|1172 |tos://.../test_video/1172.mp4 |Speaker 1 0:00:00 0:00:01<br><br>To be pink.<br><br>&nbsp;<br><br>Speaker 1 0:00:01 0:00:03<br><br>I don't know, I kind of feel... |Fully synchronized<br><br>All audio segments are accurately aligned with the on\-screen subtitles. |
|770 |tos://.../test_video/770.mp4 |Speaker 1 0:00:00 0:00:01<br><br>Easier with free Turkey...<br><br>&nbsp;<br><br>Speaker 2 0:00:04 0:00:08<br><br>This isn't another apology... |Significant desynchronization (4 out of 6 segments)<br><br>Issue types: Includes missing on\-screen subtitles, delayed appearance (0.8 seconds), and more. |
|703 |tos://.../test_video/703.mp4 |Speaker 2 0:00:01 0:00:07<br><br>Oh, and one more thing in Japan...<br><br>&nbsp;<br><br>Speaker 1 0:00:11 0:00:11<br><br>What? |Severe desynchronization (11 out of 13 segments)<br><br>Issue types: Includes missing on\-screen subtitles, delays, text splitting with mismatched timing, and various other issues. |
|710 |tos://.../test_video/710.mp4 |Speaker 2 0:00:01 0:00:03<br><br>I'd really like to travel more...<br><br>&nbsp;<br><br>Speaker 2 0:00:03 0:00:05<br><br>I want to go to Brazil. |Severe desynchronization (10 out of 12 segments)<br><br>Main issue: On\-screen subtitles generally have a delay of 0.6 to 1.6 seconds. |


<span id="461c8969"></span>
### **Step 2: Full\-scale task deployment**

After verifying that the processing pipeline works correctly on the development machine, you can package it as a custom image and create batch tasks in task management. This task will use this image to automatically and efficiently perform subtitle synchronization checks on large volumes of video data.
