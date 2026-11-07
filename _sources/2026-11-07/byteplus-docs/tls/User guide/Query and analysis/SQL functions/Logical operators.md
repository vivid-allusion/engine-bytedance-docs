---
title: "Logical operators"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Logical-operators-2"
---

This topic introduces logical operators supported by Torch Log Service (TLS) and offers examples on how to use the operators.

<span id="Syntax description"></span>
## Syntax description

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">Logical operators have calculation priority. The following priority is used: NOT, AND, and OR. Alternatively, use parentheses (<code>()</code>) to change the calculation order.</div>


* <div data-tips="true" data-tips-type="tip">A logical operator supports Boolean expressions whose values are true, false, or null on both sides.</div>




|Operator |Description |
|---|---|
|AND |If both sides of the operator are true, the response is true. |
|OR |If either side of the operator is true, the response is true. |
|NOT |The NOT operator reverses the result of a subsequent condition that uses an operator. Examples: NOT BETWEEN and NOT IN. If the condition following NOT is false, the response is true. |


<span id="43cc5d26"></span>
## Examples


|Operator |Description |Sample SQL Statement |
|---|---|---|
|AND |If the value of the status field is 200 and the value of the method field is POST, true is returned. Otherwise, false is returned. |<PreCode lang="SQL" text={`* \| SELECT status=200 AND method='POST'`}\> |
|OR |The sample statement queries logs in which the values of the request_uri field end with access or accesslog. |<PreCode lang="SQL" text={`* \| SELECT * \nWHERE request_uri LIKE '%access' \nOR request_uri LIKE '%accesslog'`}\> |
|NOT |The sample statement queries the duration of requests whose status codes are not 500. |<PreCode lang="SQL" text={`* \| SELECT request_time WHERE NOT status=500`}\> |


<span id="a37c7045"></span>
## AND

If both sides of the operator are true, the response is true.

<span id="0494138b"></span>
### Syntax


* Syntax format

   ```SQL
   boolean_expression 1 AND boolean_expression 2 
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |boolean_expression |The value is of the Boolean type. |
   

* Return value description

   The return value is of the Boolean type.


<span id="929f3dce"></span>
### Example


* Scenario

   Count the request sizes for requests with a status of 200 and a method of GET.

* Query and analysis statement

   ```SQL
   *| SELECT ReqSize,Status, Method WHERE Status=200 AND Method='GET'
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/347a4205d1ac4ad9908acef394f7fcac~tplv-goo7wpa0wc-image.image) </span>


<span id="86c485d9"></span>
## OR

If either side of the operator is true, the response is true.

<span id="bc301be8"></span>
### Syntax


* Syntax format

   ```SQL
   boolean_expression 1 OR boolean_expression 2 
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |boolean_expression |The value is of the Boolean type. |
   

* Return value description

   The return value is of the Boolean type.


<span id="40fdbdb2"></span>
### Example


* Scenario

   Count the request sizes for requests where the status is 200 or the method is GET.

* Query and analysis statement

   ```SQL
   *| SELECT ReqSize,Status, Method WHERE Status=200 OR Method='GET'
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/cb91c6e1a5134a65a0d70e55822f5e38~tplv-goo7wpa0wc-image.image) </span>


<span id="01e162ec"></span>
## NOT

The NOT operator reverses the result of a subsequent condition that uses an operator.

<span id="bf3a7d95"></span>
### Syntax


* Syntax format

   ```SQL
   NOT boolean_expression
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |boolean_expression |The value is of the Boolean type. |
   

* Return value description

   The return value is of the Boolean type.


<span id="f8c08541"></span>
### Example


* Scenario

   Count the request sizes for requests where the status is not 200.

* Query and analysis statement

   ```SQL
   *| SELECT ReqSize,Status WHERE NOT Status=200
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/0bded3a57354426598a8545a78d05701~tplv-goo7wpa0wc-image.image) </span>


<span id="d682b010"></span>
## Truth table

The value of a Boolean expression can be true, false, or null. The corresponding truth table after logical operations is shown below.


|boolean_expression 1 |boolean_expression 2 |boolean_expression 1 AND boolean_expression 2 |boolean_expression 1 OR boolean_expression 2 |NOT boolean_expression 1 |
|---|---|---|---|---|
|true |true |true |true |false |
||false |false |true ||
||null |null |true ||
|false |true |false |true |true |
||false |false |false ||
||null |false |null ||
|null |true |null |true |null |
||false |false |null ||
||null |null |null ||
