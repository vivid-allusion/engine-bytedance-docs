---
title: "Comparison operators"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Comparison-operators-2"
---

Operators are reserved characters in the Torch Log Service (TLS). They are used to specify analysis conditions or connect multiple conditions in SQL analysis statements. If the condition is true, it returns true; otherwise, it returns false. This topic introduces the comparison operators supported by TLS and examples of operators in common scenarios.

<span id="a5cad578"></span>
## Operator list

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Comparison operators can be used for any comparable data types, such as long, double, and text.</div>


* <div data-tips="true" data-tips-type="tip">Comparison operators are usually used in conjunction with the WHERE syntax. For more information, please refer to <a href="https://docs.byteplus.com/docs/tls/WHERE-syntax-2">WHERE syntax</a>.</div>




|Operator |Syntax |Description |
|---|---|---|
|Relational Operator |x = y |Determines whether the values on both sides of the operator are equal, and if so, the condition is true and returns true. |
||x <\> y |Determines whether the values on both sides of the operator are equal. If not, the condition is true and returns true. |
||x \> y |Determines whether the value on the left side of the operator is greater than the value on the right side of the operator, and if so, the condition is true and returns true. |
||x < y |Determines whether the value on the left side of the operator is less than the value on the right side of the operator. If so, the condition is true and returns true. |
||x \>= y |Determines whether the value on the left side of the operator is greater than or equal to the value on the right side of the operator, and if so, the condition is true and returns true. |
||x <= y |Determines whether the value on the left side of the operator is less than or equal to the value on the right side of the operator. If so, the condition is true and returns true. |
|BETWEEN AND |x BETWEEN y AND z |Determines whether x is in the range `[y, z]`, and if so, the condition is true and returns true. |
|IN |x IN (value1,value2...) |Determines whether x is in the `(value1, value2...)`list, and if so, the condition is true and returns true. |
|IS DISTINCT FROM |x IS DISTINCT FROM y |Determine whether x and y are not equal. Returns true if x and y are not equal, or if one of them is null. |
|IS NOT DISTINCT FROM |x IS NOT DISTINCT FROM y |Determine whether x and y are equal. Returns true if x and y are equal, or both are null. Returns false if x and y are not equal, or if one of them is null. |
|IS NULL |x IS NULL |Determine whether x is a NULL value. If it is NULL, the condition is true and return true. |
|IS NOT NULL |x IS NOT NULL |Determine whether x is a NULL value. If not, the condition is true and return true. |
|LIKE |x LIKE pattern |Determines whether x matches the pattern, and if so, the condition is true and returns true. |
|NOT IN |x NOT IN (value1,value2...) |Determines whether x is in the `(value1, value2...)`list, if not, the condition is true and returns true. |


<span id="f6e06a8c"></span>
## Relational Operator

The relational operator is used to compare the size of the values on either side of the operator. If the condition is true, return true.

<span id="d7caf05d"></span>
### Syntax


* Syntax format

   
   |Operator |Description |
   |---|---|
   |x = y |Determines whether the values of two operands are equal. If so, the condition is true. |
   |x <\> y |Determines whether the values of two operands are equal. If they are not equal, the condition is true. |
   |x \> y |Determines whether the value of the left\-side operand is greater than that of the right\-side operand. If so, the condition is true. |
   |x < y |Determines whether the value of the left\-side operand is less than the value of the right\-side operand. If so, the condition is true. |
   |x \>= y |Determines whether the value of the left\-side operand is greater than or equal to the value of the right\-side operand. If so, the condition is true. |
   |x <= y |Determines whether the value of the left\-side operand is less than or equal to the value of the right\-side operand. If so, the condition is true. |
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |A field or an expression. The value can be any data type. |
   |y |A field or an expression. The value can be any data type. |
   

* Return value type

   The return value is of boolean type.


<span id="fc723397"></span>
### Example


* Scenario

   Count the number of requests whose request status codes are greater than or equal to 400.

