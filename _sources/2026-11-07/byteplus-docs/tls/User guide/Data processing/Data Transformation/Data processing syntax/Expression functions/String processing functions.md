---
title: "String processing functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/string_processing_functions"
---

This topic describes the syntax and format of string processing functions and offers sample scenarios.

<span id="str-join-函数"></span>
## str_join function

This function concatenates strings with a delimiter.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
str_join(separator,value1，value2...)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|separator |String |Yes |/ |/ |Specify a delimiter. The following values are supported: _ # \* \- |
|value |String |Yes |/ |/ |Specify values to be concatenated. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function concatenates employee names and companies as email addresses.

* Transformation rule:

   ```python
   f_set("join",str_join("@",v("name"),v("company")))
   ```
   

* Sample log:

   ```json
   {
       "name":"zhangsan",
       "company":"by.com"
   }
   ```
   

* Transformation result:

   ```json
   {
       "name":"zhangsan",
       "company":"by.com",
       "join":"zhangsan@by.com"
   }
   ```
   


<span id="str-len-函数"></span>
## str_len function

This function calculates string length.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
str_len(value)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |String |Yes |/ |/ |Specify a field value of which the length is to be calculated. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function gets the string length of the field `company`.

* Transformation rule:

   ```python
   f_set("len",str_len(v("company"))
   ```
   

* Sample log:

   ```json
   {
     "company": "by",
     "product": "tls"
   }
   ```
   

* Transformation result:

   ```json
   {
     "company": "by",
     "product": "tls",
     "len": 9
   }
   ```
   


<span id="str-replace-函数"></span>
## str_replace function

This function replaces a substring in a string multiple times.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
str_replace(value,old,new,count)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |String |Yes |/ |/ |Specify an original string. |
|old |String |Yes |/ |/ |Specify a substring to be replaced. |
|new |String |Yes |/ |/ |Specify a string used to replace the substring. |
|count |Number |No |/ |count\>0 |Specify the number of times that the string replaces the substring. If you do not set this parameter, the whole substring is replaced. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function replaces the pinyin shanghai with Chinese characters.

* Transformation rule:

   ```python
   f_set("replace",str_replace(v("region"),"shanghai","SH")
   ```
   

* Sample log:

   ```json
   {
     "region": "shanghai"
   }
   ```
   

* Transformation result:

   ```json
   {
     "region": "SH",
     "product": "tls"
    }
   ```
   


<span id="str-format-函数"></span>
## str_format function

This function formats strings.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
str_format(format,value1，value2...)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|separator |String |Yes |/ |/ |Specify a format used for your converted string. Replace the parameters with braces ( {} ). |
|value |String |Yes |/ |/ |Specify a value to be formatted. It is variable. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function gets a detailed address by concatenating the street, county, city, and province.

* Transformation rule:

   ```python
   f_set("address",str_format("Address: {}{}{}",v("province"),v("city"),v("town"),v("detail")))
   ```
   

* Sample log:

   ```json
   {
     "province": "Sichuan Province",
     "city": "Chengdu City",
     "town": "Wuhou District"
   }
   ```
   

* Transformation result:

   ```json
   {
     "province": "Sichuan Province",
     "city": "Chengdu City",
     "town": "Wuhou District",
     "address": "Address: 231 Wuhouci Street, Wuhou District, Chengdu City, Sichuan Province."
   }
   ```
