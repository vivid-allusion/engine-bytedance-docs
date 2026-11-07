---
title: "Custom Large Model"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Custom_Large_Model"
---

<span id="4cc8d937"></span>
# **Feature Overview**

Custom large model is an intelligent data processing tool in AI\-large model processing operator, which supports Deepseek large model, Tongyi Qianwen large model operator and custom large model. Through custom model configuration, generation strategy and role personalization, unstructured data analysis, multi\-language translation and other functions are realized, which is suitable for enterprise data intelligent processing scenarios. This article shows you how to use custom large model operators.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This function is a value\-added function. If you want to use this function, you can contact the Volcano Engine technical support staff for consultation. You can use it after purchasing and activating this function.</div>


<span id="97b75090"></span>
# Prerequisite


* You have opened Deepseek large model, Tongyi Qianwen large model service or other customized large model services.

* The enterprise administrator has configured the large model for the operator, see details [Configure Large Model Invocation](https://docs.byteplus.com/docs/dataagent/Configure_Large_Model_Invocation).


<span id="a243b39e"></span>
# Operation Steps

<span id="802ba67f"></span>
## Step 1: Create a new custom large model operator


1. In the left navigation bar of Enterprise Knowledge Engine, select **Data Access** \> **Visual Knowledge Processing** .

2. In the upper left corner of the **Task List** page, click **New** and select **New Offline Task** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/821d810fbdc5401db4b70e11a6f708a8~tplv-goo7wpa0wc-image.image) </span>

3. Follow [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task)the steps in Create the offline task, and when processing the node, select Add a custom large model operator from AI\-Large Model Processing for the data connection.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2285b241ae0e495dacffe67f990e8bf0~tplv-goo7wpa0wc-image.image) </span>


<span id="4449cf9d"></span>
## Step 2: Set the model docking parameters

Click on the custom large model operator that has been dragged into the task to configure the model parameters and configure the relevant information.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e560b9a5d26f4c5fa99c9d71d7ae4c4f~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db18c46042434bdbb3eb2f55bd37a7b1~tplv-goo7wpa0wc-image.image) </span>


|configuration item |**explain** |
|---|---|
|model |Choosing a large model is supported if the enterprise administrator has configured the large model for the operator (see **Prerequisites** above for details). You can also choose to **customize the model** and complete the model related configuration. |
|model call address |If you choose a custom model, you need to fill in the calling address of the application |
|model |If you choose a custom model, enter the Model Endpoint. For example: ep\-xxxxxxxxxx\-yyyy, the acquisition method can refer to [Get Endpoint ID ](https://www.volcengine.com/docs/82379/1099522). |
|API Key |If you choose a custom model, enter the API Key required to invoke the model. For example: xxxxxxxx\-yyyy\-xxxx\-yyyy\-xxxxxxxxxxxx, the acquisition method can refer to [Get API Key and configure ](https://www.volcengine.com/docs/82379/1541594). |
|generative diversity |Select a preset mode to control the diversity of generated content. Different modes generate different randomness and Top P parameter values (modifiable).<br><br>The following modes are supported:<br><br><br>* Accurate mode: generate more stable and certain results.<br><br>* Balanced Mode: Strike a balance between stability and creativity.<br><br>* Creative mode: generate results that are more imaginative and diverse.<br><br>* Custom: Manually adjust the generated randomness and Top P parameters below. |
|generative randomness |Temperature: Increasing the output of the model will make it more diverse and innovative, while reducing the output content will make it more compliant with instruction requirements but reduce diversity. It is recommended not to adjust it at the same time as "Top p". Controls the randomness of the generated text. The higher the value, the more random and diverse the generated content; the lower the value, the more certain and conservative the content.<br><br>Value range: 0 to 1. |
|Top P |Top p is the cumulative probability: When the model generates the output, it selects the words with the highest probability until the total probability of these words accumulates to the Top p value. This allows the model to choose only these high\-probability words, thus controlling the diversity of the output. It is recommended not to adjust at the same time as "generating randomness". A method for controlling the diversity of generated text, also known as nucleus sampling. The model samples words whose cumulative probability exceeds the P value. Higher values increase diversity.<br><br>Value range: 0 to 1. |
|model parameters |Click **Add Parameter** to add parameter name and parameter value. |


<span id="5875c644"></span>
## Step 3: Configure the model persona and reply logic

Configure the prompt word associated with the reply logic.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09df0418437a444f8768d1b02cdc8db9~tplv-goo7wpa0wc-image.image) </span>

It needs to include the following four parts:


* Role definition: such as tag extraction expert.

* Skill description: such as what label to extract.

* Output format: as required by JSON format.

* Other limitations: such as focusing on extraction tasks without divergence.

   The following is an example for reference only:


```Markdown
# Role
You are a precise and efficient chatbot for bank consumer loan customer service, 
capable of quickly and accurately extracting corresponding tags from customer service 
chat records, helping banks to gain a deeper understanding of customer needs and provide 
more personalized services.

## Skills
### Skill 1：Analyze chat content and extract tags
1. Carefully study customer service chat records to accurately understand the customer's expression intentions.
2. Based on the customer's statement, determine the label to which their loan demand belongs：
    - Immediate processing: The customer clearly stated that they need to apply for a consumer loan immediately.
    - Recently considered：The customer has revealed plans to apply for a consumer loan in the near future.
    - No demand：The customer clearly expressed that there is currently no need to apply for a consumer loan.
3. Based on the customer's statement, determine the label to which their (customerType) belongs：
    - Personal：Personal user.
    - Enterprise: Enterprise users.
    - Unknown: Unable to clearly determine customer type.
4. Based on the customer's statement, determine the label to which their (focus) belongs：
    - Interest rate: Customers mainly inquire or discuss about loan interest rates.
    - Limit: The customer emphasized the situation related to the loan limit.
    - Repayment method: The customer shows interest in the repayment method.
    - Approval process: Customers are concerned about loan approval processes and related issues.
    - Other: The content that customers are concerned about does not belong to the clear categories mentioned above.
5. Based on the customer's statement, determine the label to which their (loanUsage) belongs：
    - Daily consumption: The customer stated that the loan is mainly used for daily consumption.
    - Education expenditure: The client emphasizes that the loan is used for education related expenses.
    - Medical expenses: The customer mentioned that the loan is used for medical purposes.
    - Other uses: The loan purpose mentioned by the customer does not belong to the above category.
    - Not mentioned: The customer did not mention any information related to the purpose of the loan.
6. Freely extract other valuable tags from chat records, such as customer preferences for loan terms, special requirements, etc. (output null if not available).

Output content in JSON format, as shown in the following example：

{
    "demand": "Recently considered",
    "customerType": "Personal",
    "focus": "limit",
    "loanUsage": "daily expenses",
    "otherValuableTags": null
}

If there is no matching label, null can be output.

## Restrictions
-Only analyze customer service chat content, extract exact tags, and do not perform any other unrelated operations.
-Strictly follow the established label classification for judgment, and do not create new label categories on your own.
-It is essential to ensure the accuracy and objectivity of the analysis results.
-The freely extracted tags must be truly valuable and relevant to customer needs or bank consumer loans.
```


<span id="879e9564"></span>
## Step 4: Configure template variables with user input

Configure template variables with user input. After selecting the field column for unstructured data in "Upstream Fields" of "Template Variables", configure the rules for the variable in "User Input".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3904a579ca6b4ac1ab8156554e8145ab~tplv-goo7wpa0wc-image.image) </span>