* Query and analysis statement

   ```SQL
   * | SELECT COUNT(*) AS num WHERE status >=400
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f44d6f34e1a64b97bb4b411a31fe70a6~tplv-goo7wpa0wc-image.image) </span>


<span id="653512e9"></span>
## BETWEEN AND

The BETWEEN AND operator is used to determine whether x is in the range [y, z], and if so, the condition is true and true will be returned.

<span id="eb71e84c"></span>
### Syntax


* Syntax format

   ```SQL
   x BETWEEN y AND z
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |A field or an expression. The value can be any data type. |
   |y |A field or an expression. The value can be any data type. |
   |z |A field or an expression. The value can be any data type. |
   

* return value type

   The return value is of boolean type.


<span id="f917c661"></span>
### Example


* Scenario

   Count the number of requests whose request status codes are between 200 and 299.

* Query and analysis statement

   ```SQL
   * | SELECT COUNT(*) AS num WHERE status BETWEEN 200 AND 299
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/88e07b538cbf4bdf907dd92cdd61b15b~tplv-goo7wpa0wc-image.image) </span>


<span id="7e7a3049"></span>
## IN

The IN operator is used to determine whether x is in the list of `(value1, value2...)`. If it is, the condition is true and true will be returned..

<span id="b3d50f12"></span>
### Syntax


* Syntax format

   ```SQL
   x IN (value1,value2...)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |A field or an expression. The value can be any data type. |
   |(value1,value2...) |The List. The elements in the list are case\-sensitive. |
   

* return value type

   The return value is of boolean type.


<span id="2c46c96d"></span>
### Example


* Scenario

   Query the value of the `Method` field and determine whether the value is in the list of `('POST', 'PUT', 'DELETE')`.

* Query and analysis statement

   ```SQL
   * | SELECT Method, Method IN ('POST','PUT','DELETE')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2f0f85b63ab94996807ce0f52c877db6~tplv-goo7wpa0wc-image.image) </span>


<span id="b4cde0ee"></span>
## IS DISTINCT FROM

The IS NOT DISTINCT FROM operator is used to determine whether x and y are equal. If x and y are equal, or both are null, it returns true. If x and y are not equal, or one of them is null, it returns false.

<span id="82f9abaa"></span>
### Syntax


* Syntax format

   ```SQL
   x IS DISTINCT FROM y
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |A field or an expression. The value can be any data type. |
   |y |A field or an expression. The value can be any data type. |
   

* return value type

   The return value is of boolean type.


<span id="d025e405"></span>
### Example


* Scenario

   Determines whether the value of the `status` field is 200. If it is 200, it returns false.

* Query and analysis statement

   ```SQL
   * | SELECT status IS DISTINCT FROM 200
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df8afb2c55804f23ae2ace4943c265a0~tplv-goo7wpa0wc-image.image) </span>


<span id="76fe550a"></span>
## IS NOT DISTINCT FROM

The IS NOT DISTINCT FROM operator is used to determine whether x and y are equal. If x and y are equal, or both are null, it returns true. If x and y are not equal, or one of them is null, it returns false.

<span id="a502760d"></span>
### Syntax


* Syntax format

   ```SQL
   x IS NOT DISTINCT FROM y
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |A field or an expression. The value can be any data type. |
   |y |A field or an expression. The value can be any data type. |
   

* return value type

   The return value is of boolean type.


<span id="c8d54a57"></span>
### Example


* Scenario

   Determine whether the value of the `status` field is null. If it is not null, return false.

* Query and analysis statement

   ```SQL
   * | SELECT status IS NOT DISTINCT FROM null
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/df8afb2c55804f23ae2ace4943c265a0~tplv-goo7wpa0wc-image.image) </span>


<span id="fa6465aa"></span>
## IS NULL

The IS NULL operator is used to determine whether x is a NULL value. If it is NULL, the condition is true and true is returned.

<span id="e6d13796"></span>
### Syntax


* Syntax format

   ```SQL
   x IS NULL
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |A field or an expression. The value can be any data type. |
   

