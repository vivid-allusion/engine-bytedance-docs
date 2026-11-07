---
title: "Audio Processing"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Audio_Processing"
---

Audio processing operator is used to realize the function of audio to text. Through this article, you can learn about the capabilities and usage of the various operators included in the Audio Processing Module.

# Prerequisite

The enterprise administrator has configured the large model for the operator, see details [Configure Large Model Invocation](https://docs.byteplus.com/docs/dataagent/Configure_Large_Model_Invocation).

# Audio processing operator introduction

1. **Speech to Text (ASR) \-Qwen\-Qmni**

Support for converting audio files into text data, with built\-in functions such as automatic punctuation, semantic smoothness, digital regularity, and intelligent clauses, which can be arbitrarily matched according to needs. Suitable for non\-real\-time automatic speech recognition scenarios.

2. **Speech to Text (ASR) \-Doubao Standard Edition**

Support for transcribing audio files (< 5 hours) into text data, with built\-in functions such as automatic punctuation, semantic smoothness, number regularity, and intelligent clauses, which can be arbitrarily matched according to needs. It is suitable for non\-real\-time automatic speech recognition scenarios, such as summary of meeting records, intelligent outbound call quality inspection, after\-school teaching aids and learning situation analysis.

# Operating instructions

## Speech to Text (ASR) \-Qwen\-Qmni

### Step 1: Create a new audio processing operator

1. In the left navigation bar of Enterprise Knowledge Engine, select **Data Access** \> **Visual Knowledge Processing**.

2. In the upper left corner of the **Task List** page, click **Create** and select **New Offline Task**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3ab3fcef68741eebf8a2e3ad706d7cc~tplv-goo7wpa0wc-image.image)

3. Follow the steps in [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task), while processing the node, select Add the **Speech to Text (ASR) \-Qwen\-Omin** operator in **Audio Processing** for data connections.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e3a7fcf6f42e42879d2d72573479b9e7~tplv-goo7wpa0wc-image.image)

### Step 2: Configuring the Operator

Click "Language to Text (ASR) \-Qwen\-Omin" and configure the relevant parameters on the basic information page.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/81ab0eeebaac4bdcbc037dbdd39e981f~tplv-goo7wpa0wc-image.image)

1. **Model information**

   The relevant parameters are described as follows:

   |Parameter |Configuration instructions |
   |---|---|
   |Model selection |Choosing a large model is supported if the enterprise administrator has configured the large model for the operator (see **Prerequisites** above for details). You can also choose to **customize the model** and complete the model related configuration. |
   |Model call address |The calling address of the application |
   |Inference access point |General format is `ep-xxxxxxxxxx-yyyy`, create method reference [Create custom inference access point](https://www.volcengine.com/docs/82379/1099522) |
   |API Key |The general format is `xxxxxxxx-yyyy-xxxx-yyyy-xxxxxxxxxxxx`, and the acquisition method is referred to [Get API Key and configure](https://www.volcengine.com/docs/82379/1263279) |

2. **Input parameter**

   \*\*Input Mode: \*\*Select the source mode for the input data. The following two modes are supported:

   * **URL:**  Enter the URL of the online file.

   * **File:**  Upload local files.

      \*\*Input field: \*\*According to the actual output field of the upstream operator, select the field that needs to be extracted.

   > **注意**

   > Input mode When selecting file, the input field must select file_ref.

3. **Handle configuration**

   * Enable audio sharding: After enabling, you need to configure the sharding duration (default 3600 seconds) and overlap duration (default 5000 milliseconds).

   * Language: Select Chinese or English.

   * Format: Select raw, wav, mp3, ogg, or video format.

   * Recognize prompt words: Set AI recognition prompt words as needed. You can modify the default prompt words according to business requirements to make AI processing results more accurate.

   * Custom parameters: Choose to add parameter configuration as needed, and support adding string type or boolean parameters.

4. **Advanced Settings**

   The relevant parameters are described as follows:

   |**Pparameter** |**Description** |
   |---|---|
   |Concurrent size |Sets the number of tasks to process concurrently.<br><br>Default value: 10<br><br>Value range: [Note: Please add value range] |
   |Timeout |Sets the timeout for task processing in milliseconds (ms).<br><br>Default value: 180000 ms |
   |Number of retries |Sets the number of automatic retries after a task fails.<br><br>Default value: 3 times |
   |Retry interval |Sets the interval between retries after a task fails.<br><br>Default value: 100 ms |
   |Exception handling |Configure the handling policy when a task exception occurs.<br><br>The following two strategies are supported:<br><br>• **Terminate task:**  When an exception occurs, immediately terminate the execution of the current task. This is the default option.<br><br>• **Ignore exceptions:**  When an exception occurs, ignore the error and continue with the next steps of the task. |

5. **Output Configuration**

   \*\*Output field: \*\*Specifies the name of the output field used to store the recognition result.

### Step 3: Test execution

Click "Test Execution" to view the output results in the "Test Execution Results" column.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/08b92f04a6d04af7bfd9d0e4672d0766~tplv-goo7wpa0wc-image.image)

## Speech to Text (ASR) \-Doubao Standard Edition

### Step 1: Create a new audio processing operator

1. In the left navigation bar of Enterprise Knowledge Engine, select **Data Access** \> **Visual Knowledge Processing** .

2. In the upper left corner of the **Task List** page, click **New** and select **New Offline Task**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bad0f8f332a4dfc9b58964bf3926cf3~tplv-goo7wpa0wc-image.image)

