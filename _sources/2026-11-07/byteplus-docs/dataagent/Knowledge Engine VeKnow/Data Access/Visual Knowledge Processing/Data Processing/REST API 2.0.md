---
title: "REST API 2.0"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/REST_API_2_0_"
---

<span id="92235cec"></span>
# **Feature Overview**

REST API 2.0 calls are all kinds of request processing tools in the special area operator, which can use the output data of the upstream node as the imported parameter of the API to query the data for data completion. This article describes how to call operators using REST API 2.0.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Enterprise administrators can choose to configure default information for REST API 2.0 according to business needs, or they can add more custom operators based on REST API 2.0 to adapt to different businesses. For specific operations, see <a href="https://docs.byteplus.com/docs/dataagent/Manage_Custom_Operators">Manage Custom Operators</a>.</div>


<span id="338932cd"></span>
# Operation steps

<span id="632aca91"></span>
## Step 1: Create a new REST API 2.0 call


1. In the left navigation bar of Enterprise Knowledge Engine, select **Data Access** \> **Visual Knowledge Processing** .

2. In the upper left corner of the **Task List** page, click **New** and select **New Offline Task** .

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/821d810fbdc5401db4b70e11a6f708a8~tplv-goo7wpa0wc-image.image) </span>

3. Follow [Offline Task](https://docs.byteplus.com/docs/dataagent/Offline_Task)the steps in Create Offline Task and select Add REST API 2.0 call from Featured Zone Operator for data connection while processing the node.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7b6ff765a6154ada9b8d3205e00ecbc4~tplv-goo7wpa0wc-image.image) </span>


<span id="9d858d3a"></span>
## Step 2: Configure basic information

On the basic information page, configure the relevant parameters:


|parameter |explain |
|---|---|
|URL Address |Fill in the complete URL of the API you need to connect to. Support for import and export of cURL. |
|request method |It supports GET and POST request methods.<br><br><br>* GET: Used to retrieve resources, parameters are attached to the URL<br><br>* POST: used to submit data, parameters are passed through the request body |
|OAuth2 authentication |Supports OAuth2 authorization code mode.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Enable this feature when an API request requires access to a third\-party service interface using OAuth2 authorization code mode.</div><br> |
|parameter setting |Construct complete API request parameters, including request header, request parameters, request body, pre\-operation and post\-operation. |
|Advanced Settings |Support users to set timeouts, retries, and pagination. |



1. **Configure URL address**


Fill in the URL address of the API you need to connect to. You can fill it in manually, or you can fill in the URL address, request method and parameter settings by cURL import. For the relevant configuration filled in, cURL format export is also supported.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><code>Curl</code>is a command line tool for transferring data over various network protocols such as HTTP, HTTPS, FTP, etc. It supports sending requests, receiving responses, and can carry parameters, authentication information, or file content. Examples are as follows:</div>


<div data-tips="true" data-tips-type="tip">```C
curl -X POST "https://api.example.com/import" \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{
    "name": "John Doe",
    "email": "john@example.com"
  }'
```
</div>


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8321f0661df84b6ab620ab563aa9b45a~tplv-goo7wpa0wc-image.image) </span>


* cURL Import: Click the "cURL" button, paste the cURL content that needs to be imported in the "Import via cURL" window that pops up, and click "Parse and Import". The system will automatically identify the URL address, request method, and parameter setting information, and fill in the corresponding location.

* cURL export: After manually configuring the URL address, request method, and parameter settings, if you need to export to cURL format, click "Export", and click "Copy" in the pop\-up "Export cURL" window, the system will automatically generate the cURL format content and copy it to the clipboard.

2. **Configuration request method**


It supports GET and POST request methods.


* GET: Used to retrieve resources, parameters are attached to the URL

* POST: used to submit data, parameters are passed through the request body

3. **Configuring OAuth2 Authentication**


Supports OAuth2 authorization code mode.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Enable this feature when an API request requires access to a third\-party service interface using OAuth2 authorization code mode.</div>



1. Click Authorize, open the sidebar, and enter the basic authorization information (AK, SK, and authorized jump address) here. For the specific acquisition method, see the relevant three\-party website documents. Click "Next" after the configuration is completed.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4facf6d287e64f819e1da5472c742c84~tplv-goo7wpa0wc-image.image) </span>

2. If the user is using the combination of AK and authorization jump address to configure authorization information for the first time, it is necessary to further obtain the AccessToken configuration and RefreshToken configuration. Configure the API address, request method, request parameters, return parameters and other relevant information, click Confirm, and the browser will automatically initiate the request authorization link to jump to the three\-party authorization page.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1e8b8bd17e83432ea4231efbaf939010~tplv-goo7wpa0wc-image.image) </span>

