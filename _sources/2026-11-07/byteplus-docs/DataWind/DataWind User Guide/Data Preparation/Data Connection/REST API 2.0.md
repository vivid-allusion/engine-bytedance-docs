---
title: "REST API 2.0"
product: "DataWind"
product_code: "DataWind"
source: "https://docs.byteplus.com/en/docs/DataWind/REST_API_2_0"
---

API is one of the most common solutions for data transmission and interaction between systems. This article describes how to create a new REST API 2.0 data connection.

<span id="_2-快速入门"></span>
# Entry point

<span id="_2-1-从数据连接新建"></span>
## Create from data connection


1. Go to BytePlus, click to enter a specific project, click Data Preparation, find Data Connection in the drop\-down list, and click Data Connection.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Select REST API 2.0 on the page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/efbbed265a0b4dacaed028c8c008cd6a~tplv-goo7wpa0wc-image.image) </span>

3. Next, fill in the required basic information, configure request parsing and path settings, and test the connection. After the connection is successful, click Save to complete all configurations for the current data connection.


<span id="c209220c"></span>
## Create from dataset


1. Go to BytePlus, click Data Preparation \-\-\> Dataset, select the "Create" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. When selecting a data connection, click Create Configuration.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/6a05e37543784bd1b8cfdefbb0571fe4~tplv-goo7wpa0wc-image.image" width="610px" />   </div>
   

3. The following steps are the same as steps 2 and 3 of **Create from data connection**. After completing the configuration, you will remain in the pop\-up window for selecting a data connection for the dataset, and you can proceed directly to the next step of dataset creation.


<span id="_3-1-配置基本信息"></span>
# Configure basic information

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c09c861824b44dd58b6ffd320858a4fd~tplv-goo7wpa0wc-image.image) </span>


|Parameters |Configuration instructions |
|---|---|
|Data connection name |Custom names are supported, or you can use the system default name (for example: REST_API_2.0_timestamp). |
|URL address |Enter the complete URL of the API to connect to. Supports cURL import and export. |
|Request method |Supports GET and POST request methods.<br><br><br>* GET: Used to retrieve resources. Parameters are appended to the URL.<br><br>* POST: Used to submit data. Parameters are passed in the request body. |
|OAuth2 authentication |Supports OAuth2 authorization code mode.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Enable this feature when API requests need to access third\-party service interfaces that use the OAuth2 authorization code flow.</div><br> |
|Parameter settings |Construct complete API request parameters, including request headers, request parameters, request body, pre\-processing operations, and post\-processing operations. |
|Advanced settings |Users can configure timeout, retry count, and pagination. |


<span id="8c04c008"></span>
## Data connection name

Custom names are supported, or you can use the system default name (for example: REST_API_2.0_timestamp).

<span id="986f753b"></span>
## **URL address**

Enter the URL address of the API to connect to. The user can enter it manually or use cURL import to fill in the URL address, request method, and parameter settings. For completed configurations, cURL format export is also supported.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>curl</code> is a command\-line tool used to transfer data using various network protocols (such as HTTP, HTTPS, FTP, and more). It supports sending requests and receiving responses, and can include parameters, authentication information, or file content. Example:</div>


<div data-tips="true" data-tips-type="tip">```JSON
curl -X POST "https://api.example.com/import" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com"
  }'
```
</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/11eb42e6fad3463b8d810cd66db5b5e4~tplv-goo7wpa0wc-image.image) </span>


* cURL import: Click the blue "cURL" button, paste the cURL content to be imported into the pop\-up "Import via cURL" window, and click "Parse and Import". The system will automatically recognize the URL address, request method, and parameter settings, and fill them in the corresponding fields.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cfc930805c214a3da22e6aef8f796aac~tplv-goo7wpa0wc-image.image) </span>

* cURL export: After manually configuring the URL address, request method, and parameter settings, to export in cURL format, click "Export." In the pop\-up "Export cURL" window, click "Copy." The system will automatically generate the cURL format content and copy it to the clipboard.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f60fe2f887d743bc8273ed2b72631bf8~tplv-goo7wpa0wc-image.image) </span>

<span id="6391e07b"></span>
## **Request method**

Supports GET and POST request methods.


