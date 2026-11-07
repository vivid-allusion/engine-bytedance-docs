---
title: "AI-Vectorized Model"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/AI-Vectorized_Model"
---

<span id="8836742a"></span>
# Feature Overview

AI\-vectorized models can transform unstructured data such as text and images into numerical vectors that can be understood by machines, and are a key "bridge" to connect unstructured data with downstream AI applications (especially in scenarios such as retrieval, question answering, and recommendation). This article will show you how to use the vectorized model operator.

<span id="2985421d"></span>
# Prerequisite

The enterprise administrator has configured the large model for the operator, see details [Configure Large Model Invocation](https://docs.byteplus.com/docs/dataagent/Configure_Large_Model_Invocation).

<span id="a4ff4c6e"></span>
# Operator Introduction

<span id="9148a1a3"></span>
## **Doubao Text Vectorization**

The Doubao text vectorization operator can convert text into a vector that expresses the semantics of the text (supports both Chinese and English), and calculate the semantic gap between the texts by calculating the vector. Perform natural language processing tasks such as text classification, clustering, retrieval, and generation in scenarios such as retrieval, personalized recommendation, and intelligent dialogue.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb49f080f0f94ad38faf2e2e3ec4b2dd~tplv-goo7wpa0wc-image.image) </span>


1. Click + and select **AI\-vectorization model \> Doubao text vectorization** operator.

2. Setting model information: Select model, support selecting existing models set in advanced configuration or selecting custom models. Custom models require model call addresses, inference access points, and API keys

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f3b6b69dc2d54e0e85687860e6b79db1~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Model |Choosing a large model is supported if the enterprise administrator has configured the large model for the operator (see **Prerequisites** above for details). You can also choose to **customize the model** and complete the model related configuration. |
   |Model call address |The calling address of the application. |
   |Inference access point |The general format is `ep-xxxxxxxxxx-yyyy`, and the creation method refers to [creating a custom inference access point ](https://www.volcengine.com/docs/82379/1099522). |
   |API Key |The general format is `xxxxxxxx-yyyy-xxxx-yyyy-xxxxxxxxxxxx`, and the acquisition method refers to [obtaining API Key and configuring it ](https://www.volcengine.com/docs/82379/1263279). |
   

3. Configure vectorization related information.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7e81d19c4ad40cdb9b9b70d9bf0490f~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Explain |
|---|---|
|Input field |Select one or more input fields to be vectorized, and select upstream output fields. |
|Vectorized format |Drop down the radio selection, you can choose two options: float and base64, and float is selected by default. |
|Dimension |Drop down single selection, choose 2560, 2048, 1024, 786, 512. |
|Custom parameters |Support for setting custom parameters, including parameter values and parameter names. |



4. Set the relevant parameters in the advanced settings.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ddd0e9577514c988fa9721a2da1bf3c~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Configuration instructions |
|---|---|
|Parallelism |The number of parallelizations requested, the number of parallelizations actually executed, and the resources available to the cluster are also relevant. It is recommended that the user compute the parallelism reasonably according to the interface performance of the call (QPS, QPM, etc.). |
|Timeout |Large model calculation timeout in milliseconds ms |
|Number of retries |The number of automatic retries when a request fails, in times |
|Request interval |Large model access points generally have an RPM (number of requests per minute) limit, and the request interval is set on demand according to the value of the RPM, in milliseconds ms<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The request interval is set to avoid errors in large models with limited viewership of interfaces. The general error information is as follows</div><br><br><br><div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/651d2f86502d49c0946e7616c14f2204~tplv-goo7wpa0wc-image.image" width="820px" /></div><br> |
|Complete exception handling |* Terminate the task: If the inference fails, the task fails, and the intermediate results are cleared<br><br>* Ignore Exceptions: Tolerant mode, ignore data where inference fails, use null padding, and preserve results where inference succeeds |



5. Configure the output.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f738d12f62c54f258dcc9b873a5cfe1e~tplv-goo7wpa0wc-image.image) </span>


* Output field: User\-defined output field name, field type default is array < float \> field type, a string of vectors.

* The output of this operator = the output field of the previous node + the new vectorization result field of this operator.


<span id="ca13706a"></span>
## **Doubao Multimodal Vectorization Model**

Vectorization technology that supports mixed input of text, images, and video (supported by some models). The model can convert different types of data into vector representation, which is suitable for text search, image search, mixed image search and other scenarios. By Doubao\-embedding\-vision model, users can achieve unified vectorization of multimodal data, which is convenient for processing and analyzing cross\-modal data to achieve more efficient information retrieval and data analytics.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/caadf5bbaadf45a5b8480a23a6d61232~tplv-goo7wpa0wc-image.image) </span>


