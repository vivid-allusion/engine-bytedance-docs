---
title: "Arithmetic expression functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/arithmetic_expression_functions"
---

This topic describes the syntax and format of arithmetic expression functions and offers sample scenarios.

<span id="op-add-函数"></span>
## op_add function

This function accumulates or calculates the sum of multiple values. The values can be strings or numeric values. If you specify different values for this function, make sure the values have the same data type. Supported values for calculation: The values of the Integer data type can range from \-2^52+1 through 2^52\-1, and the values of the floating point number data type can range from \-1.8e308 through 1.8e308.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_add(value1,value2)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value1 |Number or String |Yes |/ |/ |Specify a value to be calculated. |
|value2 |Number or String |Yes |/ |/ |Specify a value to be calculated. |


<span id="函数示例"></span>
### Sample function

Example 1:


* Scenario: In a scenario the scores of a student in Chinese, Mathematics, and English are known, the function calculates the sum of the scores.

* Transformation rule:

   ```python
   f_set("total",op_add(v("math"),v("chinese"),v("english")))
   ```
   

* Sample log:

   ```json
   {
     "math": 96,
     "chinese": 98,
     "total": 274
   }
   ```
   

* Transformation result:

   ```json
   {
     "math": 96,
     "chinese": 98,
     "total": 274,
     "english": 80
   }
   ```
   


Example 2:


* Scenario: The function concatenates a detailed address based on the street, county, city, and province.

* Transformation rule:

   ```python
   f_set("address",op_add("address:",v("province"),v("city"),v("town"),v("detail")))
   ```
   

* Sample log:

   ```json
   {
     "province": "Sichuan Province",
     "city": "Chengdu City",
     "town": "Wuhou District",
     "detail": "231 Wuhouci Street"
   }
   ```
   

* Transformation result:

   ```json
   {
     "province": "Sichuan Province",
     "city": "Chengdu City",
     "town": "Wuhou District",
     "detail": "231 Wuhouci Street",
     "address": "Address: 231 Wuhouci Street, Wuhou District, Chengdu City, Sichuan Province."
   }
   ```
   


<span id="op-sub-函数"></span>
## op_sub function

This function performs a subtraction operation. The function returns the difference between value1 and value2.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_sub(value1,value2)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value1 |Number |Yes |/ |/ |Specify a value to be calculated. |
|value2 |Number |Yes |/ |/ |Specify a value to be calculated. |


<span id="函数示例"></span>
### Sample function


* Scenario: The total number of employees is 100, and 48 employees are male. The function calculates the number of female employees.

* Transformation rule:

   ```python
   f_set("female",op_sub(v("total"),v("man")))
   ```
   

* Sample log:

   ```json
   {
     "total": 100,
     "female": 52
   }
   ```
   

* Transformation result:

   ```json
   {
     "total": 100,
     "female": 52,
     "man": 48
   }
   ```
   


<span id="op-mul-函数"></span>
## op_mul function

The function performs a multiplication operation. The function returns the product of value1 and value2.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_mul(value1,value2)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value1 |Number |Yes |/ |/ |Specify a value to be calculated. |
|value2 |Number |Yes |/ |/ |Specify a value to be calculated. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function calculates the distance by multiplying speed by time.

* Transformation rule:

   ```python
   f_set("distance",op_mul(v("speed"),v("time")))
   ```
   

* Sample log:

   ```json
   {
     "speed": 60,
     "time": 8
   }
   ```
   

* Transformation result:

   ```json
   {
     "distance": 480,
     "speed": 60,
     "time": 8
   }
   ```
   


<span id="op-div-函数"></span>
## op_div function

The function performs a division operation. The function return the quotient of dividing value1 by value2. The divisor value2 cannot be 0.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_add(value1,value2)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value1 |Number |Yes |/ |/ |Specify a value to be calculated. |
|value2 |Number |Yes |/ |/ |Specify a value to be calculated. |


<span id="函数示例"></span>
### Sample function


* Scenario: The function calculates the costs of each person by dividing total costs by the number of persons.

* Transformation rule:

   ```python
   f_set("avg_cost",op_mul(v("cost"),v("people")))
   ```
   

* Sample log:

   ```json
   {
     "cost": 1500,
     "avg_cost": 150
   }
   ```
   

* Transformation result:

   ```json
   {
     "cost": 1500,
     "avg_cost": 150,
     "people": 10
   }
   ```
   


<span id="op-sum-函数"></span>
## op_sum function

The function performs an addition operation. The function returns the sum of value1 and value2. In this function, value is variable. This means the function can calculate the sum of multiple values.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_sum(value1,value2...)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value1 |Number |Yes |/ |/ |Specify a value to be added. |
|value2 |Number |Yes |/ |/ |Specify a value to be added. |


<span id="函数示例"></span>
### Sample function


* Scenario: In a bill, the storage fee is 150, the traffic fee is 100, and the search fee is 200. The total fee of 450 is calculated based on these fees.

* Transformation rule:

   ```python
   f_set("total_cost",op_sum(v("storage_cost"),v("flow_cost"),v("search_cost")))
   ```
   

* Sample log:

   ```json
   {
     "storage_cost": 150,
     "flow_cost": 100,
     "total_cost": 450
   }
   ```
   

* Transformation result:

   ```json
   {
     "storage_cost": 150,
     "flow_cost": 100,
     "total_cost": 450,
     "search_cost": 200
   }
   ```
   


<span id="op-mod-函数"></span>
## op_mod function

The function calculates a remainder. The function returns the remainder obtained after dividing value1 by value2.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_add(value1,value2)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value1 |Number |Yes |/ |/ |Specify a dividend. |
|value2 |Number |Yes |/ |/ |Specify a divisor. |


<span id="函数示例"></span>
### Sample function


* Scenario: Assume that a total of 10 servings of afternoon tea are prepared and 3 servings are offered to each person. In this case, the function gets the remainder 1 after calculation.

* Transformation rule:

   ```python
   f_set("remand",op_sum(v("total"),v("avg")))
   ```
   

* Sample log:

   ```json
   {
     "total": 10,
     "remand": 1
   }
   ```
   

* Transformation result:

   ```json
   {
     "total": 10,
     "remand": 1,
     "avg": 3
   }
   ```
   


<span id="op-null-函数"></span>
## op_null function

The function determines whether the value of a field is empty. The function returns a boolean value. If the value is empty and the None keyword, the function returns true. Otherwise, the function returns false.

<span id="函数语法-格式"></span>
### Function syntax and format

```python
op_null(value)
```


The following table describes the parameters.


|Parameter |Type |Required |Default Value |Value Range |Description |
|---|---|---|---|---|---|
|value |Number |Yes |/ |/ |Specify a value to be determined. |


<span id="函数示例"></span>
### Sample function

Example 1:


* Scenario: The None keyword is empty.

* Transformation rule:

   ```python
   f_set("op_null",op_null(None))
   ```
   

* Sample log:

   ```json
   {
     "region_id": 1,
     "region": "beijing"
   }
   ```
   

* Transformation result:

   ```json
   {
     "region_id": 1,
     "op_null": "true",
     "region": "beijing"
   }
   ```
   


Example 2:


* Scenario: The field `region` is not empty.

* Transformation rule:

   ```python
   f_set("region_null",op_null(v("region"))
   ```
   

* Sample log:

   ```json
   {
     "region_id": 1,
     "region": "beijing"
   }
   ```
   

* Transformation result:

   ```json
   {
     "region_id": 1,
     "op_null": "true",
     "region": "beijing"
   }
   ```
