---
title: "Type conversion functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/type_conversion_functions"
---

This topic describes the syntax and format of type conversion functions and offers sample scenarios.

<span id="ct-int-函数"></span>
## ct_int function

This function converts the numeral system of an integer value. The function can convert a base n value to a decimal result. You can specify an original base number from 2 through 36. The default base number is 10, and the returned result is a decimal number.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
ct_int(value,base=n)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |Number or String |Yes |/ |/ |Specify an expression. |
|base |Number |Yes |10 |2～36 |Specify the base number of the current value. |


<span id="函数示例"></span>
### Sample function

Example 1:


* Scenario: The function converts a base 2 number 1001 into a decimal result 9.

* Transformation rule:

   ```python
   f_set("binary2decimal",ct_int(v("binary"),base=2)
   ```
   

* Sample log:

   ```json
   {
     "binary": "1001"
   }
   ```
   

* Transformation result:

   ```json
   {
     "binary2decimal": "9",
     "binary": "1001"
   }
   ```
   


Example 2:


* Scenario: The function converts a value of the numeric type to the int type.

* Transformation rule:

   ```python
   f_set("int_value",ct_int(v("value"))
   ```
   

* Sample log:

   ```json
   {
     "value": "10"
   }
   ```
   

* Transformation result:

   ```json
   {
     "value": "10",
     "int_value": "10"
   }
   ```
   


<span id="ct-float-函数"></span>
## ct_float function

The function converts a value of an original data type to the floating point number data type.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
ct_float(value)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |Number or String |Yes |/ |/ |Specify a value or an expression to be converted. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function converts the speed value 60 of the integer data type to the floating point number data type.

* Transformation rule:

   ```python
   f_set("ct_float",ct_float(v("speed"))
   ```
   

* Sample log:

   ```json
   {
     "speed": "60"
   }
   ```
   

* Transformation result:

   ```json
   {
     "speed": "60",
     "ct_float": "60.0"
   }
   ```
   


<span id="ct-str-函数"></span>
## ct_str function

The function converts a value of an original data type to a string.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
ct_str(value)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |Number or Boolean type |Yes |/ |/ |Specify a value or an expression to be converted. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function converts the speed value 60 of the integer data type to the floating point number data type.

* Transformation rule:

   ```python
   f_set("ct_str",ct_str(v("price"))
   ```
   

* Sample log:

   ```json
   {
     "price": "100.0"
   }
   ```
   

* Transformation result:

   ```json
   {
     "price": "100.0",
     "ct_str": "100.0"
   }
   ```
   


<span id="ct-bool-函数"></span>
## ct_bool function

The function converts a value of an original data type to the Boolean type. The original type can be string, numeric, or Boolean.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
ct_bool(value)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |Any |Yes |/ |/ |Specify a value or an expression to be converted. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function gets the Boolean value of a number or string. If the number or string is not empty, true is returned.

* Transformation rule:

   ```python
   f_set("ct_bool",ct_bool(v("id"))
   ```
   

* Sample log:

   ```json
   {
     "id": "1997"
   }
   ```
   

* Transformation result:

   ```json
   {
     "id": "1997",
     "ct_bool": "true"
   }
   ```