* return value type

   The return value is of boolean type.


<span id="4778093f"></span>
### Example


* Scenario

   Determine whether the value of the Method field is NULL. If it is not NULL, return false.

* Query and analysis statement

   ```SQL
   * | SELECT Method IS NULL
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/920fb59473874f369464bc1c12f4892f~tplv-goo7wpa0wc-image.image) </span>


<span id="8919d12c"></span>
## IS NOT NULL

The IS NOT NULL operator is used to determine whether the value of x is a NULL value. If it is not NULL, the condition is true and true is returned.

<span id="847c1265"></span>
### Syntax


* Syntax format

   ```SQL
   x IS NOT NULL
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |A field or an expression. The value can be any data type. |
   

* return value type

   The return value is of boolean type.


<span id="402a2267"></span>
### Example


* Scenario

   Determine whether the value of the `Method` field is NULL. If it is not NULL, return true.

* Query and analysis statement

   ```SQL
   * | SELECT Method IS NOT NULL
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f7a8c526977b4971946dbac51b59e601~tplv-goo7wpa0wc-image.image) </span>


<span id="e639f84f"></span>
## LIKE

The LIKE operator is used to determine whether x matches the pattern. If it does, the condition is true and true is returned.

<span id="9b8496a6"></span>
### Syntax


* Syntax format

   ```SQL
   x LIKE pattern
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |A field or an expression. The value can be any data type. |
   |pattern |The specified character pattern supports strings and wildcards `% _`. Among them, characters are case\-sensitive.<br><br><br>* Percent sign (%): represents zero, one, or multiple characters.<br><br>* Underscore (_): represents a single character. |
   

* return value type

   The return value is of boolean type.


<span id="e22a9740"></span>
### Example


* Scenario

   Determine whether the value of the `Action` field contains the string `Log`. If it does, return true.

* Log sample

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b13b1ed1eafa44ed8eeedf35e07db759~tplv-goo7wpa0wc-image.image) </span>

* Query and analysis statement

   ```SQL
   * | SELECT action like '%Log%'
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/402b74de1973497294e2471093ec11a6~tplv-goo7wpa0wc-image.image) </span>


<span id="f4314997"></span>
## NOT IN

The NOT IN operator is used to determine whether x is in the list of `(value1, value2...)`. If it is not, the condition is true and true will be returned.

<span id="52ea449a"></span>
### Syntax


* Syntax format

   ```SQL
   x NOT IN (value1,value2...)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |A field or an expression. The value can be any data type. |
   |(value1,value2...) |The list. The elements in the list are case\-sensitive. |
   

* return value type

   The return value is of boolean type.


<span id="285f035a"></span>
### Example


* Scenario

   Count the number of requests that are not `POST`, `PUT`, or `DELETE` requests.

* Query and analysis statement

   ```SQL
   * | SELECT COUNT(*) WHERE Method NOT IN ('POST','PUT','DELETE')
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/391c69202a2e4c91ae5eed0d424c17dc~tplv-goo7wpa0wc-image.image) </span>


<span id="63db2b21"></span>
## Appendix

The differences among the operators `=`, `<>`, `IS DISTINCT FROM`, and `IS NOT DISTINCT FROM` are shown in the following table.

When using the `=` and `<>` operators, if one of the numbers is null, the result returned will also be null.

When using the `IS DISTINCT FROM` and `IS NOT DISTINCT FROM` operators, they support comparing data containing null values and returning definite false or true results.


|x |y |x=y |x<\>y |*x* IS DISTINCT FROM \*\*\*\* *y* |*x* IS NOT DISTINCT FROM \*\*\*\* *y* |
|---|---|---|---|---|---|
|0 |0 |true |false |false |true |
|0 |1 |false |true |true |false |
|0 |null |null |null |true |false |
|null |null |null |null |false |true |
