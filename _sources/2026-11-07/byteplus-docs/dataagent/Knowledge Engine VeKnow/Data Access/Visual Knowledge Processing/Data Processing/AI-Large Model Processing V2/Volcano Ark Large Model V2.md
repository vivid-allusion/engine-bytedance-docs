---
title: "Volcano Ark Large Model V2"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Volcano_Ark_Large_Model_V2"
---

The Volcano Ark model is an intelligent data processing tool in AI\-large model processing operator. It supports docking with Volcano Engine large model services, and realizes functions such as unstructured data analysis and multi\-language translation through custom model configuration, generation strategies, and role personas. It is suitable for enterprise data intelligent processing scenarios. This article shows you how to use the large model of Volcano Ark.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Volcano Ark large model V2 <a href="https://docs.byteplus.com/docs/dataagent/Volcano_Ark_Large_Model">Volcano Ark Large Model</a> compared with optimized operator performance and parameter configuration logic.</div>


<span id="1d1844db"></span>
# **Feature Overview**

The Volcano Ark large model operator is connected to the Volcano Engine large model service, which can intelligently process data, such as user comment analysis, conversation content summary, image content recognition, etc. Users can automatically and intelligently process data by configuring model parameters and prompt words.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This function is a value\-added function. If you want to use this function, you can contact the Volcano Engine technical support staff for consultation. You can use it after purchasing and activating this function.</div>


<span id="c4d0e757"></span>
# Prerequisite


* Users need to register a [BytePlus](https://console.byteplus.com/auth/signup?redirectURI=https%3A%2F%2Fwww.byteplus.com%2Fen&skipAccountProfile=true) account in advance and open the Volcano Ark large model service.

* The enterprise administrator has configured the large model for the operator, see details [Configure Large Model Invocation](https://docs.byteplus.com/docs/dataagent/Configure_Large_Model_Invocation).


<span id="8313aa91"></span>
# Operation steps

<span id="7ebf1955"></span>
## Step 1: Create a new Ark model operator


1. Click "Data Access", select "Visual Knowledge Processing", click "New", and select "New Offline Task".

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/821d810fbdc5401db4b70e11a6f708a8~tplv-goo7wpa0wc-image.image) </span>

2. Follow [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task)the steps in Create the offline task and select the Volcano Ark Large Model V2 operator in AI\-Large Model Processing V2 for the data connection while processing the node.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3b4f0e59155a48e898b4911b24926798~tplv-goo7wpa0wc-image.image) </span>


<span id="15378f19"></span>
## Step 2: Configure the model and model parameters


1. Select Volcano Ark Large Model V2 in the mission drawing board.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14b657842a8e41a183247f9ac5b78194~tplv-goo7wpa0wc-image.image) </span>

2. In the **Model Information** area, complete the following configuration.

   * **Model** : If the enterprise administrator has configured a large model for the operator (see **Prerequisites** above for details), selecting a large model is supported. You can also choose to **customize the model** and complete the model related configuration.

   * **Model call address** : If you choose a custom model, you need to configure the call address of the application.

   * **Inference Access Point** : If you choose a custom model, you need to configure the inference access point. The general format is `ep-xxxxxxxxxx-yyyy`, and the creation method refers to [creating a custom inference access point ](https://www.volcengine.com/docs/82379/1099522).

   * **API Key** : If you choose a custom model, you need to configure the API Key. The general format is `xxxxxxxx-yyyy-xxxx-yyyy-xxxxxxxxxxxx`, and the acquisition method refers to [obtaining API Key and configuring it ](https://www.volcengine.com/docs/82379/1263279).

3. In the **Model Parameters** area, complete the following configuration.

   * **Temperature** : The value range is 0~ 1, and the increase will make the output of the model more diverse and innovative. On the contrary, the decrease will make the output content more follow the instruction requirements but reduce the diversity. It is recommended not to adjust with the **Top P** at the same time.

   * **Top P** : Values range from 0 to 1, a method for controlling the diversity of generated text, also known as nucleus sampling. The model samples from words whose cumulative probability exceeds the P value, and higher values increase diversity. It is recommended not to adjust at the same time as **Temperature** .

   * **Maximum output length** : Controls the maximum length of content generated by the model.

   * **Thinking mode** : Whether to show the model thinking process, you can choose to **turn it off** , **turn it on** , and **automatically** .


<span id="646bec43"></span>
## Step 3: Configure input parameters


1. Add input parameters in the **parameter configuration** area.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bb887188f16d41d4b47e9bc5e79dbbac~tplv-goo7wpa0wc-image.image) </span>

   * **Fields** : Select a field from the input parameters.

   * **Input Mode** :

      * **Content** : Content, type supports selecting **text** .

      * **File** : file, the type supports selecting **pictures** , **videos** , and **documents** .

   * **Sample data** : Optional configuration to set default sample data for input parameters.

2. In the Custom Parameters area, add additional required custom parameters and parameter values according to business needs.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11b75ea3f37049df91334c2cb7d1f92f~tplv-goo7wpa0wc-image.image) </span>


