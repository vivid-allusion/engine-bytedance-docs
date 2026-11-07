---
title: "Building high-quality speech-text pairs"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/Building_high-quality_speech-text_pairs"
---

The AI Data Lake service provides multimodal data preprocessing capabilities. By performing a series of advanced processing steps on raw audio data, it helps users automatically extract high\-quality speech\-text pairs (Speech\-Text Pairs) from massive amounts of in\-the\-wild audio data, transforming raw audio into high\-value, structured datasets that meet the training standards for large multimodal models. This article introduces the advantages and features of the speech\-text pair construction solution, explains its working principles, and guides you through building a complete audio processing task.

<span id="30f0dd5d"></span>
## Background information

The forefront of AI is rapidly evolving toward generalization and multimodality. In the audio domain, the technological wave has shifted from single tasks such as automatic speech recognition (ASR) or text\-to\-speech (TTS) to **Universal Speech Models, Expressive TTS, conversational AI**, and **music and sound effect generation**. Whether these models are **foundation models for speech** that need to understand hundreds of languages and dialects, or **voice cloning** applications designed to replicate the emotions and styles of humankind, their capabilities directly depend on the quality of the training data behind them. However, before massive in\-the\-wild audio data can become usable "model feedstock," three major challenges must be overcome:


* **Complex acoustic environments**: Audio may contain a variety of acoustic events, including **primary speaker voices, background voices, environmental noise, and background music**. For advanced models, the challenge is no longer just "noise reduction" but achieving precise "disentanglement" of sound sources—effectively separating or understanding other interfering elements while fully preserving the prosody and emotional details of the target voice.

* **Content interleaving**: In multi\-speaker conversations, meetings, or interview audio, the voices of different speakers often overlap and intertwine. For models that require **personalized speech synthesis** or **voice cloning**, even a few seconds of another person's voice mixed into the training data can cause the final synthesized voice to have mixed timbre or unclear pronunciation. Therefore, ensuring the “speaker purity” (说话人纯净度) of each training segment and performing millisecond\-level timestamp segmentation has become an indispensable prerequisite.

* **Diverse formats**: Audio files from different sources vary greatly in format, sampling rate, number of channels, and loudness.


The principle of "Garbage In, Garbage Out" is infinitely amplified in model training. Such mixed and disordered "dirty" data can, at best, lead to suboptimal model performance and mechanical\-sounding synthesized speech; at worst, it can cause the model to learn incorrect biases or even fail completely in critical applications. The construction of speech\-text pairs serves as a key step in audio data preprocessing, transforming these mixed and disordered raw audio files into clean, organized data pairs with precise text annotations, thereby laying a solid foundation for subsequent model training and applications.

<span id="6f15435b"></span>
### **Application scenarios**


* **Multimodal large model training data preparation**: Suitable for scenarios that require the construction of large\-scale, high\-quality speech\-text pair training corpora, providing high\-quality training data for multimodal large models such as text\-to\-speech (TTS), automatic speech recognition (ASR), audio\-video understanding, and more.

* **Speech content understanding and transcription**: Suitable for scenarios that require batch extraction of text content from massive amounts of audio, such as podcast transcription, meeting minutes generation, video subtitle production, online course content extraction, and more.

* **Speaker analysis and content organization**: Suitable for scenarios that require identification and separation of different speakers' voices, such as organizing multi\-person interview content, quality inspection of customer service conversations, extraction of script dialogues from film and television works, and more.


<span id="273fe9de"></span>
### **Key features**


* **Full\-process coverage**: Supports end\-to\-end processing from raw audio to final speech\-text pairs, covering all key stages such as audio normalization, vocal separation, language identification, speaker diarization, audio segmentation, and automatic speech recognition (ASR).

* **Multimodal processing capability**: Deeply integrates more than six core audio processing operators to provide comprehensive, multi\-dimensional processing and robustness for audio data.

* **Intelligent language identification**: High\-precision audio language identification (Audio LID) based on the Whisper model, providing accurate support for configuring independent ASR pipelines for different languages.

