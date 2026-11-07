---
title: "Image Processing"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Image_Processing"
---

Image processing operators are used to realize image character recognition, key information extraction and other functions. Through this article, you can learn about the capabilities and usage of the various operators included in the image processing module.

<span id="865ab9cd"></span>
# Prerequisite

The enterprise administrator has configured the large model for the operator, see details [Configure Large Model Invocation](https://docs.byteplus.com/docs/dataagent/Configure_Large_Model_Invocation).

<span id="9753af15"></span>
# Introduction to Image Processing Operators


1. **Image OCR\-Qwen**


Support for recognizing text information in images, provide text recognition results, languages and other key information, and provide solutions for image text recognition and extraction in multilingual scenarios.


2. **Image OCR\-Doubao**


Multilingual OCR service supports text recognition capabilities in 50 + languages such as Chinese, English, Japanese, French, German, Russian, and Spanish. Provide a variety of key information such as text recognition results and languages, and provide solutions for image text recognition and extraction in multilingual scenarios.

<span id="607cea18"></span>
# Operation steps

<span id="c470ce5c"></span>
## Image OCR\-Qwen

<span id="a9b86b8f"></span>
### Step 1: Create a new image OCR\-Qwen operator


1. In the left navigation bar of Enterprise Knowledge Engine, select **Data Access** \> **Visual Knowledge Processing** .

2. In the upper left corner of the **Task List** page, click **New** and select **New Offline Task** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/821d810fbdc5401db4b70e11a6f708a8~tplv-goo7wpa0wc-image.image) </span>

3. Follow [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task)the steps in Create Offline Task and select Add Image OCR\-Qwen operator from Image Processing for data connection while processing nodes.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4795f7da8e034b809eae6352aeea4924~tplv-goo7wpa0wc-image.image) </span>


<span id="2ce2bebf"></span>
### The second step: configuring the operator

Click "Image Processing OCR\-Qwen", and on the basic information page, configure the relevant parameters.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/85f8761028834cfab9fcd225ff4acfbe~tplv-goo7wpa0wc-image.image) </span>


1. **Model information**

   
   |parameter |configuration instructions |
   |---|---|
   |model selection |Choosing a large model is supported if the enterprise administrator has configured the large model for the operator (see **Prerequisites** above for details). You can also choose to **customize the model** and complete the model related configuration. |
   |model call address |The calling address of the application |
   |inference access point |General format is `ep-xxxxxxxxxx-yyyy`, create method reference [Create custom inference access point](https://www.volcengine.com/docs/82379/1099522) |
   |API Key |The general format is `xxxxxxxx-yyyy-xxxx-yyyy-xxxxxxxxxxxx`, and the acquisition method is referred to [Get API Key and configure](https://www.volcengine.com/docs/82379/1263279) |
   

2. **Handle configuration**

   \*\*Input Mode \*\*: Select the source mode for the input data.

   The following two modes are supported:

   * **Url** : Enter the URL of the online file.

   * **File** : Upload a local file.

      \*\*Input field \*\*: According to the actual output field of the upstream operator, select the field that needs to be extracted.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Input mode When selecting file, the input field must select file_ref.   </div>
   

3. **Language recognition configuration**

   Drop down the radio, support search, and select the optional language according to the technology selection. Chinese and English are currently supported.

4. **Advanced Settings**

   The relevant parameters are described as follows:

   
   |**parameter** |**explain** |
   |---|---|
   |concurrent size |Sets the number of tasks to process concurrently.<br><br>Default value: 10 |
   |timeout |Sets the timeout for task processing in milliseconds (ms).<br><br>Default value: 180000 ms |
   |retry interval |Sets the number of automatic retries after a task fails.<br><br>Default value: 3 times |
   |exception handling |Configure the handling policy when a task exception occurs.<br><br>The following two strategies are supported:<br><br>• **Terminate task** : When an exception occurs, immediately terminate the execution of the current task. This is the default option.<br><br>• **Ignore exceptions** : When an exception occurs, ignore the error and continue with the next steps of the task. |
   

5. **Output Configuration**

   \*\*Output field \*\*: Specifies the name of the output field used to store the recognition result. User\-defined output fields do not support the first space, and the rest are supported, no more than 64 characters.


<span id="50c0e6e1"></span>
### Step 3: Test execution

Click **Test Execution** to view the output in the Test Execution Results column.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d361732d1c1e451ead049a1a282029b7~tplv-goo7wpa0wc-image.image) </span>

<span id="589af667"></span>
## Image OCR\-Doubao

<span id="3d789243"></span>
### Step 1: Create a new image OCR\-Doubao operator


1. In the left navigation bar of Enterprise Knowledge Engine, select **Data Access** \> **Visual Knowledge Processing** .

2. In the upper left corner of the **Task List** page, click **New** and select **New Offline Task** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/821d810fbdc5401db4b70e11a6f708a8~tplv-goo7wpa0wc-image.image) </span>

