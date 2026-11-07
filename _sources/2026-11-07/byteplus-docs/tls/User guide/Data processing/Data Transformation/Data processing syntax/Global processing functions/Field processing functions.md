---
title: "Field processing functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/field_processing_functions"
---

This topic describes the syntax and format of field processing functions and offers sample scenarios.

<span id="v-函数"></span>
## v function

This function extracts the value of a specified field name in a log. You can pass multiple fields as a parameter, and the function returns the first existing field. If all fields in the parameter do not exist, the value specified for default is returned.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
v(field, ..., default=None)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|field |String |Yes |/ |/ |Specify the field name of a value to be extracted. |
|defalut |Any |No |None |/ |Specify the value that is returned when all specified fields do not exist. |


<span id="函数示例"></span>
### Sample function


* Scenario: This function extracts multiple fields from a log and sets the values of the first extracted fields to a new field.

* Transformation rule:

   ```python
   f_set("first_value", v("content-1", "content-2", default="hello world"))
   ```
   

* Sample log:

   ```json
   [
       {
           "content-1":"hello"
       },
       {
           "content-2":"world"
       },
       {
           "content":"test content"
       }
   ]
   ```
   

* Transformation result:

   ```json
   [
       {
           "content-1":"hello",
           "first_value":"hello"
       },
       {
           "content-2":"world",
           "first_value":"world"
       },
       {
           "content":"test content",
           "first_value":"hello world"
       }
   ]
   ```
   


<span id="f-drop-函数"></span>
## f_drop function

This function deletes fields with specified field names in the log. Specify at least one field.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
f_drop(field, ....)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|field |String |Yes |/ |/ |Specify the names of the fields to be deleted. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function deletes the `content` field in a log.

* Transformation rule:

   ```python
   f_drop("content")
   ```
   

* Sample log:

   ```json
   {
       "content":"test value",
       "name":"Paul",
       "city":"chengdu"
   }
   ```
   

* Transformation result:

   ```json
   {
       "name":"Paul",
       "city":"chengdu"
   }
   ```
   


<span id="f-keep-函数"></span>
## f_keep function

This function retains the fields with specified field names and deletes the other fields in a log. Specify at least one field.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
f_keep(field, ....)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|field |String |Yes |/ |/ |Specify the names of the fields to be retained. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function retains the`name` and `city` fields in a log, and deletes the other fields.

* Transformation rule:

   ```python
   f_keep("name", "city")
   ```
   

* Sample log:

   ```json
   {
       "name":"Paul",
       "age":"20",
       "city":"chengdu",
       "content":"hello world"
   }
   ```
   

* Transformation result:

   ```json
   {
       "name":"Paul",
       "city":"chengdu"
   }
   ```
   


<span id="f-rename-函数"></span>
## f_rename function

This function renames a specified field. Make sure key and newkey appear in pair.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
f_rename(key1, newkey1, key2, newkey2, ...)
```


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">For this function, make sure <strong>key</strong> and <strong>newkey</strong> appear in pair and specify at least one pair.</div>


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|key |string |Yes |/ |/ |Specify a log field name. The value can be a regular expression. When a field name fully meets the condition, the field is renamed. |
|newkey |string |Yes |/ |/ |Specify a new field name. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function renames the `content` field in a log to `new-content`.

* Transformation rule:

   ```python
   f_rename("content", "new-content")
   ```
   

* Sample log:

   ```json
   {
       "content":"hello world",
       "city":"hangzhou"
   }
   ```
   

* Transformation result:

   ```json
   {
       "new-content":"hello world",
       "city":"hangzhou"
   }
   ```
   


<span id="f-set-函数"></span>
## f_set function

This function adds a field or sets a value for an existing field. You can set multiple fields at the same time. Make sure field names and field values appear in pair.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
f_set(key1, value1, key2, value2, mode="overwrite")
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|key |String |Yes |/ |/ |Specify a field name. |
|value |Any |Yes |/ |/ |Specify a field value. |
|mode |String |No |overwrite |* Overwrite<br><br>* fill |Specify the processing logic used when the specified field does not exist.<br><br><br>* overwrite: performs overwriting.<br><br>* fill: sets the target field when it does not exist. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function adds a field `user_type` and a value normal to a log.

* Transformation rule:

   ```python
   f_set("user_type", "normal")
   ```
   

* Sample log:

   ```json
   {
       "name":"Elvin",
       "age":"22"
   }
   ```
   

* Transformation result:

   ```json
   {
       "name":"Elvin",
       "age":"22",
       "user_type":"normal"
   }
   ```
