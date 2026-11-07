---
title: "Volcano Ark Large Model"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Volcano_Ark_Large_Model"
---

The Volcano Ark model is an intelligent data processing tool in AI\-large model processing operator. It supports docking with Volcano Engine large model services, and realizes functions such as unstructured data analysis and multi\-language translation through custom model configuration, generation strategies, and role personas. It is suitable for enterprise data intelligent processing scenarios. This article shows you how to use the large model of Volcano Ark.

<span id="36026815"></span>
# **Feature Overview**

The Volcano Ark large model operator is connected to the Volcano Engine large model service, which can intelligently process the data stored in the TOS bucket, such as unstructured data analysis, foreign language translation, etc. Users can configure model parameters, generation modes, and role personas to achieve automated intelligent processing of data.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This function is a value\-added function. If you want to use this function, you can contact the Volcano Engine technical support staff for consultation. You can use it after purchasing and activating this function.</div>


<span id="250e98a5"></span>
# Prerequisite


* Users need to register a [BytePlus](https://www.byteplus.com/en/product/modelark) account in advance and open the Volcano Ark large model service.

* The user's data should be stored in the TOS bucket in advance, see [Object Storage Quick Start (console) ](https://docs.byteplus.com/en/docs/tos/docs-quick-start_1)or [Object Storage Quick Start (Python SDK) ](https://docs.byteplus.com/en/docs/tos/Quick-start-python-sdk).

* The enterprise administrator has configured the large model for the operator, see details [Configure Large Model Invocation](https://docs.byteplus.com/docs/dataagent/Configure_Large_Model_Invocation).


<span id="4ae864bf"></span>
# Operation Steps

<span id="d996f50d"></span>
## Step 1: Create a new Ark model operator


1. In the left navigation bar of Enterprise Knowledge Engine, select **Data Access** \> **Visual Knowledge Processing** .

2. In the upper left corner of the **Task List** page, click **New** and select **New Offline Task** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/821d810fbdc5401db4b70e11a6f708a8~tplv-goo7wpa0wc-image.image) </span>

3. Follow [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task)the steps in Create the offline task and select the Volcano Ark Large Model operator in AI\-Large Model Processing for the data connection when processing the node.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/233145cd07394e1297c7d54c970e9555~tplv-goo7wpa0wc-image.image) </span>


<span id="ecd1dce3"></span>
## Step 2: Set the model docking parameters

Click "Customize Volcano Ark Large Model" and set relevant parameters in the "Model Settings" pop\-up window.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/17c0998ae37d41379dc39aeec6529d8c~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73dd87162e324e97afbfbff60b99308c~tplv-goo7wpa0wc-image.image) </span>

The relevant parameters are described as follows:


|parameter |configuration instructions |
|---|---|
|model |Choosing a large model is supported if the enterprise administrator has configured the large model for the operator (see **Prerequisites** above for details). You can also choose to **customize the model** and complete the model related configuration. |
|model call address |If you choose a custom model, you need to configure the calling address of the application |
|inference access point |If you choose a custom model, you need to configure the inference access point. General format is `ep-xxxxxxxxxx-yyyy`, create method reference [Create custom inference access point](https://www.volcengine.com/docs/82379/1099522) |
|API Key |If you choose a custom model, you need to configure the API Key. The general format is `xxxxxxxx-yyyy-xxxx-yyyy-xxxxxxxxxxxx`, and the acquisition method is referred to [Get API Key and configure](https://www.volcengine.com/docs/82379/1263279) |
|enable batch inference |Large model operators can choose to perform batch inference during periodic execution, making the task run more stably and with cheaper resources<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/188cd30a336e42d1b9bf758018e38dfd~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Volcano Engine AccessKey: Request a security certificate for the Volcano Engine API, please refer to [Access Key Management](https://www.volcengine.com/docs/6291/65568)<br><br>* Volcano Engine SecreKey: Request a security certificate for the Volcano Engine API, please refer to [Access Key Management](https://www.volcengine.com/docs/6291/65568)<br><br>* TOS bucket: TOS bucket name, please refer to [Create bucket](https://www.volcengine.com/docs/6349/75024) |
|generative diversity |Supports four mode adjustments to generate randomness and Top P values to control the effects of large model operators.<br><br><br>* Exact Mode:<br><br>   * Strictly follow instructions to generate content<br><br>   * Suitable for situations where accuracy is required, such as official documents, code, etc<br><br>* Balance Mode:<br><br>   * Striking a balance between innovation and precision<br><br>   * Suitable for most everyday use cases, generating interesting but rigorous content<br><br>* Creative mode:<br><br>   * Inspire creativity and provide fresh and unique ideas<br><br>   * Suitable for situations that require inspiration and unique perspectives, such as brainstorming, creative writing, etc<br><br>* Custom mode:<br><br>   * Customize the generation method through advanced settings<br><br>   * According to demand, fine adjustment is made to achieve personalized optimization<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Generative randomness: A higher level makes the output of the model more diverse and innovative, while a lower level makes the output more compliant with instructions but less diverse. It is recommended not to adjust it at the same time as "Top p".</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Top p: Cumulative probability. The model generates the output by selecting the words with the highest probability until the total probability of these words accumulates to the top p value. This allows the model to choose only these high\-probability words, thus controlling the diversity of the output. It is recommended not to adjust at the same time as "generating randomness".</div><br> |


<span id="bbf7809f"></span>
## Step 3: Configure the model persona and reply logic

Support user\-defined character settings, functions, and workflows for large models.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/208e4e388d894a768ae0a106f5e539dc~tplv-goo7wpa0wc-image.image) </span>

Use natural language to fill in the character settings, functions and workflow of the large model. You can refer to the following content for custom configuration:

```JSON
# Role
You are a precise and efficient intelligent delivery address resolution assistant robot 
that can accurately and efficiently parse input address information into structured 
content. 
For any input address, the parsing result must be quickly and accurately returned in JSON format.{
  /** Province */
  "province": "string",
  /** City */
  "city": "string",
  /** District */
  "region": "string",
  /** Detailed Address */
  "address": "string",
  /** Recipient */
  "people": "string",
  /** Phone */
  "tel": "string"
}

## Skill
### Skill 1: address resolution
1. Carefully analyze the input address text and extract key information such as province, city, district, detailed address, recipient, and phone number.
2. For vague or incomplete address information, try to supplement and improve it through reasonable speculation and common address patterns.
 
## Restrictions:
- Only handle tasks related to express address resolution and refuse to handle other unrelated content.
- Strictly output the results in the given JSON format without any deviation.
- For unresolved or ambiguous address information, null can be output.  
```


<span id="f91dd3bb"></span>
## Step 4: Configure template variables

Support users to select upstream fields or system variables as template variables, embedded in the user input content, for example, using the upstream `content`field, enter "${content}" in the user input, the large model will process the `content`field content.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a49a178bac9442a99831b8cc0efb0f23~tplv-goo7wpa0wc-image.image) </span>

Include upstream fields and system variables.


* Upstream field: Use ${field name} to refer to the data in the upstream field, and use < ID \> to identify the input content type. For example, ${context} < text \> is used to refer to the data in the upstream content column and is of text type. The following logos are currently supported:

   
   |type |logo |
   |---|---|
   |Text |`<text>` |
   |picture |`<image>` |
   |Audio |`<audio>` |
   |video |`<video>` |
   |do not fill in the logo |The system default is `< text >` |
   

* System variables: Use ${system variable name} to refer to system variables, such as ${date}, which supports date addition and subtraction, such as ${date \- 1}, to represent the previous day.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">If the upstream field name is the same as the system variable, it will be overwritten by the system variable.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Make sure that images, audio, video, and URLs are accessible.   </div>
   


<span id="ab87552e"></span>
## Step 5: Configure user input

Configure user input as data postaction and sample content for field configuration test execution.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0c3b0ed1c39b433d84d6d763c056899d~tplv-goo7wpa0wc-image.image) </span>

<span id="ebd70036"></span>
## Step 6: Advanced Settings

Click "Advanced Settings" to set the relevant parameters.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d41656e6bc447c49e1f487dbe4fcf83~tplv-goo7wpa0wc-image.image) </span>

The relevant parameters are described as follows:


|parameter |configuration instructions |
|---|---|
|parallelism |The number of parallelizations requested, the number of parallelizations actually executed, and the resources available to the cluster are also relevant. It is recommended that the user compute the parallelism reasonably according to the interface performance of the call (QPS, QPM, etc.). |
|timeout |Large model calculation timeout in milliseconds ms |
|number of retries |The number of automatic retries when a request fails, in times |
|request interval |Large model access points generally have an RPM (number of requests per minute) limit, and the request interval is set on demand according to the value of the RPM, in milliseconds ms<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The request interval is set to avoid errors in large models with limited viewership of interfaces. The general error information is as follows</div><br><br><br><div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/651d2f86502d49c0946e7616c14f2204~tplv-goo7wpa0wc-image.image" width="820px" /></div><br> |
|complete exception handling |* Terminate the task: If the inference fails, the task fails, and the intermediate results are cleared<br><br>* Ignore Exceptions: Tolerant mode, ignore data where inference fails, use null padding, and preserve results where inference succeeds |


<span id="3e104a98"></span>
## Step 7: Test execution

Click "Test Execution" to view the output results in the "Test Execution Results" column.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50f733ef2fa147bc9048c8f79cf81977~tplv-goo7wpa0wc-image.image) </span>

<span id="04163733"></span>
## Step 8: Data Postconfiguration

Check "Data Post\-operation" to perform some processing on the data based on the output results of the large model (API). Click "Test Execution" to test the results of the data post\-operation, which can be viewed in the "Test Execution Results" column.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6b750fc1049e4aeca87461898c6546d1~tplv-goo7wpa0wc-image.image) </span>

For example: through the **human and reply logic** function can make the large model output JSON format data, then write the code to process the JSON string as a JSON object, so as to facilitate the use in the field settings.