3. After the user completes the authorization, it will automatically call back the ABI unified authorization callback address. The ABI callback will initiate a [Get Access Token] [Get Refresh Token] request synchronously in the background according to the previous user's authorization configuration. After the verification is passed, the configuration will take effect. You can see the completion of the authorization when you return to the data connection page.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The three\-party website authorization is usually for a single AK dimension, and if multiple data links use the same AK, they need to share the same authorization.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The system will automatically match the valid authorization according to the authorization link host and AK; if not, it needs to be configured for the first time.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">The system cannot verify the three\-party exported parameter (no uniform format), please <strong>check the parameters carefully</strong> to avoid the interface returning failure due to parameter errors. If the authorization address is the same as the AK, the system will automatically match the last configuration, and the mismatch data can only be corrected and reconfigured.   </div>
   

   * <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">[Get Access Token] The parameter key corresponding to the code in the callback request is fixed as "code" and cannot be modified.   </div>
   

4. **Configuration parameters**


The parameter setting section guides the user through a standardized process to configure the basic information of the API request, including request headers, request parameters, request body, and pre/post operations. The system provides built\-in variables and built\-in functions, please refer to [System built-in variables](https://docs.byteplus.com/docs/dataagent/REST_API_2_0_#1d0f6685), [System built-in function](https://docs.byteplus.com/docs/dataagent/REST_API_2_0_#e4d80a4c).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Parameter value supports static parameter values and dynamic parameter values. The specific specifications are as follows:</div>



* <div data-tips="true" data-tips-type="tip">Static parameter value: Just fill in the specific value of the API parameter, such as "male".</div>


* <div data-tips="true" data-tips-type="tip">Dynamic parameter values: Please fill in the format of ${params}, where params refers to the name of the "pre\-operation" output field, and the value under this field will be used as the imported parameter value of the API parameter. For example, if the imported parameter of the API is object_id, and the value of the field unit_id in the "pre\-operation" is used as the imported parameter value of the object_id, then in the API configuration, the key is object_id and the value is ${unit_id}.</div>


* **Request header** : support configuration key, value, support add, delete operations, up to 10 groups can be configured.

* **Request parameters** : Enter all query parameters required by the API.

* **Request body** : Select the request body type (form\-data or raw), both of which support the user to enter the request body in JSON format.

   General: To operate on JSON, `$`represents the root node, `and the.`sign represents the sub\-node.

   If the JSON data is:

   ```JSON
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
           "name": "阿联酋迪拉姆", // which means "UAE Dirham"
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
           "name": "澳大利亚元", //which means "Australian dollar"
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

   ```JSON
   $.showapi_fee_num = 1
   $.showapi_res_id = "6597a2f5fb638cf45b4d460c"
   $.showapi_res_body.list.* = [{"time":"14:26:57","zhesuan":"193.69" ... //omitted later
   ```
   

   * **Pre\-operation:**  This configuration can be done when you need to perform some extra steps to prepare data or obtain necessary information before the main request.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/da911c27e86b4869ac0f246191ee4751~tplv-goo7wpa0wc-image.image) </span>

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">You can set up to 5 pre\-operations.   </div>
   

   1. Click "+ Add a pre\-operation", and you need to enter the details of the pre\-operation on the configuration page, including URL address, request method, etc.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fc1bbdad99094d3cb4e722bb9db1b585~tplv-goo7wpa0wc-image.image) </span>

   2. After clicking "Initiate Request", the system will parse the pre\-request and present the parsing result in the "Request Result" area. The user needs to configure the key and result field path of the dynamic parameters to facilitate subsequent application of the pre\-request result to the current request. Dynamic parameter preparation can be referred to [Dynamic parameter writing rules](https://docs.byteplus.com/docs/dataagent/REST_API_2_0_#dc238525).

   * **Post\-operation:**  Provide a more flexible and powerful way to configure custom parameters, support **groovy syntax** , and support users to write code to achieve multi\-level request parsing. The post\-operation writing rules can be referred to [Postaction writing rules](https://docs.byteplus.com/docs/dataagent/REST_API_2_0_#6d7a0980).

      <div style="text-align: right">
      <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/208d867885214e2b99c989d0dd96a7eb~tplv-goo7wpa0wc-image.image" width="2034px" />      </div>
      

5. **Configure advanced settings**


Support users to set the timeout time, retry times, and pagination of sending requests.


|parameter |configuration instructions |
|---|---|
|parallelism |The parallelism degree sets the parallelism degree of a single Partition of a Spark task. The actual final parallelism degree is affected by the number of Partitions assigned to the task. The number of parallelism during actual execution is related to the resources available to the cluster. It is recommended that the user compute the parallelism reasonably according to the interface performance of the call (QPS, QPM, etc.). Default is 1. |
|timeout |Enter the maximum time (in milliseconds) for a request to wait without a response. The default is 3 minutes. |
|number of retries |When the request fails, the system attempts to retry up to a maximum of 5 times. |
|request interval |The final QPS of the task depends on the number of cores allocated by the output node and the request interval. Adjusting the request interval can control the task concurrency. The smaller the request interval, the larger the QPS.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">Please set the request interval carefully, there is a service risk if the concurrency is too high (when the QPS of a single task \> the global QPS, the global QPS shall prevail)</div><br> |
|complete exception handling |* Terminate the task: If the call fails, the task fails and intermediate results are cleared.<br><br>* Ignore Exceptions: Ignore the data of failed calls, fill with null, preserve the results of successful calls, task success, tolerance mode. |



6. **Configure the resolution request and path**

   1. After completing the above configuration operation, you can click " **Send Request** " and the system will parse the request.

      The order of parsing is "pre\-operation" \> "current request" \> "post\-operation", and the "parse result" will be rendered.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/137786517de74929aef26079ed325af7~tplv-goo7wpa0wc-image.image) </span>

   2. After the system completes the parsing request, the user also needs to complete the path configuration operation, including setting the field path, setting the field, and previewing the data.

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0aeff1ed49a24962b39eb3573161a5c0~tplv-goo7wpa0wc-image.image) </span>

   
   |parameter |configuration instructions |
   |---|---|
   |field path |Enter the field path, using $for the root node and the. sign for the sub\-node. Click the "Get Field" button, and the system will parse and display the "Field Configuration" area.<br><br>The root path of the parsing result is configured here, and the rules are as follows:<br><br><br>* The root path **must be a Map or Array < Map \>**  , otherwise the key of the field cannot be resolved.<br><br>* If pointing to an Array < Map \>, it must be written in a form that can resolve the key, such as ending with `. *`, such as `$.list. *`, and must not be written directly as `$.list`, so that the key cannot be resolved.<br><br>* After the configuration is complete, clicking Get Fields will only resolve the first\-level field structure under the path, and these fields are all basic data types.<br><br><br>Example:<br><br>```Java```<br>```//Take the whole result, the result in the fields include: showapi_res_error, showapi_res_id,..., showapi_res_body```<br>```$```<br>```//fetch the contents of the array```<br>```$.showapi_res_body.list.* = [{"time":"14:26:57","zhesuan":"193.69" ... //omitted later```<br> |
   |field configuration |Use the "Add" button to support new fields, and the parsing logic will parse the results based on the rootPath you entered. Also, it supports deleting configured fields.<br><br>The configuration here is the path of the final field obtained after the root path is resolved, and it is also the final field result of the data connection.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">For the case where the root path is an array, if the field path prefix is inconsistent with the root path, the resulting result set will calculate the value corresponding to the field and add it directly to each element of the array.</div><br><br><br><div data-tips="true" data-tips-type="warning">For example, for weather data, the root path is $.forcast15days.list. \*, which represents the weather in the next 15 days. If the user adds a $.city field to represent the city, the value of $.city will eventually be calculated and added directly to each future weather data as a key called city. <strong>The value of each item in the array is the same.</strong></div><br> |
   |data preview |Click the "Data Preview" button to view the first 100 rows of detailed data for the currently selected field. |
   


<span id="cfa7b99a"></span>
## Step 3: Test execution

Click "Test Execution". After the test is successful, click "Save" to complete all configurations of the current data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/331f2f0f9b9b4ed480a91f005692d563~tplv-goo7wpa0wc-image.image) </span>

<span id="9084efdc"></span>
# Related reference

<span id="dc238525"></span>
## Dynamic parameter writing rules

Both dynamic parameters and post\-script use Groovy as the scripting engine.

For ${} occurrences in params, body, header, url, **execute as groovy's string interpolation expression to get the result** . Also, some custom functions are built\-in, such as the md5 () method, date variables, and so on. Here are some examples of execution results:

```Groovy
//If there are currently two parameters configured in the pre request, as follows:
num1 = 1
num2 = 2

//The content inside ${} will be executed as an expression, 
//while the rest will be a regular string. The following expression results are:
abc               // abc
${num1}           // 1
${num1+num2}      // 3
${num1}+num2      // 1+num2
${num3}           //Error, no num3 parameter
${"${num1}"}      // ${num1}
```


<span id="6d7a0980"></span>
## Postaction writing rules

An example of postaction writing is as follows:

```Java
def convertJson(response) {
    /*    Fill in the post-operation code here.    Response represents the result returned by the api, assuming the result returned by the api is    {        "City": "Shanghai",        "forcast": [            {"temperature": 5, "day": "2024-01-01"},            {"temperature": 6, "day": "2024-01-02"},        ],        "test": "test"    }    Some code examples:    Scenario 1: Add, edit, loop, add city to each element in the list    ls = response.forcast    for (i=0; i< ls.size(); i++) {        ls[i].city = response.city    }    Scenario 2: Delete a key    response.remove("test")    */
    return response;
}
```


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ee21fb74aef84f8e9bbe9bd07ffb630b~tplv-goo7wpa0wc-image.image) </span>

<span id="9e364bcb"></span>
## Termination condition writing rule

Support for groovy syntax, no longer proceed to the next page when a termination condition is reached. Response represents the result of this request.

<span id="1d0f6685"></span>
## System built\-in variables

The built\-in dynamic parameters of the system are as follows. Do not name variables with the same name as the system variable name, otherwise they will be overwritten by the system variable.

> Effective scope: URL, header, params, body. Invalid in post operation.


```Java
${date} //date, format: yyyyMMdd
${DATE} //date, format: yyyy-MM-dd
${hour} //hour, format: HH
${HOUR} //hour, format: H
${year} //year, format: yyyy
${month} Month, format: MM
${day} //day, format: dd
${timestamp} //timestamp, format: 13-digit timestamp
${last_date} Last day of last month, format: yyyyMMdd
${last_DATE} //Last day of last month, format: yyyy-MM-dd
${last_day} Last day of last month, format: dd

The above variables support adding and subtracting dates, for example, ${date-1} represents the previous day
```


<span id="e4d80a4c"></span>
## System built\-in function

> Effective scope: URL, header, params, body, post operation.


**Instructions for use**

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can use free <a href="https://echo.free.beeceptor.com">interface debugging tools </a>for testing.</div>



* Within the scope of system built\-in functions, you can use the "${}" syntax to use supported built\-in functions as well as predefined variables (the content in curly brackets is a Grovvy expression).

* Supports multi\-line statements, which are separated by semicolons; when using multi\-line expressions, the final value is the return value of the last expression.

* Example:

   * Add md5 value and current system timestamp to URL

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3079ac26a26444378a66be836c8f8e11~tplv-goo7wpa0wc-image.image) </span>

   * Add the value evaluated by a complex expression to the request header

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c4441bd13fe849a887559563043ebcaf~tplv-goo7wpa0wc-image.image) </span>