1. Click + and select **AI\-Vectorization Model \> Doubao Multimodal Vectorization** Operator.

2. Setting model information: Select model, support selecting existing models set in advanced configuration or selecting custom models. Custom models require model call addresses, inference access points, and API keys.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b4c0469cc3da4455954cef4689ea071e~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Model |Choosing a large model is supported if the enterprise administrator has configured the large model for the operator (see **Prerequisites** above for details). You can also choose to **customize the model** and complete the model related configuration. |
   |Model call address |The calling address of the application. |
   |Inference access point |The general format is `ep-xxxxxxxxxx-yyyy`, and the creation method refers to [creating a custom inference access point ](https://www.volcengine.com/docs/82379/1099522). |
   |API Key |The general format is `xxxxxxxx-yyyy-xxxx-yyyy-xxxxxxxxxxxx`, and the acquisition method refers to [obtaining API Key and configuring it ](https://www.volcengine.com/docs/82379/1263279). |
   

3. Configure vectorization related information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8b21af80653244f38ca6b1a39c7b5228~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Explain |
   |---|---|
   |Input mode |Radio, optional content or file. |
   |Input field |Based on the actual output fields of the upstream operator, select the fields that need to be extracted.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Input mode When selecting file, the input field must select file_ref.</div><br> |
   |Vectorized format |Drop down the radio selection, you can choose two options: float and base64, and float is selected by default. |
   |Vector dimension |Drop down the radio, choose 2048, 1024, and choose 2048 by default. |
   

4. Set the relevant parameters in the advanced settings.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fbeb56ce083f4149b64e796b5d3525e2~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Configuration instructions |
|---|---|
|Parallelism |The number of parallelizations requested, the number of parallelizations actually executed, and the resources available to the cluster are also relevant. It is recommended that the user compute the parallelism reasonably according to the interface performance of the call (QPS, QPM, etc.). |
|Timeout |Large model calculation timeout in milliseconds ms |
|Number of retries |The number of automatic retries when a request fails, in times |
|Request interval |Large model access points generally have an RPM (number of requests per minute) limit, and the request interval is set on demand according to the value of the RPM, in milliseconds ms<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The request interval is set to avoid errors in large models with limited viewership of interfaces. The general error information is as follows</div><br><br><br><div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/651d2f86502d49c0946e7616c14f2204~tplv-goo7wpa0wc-image.image" width="820px" /></div><br> |
|Complete exception handling |* Terminate the task: If the inference fails, the task fails, and the intermediate results are cleared<br><br>* Ignore Exceptions: Tolerant mode, ignore data where inference fails, use null padding, and preserve results where inference succeeds |



5. Configure the output.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fde5d1f1fa964f6da88ab54073c62d34~tplv-goo7wpa0wc-image.image) </span>


* User\-defined output field name, field type default is array < float \> field type, a string of vectors.

* The output of this operator = the output field of the previous node + the new vectorization result field of this operator.


<span id="1e9c4dde"></span>
## Qwen Text Vectorization Model

Transform the text into a vector that expresses the semantics of the text, and calculate the semantic gap between the texts by computing the vector. Perform natural language processing tasks such as text classification, clustering, retrieval, and generation in scenarios such as retrieval, personalized recommendation, and intelligent dialogue.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f0df6a67419040c2b671c2ff85ea21f2~tplv-goo7wpa0wc-image.image) </span>


1. Click + and select **AI\-vectorized model \> Qwen text vectorized model** operator.

2. Setting model information: Select model, support selecting existing models set in advanced configuration or selecting custom models. Custom models require model call addresses, inference access points, and API keys.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/deff37ba4b6d4ab8b5d087266d3674c2~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Configuration instructions |
|---|---|
|Model |Choosing a large model is supported if the enterprise administrator has configured the large model for the operator (see **Prerequisites** above for details). You can also choose to **customize the model** and complete the model related configuration. |
|Model call address |The calling address of the application. |
|Inference access point |The general format is `ep-xxxxxxxxxx-yyyy`, and the creation method refers to [creating a custom inference access point ](https://www.volcengine.com/docs/82379/1099522). |
|API Key |The general format is `xxxxxxxx-yyyy-xxxx-yyyy-xxxxxxxxxxxx`, and the acquisition method refers to [obtaining API Key and configuring it ](https://www.volcengine.com/docs/82379/1263279). |



3. Configure vectorization related information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e8940e8601b644b5b9c4fc973b5fdf40~tplv-goo7wpa0wc-image.image) </span>

   * Input fields: drop\-down radio selection, you can select upstream output fields, only string, array < string \> type fields can be selected.

   * Vectorization format: drop\-down radio selection, only float can be selected, and float is selected by default.

   * Vector dimension: Support the vector dimension as shown in the figure. The default vector dimension supported by different models is inconsistent. Here, it is not included in the custom parameters.

4. Set the relevant parameters in the advanced settings.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c364abe23c48492d912609d80738c4c5~tplv-goo7wpa0wc-image.image) </span>


