---
title: "URL functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/URL-functions-2"
---

This topic describes the syntax of URL functions supported by Torch Log Service (TLS) and offers examples on how to use the functions.

<span id="26955706"></span>
## List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



|Function |Function Syntax |Description |
|---|---|---|
|URL_ENCODE |URL_ENCODE(KEY) |Encodes a URL. |
|URL_DECODE |URL_DECODE(KEY) |Decodes a URL. |
|URL_EXTRACT_FRAGMENT |URL_EXTRACT_FRAGMENT(KEY) |Extracts the fragment from a URL. |
|URL_EXTRACT_HOST |URL_EXTRACT_HOST(KEY) |Extracts the host from a URL. |
|URL_EXTRACT_PARAMETER |URL_EXTRACT_PARAMETER(KEY, parameter name) |Extracts the value of a specified parameter in the query string from a URL. |
|URL_EXTRACT_PATH |URL_EXTRACT_PATH(KEY) |Extracts the path from a URL. |
|URL_EXTRACT_PORT |URL_EXTRACT_PORT(KEY) |Extracts the port number from a URL. |
|URL_EXTRACT_PROTOCOL |URL_EXTRACT_PROTOCOL(KEY) |Extracts the protocol from a URL. |
|URL_EXTRACT_QUERY |URL_EXTRACT_QUERY(KEY) |Extracts the query string from a URL. |


<span id="URL_ENCODE"></span>
## URL_ENCODE

The URL_ENCODE function encodes a URL.

<span id="9e68b8ed"></span>
### Function **syntax**