<span id="b598ef0f"></span>
### **Summary function**

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


<span id="b35ff055"></span>
### **Mathematical function**

```Java
java.lang.Math all related functions
```


<span id="b63ff714"></span>
## Get datetime, formatting, date addition and subtraction

```Groovy
//format: format the date as a string.
currentDate = new Date()
formattedDate = currentDate.format('yyyy-MM-dd HH:mm:ss')

//plus and minus: addition and subtraction of dates.
tomorrow = currentDate + 1 
yesterday = currentDate - 1 
```


<span id="e2685e01"></span>
## String extension method

```Java
Capitalize (): Capitalize the first character of the string.
str = "groovy"
str.capitalize() //Output: "Groovy"

//reverse (): Inverts the string.
str.reverse()     //output: "yvoorg"

//contains (): Checks whether the string contains the specified substring.
str.contains("oo") //output: true

//toInteger (), toLong (), toFloat (), toDouble (): Converts string to the corresponding numeric type.
str = "123"
str.toInteger() //Output: 123

//split (): Split the string.
str = "a,b,c"
str.split(",") //Output: ["a", "b", "c"]

//isNumber (): Checks if string is a number.
str.isNumber() //output: true
```


<span id="df6cfa81"></span>
## Collection extension method

```Java
//each: Performs a closure operation on each element of the collection.
list = [1, 2, 3]
list.each { println it } //output: 1 2 3

//findAll: Filter the elements in the collection that meet the criteria.
list = [1, 2, 3, 4, 5]
evens = list.findAll { it % 2 == 0 }
println evens //output: [2, 4]

Collect: Maps each element in the collection to another value.
list = [1, 2, 3]
squares = list.collect { it * it }
println squares //Output: [1, 4, 9]

//sum: Compute the sum of all elements in the set.
list = [1, 2, 3]
println list.sum() //output: 6

Join: Concatenates the elements in the collection into a string with the specified delimiter.
list = ["a", "b", "c"]
println list.join("-") //output: "a-b-c"
```