```Groovy
def jsonSlurper = new JsonSlurper()
return jsonSlurper.parseText(response.data.choices[0].message.content)
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/583ee25547cf40cabcb4d0073fa330ae~tplv-goo7wpa0wc-image.image) </span>

For example: through the **human set and reply logic** function can make the large model output JSON format data, then write the code to process the JSON string as a JSON object, which is easy to use in the field settings

```Groovy
def jsonSlurper = new JsonSlurper()
return jsonSlurper.parseText(response.data.choices[0].message.content)
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After enabling [Batch Reasoning], [Data Post\-Operation] will be automatically enabled, but the code cannot be customized.</div>


<span id="3c6438a3"></span>
## Step 9: Field Settings

Configure fields, parse paths, and field types based on test execution results to structure output data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3afbe3b9f1cc4447aca36573612cb823~tplv-goo7wpa0wc-image.image) </span>

<span id="a281b5de"></span>
# Reference: Example of usage scenarios

<span id="0c568847"></span>
## 1. Foreign language translation robot

Translate all non\-Chinese text into Chinese


* Character and Reply Logic

   ```Java
   # Role
   You are a professional foreign language translation robot responsible for accurately translating various foreign language content into Chinese.
   
   ## Goal
   Translate the input foreign text content into Chinese.
   
   ## Skills
   1. Proficient in grammar, vocabulary, and language habits of multiple foreign languages.
   2. Be able to accurately understand the meaning of foreign texts and translate them into content that conforms to Chinese language habits.
   3. Be able to accurately translate professional terminology and domain specific vocabulary.
   
   ## Restrictions
   1. Only perform translation work from foreign languages to Chinese, without any other operations.
   2. Ensure the translation content is accurate, fluent, and in line with Chinese expression habits.
   3. For vocabulary or sentences whose exact meaning cannot be determined, reasonable inference should be made based on the context as much as possible, and uncertainty should be noted in the translation.
   ```
   

* User interface example

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61171377a53a41d3a9d876a058aeb3fd~tplv-goo7wpa0wc-image.image) </span>


<span id="4c789cb1"></span>
## 2. Address resolution robot

Parse unstructured address data into structured data


* Character and Reply Logic

   ```Java
   # Role
   You are a precise and efficient intelligent delivery address parsing robot, dedicated to accurately parsing input delivery address information into structured content.
   
   ## Goal
   Parse the input courier address and return the parsing result in JSON format：{
     /** Province */
     "province": "string",
     /** City */
     "city": "string",
     /** District */
     "region": "string",
     /** Detailed Address */
     "address": "string",
     /** Recipient */
     "people": "string",
     /** Phone */
     "tel": "string"
   }
   
   ## Skills
   1. Carefully analyze the input courier address text and extract key information such as province, city, district, detailed address, recipient, and phone number.
   2. Supplement and improve vague or incomplete courier address information based on reasonable speculation and common courier address patterns.
   3. Capable of handling various complex express delivery address situations, ensuring the accuracy and completeness of the parsing results.
   
   ## Restrictions
   1. Only focus on tasks related to express address resolution and firmly refuse to handle other unrelated content.
   2. Strictly follow the prescribed JSON format to output the parsing results, ensuring the accuracy of the format without any deviation.
   3. For delivery address information that cannot be resolved or is unclear, output null as required.
   ```
   

* User interface example

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/61171377a53a41d3a9d876a058aeb3fd~tplv-goo7wpa0wc-image.image) </span>


<span id="f6414c59"></span>
# Reference: Frequently Asked Questions

<span id="0e3f5f56"></span>
## **1. Error with limited viewership of large model interface**

**Problem performance**


* Too Many Requests

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab1eeb03333c4be1b71a558009e4f667~tplv-goo7wpa0wc-image.image) </span>

   **Solution**

* Replace the RPM larger large model access point, you can refer to the [opening management - Volcano Ark large model service platform - Volcano Engine ](https://www.volcengine.com/docs/82379/1159200); at the same time increase the **advanced settings \- request interval** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c3650e6be53b408d840214a346c5b2fc~tplv-goo7wpa0wc-image.image) </span>


<span id="9c76a376"></span>
## **2. Test execution error**

**Problem performance**


* The prompt message is that the post\-operation execution failed.

   **Solution**

* Cancel the data post\-operation first, click Test Execution, and view the current test execution results. Resize the data postaction code based on the current trial execution results.


<span id="6ae3e11f"></span>
## 3. Execute an error

**Problem performance**


* An error is reported during execution, click the View Log button, scroll down and find an error prompt: `java.lang. RuntimeException: The maximum number of failed retries has been reached, error message: http result not success, code: 400, message: Bad Request, body: {"error": {"code": "InvalidParameter", "message": "One or more parameters specified in the request are not valid`

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5cbecf2b12b4da19b75f15ee80367cd~tplv-goo7wpa0wc-image.image) </span>

   **Solution**

* The input is processed by adding a computed column operator to replace some special characters, and the expression is:

   ```Java
   replace(replace(regexp_replace(`Pending fields`, "[\\n\\r\\t]", " "), '"', '&quot;'), '\\', '&bsol;')        
   ```
