---
title: "Rest API 2.0"
product: "DataAgent"
product_code: "dataagent"
source: "https://docs.byteplus.com/en/docs/dataagent/Rest_API_2_0"
---

We support accessing data through REST API. This article explains how to access REST API data.

<span id="1fe79847"></span>
# Conditions of use

Users need to have **Project Center \- Permissions \- By User Management \- Module \- Data Management \- New Connection** permissions.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/06cd3d16a74745d99273ddd5d04f9cca~tplv-goo7wpa0wc-image.image) </span>

<span id="66f9e2dc"></span>
# Operating instructions

<span id="cc4798e9"></span>
## New connection


1. In the console, select **Data Access \> Knowledge Access**, then click **Create**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14c3d4a96b2e491096bd6c1fb0db8e10~tplv-goo7wpa0wc-image.image) </span>

2. On the **Data Connection** screen select **API \- REST API**.

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/769e60a8ff094511b7fbedab7e4b7638~tplv-goo7wpa0wc-image.image) </span>


<span id="4a2f21bb"></span>
## Configuration basic information

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d7d20970da974c3eb1bd76472bc0a616~tplv-goo7wpa0wc-image.image) </span>


|parameter |explain |
|---|---|
|data connection name |Support for custom names, or use the system default name (for example: REST_API_2 0_ timestamp) |
|URL Address |In the "URL Address" box, fill in the full URL of the API you want to connect to |
|request method |Support GET and POST request methods |
|OAuth2 authentication |After opening, you need to fill in AK, SK, and authorization jump address authorization. |
|timeout |In the "Timeout" box, enter the maximum time (in milliseconds) that a request can wait without a response. The default is 3 minutes |
|number of retries |Configure the number of retries, that is, when the request fails, the number of times the system tries to retry, up to 5 times |


<span id="95467d66"></span>
## Set parameters

<span id="c857a9db"></span>
### Field path configuration rules

General: To operate on JSON, `$`represents the root node, `and the.`sign represents the sub\-node.

If the JSON data is:

```java
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
        "name": "阿联酋迪拉姆",//which means "UAE Dirham"
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
        "name": "澳大利亚元",// which means "Australian dollar"
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

```java
$.showapi_fee_num = 1
$.showapi_res_id = "6597a2f5fb638cf45b4d460c"
$.showapi_res_body.list.* = [{"time":"14:26:57","zhesuan":"193.69" ... // omitted later
```


<span id="5352850e"></span>
#### Result field path for dynamic parameters of the preceding operation

The configuration here is the path of the corresponding field configured when the result of the pre\-request is passed into the current request as a dynamic parameter. The rules are the same as above.

<span id="b2668a37"></span>
#### Current Request \- Parse Request and Path Configuration \- Field Path

The root path of the parsing result is configured here, and the rules are as follows:


* The root path **must be a Map or Array** , otherwise the key of the field cannot be resolved.

* If pointing to an Array, it must be written in a form that can resolve the key, such as ending with `. *`, such as `$.list. *`, and must not be written directly as `$.list`, so the key cannot be resolved.

* After the configuration is complete, clicking Get Fields will only resolve the first\-level field structure under the path, and these fields are all basic data types.


Example:

```java
//Take the whole result, the result in the fields include: showapi_res_error、showapi_res_id、...、showapi_res_body
$
//fetch the contents of the array
$.showapi_res_body.list.* = [{"time":"14:26:57","zhesuan":"193.69" ... // omitted later
```


<span id="4c4ae8cd"></span>
#### Current request \- field configuration \- parse path

The configuration here is the path of the final field obtained after the root path is resolved, and it is also the final field result of the data connection.

Here it is important to note that for the case where the root path is an array, if the field path prefix and the root path are inconsistent, the resulting result set will calculate the value corresponding to the field and add it directly to each element of the array.

For example, for weather data, the root path is $.forcast15days.list. \*, which represents the weather in the next 15 days. If the user adds a $.city field to represent the city, the value of $.city will eventually be calculated and added directly to each future weather data as a key called city. **The value of each item in the array is the same.** 

<span id="3b7d21e7"></span>
### Dynamic parameter writing rules

Both dynamic parameters and post\-script use Groovy as the scripting engine.

For ${} appearing in params, body, header, url, **as groovy's string interpolation expression, execute to get the result** . Also, some custom functions are built\-in, such as the md5 () method, date variables, and so on. Here are some examples of execution results:

```json
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


<span id="8978f2c9"></span>
### Postaction writing rules

Just put the following content in the rear operation as the default content

```java
def convertJson(response) {
    /*
    Fill in the post operation code here
    Response represents the result returned by the API, assuming that the API returns a result of
    {
        "city": "Shanghai",
        "forcast": [
            {"temperature": 5, "day": "2024-01-01"},
            {"temperature": 6, "day": "2024-01-02"},
        ],
        "test": "test"
    }
    Code examples：
    Scenario 1: Add, edit, loop, add city to each element in the list
    ls = response.forcast
    for (i=0; i< ls.size(); i++) {
        ls[i].city = response.city
    }
    Scenario 2: delete some key
    response.remove("test")
    */
    return response;
}
```


<span id="878df513"></span>
## Paging function rules

<span id="faae4d5c"></span>
### Basic configuration

After enabling the paging function, you can configure it as required, where the termination condition is a groovy expression. For example, you need to end paging when the data list in the request result is empty. You can configure it as follows:

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/14fd56c1a37440c88e7b5c5ca4d671ab~tplv-goo7wpa0wc-image.image) </span>

When used, it can be referenced by ${pageNum}. The variable will start from the start page until the termination condition is reached

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/fa98c589771b40798f566146d9179d14~tplv-goo7wpa0wc-image.image) </span>

<span id="b5156039"></span>
### Termination condition rule

Support for groovy syntax, no longer proceed to the next page when a termination condition is reached. The response represents the result of this request, some examples are as follows:

```json
response.data.size() == 0   // Stop paging when the length of the data list under the response is 0 (empty list)
response.hasMore == false // Stop paging when hasMore in response is false
```


<span id="33d573e8"></span>
## Parsing requests and path configuration

After completing the above configuration, click " **Send Request** ", the system will parse the request, the order of parsing is "Pre\-operation" \> "Current request" \> "Post\-operation", and the parsing result is presented in "Parse result".

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ecc95d25715647c982abb846427830ac~tplv-goo7wpa0wc-image.image) </span>


* **Field path** : Enter the field path, using $to represent the root node and the. sign to represent the sub\-node. Click the "Get Field" button, and the system will parse and display the "Field Configuration" area.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip"><strong>Tip: The</strong> path should point to Map or Array. If you want to parse the Array, you need to add. \* at the end of the path.</div>


**Two examples are provided as follows:**  $.map1 represents the data corresponding to the map1 field under the root node; $.array1. \* represents the data corresponding to the array1 field under the root node.


* **Field configuration** : Use the "Add" button to support new fields, and the parsing logic parses the results based on the rootPath entered by the user. Also, it supports deleting configured fields.

* **Data Preview** : Click the "Data Preview" button to view the first 100 rows of detailed data for the currently selected field.


<span id="209a4c0b"></span>
## Test connection and save

Click **Test Connection** to test the data source connectivity. After the test is successful, click **Save** to complete all configurations of the current data connection.

<span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/46ef8ef99084470481301ebd0e59e67a~tplv-goo7wpa0wc-image.image) </span>