* GET: Used to retrieve resources, with parameters appended to the URL.

* POST: Used to submit data, with parameters passed in the request body.


<span id="b6e085fe"></span>
## OAuth2 authentication

Supports OAuth2 authorization code mode.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Enable this feature when an API request needs to access a third\-party service interface that uses the OAuth2 authorization code flow.</div>



1. Configure basic information. Click Authorize to open the sidebar, then enter the basic authorization information (AK, SK, and authorization redirect address). For details on how to obtain these, refer to the relevant third\-party website documentation. After configuration, click "Next."

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dbcdcab14c4d4a6f8b8ae2bc44f36bd9~tplv-goo7wpa0wc-image.image) </span>

2. If the user is configuring authorization information with this combination of AK and authorization redirect address for the first time, it is necessary to further obtain the AccessToken configuration and RefreshToken configuration. Configure the API address, request method, request parameters, response parameters, and other related information. After clicking Confirm, the browser will automatically initiate the request authorization link and redirect to the third\-party authorization page.

3. After the user completes authorization, the ABI unified authorization callback address is automatically invoked. The ABI callback will, based on the user's previous authorization configuration, initiate the [Get Access Token] and [Get Refresh Token] requests in the backend. After verification is successful, the configuration takes effect. You can see the completed authorization on the data connection page.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Authorization for third\-party websites is usually based on a single AK dimension. If multiple data connections use the same AK, they must share the same authorization.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The system will automatically match a valid authorization based on the host and AK of the authorization link; if none exists, initial configuration is required.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The system cannot validate third\-party output parameters (as there is no unified format). Please <strong>carefully check the parameters</strong> to avoid interface failures caused by incorrect parameters. If the authorization address and AK are the same, the system will automatically match the previous configuration. Incorrectly matched data can only be corrected and reconfigured.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">In the [Obtain Access Token] callback request, the parameter key corresponding to code is fixed as "code" and cannot be modified.   </div>
   


<span id="d2f5099b"></span>
## Parameter settings

The parameter settings section guides the user through a standardized process to configure the basic information for the API request, including request headers, request parameters, request body, as well as pre\-processing and post\-processing operations. The system provides built\-in variables and built\-in functions. For details, refer to [Built-in system variables](https://docs.byteplus.com/docs/DataWind/REST_API_2_0#497429b3) and [Built-in system functions](https://docs.byteplus.com/docs/DataWind/REST_API_2_0#88ac317d).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">The parameter value supports both static and dynamic parameter values. The specific entry requirements are as follows:</div>



* <div data-tips="true" data-tips-type="tip">Static parameter value: Enter the specific value of the API parameter, such as "male".</div>


* <div data-tips="true" data-tips-type="tip">Dynamic parameter value: Please enter it in the format ${params}, where params refers to the name of the output field from the "preceding operation". The value under this field will be used as the input value for the API parameter. For example, in the following scenario, suppose the API input parameter is object_id, and you want to use the value of the field unit_id from the "preceding operation" as the input value for object_id. In the API configuration, the key is object_id and the value is ${unit_id}.</div>



<span id="cf65f70c"></span>
### **Request headers**

Supports configuring key and value, and adding or deleting operations. Up to 10 groups can be configured.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3c52b0c80a594977b940e5ea62078187~tplv-goo7wpa0wc-image.image) </span>

<span id="91ac23d9"></span>
### **Request parameters**

Enter all query parameters required by the API.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b7f69364a98477085c72227d1733de6~tplv-goo7wpa0wc-image.image) </span>

<span id="3bca3bec"></span>
### **Request body**

Select the request body type (raw, form\-data, or x\-www\-form\-urlencoded). All types support entering a JSON format request body.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fb891e59609a45dc8ac0173f0691be66~tplv-goo7wpa0wc-image.image) </span>

General rule: When operating on JSON, `$` represents the root node, and `.` represents accessing a child node.

If the JSON data is as follows:

```Java
{
  "showapi_res_error": "",
  "showapi_res_id": "6597a2f5fb638cf45b4d460c",
  "showapi_res_code": 0,
  "showapi_fee_num": 1,
  "showapi_res_body": {
    "list": [
      {
        "time": "14:26:57",
        "zhesuan": "193.69",
        "code": "AED",
        "hui_out": "195.91",
        "chao_in": "192.95",
        "chao_out": "199.47",
        "name": "阿联酋迪拉姆",
        "hui_in": "194.55",
        "day": "2024-01-05"
      },
      {
        "time": "14:26:57",
        "zhesuan": "477.56",
        "code": "AUD",
        "hui_out": "481.77",
        "chao_in": "478.08",
        "chao_out": "483.16",
        "name": "澳大利亚元",
        "hui_in": "478.57",
        "day": "2024-01-05"
      }
    ],
    "listSize": 28,
    "ret_code": 0
  }
}
```


Then the values corresponding to some paths are as follows:

```Java
$.showapi_fee_num = 1
$.showapi_res_id = "6597a2f5fb638cf45b4d460c"
$.showapi_res_body.list.* = [{"time":"14:26:57","zhesuan":"193.69" ... // Omitted below
```


<span id="5af6b36f"></span>
### **Pre\-processing operations**

To perform additional steps to prepare data or obtain necessary information before the main request, use this configuration.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0787c2b0f3024cd1b8c78e95172a8384~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">You can set up to 5 preceding operations.</div>



1. Click the "Add pre\-request operation" button. On the configuration page, enter the detailed information for the pre\-request operation, including the URL address, request method, and more.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b13b0f7fb8574f28b4d73264a8d34406~tplv-goo7wpa0wc-image.image) </span>


2. After clicking "Initiate request", the system will parse this pre\-request and display the parsing result in the "Request result" area. The user needs to configure the key for the dynamic parameter and the result field path to facilitate applying the pre\-request result to the current request. For guidance on writing dynamic parameters, refer to [Dynamic parameter writing rules](https://docs.byteplus.com/docs/DataWind/REST_API_2_0#c163c21e).

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2c9b56ac502049e5ad3ea632f0ac06e9~tplv-goo7wpa0wc-image.image) </span>


<span id="bfbcd913"></span>
### **Post\-request operation**

Provides a more flexible and powerful way to configure custom parameters, supports **Groovy syntax**, and allows users to write code to implement multi\-level request parsing. For rules on writing post\-request operations, refer to [Rules for writing post-processing operations.](https://docs.byteplus.com/docs/DataWind/REST_API_2_0#d8efbf6a).

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7eb385cd3164736b08cadd49dce3351~tplv-goo7wpa0wc-image.image) </span>

<span id="e9bf3b6d"></span>
## Advanced settings

Allows users to configure the request timeout, number of retries, pagination, and more.


|Parameter |Configuration instructions |
|---|---|
|Timeout |The maximum time to wait for a response to an input request (unit: milliseconds). The default is 3 minutes. |
|Retry count |When a request fails, the number of retry attempts the system will make, up to 5 times. |
|Pagination |After enabling the pagination feature, configure as required. The termination condition is a Groovy expression. For details, refer to [Rules for writing termination conditions](https://docs.byteplus.com/docs/DataWind/REST_API_2_0#15e710b5).<br><br><span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d5c3e3c65f9d4567bd6ca4c6bf837de9~tplv-goo7wpa0wc-image.image) </span><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">To handle excessive user fields or large data volumes, it is recommended to enable pagination mode.</div><br> |


Pagination types include numeric pagination and cursor pagination:


|Numeric pagination (for APIs with explicit page numbers) |Cursor pagination (for APIs without fixed page numbers) |
|---|---|
|<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/555d7c3362bf43c2ac36449db05812e1~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Retrieve data page by page using the page number. This is suitable for scenarios where the total number of pages is known or for sequential pagination. |<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46cd3c265f1b4cbd853c37fa5482180f~tplv-goo7wpa0wc-image.image) </span><br><br><br>* Use the "cursor" returned from the previous page as the parameter for the next page request. This approach is suitable for pagination scenarios involving large volumes of data or unordered data. |


The relevant parameter configuration instructions are as follows:


