---
title: "Encoding and decoding functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/encoding_and_decoding_functions"
---

This topic describes the syntax and format of encoding and decoding functions and offers sample scenarios.

<span id=".bWQ1LWVuY29kaW5nLeWHveaVsA=="></span>
## md5_encoding function

This function encodes a specified field in MD5. This means the function calculates the MD5 value of the string.

<span id=".5Ye95pWw6K-t5rOVLeagvOW8jw=="></span>
### Function syntax and format

```python
md5_encoding(value)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |String |Yes |/ |/ |Specify a string to be encoded in MD5. |


<span id=".5Ye95pWw56S65L6L"></span>
### Sample function

The function calculates the MD5 value of the log field `content`.


* Transformation rule:

   ```python
   f_set("md5_value",md5_encoding(v("content")))
   ```
   

* Sample log:

   ```json
   {
       "content":"str"
   }
   ```
   

* Transformation result:

   ```json
   {
       "content":"str",
       "md5_value":"341be97d9aff90c9978347f66f94****"
   }
   ```
   


<span id=".YmFzZTY0LWVuY29kaW5nLeWHveaVsA=="></span>
## base64_encoding function

This function encodes specified data in Base64. This means the function calculates the Base64 value of the string.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only an RFC 4648 encoding format is supported.</div>


<span id=".5Ye95pWw6K-t5rOVLeagvOW8jw=="></span>
### Function syntax and format

```python
base64_encoding(value)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |String |Yes |/ |/ |Specify a value to be encoded in Base64. |


<span id=".5Ye95pWw56S65L6L"></span>
### Sample function

The function calculates the Base64 value of the log field `content`.


* Transformation rule:

   ```python
   f_set("base64_value",base64_encoding(v("content")))
   ```
   

* Sample log:

   ```json
   {
       "content":"341be97d9aff90c9978347f66f94****"
   }
   ```
   

* Transformation result:

   ```json
   {
       "content":"341be97d9aff90c9978347f66f94****",
       "base64_value":"MzQxYmU5N2Q5YWZmOTBjOTk3ODM0N2Y2NmY5NDVi****"
   }
   ```
   


<span id=".YmFzZTY0LWRlY29kaW5nLeWHveaVsA=="></span>
## base64_decoding function

This function decodes data in Base64.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Only an RFC 4648 encoding format is supported.</div>


<span id=".5Ye95pWw6K-t5rOVLeagvOW8jw=="></span>
### Function syntax and format

```python
base64_decoding(value)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |String |Yes |/ |/ |Specify a value to be decoded in Base64. |


<span id=".5Ye95pWw56S65L6L"></span>
### Sample function

Decode the log field `content` in Base64.


* Transformation rule:

   ```python
   f_set("base64_decode_value",base64_decoding(v("content")))
   ```
   

* Sample log:

   ```json
   {
      "content":"MzQxYmU5N2Q5YWZmOTBjOTk3ODM0N2Y2NmY5NDVi****"
   }
   ```
   

* Transformation result:

   ```json
   {
       "content":"MzQxYmU5N2Q5YWZmOTBjOTk3ODM0N2Y2NmY5NDVi****",
       "base64_decode_value":"341be97d9aff90c9978347f66f94****"
   }
   ```
   


<span id="c0dfa1c9"></span>
## str_encoding function

This function encodes a string according to a specified encoding format.

<span id="41352c64"></span>
### Function syntax and format

```Python
str_encode(value, encoding="utf8")
```


The following table describes the parameters.


|Parameter |Type |Required |Description |
|---|---|---|---|
|value |String |Yes |Specify a string to be encoded. |
|encoding |String |No |Specify an encoding format. Default value: utf8. Valid values:<br><br><br>* utf8<br><br>* ASCII<br><br>* latin1<br><br>* unicode\-escape |


<span id="7d95642b"></span>
### Sample function

The function encodes a specified string in UTF\-8.


* Transformation rule:

   ```Python
   f_set("f_encode",str_decode(str_encode("BytePlus", "utf8"), "utf8"))
   ```
   

* Log:

   ```JSON
   {
       "key": "value"
   }
   ```
   

* Transformation result:

   ```JSON
   {
       "key": "value",
       "f_encode": "BytePlus"
   }
   ```
   


<span id="bef90463"></span>
## str_decoding function

This function decodes a string in a specified format.

<span id="d8abf80b"></span>
### Function syntax and format

<span id="YEuSZFW0"></span>
### ```Python
str_decode(value, encoding="utf8")
```


The following table describes the parameters.


|Parameter |Type |Required |Description |
|---|---|---|---|
|value |String |Yes |Specify a string to be decoded. |
|encoding |String |No |Specify the decoding format. Default value: utf8. Valid values:<br><br><br>* utf8<br><br>* ASCII<br><br>* latin1<br><br>* unicode\-escape |


<span id="4365fa57"></span>
### Sample function

The function decodes a specified string in UTF\-8.


* Transformation rule:

   ```Python
   f_set("f_decode",str_decode(str_encode(v("key"))))
   ```
   

* Log:

   ```JSON
   {
       "key": "test data"
   }
   ```
   

* Transformation result:

   ```JSON
   {
       "key": "test data",
       "f_decode": "test data"
   }
   ```
