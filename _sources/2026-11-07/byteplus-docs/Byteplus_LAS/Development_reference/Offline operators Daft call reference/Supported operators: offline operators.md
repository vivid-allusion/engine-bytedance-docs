---
title: "Supported operators: offline operators"
product: "Lake AI Service"
product_code: "Byteplus_LAS"
source: "https://docs.byteplus.com/en/docs/Byteplus_LAS/offline-operators"
---

<span id="image"></span>
# Image

<span id="image-ocr"></span>
## Image OCR


|Operator name |Usage |Operator overview |
|---|---|---|
|[Image OCR (EasyOCR)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Image-OCR-EasyOCR) |* offline |* A multilingual OCR recognition component based on EasyOCR, supporting text detection and recognition in mixed Chinese and English scenarios.<br><br>* Core features:<br><br>   * Supports recognition of over 100 languages (requires configuration of corresponding language models)<br><br>   * Input format compatibility:<br><br>      * TOS URL<br><br>      * Base64 encoding<br><br>      * Binary stream<br><br>      * Numpy array<br><br>   * Performance optimization:<br><br>      * GPU\-accelerated inference<br><br>      * Model quantization (enabled by default)<br><br>      * Batch processing optimization |


<span id="image-processing"></span>
## Image Processing


|Operator name |Usage |Operator overview |
|---|---|---|
|[Image Resampling](https://docs.byteplus.com/en/docs/Byteplus_LAS/Image_Resampling) |* offline |* Image resampling processor, supporting multiple interpolation algorithms and output formats.<br><br>* Core features:<br><br>   * Offers 4 professional\-grade interpolation algorithms:<br><br>      * Nearest\-neighbor interpolation (nearest) \- Fastest speed, suitable for pixel art<br><br>      * Bilinear interpolation (bilinear) \- Balances speed and quality<br><br>      * Bicubic interpolation (bicubic) \- High\-precision smooth processing<br><br>      * Lanczos interpolation (lanczos) \- Best anti\-aliasing, suitable for photos<br><br>   * Multi\-format input support:<br><br>      * URL address (image_url)<br><br>      * Base64 encoding (image_base64)<br><br>      * Binary stream (image_binary)<br><br>   * Dual output modes:<br><br>      * Direct Base64 encoding output<br><br>      * TOS persistent storage |
|[Image Aesthetic Score](https://docs.byteplus.com/en/docs/Byteplus_LAS/Image_Aesthetic_Score) |* offline |* Image Aesthetic Score Processor, intelligently evaluates the aesthetic quality and composition effect of images<br><br>* Core features:<br><br>   * Aesthetic Scoring: Professionally evaluates the aesthetic quality of input images<br><br>   * Composition Analysis: Analyzes image composition based on visual perception theory<br><br>   * Standardized Output: Scores are normalized to the range of 0\-1 for easy subsequent processing<br><br>   * Batch Processing: Supports efficient batch image scoring<br><br>   * Multi\-format Support: Compatible with multiple image input formats |


<span id="image-vectorization"></span>
## Image Vectorization


|Operator name |Usage |Operator overview |
|---|---|---|
|[Image Embedding (ViT Series Models)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Image-Embedding-ViT) |* offline |* ViT Image Semantic Embedding Processor, suitable for scenarios like image similarity search and content retrieval.<br><br>* Core features:<br><br>   * Multi\-model support:<br><br>      * Google official ViT models<br><br>      * Meta DINOv2 visual models<br><br>   * Feature extraction modes:<br><br>      * CLS Token embedding vector<br><br>      * Global average pooling<br><br>   * Input format compatibility:<br><br>      * URL<br><br>      * Base64 encoding<br><br>      * Binary stream<br><br>   * Performance optimizations:<br><br>      * FP16 inference acceleration<br><br>      * Multi\-GPU parallel computing |


<span id="audio"></span>
# Audio

<span id="audio-generation"></span>
## Audio Generation


|Operator name |Usage |Operator overview |
|---|---|---|
|[Text-to-Speech (Doubao Speech Large Model)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Text-to-Speech-doubao) |* offline |* Speech Synthesis Module \- Text\-to\-Audio Solution Based on Doubao Speech Large Model<br><br>* Core features:<br><br>   * Integrate with the speech synthesis interface of Volcano Engine's large model (`volc.tts`)<br><br>   * Support multiple parameter configurations such as voice type, emotion, encoding format, speech rate, sampling rate, etc.<br><br>   * Process multiple text inputs concurrently, output Base64\-encoded audio and original responses<br><br>   * Suitable for scenarios like voice broadcasting, virtual human voice generation, listening content production, etc. |


<span id="audio-preprocessing"></span>
## Audio Preprocessing


|Operator name |Usage |Operator overview |
|---|---|---|
|[Audio Format Standardization](https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_Format_Standardization) |* offline |* Audio Standardization Module \- Unify audio to specified formats (sampling rate, channel, loudness, etc.)<br><br>* Core features:<br><br>   * Supports sampling rate resampling<br><br>   * Supports channel unification (e.g., convert to mono)<br><br>   * Supports loudness normalization (target dBFS with limited gain range)<br><br>   * Default input/output audio is in bytes format |


<span id="audio-processing"></span>
## Audio Processing


|Operator name |Usage |Operator overview |
|---|---|---|
|[Audio Duration Calculation](https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_Duration_Calculation) |* offline |* Audio Duration Analysis Processor: accurately calculates audio content duration<br><br>* Core features:<br><br>   * Accurately calculates audio duration (second\-level precision)<br><br>   * Supports local files, TOS storage, and binary data<br><br>   * Based on the librosa professional audio processing library |
|[Audio File Size Calculation](https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_File_Size_Calculation) |* offline |* Audio file metadata analysis processor, accurately calculates file size<br><br>* Core features:<br><br>   * Accurately calculates audio file byte size<br><br>   * Supports local files and TOS storage<br><br>   * Lightweight and efficient, suitable for batch processing |
|[Audio Segment Segmentation (with Timestamps)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio-Segment-Segmentation-Timestamps) |* offline |* Audio timestamp segmentation processor, supporting precise segment extraction.<br><br>* Core features:<br><br>   * Accurately split audio based on timestamps<br><br>   * Supports multiple input formats:<br><br>   * Local file path<br><br>   * TOS storage path<br><br>   * Binary data stream<br><br>   * Supports binary output of segments or TOS storage |
|[Audio segment splitting (by duration)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio-segment-splitting-duration) |* offline |* Split audio by duration, supporting splitting audio clips into fixed\-length segments<br><br>* Core features:<br><br>   * Split audio into multiple segments according to the specified duration<br><br>   * Support multiple input formats:<br><br>   * Local file path<br><br>   * TOS/S3 storage path<br><br>   * Binary data stream<br><br>   * Support binary output of segments or storage to TOS<br><br>   * Support filtering segments by minimum duration |
|[Audio Silence Detection](https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_Silence_Detection) |* offline |* Audio Silence Detection Processor, intelligently identifies whether audio is completely silent<br><br>* Core features:<br><br>   * Silence Detection: Analyzes the entire audio file to determine if it is silent<br><br>   * Configurable Threshold: Supports custom sensitivity thresholds (dB) for silence detection<br><br>   * Efficient Processing: Optimized volume analysis algorithm for fast processing speed<br><br>   * Accurate Analysis: Determines silence status using professional volume detection technology<br><br>   * Supports Local Files, HTTP/HTTPS URLs, and TOS/S3 Storage |
|[Audio Filter Processing](https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_Filter_Processing) |* offline |* Audio filter processor, a flexible audio effect application based on FFmpeg.<br><br>* Core features:<br><br>   * Apply common audio filters (volume, highpass, lowpass, bass, treble, aecho, etc.) via FFmpeg<br><br>   * Supports automatic download and processing of local paths and TOS/S3 remote paths<br><br>   * Supports uploading processing results to TOS or returning binary results |
|[Audio to MP3](https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_to_MP3) |* offline |* Audio format conversion processor that converts various audio formats to MP3<br><br>* Core features:<br><br>   * Supports converting multiple audio formats to MP3<br><br>   * Customizable audio quality and encoding parameters<br><br>   * Supports fine control of audio sample rate and bit rate<br><br>   * Intelligent audio track selection (All/Auto/First)<br><br>   * Supports local files, HTTP/HTTPS URLs, and TOS/S3 storage |
|[Audio Quality Score (DNSMOS)](https://docs.byteplus.com/en/docs/Byteplus_LAS/AudioQualityScore-DNSMOS) |* offline |* Audio Quality Scoring Module \- Evaluate Audio Quality Using DNSMOS Model<br><br>* Core features:<br><br>   * Evaluate audio quality using the DNSMOS (Deep Noise Suppression Mean Opinion Score) model<br><br>   * Provide scores in three dimensions: Overall Quality (OVRL), Signal Quality (SIG), and Background Noise (BAK)<br><br>   * Scores range from 1 to 5, with higher scores indicating better audio quality<br><br>   * Support automatic sample rate conversion and audio preprocessing<br><br>   * Applicable to scenarios such as speech quality evaluation, audio filtering, and quality control |
|[Audio Format Conversion](https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_Format_Conversion) |* offline |* Universal audio format conversion processor that supports conversion to any audio format<br><br>* Core features:<br><br>   * Supports conversion to multiple audio formats (MP3, WAV, FLAC, AAC, OGG, etc.)<br><br>   * Customizable audio sample rate<br><br>   * Intelligent audio track selection (all/auto/first)<br><br>   * Supports format\-specific parameters via extra_params<br><br>   * Supports local files, HTTP/HTTPS URLs, and TOS/S3 storage |
|[Audio Signal-to-Noise Ratio Calculation](https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_Signal-to-Noise_Ratio_Calculation) |* offline |* Audio Signal\-to\-Noise Ratio (SNR) Calculator, which performs signal\-noise separation based on Non\-negative Matrix Factorization (NMF).<br><br>* Core features:<br><br>   * Perform STFT spectrum analysis on audio;<br><br>   * Use NMF to decompose the spectrum into signal and noise components;<br><br>   * Calculate SNR (in dB) based on the energy ratio between the reconstructed time\-domain signal and the estimated noise. |


<span id="audio-recognition"></span>
## Audio Recognition


|Operator name |Usage |Operator overview |
|---|---|---|
|[Speech to Text (FireRed)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Speech-to-Text-FireRed) |* offline |* Speech Recognition Module \- A Multilingual Speech\-to\-Text Solution Based on FireRed ASR Models<br><br>* Core features:<br><br>   * Multilingual Recognition: Supports Chinese, English, and Chinese dialects<br><br>   * Multiple Model Options: Supports various models including AED and LLM models<br><br>   * Audio Type: Supports mono\-channel WAV audio files with 16K sampling rate |
|[Speaker Verification (ERes2Net)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Speaker-Verification-ERes2Net) |* offline |* AudioSpeakerVerificationEres2net Audio Speaker Verification Processor<br><br>* Core features:<br><br>   * Speaker verification: Determine if two audio clips belong to the same speaker and output a similarity score<br><br>   * Multi\-source audio support: Supports multiple audio input types including local files, URLs, object storage, base64, and binary<br><br>   * Batch processing: Supports efficient verification and exception handling for batch audio pairs |
|[Voice Activity Detection (Silero Model)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Voice-Activity-Detection) |* offline |* Core features:<br><br>   * Speech endpoint detection: Automatically identify the start and end times of speech segments in audio, enabling accurate segmentation between speech and silence.<br><br>   * Batch processing: Support efficient endpoint detection for large volumes of audio data.<br><br>   * Multi\-format input: Compatible with various audio input methods such as raw binary, Base64 encoding, TOS/HTTP links.<br><br>   * GPU acceleration: Supports high\-performance inference in GPU environments.<br><br>   * Strong versatility: Performs excellently when processing audio from different domains with various background noises and quality levels. |
|[Speech-to-Text (Whisper Series Models)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Speech-to-Text-Whisper) |* offline |* Speech Recognition Module \- A Multilingual Speech\-to\-Text Solution Based on the Whisper Model<br><br>* Core features:<br><br>   * Multilingual Recognition: Supports mainstream languages such as Chinese and English<br><br>   * Speech Translation: Can translate recognition results into English |
|[Voice Activity Detection (FSMN Model)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Voice-Activity-Detection-FSMN) |* offline |* Voice Activity Detection Module \- Efficient Audio Segmentation Solution Based on FSMN VAD<br><br>* Core features:<br><br>   * Voice Activity Detection: Automatically identifies the start and end times of speech segments in audio, enabling precise segmentation between speech and silence.<br><br>   * Batch Processing: Supports efficient endpoint detection for large volumes of audio data.<br><br>   * Multi\-format Input: Compatible with multiple audio input methods including raw binary, Base64 encoding, TOS/HTTP links, etc.<br><br>   * GPU Acceleration: Supports high\-performance inference in GPU environments. |
|[Audio Multilingual Recognition (whisper)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio-Multilingual-Recognition-whisper) |* offline |* AudioLidWhisper Audio Language Identification Processor<br><br>* Core features:<br><br>   * Audio decoding: Supports multiple audio formats → 16kHz waveform data<br><br>   * Language detection: Identifies dozens of language codes based on the Whisper\-large model<br><br>   * Full name mapping: Automatically converts language codes to full language names |


<span id="audio-security-identification"></span>
## Audio Security Identification


|Operator name |Usage |Operator overview |
|---|---|---|
|[Audio Risk Identification](https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio_Risk_Identification) |* offline |* Audio content risk identification processor, supporting multi\-format audio security detection<br><br>* Core features:<br><br>   * Supports multiple audio formats (mp3, m4a, wav, wma, amr, aac, ogg)<br><br>   * Supports large files (duration ≤5 hours, ≤512MB)<br><br>   * Three\-level risk determination:<br><br>      * BLOCK: Unsafe sample<br><br>      * PASS: Safe sample<br><br>      * REVIEW: Manual review recommended<br><br>   * Supports custom business scenario configuration<br><br>   * Provides detailed detection result output |


<span id="text"></span>
# Text

<span id="tos-path-pre-signature"></span>
## TOS Path Pre\-Signature


|Operator name |Usage |Operator overview |
|---|---|---|
|[Generate a Common Pre-Signature for TOS](https://docs.byteplus.com/en/docs/Byteplus_LAS/Generate_a_Common_Pre-Signature_for_TOS) |* offline |* Core features:<br><br>   * Signature Generation Mechanism: Generate time\-limited pre\-signed URLs based on the Volcengine TOS SDK.<br><br>   * URL Schema Handling:<br><br>      * Natively supports signature conversion for paths using tos/s3 protocols.<br><br>      * Automatically skips paths containing http/https protocols.<br><br>   * Security Controls:<br><br>      * Configurable signature validity period (default: 3600 seconds). |


<span id="text-classification"></span>
## Text Classification


|Operator name |Usage |Operator overview |
|---|---|---|
|[Text Language Recognition](https://docs.byteplus.com/en/docs/Byteplus_LAS/Text_Language_Recognition) |* offline |* Text Language Recognition Operator \- Provides multilingual recognition capabilities based on the FastText model<br><br>* Core features:<br><br>   * Supports recognition of 176 languages (based on fasttext/lid.176 series models)<br><br>   * Batch inference optimization, suitable for processing large\-scale text data<br><br>   * Supports simultaneous output of language labels and confidence scores<br><br>   * Supports model files from local paths and TOS paths |


<span id="text-cleaning"></span>
## Text Cleaning


|Operator name |Usage |Operator overview |
|---|---|---|
|[Specific Character Replacement](https://docs.byteplus.com/en/docs/Byteplus_LAS/Specific_Character_Replacement) |* offline |* Regular Expression Batch Replacement Processor<br><br>* Core features:<br><br>   * Dual\-mode replacement mechanism:<br><br>      * Exact string match replacement<br><br>      * Regular expression pattern match replacement<br><br>   * Batch processing capability:<br><br>      * Supports parallel processing of multiple `pattern-replacement` pairs<br><br>   * Fault tolerance mechanism:<br><br>      * Skips abnormal modes and records detailed logs |
|[html tag removal](https://docs.byteplus.com/en/docs/Byteplus_LAS/html_tag_removal) |* offline |* HTML Document Purification Processor \- Multi\-structure Parsing and Intelligent Cleaning Solution<br><br>* Core features:<br><br>   * Multi\-structure Parsing<br><br>      * Title Extraction: Automatically recognize `<h1>`\-`<h6>` tags<br><br>      * Main Text Extraction: Intelligently identify the main content of the article<br><br>      * Redundancy Filtering: Remove non\-text tags such as `<script>`/`<style>`<br><br>   * Intelligent Processing<br><br>      * Fault Tolerance Mechanism: Support parsing of incomplete HTML fragments<br><br>      * Format Preservation: Maintain text paragraph structure and line break logic |


<span id="text-processing"></span>
## Text Processing


|Operator name |Usage |Operator overview |
|---|---|---|
|[MD5 Hash Calculation](https://docs.byteplus.com/en/docs/Byteplus_LAS/MD5_Hash_Calculation) |* offline |* MD5 Hash Calculator \- Calculate MD5 Fingerprint of Text<br><br>* Core features:<br><br>   * Generate corresponding MD5 hash value for each text data entry<br><br>   * Output fixed\-length (32\-bit lowercase hexadecimal) fingerprint<br><br>   * Support batch processing |
|[Duplicate Line Calculator](https://docs.byteplus.com/en/docs/Byteplus_LAS/Duplicate_Line_Calculator) |* offline |* Duplicate Line Calculator \- Calculate the Proportion of Duplicate Lines in Text<br><br>* Core features:<br><br>   * Duplicate line detection: Automatically identify duplicate line content in text<br><br>   * Proportion calculation: Calculate the ratio of duplicate lines to original lines<br><br>   * Quality assessment: Evaluate the repetition degree and quality of the text |
|[Whitespace Normalizer](https://docs.byteplus.com/en/docs/Byteplus_LAS/Whitespace_Normalizer) |* offline |* Whitespace Normalizer \- Replace various whitespace characters in text with standard spaces<br><br>* Core features:<br><br>   * Whitespace Recognition: Automatically recognize various Unicode whitespace characters<br><br>   * Normalization Processing: Replace all whitespace characters with standard spaces |
|[Text chunk splitting (based on sentence structure)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Text-chunk-splitting-sentence) |* offline |* Multi\-format Text Chunk Processor \- Structured Parsing and Intelligent Splitting Solution<br><br>* Core features:<br><br>   * Supported Formats<br><br>      * `Plain Text`: Semantic chunking based on paragraphs/punctuation<br><br>      * `Markdown`: Preserve document structure, filter image links<br><br>      * `HTML`: Extract main content, preserve chapter structure<br><br>   * Intelligent Chunking Strategy<br><br>      * Combine semantic and grammatical rules<br><br>      * Overlap optimization to maintain context coherence |
|[Special Character Proportion Calculator](https://docs.byteplus.com/en/docs/Byteplus_LAS/Special_Character_Proportion_Calculator) |* offline |* Special Character Proportion Calculator \- Text Feature Extraction Based on Special Character Proportion<br><br>* Core features:<br><br>   * Special Character Proportion Calculation: Precisely count the proportion of special characters in text<br><br>   * Multi\-granularity Support: Allows selection of different types of special characters for calculation<br><br>   * Flexible Configuration: Supports calculating the proportion of all special characters or specific types |
|[Text Link Removal](https://docs.byteplus.com/en/docs/Byteplus_LAS/Text_Link_Removal) |* offline |* Hyperlink Removal Operator \- Text Link Regex Replacement<br><br>* Core features:<br><br>   * Identify common forms of hyperlinks such as protocol links, www links, domain names + paths, etc.<br><br>   * Replace matched hyperlinks with a specified string (`repl`), defaulting to ""<br><br>   * Process strings in batches, return None for abnormal items |
|[URL Proportion Calculator](https://docs.byteplus.com/en/docs/Byteplus_LAS/URL_Proportion_Calculator) |* offline |* URL Proportion Calculator \- Text Feature Extraction Based on URL Character Proportion<br><br>* Core features:<br><br>   * URL Proportion Calculation: Precisely count the proportion of URL characters in the text<br><br>   * Multi\-protocol Support: Supports multiple URL protocols including HTTP, HTTPS<br><br>   * Intelligent Recognition: Accurately identify URL formats using regular expressions |
|[Text Length Calculator](https://docs.byteplus.com/en/docs/Byteplus_LAS/Text_Length_Calculator) |* offline |* Text Length Calculator \- Calculate the character length of text<br><br>* Core features:<br><br>   * Text length calculation: Calculate the number of characters in the input text<br><br>   * Batch processing: Support batch text length calculation<br><br>   * Numeric output: Return the length value as an integer type |
|[Simplified and Traditional Chinese Conversion](https://docs.byteplus.com/en/docs/Byteplus_LAS/Simplified_and_Traditional_Chinese_Conversion) |* offline |* OpenCC\-based Chinese Simplified\-Traditional Conversion Operator<br><br>* Core features:<br><br>   * Multi\-directional Conversion: Supports multiple conversion directions such as Simplified\-Traditional Chinese, Taiwan Traditional, Hong Kong Traditional, etc.<br><br>   * Mixed Text Processing: Correctly handles content mixed with Chinese and English, converting only the Chinese part.<br><br>   * Efficient Batch Processing: Supports fast conversion processing of large batches of text. |
|[Maximum English Word Length Calculator](https://docs.byteplus.com/en/docs/Byteplus_LAS/Maximum_English_Word_Length_Calculator) |* offline |* Maximum English Word Length Calculator \- Calculate the maximum length of English words in text<br><br>* Core features:<br><br>   * English word recognition: Use regular expressions to identify English words in text<br><br>   * Maximum length calculation: Calculate the maximum length among all English words<br><br>   * Batch processing: Support maximum English word length calculation for batch texts |
|[Text Security Scorer](https://docs.byteplus.com/en/docs/Byteplus_LAS/Text_Security_Scorer) |* offline |* Text Security Scorer \- Security Assessment Based on ShieldLM\-6B\-chatglm3<br><br>* Core features:<br><br>   * Multilingual Support: Supports Chinese and English text security assessment<br><br>   * Three\-Category Evaluation: Outputs probabilities for three categories: safe, unsafe, controversial<br><br>   * Batch Processing: Supports batch text security assessment to improve processing efficiency |
|[Bullet Line Proportion Calculator](https://docs.byteplus.com/en/docs/Byteplus_LAS/Bullet_Line_Proportion_Calculator) |* offline |* Bullet Line Proportion Calculator \- Calculate the proportion of bullet lines in text<br><br>* Core features:<br><br>   * Bullet detection: Automatically identify lines starting with bullet points in text<br><br>   * Proportion calculation: Calculate the ratio of the number of bullet lines to the total number of lines |
|[Character Proportion Calculator](https://docs.byteplus.com/en/docs/Byteplus_LAS/Character_Proportion_Calculator) |* offline |* Character Proportion Calculator \- Text Feature Extraction Based on Letter and Digit Character Proportions<br><br>* Core features:<br><br>   * Character proportion calculation: Accurately count the proportion of letter and digit characters in the text<br><br>   * Word segmentation mode support: Option to calculate proportions based on word segmentation or character level<br><br>   * Multilingual support: Supports character recognition for multiple languages including English, Chinese, Japanese, Korean, etc. |
|[Perplexity Calculator](https://docs.byteplus.com/en/docs/Byteplus_LAS/Perplexity_Calculator) |* offline |* Perplexity Calculation Operator \- Text Quality Evaluation Solution Based on Language Model<br><br>* Core features:<br><br>   * Language Model Evaluation<br><br>      * Calculate text perplexity based on KenLM language model<br><br>      * Support Chinese and English text quality evaluation<br><br>      * Provide text readability indicators<br><br>   * Quality Evaluation<br><br>      * The lower the perplexity, the higher the text quality<br><br>      * Suitable for text quality screening and evaluation |
|[Copyright Notice Removal](https://docs.byteplus.com/en/docs/Byteplus_LAS/Copyright_Notice_Removal) |* offline |* Copyright Notice Remover \- Remove text related to copyright notices from content<br><br>* Core features:<br><br>   * Copyright Notice Detection: Automatically identify copyright notice comments in code<br><br>   * Intelligent Cleaning: Precisely remove content based on copyright notice characteristics<br><br>   * Multi\-format Support: Supports block comment and line comment formats |
|[CommonCrawl WARC File Content Extraction](https://docs.byteplus.com/en/docs/Byteplus_LAS/CommonCrawl_WARC_File_Content_Extraction) |* offline |* CommonCrawl Web Content Extractor, supporting multiple parsing strategies<br><br>* Core features:<br><br>   * Multi\-parser support: trafilatura/justext/goose3<br><br>   * Supports local and remote WARC files<br><br>   * Supports binary data and base64 encoding<br><br>   * Batch processing of WARC files to extract web page content<br><br>   * Intelligent content extraction, filtering ads and navigation elements |
|[Word Repetition Ratio Calculator](https://docs.byteplus.com/en/docs/Byteplus_LAS/Word_Repetition_Ratio_Calculator) |* offline |* Word Repetition Ratio Calculator \- Text Feature Extraction Based on N\-gram Phrase Repetition Ratio<br><br>* Core features:<br><br>   * Word repetition ratio calculation: accurately count the proportion of repeated phrases in text<br><br>   * Bilingual support: supports word segmentation for Chinese and English<br><br>   * Flexible configuration: supports calculation of N\-gram phrases of different lengths |


<span id="text-quality-evaluation"></span>
## Text Quality Evaluation


|Operator name |Usage |Operator overview |
|---|---|---|
|[English Text Quality Scoring](https://docs.byteplus.com/en/docs/Byteplus_LAS/English_Text_Quality_Scoring) |* offline |* English Text Quality Scoring Operator \- Text Quality Evaluation Based on FastText<br><br>* Core features:<br><br>   * Quality Scoring: Use the FastText model to score the quality of English text, with a preference for scientific knowledge, and only supports CPU environment.<br><br>   * Batch Processing: Support batch processing of text to improve processing efficiency |
|[Multilingual Text Quality Scoring](https://docs.byteplus.com/en/docs/Byteplus_LAS/Multilingual_Text_Quality_Scoring) |* offline |* Multilingual Text Quality Scoring Operator \- Multilingual Text Quality Evaluation Based on E5 Model<br><br>* Core features:<br><br>   * Multilingual Support: Uses the multilingual\-e5 model to support text quality scoring in multiple languages<br><br>   * Deep Learning Evaluation: Performs quality evaluation using the Transformer\-based E5 model<br><br>   * GPU Acceleration: Supports GPU inference acceleration to improve processing efficiency<br><br>   * Batch Processing: Supports batch text processing to optimize inference performance |


<span id="text-security-identification"></span>
## Text Security Identification


|Operator name |Usage |Operator overview |
|---|---|---|
|[Text Content Risk Identification](https://docs.byteplus.com/en/docs/Byteplus_LAS/Text_Content_Risk_Identification) |* offline |* Text content risk identification processor, supporting multi\-dimensional security detection<br><br>* Core features:<br><br>   * Multi\-risk type detection<br><br>   * Three\-level risk judgment:<br><br>      * BLOCK: Unsafe sample<br><br>      * PASS: Safe sample<br><br>      * REVIEW: Recommend manual review<br><br>   * Support custom business scenario configuration<br><br>   * Provide detailed detection result output |


<span id="text-translation"></span>
## Text Translation


|Operator name |Usage |Operator overview |
|---|---|---|
|[Multilingual text translation](https://docs.byteplus.com/en/docs/Byteplus_LAS/Multilingual_text_translation) |* offline |* Seed\-X Multilingual Text Translation Model \- Core Features of Cross\-Language Text Translation<br><br>* Core features:<br><br>   * Multilingual Intelligent Translation<br><br>      * Supports text conversion between multiple languages; source and target languages can be customized via the source_language and target_language parameters<br><br>      * Based on the Seed\-X\-Instruct\-7B/Seed\-X\-PPO\-7B models, delivering high\-quality translation results<br><br>      * For supported languages, please refer to: https://huggingface.co/ByteDance\-Seed/Seed\-X\-Instruct\-7B<br><br>      * In general scenarios, it is recommended to use the Seed\-X\-PPO\-7B model, which has better translation quality<br><br>   * Flexible Configuration and Optimization<br><br>      * Supports multiple computation precision options (e.g., bfloat16) to adapt to different performance requirements<br><br>      * Integrates tensor parallel processing and prefix caching technology to significantly improve inference efficiency<br><br>      * Supports automatic or manual device allocation, perfectly adapting to single\-GPU/multi\-GPU environments<br><br>   * Resource Usage<br><br>      * It is recommended to use a GPU with more than 24GB of VRAM |


<span id="text-vectorization"></span>
## Text Vectorization


|Operator name |Usage |Operator overview |
|---|---|---|
|[Text embedding (BGE model)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Text-embedding-BGE) |* offline |* Based on the BGE series of text embedding models, supports dense vector generation<br><br>* Core features:<br><br>   * Multi\-model Support:<br><br>      * Supports models such as BGE\-M3, BGE\-Large\-zh\-v1.5, BGE\-Large\-en\-v1.5, BGE\-Multilingual\-Gemma2<br><br>      * Each model has different input prompts; users can choose different models according to their needs<br><br>   * Hardware Acceleration: Supports `FP16` quantization and GPU parallel computing |
|[Text sparse & dense embedding (BGE model)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Text-sparse-dense-embedding) |* offline |* Text embedding model based on BGE\-M3, supporting sparse/dense/token three\-level vector generation<br><br>* Core features:<br><br>   * Multi\-granularity Embedding Output:<br><br>      * Sparse Vector: Term weight representation, suitable for keyword retrieval<br><br>      * Dense Vector: 1024\-dimensional semantic representation, suitable for semantic similarity calculation<br><br>      * Token Vector: Fine\-grained context representation<br><br>   * Hardware Acceleration: Supports `FP16` quantization and GPU parallel computing |


<span id="video"></span>
# Video

<span id="video-processing"></span>
## Video Processing


|Operator name |Usage |Operator overview |
|---|---|---|
|[Video to MP4 Conversion](https://docs.byteplus.com/en/docs/Byteplus_LAS/Video_to_MP4_Conversion) |* offline |* Video Format Conversion Processor, converting various video formats to MP4<br><br>* Core features:<br><br>   * Supports converting multiple video formats to MP4<br><br>   * Intelligent audio track selection (All/Auto/First)<br><br>   * Customizable video quality and encoding parameters<br><br>   * Supports video height limitation and scaling<br><br>   * Fine\-grained control over audio encoding parameters<br><br>   * Supports local files, HTTP/HTTPS URLs, and TOS/S3 storage |
|[Video Resolution Adjustment](https://docs.byteplus.com/en/docs/Byteplus_LAS/Video_Resolution_Adjustment) |* offline |* Video Resolution Adjustment<br><br>* Core features:<br><br>   * Intelligently adjust resolution to a specified range<br><br>   * Support multiple aspect ratio preservation strategies<br><br>   * Control video quality and encoding parameters<br><br>   * Keep audio streams unaffected<br><br>   * Support path input, binary input, and TOS output |
|[Video Clip Splitting (by Duration)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Video-Clip-Splitting-Duration) |* offline |* Video Segment Splitting Processor, Intelligent Division by Fixed Duration<br><br>* Core features:<br><br>   * Split video by fixed second duration<br><br>   * Support minimum duration filtering for remaining segments<br><br>   * Support segment binary output or TOS storage<br><br>   * Provide automatic format inference and customization |
|[Video Audio Extraction](https://docs.byteplus.com/en/docs/Byteplus_LAS/Video_Audio_Extraction) |* offline |* Video Audio Extraction Processor, supporting multi\-stream separation<br><br>* Core features:<br><br>   * Supports extracting audio streams from videos with multiple input sources including local files, TOS, HTTP paths, or binary input<br><br>   * Supports multi\-audio stream selection: take only the first stream or all streams<br><br>   * Supports outputting audio to TOS, returning binary data, setting sample rates, etc.<br><br>   * Supports extracting specified time intervals (start_second, end_second)<br><br>   * All output audio is in MP3 format |
|[Video Clip Segmentation (Keyframe)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Video-Clip-Segmentation-Keyframe) |* offline |* Video keyframe segmentation processor, supporting intelligent clip splitting.<br><br>* Core features:<br><br>   * Multi\-algorithm keyframe detection:<br><br>      * I_frame: Based on I\-frame detection (recommended)<br><br>      * difference: Pixel difference detection<br><br>      * histogram: Histogram difference detection<br><br>   * Supports clip binary output or TOS storage<br><br>   * Provides timestamp positioning function |
|[Video Clip Segmentation (Timestamp)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Video-Clip-Segmentation-Timestamp) |* offline |* Video Timestamp Splitting Processor, supports splitting by specified time ranges<br><br>* Core features:<br><br>   * Split video by given timestamp intervals<br><br>   * Support segment binary output or TOS storage<br><br>   * Provide automatic format inference and customization |
|[Video Frame Sampling](https://docs.byteplus.com/en/docs/Byteplus_LAS/Video_Frame_Sampling) |* offline |* An image frame sampler from video, supporting multiple sampling modes and time range control.<br><br>* Core features:<br><br>   * Multiple sampling methods:<br><br>      * by_count_uniform: Uniformly sample K frames within the time range<br><br>      * by_interval_time: Sample at time interval Δt seconds<br><br>      * by_interval_frames: Sample at decoded frame interval N<br><br>      * by_fps: Sample at target fps<br><br>      * by_timestamps: Sample according to the given timestamp list<br><br>   * Support start and end time range restrictions and whether to include the last frame<br><br>   * Output original frames (array), base64 encoding, timestamps, frame indices, and optional TOS storage paths<br><br>   * Two input sources: path input or binary input, compatible with remote URIs (via run_on_local_path) |
|[Adaptive Video Compression](https://docs.byteplus.com/en/docs/Byteplus_LAS/Adaptive_Video_Compression) |* offline |* Video Adaptive Compression<br><br>* Core features:<br><br>   * Adaptively compress video according to target file size<br><br>   * Multi\-level compression strategy: Frame rate adjustment → Resolution adjustment → Bitrate control<br><br>   * Compress file size as much as possible while maintaining video quality<br><br>   * Support CPU and GPU encoding<br><br>   * Support path input, binary input, and TOS output |
|[Video Keyframe Extraction](https://docs.byteplus.com/en/docs/Byteplus_LAS/Video_Keyframe_Extraction) |* offline |* Video keyframe extraction processor that supports dynamic detection with multiple algorithms.<br><br>* Core features:<br><br>   * Multiple algorithm support:<br><br>      * Pixel difference method (difference)<br><br>      * Optical flow method (optical_flow)<br><br>      * Histogram method (histogram)<br><br>      * I\-frame keyframe identification (I_frame)<br><br>   * Supports custom threshold and quantity control<br><br>   * Provides timestamp positioning function<br><br>   * Supports multiple output formats and storage options |


<span id="document"></span>
# Document

<span id="document-parsing"></span>
## Document Parsing


|Operator name |Usage |Operator overview |
|---|---|---|
|[Xlsx Document Parsing](https://docs.byteplus.com/en/docs/Byteplus_LAS/Xlsx_Document_Parsing) |* offline |* Excel spreadsheet parsing processor that supports multi\-format output and structured data extraction<br><br>* Core features:<br><br>   * Supports xlsx/xls format parsing<br><br>   * Outputs markdown or html format<br><br>   * Preserves table structure and data relationships<br><br>   * Supports multi\-sheet processing<br><br>   * Provides TOS storage option |
|[Intelligent PDF Document Parsing](https://docs.byteplus.com/en/docs/Byteplus_LAS/Intelligent_PDF_Document_Parsing) |* offline |* PDF Intelligent Document Parsing Processor, supporting multi\-dimensional content extraction and structured output<br><br>* Core features:<br><br>   * High\-precision PDF text extraction<br><br>   * Output text in markdown format<br><br>   * Preserve original document structure and format<br><br>   * Support recognition of tables, images, etc.<br><br>   * Provide detailed parsing results and TOS storage options |


<span id="multimodal"></span>
# Multimodal

<span id="audio-understanding"></span>
## Audio Understanding


|Operator name |Usage |Operator overview |
|---|---|---|
|[Audio Content Understanding (Qwen Omni Model)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio-Understanding-qwen) |* offline |* Qwen2.5\-Omni Multimodal Audio Understanding Model \- Core Functions for Audio Content Parsing and Natural Language Description Generation<br><br>* Core features:<br><br>   * Intelligent Content Understanding and Description Generation<br><br>      * Automatically generate detailed and accurate natural language descriptions based on audio signals, supporting custom prompts via the prompt parameter<br><br>      * Supports audio formats such as mp3, acc, m4a, etc.<br><br>   * Efficient Model Loading and Inference Optimization<br><br>      * Supports multiple computation precision options (bfloat16, float16, float32) to adapt to different performance requirements<br><br>      * Integrates FlashAttention2 acceleration technology to significantly improve inference efficiency<br><br>      * Supports automatic or manual device allocation, perfectly adapting to single\-card/multi\-card environments<br><br>   * Resource Usage<br><br>      * Recommended to use GPUs with 48G or more VRAM |
|[Audio Understanding (Kimi-Audio Series Models)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Audio-Understanding-kimi) |* offline |* Kimi\-Audio Multimodal Audio Understanding Model \- Audio Semantic Parsing and Natural Language Description Generation<br><br>* Core features:<br><br>   * Multimodal Audio Processing<br><br>      * Supports three audio formats: `URL`/`Base64 encoding`/`binary stream`<br><br>   * Audio\-Language Joint Modeling<br><br>      * Achieves accurate mapping of audio content to the semantic space<br><br>   * Conversational Prompt Support<br><br>      * Guides generation direction via the `prompt` parameter<br><br>   * Resource Usage<br><br>      * Recommended to use GPUs with 48G or higher VRAM |


<span id="image-understanding"></span>
## Image Understanding


|Operator name |Usage |Operator overview |
|---|---|---|
|[Image Content Understanding (Qwen VL Series Models, supporting large-scale models)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Image-Understanding-qwen-vl) |* offline |* Qwen2.5\-VL multimodal image understanding model supports visual semantic parsing and natural language description generation, suitable for various image analysis scenarios.<br><br>* Core features:<br><br>   * Multimodal temporal modeling: Supports three image input formats (URL, Base64 encoding, binary stream), flexibly adapting to different data sources.<br><br>   * Conversational prompt support: Customize generation direction via the `prompt` parameter to meet diverse business needs.<br><br>   * Efficient inference: Integrates VLLM inference engine, supports three precisions (`bfloat16`, `float16`, `float32`), making full use of GPU computing power.<br><br>   * Recommend using GPUs with 48G or more VRAM |
|[Image Content Understanding (Qwen VL Series Models)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Image-Understanding-qwen) |* offline |* Qwen2.5\-VL Multimodal Image Understanding Model \- Visual Semantic Parsing and Natural Language Description Generation<br><br>* Core features:<br><br>   * Multimodal Input Processing<br><br>      * Supports three image formats: `URL`, `Base64 encoding`, and `binary stream`<br><br>   * Visual\-Language Joint Modeling<br><br>      * Achieves accurate mapping of image content to semantic space<br><br>   * Conversational Prompt Support<br><br>      * Guides generation direction via the `prompt` parameter<br><br>   * Resource Usage<br><br>      * Recommended to use a GPU with 48G or more VRAM |
|[Image Content Understanding (LLaVA Series Models)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Image-Understanding-LLaVA) |* offline |* LLaVA Multimodal Image Understanding Model \- Visual Semantic Parsing and Natural Language Description Generation<br><br>* Core features:<br><br>   * Multimodal Input Processing<br><br>      * Supports three image formats: `URL`, `Base64 encoding`, and `binary stream`<br><br>   * Vision\-Language Joint Modeling<br><br>      * Achieves accurate mapping of image content to the semantic space<br><br>   * Conversational Prompt Support<br><br>      * Guides generation direction via the `prompt` parameter<br><br>   * Resource Usage<br><br>      * Recommended to use a GPU with 48G or more VRAM |


<span id="multimodal-vectorization"></span>
## Multimodal Vectorization


|Operator name |Usage |Operator overview |
|---|---|---|
|[Image-text embedding (CLIP model)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Image-text-embedding-CLIP) |* offline |* CLIP (Contrastive Language\-Image Pretraining) cross\-modal embedding generator, which implements text\-image joint embedding space mapping based on the CLIP model<br><br>* Core features:<br><br>   * Unified Multimodal Encoding<br><br>      * Text Encoding: Chinese text → 512/768/1024\-dimensional semantic vector<br><br>      * Image Encoding: Image → 512/768/1024\-dimensional visual feature vector<br><br>   * Cross\-modal Similarity Calculation<br><br>      * Supports cosine similarity/dot product calculation of the correlation between text and image embedding vectors |


<span id="video-understanding"></span>
## Video Understanding


|Operator name |Usage |Operator overview |
|---|---|---|
|[Video Content Understanding (Qwen VL Series Models)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Vedio-Understanding-qwen) |* offline |* Qwen2.5\-VL Multimodal Video Understanding Model \- Temporal Semantic Parsing and Natural Language Description Generation<br><br>* Core features:<br><br>   * Multimodal Temporal Modeling<br><br>      * Supports three video formats: `URL`/`Base64 encoding`/`binary stream`<br><br>   * Spatio\-Temporal Joint Modeling<br><br>      * Captures spatio\-temporal features and semantic correlations of videos<br><br>   * Conversational Prompt Support<br><br>      * Guides generation direction via the `prompt` parameter<br><br>   * Resource Usage<br><br>      * Recommended to use a GPU with 48G or more VRAM |
|[Video Content Understanding (Qwen VL Series Models, supports large-scale models)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Video-Understanding-qwen-vl) |* offline |* Qwen2.5\-VL multimodal video understanding model supports temporal semantic parsing and natural language description generation, suitable for various video analysis scenarios.<br><br>* Core features:<br><br>   * Multimodal temporal modeling: Supports three video input formats (URL, Base64 encoding, binary stream), flexibly adapting to different data sources.<br><br>   * Spatiotemporal joint modeling: Automatically captures spatiotemporal features and semantic correlations of videos to achieve more accurate video content understanding.<br><br>   * Conversational prompt support: Customize generation directions via the `prompt` parameter to meet diverse business needs.<br><br>   * Efficient inference: Integrates the VLLM inference engine, supporting three precisions (`bfloat16`, `float16`, `float32`), making full use of GPU computing power.<br><br>   * Recommended to use GPUs with 48G or more VRAM |


<span id="ark-large-model-series"></span>
# Ark Large Model Series

<span id="multimodal-deep-thinking"></span>
## Multimodal Deep Thinking


|Operator name |Usage |Operator overview |
|---|---|---|
|[Multimodal Deep Thinking (Doubao-Seed-1.6)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Multimodal-Deep-Thinking-Doubao-Seed-1-6) |* offline |* Provide deep thinking capabilities for large models in multimodal scenarios Use models with deep thinking capabilities to analyze and understand images, videos, or text, and return text output.<br><br>* Core features:<br><br>   * Deep thinking mechanism: The model automatically decomposes problems and performs logical reasoning before answering, generating a chain of thought (reasoning_content)<br><br>   * Multimodal scenario support: Supports image/video understanding tasks and automatically constructs message structures that comply with multimodal model specifications<br><br>   * Input simplification mechanism: Configure input formats such as base64 encoding or URLs for images/videos to enable visual understanding functions |
|[Multimodal Deep Thinking (Doubao Series Models)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Multimodal-Deep-Thinking-Doubao) |* offline |* Provides deep thinking capabilities for large models in multimodal scenarios Use models with deep thinking capabilities to analyze and understand images, videos, or text, and return text output.<br><br>* Core features:<br><br>   * Deep thinking mechanism: The model automatically decomposes problems and performs logical reasoning before answering, generating a chain of thought (reasoning_content)<br><br>   * Multimodal scenario support: Supports image/video understanding tasks and automatically constructs message structures that comply with multimodal model specifications<br><br>   * Input simplification mechanism: Configure input formats such as base64 encoding or URLs for images/videos to enable visual understanding functions |
|[Multimodal Deep Thinking (Doubao-Seed-1.6-flash)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Multimodal-Deep-Thinking-Doubao-1-6) |* offline |* Provide deep thinking capabilities of large models in multimodal scenarios Use models with deep thinking capabilities to analyze and understand images, videos, or text, and return text output.<br><br>* Core features:<br><br>   * Deep thinking mechanism: The model automatically decomposes problems and performs logical reasoning before answering questions, generating a chain of thought (reasoning_content)<br><br>   * Multimodal scenario support: Supports image/video understanding tasks, automatically constructs message structures that comply with multimodal model specifications<br><br>   * Input simplification mechanism: Configure input formats such as base64 encoding or URLs for images/videos to enable visual understanding functions |


<span id="text-generation"></span>
## Text Generation


|Operator name |Usage |Operator overview |
|---|---|---|
|[Text Generation (Doubao/DeepSeek Series Models)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Text-Generation) |* offline |* Specialized Processor for Large Model Text Generation (Doubao/DeepSeek)<br><br>* Core features:<br><br>   * Pure text scenario optimization: Automatically constructs a model\-compliant message structure based on user input text data<br><br>   * Input simplification mechanism: Natively supports str\-type input, automatically encapsulating it into {role: user, content: text} format<br><br>   * Multi\-task support: Ready\-to\-use for NLP scenarios like translation, summarization, Q&A, etc.<br><br>   * Dual prompt system:<br><br>      * system_content: System\-level behavior guidance (e.g., translation style control)<br><br>      * prompt: User\-level instruction template (supports {query} placeholder replacement) |
|[Text Generation (Deepseek-V3)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Text-Generation-ds-v3) |* offline |* Specialized Processor for Large Model Text Generation (Doubao/DeepSeek)<br><br>* Core features:<br><br>   * Plain Text Scenario Optimization: Automatically constructs a message structure compliant with model specifications based on user input text data.<br><br>   * Input Simplification Mechanism: Natively supports str\-type input and automatically encapsulates it into {role: user, content: text} format.<br><br>   * Multi\-task Support: Ready\-to\-use for NLP scenarios such as translation, summarization, and Q&A.<br><br>   * Dual Prompt System:<br><br>      * system_content: System\-level behavior guidance (e.g., translation style control).<br><br>      * prompt: User\-level instruction template (supports {query} placeholder replacement). |


<span id="visual-understanding"></span>
## Visual Understanding


|Operator name |Usage |Operator overview |
|---|---|---|
|[Visual Content Understanding (Doubao Series Models)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Visual-Content-Doubao-Models) |* offline |* Large Model Multimodal Video Understanding Processor<br><br>* Core features:<br><br>   * Multimodal Scene Support: Supports image/video understanding tasks and automatically constructs message structures compliant with multimodal model specifications<br><br>   * Simplified Input Mechanism: Configure input formats such as base64 encoding or URLs for images/videos to enable visual understanding functionality |
|[Visual Content Understanding (Doubao-1.5-vision-pro-32k)](https://docs.byteplus.com/en/docs/Byteplus_LAS/Visual-Content-Doubao-1-5) |* offline |* Large Model Multimodal Video Understanding Processor<br><br>* Core features:<br><br>   * Multimodal Scene Support: Supports image/video understanding tasks and automatically constructs message structures compliant with multimodal model specifications<br><br>   * Simplified Input Mechanism: Configure input formats such as base64 encoding or URLs for images/videos to enable visual understanding functions |


<span id="others"></span>
# Others

<span id="others"></span>
## Others


|Operator name |Usage |Operator overview |
|---|---|---|
|[Timestamp Fragment Merging](https://docs.byteplus.com/en/docs/Byteplus_LAS/Timestamp_Fragment_Merging) |* offline |* Timestamp Merging Operator \- Normalization, Merging, and Splitting of Second\-level Intervals<br><br>* Core features:<br><br>   * Normalization and Sorting: Unify input format to (start, end) floating\-point seconds and validate legality.<br><br>   * Pre\-merge Small Gaps: Merge overlapping or adjacent segments with gaps ≤ threshold (pre_merge_gap_seconds).<br><br>   * Longest Silence First Splitting: Split at the longest silence first to ensure each segment's span does not exceed max_span_seconds.<br><br>   * Forced Chunking (Optional): Split overlong segments into fixed windows to ensure each segment's length does not exceed the upper limit (enforce_chunking). |