|Parameters |Configuration notes |
|---|---|
|Starting page |Applicable to numeric pagination. Defines the starting page number for pagination requests, specifying from which page to begin retrieving data. |
|Pagination parameter path |Applicable to cursor pagination. Points to the JSON path where the cursor is stored in the response (must be of Map or Arraytype, such as `$.showapi_res_body.list.*`). |
|Request interval |Controls the interval between consecutive pagination requests (unit: milliseconds) to prevent triggering API rate limits due to high\-frequency requests. |
|Maximum pagination |Limits the maximum number of requests (to avoid infinite loops). The maximum page number for pagination is 10,000, with a default of 10. |
|Termination condition |Supports writing Groovy expressions to calculate the termination condition based on the current request.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Two examples are provided below:</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">response.data.size()==0 means that pagination stops when the length of the data list under response is 0 (an empty list)</div><br><br><br>* <div data-tips="true" data-tips-type="tip">response.hasMore == false means that pagination stops when hasMore under response is false</div><br> |


Field count, items per page, and pagination configuration limits:


|Configuration items |Note |Configuration limits |
|---|---|---|
|Number of fields |Total number of data fields to be processed |It is recommended to keep the number of fields within 150. |
|Entries per page |Number of data entries displayed per page |It is recommended that the product of the number of fields and entries per page be less than 10,000. The pagination size should take into account the interface's performance, number of fields, and data volume. |
|Pagination page number |Maximum number of pages that can be requested (pagination stops if exceeded) |The maximum pagination page number is 10,000. |


Example:

For example, to end pagination when the data list in the request result is empty, and to set the maximum pagination as the upper limit for the number of requests (default is 10, maximum is 10,000), configure as follows:

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88fc3d87e9524a1d8c94f34aa50dda88~tplv-goo7wpa0wc-image.image" width="1940px" /></div>


When in use, reference ${pageNum}; this variable will start from the initial page and continue until the termination condition is met.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2170eab6141b42ab957a9046d0d1e155~tplv-goo7wpa0wc-image.image) </span>

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">The parameter key "page" in the screenshot example must be replaced with the actual pagination parameter name accepted by the interface being integrated.</div>


* <div data-tips="true" data-tips-type="tip">Users can also add any other parameters supported by the interface to meet the requirements of different scenarios. For example, if supported by the interface, you can add a pagination size parameter (such as perPage or pageSize) to control the amount of data read in each batch.</div>



<span id="_3-2-配置参数"></span>
# Configure request parsing and path

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cd3a2e8c59ff49f284b819fab61aae6c~tplv-goo7wpa0wc-image.image) </span>


|Parameters |Configuration notes |
|---|---|
|Parsing result |After completing the **basic information configuration** operation, click **Send request**. The system will parse the request and display the parsing result here. |
|Field path |The root path specified when parsing the API request result, used to locate the data's position in the JSON structure (must be of Map or Arraytype, such as `$.showapi_res_body.list.*`). |
|Field settings |The path of the final field obtained after parsing the root path, which is also the final field result of this data connection. |
|Data preview |This section supports previewing the first 100 rows of detailed data for the currently selected field. |


<span id="64ebf4c7"></span>
## Configure request parsing

After completing the above basic information configuration, you can click "**Send request**" and the system will parse the request. The parsing order is "Pre\-request operation" \> "Current request" \> "Post\-request operation", and the "Parsing result" will be displayed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ff1c27a21f234bfa86f7d4a103b019c2~tplv-goo7wpa0wc-image.image) </span>

<span id="1ab50824"></span>
## Configure path

After the system completes request parsing, the user also needs to complete the path configuration, including setting the field path, setting fields, and data preview.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ba220eeae95465baf6b0ff6e7d671a5~tplv-goo7wpa0wc-image.image) </span>

<span id="4a470951"></span>
### **Field path**

Enter the field path, using $ to indicate the root node and the dot (.) to indicate child nodes. Click the "Get Fields" button to have the system parse and display the "Field Configuration" area.

This section configures the root path of the parsing result, with the following rules:


* The root path must point to **a Map or an Array**; otherwise, the field keys cannot be parsed.

* If it points to an Array, it must be written in a form that allows keys to be parsed, such as ending with `.*`, for example `$.list.*`. Do not write it as `$.list`, as this will not allow keys to be parsed.

* After configuration is complete, clicking Get Fields will only parse the first\-level field structure under this path, and all these fields will be basic data types.


Example:

