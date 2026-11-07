---
title: "Video Processing"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Video_Processing"
---

Video processing operators are used to implement audio & video related segmentation, summary and fusion functions. Through this article, you can learn about the capabilities and usage of the various operators included in the video processing module.

# Prerequisite

The enterprise administrator has configured the large model for the operator, for details, see [Configure Large Model Invocation](https://docs.byteplus.com/docs/dataagent/Configure_Large_Model_Invocation).

# Introduction to Video Processing Operators

1. **Video Intelligent Understanding\-Qwen**

The Qwen multimodal understanding model is used to understand the picture and voice in the video at the same time, summarize the video content, and label the scenes/segments. Support the call of Volcano Ark bean bags, Qwen and other large models to understand the multi\-modal content of the video in batches.

2. **Video Intelligent Understanding\-Doubao**

The bean bag multimodal understanding model is used to understand the picture and voice in the video at the same time, summarize the video content, and label the scenes/segments.

3. **Video keyframe extraction**

In video processing scenarios, key frame extraction (extracting representative and informative frames in video, such as core picture frames and frames containing products) is the core link of unstructured video data processing, and is widely used in video content analysis, AI training, content retrieval and other scenarios.

4. **Audio & video information fusion**

Using the ability of large model understanding, the ASR results and video understanding results are segmented and fused according to the time axis.

# Operation steps

## **Video Intelligent Understanding\-Qwen**

### Step 1: Create a new **video intelligent understanding\-Qwen** operator

1. In the left navigation bar of Enterprise Knowledge Engine, select **Data Access** \> **Visual Knowledge Processing**.

2. In the upper left corner of the **Task List** page, click **New** and select **New Offline Task**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db24f929b1e34c90a2ef1795d8263c56~tplv-goo7wpa0wc-image.image)

3. Follow the steps in [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task), and when processing the node, select Add operators from Video Processing for data connections.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/628d62add25a49d79347c46225d88ac7~tplv-goo7wpa0wc-image.image)

### Step 2: Configuring the Operator

1. Click "Video Intelligent Understanding\-Qwen", and configure relevant parameters on the basic information page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5144be1e7453497fb61a1ba0c80e3cc1~tplv-goo7wpa0wc-image.image)

|Module |Parameter |Configuration instructions |
|---|---|---|
|Model information |Model selection |Choosing a large model is supported if the enterprise administrator has configured the large model for the operator (see **Prerequisites** above for details). You can also choose to **customize the model** and complete the model related configuration. |
||Model call address |The calling address of the application |
||Inference access point |General format is `ep-xxxxxxxxxx-yyyy`, create method reference [Create custom inference access point](https://www.volcengine.com/docs/82379/1099522) |
||API Key |The general format is `xxxxxxxx-yyyy-xxxx-yyyy-xxxxxxxxxxxx`, and the acquisition method is referred to [Get API Key and configure](https://www.volcengine.com/docs/82379/1263279) |
|Input parameter |Input mode |Select the source mode for the input data.<br><br><br>* **URL:**  Enter the URL of the online file.<br><br>* **File:**  Upload local files. |
||Input field |Based on the actual output fields of the upstream operator, select the fields that need to be extracted.<br><br>> **注意**<br><br><br>> Input mode When selecting file, the input field must select file_ref.<br> |
|Handle configuration |Enable video segmentation |Once turned on, you need to configure the maximum size of a single sharding (default 2048 MB), the maximum duration of a single sharding (default 3600 seconds), and use the sharding URL switch. |
|Advanced Settings |Concurrent size |Sets the number of tasks to process concurrently.<br><br>Default value: 10 |
||Timeout |Sets the timeout for task processing in milliseconds (ms).<br><br>Default value: 180000 ms |
||Number of retries |Sets the number of automatic retries after a task fails.<br><br>Default value: 3 times |
||Retry interval |Sets the time interval for automatic retries after a task fails.<br><br>Default value: 100 ms |
||Exception handling |Configure the handling policy when a task exception occurs.<br><br>The following two strategies are supported:<br><br>• **Terminate task:**  When an exception occurs, immediately terminate the execution of the current task. This is the default option.<br><br>• **Ignore exceptions:**  When an exception occurs, ignore the error and continue with the next steps of the task. |
|Prompt word configuration |Model prompt word |A cue word used to specify model\-generated text. The default value is empty. Users can directly use templates or customize them.<br><br>Support video marking, content summary, breaking point analysis, plot analysis, tag extraction template. |

2. Click **Test,**  output the test content, and return the test results of the model.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/695f9149c5fd459a90027208f2ac9b59~tplv-goo7wpa0wc-image.image)

3. **Fill in the output field,**  specifying the name of the output field to store the recognition result. User\-defined output fields do not support the first space, the rest are supported, no more than 64 characters.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/28bedf3383284caeb2a5bd83af417994~tplv-goo7wpa0wc-image.image)

