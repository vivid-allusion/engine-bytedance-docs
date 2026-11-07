---
title: "Qwen Large Model"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Qwen_Large_Model"
---

<span id="20e34b6f"></span>
# Feature Overview

Thousand Questions Big Model is an intelligent data processing tool in AI\-Big Model Processing Operator. It realizes functions such as unstructured data analysis and multilingual translation through custom model configuration, generation strategy and role setting, and is suitable for enterprise data intelligent processing scenarios. This article shows you how to use the Thousand Questions Large Model operator.

<span id="5c39b524"></span>
# Prerequisite


* You have opened Tongyi Qianwen large model service or other customized large model services.

* The enterprise administrator has configured the large model for the operator, see details [Configure Large Model Invocation](https://docs.byteplus.com/docs/dataagent/Configure_Large_Model_Invocation).


<span id="5148fc20"></span>
# Operating instructions

<span id="fd39785c"></span>
## Step 1: Create a Thousand Questions Large Model Operator


1. In the left navigation bar of Enterprise Knowledge Engine, select **Data Access** \> **Visual Knowledge Processing** .

2. In the upper left corner of the **Task List** page, click **New** and select **New Offline Task** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/821d810fbdc5401db4b70e11a6f708a8~tplv-goo7wpa0wc-image.image) </span>

3. Follow [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task)the steps in to complete the offline task creation. When processing the node, select the Thousand Questions Large Model Operator in "AI\-Large Model Processing" for the data connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2a7fb1e8fb444f24a85825822ae00ca9~tplv-goo7wpa0wc-image.image) </span>


<span id="e234089e"></span>
## Step 2: Set the model docking parameters

Click "Custom Model" and set relevant parameters in the "Model Settings" pop\-up window.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/557d62b23d6b4313b6d6ceb427e8740e~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/21b044fd87e54e13837d01538defba84~tplv-goo7wpa0wc-image.image) </span>

The relevant parameters are described as follows:


|parameter |configuration instructions |
|---|---|
|model |Choosing a large model is supported if the enterprise administrator has configured the large model for the operator (see **Prerequisites** above for details). You can also choose to **customize the model** and complete the model related configuration. |
|model call address |If you choose a custom model, you need to fill in the call address of the application, the call address of the application |
|inference access point |If you choose a custom model, you need to set up an inference access point. General format is `ep-xxxxxxxxxx-yyyy`, create method reference [Create custom inference access point](https://www.volcengine.com/docs/82379/1099522) |
|API Key |If you choose a custom model, you need to set the API Key. The general format is `xxxxxxxx-yyyy-xxxx-yyyy-xxxxxxxxxxxx`, and the acquisition method is referred to [Get API Key and configure](https://www.volcengine.com/docs/82379/1263279) |
|generative diversity |Supports four mode adjustments to generate randomness and Top P values to control the effects of large model operators.<br><br><br>* Exact Mode:<br><br>   * Strictly follow instructions to generate content<br><br>   * Suitable for situations where accuracy is required, such as official documents, code, etc<br><br>* Balance Mode:<br><br>   * Striking a balance between innovation and precision<br><br>   * Suitable for most everyday use cases, generating interesting but rigorous content<br><br>* Creative mode:<br><br>   * Inspire creativity and provide fresh and unique ideas<br><br>   * Suitable for situations that require inspiration and unique perspectives, such as brainstorming, creative writing, etc<br><br>* Custom mode:<br><br>   * Customize the generation method through advanced settings<br><br>   * According to demand, fine adjustment is made to achieve personalized optimization<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Generative randomness: A higher level makes the output of the model more diverse and innovative, while a lower level makes the output more compliant with instructions but less diverse. It is recommended not to adjust it at the same time as "Top p".</div><br><br><br>* <div data-tips="true" data-tips-type="tip">Top p: Cumulative probability. The model generates the output by selecting the words with the highest probability until the total probability of these words accumulates to the top p value. This allows the model to choose only these high\-probability words, thus controlling the diversity of the output. It is recommended not to adjust at the same time as "generating randomness".</div><br> |


<span id="66f6b1ff"></span>
## Step 3: Configure the model persona and reply logic

Support user\-defined character settings, functions, and workflows for large models.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/174e81d2ad83436ba43a9ca05af5ad7e~tplv-goo7wpa0wc-image.image) </span>

Use natural language to fill in the character settings, functions and workflow of the large model. You can refer to the following content for custom configuration:

```JSON
# Role
You are a precise and efficient intelligent delivery address resolution assistant robot that can accurately and efficiently parse input address information into structured content. 
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


<span id="f3c963e7"></span>
## Step 4: Configure template variables

Support users to select upstream fields or system variables as template variables, embedded in the user input content, for example, using the upstream `content`field, enter "${content}" in the user input, the large model will process the `content`field content.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/31a2576c9a704faaa5848a2dfd98d201~tplv-goo7wpa0wc-image.image) </span>

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
   


<span id="80dee6a9"></span>
## Step 5: Configure user input

Configure user input as data postaction and sample content for field configuration test execution.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/227d22d2c3ba476cbcb451aff5fe1dec~tplv-goo7wpa0wc-image.image) </span>

<span id="a3375756"></span>
## Step 6: Advanced Settings

Click "Advanced Settings" to set the relevant parameters.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c8d3c117028e4040b02c0812ab351a2f~tplv-goo7wpa0wc-image.image) </span>

The relevant parameters are described as follows:


|parameter |configuration instructions |
|---|---|
|parallelism |The number of parallelizations requested, the number of parallelizations actually executed, and the resources available to the cluster are also relevant. It is recommended that the user compute the parallelism reasonably according to the interface performance of the call (QPS, QPM, etc.). |
|timeout |Large model calculation timeout in milliseconds ms |
|number of retries |The number of automatic retries when a request fails, in times |
|request interval |Large model access points generally have an RPM (number of requests per minute) limit, and the request interval is set on demand according to the value of the RPM, in milliseconds ms<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The request interval is set to avoid errors in large models with limited viewership of interfaces. The general error information is as follows</div><br><br><br><div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/651d2f86502d49c0946e7616c14f2204~tplv-goo7wpa0wc-image.image" width="820px" /></div><br> |
|complete exception handling |* Terminate the task: If the inference fails, the task fails, and the intermediate results are cleared<br><br>* Ignore Exceptions: Tolerant mode, ignore data where inference fails, use null padding, and preserve results where inference succeeds |


<span id="9e102d14"></span>
## Step 7: Test execution

Click "Test Execution" to view the output results in the "Test Execution Results" column

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d47b89b587694c689dd367ae55dbe31f~tplv-goo7wpa0wc-image.image) </span>

<span id="db41606b"></span>
## Step 8: Data post\-operation configuration

Check "Data Post\-operation" to perform some processing on the data based on the output results of the large model (API). Click "Test Execution" to test the results of the data post\-operation, which can be viewed in the "Test Execution Results" column.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/543ba41c4948445c8ba59bc66e2762e0~tplv-goo7wpa0wc-image.image) </span>

<span id="abd2400e"></span>
## Step 9: Field Settings

Configure fields, parse paths, and field types based on test execution results to structure output data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/10a8a03e82434f2d957f9f5fa34f0e90~tplv-goo7wpa0wc-image.image) </span>

&nbsp;
