---
title: "Logical expression functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/logical_expression_functions"
---

This topic describes the syntax and format of logical expression functions and offers sample scenarios.

<span id="op-if-函数"></span>
## op_if function

This function returns an expression based on the determination result. If the condition is true, the value of the first expression is returned. If the condition is false, the value of the second expression is returned.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_if(condition,expression1,expression2)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|condition |Boolean |Yes |/ |/ |The result is a Boolean value or expression. |
|expression1 |Any |Yes |/ |/ |Specify an expression returned when your condition is true. |
|expression2 |Any |Yes |/ |/ |Specify an expression returned when the condition is false. |


<span id="函数示例"></span>
### Sample function

Example 1:


* Scenario: If the field `weather` is not empty, the function returns good day.

* Transformation rule:

   ```python
   f_set("op_if",op_if(v("weather"),"good day"，"bad day"))
   ```
   

* Sample log:

   ```json
   {
     "weather": "sunny"
   }
   ```
   

* Transformation result:

   ```json
   {
     "weather": "sunny",
     "op_if": "good day"
   }
   ```
   


Example 2:


* Scenario: If the condition is False, the function returns bad day.

* Transformation rule:

   ```python
   f_set("op_if",op_if(False,"good day"，"bad day"))
   ```
   

* Sample log:

   ```json
   {
     "weather": "sunny"
   }
   ```
   

* Transformation result:

   ```json
   {
     "weather": "sunny",
     "op_if": "bad day"
   }
   ```
   


<span id="op-and-函数"></span>
## op_and function

This function performs a logical AND operation. You can specify multiple conditions. When all conditions are true, True is returned.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_and(value1,value2...)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value1 |Any |Yes |/ |/ |Specify a value to be calculated. Non\-Boolean values are converted into Boolean values. For example, values of the string, numeric, dictionary, and list data types can be converted into Boolean values. If a value is not empty, the condition is true. Otherwise, the condition is false. |


<span id="函数示例"></span>
### Sample function

Example 1:


* Scenario: If fields `weather` and `date` are not empty, True is returned.

* Transformation rule:

   ```python
   f_set("op_and",op_and(v("weather"),v("date"))
   ```
   

* Sample log:

   ```json
   {
     "weather": "sunny",
     "date": "2000-08-09"
   }
   ```
   

* Transformation result:

   ```json
   {
     "weather": "sunny",
     "date": "2000-08-09",
     "op_and": "True"
   }
   ```
   


Example 2:


* Scenario: If fields `weather` and `date` are not empty while the field `location` is empty, False is returned.

* Transformation rule:

   ```python
   f_set("op_and",op_and(v("weather"),v("date"),v("location"))
   ```
   

* Sample log:

   ```json
   {
     "weather": "sunny",
     "date": "2000-08-09"
   }
   ```
   

* Transformation result:

   ```json
   {
     "weather": "sunny",
     "date": "2000-08-09",
     "op_and": "False"
   }
   ```
   


<span id="op-or-函数"></span>
## op_or function

This function performs a logical OR operation. This function performs a logical OR operation and allows you to change the parameters. If one or more conditions are true, True is returned. If all conditions are false, False is returned.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_or(value1,value2...)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |Any |Yes |/ |/ |Specify a value to be calculated. Non\-Boolean values are converted into Boolean values. For example, values of the string, numeric, dictionary, and list data types can be converted into Boolean values. If a value is not empty, the condition is true. Otherwise, the condition is false. |


<span id="函数示例"></span>
### Sample function

Example 1:


* Scenario: If one of the fields `weather` and `date` is not empty, True is returned.

* Transformation rule:

   ```python
   f_set("op_or",op_or(v("weather"),v("date"))
   ```
   

* Sample log:

   ```json
   {
     "weather": "sunny",
     "date": "2000-08-09"
   }
   ```
   

* Transformation result:

   ```json
   {
     "weather": "sunny",
     "date": "2000-08-09",
     "op_or": "True"
   }
   ```
   


Example 2:


* Scenario: If the fields `time` and `location` are empty, False is returned.

* Transformation rule:

   ```python
   f_set("op_or",op_or(v("time"),v("location"))
   ```
   

* Sample log:

   ```json
   {
     "weather": "sunny",
     "date": "2000-08-09"
   }
   ```
   

* Transformation result:

   ```json
   {
     "weather": "sunny",
     "date": "2000-08-09",
     "op_or": "False"
   }
   ```
   


<span id="op-not-函数"></span>
## op_not function

This function performs a logical NOT operation. If the result of value is true, False is returned. Otherwise, True is returned.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_not(value)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |Any |Yes |/ |/ |Specify a value to be calculated. Non\-Boolean values are converted into Boolean values. For example, values of the string, numeric, dictionary, and list data types can be converted into Boolean values. If a value is not empty, the condition is true. Otherwise, the condition is false. |


<span id="函数示例"></span>
### Sample function

Example 1:


* Scenario: If `weather` is not empty, False is returned.

* Transformation rule:

   ```python
   f_set("op_not",op_not(v("weather"))
   ```
   

* Sample log:

   ```json
   {
     "weather": "sunny",
     "date": "2000-08-09"
   }
   ```
   

* Transformation result:

   ```json
   {
     "weather": "sunny",
     "date": "2000-08-09",
     "op_not": "False"
   }
   ```
   


Example 2:


* Scenario: If the field `location` is empty, True is returned.

* Transformation rule:

   ```python
   f_set("op_not",op_not(v("location"))
   ```
   

* Sample log:

   ```json
   {
     "weather": "sunny",
     "date": "2000-08-09"
   }
   ```
   