<span id="9ed33db4"></span>
## Step 4: Configure the prompt word

In the prompt word configuration area, the system provides **user comment analysis** , **session content summary** , **picture content recognition** three types of template prompt words for your reference. You can choose to specify a template and adjust the content of the template, or you can customize the edit model prompt according to your business needs.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5d0e6157ec514d648adf6269adeff2b7~tplv-goo7wpa0wc-image.image) </span>

Text fields are not automatically sent to the model, so you need to display the reference within the prompt word in the format of `${field name}`. After successful configuration, there will be a prompt message below the prompt word as shown in the figure below.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/41e307b4227841f28367eb07e094b4bc~tplv-goo7wpa0wc-image.image) </span>

<span id="c50ccbdc"></span>
## Step 5: Configure data postaction and test execution

Check the **data post\-operation** , and perform some processing on the data based on the output results of the large model. Click **Test Execution** to test the results of the data post\-operation, which can be viewed in the **Test Execution Results** column.

For example, in the system default configuration, messages in response results are parsed as JSON objects.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8cfefe2375304748bb18ab7deea2f1e9~tplv-goo7wpa0wc-image.image) </span>

<span id="1344249b"></span>
## Step 6: Configure advanced settings

Configure parameters in the advanced settings region.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64dd8bd54116423fa9b96d43d0f5237c~tplv-goo7wpa0wc-image.image) </span>

The relevant parameters are described as follows:


|parameter |configuration instructions |
|---|---|
|concurrent size |Sets the number of tasks to process concurrently. |
|timeout |Large model calculation timeout in milliseconds ms |
|number of retries |The number of automatic retries when a request fails, in times |
|request interval |Large model access points generally have an RPM (number of requests per minute) limit, and the request interval is set on demand according to the value of the RPM, in milliseconds ms<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The request interval is set to avoid errors in large models with limited viewership of interfaces. The general error information is as follows</div><br><br><br><div data-tips="true" data-tips-type="tip"><img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/651d2f86502d49c0946e7616c14f2204~tplv-goo7wpa0wc-image.image" width="820px" /></div><br> |
|exception handling |* Terminate the task: If the inference fails, the task fails, and the intermediate results are cleared<br><br>* Ignore Exceptions: Tolerant mode, ignore data where inference fails, use null padding, and preserve results where inference succeeds |


<span id="1f530e81"></span>
## Step 7: Configure the output parameters

On the basis of the test execution results, the **field setting** area configures the field, the parsing path, and the field type, so as to structure the output data for use by downstream nodes.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6de9bfa0b9d5450bbb6c52aa4e14841e~tplv-goo7wpa0wc-image.image) </span>

<span id="076ef6ef"></span>
# Common Problem

<span id="99189448"></span>
## **Error with limited viewership of large model interface**

**Problem performance**

Too Many Requests

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5da4c37c6c14c7bb5de38a2fae65aa6~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ab1eeb03333c4be1b71a558009e4f667~tplv-goo7wpa0wc-image.image) </span>

**Solution**

Replace the RPM larger large model access point, you can refer to the [opening management - Volcano Ark large model service platform - Volcano Engine ](https://www.volcengine.com/docs/82379/1159200); at the same time increase the **advanced settings \- request interval** .

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d41656e6bc447c49e1f487dbe4fcf83~tplv-goo7wpa0wc-image.image) </span>

<span id="7091bbfe"></span>
## **Test execution error**

**Problem performance**

The prompt message is that the post\-operation execution failed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0e29637e6ac34544a95887335ca19fba~tplv-goo7wpa0wc-image.image) </span>

**Solution**

Cancel the data post\-operation first, click Test Execution, and view the current test execution results. Resize the data postaction code based on the current trial execution results.

<span id="4d076141"></span>
## Execution error

**Problem performance**

An error is reported during execution, click the View Log button, scroll down and find an error prompt: `java.lang. RuntimeException: The maximum number of failed retries has been reached, error message: http result not success, code: 400, message: Bad Request, body: {"error": {"code": "InvalidParameter", "message": "One or more parameters specified in the request are not valid`

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a5cbecf2b12b4da19b75f15ee80367cd~tplv-goo7wpa0wc-image.image) </span>

**Solution**

The input is processed by adding a computed column operator to replace some special characters, and the expression is:

```Java
replace(replace(regexp_replace(`Pending fields`, "[\\n\\r\\t]", " "), '"', '&quot;'), '\\', '&bsol;') 
```