* **Efficient speaker diarization**: Utilizes advanced speaker diarization algorithms to accurately identify and segment speech segments from different speakers, effectively handling multi\-speaker conversation scenarios.

* **Bilingual ASR optimization**: Built\-in independently optimized ASR pipelines for Chinese and English audio; uses high\-performance Doubao ASR for Chinese and Whisper ASR for English, ensuring optimal recognition results for various types of audio data.

* **Distributed processing capability**: Based on the parallel and distributed scheduling mechanism of the Daft framework, enables high\-performance processing and transformation of terabyte\-scale audio data.

* **Flexible operator composition**: All audio processing steps are implemented using composable operators in LAS, supporting flexible adjustment, replacement, and extension of processing modules, and can be enhanced with user\-defined functions (UDFs).

* **GPU acceleration support**: Key compute\-intensive operators (such as source separation and ASR) support GPU acceleration, significantly improving the processing efficiency of large\-scale audio data.


<span id="b358b104"></span>
## Prerequisites


* Register a Volcano Engine account. For first\-time login, complete identity verification. For detailed instructions, see: [Account registration process](https://www.volcengine.com/docs/6261/64925).

* The [AI Data Lake Service](https://console.volcengine.com/las/region:las+cn-beijing/next/home?projectName=default) has been enabled.

* **General queue** and **compute queue** have been created. For detailed instructions, see: [Queue management](https://www.volcengine.com/docs/6492/1544041).

* A development machine has been created. For detailed instructions, see: [Create a development machine](https://www.volcengine.com/docs/6492/1738916). Relevant environment variables have been configured, especially `OPENSPEECH_APPID`, `OPENSPEECH_TOKEN`, and `OPENSPEECH_ENDPOINT` required for the Doubao ASR service.


<span id="5fefd906"></span>
## **How it works**

The speech\-text pair construction solution adopts a multi\-stage pipeline architecture, which includes core stages such as audio normalization, source separation, language identification, speaker diarization, audio segmentation, and speech recognition.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b57573e590b24579adcbfabc73a9a046~tplv-goo7wpa0wc-image.image) </span>

<span id="e3b0e60d"></span>
### **Core processing workflow**


|**Stage** |**Function description** |**Details** |**Operator list** |
|---|---|---|---|
|**Audio standardization** |Unify audio format, standardize sample rate, channel count, and loudness |Standardize audio files of different formats to consistent audio parameters: resample the sample rate to 16 kHz, convert channels to mono, set loudness to \-20 dBFS, and provide standardized input for subsequent processing |* AudioStandardization |
|**Audio source separation** |Separate vocals from mixed audio, remove background music and noise |Use the htdemucs deep learning model to separate clean vocal signals from mixed audio, effectively removing background music, environmental noise, and other non\-vocal interference, providing high\-quality vocal input for subsequent speaker diarization and speech recognition |* AudioSourceSeparation |
|**Language identification** |Identify the language type in the audio to provide a basis for subsequent ASR branches |Use the Whisper\-large model to identify the language of vocal audio, supporting recognition of multiple languages and improving accuracy in the ASR stage |* AudioLidWhisper |
|**Speaker diarization** |Identify speech segments of different speakers and generate timestamp information |Automatically identify different speakers in the audio using deep learning models, generating segment information that includes start time, end time, and speaker identification |* AudioSpeakerDiarization |
|**Audio segmentation** |Segment audio clips based on speaker diarization results |Precisely segment audio files based on speaker diarization timestamps to generate independent audio clips for each speaker |* AudioSplitByTimestamps |
|**Speech recognition** |Convert speech to text for each language branch to generate the final text content |Select the appropriate ASR operator for speech\-to\-text conversion based on the language identification result, and perform accurate speech recognition on each speaker's segmented audio clip<br><br><br>* Use Doubao ASR for Chinese audio,<br><br>* Use Whisper ASR for English audio |* AudioAsrDoubao<br><br>* AudioAsrWhisper |


<span id="c7fedf66"></span>
### Operator list


|**Stage** |**Operator name** |**Function description** |**Associated code function** |
|---|---|---|---|
|**1. Audio standardization** |AudioStandardization |Standardize any input audio file, converting it to a format with a 16kHz sampling rate, mono channel, and \-20dBFS loudness. This is a key preprocessing step to ensure consistent results for all subsequent model processing. |* stage_1_audio_standardization |
|**2. Source separation** |AudioSourceSeparation |Use deep learning models (such as `htdemucs`) to separate vocals from background sounds (music, noise, and more) in the audio. This operator outputs clean vocal audio, greatly improving the accuracy of subsequent speech recognition and speaker diarization. |* stage_2_audio_source_separation |
|**3. Language identification** |AudioLidWhisper |Use the Whisper model to perform language identification (LID) on the audio content. It can determine the primary language in the audio (such as Chinese `zh` or English `en`), providing a basis for selecting the most suitable ASR (Automatic Speech Recognition) model in subsequent steps. |* stage_3_audio_language_identification |
|**4. Speaker diarization** |AudioSpeakerDiarization |Analyze the audio to distinguish different speakers, and assign timestamps (start time, end time) and identity labels (such as `SPEAKER_00`, `SPEAKER_01`) to each speaker's speech segment. This process is also known as "speaker diarization." |* stage_4_audio_speaker_diarization |
|**4.5. Data expansion** |BuildTimestamps |This is a custom auxiliary operator in the code. Its function is to merge the separated `start` and `end` timestamp columns into the specific nested list format `[[start, end]]` required by the subsequent `AudioSplitByTimestamps` operator. |* stage_4_5_expand_speaker_segments |
|**5. Audio segmentation** |AudioSplitByTimestamps |Based on the timestamp information obtained from the previous speaker diarization step, precisely segment the complete audio file into multiple independent audio clips belonging to different speakers. |* stage_5_audio_split_by_speaker |
|**6. Speech recognition** |PreSignUrlForTos |This is a utility operator primarily used for the Chinese ASR branch. It converts the audio file path in Volcano Object Storage (TOS) into a publicly accessible URL with a time limit. This is because the Doubao ASR service needs to fetch audio files via a public URL. |* stage_6_audio_asr_by_language |
| |AudioAsrDoubao |[Chinese ASR branch] Calls the Volcano Engine Doubao speech recognition service. It receives a pre\-signed audio URL and returns high\-quality Chinese recognized text. |* stage_6_audio_asr_by_language |
| |AudioAsrWhisper |[English ASR branch] Uses OpenAI's Whisper model (in the code as `whisper-large-v3`) for speech recognition. It directly processes the segmented audio binary data and converts it into English text. |* stage_6_audio_asr_by_language |


<span id="20f1e346"></span>
## **Case study**

After complete pipeline processing, the original audio files, which may contain multiple types of sounds, are converted into a series of clean data pairs in the form of (audio segment, text).

**Original audio**: This document uses the [AISHELL-4](https://www.aishelltech.com/aishell_4) dataset, open\-sourced by ShellBee, as a demo to demonstrate speech\-to\-text in meeting scenarios.


* For dataset details, see [official website](https://www.aishelltech.com/aishell_4).

* HuggingFace: [For details, see the official website](https://huggingface.co/datasets/shenyunhang/AISHELL-4/tree/main/train_L/wav/20200706_L_R001S04C01).


Example:

<Attachment link="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/896df42401674a47a0a4fcad6d09918d~tplv-goo7wpa0wc-image.image" name="000000016.wav">000000016.wav</Attachment>


&nbsp;

**Processing result**: You can select files from here and store them in a TOS bucket. After completing the configuration in this document, you will obtain the demonstration result. For example, in line 13 of the sample file: `"asr_text":"我觉得咱们选址可以选在七里河附近，这边挨着水，这样的话咱们的水上设施供水能力就比较强，不用想，相对来说"`


* Build result:


```JSON
{"audio_path":"tos://xxx/xxx.wav","language_code":"zh","speaker":"SPEAKER_01","start":4.773,"end":6.241,"speaker_audio_url":"tos://xxx/xxx.wav","asr_text":"有多大？"}
{"audio_path":"tos://xxx/xxx.wav","language_code":"zh","speaker":"SPEAKER_00","start":31.081,"end":43.973,"speaker_audio_url":"tos://xxx/xxx.wav","asr_text":"但是但是你要考虑的话，就是像我们后勤部需要招大量的保安，他们可以都有当地的，咱们可以，这样的话可以给当地的居民带"}
{"audio_path":"tos://xxx/xxx.wav","language_code":"zh","speaker":"SPEAKER_03","start":16.754,"end":22.778,"speaker_audio_url":"tos://xxx/xxx.wav","asr_text":"然后那边空地也比较多，咱们这样的话，空间比较大。"}
{"audio_path":"tos://xxx/xxx.wav","language_code":"zh","speaker":"SPEAKER_02","start":26.153,"end":28.786,"speaker_audio_url":"tos://xxx/xxx.wav","asr_text":"那边也存在欺负或者"}
{"audio_path":"tos://xxx/xxx.wav","language_code":"zh","speaker":"SPEAKER_00","start":7.017,"end":11.438,"speaker_audio_url":"tos://xxx/xxx.wav","asr_text":"对，这有最起码一个这个，然后才知道里面去买什么设施。"}
{"audio_path":"tos://xxx/xxx.wav","language_code":"zh","speaker":"SPEAKER_01","start":15.927,"end":21.007,"speaker_audio_url":"tos://xxx/xxx.wav","asr_text":"咱们可以建这个水上游乐园，咱们可以是分成几个区化。"}
{"audio_path":"tos://xxx/xxx.wav","language_code":"zh","speaker":"SPEAKER_01","start":12.248,"end":14.965,"speaker_audio_url":"tos://xxx/xxx.wav","asr_text":"出现管道的费用要少一些。"}
{"audio_path":"tos://xxx/xxx.wav","language_code":"zh","speaker":"SPEAKER_00","start":0.031,"end":4.435,"speaker_audio_url":"tos://xxx/xxx.wav","asr_text":"咱一会再说这个，刚才说，说到选址方面的问题。"}
{"audio_path":"tos://xxx/xxx.wav","language_code":"zh","speaker":"SPEAKER_00","start":0.031,"end":5.819,"speaker_audio_url":"tos://xxx/xxx.wav","asr_text":"先说一下这个游乐场。"}
{"audio_path":"tos://xxx/xxx.wav","language_code":"zh","speaker":"SPEAKER_00","start":0.031,"end":9.143,"speaker_audio_url":"tos://xxx/xxx.wav","asr_text":"想听一下各位对这个创业，这个未来创业有什么想法？"}
{"audio_path":"tos://xxx/xxx.wav","language_code":"zh","speaker":"SPEAKER_01","start":21.58,"end":25.63,"speaker_audio_url":"tos://xxx/xxx.wav","asr_text":"一部分是基础基础于这个，就比如说"}
{"audio_path":"tos://xxx/xxx.wav","language_code":"zh","speaker":"SPEAKER_01","start":11.438,"end":14.932,"speaker_audio_url":"tos://xxx/xxx.wav","asr_text":"咱们可以建，现在夏天了。"}
{"audio_path":"tos://xxx/xxx.wav","language_code":"zh","speaker":"SPEAKER_01","start":0.031,"end":11.573,"speaker_audio_url":"tos://xxx/xxx.wav","asr_text":"我觉得咱们选址可以选在七里河附近，这边挨着水，这样的话咱们的水上设施供水能力就比较强，不用想，相对来说"}
{"audio_path":"tos://xxx/xxx.wav","language_code":"zh","speaker":"SPEAKER_00","start":0.031,"end":5.87,"speaker_audio_url":"tos://xxx/xxx.wav","asr_text":"这游乐场多大？有没有首先一个定义，游乐场咱们要建大概多大？"}
{"audio_path":"tos://xxx/xxx.wav","language_code":"zh","speaker":"SPEAKER_01","start":44.193,"end":45.475,"speaker_audio_url":"tos://xxx/xxx.wav","asr_text":"就这个机会。"}
```


<span id="61438383"></span>
## **Development and debugging**

The development machine is a professional development environment tailored by the AI Data Lake service for algorithm developers. It features high efficiency and convenience, enabling developers to quickly start writing, debugging, and running data processing tasks. On the LAS development machine, developers use the Daft distributed computing framework to write a complete text cleaning pipeline.

You can use a terminal or IDE such as VSCode on your local machine or other devices to connect to the development machine remotely via direct SSH connection, and quickly start writing, debugging, and running data processing tasks. For operational guidance, see [Remote connection to development machine](https://www.volcengine.com/docs/6492/1747863).

<span id="dd2a0ee5"></span>
### **Code reference**

On the LAS development machine, developers use the Daft framework to write a complete audio processing pipeline. This pipeline logically connects all operators from audio normalization to final speech recognition in a clear sequence.

The following is a complete code example showing how to build this pipeline:

```Python
import logging
from pathlib import Path

import torch
import daft
import os
from daft import col, lit

from daft.las.functions.audio.audio_standardization import AudioStandardization
from daft.las.functions.audio.audio_source_separation import AudioSourceSeparation
from daft.las.functions.audio.audio_speaker_diarization import AudioSpeakerDiarization
from daft.las.functions.audio.audio_split_by_timestamps import AudioSplitByTimestamps
from daft.las.functions.audio.audio_lid_whisper import AudioLidWhisper
from daft.las.functions.audio.audio_asr_doubao import AudioAsrDoubao
from daft.las.functions.audio.audio_asr_whisper import AudioAsrWhisper
from daft.las.functions.text.pre_sign_url_for_tos import PreSignUrlForTos
from daft.las.functions.udf import las_udf
from daft.las.io.tos import TOSConfig
from io import StringIO

log_capture = StringIO()
log_handler = logging.StreamHandler(log_capture)
log_handler.setLevel(logging.ERROR)
log_formatter = logging.Formatter("%(asctime)s - %(levelname)s - %(message)s")
log_handler.setFormatter(log_formatter)

logging.basicConfig(level=logging.INFO, format="%(asctime)s - %(levelname)s - %(message)s")
logger = logging.getLogger(__name__)
logger.addHandler(log_handler)

logging.getLogger("daft").setLevel(logging.ERROR)
logging.getLogger("pyannote").setLevel(logging.ERROR)
logging.getLogger("speechbrain").setLevel(logging.ERROR)

def stage_1_audio_standardization(df: daft.DataFrame) -> daft.DataFrame:
    """
    阶段1: 音频标准化
    
    对音频进行标准化处理，统一采样率、声道数和响度。
    使用AudioStandardization算子，目标16kHz单声道-20dBFS。
    
    Args:
        df: 包含audio_path列的DataFrame
        
    Returns:
        增加standardized_audio列的DataFrame
    """
    logger.info("阶段1: 音频标准化")
    
    df = df.with_column(
        "standardized_audio",
        las_udf(
            AudioStandardization,
            construct_args={
                "target_sr": 16000,
                "target_channels": 1,
                "target_dbfs": -20.0,
                "target_gain_range": [-3.0, 3.0],
                "num_coroutines": 2,
            },
            num_gpus=0,
            batch_size=1,
            concurrency=1,
        )(col("audio_path")),
    )
    df.collect()

    return df

def stage_2_audio_source_separation(df: daft.DataFrame, model_path: str) -> daft.DataFrame:
    """
    阶段2: 音源分离
    
    从混合音频中分离出人声，去除背景音乐和噪声。
    使用AudioSourceSeparation算子和htdemucs模型进行GPU加速处理。
    
    Args:
        df: 包含standardized_audio列的DataFrame
        
    Returns:
        增加vocal_audio列的DataFrame
    """
    logger.info("阶段2: 音源分离")
    
    df = df.with_column(
        "vocal_audio",
        las_udf(
            AudioSourceSeparation,
            construct_args={
                "model_path": model_path,
                "chunk_batch_size": 4,
                "device": "cuda" if torch.cuda.is_available() else "cpu",
                "num_coroutines": 1,
            },
            num_gpus=1 if torch.cuda.is_available() else 0,
            batch_size=1,
            concurrency=1,
        )(col("standardized_audio")),
    )
    df.collect()

    return df

def stage_3_audio_language_identification(df: daft.DataFrame, model_path: str) -> daft.DataFrame:
    """
    阶段3: 语言识别
    
    使用Whisper模型识别音频中的语言类型。
    为后续按语言分支的ASR处理提供依据。
    
    Args:
        df: 包含vocal_audio列的DataFrame
        model_path: 模型路径
        
    Returns:
        增加language_code列和language_name列的DataFrame
    """
    logger.info("阶段3: 语言识别")
    
    df = df.with_column(
        "language_result",
        las_udf(
            AudioLidWhisper,
            construct_args={
                "model_path": model_path,
                "model_name": "iic/speech_whisper-large_lid_multilingual_pytorch",
                "model_version": "v2.0.4",
                "rank": 0,
            },
            num_gpus=1,
            batch_size=1,
            concurrency=1,
        )(col("vocal_audio")),
    )
    
    df = df.with_column("language_code", col("language_result").struct.get("language_code"))
    df = df.with_column("language_name", col("language_result").struct.get("language_code_full_name"))
    df.collect()

    return df

def stage_4_audio_speaker_diarization(df: daft.DataFrame, model_path: str) -> daft.DataFrame:
    """
    阶段4: 说话人分离
    
    使用深度学习模型进行多说话人语音分离。
    识别不同说话人的语音段落和时间范围。
    
    Args:
        df: 包含vocal_audio列的DataFrame
        model_path: 模型路径
        
    Returns:
        增加speaker_segments列的DataFrame
    """
    logger.info("阶段4: 说话人分离")
    
    df = df.with_column(
        "speaker_segments",
        las_udf(
            AudioSpeakerDiarization,
            construct_args={
                "model_path": model_path,
                "rank": 0,
            },
            num_gpus=1 if torch.cuda.is_available() else 0,
            batch_size=1,
            concurrency=1,
        )(col("vocal_audio")),
    )
    df.collect()
    
    return df

def stage_4_5_expand_speaker_segments(df: daft.DataFrame) -> daft.DataFrame:
    """
    阶段4.5: 说话人分段数据展开
    
    将说话人分段的结构化数据展开为单独的行。
    使用explode操作和自定义BuildTimestamps算子生成时间戳格式。
    
    Args:
        df: 包含speaker_segments列的DataFrame
        
    Returns:
        展开后的DataFrame，增加speaker、start、end、timestamps列
    """
    import pyarrow as pa
    from daft import col
    from daft.las.functions.udf import las_udf
    from daft.las.functions.types import Operator

    class BuildTimestamps(Operator):
        """自定义 Operator，将start和end合成 [[start, end]] 形式"""

        def transform(self, start: pa.Array, end: pa.Array) -> pa.Array:
            result = []
            for s, e in zip(start.to_pylist(), end.to_pylist()):
                result.append([[s, e]])
            return pa.array(result, type=self.__return_column_type__())

        @staticmethod
        def __return_column_type__() -> pa.DataType:
            return pa.list_(pa.list_(pa.float64()))

    build_timestamps_udf = las_udf(BuildTimestamps)

    df = df.explode("speaker_segments")
    df = df.with_column("speaker", col("speaker_segments").struct.get("speaker"))
    df = df.with_column("start", col("speaker_segments").struct.get("start"))
    df = df.with_column("end", col("speaker_segments").struct.get("end"))

    df = df.where((col("end") - col("start")) >= 1.0)

    df = df.with_column("timestamps", build_timestamps_udf(col("start"), col("end")))
    df.collect()

    return df

def stage_5_audio_split_by_speaker(df: daft.DataFrame, output_dir: str) -> daft.DataFrame:
    """
    阶段5: 按说话人切分音频
    
    根据说话人分离的时间戳精确切分音频文件。
    使用AudioSplitByTimestamps算子进行精确切分。
    
    Args:
        df: 包含audio_path和timestamps列的DataFrame
        output_dir: 输出目录
        
    Returns:
        增加speaker_audio_splits列的DataFrame
    """
    logger.info("阶段4: 按说话人切分音频")

    df = df.with_column("dummy_tos_uri", lit(None))
    df = df.with_column("audio_format", lit("wav"))
    
    df = df.with_column(
        "speaker_audio_splits",
        las_udf(
            AudioSplitByTimestamps,
            construct_args={
                "output_tos_dir": output_dir,
                "output_segments_binary": True,
                "output_audio_format": True,
            },
            num_gpus=0,
            batch_size=1,
            concurrency=1,
        )(col("timestamps"), col("dummy_tos_uri") ,col("vocal_audio"),col("audio_format")),
    )
    df.collect()

    return df

def stage_6_audio_asr_by_language(df: daft.DataFrame, model_path: str) -> daft.DataFrame:
    """
    阶段6: 基于语言分支的语音识别
    
    根据语言识别结果选择合适的ASR算子进行语音转文字。
    中文使用豆包ASR，英文使用Whisper ASR。
    
    Args:
        df: 包含speaker_audio_splits和language_code列的DataFrame
        model_path: 模型路径
        
    Returns:
        增加asr_text列的DataFrame
    """
    logger.info("阶段6: 基于语言分支的语音识别")
    
    df_chinese = df.where(col("language_code") == "zh")
    df_english = df.where(col("language_code") == "en")
    
    if len(df_chinese.collect()) > 0:
        logger.info(f"处理 {len(df_chinese.collect())} 条中文音频数据")
        
        df_chinese = df_chinese.with_column(
            "speaker_audio_url",
            col("speaker_audio_splits").struct.get("segments").list.get(0)
        )
        
        df_chinese = df_chinese.with_column(
            "speaker_audio_presigned_url",
            las_udf(
                PreSignUrlForTos,
                construct_args={
                    "expire_seconds": 3600,
                },
            )(col("speaker_audio_url")),
        )
        
        logger.info("开始豆包ASR识别...")
        df_chinese = df_chinese.with_column(
            "asr_result_zh",
            las_udf(
                AudioAsrDoubao,
                construct_args={
                    "appid": os.getenv("OPENSPEECH_APPID"),
                    "token": os.getenv("OPENSPEECH_TOKEN"),
                    "uid": "speech_text_pairs_pipeline",
                    "enable_punc": True,
                    "enable_ddc": True,
                    "enable_speaker_info": False,
                    "enable_itn": True,
                    "poll_interval": 15,
                    "num_coroutines": 1,
                },
                num_gpus=0,
                batch_size=4,
                concurrency=1,
            )(col("speaker_audio_presigned_url")),
        )
        
        df_chinese = df_chinese.with_column(
            "asr_text", 
            col("asr_result_zh").struct.get("asr_result_text")
        )
        df_chinese = df_chinese.exclude("asr_result_zh", "speaker_audio_presigned_url")
        logger.info("豆包ASR识别完成")
    
    if len(df_english.collect()) > 0:
        logger.info(f"处理 {len(df_english.collect())} 条英文音频数据")
        
        df_english = df_english.with_column(
            "speaker_audio_url",
            col("speaker_audio_splits").struct.get("segments").list.get(0)
        )
        
        df_english = df_english.with_column(
            "speaker_audio_binary",
            col("speaker_audio_splits").struct.get("binaries").list.get(0)
        )
        
        logger.info("开始Whisper ASR识别...")
        df_english = df_english.with_column(
            "asr_result_en",
            las_udf(
                AudioAsrWhisper,
                construct_args={
                    "audio_src_type": "audio_binary",
                    "model_path": model_path,
                    "model_name": "openai/whisper-large-v3",
                    "dtype": "bfloat16",
                    "source_language": "english",
                    "translate_to_english": False,
                    "condition_on_prev_tokens": True,
                    "compression_ratio_threshold": 1.35,
                    "temperature": 0.5,
                    "logprob_threshold": -1.0,
                    "batch_size": 10,
                    "rank": 0,
                },
                num_gpus=1,
                batch_size=1,
                concurrency=1,
            )(col("speaker_audio_binary")),
        )
        
        df_english = df_english.with_column(
            "asr_text", 
            col("asr_result_en").struct.get("asr_result")
        )
        df_english = df_english.exclude("asr_result_en", "speaker_audio_binary")
        logger.info("Whisper ASR识别完成")
    
    if len(df_chinese.collect()) > 0 and len(df_english.collect()) > 0:
        df = df_chinese.concat(df_english)
    elif len(df_chinese.collect()) > 0:
        df = df_chinese
    elif len(df_english.collect()) > 0:
        df = df_english
    else:
        df = df.with_column("asr_text", lit(None))
    
    df.collect()
    return df

def run_speech_text_pairs_pipeline(input_dir: str, output_dir: str) -> None:
    """主函数 - 按阶段执行语音-文本对构建解决方案demo"""
    
    try:
        input_s3_dir = input_dir.replace("tos://", "s3://", 1)
        tos_config = TOSConfig.from_env()
        IO_CONFIG = daft.io.IOConfig(s3=tos_config.to_s3_config())
        
        audio_extensions = ["*.wav", "*.mp3", "*.flac", "*.m4a", "*.aac"]
        dfs = []
        
        for ext in audio_extensions:
            try:
                df_ext = daft.from_glob_path(f"{input_s3_dir}/{ext}", io_config=IO_CONFIG)
                if len(df_ext.collect()) > 0:
                    dfs.append(df_ext)
            except:
                continue
        
        if not dfs:
            logger.warning(f"未找到音频文件: {input_dir}")
            return
        
        df = dfs[0]
        for df_ext in dfs[1:]:
            df = df.concat(df_ext)
        
        df = df.with_column(
            "audio_path",
            col("path").str.replace("s3://", "tos://")
        )
        df = df.select("audio_path")
        
        logger.info(f"找到音频文件: {len(df.collect())} 个")
        logger.info(f"初始数据: {len(df.collect())} 条记录")
        
        model_path = "/opt/las/models"
        
        # Step 1: Audio normalization - standardize sampling rate, number of channels, and loudness
        df = stage_1_audio_standardization(df)
        
        # Step 2: Source separation - extract vocals from mixed audio
        df = stage_2_audio_source_separation(df, model_path)
        
        # Step 3: Language identification - identify the language type in the audio
        df = stage_3_audio_language_identification(df, model_path)
        
        # Step 4: Speaker diarization - identify speech segments from different speakers
        df = stage_4_audio_speaker_diarization(df, model_path)
        
        # Step 4.5: Speaker segment data expansion - expand structured data into individual rows
        df = stage_4_5_expand_speaker_segments(df)
        
        # Step 5: Segment audio by speaker - split audio based on speaker diarization results
        df = stage_5_audio_split_by_speaker(df, output_dir)
        
        # Step 6: Speech recognition - perform speech-to-text by language branch
        df = stage_6_audio_asr_by_language(df, model_path)
        df = df.exclude("standardized_audio","vocal_audio","language_result","language_name","speaker_segments","dummy_tos_uri","timestamps","audio_format","speaker_audio_splits")
        df.show()
        
        logger.info("Pipeline 阶段1-6执行完成!")
        
    except Exception as e:
        logger.error(f"Pipeline执行失败: {e}")
        raise

if __name__ == "__main__":
    input_dir = "tos://tos_bucket/speech_text_pairs/test_audio"
    output_dir = "tos://tos_bucket/speech_text_pairs/audio_split_by_timestamps/"
    
    run_speech_text_pairs_pipeline(input_dir, output_dir)
```


<span id="ff127496"></span>
### Processing result

The following is a sample table of processing results:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/63548046201b4c8e9bfffc63e7662739~tplv-goo7wpa0wc-image.image" width="3478px" /></div>


<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bf65710cec7459abe8ee48bb920277f~tplv-goo7wpa0wc-image.image" width="3128px" /></div>


<span id="17138448"></span>
## **Full audio processing**

After the processing pipeline is validated with sample data on the development machine, it is finalized as a custom image. Create and configure a batch task in LAS task management, which will use this image to automatically and efficiently process large\-scale raw audio data, completing the construction of high\-quality speech\-text pairs.

With this solution, you can build an efficient and reliable data cleaning pipeline for pretraining large language models, providing high\-quality corpus support for model training. For more technical details or customized requirements, please contact the technical support team.
