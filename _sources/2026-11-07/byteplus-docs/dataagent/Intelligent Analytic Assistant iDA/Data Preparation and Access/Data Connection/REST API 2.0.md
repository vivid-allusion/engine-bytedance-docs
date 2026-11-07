---
title: "REST API 2.0"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/REST_API_2_0__"
---

<span id="_1-概述"></span>
# 1. Overview

API is one of the most common solutions for data transmission and interaction between systems. How can external API data be integrated into this product for analysis? This article will describe how to integrate API data connections and use these connections to create datasets.

Before connecting data, please collect the following information:


* The IP address and port number of the server where the database is located;

* The name of the database;

* The username and password of the database.


<span id="_2-快速入门"></span>
# 2. Quick start

<span id="_2-1-从数据连接新建"></span>
## 2.1 Method 1: Create from data connection

Step 1: Enter BytePlus, click to access a specific project, click Data Preparation, find Data Connection in the dropdown list, and click Data Connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b9656a5ed4ef44509dc16dd9163db39c~tplv-goo7wpa0wc-image.image) </span>

Step 2: On the page, select **REST API 2.0**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7458601594b451481bbf8721aa9c416~tplv-goo7wpa0wc-image.image) </span>

<span id="_2-2-从数据集新建"></span>
## 2.2 Method 2: Create from dataset

Step 1: Enter BytePlus, click Data Preparation \-\-\> Dataset, select the "Create" button in the upper left corner to create a new dataset.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/43257374401d4f3ca3ebe01264cef891~tplv-goo7wpa0wc-image.image) </span>

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d809056a035b431d8ca2f4c530554168~tplv-goo7wpa0wc-image.image) </span>

Step 2: When adding a data connection, click Others.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/42d93a64f39d40b48142f1a062b24d40~tplv-goo7wpa0wc-image.image" width="573px" /></div>


Step 3: On the page, select **REST API 2.0**

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/c7458601594b451481bbf8721aa9c416~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-配置说明"></span>
# 3. Configuration instructions

<span id="_3-1-配置基本信息"></span>
## 3.1 Configure basic information

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/50ff8046de694a138526ddaf2af24c29~tplv-goo7wpa0wc-image.image) </span>

First, please complete the following configurations:

 **(1) Data connection name**: Custom names are supported, or use the system default name (for example: REST_API_2.0_timestamp).

 **(2) URL address**: The complete URL of the API to be connected.

 **(3) Request method**: Supports GET and POST request methods.

 **(4) Timeout**: Enter the maximum time to wait for a response when there is no reply (unit: milliseconds). The default is 3 minutes.

 **(5) Retry count**: The number of times the system will attempt to retry when a request fails, up to 5 times.

<span id="_3-2-配置参数"></span>
## 3.2 Configure parameters

Please complete the following parameter settings:

 **(1) Request headers**: Supports configuring key and value, as well as add and delete operations. Up to 10 groups can be configured.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/dc7bd99df76641f7b8c5724889a3c26f~tplv-goo7wpa0wc-image.image) </span>

 **(2) Request parameters**: Enter all query parameters required by the API.

 **(3) Request body**: Select the request body type (form\-data or raw). Both support user input of a JSON\-formatted request body.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4bd7669b77624999b91a7f2b745c3068~tplv-goo7wpa0wc-image.image) </span>

