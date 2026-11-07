---
title: "Mathematical statistics functions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Mathematical-statistics-functions-2"
---

This topic describes the syntax of a mathematical statistics function supported by Torch Log Service (TLS) and offers examples on how to use the function.

<span id="bfdfc967"></span>
### List of functions

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To use strings in SQL analysis statements of TLS, enclose the strings in single quotation marks ( ' ' ). Strings that are not enclosed or enclosed in double quotation marks ( " " ) indicate field names or column names. For example, <code>'time'</code> indicates a string, while <code>time</code> or <code>"time"</code> indicates a field or column name.</div>



|Function |Function Syntax |Description |
|---|---|---|
|BETA_CDF |BETA_CDF(α, β, v) |Calculates the cumulative probability that the random variable is less than v given the parameters α and β. |
|CORR |CORR(KEY1, KEY2) |Calculates the correlation between two sets of values. |
|COVAR_POP |COVAR_POP(KEY1, KEY2) |Calculates the overall covariance of two sets of values. |
|COVAR_SAMP |COVAR_SAMP(KEY1, KEY2) |Calculates the sample covariance of two sets of values. |
|INVERSE_NORMAL_CDF |INVERSE_NORMAL_CDF(x, y, p) |Calculates a value in the normal distribution based on a given cumulative probability p. |
|NORMAL_CDF |NORMAL_CDF(x, y, v) |Calculate the probability that a random variable in a normal distribution is less than or equal to a particular value v. |
|STDDEV |STDDEV(KEY) |Calculates the sample standard deviation of the values. |
|STDDEV_SAMP |STDDEV_SAMP(KEY) |Calculates the sample standard deviation of the values. |
|STDDEV_POP |STDDEV_POP(KEY) |Calculate the population standard deviation of the values. |
|VARIANCE |VARIANCE(KEY) |Calculates the sample variance of the values. |
|VAR_SAMP |VAR_SAMP(KEY) |Calculates the sample variance of the values. |
|VAR_POP |VAR_POP(KEY) |Calculates the population variance of the values. |


<span id="d097beb3"></span>
## BETA_CDF

BETA_CDF function is the cumulative distribution function (CDF) of the Beta distribution and is used to calculate the cumulative probability that the random variable is less than v given the parameters α and β.

<span id="c1c6c878"></span>
### Function syntax


* Syntax format

   ```SQL
   BETA_CDF(α, β, v)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |α |Beta distribution parameter, its value is of the double type, and the value is greater than 0. |
   |β |Beta distribution parameter, its value is of the double type, and the value is greater than 0. |
   |v |The input parameter of the cumulative distribution function, its value is of the double type, and the value range is `[0, 1]`. |
   

* Return value description

   The return value is of the double type.


<span id="986a7ba4"></span>
### Example


* Scenario

   In the Beta distribution with parameters (10 and 20), calculate the probability that the random variable is less than or equal to 0.5.

* Query and analysis statement

   ```SQL
   * | SELECT BETA_CDF(10, 20, 0.5) 
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/4e4fd4ce390f4597be0dae6a8d0f8aab~tplv-goo7wpa0wc-image.image) </span>


<span id="6ea226f5"></span>
## CORR

The CORR function is used to calculate the correlation between two sets of values. The higher the value returned, the higher the correlation between the two columns.

<span id="0460c143"></span>
### Function syntax


* Syntax format

   ```SQL
   CORR(KEY1, KEY2)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. |
   

* Return value description

   The return value is of the double type in the range [0, 1].


<span id="2815c23e"></span>
### Example


* Scenario

   Calculates the correlation between the `ReqTime`field value and the `ReqSize`field value.

* Query and analysis statement

   ```SQL
   * | SELECT CORR(ReqTime,ReqSize)
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/40a608a03b394fbdb7fe333d47561214~tplv-goo7wpa0wc-image.image) </span>


<span id="5b50a6be"></span>
## COVAR_POP

COVAR_POP function is used to calculate the overall covariance of two sets of values.

<span id="0925c655"></span>
### Function syntax


* Syntax format

   ```SQL
   COVAR_POP(KEY1, KEY2)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. |
   

* Return value description

   The return value is of double type .


<span id="c2496fc5"></span>
### Example


* Scenario

   Calculates the overall covariance of `ReqTime`and `ReqSize`.

* Query and analysis statement

   ```SQL
   *|SELECT COVAR_POP(ReqTime, ReqSize) AS "Population covariance"
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/83ea7c190fa340e993aac6a45ad6bcf6~tplv-goo7wpa0wc-image.image) </span>


<span id="e2c32954"></span>
## COVAR_SAMP

COVAR_SAMP function is used to calculate the sample covariance of two sets of values.

<span id="5b6396f2"></span>
### Function syntax


* Syntax format

   ```SQL
   COVAR_SAMP(KEY1, KEY2)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="9c305dab"></span>
### Example


* Scenario

   Calculate the sample covariance for ReqTime and ReqSize.

* Query and analysis statement

   ```SQL
   *|SELECT COVAR_SAMP(ReqTime, ReqSize) AS "Sample covariance"
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/713da4b2154e46f6b97d13ab3353c125~tplv-goo7wpa0wc-image.image) </span>


<span id="7a6b8fe8"></span>
## INVERSE_NORMAL_CDF

INVERSE_NORMAL_CDF function is the inverse of the normal cumulative distribution function, used to calculate a value in the normal distribution based on a given cumulative probability p.

<span id="62c556ef"></span>
### Function **syntax**


