---
title: "JSON functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/JSON-functions"
---

This topic describes the syntax of JSON functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="915cff32"></span>
## List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>


* <div data-tips="true" data-tips-type="tip">If a string fails to be parsed into JSON data, NULL is returned.</div>


* <div data-tips="true" data-tips-type="tip">If JSON logs are truncated during collection, when you use a JSON function to analyze the JSON logs, the system reports an error and stops the analysis. To troubleshoot the error, specify a TRY expression in a query statement to capture the error. Then, the system continues the analysis. For example, use <code>* | SELECT message, TRY(JSON_PARSE(message))</code>.</div>




|Function |Function Syntax |Description |
|---|---|---|
|JSON_ARRAY_CONTAINS |JSON_ARRAY_CONTAINS(KEY, value) |This function verifies whether a JSON array contains a specific element. |
|JSON_ARRAY_GET |JSON_ARRAY_GET(KEY, index) |This function gets the JSON element corresponding to the specified index in a JSON array. |
|JSON_ARRAY_LENGTH |JSON_ARRAY_LENGTH(KEY) |This function calculates the length of a JSON array, that is, the number of JSON elements. |
|json_EXTRACT |json_EXTRACT(KEY, json_path) |This function extracts a set of JSON values from a JSON object or a JSON array. The JSON values can be of the array or object type. |
|JSON_EXTRACT_SCALAR |JSON_EXTRACT_SCALAR(json_string, json_path) |This function extracts a set of scalar values from a JSON string. The scalar values can be of the string, integer, or Boolean type. |
|JSON_FORMAT |JSON_FORMAT(KEY) |This function converts JSON data to a string. |
|JSON_PARSE |JSON_PARSE(KEY) |This function converts a JSON string to JSON data. |
|JSON_SIZE |JSON_SIZE(KEY, json_path) |This function calculates the number of elements in a JSON object or a JSON array. |


<span id="1ea274cf"></span>
## JSON_ARRAY_CONTAINS

The JSON_ARRAY_CONTAINS function verifies whether a JSON array contains a specific element.

<span id="f74008a6"></span>
### Function **syntax**


* Syntax format

   ```SQL
   JSON_ARRAY_CONTAINS(KEY, value)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is a JSON array string. |
   |value |The JSON element. |
   

* Return value description

   The return value is of the Boolean type.


<span id="bd17671e"></span>
### Example


* Scenario

   Verify whether the JSON array `[5, 10, 3]` contains 1.

* Query and analysis statement

   ```SQL
   * | SELECT JSON_ARRAY_CONTAINS('[5, 10, 3]', '1')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bcb0abfdd95647f097a5ef506779f6de~tplv-goo7wpa0wc-image.image) </span>


<span id="e738a379"></span>
## JSON_ARRAY_GET

The JSON_ARRAY_GET function gets the JSON element corresponding to the specified index in a JSON array.

<span id="f079b713"></span>
### Function **syntax**


* Syntax description

   ```SQL
   JSON_ARRAY_GET(KEY, index)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is a JSON array string. |
   |*index* |The JSON index. The index starts from 0. |
   

* Return value description

   The return value is of the Varchar type.


<span id="dd793b7d"></span>
### Example


* Scenario

   Return the element corresponding to the index that is set to 2 from the JSON array `["mon", [0, 8], "ten"]`.

* Query and analysis statement

   ```SQL
   * | SELECT JSON_ARRAY_GET('["mon", [0, 8], "ten"]', 2)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f440f554355145959fb8b8b2383a3676~tplv-goo7wpa0wc-image.image) </span>


<span id="6ad8e4b8"></span>
## JSON_ARRAY_LENGTH

The JSON_ARRAY_LENGTH function calculates the length of a JSON array, that is, the number of JSON elements.

<span id="f09f30dc"></span>
### Function **syntax**


* Syntax format

   ```SQL
   JSON_ARRAY_LENGTH(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is a JSON array string. |
   

* Return value description

   The return value is of the Bigint type.


<span id="4563ce3f"></span>
### Example


* Scenario

   Calculate the number of JSON elements among the values of the `json_test02` field.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/976f5a4b51aa4b3492dbdc967661cc7d~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT JSON_ARRAY_LENGTH(json_test02)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af9418f4126d4b708996f4ed9256a8a7~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="449871e5"></span>
## JSON_EXTRACT

The JSON_EXTRACT function extracts a set of JSON values from a JSON object or a JSON array. The JSON values can be of the array or object type.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If JSON data to be analyzed is invalid, the JSON_EXTRACT function reports an error. In this case, we recommend that you use the JSON_EXTRACT_SCALAR function.</div>


<span id="eebd42e4"></span>
### Function **syntax**


* Function format

   ```SQL
   JSON_EXTRACT(KEY, json_path)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |The value is a JSON object or a JSON array. |
   |json_path |The JSON path. Format: `$.store.book[0].title`. |
   