### Step 3: Test execution

Click "Test Execution" to view the output results in the "Test Execution Results" column.

## Video Intelligent Understanding\-Doubao

### Step 1: Create a new video intelligent understanding\-Doubao operator

1. In the left navigation bar of Enterprise Knowledge Engine, select **Data Access** \> **Visual Knowledge Processing**.

2. In the upper left corner of the **Task List** page, click **Create** and select **Create Offline Task**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/22ff8783834a4f26819ea6d08852a7b0~tplv-goo7wpa0wc-image.image)

3. Follow the steps in [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task) and select Add Video Intelligence\-Doubao operator from Video Processing for data connection while processing nodes.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3a7054522aa04ce7b302689075f5b457~tplv-goo7wpa0wc-image.image)

### Step 2: Configuring the Operator

Click on the **Video Intelligent Understanding\-Doubao** operator in the process canvas and complete the following configuration.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd96e4d52e05490b9f178affff6bd274~tplv-goo7wpa0wc-image.image)

|**Module** |**Parameter** |**Description** |
|---|---|---|
|Model information |Model selection |Choosing a large model is supported if the enterprise administrator has configured the large model for the operator (see **Prerequisites** above for details). You can also choose to **customize the model** and complete the model related configuration. |
||Model call address |The calling address of the application. |
||Inference access point |The general format is `ep-xxxxxxxxxx-yyyy`, and the creation method refers to [creating a custom inference access point ](https://www.volcengine.com/docs/82379/1099522). |
||API Key |The general format is `xxxxxxxx-yyyy-xxxx-yyyy-xxxxxxxxxxxx`, and the acquisition method refers to [obtaining API Key and configuring it ](https://www.volcengine.com/docs/82379/1263279). |
|Input parameter |Input mode |Select the video input source mode.<br><br><br>* **URL:**  Enter the URL of the online file.<br><br>* **File:**  Upload local files. |
||Input field |Based on the actual output fields of the upstream operator, select the fields that need to be extracted.<br><br>> **注意**<br><br><br>> Input mode When selecting file, the input field must select file_ref.<br> |
|Handle configuration |Open long video understanding |Refers to when the video size exceeds the maximum length that can be processed by a large model (e.g. the limit of the Doubao VLM model is 50MB video), video adaptive processing is carried out through video segmentation, video compression, etc., and then understood through the visual model, and finally the processing results are merged. |
||Long video processing strategy |By default, video segmentation is required, and video compression can be selected.<br><br><br>* Video segmentation: Automatically segmented according to the system default policy, so that the video file size falls within the comprehensible range of the visual model (for example, a 200MB video is divided into 4 segments, each 50MB).<br><br>* Video compression: When the video has a high bit rate (such as 1080p) short video (generally less than 10min), this strategy can be used for video compression. However, it is necessary to pay attention to the parameter value settings and compress the video to a size that the visual model can understand. |
||Target resolution |The target resolution for video compression. Support to choose 480p, 720p, 1080p, the default is 720p. |
||H.264\-CRF mass factor |H.264\-CRF quality factor for video compression. The smaller the value, the clearer and larger the video. Optional range 18 to 28, 23 visually lossless, 28 significantly compressed. The recommended value is 23\-26. |
||FFMPEG parallelism |Default 4. Please enter a positive integer between 1 and 32. |
|Advanced Settings |Concurrent size |Sets the number of tasks to process concurrently.<br><br>Default value: 10 |
||Timeout |Sets the timeout for task processing in milliseconds (ms).<br><br>Default value: 180000 ms |
||Number of retries |Sets the number of automatic retries after a task fails.<br><br>Default value: 5 times |
||Retry interval |Sets the time interval between each retry after a task fails.<br><br>Default value: 10000 ms |
||Exception handling |Configure the handling policy when a task exception occurs.<br><br>The following two strategies are supported:<br><br>• **Terminate task:**  When an exception occurs, immediately terminate the execution of the current task and clear the intermediate results. This is the default option.<br><br>• **Ignore exceptions:**  When an exception occurs, ignore the error (populate the data with null) and continue with the next steps of the task. |
|Prompt word configuration |Model prompt word |A cue word used to specify a video understanding model, either directly using a template or a custom cue word.<br><br><br>* The default template includes video marking, content synopsis, breaking point analysis, plot analysis, and tag extraction.<br><br>* Support enter a video address in the **input test** and test to see if the test results meet expectations.<br><br><br>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/805c915e6b274cdc9a76ed20153bb2bd~tplv-goo7wpa0wc-image.image) |
|Output Configuration |Output field |Custom output fields. |

### Step 3: Test execution

After completing the operator configuration, the operator will automatically execute and output a data preview. You need to wait for the operator to execute and view the data preview results.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b77f60cad63b42c791fc3deaac88f490~tplv-goo7wpa0wc-image.image)