```Java
// Retrieve the entire result. The result contains fields including: showapi_res_error, showapi_res_id, ..., showapi_res_body
$
// Retrieve the contents of the array
$.showapi_res_body.list.* = [{"time":"14:26:57","zhesuan":"193.69" ... // The following is omitted
```


<span id="c62fe019"></span>
### **Field configuration**

Use the "Add" button to create new fields. The parsing logic uses the rootPath you entered as the basis for parsing the result. Additionally, deleting configured fields is supported.

This section configures the path of the final fields obtained after parsing the root path, which is also the final field result of this data connection.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">For cases where the root path is an array, if the field path prefix does not match the root path, the value corresponding to that field will be calculated and directly added to each element of the array in the final result set.</div>


<div data-tips="true" data-tips-type="warning">For example, for weather data, if the root path is $.forcast15days.list.\*, which represents the weather for the next 15 days, and the user adds a $.city field to represent the city, then the value of $.city will be calculated and directly added to each future weather entry as a key named city. <strong>The value is the same for each item in the array.</strong></div>


<span id="52e07533"></span>
### **Data preview**

Click the "Data Preview" button to view the first 100 rows of detailed data for the currently selected field.

<span id="92d1a689"></span>
# Test connection and save

After all content is configured, click **Test Connection** to perform a connectivity test for the data source. After the test is successful, click **Save** to complete all configurations for the current data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d6980adf0307483db802d7000ae3259a~tplv-goo7wpa0wc-image.image) </span>

<span id="c6c1d48e"></span>
# Next steps: Create a dataset


1. To create a dataset using the previously created data connection: Click Data Preparation \-\-\> Dataset, then select the "Create" button in the upper left corner to create a new dataset.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1a122b624fe7494684d19c0ccea499a3~tplv-goo7wpa0wc-image.image" width="2940px" />   </div>
   

2. Search for or select the previously created data connection from the dropdown.

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9a651f6ad12b4c979484f619a376fd84~tplv-goo7wpa0wc-image.image" width="450px" />   </div>
   


<span id="d9fc967c"></span>
# Related references

<span id="c163c21e"></span>
## Dynamic parameter writing rules

Both dynamic parameters and post\-processing scripts use Groovy as the script engine.

For ${} appearing in params, body, header, or url, **execute them as Groovy string interpolation expressions to obtain the result**. Additionally, some custom functions are built in, such as the md5() method, date variables, and more. The following are some examples of execution results:

```JSON
假如目前有两个参数，是在前置请求中配置好的，如下：
num1 = 1
num2 = 2

则${}里面的内容会被作为表达式执行，其余部分为普通字符串，下面表达式结果分别为：
abc               // abc
${num1}           // 1
${num1+num2}      // 3
${num1}+num2      // 1+num2
${num3}           // Error: no num3 parameter
${"${num1}"}      // ${num1}
```


<span id="d8efbf6a"></span>
## Rules for writing post\-processing operations.

Example of writing a post\-processing operation:

```Java
def convertJson(response) {
    /*Enter post-processing code hereresponse represents the result returned by the API. Suppose the API returns the following result    {"city": "上海市",        "forcast": [            {"temperature": 5, "day": "2024-01-01"},            {"temperature": 6, "day": "2024-01-02"},        ],        "test": "test"    }Some code examples:Scenario 1: Add, edit, and loop to add the city to each element in the list    ls = response.forcast    for (i=0; i< ls.size(); i++) {        ls[i].city = response.city    }Scenario 2: Remove a key    response.remove("test")    */
    return response;
}
```


<span id="15e710b5"></span>
## Rules for writing termination conditions

Groovy syntax is supported. When the termination condition is met, it will not proceed to the next page. response represents the result of the current request. Example:

```JSON
response.data.size() == 0   // Stop pagination when the length of the data list under response is 0 (empty list)
response.hasMore == false // Stop pagination when hasMore under response is false
```


<span id="497429b3"></span>
## Built\-in system variables

The following dynamic parameters are built into the system. When naming variables, do not use the same names as system variables, or the system variables will override them.

> Scope of effect: url, header, params, body. Not valid in post\-processing operations.


