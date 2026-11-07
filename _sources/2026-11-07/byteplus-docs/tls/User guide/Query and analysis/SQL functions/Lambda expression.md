---
title: "Lambda expression"
product: "Torch Log Service"
product_code: "tls"
source: "https://docs.byteplus.com/en/docs/tls/Lambda-expression"
---

It allows you to define Lambda expressions in SQL analysis statements and pass them to specified functions, thereby enhancing the functionality of the functions. This topic will introduce the basic syntax and examples of Lambda expressions.

<span id="acff2671"></span>
## Syntax

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Lambda expressions need to be used in combination with SQL functions, such as <a href="https://docs.byteplus.com/docs/tls/Array_functions#f88b951b">FILTER</a>, <a href="https://docs.byteplus.com/docs/tls/Array_functions#ed4126d8">REDUCE</a>, <a href="https://docs.byteplus.com/docs/tls/Array_functions#d07e1223">TRANSFORM</a> and <a href="https://docs.byteplus.com/docs/tls/Map-function#213d4842">MAP_FILTER</a>.</div>


```SQL
parameter -> expression
```



|Parameter |Description |
|---|---|
|parameter |Enter parameters, you can add multiple parameters, separated by English commas (,). |
|expression |An expression that operates on an input parameter.<br><br>```SQL```<br>```x -> x - 2```<br>```x -> x > 0```<br>```(x, y) -> x + y```<br>```x -> try_cast(x AS JSON)```<br>```x -> regexp_like(x, '\d+')```<br>```x -> if(x > 1, 'y', 'z')```<br> |


<span id="b8834285"></span>
## Example


* Example 1: Lambda expression `x - > x > 0`.

   * Scenario

      Combining the FILTER function with the Lambda expression `x - > x > 0`returns the elements greater than 0 in the array `[11, -3, null, 9, -8]`.

   * Query and analysis statement

      ```SQL
      * | SELECT FILTER(array[11,-3,null,9,-8],x -> x > 0)
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/1810b3ad58044838ad23c10ff0733cb9~tplv-goo7wpa0wc-image.image) </span>

* Example 2: Lambda expression `x - > x * 2`

   * Scenario

      Combining the TRANSFORM function with the Lambda expression `x - > x * 2`, multiplies the individual elements of the array `[99, 87, 16, 43, 25]` by 2, and returns the result of the evaluation.

   * Query and analysis statement

      ```SQL
      * | SELECT TRANSFORM(array[99,87,16,43,25],x -> x * 2) LIMIT 1
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/16fa3356e4864eadb7955a0f2bb1fc2f~tplv-goo7wpa0wc-image.image) </span>

* Example 3: Lambda expression `x - > regexp_like (x, '\ d +')`

   * scene

      Combining the TRANSFORM function with the Lambda expression `x - > regexp_like (x, '\ d +')` to determine whether each element in the array `['region', '010', 'name']` contains numbers, and return the judgment results.

   * Query and analysis statements

      ```SQL
      * | SELECT TRANSFORM(array['region','010','name'],x -> regexp_like(x, '\d+')) LIMIT 1
      ```
      

   * Query and analysis results

      <span>![图片](https://p9-arcosite.byteimg.com/tos-cn-i-goo7wpa0wc/b1bea76fbebf40758f14b3b698793284~tplv-goo7wpa0wc-image.image) </span>