Of which:

* Support Terminate Execution: Click **Termination of execution** in the upper right corner of the **data preview** area.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/995e4b2bcc0045049ab600647046b1f7~tplv-goo7wpa0wc-image.image)

* After terminating execution, support for re\-execution.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b38b3aac46eb42f7abe72e48397444af~tplv-goo7wpa0wc-image.image)

You can also click **Test Execution** to view the output in the Test Execution Results column.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31331e34a1d8468eb4baa4b6985f482c~tplv-goo7wpa0wc-image.image)

## **Video keyframe extraction**

### Step 1: Create a new **video key frame extraction** operator

1. In the left navigation bar of Enterprise Knowledge Engine, select **Data Access** \> **Visual Knowledge Processing**.

2. In the upper left corner of the **Task List** page, click **Create** and select **Create Offline Task**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f98dcae6042b4f5096406ec06d08d3db~tplv-goo7wpa0wc-image.image)

3. Follow the steps in [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task), and when processing the node, select Add operators from Video Processing for data connections.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d19ae0305d07462da747264f6de232c3~tplv-goo7wpa0wc-image.image)

### Step 2: Configuring the Operator

1. Click "Video Keyframe Extraction" and configure relevant parameters on the basic information page.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/388aa001dda64148b6d5fcc73af3a2e6~tplv-goo7wpa0wc-image.image)

2. **Input configuration**

In the **input configuration** area, you need to specify the source of the video to be processed.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/45749dc9b88443e1acc8d896a2dbc1f2~tplv-goo7wpa0wc-image.image)

|Configuration item |Description |
|---|---|
|**Select input type** |You can choose the file URL address or the file base64\-bit encoding.<br><br><br>* **URL:**  If your video file is stored in the cloud and accessed via URL<br><br>* **File:**  If you wish to upload local video files directly for processing |
|**Specify video field** |This is required when the **input type** is **URL**. From the drop\-down list of **video fields**, select the field that contains the video URL in the input data. The system will read the URL from this field for processing. |

3. **Frame extraction configuration**

In the **frame extraction configuration** area, you can set specific rules for video frame extraction (i.e. screenshots) to control the frequency and number of screenshots.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcc8bf5ce6e54a5887e3ebc0009be9a8~tplv-goo7wpa0wc-image.image)

|Parameter |Description |
|---|---|
|**Frame draw interval** |Set the time interval for capturing video frames in seconds, default: 1. |
|**Maximum frame number** |Sets the maximum frame number taken from the video. Default value: 100. |
|**Output format** |Select the format of the output image. Support both JPG and PNG formats. |
|**Output size** |Sets the width and height of the output image in pixels. If set to 0 x 0, the size of the output image will remain the same as the original video |

4. **Storage Configuration**

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dd03dc720d5d4ae989202b0aa685f978~tplv-goo7wpa0wc-image.image)

**S3 storage path:**  Sets the path of the file in S3 storage. Example value: `frames`

**URL valid period:**  Sets the valid time of the resulting URL generated. The unit is seconds. Example value: `604800`

5. **Advanced Configuration**

Click "Advanced Configuration" to configure the concurrency of task execution and exception handling strategy. The specific parameters can be configured as follows:

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0f7fa8ea5a4945c4a326be7cdbc74f87~tplv-goo7wpa0wc-image.image)

**Video Processing Concurrency:**  Sets the number of concurrent tasks for video processing. This configuration is required.

**Upload concurrency:**  Set the number of concurrent tasks to upload.

**Exception Handling:**  Sets the handling method when an exception is encountered during processing. This configuration is required. You can choose from the following two options:

* **Ignore:**  Ignore the exception and continue with the follow\-up process.

* **Throw:**  Throws an exception upwards to interrupt the current process.

6. **Output Configuration**

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8755833699a64ac592b1cb63f7e34c66~tplv-goo7wpa0wc-image.image)

Output field: The output field can be customized, the first space is not supported, and the rest are supported, no more than 64 words. Sets the name of the field that contains the frame URL in the output. Example values: `frame_urls`

### Step 3: Test execution

Click "Test Execution" to view the output results in the "Test Execution Results" column.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d64124e68d774141a9094c7e2f60fdb9~tplv-goo7wpa0wc-image.image)

## Audio & video information fusion

### Step 1: Create a new audio & video fusion operator