```Java
${date} // Date, format: yyyyMMdd
${DATE} // Date, format: yyyy-MM-dd
${hour} // Hour, format: HH
${HOUR} // Hour, format: H
${year} // Year, format: yyyy
${month} // Month, format: MM
${day} // Day, format: dd
${timestamp} // Timestamp, format: 13-digit timestamp
${last_date} // Last day of previous month, format: yyyyMMdd
${last_DATE} // Last day of previous month, format: yyyy-MM-dd
${last_day} // Last day of previous month, format: dd

以上变量支持日期加减，例如 ${date-1}，代表前一天
```


<span id="88ac317d"></span>
## Built\-in system functions

> Scope of effect: url, header, params, body, post\-processing operations.


<span id="04eb12f6"></span>
### Instructions for use

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can use the free <a href="https://echo.free.beeceptor.com">API debugging tool</a> for testing.</div>



* Within the scope of built\-in system functions, you can use the "${}" syntax to call supported built\-in functions and predefined variables (the content inside the curly braces is a Groovy expression).

* Multi\-line statements are supported. Separate multiple statements with semicolons. When using multiple expressions, the final value is the return value of the last expression.

* Example:

   * Add an md5 value and the current system timestamp to the URL


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2367a535518a42b588e5e84a0cfe5c99~tplv-goo7wpa0wc-image.image) </span>


* Add a value calculated by a complex expression to the request header

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/56c90ec1d0bf4d6ba843d79014319e62~tplv-goo7wpa0wc-image.image" width="1908px" />   </div>
   


<span id="607c517e"></span>
### Digest functions

```Java
String md2Hex(String data);
String md5Hex(String data);
String shaHex(String data);
String sha1Hex(String data);
String sha256Hex(String data);
String sha384Hex(String data);
String sha512Hex(String data);

byte[] md2(String data)
byte[] md5(String data)
byte[] sha(String data)
byte[] sha1(String data)
byte[] sha256(String data)
byte[] sha384(String data)
byte[] sha512(String data)
```


<span id="a2dd93d4"></span>
### Mathematical functions

```Java
java.lang.Math all related functions
```


<span id="efdc6e5a"></span>
### Obtain date and time, format, and perform date addition or subtraction

```Groovy
// format: Format date as a string.
currentDate = new Date()
formattedDate = currentDate.format('yyyy-MM-dd HH:mm:ss')

// plus and minus: Date addition and subtraction operations.
tomorrow = currentDate + 1 
yesterday = currentDate - 1 
```


<span id="7daeb92f"></span>
### String extension methods

```Java
// capitalize(): Capitalize the first character of a string.
str = "groovy"
str.capitalize() // Output: "Groovy"

// reverse(): Reverse a string.
str.reverse()     // Output: "yvoorg"

// contains(): Check whether a string contains the specified substring.
str.contains("oo") // Output: true

// toInteger(), toLong(), toFloat(), toDouble(): Convert a string to the corresponding numeric type.
str = "123"
str.toInteger() // Output: 123

// split(): Split a string.
str = "a,b,c"
str.split(",") // Output: ["a", "b", "c"]

// isNumber(): Check whether a string is a number.
str.isNumber() // Output: true
```


<span id="353de184"></span>
### Collection extension methods

```Java
// each: Execute a closure operation on each element of the collection.
list = [1, 2, 3]
list.each { println it } // Output: 1 2 3

// findAll: Filter elements in the collection that meet the criteria.
list = [1, 2, 3, 4, 5]
evens = list.findAll { it % 2 == 0 }
println evens // Output: [2, 4]

// collect: Map each element in the collection to another value.
list = [1, 2, 3]
squares = list.collect { it * it }
println squares // Output: [1, 4, 9]

// sum: Calculate the sum of all elements in the collection.
list = [1, 2, 3]
println list.sum() // Output: 6

// join: Concatenate the elements in the collection into a string using the specified delimiter.
list = ["a", "b", "c"]
println list.join("-") // Output: "a-b-c"
```


<span id="2d215576"></span>
### Map extension methods

