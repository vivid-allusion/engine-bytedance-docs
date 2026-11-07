---
title: "Flow control functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/flow_control_functions"
---

This topic describes the syntax and formats of flow control functions and offers sample scenarios.

<span id="c-if-函数"></span>
## c_if function

This function transforms logs that meet the specified requirements.


* Make sure: 1. You set conditions and operations as function parameters in pairs. 2. At least 1 condition and 1 operation meet the requirements.

* If multiple true conditions exist among the parameters, only the operation corresponding to the first true condition is executed.


<span id="函数语法-格式"></span>
### Function syntax and format

```python
c_if(condition1, operation1, condition2, operation2, ...)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|condition |Any |Yes |/ |/ |Expression or expression combination. If this parameter is not of the Boolean type, the system determines the value after the data type is converted to Boolean. |
|operation |Global processing functions |Yes |/ |/ |Global processing function or combination of this function type. |


<span id="函数示例"></span>
### Sample function


* Scenario: If the field `phone` exists in a log, the function adds the field `contact_type`.

* Transformation rule:

   ```python
   c_if(f_has("phone"), f_set("contact_type", "telephone"))
   ```
   

* Sample log:

   ```json
   [
       {
           "user_name":"Smith",
           "phone":"135xxxx5678"
       },
       {
           "user_name":"Paul",
           "city":"chengdu"
       }
   ]
   ```
   

* Transformation result:

   ```json
   [
       {
           "user_name":"Smith",
           "phone":"135xxxx5678",
           "contact_type":"telephone"
       },
       {
           "user_name":"Paul",
           "city":"chengdu"
       }
   ]
   ```
   

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The field <code>phone</code> exists in the first log, and the field <code>contact_type</code> is added after transformation. The field <code>phone</code> does not exist in the second log, and the field <code>phone</code> is not added after transformation.   </div>
   

<span id="c-if-else-函数"></span>
## c_if_else function

This function performs different logical processing after it determines whether the condition is true. If the specified condition is true, operation1 is performed. Otherwise, operation2 is performed.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
c_if_else(condition, operation1, operation2)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value range |Description |
|---|---|---|---|---|---|
|condition |Any |Yes |/ |/ |Expression or expression combination. If this parameter is not of the Boolean type, the system determines the value after the data type is converted to Boolean. |
|operation1 |Global processing functions |Yes |/ |/ |Global processing function or combination of this function type. |
|operation2 |Global processing functions |Yes |/ |/ |Global processing function or combination of this function type. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function determines whether a user is an adult based on the field `age`, then outputs the result to the new field `is_adult`.

* Transformation rule:

   ```python
   c_if_else(op_ge(v("age"), 18), f_set("is_adult", True), f_set("is_adult", False))
   ```
   

* Sample log:

   ```json
   [
       {
           "name":"Agatha",
           "age":"20"
       },
       {
           "name":"Elvin",
           "age":"17"
       }
   ]
   ```
   

* Transformation result:

   ```json
   [
       {
           "name":"Agatha",
           "age":"20",
           "is_adult":true
       },
       {
           "name":"Elvin",
           "age":"17",
           "is_adult":false
       }
   ]
   ```
   


<span id="c-switch-函数"></span>
## c_switch function

This function performs different logical processing after it determines whether the condition is true. This function performs the operation corresponding to the first true condition among multiple conditions. If all conditions are not met, the function performs the default operation.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
c_switch(condition1, operation1, condition2, operation2, ..., default=default operation)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value range |Description |
|---|---|---|---|---|---|
|condition |Any |Yes |/ |/ |Expression or expression combination. If this parameter is not of the Boolean type, the system determines the value after the data type is converted to Boolean. |
|operation |Global processing functions |Yes |/ |/ |Global processing function or combination of this function type. |
|default |Global processing functions |Yes |/ |/ |Default operation. Global processing function or combination of this function type. |


<span id="函数示例"></span>
### Sample function


* Scenario: This function determines the Region based on the log field `city`.

* Transformation rule:

   ```python
   c_switch(op_eq(v("city"), "chengdu"), f_set("region", "West"), op_eq(v("city"), "shanghai"), f_set("region", "East"))
   ```
   

* Sample log:

   ```json
   [
       {
           "name":"Agatha",
           "city":"chengdu"
       },
       {
           "name":"Elvin",
           "city":"shanghai"
       }
   ]
   ```
   

* Transformation result:

   ```json
   [
       {
           "name":"Agatha",
           "city":"chengdu",
           "region":"West"
       },
       {
           "name":"Elvin",
           "city":"shanghai",
           "region":"East"
       }
   ]
   ```
   


<span id="c-compose-函数"></span>
## c_compose function

This function is used to combine multiple operations. Set global processing functions as the operations.


* Torch Log Service (TLS) calls the specified operations in sequence. In addition, TLS transfers the log, converts the log, and returns the processed log data.

* If a global operation deletes a log data entry, TLS does not perform subsequent operations on the entry.


<span id="函数语法-格式"></span>
### Function syntax and format

```python
c_compose(operation1, operation2...)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value range |Description |
|---|---|---|---|---|---|
|operation |Global processing functions |Yes |/ |/ |Global processing functions or combination of this function type. |


<span id="函数示例"></span>
### Sample function


* Scenario: If the field `content` is included in a log, TLS updates its value to value1 and renames the field content `content_modified`.

* Transformation rule:

   ```python
   c_if(f_has("content"),c_compose(f_set("content","value1"),f_rename("content","content_modified")))
   ```
   

* Sample log:

   ```json
   {
       "content":"value"
   }
   ```
   

* Transformation result:

   ```json
   {
       "content_modified":"value1"
   }
   ```