* Syntax format

   ```SQL
   URL_ENCODE(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is a URL. |
   

* Return value description

   The return value is of the Varchar type.


<span id="906ccb99"></span>
### Example


* Scenario

   Encode the value of the `test_url_text` field.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f892c64b39384eccbfdd58e0863295d8~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT URL_ENCODE(test_url_text)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/bf2c3a9ae54a41468eff0bb1f69bd8d2~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="35d5ab88"></span>
## URL_DECODE

The URL_DECODE function decodes a URL.

<span id="d9b9ceab"></span>
### Function **syntax**


* Syntax format

   ```SQL
   URL_DECODE(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is an encoded URL. |
   

* Return value description

   The return value is of the Varchar type.


<span id="f07245ed"></span>
### Example


* Scenario

   Decode the value of the `test_url_text` field.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4fcf67b59aae4c85a9ae36d675eb86a3~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT URL_DECODE(test_url_text)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8ab058d167bc4db7b46ec661c204e4a0~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="b840d74e"></span>
## URL_EXTRACT_FRAGMENT

The URL_EXTRACT_FRAGMENT function is used to extract the fragment part from a URL.

<span id="73778e44"></span>
### Function **syntax**


* Syntax format

   ```SQL
   URL_EXTRACT_FRAGMENT(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is a URL. |
   

* Return value description

   The return value is of the Varchar type.


<span id="8026ad77"></span>
### Example


* Scenario

   Extract the fragment part of a URL from the `test_url_text` field.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3cd44fcca94e43d2b02e20ce33e22382~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT URL_EXTRACT_FRAGMENT(test_url_text) 
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0a3d6858633b4a8586fc2d4d1a22ec2f~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="ce040c04"></span>
## URL_EXTRACT_HOST

The URL_EXTRACT_HOST function extracts the host from a URL.

<span id="5806e64e"></span>
### Function **syntax**


* Syntax format

   ```SQL
   URL_EXTRACT_HOST(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is a URL. |
   

* Return value description

   The return value is of the Varchar type.


<span id="b4eb8e29"></span>
### Example


* Scenario

   Extract the host from the value of the `test_url_text` field.

* Sample log

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/91b2c1e4ee15480daef64c80925eaf98~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   

* Query and analysis statement

   ```SQL
   * | SELECT URL_EXTRACT_HOST(test_url_text)
   ```
   

* Query and analysis results

   <div style="text-align: center">
   <img src="https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a366c7f614df44e397f638809294ecf6~tplv-goo7wpa0wc-image.image" width="1282px" />   </div>
   


<span id="02be2019"></span>
## URL_EXTRACT_PARAMETER

The URL_EXTRACT_PARAMETER function extracts the value of a specified parameter in the query string from a URL.

<span id="7d007b1c"></span>
### Function **syntax**


* Syntax format

   ```SQL
   URL_EXTRACT_PARAMETER(KEY, parameter)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is a URL. |
   |parameter |The parameter name in the query string of the URL. |
   

* Return value description

   The return value is of the Varchar type.


<span id="0a31f1d5"></span>
### Example


* Scenario

   Extract the value of the `region` parameter from the value of the `url` field.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/3ad4a7f592b043f094df05f8abf5d628~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT URL_EXTRACT_PARAMETER(url,'region') AS region
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/64d33306c8104f2d9c75b2f7610b4226~tplv-goo7wpa0wc-image.image) </span>


<span id="30d1fd0e"></span>
## URL_EXTRACT_PATH

The URL_EXTRACT_PATH function extracts the path from a URL.

<span id="4fb63dce"></span>
### Function **syntax**


* Syntax format

   ```SQL
   URL_EXTRACT_PATH(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is a URL. |
   

* Return value description

   The return value is of the Varchar type.


<span id="735043a3"></span>
### Example


* Scenario

   Extract the path from the value of the `url` field.

* Sample log

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f76d79a8211c4585a6a5e35b2e90764a~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT URL_EXTRACT_PATH(url) AS path
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/73bd71f203a2480ca50df9bd8e82e94c~tplv-goo7wpa0wc-image.image) </span>


<span id="161d3fc9"></span>
## URL_EXTRACT_PORT

The URL_EXTRACT_PORT function extracts the port number from a URL.

<span id="27acaef3"></span>
### Function **syntax**


* Syntax format

   ```SQL
   URL_EXTRACT_PORT(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is a URL. |
   

* Return value description

   The return value is of the Varchar type.


<span id="7b777604"></span>
### Example


* Scenario

   Extract the port number from the value of the `url` field.

* Sample log

   ```SQL
   url:http://localhost:8080
   ```
   

* Query and analysis statement

   ```SQL
   * | SELECT URL_EXTRACT_PORT(url) AS port
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/af5798ba39654b599ea74384ad875161~tplv-goo7wpa0wc-image.image) </span>


<span id="6d9d7f56"></span>
## URL_EXTRACT_PROTOCOL

The URL_EXTRACT_PROTOCOL function extracts the protocol from a URL.

<span id="ed2ef990"></span>
### Function **syntax**


* Syntax format

   ```SQL
   URL_EXTRACT_PROTOCOL(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is a URL. |
   

* Return value description

   The return value is of the Varchar type.


<span id="c7661346"></span>
### Example


* Scenario

   Extract the protocol from the value of the `url` field.

* Sample log

   ```SQL
   url:http://localhost:8080
   ```
   

* Query and analysis statement

   ```SQL
   * | SELECT URL_EXTRACT_PROTOCOL(url) AS protocol
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/86770bab0aa946f7a3bac14f2877952a~tplv-goo7wpa0wc-image.image) </span>


<span id="0d654ea3"></span>
## URL_EXTRACT_QUERY

The URL_EXTRACT_QUERY function extracts the complete query string from a URL.

<span id="9e07911e"></span>
### Function **syntax**


* Syntax format

   ```SQL
   URL_EXTRACT_QUERY(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. The value is a URL. |
   

* Return value description

   The return value is of the Varchar type.


<span id="de5a3838"></span>
### Example


* Scenario

   Extract the query string from the value of the `url` field.

* Sample log

   ```SQL
   url:http://localhost:8080/query?name=regan
   ```
   

* Query and analysis statement

   ```SQL
   * | SELECT URL_EXTRACT_QUERY(url) AS query
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/a2a98ca14d6d4046af3edd2960c1cdd5~tplv-goo7wpa0wc-image.image) </span>