```Java
// each: Apply a closure to each entry in the Map.
map = [a: 1, b: 2, c: 3]
map.each { key, value -> println "$key: $value" } // Output: a: 1 b: 2 c: 3

// findAll: Filter entries in the Map that meet the criteria.
map = [a: 1, b: 2, c: 3]
filtered = map.findAll { key, value -> value > 1 }
println filtered // Output: [b: 2, c: 3]

// collect: Map each entry in the Map to another value.
map = [a: 1, b: 2, c: 3]
collected = map.collect { key, value -> "$key=$value" }
println collected // Output: ["a=1", "b=2", "c=3"]

// getOrDefault(Object key, Object defaultValue): Retrieve the value for the specified key; if the key does not exist, return the default value.
map = [a: 1, b: 2]
println map.getOrDefault('c', 0) // Output: 0

// collectEntries(Closure closure): Convert the Map to another Map.
map = [a: 1, b: 2, c: 3]
newMap = map.collectEntries { key, value -> [(key): value * 2] }
println newMap // Output: [a: 2, b: 4, c: 6]

// find(Closure closure): Find the first entry in the Map that meets the criteria.
map = [a: 1, b: 2, c: 3]
entry = map.find { key, value -> value > 1 }
println entry // Output: [b:2] or [c:3]

// keySet(): Retrieve all keys in the Map.
map = [a: 1, b: 2, c: 3]
println map.keySet() // Output: [a, b, c]

// values(): Retrieve all values in the Map.
map = [a: 1, b: 2, c: 3]
println map.values() // Output: [1, 2, 3]

// flatten(): Flatten a nested Map.
map = [a: [b: 2, c: 3], d: 4]
println map.flatten() // Output: [a.b:2, a.c:3, d:4]
```


<span id="0ca2e990"></span>
### List extension methods

```Java
// unique(): Remove duplicate elements from the list.
list = [1, 2, 2, 3, 4, 4]
println list.unique() // Output: [1, 2, 3, 4]

// sort(): Sort the list.
list = [3, 1, 4, 1, 5, 9]
println list.sort() // Output: [1, 1, 3, 4, 5, 9]

// flatten(): Flatten a nested list into a single list.
list = [1, [2, 3], [4, [5, 6]]]
println list.flatten() // Output: [1, 2, 3, 4, 5, 6]

// count(Closure closure): Count the number of elements that meet the criteria.
list = [1, 2, 3, 4, 5]
println list.count { it % 2 == 0 } // Output: 2
```


<span id="9b9dcd1b"></span>
### Range extension methods

```Java
// step(int step): Iterate over the elements in the range with the specified step size.
range = 1..10
range.step(2).each { println it } // Output: 1 3 5 7 9

// containsWithinBounds(Object value): Check whether the value is within the range (including boundaries).
range = 1..10
println range.containsWithinBounds(10) // Output: true

// subList(int fromIndex, int toIndex): Get the sublist within the specified index range.
range = 1..10
println range.subList(2, 5) // Output: [3, 4, 5]

// toList(): Convert the range to a list.
range = 1..5
println range.toList() // Output: [1, 2, 3, 4, 5]
```


<span id="2a385d04"></span>
### Encryption methods

```Java
// Base64 encoding and decoding
// Encoding
str = "hello world"
encoded = str.bytes.encodeBase64().toString()
println "Base64 Encoded: $encoded" // Output: Base64 Encoded: aGVsbG8gd29ybGQ=
// Decoding
encoded = "aGVsbG8gd29ybGQ="
decoded = new String(encoded.decodeBase64())
println "Base64 Decoded: $decoded" // Output: Base64 Decoded: hello world
```


<span id="f12d6679"></span>
### Digest methods

```Java
// MD5
str = "hello world"
md5Hex = str.md5()
println "MD5: $md5Hex" // Output: MD5: 5eb63bbbe01eeed093cb22bb8f5acdc3

// SHA-1
str = "hello world"
sha1Hex = str.digest("SHA-1")
println "SHA-1: $sha1Hex" // Output: SHA-1: 2aae6c35c94fcfb415dbe95f408b9ce91ee846ed

// SHA-256
str = "hello world"
sha256Hex = str.digest("SHA-256")
println "SHA-256: $sha256Hex" // Output: SHA-256: b94d27b9934d3e08a52e52d7da7dabfac484eefc56bf5ef4b102e3d8fdedfb68
```


&nbsp;