|Parameter |Configuration instructions |
|---|---|
|Parallelism |The number of parallelizations requested, the number of parallelizations actually executed, and the resources available to the cluster are also relevant. It is recommended that the user compute the parallelism reasonably according to the interface performance of the call (QPS, QPM, etc.). |
|Timeout |Large model calculation timeout in milliseconds ms |
|Number of retries |The number of automatic retries when a request fails, in times |
|Request interval |Large model access points generally have an RPM (number of requests per minute) limit, and the request interval is set on demand according to the value of the RPM, in milliseconds ms<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The request interval is set to avoid errors in large models with limited viewership of interfaces. The general error information is as follows</div><br><br><br><div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/651d2f86502d49c0946e7616c14f2204~tplv-goo7wpa0wc-image.image" width="820px" /></div><br> |
|Complete exception handling |* Terminate the task: If the inference fails, the task fails, and the intermediate results are cleared<br><br>* Ignore Exceptions: Tolerant mode, ignore data where inference fails, use null padding, and preserve results where inference succeeds |



5. Configure the output.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a40072e592014ee7a20de572adbc9c05~tplv-goo7wpa0wc-image.image) </span>

   * User\-defined output field name, field type default is array < float \> field type, a string of vectors.

   * The output of this operator = the output field of the previous node + the new vectorization result field of this operator.


<span id="53c53abc"></span>
## Qwen Multimodal Vectorization Model

Multimodal vectorization models generate continuous vectors based on user input, which can be text, images, or videos. Suitable for video classification, image classification, graphic retrieval, text/image search, text/image search video and other task scenarios.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/787d91647102491c93caab4ef3025c13~tplv-goo7wpa0wc-image.image) </span>


1. Click + and select **AI\-vectorized model \> Qwen multimodal vectorized model** operator.

2. Setting model information: Select model, support selecting existing models set in advanced configuration or selecting custom models. Custom models require model call addresses, inference access points, and API keys.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c0f51dcfd15a4fc1893ddc7051bf752c~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Model |Choosing a large model is supported if the enterprise administrator has configured the large model for the operator (see **Prerequisites** above for details). You can also choose to **customize the model** and complete the model related configuration. |
   |Model call address |The calling address of the application. |
   |Inference access point |The general format is `ep-xxxxxxxxxx-yyyy`, and the creation method refers to [creating a custom inference access point ](https://www.volcengine.com/docs/82379/1099522). |
   |API Key |The general format is `xxxxxxxx-yyyy-xxxx-yyyy-xxxxxxxxxxxx`, and the acquisition method refers to [obtaining API Key and configuring it ](https://www.volcengine.com/docs/82379/1263279). |
   

3. Configure vectorization related information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/701fa0a5b0e04d7b8dda2ab61583ce3d~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Explain |
   |---|---|
   |Input mode |There are two modes, you can choose content or file. |
   |Input field |Based on the actual output fields of the upstream operator, select the fields that need to be extracted.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Input mode When selecting file, the input field must select file_ref.</div><br> |
   |Vectorized format |Drop down the radio selection, only float can be selected, and float is selected by default. |
   |Vector dimension |Support the vector dimension as shown in the figure, the default vector dimension supported by different models is inconsistent, and it is not included in the custom parameters here. |
   

4. Set the relevant parameters in the advanced settings.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1bff031e773f426a9051b72ea7e9ea5a~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Parallelism |The number of parallelizations requested, the number of parallelizations actually executed, and the resources available to the cluster are also relevant. It is recommended that the user compute the parallelism reasonably according to the interface performance of the call (QPS, QPM, etc.). |
   |Timeout |Large model calculation timeout in milliseconds ms |
   |Number of retries |The number of automatic retries when a request fails, in times |
   |Request interval |Large model access points generally have an RPM (number of requests per minute) limit, and the request interval is set on demand according to the value of the RPM, in milliseconds ms<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The request interval is set to avoid errors in large models with limited viewership of interfaces. The general error information is as follows</div><br><br><br><div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/651d2f86502d49c0946e7616c14f2204~tplv-goo7wpa0wc-image.image" width="820px" /></div><br> |
   |Complete exception handling |* Terminate the task: If the inference fails, the task fails, and the intermediate results are cleared<br><br>* Ignore Exceptions: Tolerant mode, ignore data where inference fails, use null padding, and preserve results where inference succeeds |
   

5. Configure the output.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6d3c195209f1471c9bae454220cf35c1~tplv-goo7wpa0wc-image.image) </span>

   * User\-defined output field name, field type default is array < float \> field type, a string of vectors.

   * The output of this operator = the output field of the previous node + the new vectorization result field of this operator.


<span id="20e4880b"></span>
## BGE\-M3 Text Vectorization Model

BGE\-M3 is a "multi\-language, multi\-function, multi\-granularity" unified text embedding model, optimized based on XLM\-RoBERTa, and supports three retrieval paradigms: dense, sparse, and multi\-vector, covering 100 + languages. It can handle short sentences to 8192 token long documents, and continues to lead the C\-MTEB/MTEB multi\-language list.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b707a1b610fb4b2fa53948f5764105d3~tplv-goo7wpa0wc-image.image) </span>