General rule: When operating on JSON, `$` represents the root node, and `.` denotes accessing a child node.

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
$.showapi_res_body.list.* = [{"time":"14:26:57","zhesuan":"193.69" ... // 后面省略
```


 **(4) Pre\-processing operations:** 

You can use this configuration to perform additional steps to prepare data or obtain necessary information before the main request

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a61b3d13aeef45769582de9afe9af341~tplv-goo7wpa0wc-image.image) </span>


* **Add a pre\-processing operation**: Click the "Add Pre\-processing Operation" button. On the configuration page, you need to enter detailed information for the pre\-processing operation, including the URL, request method, and more.


<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3bb42534cbab415a86759d782797e4c0~tplv-goo7wpa0wc-image.image) </span>


* **Parsing request and path configuration**: After clicking "Initiate Request", the system will parse this pre\-processing request and display the parsing result in the "Request Result" area. The user needs to configure the key for dynamic parameters and the result field path, so that the pre\-processing request result can be used in the current request.

* **Caution:**  You can set up to 5 pre\-processing operations.


 **(5) Post\-processing operation:** 

This provides a more flexible and powerful way to configure custom parameters, supports **Groovy syntax**, and allows users to write code to implement multi\-level request parsing.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d81f87f1ed48480ea41c4cc1a5b4f9f2~tplv-goo7wpa0wc-image.image) </span>

<span id="_3-3-解析请求与路径配置"></span>
## 3.3 Parsing request and path configuration

First, after completing the above configuration steps, you can click "**Send Request**" and the system will parse the request.

The parsing order is "Pre\-processing Operation" \> "Current Request" \> "Post\-processing Operation", and the "Parsing Result" will be displayed.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2211077169b9420a9d60d02b631e9b6c~tplv-goo7wpa0wc-image.image) </span>

Next, after the system completes parsing the request, you also need to perform the following configurations for the path:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/57a791163a14410581382d79febbb485~tplv-goo7wpa0wc-image.image) </span>

 **(1) Field path**: Enter the field path, using $ to represent the root node and a period (.) to represent child nodes. Click the "Get Fields" button, and the system will parse and display the "Field Configuration" area.

This configures the root path of the parsing result, with the following rules:


* The root path **must point to a Map or Array**; otherwise, the key of the field cannot be parsed.

* If it points to an Array, it must be written in a form that can parse out the key, such as ending with `.*`, for example, `$.list.*`. It must not be written directly as `$.list`, as this cannot parse out the key.

* After configuration is complete, clicking Get Fields will only parse the first\-level field structure under this path, and these fields are all basic data types.


Example:

```Java
// Retrieve the entire result. The result includes fields such as: showapi_res_error, showapi_res_id, ..., showapi_res_body
$
// Retrieve contents from the array
$.showapi_res_body.list.* = [{"time":"14:26:57","zhesuan":"193.69" ... // Omitted below
```


 **(2) Field configuration**: Use the "Add" button to create new fields. The parsing logic is based on the rootPath you enter and generates results accordingly. It also supports deleting configured fields.

This configuration specifies the path of the final field obtained after parsing the root path, which is also the final field result for this data connection.

**Caution**: For cases where the root path is an array, if the field path prefix does not match the root path, the value corresponding to the field will be calculated and directly added to each element of the array in the final result set.

For example, for weather data, the root path is $.forecast15days.list.\*, which represents the weather for the next 15 days. If the user adds a $.city field to represent the city, the value of $.city will be calculated and directly added to each future weather data entry as a key named city. **The value is the same for every item in the array.** 

 **(3) Data preview**: Click the "Data Preview" button to view the first 100 rows of detailed data for the currently selected field.

<span id="d9fc967c"></span>
## 3.4 Dynamic parameter scripting rules

Dynamic parameters and post\-processing scripts both use Groovy as the script engine.

For ${} appearing in params, body, header, or url, **it is executed as a Groovy string interpolation expression to obtain the result**. Some custom functions are also built in, such as the md5() method and date variables. The following are some examples of execution results:

```JSON
If there are currently two parameters configured in the pre request, as follows:
num1 = 1
num2 = 2

The content inside ${} will be executed as an expression, while the rest will be a regular string. The following expression results are:
abc               // abc
${num1}           // 1
${num1+num2}      // 3
${num1}+num2      // 1+num2
${num3}           // Error: parameter num3 does not exist
${"${num1}"}      // ${num1}
```


<span id="22b251d7"></span>
## 3.5 Post\-processing scripting rules

Place the following content in the post\-processing operation as the default content:

```Java
def convertJson(response) {
    /*Write post-processing operation code here.response represents the result returned by the API. Suppose the API returns the following result:    {"city": "Shanghai",        "forcast": [            {"temperature": 5, "day": "2024-01-01"},            {"temperature": 6, "day": "2024-01-02"},        ],        "test": "test"    }Some code examples:Scenario 1: Add, edit, and loop, adding the city to each element in the list.    ls = response.forcast    for (i=0; i< ls.size(); i++) {        ls[i].city = response.city    }Scenario 2: Remove a specific key    response.remove("test")    */
    return response;
}
```


<span id="fbadb431"></span>
## 3.6 Pagination rules

<span id="00cff6c3"></span>
### 3.6.1 Basic configuration

After enabling the pagination feature, configure as required. The termination condition is a Groovy expression. For example, to end pagination when the data list in the request result is empty, the maximum pagination indicates the upper limit of request times (default is 10, maximum is 10,000). Configuration can be done as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fa85f22319e4d04ba55fd091e1f09ec~tplv-goo7wpa0wc-image.image) </span>

When in use, reference ${pageNum}. This variable starts from the initial page and continues until the termination condition is met.

<div style="text-align: center">
<img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/635a683e049f45e2a25137d7ae38579f~tplv-goo7wpa0wc-image.image" width="1826px" /></div>


<span id="929b6368"></span>
### 3.6.2 Termination condition rules

Supports Groovy syntax. When the termination condition is met, pagination will not proceed to the next page. response represents the result of this request. Some examples are as follows:

```JSON
response.data.size() == 0   // Stop pagination when the length of the data list under response is 0 (empty list)
response.hasMore == false // Stop pagination when hasMore under response is false
```


<span id="_3-4-测试连接与保存"></span>
# 4. Test connection and save

Finally, click **Test Connection** to perform a connectivity test for the data source. After the test is successful, click **Save** to complete all configurations for the current data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5ddcf18f438043c6ae8d740fcc4c3199~tplv-goo7wpa0wc-image.image) </span>

<span id="41e9f771"></span>
# 5. Built\-in system variables

The following dynamic parameters are already built into the system. When naming variables, do not use the same names as system variables, otherwise they will be overwritten by system variables.

> Scope of effect: url, header, params, body. Not effective in post\-processing operations.


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

//以上变量支持日期加减，例如 ${date-1}，代表前一天
```


<span id="2ece23af"></span>
# 6. Built\-in system functions

> Scope of effect: url, header, params, body, post\-processing operations.


<span id="2381ea50"></span>
## 6.1 Digest functions

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


<span id="0f7d94f9"></span>
## 6.2 Mathematical functions

```Java
java.lang.Math 相关的所有函数
```


<span id="ccd87f70"></span>
## 6.3 Retrieve date and time, formatting, date addition and subtraction

```Groovy
// format: Format date as string.
currentDate = new Date()
formattedDate = currentDate.format('yyyy-MM-dd HH:mm:ss')

// plus and minus: Date addition and subtraction operations.
tomorrow = currentDate + 1 
yesterday = currentDate - 1 
```


<span id="5d3bd9ae"></span>
## 6.4 String extension methods

```Java
// capitalize(): Capitalize the first character of the string.
str = "groovy"
str.capitalize() // Output: "Groovy"

// reverse(): Reverse the string.
str.reverse()     // Output: "yvoorg"

// contains(): Check whether the string contains the specified substring.
str.contains("oo") // Output: true

// toInteger(), toLong(), toFloat(), toDouble(): Convert the string to the corresponding numeric type.
str = "123"
str.toInteger() // Output: 123

// split(): Split the string.
str = "a,b,c"
str.split(",") // Output: ["a", "b", "c"]

// isNumber(): Check whether the string is a number.
str.isNumber() // Output: true
```


<span id="b46be758"></span>
## 6.5 Collection extension methods

```Java
// each: Execute a closure for each element in the collection.
list = [1, 2, 3]
list.each { println it } // Output: 1 2 3

// findAll: Filter elements in the collection that meet the condition.
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

// join: Join the elements in the collection into a string using the specified separator.
list = ["a", "b", "c"]
println list.join("-") // Output: "a-b-c"
```


<span id="f6769512"></span>
## 6.6 Map extension methods

```Java
// each: Execute a closure operation on each entry in the Map.
map = [a: 1, b: 2, c: 3]
map.each { key, value -> println "$key: $value" } // Output: a: 1 b: 2 c: 3

// findAll: Filter the entries in the Map that meet the condition.
map = [a: 1, b: 2, c: 3]
filtered = map.findAll { key, value -> value > 1 }
println filtered // Output: [b: 2, c: 3]

// collect: Map each entry in the Map to another value.
map = [a: 1, b: 2, c: 3]
collected = map.collect { key, value -> "$key=$value" }
println collected // Output: ["a=1", "b=2", "c=3"]

// getOrDefault(Object key, Object defaultValue): Get the value for the specified key, or return the default value if the key does not exist.
map = [a: 1, b: 2]
println map.getOrDefault('c', 0) // Output: 0

// collectEntries(Closure closure): Convert the Map to another Map.
map = [a: 1, b: 2, c: 3]
newMap = map.collectEntries { key, value -> [(key): value * 2] }
println newMap // Output: [a: 2, b: 4, c: 6]

// find(Closure closure): Find the first entry in the Map that meets the condition.
map = [a: 1, b: 2, c: 3]
entry = map.find { key, value -> value > 1 }
println entry // Output: [b:2] or [c:3]

// keySet(): Get all keys in the Map.
map = [a: 1, b: 2, c: 3]
println map.keySet() // Output: [a, b, c]

// values(): Get all values in the Map.
map = [a: 1, b: 2, c: 3]
println map.values() // Output: [1, 2, 3]

// flatten(): Flatten a nested Map.
map = [a: [b: 2, c: 3], d: 4]
println map.flatten() // Output: [a.b:2, a.c:3, d:4]
```


<span id="a4f8fdee"></span>
## 6.7 List extension methods

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

// count(Closure closure): Count the number of elements that meet the condition.
list = [1, 2, 3, 4, 5]
println list.count { it % 2 == 0 } // Output: 2
```


<span id="fe4b8474"></span>
## 6.8 Range extension methods

```Java
// step(int step): Iterate over the elements in the range with the specified step size.
range = 1..10
range.step(2).each { println it } // Output: 1 3 5 7 9

// containsWithinBounds(Object value): Check whether the value is within the range (including the boundaries).
range = 1..10
println range.containsWithinBounds(10) // Output: true

// subList(int fromIndex, int toIndex): Get the sublist within the specified index range.
range = 1..10
println range.subList(2, 5) // Output: [3, 4, 5]

// toList(): Convert the range to a list.
range = 1..5
println range.toList() // Output: [1, 2, 3, 4, 5]
```


<span id="d05a352d"></span>
## 6.9 Encryption methods

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


<span id="14a96f12"></span>
## 6.10 Digest methods

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