3. Follow [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task)the steps in Create Offline Task and select Add Image OCR\-Doubao operator from Image Processing for data connection while processing nodes.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7d7f8d8d22c24f73b1051e7e54aab4dc~tplv-goo7wpa0wc-image.image) </span>


<span id="bd7f6723"></span>
### The second step: configuring the operator

Click on the "Image OCR\-Doubao" operator in the process canvas and complete the following configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9e4bcf9ff764c649fb579eb6a749139~tplv-goo7wpa0wc-image.image) </span>


|**module** |**parameter** |**explain** |
|---|---|---|
|model information |model selection |Choosing a large model is supported if the enterprise administrator has configured the large model for the operator (see **Prerequisites** above for details). You can also choose to **customize the model** and complete the model related configuration. |
||Access Key ID and Secret Access Key |The access key (AK/SK) of the Volcano Engine account that has opened the image recognition and understanding service. Please refer to the operation guide:<br><br><br>* [Open image recognition and understanding services](https://www.volcengine.com/docs/86081/1660346?lang=zh)<br><br>* [API Access Key Management](https://www.volcengine.com/docs/6291/65568?lang=zh) |
|handle configuration |input mode |Select the video input source mode.<br><br><br>* \*\*Url \*\*: Enter the URL of the online file.<br><br>* **File** : Upload a local file. |
||input field |Based on the actual output fields of the upstream operator, select the fields that need to be extracted.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Input mode When selecting file, the input field must select file_ref.</div><br> |
|image recognition configuration |Text recognition mode |Support for selecting any of the following modes:<br><br><br>* **Default mode** : directly recognize the text line, identify a line and output a line.<br><br>* **Text block mode** : After recognizing the text line, the semantic coherent text is synthesized into sentences or paragraphs and then output. |
||confidence score |Set a confidence level threshold below which lines of text will be filtered out. The range of values is 0 to 100. |
|Advanced Settings |concurrent size |Sets the number of tasks to process concurrently.<br><br>Default value: 10 |
||timeout |Sets the timeout for task processing in milliseconds (ms).<br><br>Default value: 180000 ms |
||number of retries |Sets the number of automatic retries after a task fails.<br><br>Default value: 3 times |
||retry interval |Sets the time interval between each retry after a task fails.<br><br>Default value: 100 ms |
||exception handling |Configure the handling policy when a task exception occurs.<br><br>The following two strategies are supported:<br><br>• **Terminate task** : When an exception occurs, immediately terminate the execution of the current task and clear the intermediate results. This is the default option.<br><br>• **Ignore exceptions** : When an exception occurs, ignore the error (populate the data with null) and continue with the next steps of the task. |
|Output Configuration |output content |Support for selecting **Final Text** or **Final Text + Details** . Defaults to the **final text** . |
||output field |Custom output fields. |


<span id="c54a03ec"></span>
### Step 3: Test execution

After completing the operator configuration, the operator will automatically execute and output a data preview. You need to wait until the execution is complete to view the data preview results.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6c7cc3566f74808ad1b6dc93fb5ceca~tplv-goo7wpa0wc-image.image) </span>

Of which:


* Support Terminate Execution: Click **Terminate Execution** in the upper right corner of the **data preview** area.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fbff53d2b4f4af2a4c9e3bd1d8cf3f6~tplv-goo7wpa0wc-image.image) </span>

* After terminating execution, support for re\-execution.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4c51eb6394834793948a73d0751efe7b~tplv-goo7wpa0wc-image.image) </span>


You can also click **Test Execution** to view the output in the Test Execution Results column.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f984f86bc41b44ef9d33b0053729c047~tplv-goo7wpa0wc-image.image) </span>