* Syntax format

   ```SQL
   INVERSE_NORMAL_CDF(x, y, p)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |*x* |The mean of the normal distribution, which is of the double type. |
   |y |The standard deviation of the normal distribution, which is of the double type, and the value is greater than 0. |
   |p |The probability value, which is of the double type, and the value is in the range (0, 1). |
   

* Return value description

   The return value is of the double type.


<span id="4c28740a"></span>
### Example


* Scenario

   In a normal distribution with a mean of 35 and a standard deviation of 6, calculate a value in that normal distribution based on a given cumulative probability of 0.046.

* Query and analysis statement

   ```SQL
   * | SELECT INVERSE_NORMAL_CDF(35, 6, 0.046) 
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/be9473f870634b75aec1c77995d1a962~tplv-goo7wpa0wc-image.image) </span>


<span id="40b1c7c6"></span>
## NORMAL_CDF

NORMAL_CDF function is used to calculate the probability that a random variable in a normal distribution is less than or equal to a particular value v.

<span id="ce6edd5f"></span>
### Function syntax


* Syntax format

   ```SQL
   NORMAL_CDF(x, y, v)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |x |The mean of the normal distribution, which is of the double type. |
   |y |The standard deviation of the normal distribution, which is of the double type, and the value is greater than 0. |
   |v |The input parameter of the cumulative distribution function, which is of the double type. |
   

* Return value description

   The return value is of the double type.


<span id="9503b461"></span>
### Example


* Scenario

   In a normal distribution with a mean of 20 and a standard deviation of 40, calculate the probability that a random variable is less than or equal to 60.

* Query and analysis statement

   ```SQL
   * | SELECT NORMAL_CDF(20, 40, 60) 
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/09466a56811440a3b8d7de1eac99f138~tplv-goo7wpa0wc-image.image) </span>


<span id="1d3deebc"></span>
## STDDEV

STDDEV function is used to calculate the sample standard deviation of the values.

<span id="a4eb82e0"></span>
### Function syntax


* Syntax format

   ```SQL
   STDDEV(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the bigint or double type. |
   

* Return value description

   The return value is of the double type.


<span id="d028d120"></span>
### Example


* Scenario

   Computes the sample standard deviation of ReqTime.

* Query and analysis statement

   ```SQL
   *|SELECT STDDEV(ReqTime) AS "Sample standard deviation"
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/623986f25ae149dba8d1b977610d041b~tplv-goo7wpa0wc-image.image) </span>


<span id="88e182f5"></span>
## STDDEV_SAMP

STDDEV_SAMP function is used to calculate the sample standard deviation of the values.

<span id="c69553c8"></span>
### Function syntax


* Syntax format

   ```SQL
   STDDEV_SAMP(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the bigint or double type. |
   

* Return value description

   The return value is of the double type.


<span id="201a7be5"></span>
### Example


* Scenario

   Computes the sample standard deviation of ReqTime.

* Query and analysis statement

   ```SQL
   *|SELECT STDDEV_SAMP(ReqTime) AS "Sample standard deviation"
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/d91d5a69636c443d9c6fd6c745af668d~tplv-goo7wpa0wc-image.image) </span>


<span id="76826619"></span>
## STDDEV_POP

STDDEV_POP function is used to calculate the population standard deviation of the values.

<span id="99726fcc"></span>
### Function syntax


* Syntax format

   ```SQL
   STDDEV_POP(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the bigint or double type. |
   

* Return value description

   The return value is of the double type.


<span id="9ca56823"></span>
### Example


* Scenario

   Calculates the population standard deviation of ReqTime.

* Query and analysis statement

   ```SQL
   *|SELECT STDDEV_POP(ReqTime) AS "population standard deviation"
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/5e0a150684be403d9cbb39101e9c3334~tplv-goo7wpa0wc-image.image) </span>


<span id="48d83940"></span>
## VARIANCE

VARIANCE function is used to calculate the sample variance of the values.

<span id="32df9750"></span>
### Function syntax


* Syntax format

   ```SQL
   VARIANCE(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the bigint or double type. |
   

* Return value description

   The return value is of the double type.


<span id="431394e5"></span>
### Example


* Scenario

   Calculates the sample variance of ReqTime.

* Query and analysis statement

   ```SQL
   *|SELECT VARIANCE(ReqTime) AS "Sample variance"
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f99d809bc3084be8a473db6e93dcca1a~tplv-goo7wpa0wc-image.image) </span>


<span id="5a3a3ddf"></span>
## VAR_SAMP

VAR_SAMP function is used to calculate the sample variance of the values.

<span id="d0e39e30"></span>
### Function syntax


* Syntax format

   ```SQL
   VAR_SAMP(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the bigint or double type. |
   

* Return value description

   The return value is of the double type.


<span id="9f5f791f"></span>
### Example


* Scenario

   Calculates the sample variance of ReqTime.

* Query and analysis statement

   ```SQL
   *|SELECT VAR_SAMP(ReqTime) AS "sample variance"
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1203a4018dbc45ae9a733d40402c4e0a~tplv-goo7wpa0wc-image.image) </span>


<span id="d2ba1949"></span>
## VAR_POP

VAR_POP function is used to calculate the population variance of the values.

<span id="5e826ea3"></span>
### Function syntax


* Syntax format

   ```SQL
   VAR_POP(KEY)
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |KEY |A field or an expression. Specify a value of the bigint or double type. |
   

* Return value description

   The return value is of the double type.


<span id="cdc09898"></span>
### Example


* Scenario

   Calculates the population variance of ReqTime.

* Query and analysis statement

   ```SQL
   *|SELECT VAR_POP(ReqTime) AS "population variance"
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/2d158c8adc74413d9ee0c343a98bfd25~tplv-goo7wpa0wc-image.image) </span>
