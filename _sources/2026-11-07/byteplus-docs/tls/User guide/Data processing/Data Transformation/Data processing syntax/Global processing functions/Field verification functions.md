---
title: "Field verification functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/field_verification_functions"
---

This topic describes the syntax and format of field verification functions and offers sample scenarios.

<span id="f-has-函数"></span>
## f_has function

This function judges whether a specified field exists.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
f_has(field)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|field |String |Yes |/ |/ |Specify the name of a field to be judged. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function judges whether the field`msg` exists in a log. If it exists, the function adds the field`status`.

* Transformation rule:

   ```python
   c_if(f_has("msg"), f_set("status", "200"))
   ```
   

* Sample log:

   ```json
   {
       "log-level":"INFO",
       "msg":"hello"
   }
   ```
   

* Transformation result:

   ```json
   {
       "log-level":"INFO",
       "msg":"hello",
       "status":"200"
   }
   ```
   


<span id="f-not-has-函数"></span>
## f_not_has function

This function judges whether a specified field does not exist.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
f_not_has(field)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|field |String |Yes |/ |/ |Specify the name of a field to be judged. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function judges whether the field `log-level` exists in a log. If it does not exist, the function adds the field`status`.

* Transformation rule:

   ```python
   c_if(f_not_has("log-level"), f_set("status", "400"))
   ```
   

* Sample log:

   ```json
   [
       {
           "log-level":"DEBUG",
           "msg":"hello"
       },
       {
           "msg":"world"
       }
   ]
   ```
   

* Transformation result:

   ```json
   [
       {
           "log-level":"DEBUG",
           "msg":"hello"
       },
       {
           "msg":"world",
           "status":"400"
       }
   ]
   ```