1. In the left navigation bar of Enterprise Knowledge Engine, select **Data Access** \> **Visual Knowledge Processing**.

2. In the upper left corner of the **Task List** page, click **Create** and select **Create Offline Task**.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b4c97a1a6cb4333834c5db73b50729d~tplv-goo7wpa0wc-image.image)

3. Follow the steps in [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task) and select Add Audio & Video Fusion operator from Video Processing for data connection while processing nodes.

   > **说明**

   > The "audio & video information fusion" operator has two inputs, corresponding to the audio result input and the video image result input.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/eeaff87a81bc4abebf84747ca14f0393~tplv-goo7wpa0wc-image.image)

### Step 2: Configuring the Operator

Click the **audio & video information fusion** operator in the process canvas and complete the following configuration.

* Connection configuration on the left side of the page:

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7a7f1dcffd7449bda8c1357563f594a6~tplv-goo7wpa0wc-image.image)

   |**Parameter** |**Description** |
   |---|---|
   |Connection method |Set the input connection method, support selection:<br><br><br>* **Left connection:**  The left input is the main one, and the right input is fused to the left according to the timestamp.<br><br>* **Right connection:**  The right input is the main input, and the left input is fused to the right according to the timestamp.<br><br>* **Internal connection:**  Fusion only occurs when both left and right inputs have data at the same time period.<br><br>* **Fully connected:**  Retains all the data for the left and right inputs. |
   |Connection field |Set the connection field relationship of left and right input, support selection:<br><br><br>* **Auto Match:**  The system automatically matches the connection fields.<br><br>* **Custom:**  You set the fields you want to connect to. |

* Fusion configuration on the right side of the page:

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40707d649f6d4db4ab25bcfe9c2a7b5a~tplv-goo7wpa0wc-image.image)

   |**Module** |**Parameter** |**Description** |
   |---|---|---|
   |Model information |Model selection |Choosing a large model is supported if the enterprise administrator has configured the large model for the operator (see **Prerequisites** above for details). You can also choose to **customize the model** and complete the model related configuration. |
   ||Model call address |The calling address of the application. |
   ||Inference access point |The general format is `ep-xxxxxxxxxx-yyyy`, and the creation method refers to [creating a custom inference access point ](https://www.volcengine.com/docs/82379/1099522). |
   ||API Key |The general format is `xxxxxxxx-yyyy-xxxx-yyyy-xxxxxxxxxxxx`, and the acquisition method refers to [obtaining API Key and configuring it ](https://www.volcengine.com/docs/82379/1263279). |
   |Fusion configuration |ASR result column |Sets the audio recognition result column. |
   ||Video understanding result column |Sets the image result column for the video. |
   ||Fusion cue word |Customize audio & video fusion hints, specify fusion rules, output field format requirements, and more. |
   |Advanced Settings |Concurrent size |Sets the number of tasks to process concurrently. |
   ||Timeout |Sets the timeout for task processing in milliseconds (ms). |
   ||Number of retries |Sets the number of automatic retries after a task fails. |
   ||Retry interval |Sets the time interval between each retry after a task fails. |
   ||Exception handling |Configure the handling policy when a task exception occurs.<br><br>The following two strategies are supported:<br><br><br>* **Terminate task:**  When an exception occurs, immediately terminate the execution of the current task and clear the intermediate results. This is the default option.<br><br>* **Ignore Exception:**  When an exception occurs, ignore the error (padding the data with null) and continue with the next steps of the task. |
   |Output Configuration |Output field |Custom output fields. |

* Output fields on the right side of the page: Select the fields you want to enter in the field list, and you can view the field name, original name, type, and source of each field.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/173011ee1cf041a6bea125c0b1fecfba~tplv-goo7wpa0wc-image.image)

### Step 3: Test execution

After completing the operator configuration, the operator will automatically execute and output a data preview. You need to wait for the operator to execute and view the data preview results.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17ad10a46d4147538cf53299a00d829b~tplv-goo7wpa0wc-image.image)

Of which:

* Support Terminate Execution: Click **Terminate Execution** in the upper right corner of the **data preview** area.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/460946ac42c24d5fba5501acc7ec48ac~tplv-goo7wpa0wc-image.image)

* After terminating execution, support for re\-execution.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/904b2f114d334b5e8eae6dd030021015~tplv-goo7wpa0wc-image.image)

* Click **Cleaning Suggestions**, you can select columns and perform one\-click cleaning according to the suggestions and reasons given by the system.

   ![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21d707aa49c74991a9161707ef7e8d02~tplv-goo7wpa0wc-image.image)

You can also click **Test Execution** to view the output in the Test Execution Results column.

![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7e3cbfc3343477aa736516eea660be8~tplv-goo7wpa0wc-image.image)