<span id="f4337252"></span>
## Map extension method

```Java
//each: Perform a closure operation on each entry in the Map.
map = [a: 1, b: 2, c: 3]
map.each { key, value -> println "$key: $value" } //Output: a: 1 b: 2 c: 3

//findAll: Filter the entries in the Map that meet the criteria.
map = [a: 1, b: 2, c: 3]
filtered = map.findAll { key, value -> value > 1 }
println filtered //Output: [b: 2, c: 3]

//collect: Maps each entry in the Map to another value.
map = [a: 1, b: 2, c: 3]
collected = map.collect { key, value -> "$key=$value" }
println collected //Output: ["a = 1", "b = 2", "c = 3"]

//getOrDefault (Object key, Object defaultValue): Gets the value of the specified key, returns the default value if the key does not exist.
map = [a: 1, b: 2]
println map.getOrDefault('c', 0) //output: 0

//collectEntries (Closure closure): Convert the Map to another Map.
map = [a: 1, b: 2, c: 3]
newMap = map.collectEntries { key, value -> [(key): value * 2] }
println newMap //Output: [a: 2, b: 4, c: 6]

//find (Closure closure): Find the first entry in the Map that satisfies the criteria.
map = [a: 1, b: 2, c: 3]
entry = map.find { key, value -> value > 1 }
println entry //output: [b: 2] or [c: 3]

//keySet (): Get all keys in the Map.
map = [a: 1, b: 2, c: 3]
println map.keySet() //output: [a, b, c]

//values (): Get all values in the Map.
map = [a: 1, b: 2, c: 3]
println map.values() //Output: [1, 2, 3]

//flatten (): Flatten the nested Map.
map = [a: [b: 2, c: 3], d: 4]
println map.flatten() //Output: [a.b: 2, a.c: 3, d: 4]
```


