---
title: "Manage Custom Operators"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Manage_Custom_Operators"
---

In the visual knowledge processing task, the system provides rich operators for data processing. If an enterprise needs to use an external API to process data, it can access the external API to the internal knowledge engine through a custom operator. This article describes how to add and configure custom operators.

<span id="61038fd8"></span>
# Prerequisite

It is recommended that custom operators be maintained by enterprise administrators. If an enterprise administrator needs to specify another user to maintain custom operators, they need to first grant that user **advanced configuration editing and viewing** permissions for **visual modeling, datasets** . Please refer to the specific operation instructions for authorization [Authorization Management](https://docs.byteplus.com/docs/dataagent/Authorization_Management__).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c9a4098a19f64a5f9e9a7608325bc66c~tplv-goo7wpa0wc-image.image) </span>

<span id="273249dc"></span>
# New Custom Operator

The system has a built\-in custom operator by default (named **REST API 2.0 call** ), you can also add new custom operators as needed to adapt to different businesses.


1. Log in to the Marketing Agent console.

2. Select **Enterprise Knowledge Engine** in the left navigation bar.

3. In the left navigation bar of Enterprise Knowledge Engine, select **Project Center** \> **Knowledge Processing Configuration**.

4. In the left navigation bar of Knowledge Processing Configuration, select **Advanced Settings** \> **Custom Operator Management**.

5. In the upper right corner of the page, click **New Operator** and complete the following configuration.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/24d38b834df24db0aac484bd0e5ae43e~tplv-goo7wpa0wc-image.image) </span>

   * **Operator Source** : Required, select **Copy existing operator**.

   * **Select operator to copy** : Required, select **REST API 2.0 call**.

   * **Name of the new operator** : Required, custom name identifying the operator.

   * **Description** : Optional, description of the current operator, such as use, restrictions and other information.

   * **Operator Type** : Required, select **Custom Call**.

6. Click **OK** to view the new operators in the list of custom operators.

   The operation column supports **editing** and **deleting** custom operators.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Once the operator is deleted, it cannot be restored. Please proceed with caution.   </div>
   

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/96c307f811b54898a4d1b09f42e307e1~tplv-goo7wpa0wc-image.image) </span>


<span id="82a65a42"></span>
# Default Settings for Editing Operators

You can preset default configurations for custom operators, which can then be applied directly in build data processing tasks.


1. Log in to the Marketing Agent console.

2. Select **Enterprise Knowledge Engine** in the left navigation bar.

3. In the left navigation bar of Enterprise Knowledge Engine, select **Project Center** \> **Knowledge Processing Configuration**.

4. In the left navigation bar of the knowledge processing configuration, select **Advanced Settings** \> **Operator Defaults**.

5. Hover over the operator card where you need to edit the default settings and click **Settings**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7480f75acde47f4970079c416574ea1~tplv-goo7wpa0wc-image.image) </span>