<span id="651154bc"></span>
## Step 5: Advanced Settings

Click "Advanced Settings" to set the relevant parameters.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/db83282ed30446b38b041e9d76ac60a0~tplv-goo7wpa0wc-image.image) </span>

The relevant parameters are described as follows:


|parameter |configuration instructions |
|---|---|
|parallelism |The number of parallelizations requested, the number of parallelizations actually executed, and the resources available to the cluster are also relevant. It is recommended that the user compute the parallelism reasonably according to the interface performance of the call (QPS, QPM, etc.). |
|timeout |Large model calculation timeout in milliseconds ms |
|number of retries |The number of automatic retries when a request fails, in times |
|request interval |Large model access points generally have an RPM (number of requests per minute) limit, and the request interval is set on demand according to the value of the RPM, in milliseconds ms<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The request interval is set to avoid errors in large models with limited viewership of interfaces. The general error information is as follows</div><br><br><br><div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/651d2f86502d49c0946e7616c14f2204~tplv-goo7wpa0wc-image.image" width="820px" /></div><br> |
|complete exception handling |* Terminate the task: If the inference fails, the task fails, and the intermediate results are cleared<br><br>* Ignore Exceptions: Tolerant mode, ignore data where inference fails, use null padding, and preserve results where inference succeeds |


<span id="5c6b0f79"></span>
## Step 6: Test execution

Click "Test Execution" to view the output results in the "Test Execution Results" column.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91ed33c53e84465b9e13fbff7740968e~tplv-goo7wpa0wc-image.image) </span>

<span id="11d4170a"></span>
# Data Post Configuration

<span id="2b48f40d"></span>
## Data post configuration

Check "Data Post\-operation" to perform some processing on the data based on the output results of the large model (API). Click "Test Execution" to test the results of the data post\-operation, which can be viewed in the "Test Execution Results" column.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b3f2c544d8e84d3fb4b494ae7a370ed6~tplv-goo7wpa0wc-image.image) </span>

For example: through the **human and reply logic** function can make the large model output JSON format data, then write the code to process the JSON string as a JSON object, so as to facilitate the use in the field settings.

```Groovy
def jsonSlurper = new JsonSlurper()
return jsonSlurper.parseText(response.data.choices[0].message.content)
```


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After enabling [Batch Reasoning], [Data Post\-Operation] will be automatically enabled, but the code cannot be customized.</div>


<span id="7f5c1174"></span>
## Field settings

Configure fields, parse paths, and field types based on test execution results to structure output data.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/e6d248ebf341424c8e74677d42f33a11~tplv-goo7wpa0wc-image.image) </span>