* Transformation result:

   ```json
   {
     "weather": "sunny",
     "date": "2000-08-09",
     "op_or": "True"
   }
   ```
   


<span id="op-eq-函数"></span>
## op_eq function

This function performs a logical equal to operation. If the values of value1 and value2 are equal, True is returned. Otherwise, False is returned.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_eq(value1,value2)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |String or Number |Yes |/ |/ |Specify a value to be compared. |


<span id="函数示例"></span>
### Sample function

Example 1:


* Scenario: If the fields `weather` and `mind` are equal in their values, True is returned.

* Transformation rule:

   ```python
   f_set("op_eq",op_eq(v("weather"),v("mind"))
   ```
   

* Sample log:

   ```json
   {
     "weather": "sunny",
     "mind": "sunny"
   }
   ```
   

* Transformation result:

   ```json
   {
     "weather": "sunny",
     "mind": "sunny",
     "op_eq": "True"
   }
   ```
   


Example 2:


* Scenario: If the values of the fields `price` and `speed` are equal, True is returned.

* Transformation rule:

   ```python
   f_set("op_eq",op_eq(v("price"),v("speed"))
   ```
   

* Sample log:

   ```json
   {
     "price": "60",
     "speed": "60"
   }
   ```
   

* Transformation result:

   ```json
   {
     "price": "60",
     "speed": "60",
     "op_eq": "True"
   }
   ```
   


<span id="op-ge-函数"></span>
## op_ge function

This function performs a "greater than or equal to" operation. If value1 is greater than or equal to value2, True is returned. Otherwise, False is returned.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_gt(value1,value2)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value1 |Number |Yes |/ |/ |Specify a value to be compared. |
|value2 |Number |Yes |/ |/ |Specify a value to be compared. |


<span id="函数示例"></span>
### Sample function

Example 1:


* Scenario: If the value of speed is greater than the value of price, True is returned.

* Transformation rule:

   ```python
   f_set("op_ge",op_ge(v("speed"),v("price"))
   ```
   

* Sample log:

   ```json
   {
     "speed": "60",
     "price": "20",
     "op_ge": "True"
   }
   ```
   

* Transformation result:

   ```json
   {
     "speed": "60",
     "price": "20",
     "op_ge": "True"
   }
   ```
   


Example 2:


* Scenario: If the value of hour is less than the value of price, False is returned.

* Transformation rule:

   ```python
   f_set("op_ge",op_ge(v("hour"),v("price"))
   ```
   

* Sample log:

   ```json
   {
     "hour": "10",
     "price": "20"
   }
   ```
   

* Transformation result:

   ```json
   {
     "hour": "10",
     "price": "20",
     "op_ge": "False"
   }
   ```
   


<span id="op-gt-函数"></span>
## op_gt function

This function performs a "greater than" operation. If value1 is greater than value2, True is returned. Otherwise, False is returned.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_gt(value1,value2)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value1 |Number |Yes |/ |/ |Specify a value to be compared. |
|value2 |Number |Yes |/ |/ |Specify a value to be compared. |


<span id="函数示例"></span>
### Sample function

Example 1:


* Scenario: If the value of speed is greater than the value of price, True is returned.

* Transformation rule:

   ```python
   f_set("op_gt",op_gt(v("speed"),v("price"))
   ```
   

* Sample log:

   ```json
   {
     "speed": "60",
     "price": "20"
   }
   ```
   

* Transformation result:

   ```json
   {
     "speed": "60",
     "price": "20",
     "op_gt": "True"
   }
   ```
   


Example 2:


* Scenario: If the value of hour is less than the value of price, False is returned.

* Transformation rule:

   ```python
   f_set("op_gt",op_gt(v("hour"),v("price"))
   ```
   

* Sample log:

   ```json
   {
     "hour": "10",
     "price": "20"
   }
   ```
   

* Transformation result:

   ```json
   {
     "hour": "10",
     "price": "20",
     "op_gt": "False"
   }
   ```
   


<span id="op-le-函数"></span>
## op_le function

This function performs a "less than or equal to" operation. If the value of value1 is less than or equal to that of value2, True is returned. Otherwise, False is returned.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_le(value1,value2)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value1 |Number |Yes |/ |/ |Specify a value to be compared. |
|value2 |Number |Yes |/ |/ |Specify a value to be compared. |


<span id="函数示例"></span>
### Sample function


* Scenario: If the value of speed is greater than the value of price, False is returned.

* Transformation rule:

   ```python
   f_set("op_le",op_le(v("speed"),v("price"))
   ```
   

* Sample log:

   ```json
   {
     "speed": "60",
     "price": "20"
   }
   ```
   

* Transformation result:

   ```json
   {
     "speed": "60",
     "price": "20",
     "op_lt": "False"
   }
   ```
   


<span id="op-lt-函数"></span>
## op_lt function

This function performs a "less than" operation. If the value of value1 is less than that of value2, True is returned. Otherwise, False is returned.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_lt(value1,value2)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value1 |Number |Yes |/ |/ |Specify a value to be compared. |
|value2 |Number |Yes |/ |/ |Specify a value to be compared. |


<span id="函数示例"></span>
### Sample function


* Scenario: If the value of speed is greater than the value of price, False is returned.

* Transformation rule:

   ```python
   f_set("op_lt",op_lt(v("speed"),v("price"))
   ```
   

* Sample log:

   ```json
   {
     "speed": "60",
     "price": "20"
   }
   ```
   

* Transformation result:

   ```json
   {
     "speed": "60",
     "price": "20",
     "op_lt": "False"
   }
   ```