3. Follow the steps in [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task), while processing the node, select Add **Speech to Text (ASR) \-Doubao Standard Edition** operator for data connection in **Audio Processing**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc19be669e4642de83f31af32078f923~tplv-goo7wpa0wc-image.image)

### Step 2: Configuring the Operator

Click the **speech\-to\-text (ASR) \-Doubao Standard Edition** operator in the process canvas and complete the following configuration.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3d57d9e1bd954ec6b597ae41a0cb6846~tplv-goo7wpa0wc-image.image)

|**Module** |**Parameter** |**Description** |
|---|---|---|
|Model information |Model selection |Choosing a large model is supported if the enterprise administrator has configured the large model for the operator (see **Prerequisites** above for details). You can also choose to **customize the model** and complete the model related configuration. |
||AppID |App ID under the bean bag voice service, please refer to [how to get parameters App, Token, etc ](https://www.volcengine.com/docs/6561/196768?lang=zh#q1%EF%BC%9A%E5%93%AA%E9%87%8C%E5%8F%AF%E4%BB%A5%E8%8E%B7%E5%8F%96%E5%88%B0%E4%BB%A5%E4%B8%8B%E5%8F%82%E6%95%B0appid%EF%BC%8Ccluster%EF%BC%8Ctoken%EF%BC%8Cauthorization-type%EF%BC%8Csecret-key-%EF%BC%9F).<br><br>See [Bean Bun Voice Quick Start ](https://www.volcengine.com/docs/6561/163043?lang=zh)for details. |
||Access Token |Access Token under the bean bag voice service, please refer to [how to get parameter App, Token, etc ](https://www.volcengine.com/docs/6561/196768?lang=zh#q1%EF%BC%9A%E5%93%AA%E9%87%8C%E5%8F%AF%E4%BB%A5%E8%8E%B7%E5%8F%96%E5%88%B0%E4%BB%A5%E4%B8%8B%E5%8F%82%E6%95%B0appid%EF%BC%8Ccluster%EF%BC%8Ctoken%EF%BC%8Cauthorization-type%EF%BC%8Csecret-key-%EF%BC%9F). |
||Resource Information ID |* Bean Bag Recording File Recognition Model 1.0: volc.bigasr.auc<br><br>* Bean Bag Recording File Recognition Model 2.0: volc.seedasr.auc |
|Input parameter |Input mode |Select the video input source mode.<br><br><br>* **URL:**  Enter the URL of the online file.<br><br>* **File:**  Upload local files. |
||Input field |Based on the actual output fields of the upstream operator, select the fields that need to be extracted.<br><br>> **注意**<br><br><br>> Input mode When selecting file, the input field must select file_ref.<br> |
|Handle configuration |Enable audio sharding |After opening, you need to configure the sharding duration (default 3600 seconds) and the overlap duration (default 5000 milliseconds). |
||Language |Support Chinese, English, Japanese and Spanish and other multilingual options. Default is not set, the system will automatically recognize the language. |
||Format |Support selecting raw, wav, mp3, ogg, video formats. Default is not set, the system will automatically infer the format. |
||Semantic smoothness |After opening, the readability and fluency of automatic speech recognition (ASR) results are improved by deleting or modifying the non\-fluent parts of ASR results, such as pause words, modal words, semantic repetitive words, etc. |
||Hot word enhancement |After opening, you need to configure the hot word list ID. For the description of hot words in the voice of bean buns, see [Hot words ](https://docs.volcengine.com/docs/DoubaoVoice/Hotwords?lang=zh). |
||Substitute word |After opening, you need to configure the replacement word list ID. For a description of substitution words for bean buns, see [Substitution Words ](https://docs.volcengine.com/docs/DoubaoVoice/Replacementword?lang=zh). |
||Custom parameters |Support for setting more content through custom parameters. Please refer to the [Submit Task API ](https://www.volcengine.com/docs/6561/1354868?lang=zh#%E6%8F%90%E4%BA%A4%E4%BB%BB%E5%8A%A1)for supported parameters. For example, setting a custom parameter `enable_emotion_detection = happy`means turning on emotion recognition and recognizing happy emotions. |
|Advanced Settings |Concurrent size |Sets the number of tasks to process concurrently.<br><br>Default value: 10 |
||Timeout |Sets the timeout for task processing in milliseconds (ms).<br><br>Default value: 180000 ms |
||Number of retries |Sets the number of automatic retries after a task fails.<br><br>Default value: 3 times |
||Retry interval |Sets the time interval between each retry after a task fails.<br><br>Default value: 100 ms |
||Exception handling |Configure the handling policy when a task exception occurs.<br><br>The following two strategies are supported:<br><br>• **Terminate task:**  When an exception occurs, immediately terminate the execution of the current task and clear the intermediate results. This is the default option.<br><br>• **Ignore exceptions:**  When an exception occurs, ignore the error (populate the data with null) and continue with the next steps of the task. |
|Output Configuration |Output content |Support selecting **the whole result** or **the whole result + clause details**. The default is the **entire paragraph result**. |
||Output field |Custom output fields. |

### Step 3: Test execution

Click "Test Execution" to view the output results in the "Test Execution Results" column.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8138526450e4ecb960205dec85d18c6~tplv-goo7wpa0wc-image.image)