6. Complete the following configuration and click **Save**.

   
   |**module** |**configuration item** |**explain** |
   |---|---|---|
   |basic information |URL Address |API request address, support import and export through cURL. |
   ||request method |Set the interface's request method, **GET** or **POST** . |
   ||OAuth2 authentication |Support OAuth2 authentication. After enabling, you need to complete OAuth2 authorization.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Enable this feature when an API request requires access to a third\-party service interface using OAuth2 authorization code mode.</div><br><br><br><br>1. Once enabled, in the **Oauth2 Authorization Status** area, click **Click Authorization** .<br><br>2. Configuration **basic information** (AK, SK and authorized jump address), the specific way to obtain the relevant three\-party website documents, click **Next** after the configuration is completed.<br><br>3. If the user is using the combination of AK and authorization jump address to configure authorization information for the first time, it is necessary to further obtain the AccessToken configuration and RefreshToken configuration. Configure the API address, request method, request parameters and other relevant information, click Confirm, and the browser will automatically initiate the request authorization link to jump to the three\-party authorization page.<br><br>4. After the user completes the authorization, it automatically jumps to the unified authorization callback address. According to the authorization configuration of the previous user, the system initiates the request to **obtain Access Token** and **obtain Refresh Token** synchronously in the background. After the verification is passed, the configuration will take effect, and the authorization will be completed when you return to the data connection page.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The three\-party website authorization is usually for a single AK dimension, and if multiple data links use the same AK, they need to share the same authorization.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The system will automatically match the valid authorization according to the authorization link host and AK; if not, it needs to be configured for the first time.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The system cannot verify the three\-party exported parameter (no uniform format), please <strong>check the parameters carefully</strong> to avoid the interface returning failure due to parameter errors. If the authorization address is the same as the AK, the system will automatically match the last configuration, and the mismatch data can only be corrected and reconfigured.</div><br><br><br>* <div data-tips="true" data-tips-type="warning"><strong>Get Access Token</strong> The parameter key corresponding to code in the callback request is fixed as "code" and cannot be modified.</div><br> |
   ||parameter setting |1. Set the API corresponding **request header** , **request parameters** , **request body** .<br><br>   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Value supports static and dynamic parameter values.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The static parameter value can be filled in with specific values, such as <code>male</code>.   </div><br>   <br><br>      * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">For dynamic parameters, fill in the format of <code>${params \| example: value}</code>, where:   </div><br>   <br><br>         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>Params</code>refers to the name of the output field of the previous node, and the value under this field will be used as the imported parameter value of the API parameter. Required when the operator is executed.   </div><br>   <br><br>         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1"><code>Example: value</code>is the sample value, used to send a request to obtain the return format of the interface, required.   </div><br>   <br><br>         * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Example: Suppose the imported parameter of the API is object_id, and the value of the upstream output field unit_id is used as the imported parameter value of the object_id, then when filling in the API configuration, the Key is object_id, and the value is filled in in the format of ${unit_id   </div><br>   <br><br>   * <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The system provides built\-in variables and built\-in functions, please refer to <a href="https://docs.byteplus.com/docs/dataagent/REST_API_2_0_#1d0f6685">system built\-in variables</a>, <a href="https://docs.byteplus.com/docs/dataagent/REST_API_2_0_#e4d80a4c">system built\-in function</a>.   </div><br>   <br><br>   * **Request header** : support configuration key, value, support add, delete operations, up to 10 groups can be configured.<br><br>   * **Request parameters** : Enter all query parameters required by the API.<br><br>   * **Request body** : Select the request body type (form\-data or raw), both of which support the user to enter the request body in JSON format.<br><br>      General: To operate on JSON, `$`represents the root node, `and the.`sign represents the sub\-node.<br><br>      If the JSON data is:<br><br>   ```JSON```<br>```   {```<br>```     "showapi_res_error": "",```<br>```     "showapi_res_id": "6597a2f5fb638cf45b4d460c",```<br>```     "showapi_res_code": 0,```<br>```     "showapi_fee_num": 1,```<br>```     "showapi_res_body": {```<br>```       "list": [```<br>```         {```<br>```           "time": "14:26:57",```<br>```           "zhesuan": "193.69",```<br>```           "code": "AED",```<br>```           "hui_out": "195.91",```<br>```           "chao_in": "192.95",```<br>```           "chao_out": "199.47",```<br>```           "name": "阿联酋迪拉姆",// which means "UAE Dirham"```<br>```           "hui_in": "194.55",```<br>```           "day": "2024-01-05"```<br>```         },```<br>```         {```<br>```           "time": "14:26:57",```<br>```           "zhesuan": "477.56",```<br>```           "code": "AUD",```<br>```           "hui_out": "481.77",```<br>```           "chao_in": "478.08",```<br>```           "chao_out": "483.16",```<br>```           "name": "澳大利亚元",//which means "Australian dollar"```<br>```           "hui_in": "478.57",```<br>```           "day": "2024-01-05"```<br>```         }```<br>```       ],```<br>```       "listSize": 28,```<br>```       "ret_code": 0```<br>```     }```<br>```   }```<br>```   ```<br>   <br><br>   Then the values corresponding to some paths are as follows:<br><br>   ```JSON```<br>```   $.showapi_fee_num = 1```<br>```   $.showapi_res_id = "6597a2f5fb638cf45b4d460c"```<br>```   $.showapi_res_body.list.* = [{"time":"14:26:57","zhesuan":"193.69" ... // The following is omitted```<br>```   ```<br>   <br><br>2. Set the **front operation** .<br><br>   When you need to perform some additional steps to prepare data or obtain necessary information before the main request, this can be done through this configuration. You can set up to 5 pre\-operations.<br><br>   1. Click **Add a pre\-operation** , you need to enter the details of the pre\-operation on the configuration page, including URL address, request method, etc.<br><br>   2. After clicking **Send Request** , the system will parse the pre\-request and present the parsing result in the **request result** area. You need to configure the key and result field path of the dynamic parameters to facilitate subsequent application of the pre\-request result to the current request. Dynamic parameter preparation can be referred to [Dynamic parameter writing rules](https://docs.byteplus.com/docs/dataagent/REST_API_2_0_#dc238525).<br><br>3. Set the **post operation** .<br><br>   Provides a more flexible and powerful way to configure custom parameters, supports groovy syntax, and allows users to write code to achieve multi\-level request parsing. The post\-operation writing rules can be referred to [Postaction writing rules](https://docs.byteplus.com/docs/dataagent/REST_API_2_0_#6d7a0980). |
   |advanced settings |parallelism |The parallelism degree sets the parallelism degree of a single Partition of a Spark task. The actual final parallelism degree is affected by the number of Partitions assigned to the task. The number of parallelism during actual execution is related to the resources available to the cluster. It is recommended that the user compute the parallelism reasonably according to the interface performance of the call (QPS, QPM, etc.).<br><br>Default value: 1 |
   ||timeout |The maximum time an input request can wait without a response, in milliseconds (ms).<br><br>Default value: 180000 |
   ||number of retries |When a request fails, the system attempts to retry up to a maximum of 5 times.<br><br>Default value: 3 |
   ||request interval |The final QPS of the task depends on the number of cores allocated by the output node and the request interval. Adjusting the request interval can control the task concurrency. The smaller the request interval, the larger the QPS. The unit is in milliseconds (ms).<br><br>Default value: 100<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Please set the request interval carefully, there is a service risk if the concurrency is too high (when the QPS of a single task \> the global QPS, the global QPS shall prevail).</div><br> |
   ||complete exception handling |* **Terminate task** : When an exception occurs, immediately terminate the execution of the current task and clear the intermediate results. This is the default option.<br><br>* **Ignore Exception** : When an exception occurs, ignore the error (padding the data with null) and continue with the next steps of the task. |
   |parsing requests and path configuration |parsing result |After completing the above configuration, click **Send Request** in the **Basic Information** \> **Parameter Settings** area, and the system will parse the request.<br><br>The parsing order is **Pre\-Action \> Current Request \> Post\-Action** , and the **parsing result** is rendered. |
   ||field settings |According to the parsing result, add the corresponding **field key** , **parsing path** and **field type** , where the parsing path supports: `$`represents the root node, `.`number is used to identify the node level, `*`represents wild\-card, such as `$.data.items. *`. |
   


<span id="22e6b15a"></span>
# Check if the Custom Operator Configuration Takes Effect

After you have completed the "New Custom Operator" and "Edit Operator Default Settings" described in this article, you can create a test task to preview whether the corresponding operator configuration meets expectations. How to create a task, see [Step 1: Create a new task](https://docs.byteplus.com/docs/dataagent/Offline_Task#0dbb27de).


* Check if the newly created custom operator is available.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/099a56eb1366466d98829ad8cf220bd4~tplv-goo7wpa0wc-image.image) </span>

* Check if the default configuration of the custom operator is as expected.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/418ddbf6e44d4258ae97c0211f2ecd67~tplv-goo7wpa0wc-image.image) </span>
