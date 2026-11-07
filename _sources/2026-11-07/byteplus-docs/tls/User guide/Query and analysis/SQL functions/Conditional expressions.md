---
title: "Conditional expressions"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Conditional-expressions"
---

This topic introduces the conditional expressions supported by Torch Log Service(TLS) and examples of common scenarios.

<span id="861d1092"></span>
## List of conditional expressions


|Expression |Syntax |Description |
|---|---|---|
|CASE WHEN expression |```SQL```<br>```CASE WHEN condition1 THEN result1```<br>```    [WHEN condition2 THEN result2]```<br>```    ...```<br>```    [ELSE resultN]```<br>```END```<br> |Return different results based on different conditions, which can be used for data classification. |
|IF expression |```SQL```<br>```IF(condition, result)```<br> |If the condition is true, the result is returned; otherwise, null is returned. |
||```SQL```<br>```IF(condition, result1, result2)```<br> |If the condition is true, result1 is returned; otherwise, result2 is returned. |


<span id="290ddeac"></span>
## CASE WHEN expression

The CASE WHEN expression supports returning different results based on different conditions and can be used for data classification.

<span id="ceaae291"></span>
### Syntax


* Syntax format

   ```SQL
   CASE WHEN condition1 THEN result1
       [WHEN condition2 THEN result2]
       ...
       [ELSE resultN]
   END
   ```
   

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |condition |Conditional expression. |
   |THEN result |When the condition in the WHEN clause is true, return this result. |
   |ELSE result |When the condition in the WHEN clause is not true, return this result. |
   


<span id="e808e891"></span>
### Example


* Scenario

   Classify the request times through the CASE WHEN expression and calculate the number of requests in each category.

* Query and analysis statement

   ```SQL
   * |
   SELECT
     CASE
       WHEN ReqTime <= 500 then 'response fast'
       WHEN ReqTime BETWEEN 501 AND 5000 then 'response normal'
       ELSE 'response slow'
     END AS ReqTime,
     count(*) AS pv
   GROUP BY
     ReqTime
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/8381440cf1ff469ea2ebc04d80244bfd~tplv-goo7wpa0wc-image.image) </span>


<span id="06a95cdf"></span>
## IF expression

The IF expression is used to return results based on conditions. It is similar to the CASE WHEN expression.

<span id="4f2244a7"></span>
### Syntax


* Syntax format

   * If the condition is true, the result is returned; otherwise, null is returned.

      ```SQL
      IF(condition, result)
      ```
      

   * If the condition is true, result1 is returned; otherwise, result2 is returned.

      ```SQL
      IF(condition, result1, result2)
      ```
      

* Parameter description

   
   |Parameter |Description |
   |---|---|
   |condition |Conditional expression used for judgment. |
   |result |The returned result. |
   


<span id="13a052bc"></span>
### Example


* Scenario

   Classify request times with an IF expression and calculate the number of requests for each category.

* Query and analysis statement

   ```SQL
   * | SELECT IF(ReqTime > 100, 'abnormal', 'normal')  AS time, COUNT(*) AS pv GROUP BY time
   ```
   

* Query and analysis results

   <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/f8c6f64c0a7a442b98900a03acc092da~tplv-goo7wpa0wc-image.image) </span>