* Return value description

   The return value is of the String type.


<span id="de0a411b"></span>
### Example


* Scenario

   Get the value of the SIZE field from the JSON string `'[{"SIZE":100},{"STATUS":200}]'`.

* Query and analysis statement

   ```SQL
   * | SELECT JSON_EXTRACT('[{"SIZE":100},{"STATUS":200}]', '$.0.SIZE')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/9fa77c1501a544cc948fc08be2f26af1~tplv-goo7wpa0wc-image.image) </span>


<span id="e6899cf6"></span>
## JSON_EXTRACT_SCALAR

The JSON_EXTRACT_SCALAR function extracts a set of scalar values from a JSON string. The scalar values can be of the string, integer, or Boolean type.

<span id="fbfa73a6"></span>
### Function **syntax**


* Syntax format

   ```SQL
   JSON_EXTRACT_SCALAR(json_string, json_path)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |json_string |The value is a JSON object or a JSON array string. |
   |*json_path* |The JSON path. Format: `$.store.book[0].title`. |
   

* Return value description

   The return value is of the Varchar type.


<span id="7dc70993"></span>
### Example


* Scenario

   Get the value of the `STATUS` field from the JSON string `[{"SIZE":100},{"STATUS":200}]`.

* Query and analysis statement

   ```SQL
   *|SELECT JSON_EXTRACT_SCALAR('[{"SIZE":100},{"STATUS":200}]','$.1.STATUS')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/ca1f1cfce98942f7bb76f787aff157d1~tplv-goo7wpa0wc-image.image) </span>


<span id="2ea3d7c3"></span>
## JSON_FORMAT

The JSON_FORMAT function converts JSON data to a string.

<span id="7336917c"></span>
### Function **syntax**


* Syntax format

   ```SQL
   JSON_FORMAT(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |The value is of the JSON type. |
   

* Return value description

   The return value is of the Varchar type.


<span id="0b72d288"></span>
### Example


* Scenario

   Convert the JSON array `[100,200,300]` to the string `[100, 200, 300]`.

* Query and analysis statement

   ```SQL
   * | SELECT JSON_FORMAT(JSON_PARSE('[100, 200, 300]'))
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/18e2c4aadf954d9398c1061300a28352~tplv-goo7wpa0wc-image.image) </span>


<span id="d8ef35a6"></span>
## JSON_PARSE

The JSON_PARSE function converts a JSON string to JSON data. In most cases, the JSON_PARSE function is of limited use. To extract values from JSON data, we recommend that you use the JSON_EXTRACT_SCALAR function.

<span id="e9ead95e"></span>
### Function **syntax**


* Syntax format

   ```SQL
   JSON_PARSE(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |The value is a JSON string. |
   

* Return value description

   The return value is of the JSON type.


<span id="18fdb01f"></span>
### Example


* Scenario

   Get the subfields from the JSON string `{"SIZE":100,"STATUS":200}`.

* Query and analysis statement

   ```SQL
   *| SELECT MAP_KEYS(TRY_CAST(JSON_PARSE('{"SIZE":100,"STATUS":200}') AS MAP(varchar, json)))
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/7720cea2e63349528c46e1ed39bafb8d~tplv-goo7wpa0wc-image.image) </span>


<span id="39ed6221"></span>
## JSON_SIZE

The JSON_SIZE function calculates the number of elements in a JSON object or a JSON array.

<span id="bab078a2"></span>
### Function **syntax**


* Syntax format

   ```SQL
   JSON_SIZE(KEY, json_path)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |The value is a JSON object or a JSON array string. |
   |*json_path* |The JSON path. Format: `$.store.book[0].title`. |
   

* Return value description

   The return value is of the Bigint type.


<span id="8941e788"></span>
### Example


* Scenario

   Return the number of path elements in the JSON\-formatted string `[{"SIZE":100,"STATUS":200,"LEN":1}]`.

* Query and analysis statement

   ```SQL
   * | SELECT JSON_SIZE('[{"SIZE":100,"STATUS":200,"LEN":1}]', '$.0.LEN')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b2282b7960b24bb3b8e5b4e629fa38a2~tplv-goo7wpa0wc-image.image) </span>