<span id="656a140a"></span>
## List extension method

```Java
//unique (): Remove duplicate elements from the list.
list = [1, 2, 2, 3, 4, 4]
println list.unique() //Output: [1, 2, 3, 4]

//sort (): Sort the list.
list = [3, 1, 4, 1, 5, 9]
println list.sort() //Output: [1, 1, 3, 4, 5, 9]

//flatten (): flattens the nested list into a list.
list = [1, [2, 3], [4, [5, 6]]]
println list.flatten() //Output: [1, 2, 3, 4, 5, 6]

//count (Closure closure): Count the number of elements that satisfy the condition.
list = [1, 2, 3, 4, 5]
println list.count { it % 2 == 0 } //output: 2
```


<span id="50c7e61b"></span>
## Range extension method

```Java
//step (int step): Traverse the elements in the range with the specified step size.
range = 1..10
range.step(2).each { println it } //Output: 1 3 5 7 9

//containsWithinBounds (Object value): Checks if the value is in range (including bounds).
range = 1..10
println range.containsWithinBounds(10) //output: true

//subList (int fromIndex, int toIndex): Gets a sublist of the specified index range within the range.
range = 1..10
println range.subList(2, 5) //Output: [3, 4, 5]

//toList (): Converts the range to a list.
range = 1..5
println range.toList() //Output: [1, 2, 3, 4, 5]
```


<span id="6df85524"></span>
## Encryption method

```Java
//Base64 encoding and decoding
//Encoding
str = "hello world"
encoded = str.bytes.encodeBase64().toString()
println "Base64 Encoded: $encoded" //Output: Base64 Encoded: aGVsbG8gd29ybGQ =
//Decode
encoded = "aGVsbG8gd29ybGQ="
decoded = new String(encoded.decodeBase64())
println "Base64 Decoded: $decoded" //Output: Base64 Decoded: hello world
```


<span id="a1f61c13"></span>
## Summary method

```Java
// MD5
str = "hello world"
md5Hex = str.md5()
println "MD5: $md5Hex" //Output: MD5: 5eb63bbbe01eeed093cb22bb8f5acdc3

// SHA-1
str = "hello world"
sha1Hex = str.digest("SHA-1")
println "SHA-1: $sha1Hex" //Output: SHA-1: 2aae6c35c94fcfb415dbe95f408b9ce91ee846ed

// SHA-256
str = "hello world"
sha256Hex = str.digest("SHA-256")
println "SHA-256: $sha256Hex" //Output: SHA-256: b94d27b9934d3e08a52e52d7da7dabfac484eefc56bf5ef4b102e3d8fdedfb68
```