1. Click + and select **AI\-Vectorized Model \> BGE\-M3 Text Vectorized Model** Operator.

2. Setting model information: Select model, support selecting existing models set in advanced configuration or selecting custom models. Custom models require model call addresses, inference access points, and API keys.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/038532b9e1bb41ffa8b62e934e11a199~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Model |Choosing a large model is supported if the enterprise administrator has configured the large model for the operator (see **Prerequisites** above for details). You can also choose to **customize the model** and complete the model related configuration. |
   |Model call address |The calling address of the application. |
   |Inference access point |The general format is `ep-xxxxxxxxxx-yyyy`, and the creation method refers to [creating a custom inference access point ](https://www.volcengine.com/docs/82379/1099522). |
   |API Key |The general format is `xxxxxxxx-yyyy-xxxx-yyyy-xxxxxxxxxxxx`, and the acquisition method refers to [obtaining API Key and configuring it ](https://www.volcengine.com/docs/82379/1263279). |
   

3. Configure vectorization related information.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9f907f97526847bc9b80c7f78e4e6eb4~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Explain |
   |---|---|
   |Input field |Drop down the radio, you can select the upstream output field, you can only select the string, array type field. |
   |Vectorized format |Drop down the radio selection, only float can be selected, and float is selected by default. |
   |Vector dimension |Support the vector dimension as shown in the figure, the default vector dimension supported by different models is inconsistent, and it is not included in the custom parameters here. |
   |Custom parameters |Support user\-defined parameters, parameter names and parameter values need to be set. |
   

4. Set the relevant parameters in the advanced settings.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f616d0a0fb454587bfccfcfb36791b43~tplv-goo7wpa0wc-image.image) </span>

   
   |Parameter |Configuration instructions |
   |---|---|
   |Parallelism |The number of parallelizations requested, the number of parallelizations actually executed, and the resources available to the cluster are also relevant. It is recommended that the user compute the parallelism reasonably according to the interface performance of the call (QPS, QPM, etc.). |
   |Timeout |Large model calculation timeout in milliseconds ms |
   |Number of retries |The number of automatic retries when a request fails, in times |
   |Request interval |Large model access points generally have an RPM (number of requests per minute) limit, and the request interval is set on demand according to the value of the RPM, in milliseconds ms<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The request interval is set to avoid errors in large models with limited viewership of interfaces. The general error information is as follows</div><br><br><br><div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/651d2f86502d49c0946e7616c14f2204~tplv-goo7wpa0wc-image.image" width="820px" /></div><br> |
   |Complete exception handling |* Terminate the task: If the inference fails, the task fails, and the intermediate results are cleared<br><br>* Ignore Exceptions: Tolerant mode, ignore data where inference fails, use null padding, and preserve results where inference succeeds |
   

5. Configure the output.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2ecc2bf2b4ab453797d8a573bc10e899~tplv-goo7wpa0wc-image.image) </span>

   * You can customize the output field name, and the field type defaults to the array < float \> field type.

   * The output of this operator = the output field of the previous node + the new vectorization result field of this operator.
